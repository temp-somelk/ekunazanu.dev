+++
title = "Probabilistic Data Structures"
description = "Bloom Filters, Count-min Sketches and HyperLogLog."
date = 2024-09-28
draft = true
template = "article.html"
[extra]
type = "article"
thumbnail = "lab.die.svg"
thumbnailalt = "Die with five dots visible on its one square face."
+++

Probabilistic data structures are what their names suggest — these are [data structures](https://en.wikipedia.org/wiki/Data_structure) that give probabilisitic answers to queries. What is lost in [precision](https://en.wikipedia.org/wiki/Accuracy_and_precision#/media/File:Accuracy_and_precision.svg) is more than made up for in extremely efficient use of memory and/or computational resources.

## Hashing

A hash function is simply a mathematical function that maps an input to an output. In practice however, the output of hash functions have certain properties:

* **Deterministic** — Hash functions produce the same output for the same input.
* **Fixed Length** — For any input, most hash functions produce a fixed length output.
* **Pseudorandom** — Most hash functions produce a hash that is [pseudorandom](https://en.wikipedia.org/wiki/Pseudorandomness); hash outputs appear and behave random, but are ultimately deterministic.
* **One-Way** — For most hash functions, it is difficult to determine the input just from the output. This is useful for [cryptographic applications](https://en.wikipedia.org/wiki/Cryptographic_hash_function); this is not necessarily useful for probabilistic data structrues.
* **Collision Resistant** — Despite having fixed length ouputs, hash functions are designed to minimize cases where two inputs output the same hash. Collisions are not impossible however, because of the limited output space.

Some of these properties are immensely useful and form the basis of most probabilistic data structures.

<input placeholder="Enter some input"> <button>Hash</button><br>
hash("Hello"): <code>0x2D4</code>

## Bloom Filters

Bloom filters are one of the most popular probabilistic data structures, that are used to check for membership in sets or multisets. In simpler words, bloom filters are used to check if an element is present in a set or not. Bloom filters cannot identify if an element exists in a set with absolute certainty, but it can report with certainty if it does **not** exist in a set. And it does it for big datasets using very little space.

### Approaches

Rather than outright specifying how bloom filters work, it's more effective to discuss possible solutions first. It'll help build a natural intuition as to why bloom filters are a better approach — at least when accuracy is not a big priority.

Consider these elements:

![multiset](static)

We need to know if `Hello` is in the multiset. One possible solution is to store the entire multiset, and then performing a [linear search](https://en.wikipedia.org/wiki/Linear_search) — going through each element one-by-one and checking if it exists.

![linear search performed on multiset](animation)

Or if you've studied computer science, you can sort the multiset in [lexicographic order](https://en.wikipedia.org/wiki/Lexicographic_order) and then perform a [binary search](https://en.wikipedia.org/wiki/Binary_search_algorithm).

![binary search performed on ordered multiset](animation)

That makes querying faster, but we still need space to store all the elements. We can optimize on that front. Maybe you can start by storing only the (sorted) unique values and purging all the duplicates:

![binary search on ordered set](animation)

It's off to a decent start, but definitely very far from optimal. Second, maybe we can compress individual elements using some compressing strategy:

![binary search on ordered compressed set](animation)

But even then, the space required will still roughly scale linearly with the number of elements and the size of each element. Perhaps it's time to introduce some hashing functions to exploit some of the properties of hashes to solve our problem. We can maybe try hashing individual elements and storing only the unique hashes. Also, we'll need to search for `0x2E` instead — the hash for `Hello`.

![lookup hash on hash set/table](animation)

Using hashes is arguably better than storing long elements and somewhat better than storing compressed elements. But because most hashing functions always produce a fixed length number for any input, it can be exploited to exponentially decrease the amount of storage needed to store the hashes.

Consider the above example where the hash function produces an output between `0x00` and `0xFF`. In decimal, it is between `0` and `255`. Now instead of storing all the numbers individually, we can create a [bit-array](https://en.wikipedia.org/wiki/Bit_array) (with all bits initially set to zero), and just flip the bit corresponding to the hash to one. For example if the output hash is `0x5E` (`94` in decimal), the 94th bit is flipped to one. This is the analogous to storing the number itself, since we are only concerned whether the hash (and therefore the elements) exists.

![multiple hashes -> each hash inside boxes with unit memory boxes to emphasize multiple hashes memory units](static)

In the previous approach, multiple bits were needed to store individual hashes which unnecessarily wasted space.

However the new approach is much more compact, requiring only one bit per hash.

![one bitmap (represented with linear box memory unit thingy) with arrows from hash pointing to bits in the bit map. emphasis on one final bitmap](static)

And this is what a bloom filter is. It is fundamentally a bit-array, where a bit corresponds to an individual hash output — and that hash output is related to a corresponding element (or more elements) in a set. The only difference is multiple hash functions are used in bloom filters to minimize collisions.

### Querying

We discussed storing elements, but we glossed over the actual details of how to know if a queried element exists. Ultimately querying is similar to adding elements. The element is hashed, and then instead of flipping the corresponding bit in the bit-array to one, we instead check if the corresponding bit is one.

![add elements by hashing and then query elements by hashing](animation)


### Hash Collisions

While hash functions are designed to be collision resistant, they are not collision proof. Sometimes two elements may have the same hash (and if the input space — the number of elements — is bigger than the output space of the hash function, collisions are guaranteed due to the [pigeonhole principle](https://en.wikipedia.org/wiki/Pigeonhole_principle)). In such cases, an element that was added may have the same hash as a different element being queried, leading to a false positive.

For example, `Hello` has a hash `0x2E`, which is then added/updated in the bloom filter. Suppose we need to check membership for `Bye`, which has the same hash `0x2E`. Since the bit for `0x2E` in the bit-array is one, the bloom filter wrongly reports that `Bye` exists in the set.

![collision -> false positive](animation)

Multiple hash functions can also be used for each element. In that case, querying an element will return true only if **all** bits corresponding to the hashes are one.

![two hash functions; one same as above -> collision; the other different -> no collision; no false positive](animation)

The probability of two elements having the same hash outputs is `1/m` where `m` is the size of the bloom filter. However, if two hash functions are used for every element, the probability of two elements having the same hash outputs is roughly `1/m * 1/m`. In general, using more hashing functions exponentially decreases the probability that **all** the hash outputs of two elements will collide. Thus, using more hash functions results in lower false positives. This assumes the output of the hash functions are pretty randomly distributed and are not correlated to each other.

![collision using three hash functions -> no false positive, rare](animation)

However using too many hashing functions can also increase the false positive rate. It might feel counterintuitive, especially right after showing it *decreases* false positives, but consider this: The bloom filter is finite. The more the number of hash functions, the higher the probability that it fills up quickly and most bits are set to one. When querying from a bloom filter where most bits are set to one, the higher the probability that any query results in a positive — even if the element is not in the set.

![collision using 16 hash functions -> false positive](animation)

In the extreme case when all the bits in a bloom filter are set to one, the bloom filter would **always** report positive for membership — regardless of whether the element actually exists in the set.

Other than using a large number of hashing functions, a bloom filter can also be quickly saturated if the number elements to be hashed (added) is huge. Decreasing the number of hash functions will not help beyond a certain point — especially if we're already down to our last hashing function. The only way to decrease false positives then, is by increasing the size of the bloom filter itself. Increasing the size of the bloom filter bit-array equates to a larger output space for the hash functions, reducing the probability for collisions.

![smaller bit array on top and bigger bit array on bottom -> more false positive above](animation)

Thus the false positive rate is also dependent on the size of the bloom filter and the number of (unique) elements to be added.

### Space Efficiency

As seen above, the false positive rate depends on the number of hash functions used per element, the number of elements hashed/added, and the size of the bloom filter. Conversely, it can be said that the size of the bloom filter and the number of hash functions depend on the tolerance for false positives and the number elements to be added.

To be more specific, the [optimal size for a bloom filter](https://en.wikipedia.org/wiki/Bloom_filter#Optimal_number_of_hash_functions) is roughly `-2.08·ln(p)·n`, where `p` is the tolerance for the false positive rate and `n` is the number of unique elements one expects to observe. The [optimal number of hash functions](https://en.wikipedia.org/wiki/Bloom_filter#Optimal_number_of_hash_functions) is roughly `ln(2)·(m/n)`, where `m` is the size of the bloom filter and `n` is the number of expected elements. Thomas Hurst beautifully visualizes how the factors affect each other in his [bloom filter calculator](https://hur.st/bloomfilter/).

Here's a working example of a bloom filter that can store and query roughly \<n\> elements with 95% probability of being correct, before the false positive rate shoots up:

![working bloom filter. add an insert, query, and reset button.](interactive)

### Deletion

While deletion of elements in a bloom filter is technically possible, it introduces false negatives. Deletions can be achieved by unsetting the bits corresponding to the hash of the element to be deleted to zero. However, if one of the bits was previously set by a different element, then checking membership for that element would lead to a false negative.

![deletion collision -> false negative](animation)

The general consensus for bloom filters is to forbid deletions in exchange for removing the possibility of getting false negatives.

## Count-Min Sketch

A count-min sketch is a probabilisitc data structure that calculates the maximum occurences of elements in a set. It is what a bloom filter would have been if it was a frequency table instead.

### Counting Bloom Filter

Count-min sketches are very similar to bloom filters, so it's helpful to start off with a bloom filter.

```
.---+---+---+---+---+---+---+---.
| 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
'---+---+---+---+---+---+---+---'
```

A bloom filter is essentially just a bit-array. Now, instead of using one bit per hash, what if a few more bits per hash were used instead?

```
.-----+-----+-----+-----+-----+-----+-----+-----.
| 000 | 000 | 000 | 000 | 000 | 000 | 000 | 000 |
'-----+-----+-----+-----+-----+-----+-----+-----'
```

One way to utilize this new space is use it as 'counters' to store information about frequency, by incrementing it by one whenever a hash (and therefore, an element) is added. This expands its ability from just storing information about the **existence** of an element to instead storing information about its **frequency** as well.

<pre>
.---+---+---+---+---+---+---+---.
| 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
'---+---+---+---+---+---+---+---'
.-----+-----+-----+-----+-----+-----+-----+-----.
| 000 | 000 | 000 | 000 | 000 | 000 | 000 | 000 |
'-----+-----+-----+-----+-----+-----+-----+-----'

<input placeholder="Add element"> <button>Hash and add to set</button>
<input placeholder="Search element"> <button>Hash and query frequency</button>
</pre>

The array on top is a bloom filter, which helps us query membership; the one below that is a counting bloom filter which helps us query frequency information as well.

In the counting bloom filter, the counters for the corresponding hash of an element get incremented whenever an element is added. However the counters can [overflow](https://en.wikipedia.org/wiki/Integer_overflow) and reset back to zero, leading to wrong estimates. It is therefore necessary to approximate and assign an appropriate number of bits for each counter beforehand, to minimize errors. This isn't much of an issue though, since even thirty-two bits are enough to store values upto about four billion.

Querying involves hashing to find the counter address and then retrieivng the value stored in the counter — similar to bloom filters.

### Hash Collisions

The main way error seeps through in the counters is via hash collisions. Sometimes two elements will map to the same hash, increasing the count of the other element. This means elements can be over-counted. However there is no way for elements to be under-counted (barring overflows).

<pre>
.-----+-----+-----+-----+-----+-----+-----+-----.
| 000 | 000 | 000 | 000 | 000 | 000 | 000 | 000 |
'-----+-----+-----+-----+-----+-----+-----+-----'

Hash(A) = Hash(C)
<button>Add A to set</button> <button>Query frequency of A</button>
<button>Add B to set</button> <button>Query frequency of B</button>
<button>Add C to set</button> <button>Query frequency of C</button>
Actual frequency of A: 0
Actual frequency of B: 0
Actual frequency of C: 0
</pre>

When it comes to reducing errors, a similar approach to bloom filters is the first solution that comes to mind: By increasing the size of the array, and using multiple hash functions. The solutions might look plausible on the surface because of the counting bloom filter's similiarities to a bloom filter, but they need further investigation before concluding anything concrete.

The first solution is pretty easy to verify. Increasing the size of the array increases the output space of the hash functions, reducing collisions — regardless of the number of hashing functions used. The reasoning is similar to bloom filters, discussed above.

![smaller bit array on top and bigger bit array on bottom -> more false positive above; but with counters this time](animation)

Similar to bloom filters, when querying using multiple hash functions per element, the intersection of all the counters and using the minimum value of all the counters is used. Since collisions only cause elemented to be overcounted and there is no way for elements to be under-counted, the minimum value is the closest to the true frequency.

![multiple hash functions intersection](interactive)

It might seem that it using multiple hash functions would reduce errors similar to bloom filters. However when it comes to increasing the number of hash functions, it does not decrease errors — in fact it actually leads to slightly higher errors. Initially it can be difficult to deduce why.

![more hash functions -> more collisions, finite space](animation)

It's important to mention that in both bloom filters and counting bloom filters, increasing the number of hash functions per element increases the probability of a collision. But in the case of bloom filters, any hash collision did not change the value of a bit in the bloom filter itself — it would be set to one regardless. In fact hash collisions [decrease overall error](https://stackoverflow.com/a/72509014) by preventing the bloom filter from getting saturated too quickly.

![an element with multiple hash functions mapping to same output but does not change the value](interactive)

Compare that to a counting bloom filter, where every collision increases the value of the counter by one. In the case of a single hash function being used, a counter would get incremented by one. However if multiple hash functions are used, the probability when an element with multiple hash functions would map to the same counter is non-zero. Adding an element to the sketch would then increment the counter by more than one. And worse, the probability of over-counting an element only increases as the number of hash functions per element increases.

![an element with multiple hash functions mapping to same output and increments value](interactive)

The solution to reducing errors then would be to increase the size of the array and to stick to using a single hash function. And while that is fair, there are better ways to go about it.

### Separate Hash Ranges

There is an upside in using multiple hash functions — while querying the frequency of an element, it gets expenontially less probable that the **all** hashes of the elements will be the same as some other element. The downside is that adding an element using multiple hashes can lead to collisions, leading to increased over-counting.

A way to resolve the downside is by assigning the ouput of each hash function to separate output spaces — preventing over-counting of an element when it is added. This does not prevent over-counting completely though, since collisions from hashes of other elements are still possible.

![above collsions with counting bloom filter, down count min sketch](animation)

The resulting data structure is a count-min sketch. It can also be thought of as a two dimensional array with `w` columns and `d` rows — where `d` is the total number of hash functions and `w` is the output range for the hash outputs. Each hash function outputs to their respective row, and the hashes are [pairwise independent](https://en.wikipedia.org/wiki/Pairwise_independence) — the outputs are effectively random.

```
.-----+-----+-----+-----+-----+-----+-----+-----.
| 000 | 000 | 000 | 000 | 000 | 000 | 000 | 000 |
'-----+-----+-----+-----+-----+-----+-----+-----'
.-----+-----+-----+-----+-----+-----+-----+-----.
| 000 | 000 | 000 | 000 | 000 | 000 | 000 | 000 |
'-----+-----+-----+-----+-----+-----+-----+-----'
.-----+-----+-----+-----+-----+-----+-----+-----.
| 000 | 000 | 000 | 000 | 000 | 000 | 000 | 000 |
'-----+-----+-----+-----+-----+-----+-----+-----'
.-----+-----+-----+-----+-----+-----+-----+-----.
| 000 | 000 | 000 | 000 | 000 | 000 | 000 | 000 |
'-----+-----+-----+-----+-----+-----+-----+-----'
```

The count-min sketch is capable of answering more than simple point queries. It can also respond to [range and inner-product queries](https://cs.stanford.edu/~rishig/courses/ref/l12b.pdf).

### Space efficiency

Again, similar to bloom filters, the space required by a count-min depends on [the tolerance for error and the number of elements to be hashed](http://dimacs.rutgers.edu/~graham/pubs/papers/cmsoft.pdf). The optimal width of the array `w` is `2n/ε` and depth `d` is `log(δ)/log(1/2)` — where `n` is the number of elements, `ε` defines the bounds for frequency estimates, and `δ` is the probability the estimates exceeds those bounds.

## HyperLogLog

HyperLogLog is another probabilistic data structure, used to approximate the cardinality (total number) of distinct elements in a multiset. It uses hash functions as well, but unlike a bloom filter or a count-min sketch, it relies on the pseudorandomness of the output hashes as its basis to calculate the cardinality.

### Probability

To understand HyperLogLog, it would be useful to discuss probabilities first. The most classic example for calculating the probability of a random (unbiased) event is the flipping of a coin.

Consider this thought expirement: Take a few coins where each coin has an equal probability of landing on heads or tails and toss them all at once. The probability that the first coin is heads is half, or one in `2`. The probability that both the first and second coin are heads is one in `4`. The probability that all three first coins are heads is one in `8`. In general, for all the first `n` coins to be heads, the probability is one in `2^n`.

```
 ._.   ._.   ._.   ._.   ._.   ._.   ._.   ._.
| H | | H | | H | | H | | H | | H | | H | | H |
 '-'   '-'   '-'   '-'   '-'   '-'   '-'   '-'
 50% · 50% · 50% · 50% · 50% · 50% · 50% · 50%
'---25%---'    
'------12%------'
'---------6%----------'
'----------(...)------------'
```

Alternatively, we can say that we need to try tossing all the coins roughly `2^n` times to observe `n` consecutive heads at the beginning of the coin array.

<pre>
 ._.   ._.   ._.   ._.   ._.   ._.   ._.   ._.
| H | | H | | H | | H | | T | | H | | T | | T |  (Heads colored blue when counter updated)
 '-'   '-'   '-'   '-'   '-'   '-'   '-'   '-'
<span style="color: #912; font-weight: 800; font-size: 1rem;">18</span> tosses to get <span style="color: #129; font-weight: 800; font-size: 1rem;">4</span> consecutive heads
Total tosses: 21
<button>Toss</button> <button>Reset</button>
</pre>

Conversely, if shown `n` consecutive heads (occurring at the beginning), we can estimate that there were roughly `2^n` tosses to get there.

<pre>
 ._.   ._.   ._.   ._.   ._.   ._.   ._.   ._.
| H | | H | | H | | H | | T | | H | | T | | T | (Heads colored blue when counter updated)
 '-'   '-'   '-'   '-'   '-'   '-'   '-'   '-'
<span style="color: #129; font-weight: 800; font-size: 1rem;">4</span> consecutive heads suggests roughly <span style="color: #912; font-weight: 800; font-size: 1rem;">16</span> tosses
Actual tosses: <strong>21</strong>
<button>Toss</button> <button>Reset</button>
</pre>

The highest number of consecutive heads gives us an approximation about the number of times we tossed all the coins. Just storing that number is enough to give a rough estimate, instead of having to store all the individual tosses.

This is the fundamental principle behind HyperLogLog. Coins are replaced with bits — A hash function is chosen such that output is pseudorandom, with each of the output bits of the hash acting as an unbiased coin — having an equal probability of being `0` or `1`. Then, the total number of elements can be estimated by just storing the length of the longest run of consecutive zeroes of their hashes.

<pre>
<input placeholder="Enter some input"> <button>Hash</button> <button>Hash random element</button>
hash(1) = 00000101
+-------------------------------+
| <span style="color: #129; font-weight: 800; font-size: 16px;">0</span> | <span style="color: #129; font-weight: 800; font-size: 16px;">0</span> | <span style="color: #129; font-weight: 800; font-size: 16px;">0</span> | <span style="color: #129; font-weight: 800; font-size: 16px;">0</span> | <span style="color: #129; font-weight: 800; font-size: 16px;">0</span> | 1 | 0 | 1 |
+-------------------------------+
<span style="color: #129; font-weight: 800; font-size: 1rem;">5</span> consecutive 0s suggests roughly <span style="color: #912; font-weight: 800; font-size: 1rem">32</span> elements hashed.
Actual number of unique elements: 35
<button>Reset</button>
</pre>


As observed above (if you tried) — since hashes are deterministic, duplicate elements will yield the same hashes and would not affect the cardinality calculation. The longest run of consecutive zeroes gives an approximation about the number of hashes — and by extension, the number of distinct elements in a multiset.

### Weakness

There is a glaring flaw in this approach however. The gaps between the approximations double every time an extra consecutive zero is observed — it can only provide estimates that are powers of two, and nothing in between. Second, sometimes a hash output may have a lot of consecutive zeros at the beginning just out of sheer bad luck, leading to an estimate that is wildly off and above the true cardinality.

Instead of storing one counter that measures the longest run of zeroes for the entire multiset, multiple counters can be used that store the longest run of zeroes for different subsets of the multiset. The values are then averaged to find the cardinality estimate. This scales down both the above problems and improves the accuracy of the estimate to somewhat acceptable levels.

### Buckets

The way of segregating the data of a multiset into different subsets in HyperLogLog is to use '[buckets](https://en.wikipedia.org/wiki/Hash_table#/media/File:Hash_table_3_1_1_0_1_0_0_SP.svg)'. In the case of HyperLogLog, a bucket is just a container for storing the length of the longest run of zeroes of hashes for a particular subset of elements. The first `b` bits of the hash of an element are reserved to select which bucket to update the values, and the remaining hash is used to find the longest run of consecutive zeroes for that bucket.

<pre>
<input placeholder="Enter some input"> <button>Add</button> <button>Add random element</button>
hash(1) = 11000001
+-------------------------------+
| <span style="color: #192; font-weight: 800; font-size: 1rem;">1</span> | <span style="color: #192; font-weight: 800; font-size: 1rem;">0</span> | <span style="color: #129; font-weight: 800; font-size: 16px;">0</span> | <span style="color: #129; font-weight: 800; font-size: 1rem;">0</span> | 1 | 1 | 0 | 1 |
+-------------------------------+

<span style="color: #129; font-weight: 800; font-size: 1rem;">2</span> consecutive 0s observed.
Bucket <span style="color: #192; font-weight: 800">10</span> updated|not updated.

Buckets:
+---------------+
| 3 | 2 | 3 | 4 |           (Blue color number if updated)
+---------------+
<span style="color: #192;"> 00  01  10  11</span>
</pre>

Since each bucket stores the longest run of zeroes, calculating the cardinality involves calculating the estimates for each bucket and then finding their average using the [harmonic mean](https://en.wikipedia.org/wiki/Harmonic_mean). The harmonic mean is used in particular to reduce the influence the large outliers from affecting the estimate.

<pre>
Buckets:
+---------------+
| 3 | 2 | 3 | 4 |
+---------------+

<button>Calculate cardinality</button>

Cardinality estimate of bucket <span style="color: #192;">00</span>: <span style="color: #912; font-weight: 800;">8</span>
Cardinality estimate of bucket <span style="color: #192;">01</span>: <span style="color: #912; font-weight: 800;">4</span>
Cardinality estimate of bucket <span style="color: #192;">10</span>: <span style="color: #912; font-weight: 800;">8</span>
Cardinality estimate of bucket <span style="color: #192;">11</span>: <span style="color: #912; font-weight: 800;">16</span>

Harmonic mean of all the estimates: 7
Actual number of unique elements: 6
<button>Reset</button>
</pre>

### Scaling and Discarding

Despite using multiple counters and using the harmonic mean to prevent overestimating the cardinality, the estimate is still higher than the true cardinality. [Researches have discovered](https://research.google/pubs/hyperloglog-in-practice-algorithmic-engineering-of-a-state-of-the-art-cardinality-estimation-algorithm/) that by discarding the largest 30% of the values in the buckets before averaging, the estimate can be made much more accurate.

Another thing intentionally glossed over earlier to keep things neater is the correction factor. Even before separating estimates into buckets and discarding the largest values, and then using the harmonic mean to get smaller estimates, we could've done something much simpler — very simple, in fact. The simplest way to scale down the estimates is to, well, scale it down. There is a predictable [bias](https://www.moderndescartes.com/essays/hyperloglog/#loglog) towards the larger estimates, and scaling the final estimate by a correction factor that ranges from `0.673` to `0.709` can get smaller estimates that are much closer to the true cardinality value.

All of these things combined brings down the error rate to `1.04/√m`, where `m` is the number of buckets.

This in all is HyperLogLog. In summary, adding elements involves hashing them and storing their longest run of leading zeroes in buckets. And to calculate the approximate cardinality, the harmonic mean of the smallest 70% of values is taken and then scaled by a correction factor. 

<pre>
<input placeholder="Enter some input"> <button>Add</button> <button>Add random element</button>
hash(1) = 11000001
+---------------------------------------------------------------+
| <span style="color: #192; font-weight: 800; font-size: 1rem;">1</span> | <span style="color: #192; font-weight: 800; font-size: 1rem;">0</span> | <span style="color: #192; font-weight: 800; font-size: 1rem;">1</span> | <span style="color: #129; font-weight: 800; font-size: 16px;">0</span> | <span style="color: #129; font-weight: 800; font-size: 1rem;">0</span> | 1 | 1 | 0 | 1 | 0 | 0 | 1 | 0 | 1 | 1 | 0 |
+---------------------------------------------------------------+

<span style="color: #129; font-weight: 800; font-size: 1rem;">2</span> consecutive 0s observed.
Bucket <span style="color: #192; font-weight: 800">101</span> updated|not updated.

Buckets:
+-------------------------------+
| 4 | 2 | 4 | 4 | 3 | 2 | 1 | 5 |               (Blue color number if updated)
+-------------------------------+

<button>Calculate cardinality</button>

Cardinality estimate of bucket <span style="color: #192;">000</span>: <span style="color: #912; font-weight: 800;">16</span>
Cardinality estimate of bucket <span style="color: #192;">001</span>: <span style="color: #912; font-weight: 800;">4</span>
Cardinality estimate of bucket <span style="color: #192;">010</span>: <span style="color: #912; font-weight: 800;">16</span>
Cardinality estimate of bucket <span style="color: #192;">011</span>: <span style="color: #912; font-weight: 800;">16</span>
Cardinality estimate of bucket <span style="color: #192;">100</span>: <span style="color: #912; font-weight: 800;">8</span>
Cardinality estimate of bucket <span style="color: #192;">101</span>: <span style="color: #912; font-weight: 800;">4</span>
Cardinality estimate of bucket <span style="color: #192;">110</span>: <span style="color: #912; font-weight: 800;">2</span>
Cardinality estimate of bucket <span style="color: #192;">111</span>: <span style="color: #912; font-weight: 800;">32</span>

Harmonic mean of 70% of the smallest estimates: 6
Estimate after being scaled by the correction factor: 5

Final cardinality estimate: 5

Actual number of unique elements: 6

<button>Reset</button>
</pre>

It is less acccurate when the number of elements are low, and steadily becomes more accurate as the cardinality grows.

### Space Efficiency

The only thing needed (to store) for calculating the cardinality are the buckets. So the total amount of space required is the number of buckets times the size of each bucket. The number of buckets depends on the degree of accuracy required — the error rate is inversely proportional to the sqaure root of quantity of buckets. More buckets lead to more accurate estimates and vice versa.

The largest number than can be stored in each bucket (before they overflow) depends on the number of bits assigned for each bucket. A five-bit bucket can store values from 0 to 31. A hash with 31 leading zeroes in a hash suggests roughly 2.1 billion unique elements were hashed. Hence, to store cardinalities of up to 2.1 billion unique elements, the size of each bucket needs to be only 5 bits. In general, to store cardinality of `n` unique elements, the size of each bucket needs to be `log(log(n))` bits. That's also where its name comes from.

![level1 (top) -> five bits; level1.5 -> number n represented by level1; level2 (middle) -> string of n zeroes; level2.5 -> mumber represented by n zeroes; level3 -> roughly 2^n unique elements](static)

For example, HyperLogLog is able to estimate cardinalities of more than a billion unique elements with an an error of 2% using 2500 five-bit buckets — only 1.5 kB of memory. Or alternatively, just 0.25 kB for an error of 5% using 400 buckets.

## Other Data Structures

There are lots of other probabilistic data structures that trade accuracy for efficiency. In addition to bloom filters, both [cuckoo filters](https://en.wikipedia.org/wiki/Cuckoo_filter) or [quotient filers](https://en.wikipedia.org/wiki/Quotient_filter) are useful probabilistic data structures used for membership queries. Or [linear counting](https://doi.org/10.1145/78922.78925), which is used for estimating distinct elements, but the underlying principle is similar to bloom filters. Rank can be approximated using [t-digests](https://doi.org/10.48550/arXiv.1902.04023), or [KLL sketches](https://doi.org/10.48550/arXiv.1603.05346), and similarities can be estimated using [LSH](https://en.wikipedia.org/wiki/Locality-sensitive_hashing), [MinHash](https://en.wikipedia.org/wiki/MinHash), and [SimHash](https://doi.org/10.1145/509907.509965). There's a lot of other resources online to know more about the different kinds of probabilisitc data structures that exist.

---

## References

* Florian Hartmann: [Bloom Filters](https://florian.github.io/bloom-filters/)
* Eric Crahen: [Count-Min Sketching, Configuration & Point-Queries](https://crahen.github.io/algorithm/stream/count-min-sketch-point-query.html)
* Engineering at Meta: [HyperLogLog in Presto: A significantly faster way to handle cardinality estimation](https://engineering.fb.com/2018/12/13/data-infrastructure/hyperloglog/)
* Cheng-Wei Hu: [HyperLogLog: A Simple but Powerful Algorithm for Data Scientists](https://chengweihu.com/hyperloglog/)

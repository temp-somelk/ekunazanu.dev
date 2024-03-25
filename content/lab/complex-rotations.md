+++
title = "Complex Rotations"
description = "Building intuition for imaginary numbers and rotations."
date = 2024-06-10
draft = true
template = "article.html"
[extra]
type = "article"
thumbnail = "lab.rotation.svg"
thumbnailalt = "Two lines of unit length on the XY plane surrounded by a unit circle."
+++

In mathematics there are multiple ways to represent the same underlying principles or ideas. There are different ways to represent two dimensional spaces — the [cartesian](https://en.wikipedia.org/wiki/Cartesian_coordinate_system), [polar](https://en.wikipedia.org/wiki/Polar_coordinate_system) and [other](https://en.wikipedia.org/wiki/Category:Two-dimensional_coordinate_systems) coordinate systems; and multiple ways to morph that space. Complex numbers are a way to represent two dimensional spaces, and are an even more elegant way to represent two dimensional rotations.

## Real Numbers

This a real number line:

![integer number line](static)

It can be thought of as a one dimensional space — where any real number `x` is a point on the space with distance `x` from the origin point, zero. Positive numbers are on the right, and negative numbers on the left.

Since any real number is a point on this space, the output of any operation that results in a real number will also be a point on the one dimensional space. For example, addition and multiplication are very common functions that can take real numbers as inputs and then produce real numbers as outputs — both the input and output can be mapped on the real number line.

![number line, with addition output a number, mapped to the number line represented using an arrow or something](static/animated)

Consider Addtion: If a point/number is taken and an addend `d` is added to it, and then the sum would lie `d` distance to the right or left from the original point on the number line, depending on the sign. Since this is true for all points/numbers, it can be thought of as the entire number line **shifting** by a distance specified by the addend `d`.

![number line](static/interactiveD)

To keep things simple, one point is emphasized — zero. It's important to keep in mind that the entire number line is getting shifted.

![morphing number line with numbers above, (show original number line in the background with muted colors numbers below) - input: addends - highlight 0; shift numline by (multiple) addends](interactive)
<input placeholder="Enter value to add"> <button>Add</button>

Multiplication morphs the number by scaling, or **stretching** the number line by the amount specified by the multiplier, and the new point with respect to the old coodinates gives us the result of the multiplication transformation. Multiplying with a negative value flips the number line.

![morphing number line with numbers above, (show original number line in the background with numbers below) - input: multipliers - highlight 1; shift numline by (multiple) multipliers](interactive)
<input placeholder="Enter value to multiply"> <button>Multiply</button>

Similar to addition and multiplication, finding the visual trasnformation analogues on a number line for the square and square root function should not be that hard, since squaring a number invloves multiplication; and finding its square root is just the inverse function of the square.

Squaring a number involves multiplying it by itself — stretching the number line twice by the same magnitude.

![morphing number line with numbers above, (show original number line in the background with numbers below) - input: base; highlight 1; stretch numline by base twice after some delay](interactive)
<input placeholder="Enter value to square"> <button>Square</button>

Unfortunately, visualizing the square root function to a simple number line morph is trickier. Alternatively we can define the square root function using the square function. Luckily, that's just enough for our purpose. The root shall be defined as the number which, when performed the square transformation, results in the input number.

![morphing number line with numbers above, (show original number line in the background with numbers below)  - input: root; highlight square and 1; stretch numline by root twice such that root overlaps with square. when overlapping, it is the square root](interactive)
<input placeholder="Enter value to square"> <button>Square</button>

There is a problem with this definition however. It is impossible to find the square root of negative numbers. No matter which numbers are taken, the final output of the square function is always mapped to a non-negative number — making it impossible to find a number that maps to a negative value.

![morphing number line with numbers above, (show original number line in the background with numbers below) - input: root; highlight negative square and 1; stretch numline by root twice such that root tries to overlap with square. never overlap](interactive)
<input placeholder="Enter value to square"> <button>Square</button>

## Imaginary Numbers

Suppose such numbers do exist, then it becomes a challenge on how to place those numbers on the number line. This is where it helps to make certain assumptions.

* **Assumption I**: Since the square root of negative numbers could not be mapped on the real number line, they must lie on a completely different number line. Rather aptly, the square roots of negative numbers will also be referred to as imaginary numbers from now on.

![real number line above and imaginary number line below](static)

* **Assumption II**: The square root of any negative numbers (imaginary numbers) can derived using the square root of negative one and scaling it with a **real number**. Square root of negative one shall be denoted as `i`. So an imaginary number can be represented as `b·i`, where `b` is a real number. The real and imaginary numbers together shall be described as a sum `a+bi`, where `a` and `b` are real numbers and `i` is the square root of negative one.

![real number line above and imaginary number line below with a sum sign in the middle](static)

* **Assumption III**: Addition is defined as `(a+bi) + (c+di)` = `(a+c) + (b+d)i`; ie. both operate on their own respective real and imaginary components. Multiplication is defined as `(a+bi) · (c+di)` = `a·c + a·i + bi·c + bi·di` or simplified, `(ac-bd) + (ad+bc)i` ie. multiplication is distruted over addition.

The assumptions lead to the following insights:
* Addition affects their own component and has no effect on the other entity.
* Since any imaginary number can be thought of as root of negative one scaled up by a real number, **multiplying a real with any imaginary number results in a (scaled) imaginary number** as well. That is, `b · i` = `bi`.
* Multiplying an imaginary number with an imaginary number can be thought of as multiplying their scalars and multiplying their roots of negative one. Squaring the root of negative one is negative one, thus **multiplying two imaginary numbers results in a (scaled) negative real number**. That is, `bi · di` can be rewritten as `b·d · i·i` = `bd · -1` = `-bd`.
* Multiplying two numbers with both non-zero real and imaginary components results in a number that is the product of the two numbers, following the rules of distributive multiplication over addition.

It is difficult to visualize what multiplication of numbers with both non-zero real and imaginary numbers does to the number lines for now, and will be discussed later. However, addition and multiplication with either only a real component or an imaginary component is relatively easier to vizualize. Geometerically:

* Addition with real numbers shifts the real number line.
* Addition with imaginary numbers shifts the imaginary number line.
* Multiplication with real numbers stretches the real number line as well as the imaginary number lines.
* Multiplication with imaginary numbers morphs number lines such that:
    * If the number (line) was on the real number line, it now exists on the imaginary number line.
    * If the number (line) was on the imaginary number line, it now exists on the flipped real number line.

![real number line above and imaginary number line below; swap real and imaginary number lines when multiplied by i. labels and background lines stay in position](interactive)
Real: <input> <button>Add</button> <button>Multiply</button><br>
Imag: <input> <button>Add</button> <button>Multiply</button>

These assumptions, constraints and the resulting visual transforms might seem arbitrary at first, but the motivation behind it starts making sense when we expand into the second dimension.

## Complex Plane

The pattern when multiplying by `i` might not seem obvious by looking at the above number line transforms. To spot a pattern in the results, we'll restrict the multiplications operations on the number line to only multiplications with `i`.

![real number line above and imaginary number line below; swap real and imaginary number lines when multiplied by i. labels and background lines stay in position](interactive)
Real: <input> <button>Add</button><br>
Imag: <input> <button>Add</button><br>
<button>Multiply by i</button>

The pattern is more evident now — the real and imaginary number lines get swapped, and the real number line gets flipped. But its relavance is still unclear. For that, take any point on a cartesian plane and keep track of its `x` and `y` axes when it is rotated counter clockwise:

![plane on top with bottom: x line above and y line below; swap real and imaginary number lines when rotated by a. labels and background lines stay in position](interactive)
<input> <button>Set X</button><br>
<input> <button>Set Y</button><br>
<button>Rotate</button>

The behaviour of the `x` and `y` axes is same as the behaviour of real and imaginary number lines when multiplied by `i`. If th

The key takeaway from this subsection is that if the real and imaginary number lines are perpendicular to each other, then multiplication with `i`, results in a 90° counter clockwise rotation of the plane. Now the question arises — can multiplication rotate the plane by some other angle?

## Generalizing for Other Angles

![Getting to -1 in 2 steps](/media/geogebra-export(2).png)

From $(2 + 5i) \\cdot (-1) = (-2 - 5i)$ and $(2 + 5i) \\cdot n \\cdot n = (-2 - 5i)$, we can deduce that $n \\cdot n = -1$, or $n = i$. And multiplying $(2 + 5i)$ by $i$ does indeed give a product, in this case $(-5 + 2i)$, which is a 90° counter clockwise rotation of the original point. Sweet.

We can go even further. What if we took four steps to get to $-1$? In that case we would end up with $n \\cdot n \\cdot n \\cdot n = -1$. Intution tells us that if it took 4 steps to get to $-1$ or a 180° rotation, each one of the steps would equate to a 45° rotation.

![Getting to -1 in 4 steps](/media/geogebra-export(1).png)

Coming back to the expression, $n \\cdot n \\cdot n \\cdot n = -1$, if we simplify it, we get $n = \\sqrt{i}$. And it makes sense if you think about it. If multiplying by $-1$ rotates the point by 180° and multiplying by $\\sqrt{-1}$ or $i$ rotates that point by 90°, it would seem logical that multiplying by $\\sqrt{\\sqrt{-1}}$ or $\\sqrt{i}$ would result in a 45° rotation. But what in world does $\\sqrt{i}$ even mean? We defined $\\sqrt{-1}$ to be i, but how do we define $\\sqrt{i}$ ? Do we have to now again define what $\\sqrt{i}$ would mean? What about for 22.5° rotations? Do we have to define $\\sqrt{\\sqrt{i}}$ as well? Luckily we don't have to. Turns out we can describe $\\sqrt{i}$ and other angles using $i$ itself.

Let us assume there is a complex number $(a + bi) = \\sqrt{i}$, **where $a$ and $b$ are real numbers**.

$$
\\implies (a + bi)^{2} = i \\\\
\\implies a^{2} - b^{2} + 2abi = i
$$

Comparing the real components,
$$
\\implies  a^{2} - b^{2} = 0 \\longrightarrow I \\\\
\\implies a = \\pm b \\\\
$$

Comparing the imaginary components,

$$
\\implies 2ab = 1 \\\\
\\implies b = \\tfrac{1}{2a}\\ or\\ a = \\tfrac{1}{2b} \\\\
$$

Now, substituting values of $a$ from $I$,

$$
\\implies b = \\tfrac{1}{\\pm 2 b} \\\\
\\implies b^{2} = \\pm \\tfrac{1}{2}
$$

But we assumed $b$ is real ($b$ is real, $bi$ is imaginary), hence

$$
\\implies b^{2} = \\tfrac{1}{2} \\\\
\\implies b = \\tfrac{1}{\\sqrt{2}} \\\\
Similarly,\\ a = \\tfrac{1}{\\sqrt{2}} \\\\
$$

Thus, we end up with:

$$
\\sqrt{i} = (a + bi) = \\left(\\frac{1}{\\sqrt{2}} + \\frac{1}{\\sqrt{2}}i \\right)
$$

So by our logic, if we multiply any complex number by $\\sqrt{i}$ or $\\left( \\frac{1}{\\sqrt{2}} + \\frac{1}{\\sqrt{2}}i \\right)$, we must get a point that is rotated by 45°. Let's try it with the complex number, $2 + 5i$ :

$$
(2 + 5i) \\cdot \\left(\\tfrac{1}{\\sqrt{2}} + \\tfrac{1}{\\sqrt{2}} i \\right) \\\\
= \\left(2 \\cdot \\tfrac{1}{\\sqrt{2}} + 2 \\cdot \\tfrac{1}{\\sqrt{2}}i \\right) + \\left( 5i \\cdot \\tfrac{1}{\\sqrt{2}} + 5i \\cdot \\tfrac{1}{\\sqrt{2}}i \\right) \\\\
= \\left( \\tfrac{2}{\\sqrt{2}} + \\tfrac{2}{\\sqrt{2}}i \\right) + \\left( \\tfrac{5}{\\sqrt{2}}i - \\tfrac{5}{\\sqrt{2}} \\right) \\\\
= \\left( - \\tfrac{3}{\\sqrt{2}} + \\tfrac{7}{\\sqrt{2}} i \\right) \\\\
$$

![2 + 5i rotated 45°](/media/geogebra-export(6).png)

And sure enough, the point $\\left( - \\frac{3}{\\sqrt{2}} + \\frac{7}{\\sqrt{2}} i \\right)$ lies where $(2 + 5i)$ would have landed if it was rotated 45° with respect to the origin.

Similary getting to $-1$ and $i$ in three steps, or $\\sqrt[3]{-1}$ and $\\sqrt[3]{i}$ should correspond to 60° and 30° rotations respectively.

![Getting to -1 in 3 steps](/media/geogebra-export(8).png)

![Getting to i in 3 steps](/media/geogebra-export(7).png)

Solving for $(a + bi) = -1^{3}$, we get $\\sqrt[3]{-1} = \\left( \\frac{1}{2} + \\frac{\\sqrt{3}}{2} i \\right)$. We, of course, also get $(-1 + 0i)$ as a solution, but we'll ignore that since it doesnt help us to represent 60° rotations. But if you are curious as to how the solution $-1$ would map out geometrically, think of it as rotating the plane thrice by 180°. First, we multiply by $-1$ to rotate it 180°, and then multiply it again by $-1$ (which is the same as multiplying by $1$), we rotate a total of 360° and get back the same position. We multiply a final third time to again end up at the 180° rotated position. $(-1 + 0i)$ is indeed a valid solution, but it's not important for us. We just take the solution $\\left( \\frac{1}{2} + \\frac{\\sqrt{3}}{2} i \\right)$ for our case. Similarly, for $i$ we get $\\sqrt[3]{i} = \\left( \\frac{\\sqrt{3}}{2} + \\frac{1}{2} i \\right)$. You can verify it, but multiplying a complex number by the above values does indeed rotate the plane by 60° and 30°.


By now, we can recognize that multiplying any complex number with another complex number that makes an angle $\\alpha$ with the origin rotates the plane by a by that angle, and that the angle is determined by the ratio of the real and imaginary component. To be precise, $\\theta = \\tan^{-1} \\left( \\frac{b}{a} \\right)$ for a complex number $(a + bi)$.

![$\\tan \\left( \\theta \\right) = b/a$](/media/geogebra-export(10).png)

## Explanation

To reason about why complex multiplication has the effect of rotating the plane, it helps to analyze how the real and imaginary components of the resultant number change with respect to the input complex numbers. Assuming two complex numbers `a+bi` and `c+di`, their product is `ac-bd + (ad+bc)i`. The real component of the resultant product is `ac-bd` and the imaginary component is `ad+bc`.

For the real component, `ac` signifies that the real components of the resultant is affected the product of the real components of the input numbers. This should make sense, since it is the same as normal multiplication of real numbers. However, it also gets subtracted by `bd` — the product of the imaginary components. One way to think about it is if the imaginary components increases compared to the real components, their arguments increase as well. As the arguement of a complex number increases, its projection on the real number line shrinks.

If `b` and `d` are sufficiently bigger than `a` and `c` — both numbers would have an combined argument greater than π/2, and the real component becomes negative. This is consistent with the fact that if `bd > ac` then `ac - bd < 0`.

![a,b,c,d sliders -> output value of real component and projection of product of two complex numbers on real axis. show two input numbers as well, but using muted colors](interactive)

The resultant number also has an imaginary component, `ad+bc`. These numbers suggest that the imaginary component is depedent on the real component of one number and the imaginary component of the other. To help build an intuition, `b` and `c`, are kept fixed for now. Then, `a` can be thought of as determining the magnitude of the first number, while `d` can be thought of as determining the argument of the other number. Multiplying them implies in a ways that the magnitude of the first number gets rotated by the argument of the second number. As either of the magnitude or argument gets bigger, the resultant's projection on the imaginary axis gets bigger.

A similar argument can be made for `bc` — the magnitude of the second number gets rotated by the argument of the first number.

![a,d sliders -> output value of imaginary component and projection of product of two complex (b,c are fixed, or separate single-same slider for both) numbers on imaginary axis. show two input numbers as well, but using muted colors](interactive)

These are only useful to build an initial intuition, and are in no way complete, and are not at all precise.

### Trigonometric Proof

To be more rigorous, some knowledge about trigonometry is required. Let us assume the same two complex numbers, but this time represented using magnitudes `z1` and `z2`, with arguments `α` and `β` respectively. The components can then be represented as:

`a = z1·cos(α)`\
`b = z1·sin(α)`\
`c = z2·cos(β)`\
`d = z2·sin(β)`

![two complex numbers as two points -> sliders for alpha,beta, z1, z2](interactive)

Multiplying the complex numbers `a+bi` and `c+di` would then result in:

`+ z1·z2·cos(α)·cos(β)`\
`- z1·z2·sin(α)·sin(β)`\
`+ z1·z2·cos(α)·sin(β)·i`\
`+ z1·z2·sin(α)·cos(β)·i`

If the magnitudes are factored out, then we get:

`cos(α)·cos(β) - sin(α)·sin(β)` as the real component\
`cos(α)·sin(β) + sin(α)·cos(β)` as the imaginary component.

Using [basic trigometric identities](https://en.wikipedia.org/wiki/List_of_trigonometric_identities#Angle_sum_and_difference_identities), it can be deduced that resultant product will have a real component `cos(α+β)` and imaginary component `sin(α+β)`. It is easily evident that the argument of the resultant number will be `α+β`.

![cos(alpha+beta) and sin(alpha+beta) coordinates and argument alpha+beta](interactive)

And if the magnitudes are factored back in as well, the final result is `z1·z2 · (cos(α+β) + sin(α+β)i)`. So, the magnitude is the product of the individual magnitudes of the inputs.

**Rewrite (or delete this) after finishing main artcile:** Thus, it can be said that multiplying with a complex number has the effect of applying a stretching the complex plane by its magnitude, and also rotating the complex plane by its argument.

## Purpose

It can be argued that two dimensional rotations can also be described using vectors and [rotational matrices](https://en.wikipedia.org/wiki/Rotation_matrix), and that it is considerably more powerful since it is not restricted to two dimensions. It is true — complex numbers are relatively limited and are not strictly necessary.

**Rewrite after finishing main article:** But the beauty of the complex plane shines in the [Euler's Formula](https://en.wikipedia.org/wiki/Euler%27s_formula). The Euler's formula states that `exp(α·i) = cos(α) + isin(α)`. It means when an imaginary number, the result is always a complex number having magnutude one and argument, well, the argument. Exponentials have the property `exp(a+b) = exp(a)·exp(b)`.

For . This means. Although it could be done without the use of complex numbers, using them makes it a lot simpler and elegant.

In [pure mathematics](https://en.wikipedia.org/wiki/Pure_mathematics) however, the 'necessity' of complex numbers is much more apparent and significant — they form the algebraically closed field for real numbers.

{% tangent(summary="Algebraically Closed Fields", open=true) %}
In mathematics, an [algebraic structure](https://en.wikipedia.org/wiki/Algebraic_structure) is a set of elements and operations, that satisfy certain rules. A [field](https://en.wikipedia.org/wiki/Field_(mathematics)) is an algebraic structure that [satisfies certain properties](https://en.wikipedia.org/wiki/Field_(mathematics)#Alternative_definition"), namely the properties of addition, subtraction, multiplication, and division. Real numbers are fields. An [algebraically closed field](https://en.wikipedia.org/wiki/Algebraically_closed_field) must be a field that has roots in that field for a non-constant polynomial with coefficients as elements of that field. For example, `x^2 + 1 = 0` does not have roots defined in real numbers even though the coefficients are real, and real numbers are therfore not algebraically closed. The roots *are* defined for all complex numbers however, forming an algebraically closed field.
{% end %}

## Rethinking Conventions

The new definition of multiplication is consistent with its previous behaviour. It expands the multiplication function rather than altering it in a way that breaks its previous behaviour. Similarly, the assumption about the existence of an imaginary line that is perpendicular to the real number line does not break any current conventions either. In fact, when combined with our new defintion of multiplication, it can describe two dimensional rotations in a very elegant manner.

So now the question arises: Does it warrant redefining multiplication, and creating a new number system simply to describe rotations? Absolutely. So much so that quantum mechanics make extensive use of imaginary numbers to simplify [wave functions](https://en.wikipedia.org/wiki/Wave_function). Does it make sense then, that a number system — that feels intuitive, and are used to describe reality as we know it — are called imaginary? Absolutely not. Would you describe negative numbers as 'unnatural' because they aren't a part of natural numbers?

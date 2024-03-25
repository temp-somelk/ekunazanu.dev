+++
title = "Generative Music"
description = "Using music theory to generate ambient music."
date = 2026-05-01
draft = true
template = "article.html"
[extra]
type = "article"
thumbnail = "lab.airwaves.svg"
thumbnailalt = "Air particles as black dots with a sine wave on a yellow background."
+++

This is another one of the more experimental posts.

I like music — a lot of people do. I also like math — a lot of people do **not**. It's time to mix both these arts. It's time to experiment and create.

## Music Theory
 
To create music, it first helps to have an understanding of what is sound and what makes certain sounds more pleasant than others.

![airparts](airparticles)

The particles above loosely represent air molecules. A vibrating or oscillating object can cause the air molecules to vibrate and oscillate as well, creating pressure waves. sound. If the air pressure at a point is plotted with respect to time, then the resulting graph is similar to a sine wave:

![particles and corresponding wave below, (air pressure at ear at position on the left mapped on y axis, with time on moving x axis) adjustable pitch and amplitude](interactive)

{% tangent(summary="Sine waves", open=true) %}
The pressure graph draws out looks similar to sine wave since the source creating the vibrations is oscillating in a sine like motio .
{% end %}

The amplitude of the wave corresponds to the difference in sound pressure — the intensity or **loudness** of the sound, and the frequency of the wave corresponds to the **pitch** of the sound. From this point on, the abstracted wave representation will be used instead of air particles because it is simpler to represent and easier to comprehend.

### Intervals

The previous example used a sound that had a singular frequency — this time, another wave is added:

![two waves with adjustable freq -> same amplitude base frequency 1st in black and 2nd freq in gray](interactive)

Try changing the frequency of the second sound (wave) to twice of the original. Now try it again with one and a half times the original. Try it with other frequencies too, and notice when they sound pleasant. When the freuqency of the two sounds are in simple ratios, they sound harmonious.

Music theory is based around these ratios, or [intervals](https://en.wikipedia.org/wiki/Interval_(music)). A frequency ratio of 2:1 is the perfect octave. A ratio of 3:2 gives us the perfect fifth, 4:3 is the perfect fourth, 5:4 is the major third, 9:8 is the major second, and so on. The smallest of the intervals is the minor second also called the semitone, has a ratio of 16:15. The minor second along with a few other intervals sound [dissonant](https://en.wikipedia.org/wiki/Consonance_and_dissonance) since they do not have simple frequency ratios, but are still useful for creating tension.

![all 12 notes with interval ratio multiple and interval name above -> base in black, all others in gray](static)

This simple integer ratio interval system is the [just intonation](https://en.wikipedia.org/wiki/Just_intonation). However because of the way the intervals are defined, it is [mathematically impossible](https://www.youtube.com/watch?v=1Hqm0dYKUx4) to get a perfect scale that have consistent interval ratios between any other two notes in the scale. Instead, the [equal temperament](https://en.wikipedia.org/wiki/Equal_temperament) (equally spaced intervals) system is used to minimize the *overall* deviations in intonation.

![All notes with equal temperament ratio multiple (both root 2 and decimal) and interval name above](static)

### Scales

There are twelve notes in music theory — A, A#, B, C, C#, D, D#, E, F, F#, G, G# — or if using flats, then A, B♭, B, C, D♭, D, E♭, E, F, G♭, G, A♭. It's unnecessarily complicated, but that's just the way it is. The most common standard frequency around which the other notes are derived from, is 440Hz. All other notes are derived using the interval ratios mentioned before. 

![all notes with note name (A to G#/Aflat) and frequencies below and fixed ratio multiple BUT NO interval name above](static)

Note: There is more than one [octave](https://en.wikipedia.org/wiki/Octave), but we'll restrict ourselves to one to keep things simpler.

![All notes (bigger superset from C1 to C7) with and note name below and ratio multiple/divisor above NO interval name zoomed out ABOVE and zoomed in on one octave A4 - G#4 (same as above) BELOW](static)

From these twelve notes, a subset can be selected to get a [scale](https://en.wikipedia.org/wiki/Scale_(music)). Scales can be described by their number of notes and by the structure of their intervals, to set a specific 'mood' for the melody. Usually music in a [major scale](https://en.wikipedia.org/wiki/Major_scale) sounds upbeat, while music in [minor scales](https://en.wikipedia.org/wiki/Minor_scale) sound melancholic. [Pentatonic scales](https://en.wikipedia.org/wiki/Pentatonic_scale) are similar but have five notes instead. [Modes](https://en.wikipedia.org/wiki/Mode_(music)) are similar in the sense they define the structure of intervals, but are generalized; not necessarily linked to specific [keys](https://en.wikipedia.org/wiki/Key_(music)), and have eight notes.

Here's an interactive example to get a sense of different scales and modes:

![all twelve notes - scrollable. on top interval name - fixed. clicking on the note horizontal scrolls twelve notes to get new base note. keys of scale are highlighted with colored background circle. dropdown menu to select scale/mode. in case of Modes, remove notes and only show background circle — to emphasize interval structure. Bottom -> "Scale of C/D#/etc or Mixolydian/Ionian Mode" and play button below. play individual notes in asc. order](interactive)

### Chords

When two notes are played separately in succession, it is called a [melodic interval](https://en.wikipedia.org/wiki/Melody). When the two notes are played in unison, it is called a [harmonic interval](https://en.wikipedia.org/wiki/Harmony). And when three or more notes are played simultaneously, it is a [chord](https://en.wikipedia.org/wiki/Chord_(music)). Except [power chords](https://en.wikipedia.org/wiki/Power_chord) (consiting of two notes) are a thing, and [arpeggios](https://en.wikipedia.org/wiki/Chord_(music)) (broken chords) can be chords too sometimes, so the definition is somewhat loose. Usually, chords are triads — consiting of the root note, a major or minor third, and a perfect fifth.

Again, below is an example to experiment with different chords:

![all twelve notes - scrollable. on top interval name - fixed. clicking on the note horizontal scrolls twelve notes to get new base note. keys of scale are highlighted with colored background circle. dropdown menu to select chord. First row same as above example - select scale. Second row for chords, using different color for background circle. Bottom -> "CMaj/D#Min/GMaj7 etc Chord" and play button below. play in unison once.](interactive)

### Dynamics

We discussed about the frequency or pitch of sounds, but the [amplitude or loudness](https://en.wikipedia.org/wiki/Dynamics_(music)) can just as well be altered to express a feeling. The loudness of a section can ascend (crescedo) to create drama and tension, or it can gradually descend (decrescendo) after resolving the tension. Sounds can also be soft and quiet (piano) to emphasize the pieces that are strong and loud (forte) following them.

### Timbre

Going back to sound waves, it is important to specify that so far we've only been dealing with sine waves. But waveforms other than the sinusoid exist too — notable ones include the square wave, triangular wave, and sawtooth wave. These however sound different when compared against the sine waves — even at the same frequency.

![square, sawtooth, triangular, sine at same (adjustable) freq play buttons for each below/on the side](interactive)

Using [fourier analysis](https://en.wikipedia.org/wiki/Fourier_analysis), these waves can be decomposed into multiple sine waves. The human ear perceives the square wave (and the sawtooth and triangular wave for that matter) as a group of multiple sine waves with frequencies.

![decomposed square,trian,sawtooth to sine frequencies](interative)

Try creating your own waveform to see how it sounds at the frequency:

![self waveform draw and play with frequency selector slider and play button](interactive)

Similarly, different instruments have different and unique waveforms and hence sound different even at the same frequency. This is why instruments sound different even when playing the same notes. Notes played on some instruments like guitars or pianos quickly become quieter over time — the change in amplitude of the sound over time, described by their [envelope](https://en.wikipedia.org/wiki/Envelope_(music)) — differ based on the instrument, also giving each of them a unique tone. The unique tone quality of an instrument is called its [timbre](https://en.wikipedia.org/wiki/Timbre). For example, this is the waveform and envelope of a piano and a guitar playing at 440Hz.

![piano and guitar difference](maybevideo)

### Rhythm

Try playing these beats:

![irregular beats](audio)
![regular beats](audio)
![waltz beats](audio)

The first beat is random, and does not necessarily sound enjoyable. The second is periodic, and is slightly more pleasant but nonetheless feels monotonous and dull. The last one feels rhythmic and dynamic; more enjoyable compared to the previous two. One way to make music sound more satisfying is to use stick to regular pulse beat groupings and accentuating certain beats — using a [metre](https://en.wikipedia.org/wiki/Metre_(music)). The [number](https://en.wikipedia.org/wiki/Time_signature) of beats per [grouping](https://en.wikipedia.org/wiki/Bar_(music)) is usually four or three — called [common time](https://en.wikipedia.org/wiki/Duple_and_quadruple_metre#Quadruple_metre) and [waltz](https://en.wikipedia.org/wiki/Triple_metre) respectively.

Even after sticking to a meter, the music might sound rhythmic for a while, but if played long enough, even it will begin to sound repetitive. The obvious way to go about it is to introduce variations in the duration of certain notes, while still loosely sticking to the selected beat structure. Notes can be half, twice, quadruple the duration of a single beat, or [somewhere in between](https://en.wikipedia.org/wiki/Note_value).

While using certain rhythm patterns can make music sound structured and more pleasing, it can also be used to set the of vibe of the music. The number of [beats per minute](https://en.wikipedia.org/wiki/Tempo) can be varied to express emotions. Music with a fast tempo sounds lively and energetic, while music with a slow tempo sounds sad and mellow.

![upbeat music](audio)
![slow sad song](audio)

## Playground

On that note (pun not intended), it's time to see wha the amalgamation of all the previously mentioned parameters has all led to.

---

## References

* Make sounds similar to Limbo game OST
* https://ivanish.ca/diminished-fifth/
* https://generative.fm/
* https://ciechanow.ski/sound/
* search for algorithmic composition
* Alt -> https://alterebro.com/ for generative images
* https://www.youtube.com/@marcevanstein
* https://learningmusic.ableton.com/make-beats/tempo-and-genre.html

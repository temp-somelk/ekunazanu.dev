+++
title = "Quantifying Colour"
description = "A few things about colours and colour formats."
date = 2024-07-13
draft = true
template = "article.html"
[extra]
type = "article"
thumbnail = "lab.colours.svg"
thumbnailalt = "Red, green and blue lines representing a screen."
+++

There's a lot of different ways to describe colours. But to pinpoint an exact colour, there needs to be a standard way to represent it. Even some surface level research about the topic reveals that there's extensive science and math behind this seemingly simple task. And while it might seem intimidating at first, it starts making a lot of sense once there is a solid understanding behind the core fundamentals of how colours are perceived.

## Defintion

Before discussing the different subtopics of colours, it is important to first define what colour even means. [Wikipedia](https://en.wikipedia.org/wiki/Color) defines it as "The visual perception based on the electromagnetic spectrum". This reveals a few important bits of information. A colour, by definition, is inherently not an objective property of matter — but rather, also depends on the perception of the viewer. Different animals might perceive objects with the same 'colour' differently. Even humans might percieve the colour of same objects in different ways. What is objective however, is the second part of the rather informal definition — the visual perception based on the **electromagnetic spectrum**.

## Spectral Power Distribution

To start off, we need to know a little about [photons](https://en.wikipedia.org/wiki/Photon). Light is made up of photons. These can thought of tiny abstract particles carrying a specific amount of [energy](https://en.wikipedia.org/wiki/Photon_energy) which can be described by their [wavelength or freuqency](https://en.wikipedia.org/wiki/Photon_energy#Physics).

![animation of a packet of animated wave with slider for wavelength; show higher energy for high frequency](interactive)

{% tangent(summary="Photon wave-particle duality", open=true) %}
The above is an *interpretation* of a photon, and is not necessarily accurate. The exact shape of photons is difficult to visualise and describe since photons exhibit [both particle and wave-like behaviour](https://en.wikipedia.org/wiki/Wave%E2%80%93particle_duality#Wave-particle_duality_of_light), and trying to visualize photons as both as a particle and a wave can get tricky quickly.
{% end %}

The full range of the different wavelengths (or frequencies) of photons forms the [electromagnetic spectrum](https://en.wikipedia.org/wiki/Electromagnetic_spectrum).

![image of packets of aninated waves of different wavelength with a sepectrum legend below](animated)

{% tangent(summary="Electromagnetic fields", open=true) %}
It is called the 'electromagnetic' spectrum is because a photon is technically a quantum (minimum discrete quantity) of an [electromagnetic field](https://en.wikipedia.org/wiki/Electromagnetic_field). An explanation of the electromagnetic field warrants a thorough analysis, but is unfortunately beyond the scope of this article.
{% end %}

Since photons carry energy, any body that radiate photons also radiate energy. The *rate* of amount of this energy being transferred via photons can be measured as [power](https://en.wikipedia.org/wiki/Power_(physics)).

![moving photons from left to right onto an power sensor; rate of number of photons slider; column-ish power indicator below — make it somewhat similar (but reduced/minimal) version of the following spd graph below](interactive)

If a body is radiating photons of different wavelengths, and if their [intensity](https://en.wikipedia.org/wiki/Intensity_(physics)) (power per unit area) is plotted per wavelength, then the resulting curve yields a [spectral power distribution](https://en.wikipedia.org/wiki/Spectral_power_distribution).

![moving photons from left to right onto an smaller fixed size power sensor; rate of number of photons slider for three/four/five/six wavelengths; spd graph below](interactive)

{% tangent(summary="Shorter wavelengths transfer more power", open=true) %}
Since photons with shorter wavelengths carry more energy, more power is transferred by shorter wavelength photons than longer wavelength photons even if the number of photons being radiated per unit time is the same.
{% end %}

The spectral power distribution is fundamenetal to determining the 'colour' of an object.

## Photoreceptor Cells

The sun radiates a large amount of photons, and the spectral power distribution of the sun looks roughly like this:

![spd of sunlight](static)

The wavelength of photons emitted by the sun having the highest intensity is around 500nm. Human eyes have naturally evolved to become sensitive to photons with these wavelengths. In fact, the human eye has developed different kinds of [photoreceptor cells](https://en.wikipedia.org/wiki/Photoreceptor_cell) which are sensitive to wavelengths ranging from roughly 400nm to around 700nm. Depending on the energy carried by the photons (their wavelength and intensity), they can 'excite' the photoreceptor cells to produce a specific response. The average human eye has two kinds of photoreceptor cells — [rod cells](https://en.wikipedia.org/wiki/Rod_cell) and three types of [cone cells](https://en.wikipedia.org/wiki/Cone_cell).

The different types of photoreceptor cells are sensitive to different wavelengths of light by differing amounts — for example some cones (S-cones) will not produce a significant response to lights with longer wavelengths but other types (L-cones) will. The [sensitivity](https://en.wikipedia.org/wiki/Spectral_sensitivity) curves of the different photoreceptor cells are shown below:

![absolute response curves above; normalized response curves below;](static)

{% tangent(summary="Normalized curves", open=true) %}
The sensitivity of S-cones is significantly lower compared to the other cones. Similarly, rods are relatively more sensitive to light than cones. However, the sensitivity curves are normalized, such that the curves have equal areas under the curves — to make calculations simpler.
{% end %}

The response of the different photoreceptor cells to lights of different wavelengths is dependent on the spectral power distribution of the incident light, and the sensitivty curves of the rods and cones — ie. the response generated by the cells depends on the wavelength (and intensity) of the photons, and how sensitive the specific type of photoreceptor cell is to that wavelength. The responses generated by the cells for [monochromatic light](https://en.wikipedia.org/wiki/Monochromatic_radiation) (light with a single, or a very narrow band of wavelengths) is illustrated below:

![spd on top — single spike on spd at wavelength dependent on sliders on top; sensitivity curve graph of photoreceptor cells below; response curve of above two graphs below — shade the areas below with colour of photoreceptor type (rod=black,s=blue,m=greenish,l=yellowish-to-red); slider for wavelength & number of photons at bottom below all graphs; show amount of response of each type of receptors (rods and cones) as a sort of (progress/without sliding knob) bars on the right of the sliders for wavelength and intensity of photons; eg: https://jamie-wong.com/images/color/ConeExcitation1.png — combine all the three coloumns to one graph; keep rows separate; highlight response of cones progress bars and cones curves — by greying/reducing contrast of rods response progress bars, rods sensitivity curves, and rods response curves;](interactive)

{% tangent(summary="Photoreceptor cell responses", open=true) %}
The response curve of the types of photoreceptor cells is the [point-wise product](https://en.wikipedia.org/wiki/Pointwise#Examples) of the spectral power distribution curve and the photoreceptor sensitivity curves. The overall response from each type of photoreceptor cell is the total area under their corresponding response curves.
{% end %}

Light with differing intensity and wavelengths produce different and unique responses in the three types of cones. The different responses are [perceived by the brain](https://en.wikipedia.org/wiki/Color_vision#/media/File:Diagram_of_the_opponent_process.png) as a colour.

![spd on top — single spike on spd at wavelength dependent on sliders; sensitivity curve graph of photoreceptor cells below; response curve of above two graphs below — shade the areas below with colour of photoreceptor type (rod=black,s=blue,m=greenish,l=yellowish-to-red); slider for wavelength & number of photons at bottom below all graphs; show amount of response of each type of receptors (rods and cones) as a sort of (progress/without sliding knob) bars on the right of the sliders for wavelength and intensity of photons; eg: https://jamie-wong.com/images/color/ConeExcitation1.png — combine all the three coloumns to one graph; keep rows separate; small colour box below or next to right to response (progress-like) bar, showing colors and colour names below the box at specific cone reponses (specific wavelengths and intensity); highlight response of cones progress bars and cones curves — by greying/reducing contrast of rods response progress bars, rods sensitivity curves, and rods response curves;](interactive)

{% tangent(summary="Colour Classifications", open=true) %}
There can be more or fewer colour names for these wavelengths depending on the [classification](https://en.wikipedia.org/wiki/Spectral_color#Spectral_color_terms).
{% end %}

Rods do not have a big effect on colour perception. In [well-lit conditions](https://en.wikipedia.org/wiki/Photopic_vision), the cones might produce different responses based on the wavelength of light. But in such conditions, the rod cells produce a saturated response, since rods are more sensitive than cones. As the response of rods in bright environments is indifferent to wavelengths, it is not very useful in differentiating between different wavelengths, and therefore does not play a significant role when it comes to colour perception.

![spd on top — single spike on spd at wavelength dependent on sliders on top; sensitivity curve graph of photoreceptor cells below; response curve of above two graphs below — shade the areas below with colour of photoreceptor type (rod=black,s=blue,m=greenish,l=yellowish-to-red); slider for wavelength & number of photons at bottom below all graphs; show amount of response of each type of receptors (rods and cones) as a sort of (progress/without sliding knob) bars on the right of the sliders for wavelength and intensity of photons; eg: https://jamie-wong.com/images/color/ConeExcitation1.png — combine all the three coloumns to one graph; keep rows separate; highlight response of rods progress bars and rod curves — by greying/reducing contrast of cone response progress bars, cone sensitivity curves, and cone response curves; restrict intensity slider to NON-LOW intensity values — and maybe grey out the first 10% of the slider;](interactive)

{% tangent(summary="Saturated response", open=true) %}
The response from rods remain saturated, and no meaningful information about the wavelength is obtained from the response. Cones on the other hand, respond differently to different wavelengths, and the different responses can be interpreted by the brain as different wavelengths. However, a source of light with high enough intensity can saturate the response of even cone cells, and the brain perceives the colour as white — regardless of the wavelength of the light.
{% end %}

In [darker environments](https://en.wikipedia.org/wiki/Scotopic_vision) however, rods produce a response when cones may not. But since all rod cells have almost identical sensitivity curves, it becomes impossible to distinguish between different wavelengths and intensities of light.

There are many instances when two sources of lights with two differing wavelengths and intensity produce the same response in rods, causing the two light sources with different wavelengths to appear similar. There is no way to differentiate between different wavelengths and intensity of light and the brain simply evolved to perceive the response from the rods as a single brightness value — making things appear different shades of gray in the dark.

![two different spds on top, side-by-side — single spike on spds at wavelength dependent on sliders; two IDENTICAL sensitivity curve graph of photoreceptor cells below; two different response curve of above two (four in total) graphs below — shade the areas below with colour of photoreceptor type (rod=black,s=blue,m=greenish,l=yellowish-to-red); sliders for wavelength & number of photons at bottom below, for each of two columns of graphs on left and right; show amount of response of each type of receptors (rods and cones) as a sort of (progress/without sliding knob) bars on the right of the sliders for wavelength and intensity of photons — two for each of the two columns of response curves; eg: https://jamie-wong.com/images/color/ConeExcitation1.png; keep rows separate; highlight response of rods progress bars and rod curves — by greying/reducing contrast of cone response progress bars, cone sensitivity curves, and cone response curves; restrict intensity slider to LOW intensity values (gry out 90% of the right of the original sized slider) — and maybe extend the slider to the left a bit and use different scaling, mentioning the altered scale below](interactive)

{% tangent(summary="Wavelength ambiguity", open=true) %}
Two light sources with wavelengths [XXXnm and YYYnm](switch#) produce a similar response in rods, and are thus perceived as similar by the eye (in dark conditions). Light with both varying [wavelengths and intensity](switch#) can also produce identical responses in rods. Going through different wavelengths and intensities reveals there are many more such instances of ambiguity.
{% end %}

### Colour Blindness

Ambiguity of wavelengths is not strictly limited to rod cells. Light with different wavelengths and intensities may produce identitical responses in cones as well. It is much less likely to happen however, because there are three types of cone cells and each of them produce a different response at different wavelengths.

But the photoreceptor cell response curves are not the same for everyone. Few people may have significant overlap in the response curves of the L-cones and M-cones, resulting in between different wavelengths producing similar responses in the cones — similar to rods in low light conditions.

![two different spds on top, side-by-side — single spike on spds at wavelength dependent on sliders; two DIFFERENT sensitivity curve graph of photoreceptor cells below — one normal on left, one with overlapping L-cones and M-cones sensitivity curves on right; two different response curve of above two (four in total) graphs below — shade the areas below with colour of photoreceptor type (rod=black,s=blue,m=greenish,l=yellowish-to-red); sliders for wavelength & number of photons at bottom below, for each of two columns of graphs on left and right; show amount of response of each type of receptors (rods and cones) as a sort of (progress/without sliding knob) bars on the right of the sliders for wavelength and intensity of photons — two for each of the two columns of response curves; eg: https://jamie-wong.com/images/color/ConeExcitation1.png; keep rows separate; highlight response of cones progress bars and cones curves — by greying/reducing contrast of rods response progress bars, rods sensitivity curves, and rods response curves; REMOVE SENSITIVITY CURVES, RESPONSE CURVES, RESPONSE PROGRESS BARS FOR RODS FROM THIS POINT ON (unless explicitly mentioned);](interactive)

{% tangent(summary="Wavelength ambiguity", open=true) %}
Wavelengths [XXXnm and YYYnm](switch#) produce a similar responses in cones, and are perceived as similar colours.
{% end %}

This can happen if the L-cones have an anomaly and shift their response curves slightly towards shorter wavelengths ([protanomaly](switch#)), or the M-cones shift their response curves towards longer wavelengths ([deuteranomaly](switch#)). People may also lack functional L-cones ([protanopia](switch#)) or M-cones ([deuteranopia](switch#)) entirely. The result is similar in all the cases — reds and greens look similar, to almost identical. In very rare cases, some people may also have anomalous S-cones, resulting in [tritanomaly](switch#) and [tritanopia](switch#). In even rarer cases, people may [only have S-cones](switch#), or [no cone cells at all](switch#) — resulting in total colour blindess.

![spd above response curves; two response curve graphs of photoreceptor cells; one set sliders for wavelength & number of photons, another set of sliders for wavelength & number of photons; one vertical line overlaid on each of two response graphs to show wavelengths; show amount of response of each type of receptor cells as (unmovable/grayed out) bars on the right (vertical) or below (horizontal) on both graphs; emphasis on response of cones; others are lightened out (maybe low contrast); show interesection of wavelength vertical line indicator and response curve as small (but bigger than lines) dots; emphasis on intersection cones curve (others are grayed/low-contrast out); curve changes as intensity slider changes; menu to select protanomaly/deutanomly/tritanomaly/prot/achromatopsia/BCM/etc; change menu option changes response curves](interactive)

### Non-Spectral Colours

All the examples in the above subsections were about [spectral colours](https://en.wikipedia.org/wiki/Spectral_color) — colours with a single, very narrow band of wavelengths. But not all colours are spectral colours. [Purple and magenta](https://en.wikipedia.org/wiki/Line_of_purples) are examples of colours that cannot be created using light with a narrow band of wavelengths. Shades of gray cannot be produced using only monochromatic light either. Pink is another example of a non-spectral colour.

The spectral power distribution of non-spectral colours is not a single spike at a specfic wavelength, unlike spectral colours:

![spd of green; spd of magenta; spd of pink; spd of gray](static)

The set of responses from the cones for non-spectral colours like magenta or gray is different from the set of responses produced by the cones for spectral colors — in fact, a similar response from cones cannot be recreated using light with just one wavelength. The brain perceives these unique set of responses from the cones as a separate colour.

Try finding a spectral colour that has an identical response as magenta. It is impossible:

![fixed spd of magenta above response curve graph with fixed vertical wavelength lines; changing spd — depending on wavelength and intensity slider — above response curve graph with wavelength and intensity slider; two response curve graphs of photoreceptor cells; two FIXED vertical lines overlaid on one response graph to show two wavelengths of blue and red; one set sliders for wavelength & number of photons below the other response curve graph; one vertical line to show changeable wavelength in the above the slider; show amount of response of each type of receptor cells as (unmovable/grayed out) bars on the right (vertical) or below (horizontal); emphasis on response of cones; others are lightened out (maybe low contrast); show interesection of wavelength vertical line indicator and response curve as small (but bigger than lines) dots; emphasis on intersection cones curve (others are grayed/low-contrast out); curve changes as intensity slider changes; another set of (unmovable/grayedout) bars BUT FIXED to show response of cones for magenta (blue and red); show response of magenta as addition of (unmovable/grayedout bars) responses of blue wavelength and response of red wavelength (another unmovable/grayedout) bars) — with sum as magenta response(unmovable/grayedout bars); user tries to move movable wavelength and intensity to change output of grayedoutbars to match FIXED grayedout bars of magenta response;](interactive)

[Grays](switch#) and [pinks](switch#) too, are composed of light with multiple wavelengths. The response of cones can be thought of as the area under the cruve. In either of the cases, the resonse of the cones is unique and different from the responses generated by monochromatic light.

![spd of pink, and gray, and (make it sketchable by user — BIG MAYBE) on top; response curves below. another curve multiplication of both curves. shade area under product of curves — display that as the value of response of cones; the example image has three sets of curves for each cone — try to combine all of them in one graph for each row — aka combine the top 3 curves as one spd graph; middle 3 as previous cone response graph; bottom 3 curves as a product response graph](interactive)

{% tangent(summary="Addition of different wavelengths", open=true) %}
The response of cones to light with multiple wavelengths is complicated. This is an imprecise *interpretation* of how cones repond when exposed to lights with multiple wavelengths.
{% end %}

### Metamerism

In the above cases, various wavelengths of light together created unique responses in cones, which is different from the responses when cones are exposed to monochromatic light. However, multiple wavelengths of light together can also produce a response that is very similar to the response of a spectral colour.

By using just three wavelengths of light and varying their intensity, it is possible to produce similar cone responses when stimulated by monochromatic light. Empirical data from colour matching experiments by [William David Wright](https://doi.org/10.1088/1475-4878/30/4/301) and [John Guild](https://doi.org/10.1098/rsta.1932.0005) mapped light of three fixed wavelengths (435nm, 546nm, and 700nm) but with varying intensities, to spectral colours such that they were perceived as the same colour by a group of observers. The results were summarised, and the resulting intensities for the three wavelengths yielded a curve similar to this:

![cie colour matching function graph;](static)

{% tangent(summary="Negative intensity", open=true) %}
Adding colours to one side is equivalent to sutracting colours from the other side, according to [Grassman's laws](https://en.wikipedia.org/wiki/Grassmann%27s_laws_(color_science)). In the colour matching experiment, adding light to the spectral colour being compared is represented as subtracting (resulting in negative intensity) from the colour matching function curves.

It is important to note that, it is impossible to create light with negative intensity. So, it is physically impossible to reproduce certain colours using only three wavelengths of light.
{% end %}

It can be observed that the three wavelengths does produce similar responses to spectral colours in the cones — making them appear similar:

![spd of single wavelength light on left above; response curve below; and product of both bottom; slider for wavelength but grayed out slider for intensity below bottom; grayed out sliders for 700nm and 546nm light may appear and disappear depending on wavelenght; the sliders have grayed out wavelenths (fixed at 700/546nm) and grayed out (but moveable) sliders for intensity; spd of three wavelengths on right above; response curve below; and product of both bottom; grayed out sliders for wavelenghts (grayed out and stays fixed as well) and intensity (grayed out moves) of light sources; separate cone responses for both graphs below respective graphs](/media/lab/quantifying-colours/samp.png)

The experiment has used three spectral colours to replicate most other spectral colours. But they can also be used to mimic non-spectral colours. In general bodies with [different spectral power distributions](switch#below) can be perceived as similar colours because they produce similar responses in cones — the term for it is called [metamerism](https://en.wikipedia.org/wiki/Metamerism_(colour)).

![spd on left above; spd on right above; identical response curves below on both left and right; separate products at the bottom on left and right; show cone response bars below bottom; make the spd drawable; if drawing is not feasible, make it such that the "different spd" link cycles through various metamer spds — every time it is clicked;](interactive)

## Colour Space

Since the amount of response produced by the L-cones, M-cones, and S-cones correspond to a colour, it means the set of (L,M,S) values can be used to uniquely identify a colour. But the (L,M,S) values can also be mapped as points in a three dimensional space. If the (L,M,S) values are thought of as points in a three dimensional space, then the resulting space forms a [colour space](https://en.wikipedia.org/wiki/Color_space), where a point in this space can identify a colour.

{% tangent(summary="Measuring LMS values" open=false) %}
The (L,M,S) values is the total response of their respective cones. The total response of each cone is simply the area under their corresponding response curves, and the response curves of the cones are the pointwise product of their normalized sensitivity curves and the spectral power distribution. So, if `J(λ)` is the spectral power distrubtion of the light source, and `l(λ)`, `m(λ)`, and `s(λ)` are the sensitivity curves of the L-cones, M-cones, and S-cones — then the L, M, and S values is given by:\
`L = ∫ J(λ)·l(λ) dλ`\
`M = ∫ J(λ)·m(λ) dλ`\
`S = ∫ J(λ)·s(λ) dλ`
{% end %}

In this case, the colour space is the [LMS colur space](https://en.wikipedia.org/wiki/LMS_color_space) — where a colour (in fact, every perceivable colour) can be described as points in this space as a set of (L,M,S) values.

![LMS colour cube on left — isomorphic projection; sliced plane of cube on right for specific value of L — plane has (M, S) as coordinates — show point on place corresponding to M S values; sliders for 'L, M, S response' below/at bottom; colour box on right of sliders;](static/interactive-maybe3d)

{% tangent(summary="Impossible colours", open=true) %}
While all colours can be represented using LMS values, the reverse is not always true. Not all LMS values correspond to perceivable colours. The sensitivity curves of the M-cones has overlap with the sensitivity curves of L-cones and S-cones, so if any type of light excites the M-cones, it must also excite the L-cones, or S-cones, or both. So 'colours' with LMS values (0,1,0) are [imaginary and not physically possible](https://en.wikipedia.org/wiki/Impossible_color#Imaginary_colors).
{% end %}

The LMS colour space is one way to describe colours, but is not the only one. There are many other to describe colours. While fundamental and somewhat intuitive, the LMS colour space is not the standard reference for other colour spaces — it is the [CIE 1931 colour space](https://en.wikipedia.org/wiki/CIE_1931_color_space).

### CIE 1931

The LMS colour space uses the response of the cones as the bases for the colour space. That is, colours could be decribed by a set of (L,M,S) values. However, other bases can also be used.

In the Wright-Guild colour matching experiments, light with three wavelengths were used to recreate certain spectral colours by varying the intensity of the three wavelengths. But instead of using a specific intensity of light for each of the three wavelenths to recreate a spectral colour, the intensity can also be arbitrarily selected — in which case it would be able to reproduce non-spectral colours as well.

These colours can be represented as three intensity values of the three wavelengths — and these values can again be represented as points in a three dimensional space where a point represents a colour. The resultant space is again a colour space, called the [CIE RGB](https://en.wikipedia.org/wiki/CIE_1931_color_space#CIE_RGB_color_space) colour space.

![RGB colour space cube on left; slice of plane on right; similar to LMS color space; sliders should explicitly mention 'Xnm intensity' and not cone response; colour box on right of sliders;](interactive)

{% tangent(summary="CIE RGB bases", open=true) %}
The CIE RGB colour space uses as lights of 700nm (R), 546nm (G), and 435nm (B) as its [primaries](https://en.wikipedia.org/wiki/Primary_color#Real_primaries) (colours used to recreate other colours). The wavelengths were selected based on Wright-Guild experiments. The (R,G,B) values represent the intensity of the primaries, and a set of (R,G,B) values can describe a colour — forming a colour space.
{% end %}

Points in the CIE RGB colour space corresponds to different colours, just like the LMS colour space. But unlike the LMS colour space, it cannot describe all perceivable colours using positive sets of values.

Spectral colours can be mapped in the CIE RGB colour space too, using the same data from the Wright-Guild colour matching experiments. The resultant curve is called the [spectral locus](https://en.wikipedia.org/wiki/Spectral_color#In_color_spaces) — the curve representing the intensity of CIE RGB primaries required to replicate spectral colours.

![spectral locus mapped on CIE RGB color cube; sliced plane on right — like earlier; slider for wavelength;](interactive)

The spectral locus has negative values in the CIE RGB colour space for certain spectral colours. The negative values does not imply that the colours are not perceivable. As mentioned earlier in the [metamerism subsection](#Metamerism), the negative values simply means that the CIE RGB primaries cannot physically recreate certain colours. It also means that the CIE RGB colour space cannot describe all colours using only positive sets of values.

It was decided that a different colour space that could map all perceivable colours to positive values was desirable. Instead of conducting more experiments to construct the new colour space, the existing CIE RGB colour space could be transformed using simple linear transformations. The transformation of the three dimensional colour space can be defined by a 3x3 matrix:

![colour space with spectral locus with bouding boxes drawing with dotted lines on left — also has three orthogonal lines to depict primaries; arrow with matrix below the arrow in middle; transformed space on the right — transforming space transforms primaries — use red, green, blue for old primaries that change with space transform — but also include gray orthogonal lines that stay in place regardless of transform; below inputs for matrix on left; on right of matrix inputs include views depicting top, side and front views — option to select which view — include transformed primaries and fixed orthogonal primaries;](interactive)

{% tangent(summary="Colour space transformations", open=true) %}
From Grassman's laws it can be inferred that linear transformation of colour spaces is possible since human colour perception is nearly linear.
{% end %}

[Transforming](switch#transformToXYZ) the space has the effect of the transforming the RGB primaries as well, which means the new space is now defined by different new primaries. It should make sense since earlier the spectral colour with 500nm wavelength had to be defined by negative values of the red primary (700nm light) — but now the same colour is defined by positive values. It suggests that the coordinate system (primaries) itself has to contain some sort of a negative intensity. Since it is physically impossible for light to have negative intensity, it implies that the primaries for the new colour cannot physcially exist, and are imaginary.

Since the primaries of the new colour space are imaginary, it is reasonable to define the new primaries to represent more abstract concepts instead of physical quantities. Again, it was decided that one of the primaries would define the [luminance](https://en.wikipedia.org/wiki/Luminance) of the colour, and the other two can be used to derive its [chromaticity](https://en.wikipedia.org/wiki/Chromaticity). The primaries of this new colours space are named X, Y, and Z — and the resulting colour space is called [CIE XYZ](https://en.wikipedia.org/wiki/CIE_1931_color_space#Meaning_of_X,_Y_and_Z) colour space. The Y primary represents the luminance of a colour, while the X and Z primaries are used to derive its chromaticity.

{% tangent(summary="Luminance and chromaticity", open=true) %}
Luminance refers to the perceived brightness of a colour, while chromaticity is analogous to hues. According to the [opponent process](https://en.wikipedia.org/wiki/Opponent_process) theory, colours are perceieved as pairs of opposing colours — red vs green, blue vs yellow (chromaticity), and black vs white (luminance). Hence, it is possible to describe a colour by how red it is compared to how green it is, how blue it is compared to how yellow it is, and how bright the overall colour is — ie. defining colours based on luminance and chromaticity values.
{% end %}

Similar to how the sensitivity of different cones can be measured, the average sensitivity of all the cones can also be measured — resulting in a [curve](https://en.wikipedia.org/wiki/Luminous_efficiency_function) that acts as a luminosity sensitivity curve:

![photopic vision luminosity function](static)

This curve can also be approximated as a weighted sum of the individual RGB colour matching function curves:

![three color matching function curves side-by-side on left — with number values below them denoting weights — add symbol between them; equal symbol between input curves on left and output curve on right; output curve on right; output curve also has fixed luminosity function curve in gray;](interactive)

The [factors](switch#above) represent how much the RGB primaries contribute to the overall brightness or luminance of a colour. But the luminance of of a colour is the Y primary in the XYZ colour space. So, this represents how much each of the RGB primaries contribute to the Y primary in the XYZ colour space — and forms one row of the transformation matrix:

![colour space transform as above; matrix transform but with time with fixed middle rows;](interactive)

The X and Z primaries was defined such that the new colour space fulfilled [certain properties](https://en.wikipedia.org/wiki/CIE_1931_color_space#Construction_of_the_CIE_XYZ_color_space_from_the_Wright%E2%80%93Guild_data), decided by the CIE — resulting in a transformation matrix with values:

![matrix transform as above; fixed values for matrix;](interactive/static)

The X and Z primaries do not directly represent the chromaticity of a colour, but can be used to derive it. But to understand how the X and Z primaries are used to derive the chromaticity in the CIE XYZ colour space, it first helps to understand how the same can be achieved in the CIE RBG colour space.

### Chromaticity

In the CIE RGB colour space, the sum of the intensity of its primaries (R+G+B) can act as a crude approximation for luminance, and the ratio among the different intensity of the RGB primaries can serve as an approximation for a colour's chromaticity. The ratios r, g, b can be easily calculated by normalizing out the total intensity of the primaries:

`r = R/(R+G+B)`\
`g = G/(R+G+B)`\
`b = B/(R+G+B)`

The chromaticity estimates (r,g,b) together with the luminance estimate (R+G+B), can define a colour, and in a way can be thought of a yet another colour space.

{% tangent(summary="Luminance-chromaticity estimates", open=false) %}
While the luminance and chromaticity are approximations, it does not mean that there is loss of information. The exact RGB values can be recreated using the luminance and chromaticity estimates. The approximation simply refers to the imperfect separation of luminance and chromaticity.
{% end %}

If the luminance is fixed to one, then R+G+B = 1 forms a diagonal plane in the RGB space, bounded by (1,0,0), (0,1,0), and (0,0,1):

![sliced plane RGB space — https://jamie-wong.com/images/color/TriangleSliceRGB.png](static)

Since R+G+B = 1, then the point (r,g,b) would be exactly equal to the (R,G,B). The points would lie on the plane R+G+B = 1:

![sliced plane RGB space on top on left; 2d plane for R+G+B=1 as another figure on right of cube; sliders for (R,G,B) below on left; L as a progress bar (non-adjustable; fixed to 1); stacked horizontal bar chart bars for (r,g,b) on right of RGB slider — but maybe include numerial values below too; increasing any one of the RGB values decreases the remaing two primaries (proportionally, such that the ratio bewteen the other primaries is maintained; maybe or maybe not emphasize that r=R, g=G, b=B); see below visualisation for more info — make both of them look similar — exceptions being the fixed luminance to one — and no chromaticity line projection thingy — and only one sliced plane; plot (R,G,B) and (r,g,b) as points on both the sliced plane in the cube figure and the 2d plane figure](interactive)

For some other luminance, R+G+B = k would define a diagonal plane in the RGB space bounded by (k,0,0), (0,k,0,), and (0,0,k). The point (R,G,B) would lie on that plane, while the point (r,g,b) would be the projection of (R,G,B) on the plane R+G+B = 1:

![greyed out sliced plane R+G+B=1 space on top; another greyed out plane for R+G+B=k; 2d sliced plane for R+G+B=1 (NOT R+G+B=k) as another figure on right of cube; sliders for RBG below; k values as a progress bar (non adjustable — determined by RGB values — max value 3 I guess) on right of sliders; rgb values (non-adjustable, determined by RGB values) as a stacked proportional horizontal bar chart type bar — https://media.geeksforgeeks.org/wp-content/uploads/20200923090400/1.PNG — but numerical values below; plot (R,G,B) on the R+G+B=k plane on the cube figure; plot (r,g,b) as points on the plane R+G+B=1 in the sliced plane cube figure, as well as the separate plane figure on the right; in the cube figure include a faint line joining (0,0,0) to (R,G,B) passing through (r,g,b) to signify projection;](interactive)

{% tangent(summary="Dimensionality reduction", open=true) %}
The line connecting a point (R,G,B) to the origin (0,0,0) can be thought of as lines of chromaticity. The distance of a point (R,G,B) from the origin, or the length of the line light represents the luminance. So two points lying on the same line but at different distances represent two colours having the same chromaticity but differing luminance values. Projecting both the points on the same plane means there is [loss of information](https://en.wikipedia.org/wiki/Dimensionality_reduction).

So, the chromaticity plane contains information about chromaticity, and generally does not contain any information about luminance. So unless luminance is explicitly specified, it is impossible to recreate the corresponding RGB values for (r,g,b).
{% end %}

Since (r,g,b) denote ratios (and as evident from above), r+g+b is always equal to one — making one of values redundant. Knowing two, the third can be deduced by subtracting the other values from one. Generally, r and g are kept and b is discarded. Geometrically, it is equivalent to projecting the R+G+B = 1 plane on the RG plane. While the points are projected on the RG plane, it makes more sense semantically to label it as the rg plane:

![greyed out sliced plane R+G+B=1 space on top; another greyed out plane for R+G+B=k; 2d sliced plane for R+G+B=1 (NOT R+G+B=k) as another figure on right of cube — in the middle; rg plane on the right — right of separate sliced 2d plane figure — maybe make it selectable to choose rg-plane, gb-plane or rb-plane OR make a smooth transition between rg-plane and R+G+B=1 plane; sliders for RBG below; k values as a progress bar (non adjustable — determined by RGB values — max value 3 I guess) on right of sliders; rgb values (non-adjustable, determined by RGB values) as a stacked proportional horizontal bar chart type bar — https://media.geeksforgeeks.org/wp-content/uploads/20200923090400/1.PNG — but numerical values below; plot (R,G,B) on the R+G+B=k plane on the cube figure; plot (r,g,b) as points on the plane R+G+B=1 in the sliced plane cube figure, as well as the separate plane figure on the right — as well as the rg-plane diagram; in the cube figure include a faint line joining (0,0,0) to (R,G,B) passing through (r,g,b) to signify projection;](interactive)

{% tangent(summary="The rg plane", open=true) %}
The (r,g) values — and by extension, the rg plane — contain complete information about the chromaticity of a colour, but contain no information about the luminance of a colour. On the other hand (R,G) values represent the intensity of R and G primaries — they contain partial and incomplete information about the chromaticity of a colour as well as the incomplete information about the luminance of a colour. Both planes represent different quantities and are not the same.
{% end %}

It is important to note that changing from the R+G+B = 1 plane to the rg plane does not result in reduction of dimensionality as there is no loss of information. Intuitively, it can be visualised as a simple transformation of a two dimensional space rather than a reduction of a three dimensional space into a two dimensional plane.

These projections result in a chromaticity plane that describes the chromaticity of a colour using (r,g) values. However, the [rg chromaticity space](https://en.wikipedia.org/wiki/Rg_chromaticity) cannot describe all possible chromaticity of colours since the RGB space itself cannot describe all perceivable colours — using positive values at least. But the same idea can be translated for the CIE XYZ space, such that the chromaticity of all perceivable colours can be described using positive values.

Similar to how colours were projected on the rg plane in the RGB colour space, the spectral locus too can be projected on the xy plane in the CIE XYZ colour space:

![greyed out sliced plane X+Y+Z=1 space on top; another greyed out plane for X+Y+Z=k — k determined by wavelength parameter; 2d sliced plane for X+Y+Z=1 (NOT X+Y+Z=k) as another figure on right of cube — in the middle; rg plane on the right — right of separate sliced 2d plane figure — maybe make a smooth transition between xy-plane and X+Y+Z=1 plane; slider for wavelength of specteal colour; xyz values (non-adjustable, determined by wavalength parameter) as a stacked proportional horizontal bar chart type bar — https://media.geeksforgeeks.org/wp-content/uploads/20200923090400/1.PNG — but numerical values below; plot (X,Y,Z) on the X+Y+Z=k plane on the cube figure; plot (x,y,z) as points on the plane X+Y+Z=1 in the sliced plane cube figure, as well as the separate plane figure on the right — as well as the xy-plane diagram; in the cube figure include a faint line joining (0,0,0) to (X,Y,Z) passing through (x,y,z) to signify projection;](interactive)

{% tangent(summary="Meaning of xy", open=true) %}
The naming convention used in the CIE XYZ colour space to describe chromaticity is analagous to the naming convention used in the CIE RGB colour space. So, x = X/(X+Y+Z) and y = Y/(X+Y+Z).
{% end %}

The spectral locus projected on the xy plane results in a horseshoe like shape, which forms the outline of the [CIE xy chromaticity diagram](https://en.wikipedia.org/wiki/CIE_1931_color_space#/media/File:CIE1931xy_CIERGB.svg). Since the chromaticity of spectral colours can be represented using (x,y) — it stands to reason then that non-spectral colours can also be represented as a point in the xy chromaticity space. While in the rg chromaticity space it was easy to visualise the ratio of the intensity of the primaries, it is much harder to imagine how different ratios of the imaginary primaries translates to chromaticity. But since human color perception is nearly linear, it becomes easier to circumvent this issue.

{% tangent(summary="Colour perception linearity", open=false) %}
The near linearity of human colour perception is inferred from Grassman's laws.
{% end %}

If two points can define a line in the xy plane, a point on that line can be represented as the ratio of these two points:

![horseshoe curve on xy plane; line crossing through x,y axes; two points for selecting line — draggable on the xy plane — maybe make it so the line always lies inside positive (triangle quadrant?); point on line — determined by the ratio slider; two sliders for ratio of two primaries — sum is one — increasing one decreases the other; stacked horizontal bar chart type bars on right of sliders showing ratio of two primaries — on left of bar char bar the (x,y,z) coordinates of one draggable point — on right of bar the (x,y,z) coordinates of the other draggable point;](interactive)

The line can also [intersect the spectral locus](switch#below). Then, the point can also be represented as the ratio of the points on the spectral locus:

![same as above; but include new (keep the original bar) and separate stacked horizontal bar chart for ratio of showing spectral colour intensities — emphasize ratio of spectral intensities;](interactive)

But the points on spectral locus represent the chromaticity of monochromatic colours which can be physically perceived. Since colour perception is linear, the chromaticity of the point is the ratio of the intensity of the two monochromatic lights — but now can be represented using (x,y) values using the (x,y) coordinates of its constituent spectral colours.

In general, the chromaticity of all the points inside the spectral locus are non-spectral colours and their chromaticity can be represented as the ratio of intensity of other spectral colours. If the chromaticity of those colours are mapped in the xy plane, it results in the CIE xy chromaticity diagram:

![cie xy diagram without planckian locus and white points — just outline (with spectral locus wavelegnth labels — huge maybe) and chromaticity](static)

{% tangent(summary="CIE xyY colour space", open=true) %}
The CIE xy chromaticity diagram represents chromaticity, but not colours since there is no information about luminance. Adding a luminance component allows it to represent colours, forming a colours space. In the RGB colour space the luminance of a colour was approximated as the sum of the primaries, but in CIE XYZ space the luminance is already somewhat accurately described by the Y primary — which means it can be represented using the Y primary. The chromaticity (x,y) along with luminance Y forms the CIE xyY colour space.
{% end %}

The chromaticity outside the spectral locus are imaginary, but all the points inside contain the chromaticity of colours perceviable by an average human. Since the CIE xy chromaticity diagram can represent all perceivable chromaticities, it is often used for comparing other colour spaces.

{% tangent(summary="The xy plane to compare colour spaces", open=true) %}
The xy chromaticity diagram represents a *chromaticity* space, not a *colour* space. Using a chromaticity space to compare colour spaces is not perfectly accurate, since luminance information cannot be compared. However comparing chromaticity information is simpler, and sufficient in certain cases. For a more complete comparison of colour spaces, the CIE XYZ colour space is generally used as the standard reference instead.
{% end %}

## Gamut

The chromaticity of a colour can be described by the ratio of the intensity of two monochromatic colours. Conversely, two monochromatic light sources can produce colours having a chromaticity that lies on the line joining the corresponding two points in the CIE xy plane:

![similar diagram as the line joining xy plane with a point — line and point determined by sliders; make line endpoints un-draggable — instead determined by two sliders for wavelengths — endpoints would lie on spetral locus; two more sliders determines relative intensity of both primaries — increasing intensity of one decreases the other; stacked horizontal bar chart bar to show ratios of primaries;](interactive)

Adding a third monochromatic light allows for more combinations of ratios of among the primaries — greatly expanding the chromaticty of colours that can be recreated:

![xy plane with faint dotted triangle outline — vertices determined by sliders; make line endpoints un-draggable — instead determined by three sliders for wavelengths — vertices would lie on spetral locus; three more sliders determines relative intensity of primaries — increasing intensity of one decreases the other two — such that the ratio between the other two is preserved; stacked horizontal bar chart bar to show ratios of primaries; two solid distinct lines on xy plane and show final point as point on a line — and the line is determined by a point on another line — similar to https://graphics.stanford.edu/courses/cs148-10-summer/docs/2010--kerr--cie_xyz.pdf PAGE 13 — but make the point and lines adjustable using sliders;](interactive)

Using more sources of monochromatic light generally results in a bigger chromaticity space that can be physically recreated by the light sources:

![mostly same as above; but instead of triangle, a convex polygon — number of vertices (max 5, min 2) determined by checkboxes; same sliders as above, but five this time — unselecting the primary disables the slider and ratio bar (and sliders) gets accordingly reset;](interactive)

All the chromaticitiy points that lie outside the bounded [convex polygon](https://en.wikipedia.org/wiki/Convex_polygon) cannot be physically recreated, since it would involve creating light with negative intensity. The colours that can be physically created using the primaries is called its [gamut](https://en.wikipedia.org/wiki/Gamut).

The gamut of the CIE RGB primaries on the CIE xy chromaticity diagram would then look like this:

![xy plane with solid triangle outline — vertices fixed at CIE RGB primaries; three more sliders determines relative intensity of primaries — increasing intensity of one decreases the other two — such that the ratio between the other two is preserved; stacked horizontal bar chart bar to show ratios of primaries; two faint lines on xy plane and show point as point on a line — and the line is determined by a point on another line — similar to https://graphics.stanford.edu/courses/cs148-10-summer/docs/2010--kerr--cie_xyz.pdf PAGE 13 — but make the point and lines adjustable using sliders;](interactive)

{% tangent(summary="CIE RGB chromaticity gamut", open=true) %}
It has been frequently stated that the CIE RGB cannot reproduce certain colours and this is yet another representation of the same idea. Although in this case, the diagram represents the *chromaticities* that cannot be reproduced, instead of the exact colours.
{% end %}

Most screens do not use the CIE RGB primaries though, if any at all. It is economically efficient to use just three primaries — which are not purely monochromatic. Certain colour spaces are designed keeping such gamut constraints in mind, such as the [sRGB](https://en.wikipedia.org/wiki/SRGB) colour space or the [DCI-P3](https://en.wikipedia.org/wiki/DCI-P3) colour space.

![cie xy chromaticity diagram; triangles/convex polygons overlaid on top depending on colour space chosen; menu select for colour space;](interactive)

{% tangent(summary="Gamut vs colour space", open=true) %}
Gamut is different from colour spaces since it refers to the colours that can be physically recreated by an output device, while a colour space is simply a mathematical model used to describe colours. Colour spaces may arbitrarily restrict itself to certain values to more accurately represent physical and economic constraints.
{% end %}

Displays may have gamuts that span all of the sRGB space — but the sRGB space itself only covers around a small part of all perceivable chromaticities. This means the CIE xy chromaticity diagram on the screen it is being displayed is not a faithful representation of the actual xy chromaticity diagram since it is physically impossible for most displays to create colours with certain chromaticities.

## White Point

Back to some physical science — all bodies radiate photons, due to [blackbody radiation](https://en.wikipedia.org/wiki/Black-body_radiation). The spectral power distribution of the radiation is a [function of temperature](https://en.wikipedia.org/wiki/Planck%27s_law):

![black coloured spherical body radiating photons; spd below; slider for temperature bottom;](interactive)

The photons being emitted produces a response in the cones, which is perceived as a colour:

![spd on top — dependent on slider for temperature; another spd below — zoomed in on range 400nm-700nm — maybe show lines on above spd to indicate it is zoomed in view of the above spd; sensitivity curve graph of photoreceptor cells below; response curve of above two graphs below — shade the areas below with colour of photoreceptor type (rod=black,s=blue,m=greenish,l=yellowish-to-red); slider for temperature at bottom below all graphs; show amount of response of each type of receptors (rods and cones) as a sort of (progress/without sliding knob) bars on the right of the sliders for wavelength and intensity of photons; eg: https://jamie-wong.com/images/color/ConeExcitation1.png — combine all the three coloumns to one graph; keep rows separate; small colour box below or next to right to response (progress-like) bar, showing colors BUT NO colour names below the box; highlight response of cones progress bars and cones curves — by greying/reducing contrast of rods response progress bars, rods sensitivity curves, and rods response curves;](interactive)

The colours above have a corresponding chromaticity — and when mapped on the CIE xy chromaticity diagram, form the [planckian locus](https://en.wikipedia.org/wiki/Planckian_locus):

![cie xy chromaticity diagram with faint planckian locus (NO correlated colour temp lines) with correlated colour temperature lines; point on the locus — determined by temperature; reuse slider for temperature above;](interactive)

REVIEW FROM HERE ON:

The colour temperature is another way to describe certain colours and chromaticities — and is used since most sources of light have historically as a result of black body radiation. The sun at 6500K, or incandescent bulbs at 3000K produce blackbody radiation.

Most bodies however are not perfect blackbodies — the spectral power distribution. Also, [flourescent lights](https://en.wikipedia.org/wiki/Fluorescent_lamp#Color_temperature) — resulting in a different chromaticity point from incandescent lamps. But it is still useful to represent it as .

The lines that represent the [correlated colour temperature](https://en.wikipedia.org/wiki/Correlated_color_temperature) can also be mapped alongside the planckian locus:

![cie xy chromaticity diagram with planckian locus with correlated colour temperature lines](static)

Strict definitions There also exist [standard illuminants](https://en.wikipedia.org/wiki/Standard_illuminant) — theoretical sources of light with a definite spectral power distribution.

![spd for illuminants above; cie xy diagram with faint spectral locus below; point showing chromaticity for selected illuminant; radio buttons for selecting "Blackbody at 6500K" or "Standard Illuminant D65" etc below; NO small colour box on right](interactive)

While all the above points have different chromaticity values, [chromatic adaptation](https://en.wikipedia.org/wiki/Chromatic_adaptation) may make the colours look similar. It can also cause objects with different colours appear similar under different lighting conditions.

![cie xy chromaticity diagram;](interactive)

To adjust for chromatic adaptation, a standard [white point](https://en.wikipedia.org/wiki/White_point) can be specified using standard illuminants. Most colour spaces have D65 as the white point as D65 represents average daylight, having a correlated colour temperature of 6500K.

## Colour Science

Colours are an exteremly interesting topic, since it involves quantifying something that feels innately qualitative. So far, only [additive colour models](https://en.wikipedia.org/wiki/Additive_color) have been discussed. But there are also [other colour models](https://en.wikipedia.org/wiki/Color_mixing), like the [subtractive colour model](https://en.wikipedia.org/wiki/Subtractive_color) — which includes the [CMYK model](https://en.wikipedia.org/wiki/CMYK_color_model) that most people may be familiar with.

Most of these topics involve ways to [describe and recreate colours](https://en.wikipedia.org/wiki/Colorimetry). But there's also an entirely different branch of science that deals with the [psychology of colours](https://en.wikipedia.org/wiki/Color_psychology) — why certain [colour combinations](https://en.wikipedia.org/wiki/Color_scheme) appear pleasing, or how the [meaning of colours](https://en.wikipedia.org/wiki/Color_symbolism) vary among cultures. Or how colours can [affect other senses](https://en.wikipedia.org/wiki/Color_psychology#Influence_of_color_on_perception).

The subject of colours is vast — spanning various scientific domains from quantum physics and electromagnetism to physiology and psychology. This post is a very tiny fraction of what constitutes [colour science](https://en.wikipedia.org/wiki/Color_science).

---

## References

* Jamie Wong: [Color: From Hexcodes to Eyeballs](https://jamie-wong.com/post/color/)
* Bartosz Ciechanowski: [Color Spaces](https://ciechanow.ski/color-spaces/)
* Douglas A. Kerr: [The CIE XYZ and xyY Color Spaces](https://graphics.stanford.edu/courses/cs148-10-summer/docs/2010--kerr--cie_xyz.pdf)

<!--
Assign (switch#) links a class and make them distinct from other links.
maybe show values next to all sliders
-->

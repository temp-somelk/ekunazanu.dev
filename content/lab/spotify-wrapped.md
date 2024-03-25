+++
title = "Spotify Wrapped"
description = "Analyzing and visualizing six years of Spotify data."
date = 2024-12-06
draft = true
template = "article.html"
[extra]
type = "article"
thumbnail = "lab.spotify.svg"
thumbnailalt = "Spotify logo centered among a lot of green bubbles bubbles."
+++

This is one of the more experimental posts. . I'm consistently procrastinated a lot.

{{ loadData(path="/media/lab/spotify-wrapped/graph.svg") }}
{{ loadData(path="/media/lab/spotify-wrapped/graph.svg") }}
{{ loadData(path="/media/lab/spotify-wrapped/graph.svg") }}
{{ loadData(path="/media/lab/spotify-wrapped/graph.svg") }}
{{ loadData(path="/media/lab/spotify-wrapped/graph.svg") }}
{{ loadData(path="/media/lab/spotify-wrapped/graph.svg") }}

<svg height="1rem" viewBox="0 0 10 1" fill="none">
<rect width="1" height="1" x="0" y="0" fill="#E5E5EF" />
<rect width="1" height="1" x="1" y="0" fill="#DAC8DB" />
<rect width="1" height="1" x="2" y="0" fill="#D3ACC8" />
<rect width="1" height="1" x="3" y="0" fill="#D394B7" />
<rect width="1" height="1" x="4" y="0" fill="#D07BA4" />
<rect width="1" height="1" x="5" y="0" fill="#B16794" />
<rect width="1" height="1" x="6" y="0" fill="#91638F" />
<rect width="1" height="1" x="7" y="0" fill="#6E5480" />
<rect width="1" height="1" x="8" y="0" fill="#4B3B66" />
<rect width="1" height="1" x="9" y="0" fill="#2E214D" />
</svg>

* Selection menu for:
    * Top Artists. Use similar color for similar artists — pehaps sorted by artist genre.
    On hover: Top 5 artists of day, based on:
        * Time listened
        * Number of times played
    Submenu for viewing certain top artist — time per day — same colors — below main selection menu.
    * Top Songs. Use similar color for similar songs — pehaps sorted by artist genre.
    On hover: Top 5 songs based on:
        * Time listened
        * Number of times played
    Submenu for viewing certain top song — time per day — same colors — below main selection menu.
    * Genre — Colorscale legend at the bottom, above the selection menu.
    On hover: Top 5 genres of day based on:
        * Genre breakdown for the day (proportional line chart — like a pie chart but using a line). Legend shown below
    * Mood — Colorscale legend at the bottom, above the selection menu. Blue for sad, orange for upbeat.
    On hover: Top 5 genres of day based on:
        * Moodiness score of top 5 songs for the day (based on time listened)
        * Number of sad songs listened on that day
        * Number of upbeat songs listened on that day
    * Times listened — Colorscale legend at the bottom, above the selection menu.
    On hover:
        * 24 dots arranged as (8-12 morning, 12-16 daytime, 16-20 evening, 20-0 night, 0-4 late night, 4-8 ultra late night) with same colors, signifying hours.
    Time per hour — Slider for selecting hour+an overall for the day option, above the selection menu. No hover if hour is selected.

On hover show date regardless of menu option. Maybe use diving lines on date graph to differentiate months.

https://observablehq.com/@observablehq/plot-calendar

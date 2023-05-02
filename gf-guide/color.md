<link href="style.css" rel="stylesheet">

<a href="./index"><button class="button button-i">&larr; GF Guide Index</button></a>

# Color fonts specifics
{:.no_toc}

<div class="callout">

<br><br>
This guide will give users all the detailed information related to Color fonts GF requirements.
</div>

<div class="context-reading">
    Background reading:<br>
    <mark class="green"><b>must&rarr;</b></mark> <a href="./requirements" style="font-weight:bold">Overall font requirements</a><br>
    <mark class="green"><b>must&rarr;</b></mark> <a href="https://developer.chrome.com/blog/colrv1-fonts/" style="font-weight:bold">https://developer.chrome.com/blog/colrv1-fonts/</a>
</div>

## Table of contents
{:.no_toc}
* TOC goes here
{:toc}

## Requirements

* The font must support the `COLR` table.
   * It can use COLR v0 or COLR v1.
* If the font is static it must have an SVG table equivalent to the COLR table
   * Add SVG to a font with COLR, or vice versa, using [maximum_color](https://github.com/googlefonts/nanoemoji#adding-color-tables-to-existing-fonts) from nanoemoji
* If the font is variable it must *not* have an SVG table

## Useful links

* https://developer.chrome.com/blog/colrv1-fonts/ - introduces COLRv1
* https://fonts.google.com/?coloronly=true - open source color fonts
* https://github.com/googlefonts/nanoemoji - compiles SVGs to color fonts

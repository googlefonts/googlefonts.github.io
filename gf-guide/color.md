<link href="style.css" rel="stylesheet">

<a href="./index"><button class="button button-i">&larr; GF Guide Index</button></a>

# Color fonts specifics
{:.no_toc}

<div class="callout">
This guide will give users all the detailed information related to Color fonts GF requirements.
</div>

<div class="context-reading">
    Background reading:<br>
    <mark class="green"><b>must&rarr;</b></mark> <a href="./requirements" style="font-weight:bold">Overall font requirements</a><br>
</div>

## Table of contents
{:.no_toc}
* TOC goes here
{:toc}

## Requirements

### Design

* The default palette should be high contrast for white and black backgrounds, to pass accessibility color contrast requirements. Ideally there are at least 3 palettes, the default being general purpose, one for black ground and one for white ground, and those can have flags for dark mode and light mode.

### Technical

* The font must support the `COLR` table.
   * It can use COLR v0 or COLR v1.
* If the font is static and uses COLR v1 it must have an SVG table equivalent to the COLR table
   * Add SVG to a font with COLR, or vice versa, using [maximum_color](https://github.com/googlefonts/nanoemoji#adding-color-tables-to-existing-fonts) from nanoemoji
   * COLR v0 is widely supported; SVG is not required for COLR v0 fonts
* If the font is variable it must *not* have an SVG table (because SVG does not support OpenType Variations).

## Useful links

* [Introduction to COLRv1 on the Chrome blog](https://developer.chrome.com/blog/colrv1-fonts/)
* [Introduction to COLRv1 by Simon Cozens](https://simoncozens.github.io/colrv1-rocks/)
* [Open source color fonts on GF]([https://fonts.google.com/?coloronly=true](https://fonts.google.com/?categoryFilters=Technology:%2FTechnology%2FColor))
* [Nano Emoji](https://github.com/googlefonts/nanoemoji) (compiles SVGs to color font)

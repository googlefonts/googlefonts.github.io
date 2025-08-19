<link href="style.css" rel="stylesheet">

<a href="./index"><button class="button button-i">&larr; GF Guide Index</button></a>

# The font tables explained
{:.no_toc}

<div class="callout">

Understanding the what are the font tables and what they do is a core skill in font engineering.
<br><br>
<b>You can view the name tables using these tools:</b>
<ul>
    <li><a href="https://glyphsapp.com/tools/fonttableviewer" target="_blank">Font Table Viewer</a></li>
    <li><a href="https://www.fontmaster.nl/otmaster.html" target="_blank">DTL OT Master</a></li>
    <li><a href="https://fonttools.readthedocs.io/en/latest/ttx.html" target="_blank">ttx</a>, a practical command line tool of <a href="https://github.com/fonttools/fonttools" target="_blank">fonttools</a></li>.
</ul>
<b>Some font testing web pages allow you to view a selection of tables:</b>
<ul>
    <li><a href="https://fontdrop.info/#">fontdrop</a> → in the “data” tab</li>
    <li><a href="https://fontgauntlet.com">fontgauntlet</a> → if you click on the small search icon next to the font name</li>
</ul>

</div>

## Table of contents
{:.no_toc}
* TOC goes here
{:toc}

## Required tables

-   `cmap` Character to glyph mapping
-   `head` Font header
-   `hhea` Horizontal header
-   `hmtx` Horizontal metrics
-   `maxp` Maximum profile
-   `name` Naming table
-   `OS/2` OS/2 and Windows specific metrics
-   `post` PostScript information

## TT outlines tables

-   `cvt `Control Value Table (optional table)
-   `fpgm` Font program (optional table) 
-   `glyf` Glyph data
-   `loca` Index to location
-   `prep` CVT Program (optional table)
-   `gasp` Grid-fitting/Scan-conversion (optional table)

## CFF outlines tables

-   `CFF `Compact Font Format 1.0
-   `CFF2` Compact Font Format 2.0
-   `VORG` Vertical Origin (optional table)

## SVG outlines tables

-   `SVG `The SVG (Scalable Vector Graphics) table

## Bitmap glyphs tables

-   `EBDT` Embedded bitmap data
-   `EBLC` Embedded bitmap location data
-   `EBSC` Embedded bitmap scaling data
-   `CBDT` Color bitmap data
-   `CBLC` Color bitmap location data
-   `sbix` Standard bitmap graphics

## Advance typographic tables

-   `BASE` Baseline data
-   `GDEF` Glyph definition data
-   `GPOS` Glyph positioning data
-   `GSUB` Glyph substitution data
-   `JSTF` Justification data
-   `MATH` Math layout data

## VF Tables

-   `avar` Axis variations
-   `cvar` CVT variations (TrueType outlines only)
-   `fvar` Font variations
-   `gvar` Glyph variations (TrueType outlines only)
-   `HVAR` Horizontal metrics variations
-   `MVAR` Metrics variations
-   `STAT` Style attributes (required for variable fonts, optional for non-variable fonts)
-   `VVAR` Vertical metrics variations

## Color fonts tables

-   `COLR` Color table
-   `CPAL` Color palette table
-   `CBDT` Color bitmap data
-   `CBLC` Color bitmap location data
-   `sbix` Standard bitmap graphics
-   `SVG `The SVG (Scalable Vector Graphics) table

## Other opentype tables

-   `DSIG` Digital signature
-   `hdmx` Horizontal device metrics
-   `kern` Kerning
-   `LTSH` Linear threshold data
-   `MERG` Merge
-   `meta` Metadata
-   `STAT` Style attributes
-   `PCLT` PCL 5 data
-   `VDMX` Vertical device metrics
-   `vhea` Vertical Metrics header
-   `vmtx` Vertical Metrics

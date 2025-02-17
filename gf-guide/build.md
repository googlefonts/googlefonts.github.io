<link href="style.css" rel="stylesheet">

<a href="./index"><button class="button button-i">&larr; GF Guide Index</button></a>

# Build the fonts
{:.no_toc}

<div class="callout">

🦕 Because of our commitment to <a href="./cuture">Libre font culture</a>, all Google Fonts projects must be built using a reproducible, libre toolchain. We do not onboard binaries exported from font editors.

This chapter aims to guide designers in building their font binaries using open-source tools as per our production requirements. Everything related to font file settings is detailed in the <a href="https://googlefonts.github.io/gf-guide/index#pre-production-getting-your-fonts-ready-for-gf">Pre-production</a> section of this guide, and for practicality, that information will not be repeated here.
<br><br>
 If you read “you should follow the recommendation” or “respect the requirements” etc, please refer to the chapters labeled <mark class="blue">start</mark> and <mark class="green"><b>must&rarr;</b></mark> in the <b>Pre-production: Getting your fonts ready for GF</b> section of this guide. You will have a better understanding of the following guidelines if you have read them first.
<br><br>
We recommend you install all the tools in a virtual environment, to avoid conflict between packages. Further information is detailed in the <a href="./tools">Tools and Dependencies</a> section. 
<br><br>
For the rest of this chapter, it would be better if you have basic knowledge of:
<ul>
  <li>Font tables and font formats</li>
  <li>Command line tools</li>
</ul>

</div>

<div class="context-reading">
    Background reading:<br>
    <mark class="blue">start</mark> <a href="./tools" style="font-weight:bold">Tools and Dependencies</a>
    <br>
    <mark class="green"><b>must&rarr;</b></mark> <a href="https://googlefonts.github.io/gf-guide/index#pre-production-getting-your-fonts-ready-for-gf" style="font-weight:bold">Pre-production: Getting your fonts ready for GF</a> 
    <br>
    <mark class="green"><b>must&rarr;</b></mark> <a href="./production" style="font-weight:bold">Production requirements</a>

</div>

## Table of contents
{:.no_toc}
* TOC goes here
{:toc}

## Fontmake

[Fontmake](https://github.com/googlefonts/fontmake) is a tool to generate font binaries. Run `fontmake --help` to see all the options.

Fontmake makes use of a variety of Python libraries to build TTF fonts from UFO or Glyphs source files:

-   [glyphsLib](https://github.com/googlefonts/glyphsLib) to convert `.glyphs` files into UFO format;
-   [ufo2ft](https://github.com/googlefonts/ufo2ft) to turn the UFOs into FontTools objects;
-   [fonttools](https://github.com/fonttools/fonttools) is responsible for exporting the actual font binaries.

You don’t have to understand this very well to start working with the tools, but it can come in handy if you have a bug to report, or if you want to understand the relationship between the different libraries. See “[What happens when you build a variable font (using the open source tool chain)](https://simoncozens.github.io/compiling-variable-fonts/)” for more details.

## gftools

Unfortunately, Fontmake is not enough to generate fonts that can be onboarded to Google Fonts. Some post-processing is needed to meet Google Fonts requirements. The `gftools` scripts are an enhanced collection of helpers to do that post-processing.

Run `gftools --help` to see the available scripts.

These scripts are extremely useful to batch patch binaries (as well as UFO).

### gen-stat

You can use for example `gftools gen-stat` to easily patch a `STAT` table to your variable font:

``` code
gftools gen-stat path/to/*.ttf --src stat.yaml --inplace
```

`--inplace` would be to override the font files, `--src` would be to use an external `yaml` file with axis values instructions, for example:

``` code
# stat.yaml
- name: Width
  tag: wdth
  values:
  - name: Condensed
    value: 75
  - name: Normal
    value: 100
- name: Weight
  tag: wght
  values:
  - name: Regular
    value: 400
    linkedValue: 700
        flags: 2
  - name: Bold
    value: 700
```

If you need to patch a different STAT table on separated fonts of the same family—for example in the case of Italic—you can add file name information, such as:

``` code
# stat.yaml
Fontname[wght].ttf:
- name: Weight
  tag: wght
  values:
  - name: Regular
    value: 400
        flags: 2
- name: Italic
    tag: ital
    - name: Regular
        value: 0
    linkedValue: 1
        flags: 2
Fontname-Italic[wght].ttf:
- name: Weight
  tag: wght
  values:
  - name: Regular
    value: 400
- name: Italic
    tag: ital
    - name: Italic
        value: 1
```

## The build script

Google Fonts has a policy of building all exports in one step to simplify the font generation process. To generate the font with Fontmake, and then post-process the binaries with some `gftools` scripts, users often created a bash shell script.

Example: [Public Sans](https://github.com/uswds/public-sans/blob/c5d5d314758605ded9aa27940de7ab841529dff5/sources/build-font.sh)

As you can see in the example, these build scripts were extremely long and redundant. That is why `gftools builder` was created.

## gftools builder

[gftools builder](https://github.com/googlefonts/gftools/blob/main/Lib/gftools/builder/__init__.py) is a command line tool that wraps [Fontmake](https://github.com/googlefonts/fontmake) to efficiently generate several font formats in one command, as well as several `gftools fix-*` and `gftools gen-stat` scripts to post-process the generated fonts following Google Fonts’ specifications.

Run `gftools builder --help` to see all the options.

### Usage from the CLI

The Builder can take source files (`.glyphs`, `.ufo`, `.designspace`) as direct argument.

You can do that if:

-   Any variable axes in your font are registered in the [GF Axis Registry](https://github.com/googlefonts/axisregistry).
-   The axis values match with the [GF Axis Registry](https://github.com/googlefonts/axisregistry)’s axis definition.
-   The instances are set up as recommended.
-   The file name follows Google recommendations.

Example:

``` code
gftools builder FontName.glyphs FontName-italic.glyphs
```

This will generate Static `OTF`, `TTF`, `WOFF2` and `Variable TTF`, using the Axis Registry to set up the `STAT` table.

Using a `yaml` file with more detailed instructions is a preferred option to have more control over the outcome. Once this “config” file is set up, you would just have to run, for example:

``` code
gftools builder config.yaml
```

### Config file for a simple font

For Example: [JetBrains Mono](https://github.com/JetBrains/JetBrainsMono/blob/master/sources/config.yaml)

-   The font is using [Axis Registry](https://github.com/googlefonts/axisregistry)’s axes and axes location.
-   You are happy with a STAT format 3.
-   The repository respects the upstream repo structure.
-   The font files are set up following the GF guidelines.

``` code
# config.yaml
sources:
    - FontName[axis].glyphs
    - FontName-Italic[axis].glyphs
axisOrder:
    - wght
    - ital
familyName: "Font Name"
```

Google Fonts only needs `TTF` fonts, so you can avoid building OTF as well by adding:

``` code
buildOTF: false
```

→ Note that the `ital` axis shouldn’t be in the source files if the Roman is separated for from the Italic. Although, the axis order is here to describe the entire design space of the family, so the `ital` should be mentioned to properly set up the style linking between the two files, as well as a complete `STAT` table.

### Config file for a complex font

For example: [Texturina](https://github.com/Omnibus-Type/Texturina/blob/master/sources/config.yaml), [Montserrat](https://github.com/googlefonts/Montserrat/blob/master/sources/config.yml), [Roboto Serif](https://github.com/googlefonts/roboto-serif/blob/main/sources/config.yml).

-   **If there is a non-registered axis or there is an Optical Size axis**, you would have to detail the STAT table information because, in that case, the Axis Registry can’t be used:

    ``` code
    sources:
        - FontName[opsz,wght].glyphs
        - FontName-Italic[opsz,wght].glyphs
    axisOrder:
        - opsz
        - wght
        - ital
    FamilyName: "Font Name"
    stat:
      FontName[opsz,wght].ttf:
      - name: Optical size
        tag: opsz
        values:
        - name: 12pt
          value: 12
        - ...
      - name: Weight
        tag: wght
        values:
        - name: Regular
          value: 400
          linkedValue: 700
          flags: 2
        - ...
        - name: Bold
          value: 700
      - name: Italic
        tag: ital
        values:
        - name: Roman
          value: 0
          linkedValue: 1
          flags: 2
      FontName-Italic[opsz,wght].ttf:
      - name: Optical size
        tag: opsz
        values:
        - name: 12pt
          value: 12
        - ...
      - name: Weight
        tag: wght
        values:
        - name: Regular
          value: 400
          linkedValue: 700
          flags: 2
        - ...
        - name: Bold
          value: 700
      - name: Italic
        tag: ital
        values:
        - name: Italic
          value: 1
    ```
-   **If you want a STAT table format 2** (min and max ranges) your axis value should look like this:

    ``` code
    stat:  
        - name: Width
            tag: wdth
            values:
            - name: Condensed
              rangeMinValue: 40
              nominalValue: 50
              rangeMaxValue: 75
                ...
    ```
-   **If you want a STAT table format 4** (multi axes) you should add this after defining the axes, at the same level as the “normal” stat definition:

    ``` code
    stat:
    …
    statFormat4:
          - name: Green
            location:
              wght: 300
              wdth: 200
          - name: Blue
            location:
              wght: 400
              wdth: 200
    ```
-   **If there is a VTT manual hinting program** you should add this to this example:

    ``` code
    vttSources:
      FontName[opsz,wght].ttf: VTT/roman-hinting.ttx
      FontName-Italic[opsz,wght].ttf: VTT/italic-hinting.ttx
    ```
-   **If you want to set up static instances**, different from the one set up in your `.designspace` file or in your `.glyphs` sources:

    ``` code
    instances:
      FontName[opsz,wght].ttf:
        - familyName: "FontName 8pt"
          styleName: "Regular"
          coordinates:
            opsz: 8
            wght: 400
        - familyName: "FontName 8pt"
          styleName: "Medium"
          coordinates:
            opsz: 8
            wght: 500
    ```

------------------------------------------------------------------------

## Useful tools

Unfortunately, the Builder can’t do everything yet. You will have to use an external bash script in these cases:

-   To slice a variable font. use **[Fonttools’ varLib instancer](https://fonttools.readthedocs.io/en/latest/varLib/instancer.html)**.
-   To generate `WOFF`. use **[homebrew webfont tools](https://github.com/bramstein/homebrew-webfonttools)**.
-   To hint OTF: use **[AFDKO](https://github.com/adobe-type-tools/afdko)**.
-   To subset the font: use **[Fonttools’ subsetter](https://fonttools.readthedocs.io/en/latest/subset/index.html)**.
-   If you are using any other font format than `.glyphs`, `.glyphspackage`, and `.ufo`: the build script should contain a step that converts the sources to UFO. Use **[Fontlab to UFO](https://pypi.org/project/vfb2ufo3/)** or **[FontForge to UFO](https://github.com/fontforge/sfd2ufo)** for example.

<div class="next-reading">
    Further reading:<br>
    <mark class="green"><b>must&rarr;</b></mark> <a href="./statics" style="font-weight:bold">Static fonts specifics</a>
    <br>
    <mark class="green"><b>must&rarr;</b></mark> <a href="./metrics" style="font-weight:bold">Vertical metrics</a>
    <br>
    <mark class="green"><b>must&rarr;</b></mark> <a href="./testing" style="font-weight:bold">QA - Local testing</a>
</div>

<link href="style.css" rel="stylesheet">

<a href="./index"><button class="button button-i">&larr; GF Guide Index</button></a>

# Variable fonts specifics
{:.no_toc}

<div class="callout">

🦥 The variable font technology has existed for a long time, but the format is actually quite recent (2016). It took time for OS and Apps to support this format, and some still did not make the step. In general, GF does not quite recommend the use of variable fonts in documents made to be printed.
<br><br>
This guide will give users all the detailed information related to Variable fonts GF requirements. If you are developing a <em>Static</em> font project, please refere to the specifics on statics section.

<!-- Before proceeding, make sure:

<ul>
  <li>you read the <a href="https://googlefonts.github.io/gf-guide/requirements.html">requirements for all font files</a></li>
  <li>you read the specific <a href="https://googlefonts.github.io/gf-guide/statics.html">requirements for static fonts</a></li>
</ul> -->
</div>

<div class="context-reading">
    Background reading:<br>
    <mark class="green"><b>must&rarr;</b></mark> <a href="./requirements" style="font-weight:bold">Overal font requirements</a>
</div>

## Table of contents
{:.no_toc}
* TOC goes here
{:toc}

## New vs Pre-existing fonts

### The family doesn't exist on Google Fonts:

-   The `wght` axis range must include `400`. For example: `100-900`, `400-900`, `100-400`.
-   Other than the above, fonts must conform to the requirements below, like pre-existing fonts.

### The family already exists on Google Fonts

In addition to complying with the requirements listed in the [**New additions & Upgrading fonts**](onboarding.md) section:

-   `Name ID 6` should be preserved if possible.
-   Every style that was already available on Google Fonts must be included as an instance in the `fvar` table.
-   Hinting should match as closely as possible. If `ttfautohint-vf` produces bad results, we can release the family unhinted.
-   A good rule to consider is that users should be able to swap the old family with the new VFs and not notice any differences.

## Variable Font filenames

Font file names must be based on the following schema:

-   Suffixes like `VF` or `VAR` or any other *must not* be appended to the file name. Instead the axes are appended in between brackets:

    `FamilyName[axis1,axis2].ttf` e.g. `Montserrat[wdth,wght].ttf`
-   Axes should be listed in alphabetical order (but `wght` always last).
-   If your font contains unregistered axes not found in the [Microsoft registered axes](https://docs.microsoft.com/en-us/typography/opentype/spec/dvaraxisreg), they should be capitalized and be listed first (alphabetically). 
 
    e.g. `Montserrat[GOOF,VEST,wdth,wght].ttf`
-   If the family consists of two VFs, one for Italic, the other for Roman, the fonts should be named: 
  
    e.g. `Montserrat[axis1,axis2...].ttf` and `Montserrat-Italic[axis1,axis2...].ttf`

## Font (zero) origin

A variable font is simply a static font that has some additional tables FVAR, GVAR etc. These new tables allow text clients to visually alter the font so it has a different appearance to end-users.

Type designers tend to conceive of the variable font as consisting of a bunch of “master fonts” which can then be interpolated between. But in fact, there is only a single master, and what the designer thinks of as additional masters are just sets of instructions to move points around (the famous delta points). That single master is the *font origin*, or in the OpenType Specification the *zero origin*.

Often font developers are unaware of what the font origin is within their fonts. They will then complain that Fontbakery is failing many checks. It is recommended that font developers read the [Microsoft OpenType Font Variations Overview](https://docs.microsoft.com/en-us/typography/opentype/spec/otvaroverview) to better understand how a variable font works.

The important thing to know is that the font origin will be the actual default instance displayed in environments that don’t support the variable font format (and the only accessible instance for some other). For example, if the font origin of the font is the `Thin` style, then in some environments, only the `Thin` instance will be displayed. GF tends to seek consistency between the name and the displayed font: so the full name of the variable font would be `Font Name Thin`. That way, if variable font specific tables are to be removed, the resulting static font would have matching bits and name records.

It often happens that designers are annoyed by that. The only way to work around that is to add a `Regular` master and make it the zero origin of the font or to modify directly the name tables. We do not recommend any of those tricks; the first one will increase the file size (if you don’t strictly need a Regular master for your design), and the second one will create an inconsistency between the style displayed by default and the style name.

## Axis Registry

The [Axis Registry](https://github.com/googlefonts/axisregistry) is now a Python module and has its own repository. All related issues should be opened there.

### Supported Axes

Google Fonts supports all the [Microsoft registered axes](https://docs.microsoft.com/en-us/typography/opentype/spec/dvaraxisreg) for variable fonts. To follow their convention, MS supported axis tags should be written in lowercase using their convention, and tags of the unsupported ones should be written in capitals.

For example, the Weight axis tag is by convention `wght`, and a custom axis that we would call “Jump” could have the following tag: `JUMP`.

GF has its own [Axis Registry](https://github.com/googlefonts/axisregistry), which defines the names and ranges of additional axes supported by the API. This registry is used to generate the static instances of each variable family (which you can find in the downloadable zip file); the API will generate only those locations registered in the registry.

For example, if your VF has a `JUMP[0-100]` axis, which is supposed to fall back to `Down[0]` and `Up[100]` styles, the API would be able to generate such static instances *only* if the Axis Registry contains a definition of a “Jump” axis.

### Unsupported Axes

To provide a consistent user experience, GF cannot publish fonts with unsupported custom axes. Too great is the chance of a similar axis being accepted later under a different name with live fonts being subject to regressions.

The requirements and principles of axis definition have been established mainly by a cross-functional group of fonts team members by Q3 2022 and have been documented in the [Axis Registry Protocol](./axis-registry.md). If you want to see a custom axis of yours added, please refer to the protocol for detailed information on the requirements and process.

<!-- If you want to see an axis of yours added, you can use the `gftools add-axis` script to generate a template of axis definition and submit it to GF through the issue tracker. -->

You can submit your fonts without the unsupported custom axis simply by stripping it of the axis at the binary font level rather than removing it in the sources, using *fonttools*’ instancer.

This example removes the `CNTR` axis:

``` code
fonttools varLib.instancer -o "fonts/variable/Akshar[wght].ttf" CNTR=0 "fonts/variable/Akshar[CNTR,wght].ttf"
```

Once a new axis has been accepted into GF’s Axis Registry, you may submit an update of your font containing the new axis.

## Most common axes

Any new variable font with a weight or width axes will need the instance’s coordinate values to match the conventional [usWeightClass](https://docs.microsoft.com/en-us/typography/opentype/spec/os2#usweightclass) and the [usWidthClass](https://docs.microsoft.com/en-us/typography/opentype/spec/os2#uswidthclass) of the said instances. In order to do so you will probably need to set up an axis mapping (process described below).

### `wght`

[MS Spec wght info](https://docs.microsoft.com/en-us/typography/opentype/spec/dvaraxistag_wght)

| name       | wght coordinate value |
|------------|----------------------:|
| Thin       |  100                  |
| ExtraLight |  200                  |
| Light      |  300                  |
| Regular    |  400                  |
| Medium     |  500                  |
| SemiBold   |  600                  |
| Bold       |  700                  |
| ExtraBold  |  800                  |
| Black      |  900                  |
| ExtraBlack | 1000                  |

### `wdth`

[MS Spec wdth info](https://docs.microsoft.com/en-us/typography/opentype/spec/dvaraxistag_wdth)

| name           | wdth coordinate value |
|----------------|----------------------:|
| UltraCondensed |  50.0                 |
| ExtraCondensed |  62.5                 |
| Condensed      |  75.0                 |
| SemiCondensed  |  87.5                 |
| Normal         | 100.0                 |
| SemiExpanded   | 112.5                 |
| Expanded       | 125.0                 |
| ExtraExpanded  | 150.0                 |
| UltraExpanded  | 200.0                 |

### `opsz`

[MS Spec opsz info](https://docs.microsoft.com/en-us/typography/opentype/spec/dvaraxistag_opsz)

| name | opsz coordinate value |
|------|----------------------:|
| Xpt  |                     X |
|      | between 5 and 1200     |

X can be any **integer number value** within the minimum (5) and maximum (1,200) as defined in the [Google Fonts Axis Registry](https://github.com/googlefonts/axisregistry) for the [Optical Size](https://github.com/google/fonts/blob/main/axisregistry/Lib/axisregistry/data/optical_size.textproto#L6-L7) axis.

The default value should not be elided in the STAT table (#83).

Named sizes like "Display", "Text", "Micro" etc are not allowed, because they are imprecise and inconsistent.

As of May 2023, the download ZIPs available from fonts.google.com will only create just 2-5 sets of static fonts from your optical size range, using values in the axis registry, and a "clamping" heuristic codenamed the "green dot algorithm." It is helpful for users to have the same named styles available as static fonts in the ZIP also available as named styles in the STAT table.

### `ital` **/** `slnt`

GF only supports the `ital` axis as a boolean (`0`/`1`) value to link two separate VFs (Roman/Italic) in the STAT table. And slant axis if the font is not meant to have italic instances.

**→ GF doesn’t support the ital axis within one VF as a variation axis.***

So if you have one VF with `slant` or `ital` axis, it won’t have italics served by GF API. If you want italic instances served by the GF API, then you will have to deliver **two variable font files**.

e.g. `Texturina[wght].ttf` and `Texturina-Italic[wght].ttf`

Style linking between these two files will be preserved by:

-   The [post-script name ID 25](https://adobe-type-tools.github.io/font-tech-notes/pdfs/5902.AdobePSNameGeneration.pdf) for Adobe Indesign, which (for now) requires this scheme: `FontName` for the Roman font, and `FontNameItalic` for the Italic font. The [Builder](build.md) will set that up for you using default settings and/or your STAT table values.
-   The `ital` axis in the `STAT` table.
-   The italic style bits in the `head` and `OS/2` table
-   The italic angle value in the `post` table.

## Design space

A set of axes form a "design space" and you should understand this concept. You can read these articles to get familiar with it:

-   [Superpolator’s article about design space](https://superpolator.com/designspace.html)
-   [Simon Cozen’s article about user-space and design-space](https://simoncozens.github.io/userspace-and-designspace)
-   [Fontlab’s article about variable fonts](https://help.fontlab.com/fontlab/7/manual/Variable-Fonts/)

### The Axis Mapping

Be careful to the following because this is confusing for designers who don’t have a broad understanding of web and software engineering.

As a designer, you map your masters and instances to **design(space) coordinates** that fit your process. This is personal to the design process.

As an example, you could choose stem thicknesses to map your styles on the weight axis:

| Style name | Design coordinates |
|------------|--------------------|
| Light      | 30                 |
| Regular    | 40                 |
| Bold       | 70                 |

The font file though should display values that make sense to *users and softwares*, these are the **user(space) values**. A user shouldn’t have to dig into a font binary file to find the location of common styles, so for example, on the weight and the width axis, these values are *standardized.* They should refer to the [usWeightClass](https://docs.microsoft.com/en-us/typography/opentype/spec/os2#usweightclass) (”us” as in “user”) and the [usWidthClass](https://docs.microsoft.com/en-us/typography/opentype/spec/os2#uswidthclass) of the [OS/2 table](https://docs.microsoft.com/en-us/typography/opentype/spec/os2). Indeed these values are the ones used on the web and in desktop app to select styles. Be also aware that most foundries will rip out the name tables from webfonts to make them unusable on desktop app. The only values remaining to select a style would then be the user values.

See some [CSS properties](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Fonts/Variable_Fonts_Guide#introducing_the_variation_axis) that a developer would use, whatever the actual style name you gave to your instance:

<div class="indented">

-   <code>font-style: normal;</code> → will select the style at <code>400</code><br>
-   <code>font-weight: bold;</code> → will select the style at <code>700</code><br>
-   <code>font-weight: 500</code> → a “Medium” weight style is expected.<br>
-   <code>font-variation-settings: 'wght' 300 'wdth' 75</code> → Condensed Light instance expected.<br>
  
</div>

This is known by developers and software engineers who are supposed to have read the [OT Spec](https://docs.microsoft.com/en-us/typography/opentype/spec/) (which are rules for machines to support the OpenType font format) to know how to implement font support (or some guidelines summarizing them).

If an axis of the [MS Registered Axis](https://docs.microsoft.com/en-us/typography/opentype/spec/dvaraxisreg) doesn’t follow the values and names, then the font is considered as invalid, and a user may not be able to use it on their machine.

To follow our previous example, we then should have these user values:

| Style name | User values |
|------------|-------------|
| Light      | 300         |
| Regular    | 400         |
| Bold       | 700         |

The **Axis Mapping** is here to make the conversion between the user values (also called referred as “input”) and design coordinates (also referred as “output”).

For example, if a user enter `400` to get a `Regular` style, the font file should return the design at the location `40`. Don’t worry, also developpers finds the input/output logic a bit counter-intuitive.

| Style name | User values / input | Design coordinates / output |
|------------|---------------------|-----------------------------|
| Light      | 300                 | 30                          |
| Regular    | 400                 | 40                          |
| Bold       | 700                 | 70                          |

This is what it would look like in a `.designspace` file:

``` code
<axes>
    <axis tag="wght" name="Weight" minimum="300" maximum="500" default="400">
      <map input="300" output="30"/>
      <map input="400" output="40"/>
      <map input="700" output="70"/>
    </axis>
  </axes>
```

Note that style names are not even mentioned.

For custom axes of your own invention, you can do whatever makes sense to you. Although you are never safe from a new axis being registered, or becoming conventional. You should always make further research to see if there is already some common practices ([see GRAD axis](https://fonts.google.com/knowledge/glossary/grade_axis)).

The axis mapping is set up in Glyphs using the `Axis Location` parameter (has to be set in all masters and intermediate instances). Although Google Fonts Tools decided not go with it, to the benefit of the `Axis Mapping` parameter that is less redundant and oblige to a consistent approach.

<figure>
<img src="images/variable/Capture_d_ecran_2023-03-28.png" style="width:1982px" alt="Axis Mapping parameter in GlyphsApp 3.2"/>
</figure>

Since version 3.2, GlyphsApp has been using **internal coordinates** as **design values** (output), and **external coordinates** as **user values** (input). Which is the opposite of how they were handling it before; designer may need to reverse there Axis Mapping when they upgrade.

Now that we have a better understanding of the axis mapping concept, let’s see the three tables linked to the axis mapping that are particularly important to translate correctly the design space: the `AVAR`, the `STAT`, the `FVAR` tables.

### The `AVAR` table

[MS Spec avar table info](https://docs.microsoft.com/en-us/typography/opentype/spec/avar)

This table normalizes the progression of the interpolation of one axis on a scale `-1:1`, the location of the font-origin being `0` (zero-origin). Basically, it takes the axis mapping and convert it so `max location = 1`, `default location = 0`, `min location = -1`.

The `AVAR` has two goals:

-   It changes the “pace” of the interpolation.
-   It allows the interpolation of instances following a *non-linear* progression.

To have a better understanding of these two complicated concepts, you can read the articles:

-   [Lucas de Groot’s interpolation theory](https://www.lucasfonts.com/learn/interpolation-theory)
-   [Glyphs’s Axis Mapping and Location](https://glyphsapp.com/learn/creating-a-variable-font#g-axis-mappings-and-locations)
-   [Underware foundry’s HOI concept](https://underware.nl/case-studies/hoi/)

**Example: linear interpolation**

In the case of a linear interpolation, normalised design and user values on a `-1:1` scale are **the same**. An `avar` table in that case is useless and is therefore not exported. Since the interpolation is “linear” all the design space, a simple cross product allows a software to find the location of interpolated instances.

<div id="58670f19-9bef-4b47-806e-bdbb85be6cc7" class="column-list">

  <div id="3a9c8f51-9d2b-4cb5-900d-806de71eecee" class="column" style="width:37.5%">

    <figure>
    <img src="images/variable/Capture_decran_2022-03-24_a_17.04.01.png" style="width:1318px" />
    </figure>

  </div>

  <div id="d747a9da-7e84-46a2-ad46-5966ea20522c" class="column" style="width:62.5%">

  ``` code
  <axes>
    <axis tag="wght" name="Weight" minimum="300" maximum="700" default="400">
      <map input="300" output="30"/>
      <map input="400" output="40"/>
      <map input="700" output="70"/>
    </axis>
  </axes>
  ```

  </div>

</div>

|              | User coordinates | Normalised | Design coordinates | Normalised |
|--------------|------------------|------------|--------------------|------------|
| min          | 300              | -1         | 30                 | -1         |
| default      | 400              | 0          | 40                 | 0          |
| interpolated | 500              | 0.3333     | 50                 | 0.3333     |
| interpolated | 600              | 0.6667     | 60                 | 0.6667     |
| max          | 700              | 1          | 70                 | 1          |

A consequence of this interpolation is that you may not be happy with the pace of it. For example the interpolation pace could feel “faster” at the beginning, and “slower” at the end of the axis range. This depends greatly on your design: in general there is a larger optical weight difference between Thin and Medium, than between Medium and Black. Some instance could benefit from not being located “regularly” on the weight axis; maybe Regular could be located closer to light, and Black further away from ExtraBold, like this:

<figure>
<img src="images/variable/Capture_decran_2022-04-22_a_12.46.40.png" style="width:1972px" alt="This is what we call a non-linear interpolation." />
<figcaption aria-hidden="true">This is what we call a non-linear interpolation.</figcaption>
</figure>

**Example: non-linear interpolation**

Now let’s pretend that you want your Medium style actually thinner that what the machine could calculate itself, and so you locate it at `45` instead of `50`: you would have then to let the machine knows that it has to adapt the interpolation curve to reach that location. The AVAR table is here to give that factor.

<div id="4b113fbc-b8d6-4fe7-8801-582d3eb0d1d9" class="column-list">

  <div id="1d5b28b6-3aaa-4133-90da-738971f605dd" class="column" style="width:43.75%">

    <figure>
    <img src="images/variable/Capture_decran_2022-03-24_a_17.03.33.png" style="width:288px" />
    </figure>

  </div>

  <div id="47ca15ce-c4c0-4247-a490-9d33dec0a2fc" class="column" style="width:56.25%">

  ``` code
  <axes>
      <axis tag="wght" name="Weight" minimum="300" maximum="700" default="400">
        <map input="300" output="30"/>
        <map input="400" output="40"/>
        <map input="500" output="45"/>
        <map input="600" output="62"/>
        <map input="700" output="70"/>
      </axis>
    </axes>
  ```

  </div>

</div>

``` code
<avar>
    <segment axis="wght">
      <mapping from="-1.0" to="-1.0"/>
      <mapping from="0.0" to="0.0"/>
      <mapping from="0.3333" to="0.1667"/>
      <mapping from="0.6667" to="0.73334"/>
      <mapping from="1.0" to="1.0"/>
    </segment>
 </avar>
```

|              | User coordinates | Normalised | Design coordinates | Normalised |
|--------------|------------------|------------|--------------------|------------|
| min          | 300              | -1         | 30                 | -1         |
| default      | 400              | 0          | 40                 | 0          |
| interpolated | 500              | 0.3333     | 45                 | 0.1667     |
| interpolated | 600              | 0.6667     | 62                 | 0.73334    |
| max          | 700              | 1          | 70                 | 1          |

All of that is suppose to explain why Google Fonts recommend to set up an AVAR table in variable fonts having a weight axis—although it depends greatly on the design and the axis range.

The hard compromise to make is often to find the right balance between what your instance should look like visually and the pace of the interpolation—indeed both factors can come in contradiction.

## Fvar instances

GF only allows weight and italic particles for the instances in the `fvar` table of a variable font. If a font contains additional axes, they must not be mentioned in the instance names and the coordinates for each instance must be set to reasonable default. For example if your font contains a `wdth` axis, you don't want every instance's wdth coordinate value to be set to Condensed (`75`), you would set it to Normal (`100`).

Google Fonts only allows the following named instances:

| Roman      | Italic            |
|------------|-------------------|
| Thin       | Thin Italic       |
| Light      | Light Italic      |
| Regular    | Italic            |
| Medium     | Medium Italic     |
| SemiBold   | SemiBold Italic   |
| Bold       | Bold Italic       |
| ExtraBold  | ExtraBold Italic  |
| Black      | Black Italic      |

We have imposed this restriction for the following reasons:

-   Backwards compatibility with static fonts. Documents won't break if users swap static fonts for variable fonts.
-   To ensure a functional RIBBI style linking.
-   We don't lock ourselves into an implementation we may want to change in the future. The specs are constantly evolving so it's best we wait for these to mature.
-   DTP applications do not properly support variable fonts yet. Variable font support is [experimental in Adobe applications](https://community.adobe.com/t5/indesign/variable-fonts-in-indesign/td-p/10718647).

## STAT Table

All variable fonts must contain a `STAT` table (Style Attributes Table). This table has several features but a key benefit is that it will enable desktop applications to have better font menus. Currently, most font menus only offer a single drop down menu to select a font style. A `STAT` table enables us to have a drop down menu for each variable font axis.

We recommend reading the [MS Spec STAT table info](https://docs.microsoft.com/en-us/typography/opentype/spec/stat) to know more about this table.

Creating good STAT tables is complex. Fortunately, GF has created a `gftools` script called [gftools gen-stat](https://github.com/googlefonts/gftools/blob/main/bin/gftools-gen-stat.py) which can generate a `STAT` table for a family automatically based on GF [Axis Registry](https://github.com/google/fonts/tree/main/axisregistry). [The Builder](build.md) is wrapping that script, which means that you can set up the `STAT` table directly with this tools.

A `STAT` table is defined by these fields:

-   **Axis index / Axis order**

    GF requires `wght` and `ital` axes to be last.
-   **Axis name ID**

    This value will refer to a `name ID` in the `name` table. The axis name should be full string with first letter in capital, for eg. “Weight”.
-   **Axis tag**

    Four-letter ID of the axis. In lowercases for MS registered axes, and in capitals for MS unregistered axes (cf. paragraph above). E.g. “wght” and “JUMP”.

``` code
<!-- DesignAxisCount=3 -->
    <DesignAxisRecord>
      <Axis index="0">
        <AxisTag value="opsz"/>
        <AxisNameID value="257"/>  <!-- Optical size -->
        <AxisOrdering value="0"/>
      </Axis>
      <Axis index="1">
        <AxisTag value="wght"/>
        <AxisNameID value="256"/>  <!-- Weight -->
        <AxisOrdering value="1"/>
      </Axis>
      <Axis index="2">
        <AxisTag value="ital"/>
        <AxisNameID value="278"/>  <!-- Italic -->
        <AxisOrdering value="2"/>
      </Axis>
    </DesignAxisRecord>
```

-   **Axis values**

    -   `STAT` table format for that Axis Value:

        → GF doesn’t recommend format 2 which allows ranges.

    -   Axis Index that refers to a name ID in the `name table`

    -   Value that refers to the **user value**.

    -   Linked value for style linking:

        → `700` for link to Bold on the wght axis, `1` for link to Italic on the ital axis.

    -   Flags

        → if elided/default (`2`) or not (`0`).

    Example for Regular instance in the `STAT` table:

    ``` code
    <AxisValue index="5" Format="3">
    <AxisIndex value="1"/>
    <Flags value="2"/>  <!-- ElidableAxisValueName -->
    <ValueNameID value="261"/>  <!-- Regular -->
    <Value value="400.0"/>
    <LinkedValue value="700.0"/>
    </AxisValue>
    ```

`gftools gen-stat` and the Builder allows you to have external config files which simplify the set up of the STAT table. Read the chapter about [how to build a font](build.md) to have a better understanding of this file.

In 2021, only one desktop application use the STAT table: Microsoft Office for Mac (version 16.46, February 2021 update). However, Indesign, Sketch and other pro type setting applications provide sliders for users to select individual axis locations.

## Instantiated Static Fonts

The fonts API is a system used by millions of people, with lots of different software, and so the system tries to support them all as best as it can - especially with 'backwards compatible' changes that do not "break" existing usage.

As we are in a transition period where some software is VF capable and others are not, or, the old versions of the newly VF capable software remains in use, according to that principle of backwards compatibility, when a variable font is onboarded to Google Fonts, the API provides "fallbacks", static fonts derived from the variable font, for legacy software. And, according to the systematization principle, the system goes along the axis, and derives a static font at each of the nine 100 values, if the axis covers that value (whether or not they are included in the designer's original design space), and names it accordingly. 

For example, if a font design space includes a `wght` axis ranging from `300` to `700` but only includes the `Light` `Regular` and `Bold` instances, the API will also generate the `Medium` and `SemiBold` static fonts by default.

Those static font files are included in the download ZIP file alongside the VF font file, and they are served as web fonts to web browsers not capable of using VFs.

## VF Hinting

The manual hinting of variable font is a complicated process and the auto-hinting often results in a worse rendering than no hinting at all. That is why GF recommend to not hint variable fonts in general. If the font is aimed to a particular device or context GF recommends the tool [VTT](https://docs.microsoft.com/en-us/typography/tools/vtt/) and you can read [the guide to hint variable fonts with VTT](https://googlefonts.github.io/how-to-hint-variable-fonts/) to learn how to do it.

### Family does not exist on Google Fonts

-   RFonts should be unhinted (default setting of [gftools builder](https://googlefonts.github.io/gf-guide/build.html#gftools-builder)).
-   Run fonts through `gftools fix-nonhinting` if you don’t use `gftools builder`.

### Family already exists on Google Fonts and has manual TT hinting

-   If the family has over a billion weekly views, use [VTT](https://docs.microsoft.com/en-us/typography/tools/vtt/). 
-   You can patch a VTT program with [gftools builder](package.md) — see [Montserrat](https://github.com/googlefonts/Montserrat/tree/master/sources) as an example.
-   If the font has been hinted using VTT, run the fonts through `gftools fix-hinting`. 

------------------------------------------------------------------------

## Useful links

**How to use variable fonts:**

-   [Google Fonts Knowledge - variable fonts](https://fonts.google.com/knowledge/introducing_type/introducing_variable_fonts)
-   [variablefonts.io](https://variablefonts.io/)
-   [v-fonts.com](https://v-fonts.com/)
-   [Developer Mozilla VF guide](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Fonts/Variable_Fonts_Guide)

**Testing web pages dedicated to variable fonts:**

-   [Samsa](https://www.axis-praxis.org/samsa/)
-   [Dinamo](https://fontgauntlet.com)
-   [TN type tool](https://typetools.typenetwork.com)

**You can view the name tables using these tools:**

-   [Font Table Viewer](https://glyphsapp.com/tools/fonttableviewer)
-   [DTL OT Master](https://www.fontmaster.nl/otmaster.html)
-   [ttx](https://fonttools.readthedocs.io/en/latest/ttx.html), a practical command line tool of [fonttools](https://github.com/fonttools/fonttools)

**Some font testing web pages allow you to view a selection of tables:**

-   [FontDrop](https://fontdrop.info/#/) → in the “data” tab
-   [fontgauntlet](https://fontgauntlet.com/) → if you click on the small search icon next to the font name

<div class="next-reading">
    Further reading:<br>
    <mark class="green"><b>must&rarr;</b></mark> <a href="./statics" style="font-weight:bold">Static fonts specifics</a>
    <br>
    <mark class="green"><b>must&rarr;</b></mark> <a href="./metrics" style="font-weight:bold">Vertical metrics</a>
    <br>
    <mark class="green"><b>must&rarr;</b></mark> <a href="./testing">QA - Local testing</a>
    <br>
    <mark class="yellow">learn</mark><a href="./axis-registry">Axis Registry Protocol</a> 
    <br>
    <mark class="yellow">learn</mark> <a href="./build">Build the fonts</a>
</div>

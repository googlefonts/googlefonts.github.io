<link href="style.css" rel="stylesheet">

<a href="./index"><button class="button button-i">&larr; GF Guide Index</button></a>

# Overall font files requirements
{:.no_toc}

<div class="callout">

🦥  The following guidelines apply to all fonts, regardless of their format (static or variable fonts) or if you want to add a new font or update one already included in the catalog.
<br><br>
For specific information on any of those cases, please read the pages with the requirements on them. before continuing.

</div>

<div class="context-reading">
    Background reading:<br>
    <mark class="blue">start</mark> <a href="./culture" style="font-weight:bold">Libre Font Culture</a>
    <br>
    <mark class="green"><b>must&rarr;</b></mark> <a href="./onboarding" style="font-weight:bold">Adding & upgrading fonts to Google Fonts</a> 
    <br>
    <mark class="green"><b>must&rarr;</b></mark> <a href="./production" style="font-weight:bold">Production requirements</a>
</div>

## Table of contents
{:.no_toc}
* TOC goes here
{:toc}


## Font name

Naming a font is pretty difficult, and not only because of the need of originalty and creativity. Google Fonts expects font names to comply with basic SEO and tooling limitations. 

For example, the hyphen is used to separate the family name from the style name in the file path; adding a hyphen to your family name may cause the QA tool to think that your style name is unconventional, and therefore fail the font. It will also break the file naming convention put in place across the entire collection (no foundy likes that). And finally, a user searching for the font in Google Fonts may not find it if they forget about the hyphen.

- no camelCase, use spaces instead
- no abbeviation/accronyms (exceptions allowed for companies, i.e. IBM Plex Sans, no exceptions for foundry names)
- no all caps
- only basic ASCII glyphs (A-Z, a-z, 0-9), ie no hyphens, underscores nor accented letters.
- the combined length of family name and style name shall not go over 32 characters.
- the family name must not have "color" "colr" "colored" in the name, since that doesn't tell users what kind of treatment the color font technology provides (whereas e.g. words like "ink" or "fun" does), and invites filtering of color fonts based on having "color" in the family name, which is bad.

Any exception to these rules shall be discussed and validated prior to onboarding, and listed in [Fontbakery's exceptions lists](https://github.com/googlefonts/fontbakery/tree/main/Lib/fontbakery/data/googlefonts) to avoid FAILS.

## Font versioning

**Every new version onboarded to GF should have an increased version number compared to the precedent.** This is explained in the [Main contribution cases](onboarding.md) chapter under the Font Upgrades section.

Versioning is based on [semver](https://semver.org/), apart from we use `MAJOR.SIGNIFICANTMINORPATCH`, instead of `MAJOR.MINOR.PATCH`.

**Examples:**

If a breaking change is made e.g. converting a static font family to a variable font family, the **MAJOR** must be incremented by 1, and the others reset, e.g.:

Current `1.230`, new `2.000`

If a new character set is inserted, **SIGNIFICANT** should be incremented, e.g.:

Current `1.230`, new `1.330`

If a few new glyphs are added, **MINOR** should be incremented, e.g.:

Current `1.230`, new `1.240`

If a name table record is updated such as the copyright string, **PATCH** should be incremented, e.g.:

Current `1.230`, new `1.231`

## Font Embedding (fsType)

[fsType](https://docs.microsoft.com/en-us/typography/opentype/spec/os2#fstype) is one of the parameters of the `OS/2` table in which the embeding permissions of a font are declared. For Libre Fonts it should be set to bit `0` (Installable embedding).

This is how it should look like in the OS/2 table: `<fsType value="00000000 00000000"/>`

If you are using the Glyphs font editor, create a new custom parameter called “fsType” in the “Font” tab of the Font Info pane. Change the Embedding drop-down to “Installable” and leave the “Subsetting Forbidden” checkbox unchecked.

## Font Vertical Metrics

Please read the [following pages about vertical metrics](metrics.md) for setting vertical metrics.

## Font copyright and license

These font info parameters are not optional and should follow the same scheme within the entire GF library.

-   **The font must contain a copyright string within the name table** with the following format:

    ``` code
       Copyright { year } The { family } Project Authors ({ git_url })
    ```

    E.g. Copyright 2011 The Montserrat Project Authors (<https://github.com/JulietaUla/Montserrat>)

    If you are using the Glyphs font editor, add a “Copyright” entry under the “Font” tab of the Font Info panel.

-   **The first line of the [OFL.txt](license-file.md) file should be identical to the font copyright string detailed above**.
  
-   **The license string must be the same for all GF font projects:**

    ``` code
    This Font Software is licensed under the SIL Open Font License, Version 1.1. This license is available with a FAQ at: https://scripts.sil.org/OFL
    ```

    If you are using the Glyphs font editor, add this string to a “License” entry in the “Font” tab of the Font Info panel.

-   **The license URL must be the same for all GF fonts projects:**

    ``` code
    https://scripts.sil.org/OFL
    ```

    If you are using the Glyphs font editor, add this string to a “License URL” entry in the “Font” tab of the Font Info panel.

## Trademarks

Typically libre fonts are not subject to any trademarks.

**If you do not trademark your project name:**
<br>
-   Do not declare trademarks in font info metadata.

**If you do trademark your project name:**
<br>
-   Declare trademarks in font info metadata.
-   License your trademarks for redistribution in a `TRADEMARKS.md` file.

    Example:

    ``` code
    Font Name is a trademark of Company Name.
    ```
-   Explicitly permit Google to use the trademarks. Email <fonts@google.com> with an email like this:

    > *Dear Google Fonts*
    >
    > *We would like our font project "Font Family Name" to be included in Google Fonts and other Google products.*
    >
    > *I hereby grant permission in perpetuity to Google LLC and affiliates to use the following trademarks, and Reserved Font Names declared in the SIL Open Font License notices, for the following font family names:*
    >
    > *Font Family Name Font Family Name Mono Font Family Name Sans*
    >
    > *Best regards,*
    >
    > *Firstname Othername*
    >
    > *Job Title, Organization*

## Monospace fonts

We require the post table `isFixedPitch` to be set and the OS/2 `panose` table to have `OS/2.panose.bProportion` (bit 4) set correctly. If either of these is set incorrectly, users may get fallback glyphs that are not monospaced if they type a character that doesn't exist in the font.

-   Set `post.isFixedPitch` to 1
-   If `OS/2.panose.bFamilyType` is 2 (Latin Text), set `OS/2.panose.bProportion` to 9.
-   If `OS/2.panose.bFamilyType` is 3 (Latin Script), set `OS/2.panose.bProportion` to 3.
-   If `OS/2.panose.bFamilyType` is 5 (Latin Picture), set `OS/2.panose.bProportion` to 3.
-   If you are unsure what to set `OS/2.panose.bFamilyType` to, use 2 for "normal" fonts.
-   If `OS/2.panose.bFamilyType` is 4, you do not need to worry about `OS/2.panose.bProportion`.

Developers can set these automatically by using the following gftools command: `gftools fix-isfixedpitch`

## Glyph Sets

[GF Glyphsets](https://github.com/googlefonts/glyphsets/tree/main/GF_glyphsets) provides the glyph set definition standards that Google Fonts fonts must adhere to.

The structure of these sets is based on a modular scheme that allows the use of different blocks of information to be combined to build sets of glyphs with different levels of complexity according to the needs of each project.

This system aims to give enough flexibility to define the intended scope of each project as well as a way to better assess the font development status and quality analysis.

Currently, the most used ones are:

-   [**GF Latin Kernel**](https://github.com/googlefonts/glyphsets/blob/main/GF_glyphsets/Latin/txt/nice-names/GF_Latin_Kernel.txt) is the minimum Latin set required to be included within fonts targeting non-latin scripts users. *Please note that since it matches the ASCII set, it only includes full support for the English language*.
-   [**GF Latin Core**](https://github.com/googlefonts/glyphsets/blob/main/GF_glyphsets/Latin/txt/nice-names/GF_Latin_Core.txt) is the minimum set required to be included within any font family that addresses Latin based languages (*be it an open contribution or a commissioned font*). It includes the Latin Kernel plus additional glyphs to support the most widely used languages, including those encompassing Central and Western Latin based languages, among \~200 others.
-   [**GF Latin Plus**](https://github.com/googlefonts/glyphsets/blob/main/GF_glyphsets/Latin/txt/nice-names/GF_Latin_Plus.txt) includes additional numerals sets (like numerators, denominators, inferior and superior), expanded math and currency symbols, as well as arrows and bullets in use in Google Docs.
-   [**Latin Vietnamese**](https://github.com/googlefonts/glyphsets/blob/main/GF_glyphsets/Latin/txt/nice-names/GF_Latin_Vietnamese.txt) includes the extended marks and combined letters required to support the Vietnamese language. It requires to be combined with Latin Core for complete Latin + Vietnamese support.

Find all the glyphsets definition and filter lists in the [Glyphsets repository](https://github.com/googlefonts/glyphsets/tree/main/GF_glyphsets). Be aware that these glyphsets are still a work in progress and any advise or recommendation can be submitted using the [Glyphsets’ issue tracker](https://github.com/googlefonts/glyphsets/issues).

## OpenType Features support

### Required Features

The Google Fonts API currently has limited support for some "required" or "always on" OpenType features, such as number sets like Tabular Numbers (`tnum`).

The default numerals (ASCII 0 to 9) should be proportional, and complemented by a Tabular Numbers (`tnum`) feature.

### Optional/Discretionary Features

The Google Fonts API currently does not support requesting the inclusion of optional (also known as discretionary, or opt-in) OpenType Features, such as Stylistic Sets (`salt`) or Small Caps (`smcp`, `c2sc`).
Instead the glyphs contained in these features may be published as a separate family, as follows:

The vertical metrics should be the same in each sibling family, and the "Use of Typo Metrics" flag should be set.
Please refer to the [Vertical Metrics](metrics.md) section for further details.

- **Small Caps**
  - If the subfamily covers the Small Caps component of the project, then the SC suffix must be appended to the family name
  
  `FamilyNameSC-Style.ttf` E.g. `CormorantSC-Regular.ttf`

  - The variant glyphs from the Small Caps should substitute the base glyph from the original family in the new family.

- **Stylistic Sets**
  - If the subfamily covers a Stylistic Set variant instead of original base glyphs, then the SS feature name is appended to the family name
  
  `FamilyNameSC-StyleName.ttf` E.g. `CormorantSC-Infant.ttf`

  - The variant glyphs from the stylistic sets should substitute the base glyph from the original family in the new family, for the user to receive the intended Stylistic Set behavior.
  -  The stylistic sets could be available in the downloadable version of the main font, but they are subsetted from the version served by the API. Thus, for a user experience matter, it is required to name each of the stylistic sets to match the name of the sibling family published. If you are using Glyphs font editor, please check the instructions on adding the names under the [Stylistic Sets Tutorial](https://glyphsapp.com/learn/stylistic-sets). 


<div class="next-reading">
    Further reading:<br>
    <mark class="green"><b>must&rarr;</b></mark> <a href="./statics" style="font-weight:bold">Static fonts specifics</a>
    <br>
    <mark class="green"><b>must&rarr;</b></mark> <a href="./variable" style="font-weight:bold">Variable fonts specifics</a>
    <br>
    <mark class="green"><b>must&rarr;</b></mark> <a href="./metrics" style="font-weight:bold">Vertical metrics</a>
    <br>
    <mark class="green"><b>must&rarr;</b></mark> <a href="./color" style="font-weight:bold">Color fonts</a>
</div>

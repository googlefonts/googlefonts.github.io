<link href="style.css" rel="stylesheet">

<a href="./index"><button class="button button-i">&larr; GF Guide Index</button></a>

# Vertical metrics
{:.no_toc}

<div class="callout">

🐸 Vertical metrics are used to determine the space between two lines of text. Some metrics are meant for Mac, others for Windows, and they are interpreted differently according to web or desktop usage.
<br><br>
Throughout countless threads and discussions, GF decided to prioritize cross-platform compatibility and, in consequence, apply the following requirements. Read them carefully because once a family is onboarded, vertical metrics are meant to remain always the same to avoid regression, as mentioned in <a href="./onboarding">Adding & upgrading fonts to Google Fonts</a>.
<br><br>
Please note that the first metrics guidelines referred to in this guide are Latin-focused and probably will not fully work for other complex scripts, such as Burmese or Devanagari. CJK fonts (Chinese-Japanese-Korean scripts) are treated as special cases and should follow the instructions at the end of the document.

</div>

<div class="context-reading">
    Background reading:<br>
    <mark class="green"><b>must&rarr;</b></mark> <a href="./onboarding" style="font-weight:bold">Adding & upgrading fonts to Google Fonts</a>
    <br>
    <mark class="green"><b>must&rarr;</b></mark> <a href="./requirements" style="font-weight:bold">Overall font files requirements</a>
</div>

## Table of contents
{:.no_toc}
* TOC goes here
{:toc}

## Requirements for all fonts **(except CJK)**

The following rules apply to all new font families and should be enforced for upgraded font families when possible. 
For font families designed for Chinese, Japanese, and Korean (CJK), please refer to the ([CJK Vertical Metrics section below](#CJK-vertical-metrics).)

#### 1. Vertical metrics must not be calculated by the font editor automatically

This is an overall best practice in design. When defining line spacing, it's important to strike a balance between legibility and avoiding overlapping letters. At Google Fonts, we have established a specific system that prioritizes optimal performance for various situations while still leaving room for future update improvements, like adding more languages without causing regressions. 

#### 2. Vertical metrics must be consistent across a family.

Each font in a family must share the same vertical metrics values.

This rule can be avoided if a font is being upgraded and previously had inconsistent family metrics. In this case, the aim should be to visually match the line spacing of each font but fix any clipping issues caused by incorrect `WinAscent` and `WinDescent` values.

#### 3. If the family is being updated, the line height must visually match the previous release

Some applications do not allow users to control their fonts' line height/leading. Word processors and text editors are common culprits. It is essential their documents do not reflow.

#### 4. The following vertical metric parameters must be set for each font in a family

| OpenType spec (font binaries) | Glyphs.app Master customParameter | FontLab                | ufo3 fontinfo.plist      |
|-------------------------------|-----------------------------------|------------------------|--------------------------|
| \[OS/2\] sTypoAscender        | typoAscender                      | \[OS/2\] TypoAscender  | openTypeOS2TypoAscender  |
| \[OS/2\] sTypoDescender       | typoDescender                     | \[OS/2\] TypoDescender | openTypeOS2TypoDescender |
| \[OS/2\] sTypoLineGap         | typoLineGap                       | \[OS/2\] TypoLineGap   | openTypeOS2TypoLineGap   |
| \[hhea\] Ascender             | hheaAscender                      | \[hhea\] Ascender      | openTypeHheaAscender     |
| \[hhea\] Descender            | hheaDescender                     | \[hhea\] Descender     | openTypeHheaDescender    |
| \[hhea\] LineGap              | hheaLineGap                       | \[hhea\] LineGap       | openTypeHheaLineGap      |
| \[OS/2\] usWinAscent          | winAscent                         | \[OS/2\] WinAscent     | openTypeOS2WinAscent     |
| \[OS/2\] usWinDescent         | winDescent                        | \[OS/2\] WinDescent    | openTypeOS2WinDescent    |

*For brevity, we will refer to the three sets of metrics as* `Typo`*,* `Hhea`*,* `Win`*.*

#### 5. [Use_Typo_Metrics](https://www.microsoft.com/typography/otspec/os2.htm#fss) must be enabled

This will force Microsoft Applications to use the `Typo` values instead of the `Win` values for line spacing. Doing this allows us to freely set the `Win` values to avoid clipping and control the line height with the `Typo` values. It has the added benefit of future line height compatibility. When adding a new script, we simply change the `Win` values to the latest `yMin` and `yMax` without worrying if the line height has changed. Note that the `Use_Typo_Metric` flag is also called `fsSelection bit 7 `(related to how it is set in the OS/2 table).

-   In Glyphs.app, set `Use_Typo_Metrics` custom parameter to `true` in the **Font** tab of **Font Info**.
-   In RoboFont, this is under **Font Info \> OpenType \> OS/2 Table \> fsSelection \> USE_TYPO_METRICS**.
-   In the OS/2 table: `<fsSelection value="00000000 10000000"/>`

#### 6. WinAscent and WinDescent values must be the same as the family's tallest/deepest yMin and yMax bounding box values

Microsoft's [OpenType specification](https://www.microsoft.com/typography/otspec/os2.htm#wa) recommends the following:

> If any clipping is unacceptable, then the value should be set to `yMax`.

[Overpass issue \#33](https://github.com/RedHatBrand/Overpass/issues/33) demonstrates what happens in MS applications when the `winAscent` and `winDescent` are not set correctly.

Changing these values will increase the line height in MS applications. This can lead to very loose line heights if the bounding box is exceedingly tall. This mainly occurs in families featuring Vietnamese, Devanagari, Arabic, or other tall scripts. To counteract this, we enable the [Use Typo Metrics](https://www.microsoft.com/typography/otspec/os2.htm#fss) flag and set the `Typo` values to match the previous `Win` values. By swapping the sets, we should retain the previous line heights in Windows as well as remove the clipping.

#### 7. Hhea and Typo metrics should be equal

`Hhea` metrics are used in macOS, while Microsoft uses `Typo` when `Use_Typo_Metrics` is enabled. They should ideally be identical.

This rule can be avoided if a font is being upgraded and previously had inconsistent values.

#### 8. LineGap values must be 0

The `LineGap` value is a space added to the line height created by the union of the `(typo/hhea)Ascender` and `(typo/hhea)Descender`. It is handled differently according to the environment. Most desktop apps will add This leading value above the text line. It will be shared above *and* under in web browsers and ignored in Windows if `Use_Typo_Metrics` is disabled. For better line spacing consistency across platforms, the `(typo/hhea)LineGap` values must be `0`.

#### 9. Uppercases should be centered in the text line 

For fonts whose primary script has uppercase letterforms, such as Latin, Greek, and Cyrillic, web designers will thank you if you manage to have the same space above and under capitals: `typoAscender—CapsHeight = abs(typoDescender)`. It will make it easier for them to set padding in buttons, for example.

#### 10. typo/hheaAscender value should leave open room for stacked diacritics.

Following recent tests to confirm our vertical metrics policies, we now require the `(typo/hhea)Ascender` to be equal to `Abreveacute U+1EAE`. For families with multiple weights, you must use the tallest `Abreveacute U+1EAE` (e.g., in the Black master) as the reference point to guarantee uniform positioning across the entire font family.

Even if the font does not support Vietnamese yet, we strongly suggest estimating the ascenders value foreseeing the `Abreveacute U+1EAE` height based on two main reasons:

**Once the font is published, the vertical metric values cannot be modified.** By implementing the above approach, we can keep the option of updating the font in the future to support additional languages like Vietnamese.
- Certain Mac applications, including TextEdit, determine the height of the first line of text by either the `Agrave U+00C0` height or the font's `hheaAscender`, whichever is taller (for additional information on this topic, please refer to this issue: <https://github.com/googlefonts/fontbakery/issues/3170>). So `Agrave U+00C0` is a required minimum, and `Abreveacute U+1EAE` is a strongly recommended minimum.

#### 11. The sum of the font’s vertical metric values (absolute) should be 20-30% greater than the font’s UPM

By default, DTP applications such as Indesign will set the line height to be 20% greater than the font’s size (10pt size / 12pt leading). For consistency, we recommend setting the vertical metric values so their sum is in a similar range, for example:

``` code
UPM = 1000
(typo/hhea)Ascenders = 900
(typo/hhea)Descenders = -300
(typo/hhea)LineGap = 0

Total:
ascender + abs(descenders) + linegap = 1200
```

Exceptions are usually made if the font’s primary script isn’t Latin, Greek, or Cyrillic. Some scripts such as Devanagari contain very tall and shallow glyphs. It may make more sense for the sum of the metrics to exceed 130% to avoid interline glyph collisions.

## Note

**Please keep in mind that this calculation will need to be set according to the specificities of each font.**

-   The 120% suggested above is for compatibility with desktop publishing apps (like InDesign's automatic alignment ratio). Still, it can often be too tight if your font covers more languages than basic Latin, Greek, and Cyrillic or if you have a particular design with short ascenders.  
-   Please pay careful attention to the design of diacritic marks, especially the [stacked diacritics](https://googlefonts.github.io/gf-guide/diacritics.html#stacked-diacritics). This way, you ensure the ascender value is not unnecessarily high. You could also determine an ideal line spacing and then draw the diacritics accordingly or adapt them to it.
-   Google Fonts is trying to push designers to include proper support of the [mark-to-mark](https://googlefonts.github.io/gf-guide/diacritics.html#the-glyph-positioning-gpos-table) feature, allowing the combination of diacritics and display of non-encoded accented glyphs. Pay attention to your anchor placement so that, if, for example, you combine breve and acute, you don't end up with a severe interline glyph clashing. 


## Concrete cases:

Setting vertical metrics usually falls into the following two categories:

1.  Calculating the vertical metrics for a new family
2.  Recalculating the vertical metrics for an upgraded family

### 1. Calculating the vertical metrics for a new family

Set these values to be the same across all masters to ensure that output instances have equal vertical metrics:

-   `typoAscender` and `hheaAscender` set to equal or higher than `Ắ`
-   `typoLineGap` and `hheaLineGap` set to `0`
- `typoDescender` and `hheaDescender` are set to visually leave Caps height centered in the line but lower than the deepest descender of the primary script.
-   `winAscent` and `winDecent` set to `yMax` and `yMin` (the absolute highest and lowest point in the font)
-   `use_typo_metrics` is enabled

Expected result: vertical metrics should be around 130% of UPM. Anything greater, and the metrics may look too loose.

**Example**

A new Latin family has the following qualities:

-   UPM is `1000`
-   `Abreveacute U+1EAE` glyph `yMax` value (taller in the family, Black style for this example) = `1015`
-   Deepest a-z glyph in the family `yMin` value (`g` bold in this example) = `-210`
-   Caps height (`H`or `Z` bbox height) = `700`
-   Family's `yMax = 1116` (Black `Abrevehookabove U+1EB2` for this family)
-   Family's `yMin = -260` (Black `ccedilla U+00E7` for this family)

1.  Set the default values following the schema above:

``` code
typoAscender = 1015 # which matches the tallest `Abreveacute U+1EAE` in the family (see below)
typoDescender = -315 # an equal or similar value added to the Cap's Height to leave them centered in the line and is greater than the deepest letterform.
typoLineGap = 0
hheaAscender = 1015 # ==typoAscender
hheaDescender = -315 # ==typoDescender
hheaLineGap = 0 # ==typoLineGap
winAscent = 1116 # which matches Font bbox yMax, `Abrevehookabove U+1EB2` in the family 
winDescent = 315 # *absolute value* of Font bbox yMin ie. a positive integer
```

2.  Be sure to copy these same metric values to all of the masters in the family
3.  Be sure to enable `Use_Typo_Metrics`
4.  If working in GlyphsApp, you can add the "EditView Line Height" parameter in Font Info and set it up to UPM*1.3 (so 1300 if your UPM value is 1000). This allows you to view your line spacing at the glyph view window.

Note: In step 1, for determining the `typoAscender` value, matching the tallest `Abreveacute` in the family is not done with a rote mathematical formula (like `≈ [(UPM * 1.3 - CapsHeight) / 2] + CapsHeight`) - because almost nothing is mathematically calculated in typography, but rather it is about proportions, so absolute math may bring more confusion than clarity, even when dealing with a family's vertical metrics. 
For instance, once the height of `Abreveacute` has been established, it can give a sense of how much is being added to the Cap Height.
In this example, with a Caps height of `700`, according to the math formula, the value would have been `300`, but a better fitting proportion is `+315` due to its `Abreveacute` height.

People tend to think that math formulas are more precise and, hence, follow them blindly. 
On the other hand, if the `Abreveacute` height is very high, forcing the average vertical metrics to be absurdly tall—way beyond the suggested 130% overall—then the stacked mark positions would need to change to fit better that percentage.

### 2. Recalculating the vertical metrics for an upgraded family

Many font families receive upgrades, either by the original author or a third party. When character extensions modify the font's bounding box, the vertical metrics need to be recalculated.

Imagine we have a previous v1.000 release. We're now adding Vietnamese. The version number has been bumped to V2.000. The font's bbox `yMax` has changed from `1000` to `1102` and `yMin` from `-200` to `-314`.

v1.000 had the following family vertical metrics:

``` code
typoAscender = 800
typoDescender = -200
typoLineGap = 200
hheaAscender = 800
hheaDescender = -200
hheaLineGap = 200
winAscent = 1000
winDescent = 200
```

*Notice each set set adds up to 1200, if the negative integers are converted to positive. This should lead to consistent metrics across each platform*

There are two cases that can occur.

**I.** `Use_Typo_Metrics` **was already enabled in the v1.000 release.**

- The `Win` values need to reflect the new `yMin` and `yMax` values.
- The `LineGap` needs to change to `0` for better cross-platform compatibility.
- Since browsers would display the `LineGap` evenly above the Ascender and below the Descender, the old `LineGap` value needs to be evenly distributed between the old `typoAscender` and `typoDescender` values.
- The `hhea` values then need to reflect the new `typo` values for better cross-platform compatibility.

1.  v2.000 vertical metrics:

    ``` code
    typoAscender = 900 # Old typoAscender + typoLineGap/2
    typoDescender = -300 # Old typoDescender + typoLineGap/2
    typoLineGap = 0 
    hheaAscender = 900 # typoAsender
    hheaDescender = -300 # typoDescender
    hheaLineGap = 0 # typoLineGap
    WinAscent = 1102 # Font bbox yMax
    WinDescent = 314 # Font bbox yMin (positive integer)
    ```
2.  Repeat the process for each weight/style if values are not unique in v1.000

**II.** `Use_Typo_Metrics` **was** ***not*** **enabled in the previous release.**

The Typo Metrics need to inherit the v1.000 Win values. The WinAscent and WinDescent also need to reflect the new yMin and yMax values.

1.  v2.000 vertical metrics:

    ``` code
    typoAscender = 1000 # Old WinAscent
    typoDescender = -200 # Old negative WinAscent
    typoLineGap = 0 # Win Metrics has no LineGap parameter so we set this to 0
    hheaAscender = 1000 # typoAscender
    Hhea Descender = -200
    hheaLineGap = 0 # typoLineGap
    winAscent = 1102 # Font bbox yMax
    winDescent = 314 # Font bbox yMin positive integer
    ```
2.  Repeat the process for each weight/style if values are not unique in v1.000
3.  Enable Use_Typo_Metrics

If the font is already hosted on [fonts.google.com](http://fonts.google.com/), you can confirm the upgraded vertical metrics visually match by using [diffenator2](https://github.com/googlefonts/diffenator2) with the command `diffenator2 diff -fb font1.ttf -fa font2.ttf -o out_dir` where `-fb` stands for `--fonts-before` and `-fa` for `--fonts-after`.

## CJK Vertical Metrics

Vertical metrics for CJK fonts are based on the font emBox values. This ensures that the ideographs (or syllables) are properly positioned in the center of the emBox both in horizontal and vertical typesetting. 

The following metrics are a distinct split from the standard approach of setting vertical metrics for CJK fonts, which normally set the `sTypo` metrics to align with the emBox values. This is also how the [OT spec recommendations](https://learn.microsoft.com/en-us/typography/opentype/spec/os2#stypoascender) are written. However, following [investigation into performance of CJK fonts](https://github.com/google/fonts/issues/8911) under the primary scenarios that Google Fonts prioritizes, the following new metrics have been established:

| Attrib                                    | Value                                    | Example using Iansui       |
|-------------------------------------------|------------------------------------------|----------------------------|
| OS/2.sTypoAscender                        | ideoEmBoxTop \+ (10–20% \* emBox)/2      | 940                        |
| OS/2.sTypoDescender                       | ideoEmBoxBottom \- (10–20% \* emBox)/2   | -180                       |
| OS/2.sTypoLineGap                         | 0                                        | 0                          |
| hhea.ascender                             | OS/2.sTypeAscender                       | 940                        |
| hhea.descender                            | OS/2.sTypoDescender                      | -180                       |
| hhea.lineGap                              | 0                                        | 0                          |
| OS/2.usWinAscent                          | Font bbox yMax                           | 1066                       |
| OS/2.usWinDescent                         | Font bbox yMin                           | 273                        |
| OS/2.fsSelection bit 7 (Use_Typo_Metrics) | Set / enabled                            | ✅                         |
| BASE table                                | Required                                 |                            |

In the case of `sTypoAscender` and `sTypoDescender`, a range of values is acceptable, per the designer's perspective and specific needs. Generally ~18% tends to produce good results, but depending on the project, wider or narrower metrics may be required. 

**Note** If the font is being built with `makeotf`, be aware that Adobe\'s default settings expect `sTypoMetrics` to match the emBox. Unless glyph heights are manually set for all glyphs, the `vmtx` values will not be set properly. As such, it may be easier to set vertical metrics as usual in the source, and adjust in post-production.

These metrics were established based on investigations into improving metrics performance of CJK fonts across the library. Please see the following issue for more information:
-   <https://github.com/google/fonts/issues/8911>

### Base Table

In addition to the above metrics, CJK fonts are now required to include a `BASE` table (https://learn.microsoft.com/en-us/typography/opentype/spec/baselinetags) to ensure broad compatibility. 

For a standard square emBox font (1000 units wide for a 1000 UPM font), such as Iansui, the following BASE table was added to the `.fea` file. 
```
table BASE {
  HorizAxis.BaseTagList                 icfb  icft  ideo   romn;
  HorizAxis.BaseScriptList  DFLT  ideo   -67   827  -120      0,
                            hani  ideo   -67   827  -120      0,
                            kana  ideo   -67   827  -120      0,
                            latn  romn   -67   827  -120      0,
                            cyrl  romn   -67   827  -120      0,
                            grek  romn   -67   827  -120      0,

  VertAxis.BaseTagList                  icfb  icft  ideo  romn;
  VertAxis.BaseScriptList   DFLT  ideo    53   947     0   120,
                            hani  ideo    53   947     0   120,
                            kana  ideo    53   947     0   120,
                            latn  romn    53   947     0   120,
                            cyrl  romn    53   947     0   120,
                            grek  romn    53   947     0   120,
} BASE;
```
The BASE tags above are:

- `icfb`: Ideographic character face bottom edge (in HorizAxis) / left edge (in VertAxis)
- `icft`: Ideographic character face top edge (in HorizAxis) / right edge (in VertAxis)
- `ideo`: ideographic em-box bottom edge (in HorizAxis) / left edge (in VertAxis)
- `romn`: Latin baseline. Usually 0 in HorizAxis, inverse of ideo in VertAxis

Some additional tags which may be useful can be reviewed on the [official documentation](https://learn.microsoft.com/en-us/typography/opentype/spec/baselinetags). 

In the case of a design that is narrower than the usual square emBox, it is recommended to also include `idtp` to mark the top edge (opposite of `ideo`). For example, WD XL Lubrifont, which has an advance width of 765, has the following base table:

```
table BASE {
  HorizAxis.BaseTagList                 icfb  icft  ideo  idtp  romn;
  HorizAxis.BaseScriptList  DFLT  ideo  -104   814  -120   880     0,
                            hani  ideo  -104   814  -120   880     0,
                            kana  ideo  -104   814  -120   880     0,
                            latn  romn  -104   814  -120   880     0,
                            cyrl  romn  -104   814  -120   880     0,
                            grek  romn  -104   814  -120   880     0;

  VertAxis.BaseTagList                  icfb  icft  ideo  idtp  romn;
  VertAxis.BaseScriptList   DFLT  ideo    49   716     0   765     0,
                            hani  ideo    49   716     0   765     0,
                            kana  ideo    49   716     0   765     0,
                            latn  romn    49   716     0   765     0,
                            cyrl  romn    49   716     0   765     0,
                            grek  romn    49   716     0   765     0;
} BASE;
```
Note the `idtp` value in the VertAxis is present to indicaate the narrower width. 

------------------------------------------------------------------------

## Useful links

-   [Glyphs.app tutorial for vertical metrics](https://glyphsapp.com/learn/vertical-metrics)
-   [Kalapi vertical metrics schema](https://groups.google.com/d/msg/googlefonts-discuss/W4PHxnLk3JY/KoMyM2CfAwAJ)
-   [Khaled vertical metrics schema](https://groups.google.com/d/msg/googlefonts-discuss/W4PHxnLk3JY/MYgVlQMjAwAJ)
-   [Show Vertical Metrics](https://github.com/mekkablue/ShowVerticalMetrics) plug-in in GlyphsApp
-   Mekkablue’s [Vertical Metrics Manager](https://github.com/mekkablue/Glyphs-Scripts/blob/master/Font%20Info/Vertical%20Metrics%20Manager.py)
-   [Impallari/testing](https://github.com/impallari/Font-Testing-Page): Font tester which has no css line-height property set ([live site](http://cyreal.org/Font-Testing-Page))
-   [Diffenator2](https://github.com/googlefonts/diffenator2): Create diffing docs to compare local updated fonts against currently hosted versions on [fonts.google.com](http://fonts.google.com/)

<!-- <div class="next-reading">
    Further reading:<br>
    <mark class="green"><b>must&rarr;</b></mark> <a href="./qa">QA process & tools</a>
</div> -->

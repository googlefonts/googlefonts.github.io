<link href="style.css" rel="stylesheet">

<a href="./index"><button class="button button-i">&larr; GF Guide Index</button></a>

# Vertical metrics
{:.no_toc}

<div class="callout">

🐸 Vertical metrics are used to determine the space between two lines of text. Some metrics are meant for Mac, other for Windows; and are interpreted differently according to web or desktop usage.
<br><br>
Throughout countless threads and discussions, GF decided to make the priority on cross-platform compatibility and therefore apply the following requirements. Read them carefully because once a family is onbaorded, vertical metrics are meant to remain always the same to avoid regression, as mentioned in <a href="./onboarding">Adding & upgrading fonts to Google Fonts</a>.
<br><br>
Please note that the first metrics guidelines referred to in this guide are Latin focused and probably will not fully work for other complex scripts such as Burmese and Devanagari among others. CJK fonts (Chinese-Japanese-Korean scripts) are treated as special cases and should follow the instructions at the end of the document.

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

The following rules apply to all new font families, and should be enforced to upgraded font families when possible. 
For font families designed for Chinese, Japan and Korean (CJK), please refer to the ([CJK Vertical Metrics section below](#CJK-vertical-metrics).)

#### 1. Vertical metrics must not be calculated by the font editor automatically

This is an overall best practice in design. When defining line spacing, it's important to strike a balance between legibility and avoiding overlapping letters. At Google Fonts, we have established a specific system that prioritizes optimal performance for various situations while still leaving room for future update improvements, like adding more languages without causing regressions. 

#### 2. Vertical metrics must be consistent across a family.

Each font in a family must share the same vertical metrics values.

This rule can be avoided if a font is being upgraded and previously had inconsistent family metrics. If this is the case, the aim should be to visually match the line spacing of each font, but fix any clipping issues caused by incorrect `WinAscent`, `WinDescent` values.

#### 3. If the family is being updated, the line height must visually match the previous release

Some applications do not allow users to control the line height/leading of their fonts. Word processors and text editors are common culprits. It is essential their documents do not reflow.

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

*For brevity, we will refer to the 3 sets of metrics as* `Typo`*,* `Hhea`*,* `Win`*.*

#### 5. [Use_Typo_Metrics](https://www.microsoft.com/typography/otspec/os2.htm#fss) must be enabled

This will force Microsoft Applications to use the `Typo` values instead of the `Win` values for line spacing. By doing this, we can freely set the `Win` values to avoid clipping and control the line height with the `Typo` values. It has the added benefit of future line height compatibility. When a new script is added, we simply change the `Win` values to the new `yMin` and `yMax`, without needing to worry if the line height have changed. Note that the `Use_Typo_Metric` flag is also called `fsSelection bit 7 `(related to how it is set in the OS/2 table).

-   In Glyphs.app, set `Use_Typo_Metrics` custom parameter to `true` in the **Font** tab of **Font Info**.
-   In RoboFont, this is under **Font Info \> OpenType \> OS/2 Table \> fsSelection \> USE_TYPO_METRICS**.
-   In the OS/2 table: `<fsSelection value="00000000 10000000"/>`

#### 6. WinAscent and WinDescent values must be the same as the family's tallest/deepest yMin and yMax bounding box values

Microsoft's [OpenType specification](https://www.microsoft.com/typography/otspec/os2.htm#wa) recommends the following:

> If any clipping is unacceptable, then the value should be set to `yMax`.

[Overpass issue \#33](https://github.com/RedHatBrand/Overpass/issues/33) demonstrates what happens in MS applications when the `winAscent` and `winDescent` are not set correctly.

By changing these values, the line height will be increased in MS applications. This is can lead to very loose line heights if the bounding box is exceedingly tall. This mainly occurs in families featuring Vietnamese, Devanagari and Arabic or other tall scripts. To counteract this, we enable the [Use Typo Metrics](https://www.microsoft.com/typography/otspec/os2.htm#fss) flag and set the `Typo` values to match the previous `Win` values. By swapping the sets, we should retain the previous line heights in Windows as well as remove the clipping.

#### 7. Hhea and Typo metrics should be equal

`Hhea` metrics are used in macOS, whilst Microsoft uses `Typo` when `Use_Typo_Metrics` is enabled. They should ideally be identical.

This rule can be avoided if a font is being upgraded and previously had inconsistent values.

#### 8. LineGap values must be 0

The `LineGap` value is a space added to the line height created by the union of the `(typo/hhea)Ascender` and `(typo/hhea)Descender`. It is handled differently according to the environment. This leading value will be added above the text line in most desktop apps. It will be shared above *and* under in web browsers, and ignored in Windows if `Use_Typo_Metrics` is disabled. For better linespacing consistency across platforms, `(typo/hhea)LineGap` values must be `0`.

#### 9. Uppercases should be centered in the text line 

For fonts which primary script has uppercases letterforms such as Latin, Greek and Cyrillic. Web designers will thank you if you managed to have the same space above and under capitals: `typoAscender - CapsHeight = abs(typoDescender)`. It will make easier for them the setting of padding in buttons for example.

#### 10. typo/hheaAscender value should leave open room for stacked diacritics.

Following recent tests to confirm our vertical metrics policies, we now require that the typo/hheaAscender be equal to `A breve acute`. For families with multiple weights you must use the tallest `A breve acute` (in e.g., the Black master) as the reference point to guarantee uniform positioning across the entire font family.

Even if the font does not support Vietnamese yet, we strongly suggest estimating the ascenders value foreseeing the `A breve acute` height based two main reasons:

- Once the font is published, it is not possible to modify the vertical metric values. By implementing the above approach, we can keep the option of updating the font in the future to support additional languages like Vietnamese.
- Certain Mac applications, including TextEdit, determine the height of the first line of text by either the `A grave` height or the font's `hheaAscender`, whichever is taller (for additional information on this topic, please refer to this issue: <https://github.com/googlefonts/fontbakery/issues/3170>). So `Agrave` is a required minimum, and `Abreveacute` is a strongly recommended minimum.

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

Exceptions are usually made if the font’s primary script isn’t Latin, Greek or Cyrillic. Some scripts such as Devanagari contain very tall and shallow glyphs. It may make more sense for the sum of the metrics to exceed 130% to avoid interline glyph collisions.

## Note

Please keep in mind that this calculation is to be set according to the specificities of each font.

-   The 120% suggested above is for compatibility with desktop publishing apps (like InDesign automatic alignment ratio). Still, it can often be too tight if your font covers more languages than basic Latin, Greek, and Cyrillic, or if you have a particular design with short ascenders.  
-   Please pay careful attention to the overall design of diacritic marks, especially the [stacked diacritics](https://googlefonts.github.io/gf-guide/diacritics.html#stacked-diacritics). This way you ensure the ascenders value is not unnecessarily high. You could also determine an ideal line spacing and then draw the diacritics accordingly or adapt them to it.
-   Google Fonts is trying to push designers to include proper support of the [mark-to-mark](https://googlefonts.github.io/gf-guide/diacritics.html#the-glyph-positioning-gpos-table) feature allowing combination of diacritics and display of non-encoded accented glyphs. Pay attention to your anchor placement so that, if you combine breve and acute for example, you don't end up with a severe interline glyph clashing. 


## Concrete cases:

Setting vertical metrics usually falls into the following two categories:

1.  Calculating the vertical metrics for a new family
2.  Recalculating the vertical metrics for an upgraded family

### 1. Calculating the vertical metrics for a new family

Set these values to be the same across all masters to ensure that output instances have equal vertical metrics:

-   `typoAscender` and `hheaAscender` set higher than `Ắ`
-   `typoLineGap` and `hheaLineGap` set to `0`
-   `typoDescender` and `hheaDescender` set to visually leave Caps height centered in the line, but lower than the deepest descender of the primary script.
-   `winAscent` and `winDecent` set to `yMax` and `yMin` (absolute highest and lowest point in the font)
-   `use_typo_metrics` is enabled

Expected result: vertical metrics should be around 130% of UPM. Anything greater, and the metrics may look too loose.

**Example**

A new Latin family has the following qualities:

-   UPM is `1000`
-   `yMax` of tallest `A breve acute` in the familly (black for this example) = `1015`
-   `yMin` of deepest a-z letter (`g` bold in this family) = `210`
-   Caps height (`H`or `Z` bbox height) = `700`
-   Family's `yMax = 1116` (Black `A breve hookabove` for this family)
-   Family's `yMin = -260` (Black `c cedilla` for this family)

1.  Set the default values, following the schema above:

``` code
typoAscender = 1015 # which matches tallest `A breve acute` in the family and is ≈ [(UPM * 1.3 - CapsHeight) / 2] + CapsHeight
typoDescender = -315 # an equal or similar value added to the Caps Height to leave them centered in the line, and is greater than deepest letterform.
typoLineGap = 0
hheaAscender = 1015 # typoAscender
hheaDescender = -315 # typoDescender
hheaLineGap = 0 # typoLineGap
winAscent = 1116 # Font bbox yMax
winDescent = 315 # *absolute value* of Font bbox yMin ie. a positive integer
```

1.  Be sure to copy these same metric values to all of the masters in the family
2.  Be sure to enable `Use_Typo_Metrics`
3.  If working on GlyphsApp, you can add the "EditView Line Height" parameter in font info and set it up to UPM*1.3 (so 1300 if your UPM value is 1000). This allows you to view your line spacing at the glyph view window.

### 2. Recalculating the vertical metrics for an upgraded family

Many font families receive upgrades, either by the original author or a 3rd party. When character extensions occur which modify the font's bounding box, the vertical metrics will need to be recalculated.

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

There are two cases which can occur.

**I.** `Use_Typo_Metrics` **was already enabled in the v1.000 release.**

- The `Win` values needs to reflect the new `yMin` and `yMax` values.
- The `LineGap` needs to change to `0` for better cross-platform compatibility.
- Since browsers would display the `LineGap` evenly above the Ascender and below the Descender, the old `LineGap` value needs to be evenly distributed between the old `typoAscender` and `typoDescender` values.
- The `hhea` values then needs to reflects the new `typo` values for better cross-platform compatibility.

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
2.  Repeat process for each weight/style if values are not unique in v1.000

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
2.  Repeat process for each weight/style if values are not unique in v1.000
3.  Enable Use_Typo_Metrics

If the font is already hosted on [fonts.google.com](http://fonts.google.com/), you can test the upgraded vertical metrics visually match by using [diffenator2](https://github.com/googlefonts/diffenator2) with the command `diffenator2 diff -fb font1.ttf -fa font2.ttf -o out_dir` where `-fb` stands for `--fonts-before` and `-fa` for `--fonts-after`.

## CJK Vertical Metrics

*The following CJK vertical metrics are based on Source Han and Noto CJK fonts.*

The values for CJK vertical metrics are based on a few core concepts:

1. The OS/2.sTypoAscender and OS/2.sTypoDescender values defines the ideographic em-box, such as CJK ideographs and full-width symbols. Thus, the value of OS/2.sTypoAscender - OS/2.sTypoDescender must equals UPM value, or in other words, the difference of the UPM factors for OS/2.sTypoAscender and OS/2.sTypoDescender should equals 1.
    > Source Han/Noto CJK uses 880/-120 or 0.88/-0.12. Other usual pairs are 0.85/-0.15 and 0.8/-0.2. The factors may be modified to match the Latin part of the font.
2. Line gaps should be set to 0 matching Latin font practice. See above [Requirement point 8](#8-linegap-values-must-be-0).
3. hhea values should be set to look harmonized (excluding extreme vertical height symbols only used in vertical typesetting such as U+3031 and U+3032), including Latin parts (such as hanyu pinyin Ǚ). See above [Requirement point 10](#10-typohheaascender-value-should-leave-open-room-for-stacked-diacritics).
    > Source Han Sans/Noto Sans CJK uses 1160/-288.
4. Disable OS/2.fsSelection bit 7 (Use_Typo_Metrics) as both sType* and usWin* are same.

The following vertical metric values may be applied to CJK fonts. 

| Attrib                                    | Value                                    | Example using 1000upm font |
|-------------------------------------------|------------------------------------------|----------------------------|
| OS/2.sTypoAscender                        | 0.88 \* font upm                         | 880                        |
| OS/2.sTypoDescender                       | -0.12 \* font upm （should be negative） | -120                       |
| OS/2.sTypoLineGap                         | 0                                        | 0                          |
| hhea.ascender                             | Set to look comfortable (\~1.16 \* upm)  | 1160                       |
| hhea.descender                            | Set to look comfortable (\~-0.288 \* upm, should be negative) | -288                       |
| hhea.lineGap                              | 0                                        | 0                          |
| OS/2.usWinAscent                          | Same as hhea.ascent                      | 1160                       |
| OS/2.usWinDescent                         | abs(value) of hhea.descent               | 288                        |
| OS/2.fsSelection bit 7 (Use_Typo_Metrics) | Do not set / disabled                    | 0                          |

Our decision to follow the Adobe schema was based on Dr. Ken Lunde’s comments and his release notes on Source Han Sans:

-   <https://github.com/source-foundry/font-line/issues/2>
-   [SourceHanSansReadMe.pdf](https://github.com/adobe-fonts/source-han-sans/raw/release/SourceHanSansReadMe.pdf)

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

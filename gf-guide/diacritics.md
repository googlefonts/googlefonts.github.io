<link href="style.css" rel="stylesheet">

# Diacritic marks
{:.no_toc}

<div class="callout">

🐳 A diacritic is a mark used in combination with a base letter for many purposes, such as modifying the pronunciation by extending a basic alphabet to include more phonemes; adding stress to a word that could differentiate similar words (hence meanings); and, in some languages, adding or modifying a vowel in a word.
<br><br>
Many diacritics are separated from the base letter, and can be placed above, below, aside, or through it; while other diacritics connect to the base. 
<br><br>

</div>

## Table of contents
{:.no_toc}
* TOC goes here
{:toc}

## Design considerations

- Diacritics must be coherent and harmonious with the general design of the font. Take care of details like construction, contrast, thickness, stroke terminal shapes, etc.
- It is suggested that you design the diacritical marks with the most strict users in mind. This means respecting conventional contemporary shapes and sizes, and not reusing or interchanging the forms of different diacritics. (For example, a `breve` should not be reused as a `caron`.)
- Pay attention to the proportion requirements. There are some marks (for example, the `horn`) which, once combined with the base letter, will blend into the base and resemble an integral part of it.
- Compound letters must be perceived as a whole. The distance to the base letter is crucial and can affect legibility. If the mark glyph is too close to the base font, it could appear to collide with the base letter, adding darker spots to the line of text, especially at small sizes. If the mark is too far from the base letter, they would appear separate, making the reading process difficult.
- The horizontal position is also essential for readability. In Latin script, the symmetric marks are placed in the optical center of the base letter while the asymmetric ones follow other rules. (Note that the optical center is often distinct from the mathematical center.) But remember, they must be seen as a unity, so they must not be separated or detached from the base letter.
- In Latin script, it is expected that all marks share the same distance to the base letter. For particular cases like script fonts where the x-height could vary, marks should at least appear to be at the same optical distance to the base letter.
- Idiosyncratic or decorative brands have given way to more universal or neutral forms.
- You also need to create all the combining marks required for the language you are supporting, as well as the so-called "Legacy Marks". (See below.) Google Fonts requires at least the GF Latin Core as the minimum set for a font addressing the Latin script. Please read more about our <a herf="https://googlefonts.github.io/gf-guide/requirements.html#glyphsets">Glyphsets</a>.
- Usually, the design of the diacritics needs to be adjusted in size or slope to work better with the uppercase letters. So ideally there should be at least two sets of diacritics: lowercase and uppercase marks. (e.g. `acutecomb` and `acutecomb.case`)

## Legacy – Spacing marks

The spacing diacritical marks (for example, U+00B4 `ACUTE ACCENT`) are required mainly for historical reasons and for backward compatibility. This is why they are also known as "Legacy marks".

These marks are only used as placeholder when typing for a combination of keys to add an accent to a base letter e.g. `´` + `a` to obtain a `á`. 

**Requirements::**

- **Legacy marks must have a positive advance width value `≠0`** Due to their function as displaying the accent as a standalone character, they are expected to have an advance width value with positive sidebearings, that is, they should not be zero width glyphs. 
- They should share the design of the `combining marks` for consistency reasons. To ensure this in a practical way, it is suggested to create them by using the combining marks as components in the source file.
- They use the simple name of the mark, e.g. `acute` or `grave`
- They must have the correct Unicode codepoint in your source file to work properly.
- Although they represent marks, they need to behave as though they are base glyphs; that is, in the GDEF table their "Glyph Class" should be 1. ("Base glyph") In the Glyphs "Glyph info" pane, they should have `Category=Mark` and `Subcategory=Spacing`.

## Combining diacritical marks - Nonspacing

As the name suggests, the combining diacritics are the marks actually used to construct the accented letters, which would be done either by:

- Creating the [precomposed characters](https://en.wikipedia.org/wiki/Precomposed_character), the accented letters already included in the font source file, e.g. `00C1 Á LATIN CAPITAL LETTER A WITH ACUTE`
- Or to allow the character composition of the accented letters by using the mark + base glyphs on the fly as the user types, e.g. `0041 LATIN CAPITAL LETTER A` followed by the combining diacritical mark `0301 COMBINING ACUTE ACCENT`, which would be the decomposition or [Unicode equivalence](https://en.wikipedia.org/wiki/Unicode_equivalence) of the above.

### Anchors

All the glyphs involved in the generation of accented letters use *Anchors*, which are special points that allow the attachment of glyphs to one another, that play a key role in the identification of the glyph definition as well as the generation of the "Mark to base positioning" ([`mark`](https://docs.microsoft.com/en-us/typography/opentype/spec/features_ko#tag-mark)) and the "Mark to mark positioning" ([`mkmk`](https://docs.microsoft.com/en-us/typography/opentype/spec/features_ko#mkmk)) features.

Anchors are commonly represented as a red rhombus in the glyph view of the source file and are identified with a name. The name part should be shared among the base glyph and the mark glyph, but in the mark glyph there should be a preceding underscore. For example, there should be a `top` anchor in the base glyph and a corresponding `_top` anchor in the mark.
This name schema is crucial for the positioning to work as expected - for example if the underscore is omitted in the mark glyph, it would not be attached to the base letter - so you must pay special care and attention to them.  

<!-- Include information about stacked diacritics -->


**Requirements for combining marks:**

- **They must have a zero width value once in the font binary `=0`**. During the design process, you could use a 0 sidebearing value to facilitate access to the glyph while working on the source file. But once the font binaries are complied, Glyphs or Fontmake will remove the width value to comply with the requirement that they must be zero value width glyphs (hence the name **nonspacing**).
- The glyph name of combining marks should use the *comb* suffix, e.g. `acutecomb`, `gravecomb`. 
- The outlines' design should follow the design considerations detailed above.
- They must include anchors named as explained above. To better manage the positions for specific language requirements, such as constructing stacked diacritics in Vietnamese, it maybe useful to use custom names: for example, `top_viet` and `_top_viet`, accordingly.
- The amount of combining marks and precomposed glyphs required will be determined by the language support your font intendeds. For Google Fonts see the [Glyphsets](https://googlefonts.github.io/gf-guide/requirements.html#glyphsets) definition.
- They must be assigned the right Unicode codepoint in your source file to work properly. See the [Combining diacritical marks](https://unicode.org/charts/PDF/U0300.pdf) Unicode chart, that ranges from 0300 to 036F codepoints.
- In the GDEF table, their "Glyph Class" should be 3. ("Mark glyph") In the Glyphs "Glyph info" pane, they should have `Category=Mark` and `Subcategory=Nonspacing`.


## Text Shaping process and Open Type Layout


For a text to be displayed in a readable way on screens or desktop apps, there is a required process called [shaping](https://fonts.google.com/knowledge/glossary/shaping) which consist on translating a string of character codes into an ordered sequence of glyphs, and this process is performed by a engines like [Harfbuzz](https://harfbuzz.github.io/what-is-harfbuzz.html)

For text shaping to work, it depends on four factors: the input string given, the inclusion of [Open Type Layout required tables](https://docs.microsoft.com/en-us/typography/opentype/spec/chapter2) in the font, the writing system (script), and the language of the text. For shaping to occur at all, the `GDEF`, `GSUB` and `GPOS` tables must be present in the font.

### The Glyph Definition (GDEF) table

The `GDEF` table provides various glyph properties used in OpenType Layout processing in six types of information provided in different subtables. One of them is the [*GlyphClassDef*](https://docs.microsoft.com/en-us/typography/opentype/spec/gdef#glyph-class-definition-table) that classifies the different types of glyphs in the font. This subtable will identify each glyph in one of the following classes:

| Class | Description                                                   |
|-------|---------------------------------------------------------------|
| 1     | **Base glyph** (single character, spacing glyph)              |
| 2     | **Ligature glyph** (multiple character, spacing glyph)        | 
| 3     | **Mark glyph** (non-spacing combining glyph)                  |
| 4     | **Component glyph** (part of single character, spacing glyph) | 

Both the `GSUB` and `GPOS` tables rely on this information to identify which glyph classes to adjust with lookups.

For any glyph to be classified into the right class, the following must be ensured on each one:

- The glyph name must be correct. For more context please read the [Glyphs app name tutorial](https://glyphsapp.com/learn/getting-your-glyph-names-right)
- Every `combining mark` must have anchors, as well as the letters intended to become a `base letter`.
- The anchors must have the right name (depending on the the schema explained above).

If a glyph is not in the correct class, this may be corrected by using the "Glyph Info" pane in Glyphs and setting the Category and Subcategory fields as described above.

------------------------------------------------------------------------

## Useful links

Design related

- [Problems of diacritic design](https://gaultney.org/jvgtype/typedesign/diacritics/)
- [Diacritics](http://diacritics.typo.cz/index.php?id=12)
- [On diacritics](https://ilovetypography.com/2009/01/24/on-diacritics/)
- [The insects project](http://theinsectsproject.eu/)
- [Polish diacritics how to](http://www.twardoch.com/download/polishhowto/intro.html)
- [Vietnamese Typography](https://vietnamesetypography.com/tone-marks/)
- [Context of Diacritics](https://www.setuptype.com/x/cod/)


Production related

- [Harfbuzz, a text-shaping engine](https://harfbuzz.github.io/what-is-harfbuzz.html)
- [Substitution and Positioning Rules](https://simoncozens.github.io/fonts-and-layout//features-2.html) - advanced reading


<!-- List of contents

What is a diacritic mark and why are they needed

Common design recomendations
    - style coherence - consider weight
    - size
    - v-position
    - h-position
    - lowercase
    - uppercase
    - needed kerning

Legacy Marks
    Which
    Purpose/use
Combining marks
    Which
    Purpose
    Anchors _naming / Viet
    Encodings
Base letters
    Anchors _naming

GDEF table Vs GPOS table differences
Positions on
--> 

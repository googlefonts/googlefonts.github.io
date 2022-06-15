<link href="style.css" rel="stylesheet">

# Diacritic marks
{:.no_toc}

<div class="callout">

🐳 A diacritic is a mark used in combination with a base letter for many purposes, such as modifying the pronunciation by extending a basic alphabet to include more phonemes; adding stress to a word that could differentiate similar words (hence meanings), and in some languages to add or modify a vowel into a word.
<br><br>
Many diacritics are separated from the base letter and can be placed above, below, aside, or through it, while others connect to the base. 
<br><br>

</div>

## Desing considerations 

- Diacritics must be coherent and harmonious with the general design of the font. Take care of details like construction, contrast, thickness, stroke terminal shapes, etc.
- Designing the diacritical marks with the most strict users in mind is suggested. That is respecting conventional contemporary shapes and sizes without reusing or interchanging the forms, e.g. a `breve` with a `caron`.
- Pay attention to the proportion requirements. There are some marks that, once combined with the base letter, will blend and resemble another part of it. E.g. the `horn`.
- Compound letters must be perceived as a whole. The distance to the base letter is crucial and can affect legibility. If the markup is too close to the base font, it could appear to collide with the base letter, adding darker spots to the line of text, especially at small sizes. If the mark is too far from the base letter, they would add a lot of extra noise and make the reading process difficult.
- The horizontal position is also essential for readability. In Latin script, the symmetric marks are placed in the optical center of the base letter while the asymmetric ones follow other rules. But remember, they must be seen as a unity, so they must not be separated or detached from the base letter.
- In Latin script, it is expected that all marks share the same distance to the base letter, or for particular cases like script fonts where the x-hight could variate, at least the same optical distance to the base letter.
- Idiosyncratic or decorative brands have given way to more universal or neutral forms.
- You would need to create all the combining marks required for the language you are giving support to, as well as the so-called Legacy marks. Google Fonts requires at least the GF Latin Core as the minimum set for a font addressing the Latin script. Please read more about our <a herf="https://googlefonts.github.io/gf-guide/requirements.html#glyphsets">Glyphsets</a>.
- Usually, the design of the diacritics needs to be adjusted in size or slope to work better with the uppercase letters. So, ideally, there should be at least two sets: lowercase and uppercase marks. E.g. `acutecomb` and `acutecomb.case`

## Legacy – Spacing marks

The spacing diacritical marks are required mainly for historical reasons and, therefore, for backward compatibility, which is why they are also known as Legacy marks.

They are only used as placeholder when typing for a combination of keys to add an accent to a base letter e.g. `´` + `a` to obtain a `á`. 

**Conditions:**

- **They must have a positive width value.** Due to this function, they are expected to have an advanced width value with positive sidebearings, that is, they should not be 0 width glyphs. 
- They should share the design of the `combining marks` for consistency reasons. To ensure this in a practical way, it is suggested to create them by using the combining marks as components in the source file.
- They use the simple name of the mark, e.g. `acute` or `grave`
- They must have the right Unicode codepoint in your source file to work properly.
- They belong to the mark-spacing category in the Glyphs Definiton of the `GDEF` table.

## Combining diacritical marks - Nonspacing

As the name suggests, the combined diacritics are the marks actually used to construct the accented letters, which would be done either by:

- Creating the [precomposed characters](https://en.wikipedia.org/wiki/Precomposed_character), the accented letters already included in the font source file, e.g. `00C1 Á LATIN CAPITAL LETTER A WITH ACUTE`
- Or to allow the character composition of the accented letters by using the mark + base glyphs on the fly as the user types, e.g. `0041 LATIN CAPITAL LETTER A` followed by the combining diacritical mark `0301 COMBINING ACUTE ACCENT`, which would be the decomposition or [Unicode equivalence](https://en.wikipedia.org/wiki/Unicode_equivalence) of the above.

**Anchors**

All the glyphs involved in the generation of accented letters use *Anchors*, which are special points that allow the attachment of glyphs to one another, that play a key role in the identification of the glyph definition as well as the generation of the Mar to base positioning [`mark`](https://docs.microsoft.com/en-us/typography/opentype/spec/features_ko#tag-mark) and teh Mark to mark positioning [`mkmk`](https://docs.microsoft.com/en-us/typography/opentype/spec/features_ko#mkmk) fetures.

Anchors are commonly represented as red rhombus in the glyph view of the source file and are identified with a name. The name word should be shared among base and mark, but with a preceding underscore in the latter. E.g. `top` in the base letter and `_top` in the mark
Anchors' name schema is crucial for the positioning to work as expected, for example if the underscore is ommited in the mark it would not be attached to the base letter, so you must pay special care and attention to them.  


**Conditions for combining marks:**

- Combining marks name should use the *comb* sufix, e.g. `acutecomb`, `gravecomb`. 
- The outlines desing should follow the design considerations detailed above.
- They must include anchors points named as explained above. To better administrate the positions to language requirements, like stacked diacritics in Vietnamese, it is useful to use custom names for them, e.g. `top_viet` and `_top_viet` accordingly.
- The amount of combining marks and precomposed glyphs required will be determine to the language support your font is intended to. For Google Fonts see the [Glyphsets](https://googlefonts.github.io/gf-guide/requirements.html#glyphsets) definition.
- They must have the right Unicode codepoint in your source file to work properly. See the [Combining diacritical marks](https://unicode.org/charts/PDF/U0300.pdf) Unicode chart, that ranges from 0300 to 036F codepoints.
- They belong to the mark-nonspacing category in the Glyphs Definiton of the `GDEF` table.


## Text Shaping process and Open Type Layout


For a text to be displayed in a readable way on screens or desktop apps, there is a required process called [shaping](https://fonts.google.com/knowledge/glossary/shaping) which consist on translating a string of character codes into an ordered sequence of glyphs, and this process is performed by a engines like [Harfbuzz](https://harfbuzz.github.io/what-is-harfbuzz.html)

For the text shaping to work, it depends on four factors: the input string given, the inclusion of [Open Type Layout required tables](https://docs.microsoft.com/en-us/typography/opentype/spec/chapter2) in the font, the writing system (script), and the language of the text. For non-complex scripts (such as Latin, Cyrillic, Greek, Armenian, Georgian, among others) at least the `GDEF`, `GSUB` and `GPOS` tables would be required in the font.




<!-- Legacy marks are required mainly for historical reasons and therefore backwards compatibility -->


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

List of contents

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

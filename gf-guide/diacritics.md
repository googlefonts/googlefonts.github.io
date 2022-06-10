<link href="style.css" rel="stylesheet">

# Diacritic marks
{:.no_toc}

<div class="callout">

A diacritic is a mark used in combination with a base letter for many purposes, such as modifying the pronunciation by extending a basic alphabet to include more phonemes; adding stress to a word that could differentiate similar words (hence meanings), and in some languages to add or modify a vowel into a word.
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

## Legacy – spacing marks

The spacing diacritical marks are required mainly for historical reasons (they were included in the first ASCII encoding) and therefore backwards compatibility, which is why they are also known as Legacy marks.

They are used as placeholder when you type for a combination of keys to add an accent to a base letter e.g. `´` + `a` to obtain a `á`.

##


<!-- Legacy marks are required mainly for historical reasons and therefore backwards compatibility -->


------------------------------------------------------------------------

## Useful links

Design related
[Problems of diacritic design](https://gaultney.org/jvgtype/typedesign/diacritics/)
http://diacritics.typo.cz/index.php?id=12
https://ilovetypography.com/2009/01/24/on-diacritics/
http://www.twardoch.com/download/polishhowto/intro.html
http://diacritics.typo.cz/index.php?id=12
https://vietnamesetypography.com/tone-marks/
[Context of Diacritics](https://www.setuptype.com/x/cod/)
[The insects project](http://theinsectsproject.eu/)

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

<link href="style.css" rel="stylesheet">

<a href="./index"><button class="button button-i">&larr; GF Guide Index</button></a>

# Description file
{:.no_toc}

<div class="callout">

🦉 The <mark class="grey">DESCRIPTION.en_us.html</mark> file contains the information that appears in the <code>#About</code> section on any specimen page of <a href="https://fonts.google.com">Google Fonts</a> to give further information about the font family.
<br><br>
This file will be created by the team member onboarding the font. Thus the actual file a designer should write carefully would be the <a href="./readmefile">README.md</a> file as the information provided in it is crucial to building a good <a href="https://fonts.google.com/specimen/Brygada+1918#about">#About</a> section.

</div>

<div class="context-reading">
    Background reading:<br>
    <mark class="green"><b>must&rarr;</b></mark> <a href="./readmefile" style="font-weight:bold">README file</a>
</div>

## Table of contents
{:.no_toc}
* TOC goes here
{:toc}

## Requirements

-   **The text length** should be around 500 words, and more than 100 characters.
-   **Allowed HTML elements:** `<a>`, `<em>`, `<i>`, `<strong>`, `<b>`, `<p>`, `<ol>`, `<ul>`, `<li>`
-   **Forbidden HTML elements:**  `<applet>`, `<base>`, `<embed>`, `<form>`, `<frame>`, `<frameset>`, `<head>`, `<iframe>`, `<link>`, `<math>`, `<meta>`, `<object>`, `<script>`, `<style>`, `<svg>`, `<template>`
-   **Other HTML elements:** These are generally **not allowed** either, and will be removed by the catalog web app.
-   **All links in it must be properly working.**
-   **It must include a hypertext link to the upstream repository** — where the font project files are available (designer’s GitHub repository). You can copy the following line, and copy it at the bottom of the description file (don’t forget to adjust the URL):

``` code
To contribute, see <a href="https://github.com/owner/fontname">github.com/owner/fontname</a>
```

-   **Text should be updated when the font is upgraded** to let people know what changed.

    <span style="border-bottom:0.05em solid">Example:</span>

    > This font was upgraded in July 2021 to expand language coverage. It is now supporting Greek and Cyrillic.
-   **We only accept** **`.en_us`** **extension**, but you can definitely add a translation to the description in the case when the font is primarily targeting an audience reading a non-Latin script.

See [Zen+Antique#about](https://fonts.google.com/specimen/Zen+Antique#about) as an example, provided by this file [DESCRIPTION.en_us.html](https://github.com/google/fonts/blob/main/ofl/zenantique/DESCRIPTION.en_us.html).

## Format text with the font family

You may format text with the font family by using HTML span tags with the `"autonym"` class.  This should not be used to style the entire document.  Use it sparingly to document available features in the font family.  For example, to style the text "THIS TEXT" with the font family, enter HTML like this:

```html
<span class="autonym">THIS TEXT</span>
```

## Example

### Without localised text

See [Space+Grotesk#about](https://fonts.google.com/specimen/Space+Grotesk?query=Space+Grotesk#about) provided by [DESCRIPTION.en_us.html](https://github.com/floriankarsten/space-grotesk/blob/master/DESCRIPTION.en_us.html) as an example: it gives plenty of links (mini-website, original authors, referenced font published in GF), and follows all requirements.

**HTML snippet**

``` code
<p>Space Grotesk is a proportional sans-serif typeface variant based on <a href="https://www.colophon-foundry.org">Colophon Foundry's</a> fixed-width <a href="https://fonts.google.com/specimen/Space+Mono">Space Mono</a> family (2016). 
Originally designed by <a href="https://fonts.floriankarsten.com">Florian Karsten</a> in 2018, Space Grotesk retains the monospace's idiosyncratic details while optimizing for improved readability at non-display sizes.</p>

<p><a href=https://floriankarsten.github.io/space-grotesk/><b>→ floriankarsten.github.io/space-grotesk</b><a><p>

<p>Space Grotesk includes Latin Vietnamese, Pinyin, and all Western, Central, and South-Eastern European language support, as well as several OpenType features (old-style and tabular figures, superscript and subscript numerals, fractions, stylistic alternates).</p>

<p>To contribute, see <a href="https://github.com/floriankarsten/space-grotesk" target="_blank">github.com/floriankarsten/space-grotesk</a>.</p>
```

**Result on Google Fonts**

> ***About Space Grotesk***
>
> *Space Grotesk is a proportional sans-serif typeface variant based on* [*Colophon Foundry*](https://www.colophon-foundry.org)*'s fixed-width* [*Space Mono*](https://fonts.google.com/specimen/Space+Mono) *family (2016). Originally designed by* [*Florian Karsten*](https://fonts.floriankarsten.com) *in 2018, Space Grotesk retains the monospace's idiosyncratic details while optimizing for improved readability at non-display sizes.*
>
> *[**→ floriankarsten.github.io/space-grotesk**](https://floriankarsten.github.io/space-grotesk)*
>
> *Space Grotesk includes Latin Vietnamese, Pinyin, and all Western, Central, and South-Eastern European language support, as well as several OpenType features (old-style and tabular figures, superscript and subscript numerals, fractions, stylistic alternates).*
>
> *To contribute, see [github.com/floriankarsten/space-grotesk](https://github.com/floriankarsten/space-grotesk).*

### With localised text

If the “first” script of your font is not Latin, we strongly recommend you to also provide a translation of the description using the actual main script. **This localised text must be in the same HTML snippet as the English text.**

See [Zen+Antique#about](https://fonts.google.com/specimen/Zen+Antique#about) as an example, provided by this file [DESCRIPTION.en_us.html](https://github.com/google/fonts/blob/main/ofl/zenantique/DESCRIPTION.en_us.html).

**HTML snippet**

``` code
<p>Zen Antique features two kinds of Antique Japanese with Kanji.
The impression of the weights (thickness) of strokes are different among characters—Hiragana and Latin alphabets are slightly lighter, 
while Katakana and Kanji are slightly heavier, which gives the unique rhythm and taste in this font.
<a href="https://fonts.google.com/specimen/Zen+Antique+Soft">Zen Antique Soft</a> has a slightly rounded effect on the corners.</p>

<p>To contribute to the project, visit <a href="https://github.com/googlefonts/zen-antique">github.com/googlefonts/zen-antique</a></p>
<p>Zen Antique には、古風な雰囲気の二種類の漢字を含む日本語書体があります。
文字によって画線の太さに変化があり、ひらがなと欧文は細め、カタカナと漢字は太めで、フォントに独特のリズムと味わいを与えています。
また、<a href="https://fonts.google.com/specimen/Zen+Antique+Soft?subset=japanese">Zen Antique Soft</a> では、角が少し丸くなっています。</p>

<p>このプロジェクトに参加して貢献したい方は、次の URL をご参照ください。<a href="https://github.com/googlefonts/zen-antique">github.com/googlefonts/zen-antique</a></p>
```

**Result on Google Fonts**

> ***About Zen Antique***
>
> *Zen Antique features two kinds of Antique Japanese with Kanji. The impression of the weights (thickness) of strokes are different among characters—Hiragana and Latin alphabets are slightly lighter, while Katakana and Kanji are slightly heavier, which gives the unique rhythm and taste in this font. [Zen Antique Soft](https://fonts.google.com/specimen/Zen+Antique+Soft) has a slightly rounded effect on the corners.*
>
> *To contribute to the project, visit [github.com/googlefonts/zen-antique](https://github.com/googlefonts/zen-antique)*
>
> *Zen Antique* には、古風な雰囲気の二種類の漢字を含む日本語書体があります。 文字によって画線の太さに変化があり、ひらがなと欧文は細め、カタカナと漢字は太めで、フォントに独特のリズムと味わいを与えています。 また、*[Zen Antique Soft](https://fonts.google.com/specimen/Zen+Antique+Soft?subset=japanese)* では、角が少し丸くなっています。
>
> このプロジェクトに参加して貢献したい方は、次の URL をご参照ください。*[github.com/googlefonts/zen-antique](https://github.com/googlefonts/zen-antique)*

## The Article

The Article is a new expanded version of the `DESCRIPTION.en_us.html` file that can include images and longer-form information and content. It appears on the Google Fonts site as the main content in the About & License section. For example, see the About page for [Gulzar](https://fonts.google.com/specimen/Gulzar/about), and then view the `ofl/gulzar` directory in the Google Fonts repo: [github.com/google/fonts/tree/main/ofl/gulzar](https://github.com/google/fonts/tree/main/ofl/gulzar). 

The `ARTICLE.en_us.html` file and images should live in an `article/` directory alongside the `METDATA.pb` file in the root of the `ofl/fontname` directory. Typically, only the Noto fonts are expected to combine the `DESCRIPTION.en_us.html` and `ARTICLE.en_us.html` files. For all the other families (non-Noto), if an article with images is added, the description should be overwritten by the Article. This means we should shift all the Description content into the Article and keep and empty the `DESCRIPTION.en_us.html` — note that dev-sandbox will be broken if you remove the description file, so don't.

Here are some guidelines for how to prepare the `article/` directory and files:

**Images**
- Supported image formats: JPG, PNG, SVG, but there is a strong preference for JPG/SVG. JPEGs are optimized so that lower resolution images will be downloaded on smaller viewport sizes.
- Max image size for SVG is 800 KB; for other formats, it is 1.75 MB (enforced by knowledge_graph.py GitHub workflow)
- Width recommended: at least 1000px. No particular proportions are needed; the container will resize the image.
- Resolution: 72dpi.

**Allowed HTML elements:** Same as description with the addition of `<img>` and more elements including: 
`<a>`, `<b>`, `<blockquote>`, `<code>`, `<em>`, `<figcaption>`, `<figure>`, `<hr>`, `<h3>`, `<h4>`, `<h5>`, `<i>`, `<img>`, `<li>`, `<p>`, `<pre>`, `<span>`, `<strong>`, `<ul>`, `<ol>`, `<sub>`
**Forbidden HTML elements:** Remain the same, including:
`<applet>`, `<base>`, `<embed>`, `<form>`, `<frame>`, `<frameset>`, `<head>`, `<iframe>`, `<link>`, `<math>`, `<meta>`, `<object>`, `<script>`, `<style>`, `<svg>`, `<template>`

<link href="style.css" rel="stylesheet">

<a href="./index"><button class="button button-i">&larr; GF Guide Index</button></a>

# Article and Description files
{:.no_toc}

<div class="callout">

🦉 Both the <mark class="grey">ARTICLE.en_us.html</mark> and <mark class="grey">DESCRIPTION.en_us.html</mark> files are used to bring the information that appears in the <code>#About</code> section on any specimen page of <a href="https://fonts.google.com">Google Fonts</a> to provide further information about the font family.
<br><br>
Any of these files will be created by the team member onboarding the font. Thus, the actual file a designer should write carefully is the <a href="./readmefile">README.md</a> file of the font's repository as the information in it will be crucial create a descriptive <a href="https://fonts.google.com/specimen/Kalnia#about">#About</a> section.

</div>

<div class="context-reading">
    Background reading:<br>
    <mark class="green"><b>must&rarr;</b></mark> <a href="./readmefile" style="font-weight:bold">README file</a>
</div>

## Table of contents
{:.no_toc}
* TOC goes here
{:toc}

## The Article

The Article is a new expanded version of the `DESCRIPTION.en_us.html` file that includes images and longer-form information and content. It appears on the Google Fonts site as the main content in the About & License section. For example, see the About page of [Playpen Sans](https://fonts.google.com/specimen/Playpen+Sans/about), and then view the `ofl/playpensans` directory in the Google Fonts repo: [github.com/google/fonts/tree/main/ofl/playpensans](https://github.com/google/fonts/tree/main/ofl/playpensans). 

The `ARTICLE.en_us.html` file and images should live in an `article/` directory alongside the `METDATA.pb` file in the root of the `ofl/fontname` directory. Typically, only the Noto fonts are expected to combine the `DESCRIPTION.en_us.html` and `ARTICLE.en_us.html` files. For all the other families (non-Noto), if an article with images is added, the description should be overwritten by the Article. This means we should shift all the Description content into the Article and delete the `DESCRIPTION.en_us.html`.

Here are some guidelines for how to prepare the `article/` directory and files:

### Requirements

- **Pay attention to the content** Feel free to write a comprehensive text that will pay tribute to your project. Here are added examples of 'About' sections on Google Fonts. <a href="https://fonts.google.com/specimen/Ojuju/about"> Ojuju</a> and <a href="https://fonts.google.com/specimen/Roboto+Flex/about"> Roboto Flex</a>.
- **The text length** should be around 500 words, and more than 100 characters.
- **If the font is derived from another font** it is suggested to mention it in the Description file.
- **All links in it must be properly working.**
- **It must include a hypertext link to the upstream repository** — that is the designer’s GitHub repository. This usually goes at the end of the first paragraph, before the line that separates it from the added text when the article has a long text. 
<br>
You can copy the following line, and copy it at the bottom of the description file (don’t forget to adjust the URL):

    ``` code
    To contribute, see <a href="https://github.com/owner/fontname">github.com/owner/fontname</a>
    ```

-   **The text should be updated when the font is upgraded** to let people know what changed.

    <span style="border-bottom:0.05em solid">Example:</span>

    > This font was upgraded in July 2021 to expand language coverage. It is now supporting Greek and Cyrillic.
-   **We only accept** **`.en_us`** **extension**, but you can definitely add a translation to the description in the case when the font is primarily targeting an audience reading a non-latin script.
-   If the “first” script of your font is not Latin, we strongly recommend you to also provide a translation of the text using the actual main script. **This localised text must be in the same html snippet as the English text.**

### Format text with the font family

You may format text with the font family by using HTML span tags with the `"autonym"` class. This should not be used to style the entire document. Use it sparingly to document available features in the font family. For example, to style the text "THIS TEXT" with the font family, enter HTML like this:

```html
<span class="autonym">THIS TEXT</span>
```

### Images

Please refer to the [Promote yout font](./promotion.md) section of this Guide for a fully detailed information of these images. The following is a summarize of the main specification for the required images.

- Supported image formats: JPG, PNG, SVG, but there is a strong preference for JPG/SVG. JPEGs are optimized so that lower resolution images will be downloaded on smaller viewport sizes.
- Max image size for SVG is 800 KB; for other formats, it is 1.75 MB (enforced by knowledge_graph.py GitHub workflow)
- Width recommended: at least 1000px. No particular proportions are needed; the container will resize the image.
- Resolution: 72dpi.

### Allowed HTML elements

-  `<a>`, `<blockquote>`, `<code>`, `<em>`, `<figcaption>`, `<figure>`, `<hr>`, `<h3>`, `<h4>`, `<h5>`, `<img>`, `<li>`, `<p>`, `<pre>`, `<span>`, `<strong>`, `<ul>`, `<ol>`, `<sub>`
- The Article file can also include `<img>` and `<video>`

 ### Forbidden HTML elements
 
- `<applet>`, `<base>`, `<embed>`, `<form>`, `<frame>`, `<frameset>`, `<head>`, `<iframe>`, `<link>`, `<math>`, `<meta>`, `<object>`, `<script>`, `<style>`, `<svg>`, `<template>`
- The Description file can't include `<img>` and `<video>`
- **Other HTML elements** are generally **not allowed** either, and will be removed by the catalog web app.

## Examples

### Without localised text

See [Space+Grotesk#about](https://fonts.google.com/specimen/Space+Grotesk?query=Space+Grotesk#about) provided by [DESCRIPTION.en_us.html](https://github.com/floriankarsten/space-grotesk/blob/master/DESCRIPTION.en_us.html) as an example: it gives plenty of links (mini-website, original authors, referenced font published in GF), and follows all requirements.


### With localised text

See [Zen+Antique#about](https://fonts.google.com/specimen/Zen+Antique#about) as an example, provided by this file [DESCRIPTION.en_us.html](https://github.com/google/fonts/blob/main/ofl/zenantique/DESCRIPTION.en_us.html).

**Html snippet**

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

## The Description

This file follows the same requirements as the Article file with some exceptions:

- The content might be more succinct.
- It can't include images, so the HTML elements `<img>` and `video` are not allowed.

However, please bear in mind that following our new efforts to promote the fonts, the Description file is considered legacy.
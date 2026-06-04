<link href="style.css" rel="stylesheet">

<a href="./index"><button class="button button-i">&larr; GF Guide Index</button></a>

# The Article file
{:.no_toc}

<div class="callout">

🦉 The <mark class="grey">ARTICLE.en_us.html</mark> file provides the information that appears in the <code>#About</code> section of any specimen page on <a href="https://fonts.google.com">Google Fonts</a>, giving readers further details about the font family.
<br><br>
The team member onboarding the font creates this file. The file a designer should write carefully is the <a href="./readmefile">README.md</a> file of the font's repository, as the information in it is crucial to building a descriptive <a href="https://fonts.google.com/specimen/Kalnia#about">#About</a> section.

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

The Article file includes images and longer-form information and content. It appears on the Google Fonts site as the main content in the About & License section. For example, see the About page of [Playpen Sans](https://fonts.google.com/specimen/Playpen+Sans/about), and then view the `ofl/playpensans` directory in the Google Fonts repo: [github.com/google/fonts/tree/main/ofl/playpensans](https://github.com/google/fonts/tree/main/ofl/playpensans).

The `ARTICLE.en_us.html` file and its images should live in an `article/` directory alongside the `METADATA.pb` file in the root of the `ofl/fontname` directory.

Every family now uses an `ARTICLE.en_us.html` file, even when it contains no images. (The legacy `DESCRIPTION.en_us.html` file has been retired: all of the About content now lives in the Article.)

Here are some guidelines for how to prepare the `article/` directory and files:

### Requirements

- **Pay attention to the content.** Feel free to write a comprehensive text that pays tribute to your project. Here are some examples of 'About' sections on Google Fonts: <a href="https://fonts.google.com/specimen/Ojuju/about">Ojuju</a> and <a href="https://fonts.google.com/specimen/Roboto+Flex/about">Roboto Flex</a>.
- **It should be written in the third person.**
- **Copywriting should not be inappropriate, stereotypical, or offensive.** For example, "This family demonstrates a feminine energy with its fragile aspect" is unacceptable.
- **The text length** should be around 500 words, and no fewer than 100 characters.
- **If the font is derived from another font,** it should mention the original with a URL to the font on Google Fonts if it exists.
- **All links in it must work properly.**
- **It should not contain biography information.** Bio info should go in the [designer's credits](./profile). We accept credits if they are not already mentioned in the credits section (for example, help with development, or the specific names of people involved when only a collective name is credited).
- **It must include a hypertext link to the upstream repository** — that is, the designer's GitHub repository. This line of text usually goes at the end of the first paragraph, before the line that separates it from the added text when the article is long.
<br>
You can copy and paste the following line (don't forget to adjust the URL):

    ``` code
    To contribute, see <a href="https://github.com/owner/fontname">github.com/owner/fontname</a>
    ```

-   **The text should be updated when the font is upgraded,** to let people know what changed.

    <span style="border-bottom:0.05em solid">Example:</span>

    > This font was upgraded in July 2021 to expand its language coverage. It now supports Greek and Cyrillic.
-   **We only accept the** **`.en_us`** **extension,** but you can add a translation to the text when the font primarily targets an audience reading a non-Latin script.
-   If the primary script of your font is not Latin, we strongly recommend that you also provide a translation of the text using the actual main script. **This localized text must be in the same HTML snippet as the English text.**

### Format text with the font family

You may format text with the font family by using HTML span tags with the `"autonym"` class. This should not be used to style the entire document; use it sparingly to document available features in the font family. For example, to style the text "THIS TEXT" with the font family, enter HTML like this:

```html
<span class="autonym">THIS TEXT</span>
```

### Images

The Article file supports images, which must live in the `article/` directory alongside `ARTICLE.en_us.html`. For the full image specifications — formats, file sizes, resolution, and social media requirements — see the [Promote your font](./promotion.md) section of this Guide. In summary:

- Supported formats: JPG, PNG and SVG, with a strong preference for JPG/SVG. JPEGs are optimized so that lower-resolution images are downloaded on smaller viewport sizes.
- Recommended width: at least 1000px. You don't need any particular proportions; the container will resize the image.
- Resolution: 72dpi.
- Maximum file size: 800 KB for SVG; 1.75 MB for other formats (enforced by the `knowledge_graph.py` GitHub workflow).

The images in this repository are licensed under the CC https://creativecommons.org/licenses/by-sa/4.0/. This license mention must be present in the repository, inside the `documentation` folder (see [Promote your font](./promotion.md) for details).

#### Videos

There are two options for including videos in the Article file: an `MP4` with a maximum file size of 1.4 MB, or a `YouTube` link.

- For an `MP4` video, it must follow this format:

   `<video autoplay muted src="your-video-name.mp4" type="video/mp4"></video>`

   or, if you need to loop it:

   ```<video loop autoplay muted src="video1.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>```

   You can use these cases as reference: <a href="https://github.com/google/fonts/blob/main/ofl/danfo/article/ARTICLE.en_us.html">Danfo</a>, <a href="https://github.com/google/fonts/blob/main/ofl/savate/article/ARTICLE.en_us.html">Savate</a>

- The `YouTube` link option requires a cover image to display as a preview, and must follow this format:

   `<a href="https://youtu.be/videoIDnumber"><img src="your-cover-image.png" /></a>`

   `<p><em><a href="https://youtu.be/videoIDnumber">Watch the introduction video on YouTube</a></em></p>`

### Allowed HTML elements

-  `<a>`, `<blockquote>`, `<code>`, `<em>`, `<figcaption>`, `<figure>`, `<hr>`, `<h3>`, `<h4>`, `<h5>`, `<img>`, `<li>`, `<p>`, `<pre>`, `<span>`, `<strong>`, `<ul>`, `<ol>`, `<sub>`
- The Article file may also include `<img>` and `<video>`.

### Forbidden HTML elements

- `<applet>`, `<base>`, `<embed>`, `<form>`, `<frame>`, `<frameset>`, `<head>`, `<iframe>`, `<link>`, `<math>`, `<meta>`, `<object>`, `<script>`, `<style>`, `<svg>`, `<template>`
- **Other HTML elements are generally not allowed** either, and the catalog web app will remove them.

## Examples

### Without localized text

See [Space+Grotesk#about](https://fonts.google.com/specimen/Space+Grotesk?query=Space+Grotesk#about) as an example: it gives plenty of links (mini-website, original authors, referenced font published on GF), and follows all the requirements.

### With localized text

See [Zen+Antique#about](https://fonts.google.com/specimen/Zen+Antique#about) as an example.

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
> *Zen Antique features two kinds of Antique Japanese with Kanji. The impression of the weights (thickness) of strokes are different among characters—Hiragana and Latin alphabets are slightly lighter, while Katakana and Kanji are slightly heavier, which gives the unique rhythm and taste in this font. [Zen Antique Soft](https://fonts.google.com/specimen/Zen+Antique+Soft) has a slightly rounded effect on the corners.*
>
> *To contribute to the project, visit [github.com/googlefonts/zen-antique](https://github.com/googlefonts/zen-antique)*
>
> *Zen Antique* には、古風な雰囲気の二種類の漢字を含む日本語書体があります。 文字によって画線の太さに変化があり、ひらがなと欧文は細め、カタカナと漢字は太めで、フォントに独特のリズムと味わいを与えています。 また、*[Zen Antique Soft](https://fonts.google.com/specimen/Zen+Antique+Soft?subset=japanese)* では、角が少し丸くなっています。
>
> このプロジェクトに参加して貢献したい方は、次の URL をご参照ください。*[github.com/googlefonts/zen-antique](https://github.com/googlefonts/zen-antique)*

<div class="next-reading">
    Further reading:<br>
    <mark class="grey">templ</mark> <a href="./promotion">Promote your font</a>
    <br>
    <mark class="grey">templ</mark> <a href="./profile">Designer Profile</a>
</div>

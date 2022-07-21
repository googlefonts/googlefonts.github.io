<link href="style.css" rel="stylesheet">

<a href="./index"><button class="button button-i">&larr; GF Guide Index</button></a>

# README file
{:.no_toc}

<div class="callout">

🦦  The README.md is a page you find at the root of any repository. It is the first readable text that a user can see when arriving in the repository on GitHub’s website.<br>
<ul>
    <li>GF wants to encourage you to share anything you think may be interesting or relevant about your typeface such as the inspiration, process, challenges you encountered, etc. So this is your moment. You can go wild and write a complete article if you feel like it. You can even include imagery to help illustrate the story.</li>
    <li>Take into account that this file will be taken as the base information that would be used to create the <a href="./description">Description file</a> that feeds the <code>#About</code> section of the specimen page of your font(s) on <code>fonts.google.com/Family+Name#about</code>, e.g. <b>Roboto</b> <a href="https://fonts.google.com/specimen/Roboto#about" target="_blank">https://fonts.google.com/specimen/Roboto#about</a>
    <br>
    As a designer, you would need to care about the <code>README.md</code> rather than creating the description file, as the actual team member who will onboard the font will be able to create the latter if the first is well developed.</li>
</ul>
This page will help designers to write a good README file.

</div>

<div class="context-reading">
    Background reading:<br>
    <mark class="green"><b>must&rarr;</b></mark> <a href="./upstream" style="font-weight:bold">Upstream repository structure</a>
</div>

## Table of contents
{:.no_toc}
* TOC goes here
{:toc}

## What to include

The informations you provide in your font project’s `README.md` is key for GF and for users. It is therefore mandatory to apply the following instructions. Whilst only you can judge what makes sense or not for your font project description in term of detail and length, we can only recommend you to be generous with them:

-   **The name of your font as the title**
  
-   **A concise description that resumes the key points:**

    -   One or two key descriptor(s) (e.g. variable, minimal, grotesque, etc).

    -   Why it was created and what it’s designed to do.

    -   Notable characteristics and features.

    -   Anything extra you want people to know.

    -   Scripts (e.g. Latin, Cyrillic, etc).

    Example:

    > *Roboto Serif is a variable typeface family designed to create a comfortable and frictionless reading experience. Minimal and highly functional, it is useful anywhere (even for app interfaces) due to the extensive set of weights and widths across a broad range of optical sizes. While it was carefully crafted to work well in digital media, across the full scope of sizes and resolutions we have today, it is just as comfortable to read and work in print media.*

-   **At least one image displaying the font (its name, the glyphset, or notable features).**
    <br>
    Typefaces are visual products, images are therefore mandatory for the `README.md`. You could use of the `image.py` tool (provided in the [Google Fonts Project Template repo](https://github.com/googlefonts/googlefonts-project-template/tree/main/documentation)) that you could customize at will and generate at least a black and white image showcasing your font. E.g. [Luxurious Script](https://github.com/googlefonts/luxurious#luxurious-script).
    <br><br>
    However, bear in mind that GF also could use the images you include in the README for the `#about` section of your font family specimen page on Google Fonts, so you would probably like to include more expressive images.
    <br><br>
    You should include at least one at 760 x 506. Additional optional images at 760 x 506 or 360 x 202.

-   **Further research and process definition.**
  
-   **Further development on special features and language support.**
  
-   **A Build section with detailed instructions on how to build the fonts.**
  
-   **A Changelog**
    <br>
    List all the changes of the relevant upgrades indicating dates of release and font version numbers.

-   **Acknowledgements and credits**
    <br>
    List of all the authors and contributors to the project, the role they played, and additional information such as profession, email, website.

-   **A mention to the licence**
    <br>
    It could be the same string required for the nameID 13, that you provide as "License description" from the Font Info pane in your source file:
    > *This Font Software is licensed under the SIL Open Font License, Version 1.1. This license is in this repo* <span style="border-bottom:0.05em solid">*OFL.txt*</span> *and is also available with a FAQ at:* *<https://scripts.sil.org/OFL>.*

## Concrete examples

You may get inspire by these examples to build up your `README.md`. Please note that none is actually perfect, and ideally, you should combine the best part of them all if relevant to your project.

-   [Montagu Slab](https://github.com/floriankarsten/montagu-slab)
    Has a detailed non-standard building process.
    
-   [Texturina](https://github.com/Omnibus-Type/Texturina)
    Has a changelog (aka “Fontlog”) and an extensive language support description.
    
-   [JetBrains Mono](https://github.com/JetBrains/JetBrainsMono)
    Has a comprehensive description of special font features.
    
-   [Brygada 1918](https://github.com/kosmynkab/Brygada-1918)
    Has a short description, and a development about the research and process.
    
-   [Radio Canada](<https://github.com/cbcrc/radiocanadafonts>)
    Has image building automation and a comprehensive axes description.

------------------------------------------------------------------------

## Useful links

-   [About Readmes](https://docs.github.com/en/repositories/managing-your-repositorys-settings-and-features/customizing-your-repository/about-readmes)


<div class="next-reading">
    Further reading:<br>
    <mark class="brown">team&nbsp;</mark> <a href="./description" style="font-weight:bold">Description file</a>
</div>
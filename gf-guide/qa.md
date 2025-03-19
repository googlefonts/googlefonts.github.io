<link href="style.css" rel="stylesheet">

<a href="./index"><button class="button button-i">&larr; GF Guide Index</button></a>

# Quality Assurance
{:.no_toc}

<div class="callout">

🐯 Quality Assurance is an essential factor in Google Fonts. On the one hand, we expect the submitted fonts to follow the best standards and conventions of type design. On the other hand, committed to the understanding of fonts as software, we need to ensure that they fulfill the technical requirements of the major OS, applications, and browsers.
<br><br>
This chapter aims to guide designers to have a more automated approach of their binaries quality assurance. We recommend you install all the tools in a virtual environment, to avoid conflict between packages. Further information is detailed in the <a href="./tools">Tools and Dependencies section</a>. 
<br><br>
For the rest of this chapter, it would be better if you have basic knowledge of:
<ul>
  <li>Using the command line interface</li>
  <li>Installing python packages</li>
</ul>

</div>

<div class="context-reading">
    Background reading:<br>
    <mark class="blue">start</mark> <a href="./tools" style="font-weight:bold">Tools and Dependencies</a>
    <br>
    <mark class="green"><b>must&rarr;</b></mark> <a href="./requirements" style="font-weight:bold">Overall font files requirements</a>
    <br>
    <mark class="yellow">learn</mark> <a href="./build" style="font-weight:bold">Build the fonts</a> 
    <br>

</div>

## Table of contents
{:.no_toc}
* TOC goes here
{:toc}


## Tools 

### Checking the font tables

Beyond the visible outlines of a typeface, each font binary is composed of an ensemble of [required tables](https://learn.microsoft.com/en-us/typography/opentype/spec/otff#font-tables). These tables store fundamental metadata for the font to transmit operating information to the different environments (OS, applications, browsers) and, therefore, for it to function properly in all of them.

Hence, it is important to inspect them to verify all the information is as expected. You can make use of the following 

-   [TTX](https://fonttools.readthedocs.io/en/latest/ttx.html) open XML file, a human-readable version of the font tables;
-   [Font table viewer](https://glyphsapp.com/tools/fonttableviewer) to turn the UFOs into FontTools objects;
-   [DTL OT Master](https://www.fontmaster.nl/otmaster.html) to also edit them.

### Checking with Fontbakery

Fontbakery is our primary quality assurance testing tool to make it easier to check that font projects are optimal, making sure that the fonts **are reliable** before they are submitted to the users.

#### Log levels results

The check results are categorized according to levels of relevance, ranging from ERROR to SKIP. The icons are helpers to identify the severity. Be calm! There-could be many of them. Get comfortable with receiving them and embrace them as a way to improve your font.

- 💔 **ERROR** Is a problem with the program itself, not the fonts. For example a bug or a check that requires an internet connection. 
If you get an Error, please give it a quick look to see which case it is. If it’s not an internet connection issue, please help us to improve the tool by reporting it in the [issue tracker of the Fontbakery repository](github.com/googlefonts/fontbakery/issues).

- 🔥 **FAIL** Is a problem with the font that **must be fixed**. 

- ⚠️ **WARN** Is something worth warning about the font but requires human judgment. It might be something expected by design decision but needs to be considered.

- 💤 **SKIP** Happens when the check does not apply to the given font (for example a static font check will not run when you give it a variable font - like it happens with the overlapping contours check)

- ℹ️ **INFO** Simply prints something useful for information purposes. For example, there is an INFO check that tells you what is the file size impact of hinting on a font.

- 🍞 **PASS** Means the font looks-good for the given checking routine.


#### Profiles

Checks are separated into different collections called profiles (and a profile can include all or some checks from other profiles).

Main profiles are:

- **OpenType Specification.** Checking routines are directly mapped to the requirements of the OpenType specification table by table.

- **Universal.** Collects checks for good practices not formalized by the Open Type spec, but broadly accepted among the type-design community.

- **Vendor Specific.** Requirements that are not useful for everyone but something that is a specific vendor need. 

    - **Google Fonts Profile** is currently the largest one, which includes also the checks from the Open Type, Universal, and other vendor-specific checks (such Adobe). 

    To onboard fonts to Google Fonts they must pass the checks of this profile. Sometimes users consider a reported fail inappropriate, but remember that a FAIL for the googlefonts profile may be only specific to Google Fonts API, not all environments.

    The command to run this profiles is:

    `fontbakery check-googlefonts path/fonts/Family-*.ttf` 

    There is also an option to filter the check result by log-level. For a font to be published in GF it should be at least from Warn level. There is also an option to generate a output file of the report in Markdown format:
    
    `fontbakery check-googlefonts -l WARN --ghmarkdown report.md`

  To see all the commands available in a profile run:
  
   `fontbakery [profile] --help` 

Some foundries created their own profile to have vendor-specific checks. This is the case of Fontwerk and Font Bureau, and you could do it too with a little bit of python skill!



### Proofing with Diffenator2

Diffenator2 is a tool allows you to generate HTML with real words to proof the font functioning, and also to compare two different versions of a font.

To see the available options run one of the following commands:

 `diffenator2 proof --help` or `diffenator2 diff --help`

You can also check for install instructions and more options in its [GitHub repository](https://github.com/googlefonts/diffenator2).


<!-- #### gftools qa

`gftools qa` wraps `gftools gen-html` and `fontbakery`.

`gftools qa -f *.ttf -a -o ~/Desktop/font_QA`
add `-gfb` if you want to have a diff with previous published version on Google Fonts. 

Add note that images are only available to team members. -->

## Outlines and type design

There are many standards and conventions established over centuries around the design and drawing of fonts. Providing a comprehensive list of them goes out of the scope of the current Guide. 

However, you could:

- Start by reading the [How typefaces are designed & fonts are made](https://fonts.google.com/knowledge/introducing_type/how_typefaces_are_designed_and_fonts_are_made) section on the Font Knowledge page which includes some bibliography listed. 

- Read the <a href="./outlines">Outline Quality Checklist</a> and the <a href="./diacritics">Diacritic Marks</a> sections of this Guide.

- And check some helpful links to many resources at the bottom of this page.



------------------------------------------------------------------------

## Useful links

<div id="col1">
    <ul>
      <li><a href="https://font-bakery.readthedocs.io/en/stable/" target="_blanck">Fontbakery's documentation</a></li>
      <li><a hfer="https://github.com/microsoft/Font-Validator" target="_blank">Microsoft's font validator</a> is the official font checking tools for Microsoft environement.</li>
    </ul>
  <b>Type Design</b>
    <ul>
      <li><a href="https://typedesignresources.com/" target="_blank">Type Design Resources</a></li>
      <li><a href="https://typedesignschool.com/" target="_blank">Foundations of Type Design</a></li>
      <li><a href="https://ohnotype.co/blog/tagged/teaching" taget="_blank">OH no Type Teaching</a></li>
    </ul>
  <b>Testing web pages:</b>
    <ul>
      <li><a href="https://wakamaifondue.com/" target="_blank">Wakamai Fondue</a></li>
      <li><a href="https://fontdrop.info/" target="_blank">FontDrop</a></li>
      <li><a href="https://www.axis-praxis.org/specimens/__DEFAULT__" target="_blank">Axis-Praxis</a> 
      and <a href="https://www.axis-praxis.org/samsa/" target="_blank">Samsa</a></li>
      <li><a href="http://www.rosaliewagner.com/font-testing/index.php" target="_blank">Impallari Testing Pages</a></li>
      <li><a href="https://dinamodarkroom.com/gauntlet/" target="_blank">Dinamo Font Gautlet</a></li>
      <li><a href="https://typetools.typenetwork.com" target="_blank">Type Network’s Tools</a></li>
      <li><a href="https://idiotproofed.com/" target="_blank">Idiot Proof</a></li>
      <!-- BROKEN LINK <li><a href="https://www.fontspecimen.com/" target="_blank">Monotype’s interactive font specimen</a></li> -->
    </ul>
</div>

  <div id="col2">
    <b>Testing apps:</b>
    <ul>
      <li><a href="https://www.fontmaster.nl/otmaster.html" target="_blank">DTL OT Master</a></li>
      <li><a href="https://glyphsapp.com/tools/fonttableviewer" target="_blank">Font table viewer</a></li>
      <li><a href="https://github.com/silnrsi/fontproof" target="_blank">Fontproof</a> (still in development)</li>
      <li><a href="https://fontgoggles.org/" target="_blank">FontGoggles</a></li>
    </ul>
  </div>

<div class="next-reading">
    Further reading:<br>
    <mark class="yellow">learn</mark> <a href="./testing" style="font-weight:bold">Local Testing</a>
    <br>
    <mark class="yellow">learn</mark> <a href="./outlines" style="font-weight:bold">Outline quality</a>
    <br>
    <mark class="yellow">learn</mark> <a href="./diacritics" style="font-weight:bold">Diacritics requirements</a>
</div>

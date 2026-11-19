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
    <mark class="yellow">learn</mark> <a href="./build">Build the fonts</a> 
    <br>

</div>

## Table of contents
{:.no_toc}
* TOC goes here
{:toc}


## Tools 

### Checking the font tables

Beyond the visible outlines of a typeface, each font binary is composed of an ensemble of [required tables](https://learn.microsoft.com/en-us/typography/opentype/spec/otff#font-tables). These tables store fundamental metadata for the font to transmit operating information to the different environments (OS, applications, browsers) and, therefore, for it to function properly in all of them.

Hence, it is important to inspect them to verify all the information is as expected. You can make use of the following tools:

-   [TTX](https://fonttools.readthedocs.io/en/latest/ttx.html) open XML file, a human-readable version of the font tables;
-   [Font table viewer](https://glyphsapp.com/tools/fonttableviewer) to turn the UFOs into FontTools objects;
-   [DTL OT Master](https://www.fontmaster.nl/otmaster.html) to also edit them.

### Checking with Fontspector

[Fontspector](https://github.com/fonttools/fontspector) is our primary quality assurance testing tool. It is a Rust port of Fontbakery, which Google Fonts used previously, and runs the same kind of checks much faster. It helps to ensure that font projects are optimal and that the fonts are reliable before being delivered to users.

See the [Tools and Dependencies section](./tools#fontspector) to install it. To check a few fonts without installing anything, you can also use the [web version of Fontspector](https://fonttools.github.io/fontspector/), which runs in your browser without uploading your fonts.

#### Log levels results

The check results are categorised according to levels of relevance, ranging from ERROR to SKIP. The icons used in the HTML and Markdown reports help to identify the severity. Be calm! There could be many of them. Get comfortable with receiving them and embrace them as a way to improve your font.

- 💥 **ERROR** Is a problem with the program itself, not the fonts. For example a bug, or a check that requires an internet connection. 
If you get an Error, please give it a quick look to see which case it is. If it’s not an internet connection issue, please help us to improve the tool by reporting it in the [issue tracker of the Fontspector repository](https://github.com/fonttools/fontspector/issues).

- ☠ **FATAL** Is a critical defect of the font that would break the font-serving infrastructure. It **must be fixed**.

- 🔥 **FAIL** Is a problem with the font that **must be fixed**. 

- ⚠️ **WARN** Is something worth warning about the font but requires human judgment. It might be something expected by design decision but needs to be considered.

- ⏩ **SKIP** Happens when the check does not apply to the given font (for example a check for static fonts will not run when you give it a variable font).

- ℹ️ **INFO** Simply prints something useful for information purposes. For example, there is an INFO check that tells you what is the file size impact of hinting on a font.

- ✅ **PASS** Means the font looks good for the given checking routine.


#### Profiles

Checks are separated into different collections called profiles (and a profile can include all or some checks from other profiles).

Main profiles are:

- **OpenType Specification** (`opentype`). Checking routines are directly mapped to the requirements of the OpenType specification table by table.

- **Universal** (`universal`). Collects checks for good practices not formalized by the OpenType spec, but broadly accepted among the type-design community. It includes the OpenType profile.

- **Vendor Specific.** Requirements that are not useful for everyone but something that is a specific vendor need (for example `iso15008` or `fontwerk`).

- **Google Fonts Profile** (`googlefonts`) is currently the largest one: it includes all the checks from the Universal profile (and therefore from the OpenType profile), plus the checks specific to Google Fonts. 

    To onboard fonts to Google Fonts they must pass the checks of this profile. Sometimes users consider a reported fail inappropriate, but remember that a FAIL for the googlefonts profile may be only specific to Google Fonts API, not all environments.

    The command to run this profile is:

    `fontspector --profile googlefonts path/fonts/Family-*.ttf` 

    By default, only the results from the WARN level and above are displayed; you can change this with the `-l` (`--loglevel`) option. For a font to be published on Google Fonts, you should at least review all the WARN results, and fix all the FAILs. You can also write the report to a file, in Markdown (`--ghmarkdown`), HTML (`--html`) or JSON (`--json`) format:
    
    `fontspector --profile googlefonts -l warn --ghmarkdown report.md --html report.html path/fonts/Family-*.ttf`

  To see all the checks available in a profile run:
  
   `fontspector --profile [profile] --list-checks` 

  To run only some checks, or to exclude some of them, use the `-c` (`--checkid`) and `-x` (`--exclude-checkid`) options. Run `fontspector --help` to see all the available options.


### Proofing with Diffenator3

[Diffenator3](https://github.com/googlefonts/diffenator3) is a Rust port of Diffenator2. It comes with two command-line tools:

-   `diffenator3` compares two versions of a font (for example your new version against the one currently served by Google Fonts) and reports the differences in tables, glyphs, kerning and rendered words, in text, JSON or HTML format:

    `diffenator3 --html --output out/diffenator path/to/old/Family[wght].ttf path/to/new/Family[wght].ttf`

-   `diff3proof` generates HTML proof pages with real words to check how the fonts render in different browsers. It also works with a single font, which is useful when onboarding a new family:

    `diff3proof --output out/proof path/fonts/Family[wght].ttf`

To see all the available options, run `diffenator3 --help` or `diff3proof --help`. Install instructions are available in the [Tools and Dependencies section](./tools#gftools-qa) and in the [GitHub repository](https://github.com/googlefonts/diffenator3). Diffenator3 also has a [web version](https://googlefonts.github.io/diffenator3) to compare two fonts in your browser.


### Using gftools QA

`gftools qa` wraps `fontspector`, `diffenator3`, `diff3proof` and an interpolation checker, which generates a PDF reporting interpolation issues in variable fonts.

From your fonts directory, you can run:

`gftools qa -f *.ttf -a -o qa`

Add `-gfb` (`--googlefonts-before`) if you want to have a diff with the previous version published on Google Fonts. The reports are written in the directory given with `-o` (`out` by default).


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
      <li><a href="https://github.com/fonttools/fontspector/blob/main/USING.md" target="_blank">Fontspector's documentation</a></li>
      <li><a href="https://fonttools.github.io/fontspector/" target="_blank">Fontspector's web version</a></li>
      <li><a href="https://github.com/microsoft/Font-Validator" target="_blank">Microsoft's font validator</a> is the official font checking tool for Microsoft environment.</li>
    </ul>
  <b>Type Design</b>
    <ul>
      <li><a href="https://typedesignresources.com/" target="_blank">Type Design Resources</a></li>
      <li><a href="https://typedesignschool.com/" target="_blank">Foundations of Type Design</a></li>
      <li><a href="https://ohnotype.co/blog/tagged/teaching" target="_blank">OH no Type Teaching</a></li>
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
    <mark class="yellow">learn</mark> <a href="./testing">Local Testing</a>
    <br>
    <mark class="yellow">learn</mark> <a href="./outlines">Outline quality</a>
    <br>
    <mark class="yellow">learn</mark> <a href="./diacritics">Diacritics requirements</a>
</div>

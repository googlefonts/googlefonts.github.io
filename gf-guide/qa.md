<link href="style.css" rel="stylesheet">

<a href="./index"><button class="button button-i">&larr; GF Guide Index</button></a>

# Quality Assurance Tools
{:.no_toc}

<div class="callout">

🐯 This chapter aims to guide designers to have a more automated approach of their binaries quality assurance.
<br><br>
We recommend you install all the tools in a virtual environment, to avoid conflict between packages. Further information is detailed in the <a href="./tools">Tools and Dependencies section</a>. 
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

## Checking the font tabes

Sentence that explain why you would want to check font tables.

-   [TTX]() open xml file, a human readible version of the font tables;
-   [Font table viewer]() to turn the UFOs into FontTools objects;
-   [DTL OT Master]() to aslo edit them.


## Proofing with `gftools gen-html`

Sentence that explains that gftools allows to proof your binaries + generate screenshots from different browsers

Run `gftools gen-html proof --help` or `gftools gen-html diff --help` to see the available options.

Explain here how it is customisable.

## Checking with Fontbakery

Brief description of fontbakery
Explain the different profiles and the log levels.

Log levels:
- PASS
- INFO
- WARN
- FAIL

Main profiles:
- Universal
- Adobe
- Google Fonts

`check-googlefonts` contains all the check from Universal and Adobe, in addition to vendore specific checks that would only apply to fonts which gets published on Google Fonts. Often users complain of inapropriate fails, but remember that a FAIL for the googlefonts profile may be only specific to Google Fonts API, not all environments.

`fontbakery check-googlefonts -l WARN --succinct --ghmarkdown report.md`

Run `fontbakery [profile] --help` to see all the commands.

Some foundries created their own profile to have vendor-specific checks. This is the case of Fontwerk and Font Bureau, and you could do it too with a little bit of python skill!

### gftools qa

`gftools qa` wraps `gftools gen-html` and `fontbakery`.

`gftools qa -f *.ttf -a -o ~/Desktop/font_QA`
add `-gfb` if you want to have a diff with previous published version on Google Fonts. 

Add note that images are only available to team members.

------------------------------------------------------------------------

## Useful links

- [Fontbakery's documentation](https://font-bakery.readthedocs.io/en/stable/)
- [Microsoft's font validator](https://github.com/microsoft/Font-Validator) is the official font checking tools for Microsoft environement.

<div id="col1">
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
      <li><a href="https://www.fontspecimen.com/" target="_blank">Monotype’s interactive font specimen</a></li>
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

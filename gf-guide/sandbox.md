<link href="style.css" rel="stylesheet">

<a href="./index"><button class="button button-i">&larr; GF Guide Index</button></a>

# Reviewing PRs and Sandbox
{:.no_toc}

<div class="callout">

🐯 This chapter aims to share the validation process of a font from the moment it is in a google/fonts PR. To fix issues you will need to know about the other related repository: the Axis Registry, Glyphsets and Lang. You need to know this entire documentation. You need to communicate with the internal engineer team. 

</div>

<div class="context-reading">
    Background reading:<br>
    <mark class="yellow">learn</mark> <a href="./build" style="font-weight:bold">QA Tools</a> 
    <br>
    <mark class="brown">team&nbsp;</mark> <a href="./requirements" style="font-weight:bold">Onboarder workflow guide</a>
    <br>
    <mark class="brown">team&nbsp;</mark> <a href="./requirements" style="font-weight:bold">METADATA file</a>
    <br>
    <mark class="brown">team&nbsp;</mark> <a href="./requirements" style="font-weight:bold">Description file</a>
</div>

## Table of contents
{:.no_toc}
* TOC goes here
{:toc}

## Before merging a PR
### Right panel
- There are at least 2 labels: ready for review + new/upgrade/small fix. 
  If upgrade; an orange label. 
  If complex script: green label.
- PR is in traffic jam
- Issue is linked

### Fontbakery report
- No fails
- No easy-to-fix warns

### Changed files
**METADATA.pb**
- Has all necessary subsets
- If noto: has languages
- If complex script: has primary script
- If optical size axis: check default or override
- Correct designer name
- Correct category
- URL is consistent with description and License

**OFL.txt**
- Consistent github URL with METADATA.pb and Description

**Upstream.yml**
- If Noto: article is linked

**Description**
- No typos
- Respect the rules (3rd person etc.)
- URL is consistent with Licence and METADATA.pb

### Checks (download artifacts)
**Diffenator**

**Diffbrowser**

## If pass
- Add "to sandbox label", remove "ready for review" and merge.
- Add font to the to_sandbox list.

## If issue
- Report the issue in comment of the PR
- Add appropriate label ("need confirmation", "regression", "needs upstream resolutuon" etc.)
- Review again after corrective commit happen


## Checking in Sandbox

-   Making sure the font was pushed
-   To check if the font behave correctly
-   Double checking previous QA before sending to prod. Most problems could be avoided with thorough QA before merging, but errors can happen.

### Home page

-   No Tofu
-   The proper Primary script is displayed

### Specimen

-   Primary script is displayed first
-   No tofu
-   All expected instances (every 100) are displayed and look okay
-   Any kind of weirdness
-   Font style matches category

### Type Tester

-   No tofu
-   All axes work
-   No interpolation issue on the few glyphs displayed

### Glyphs

-   Primary script first
-   Latin style matches the primary script style

### About&License

-   Not empty
-   No typos
-   Correct bios
-   No missing elements (image, URL, etc)

### Download button

-   Package is downloadable
-   Font version is the expected one

### If pass
- Remove "to sandbox", add "to production"
- Add font to `to_production` list

### If issue
- Add "blocked" and "in sandbox", remove "to sandbox"
- report in comment of PR
- re-open issue

## Checking in prod

- Quicly recheck just like in sandbox
- Check it is the proper version
- Add “live” to PR and remove “to prod”



------------------------------------------------------------------------

## Useful links

- 

<div class="next-reading">
    Further reading:<br>
    <mark class="grey">templ</mark> <a href="./testing" style="font-weight:bold">Promo/Marketing</a>
    <br>

</div>

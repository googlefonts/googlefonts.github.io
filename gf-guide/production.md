<link href="style.css" rel="stylesheet">

<a href="./index"><button class="button button-i">&larr; GF Guide Index</button></a>

# Production requirements
{:.no_toc}

<div class="callout">

🐰 <a href="https://fonts.google.com/" target="_blank">Google Fonts</a> (GF) designates in fact two things. First, it is a <b>directory</b> of fonts, which can be downloaded and used locally on your machine. Second, it is also an <b>API</b> that delivers a web service: this means a website can request fonts, and Google Fonts delivers them to the website. In that second case, the fonts are hosted by Google Fonts and not by the website’s own server. 
<br><br>
This section will help users to understand the implications of publishing fonts on the Google Fonts platform, and will review the basic font production considerings and requirements that are mandatory for any Font to be included in the Catalog.

</div>

<div class="context-reading">
    Background reading:<br>
    <mark class="blue">start</mark> <a href="./culture" style="font-weight:bold">Libre Font Culture</a>
    <br>
    <mark class="blue">start</mark> <a href="./required-knowledge" style="font-weight:bold">Knowledge, tools and dependencies required</a>
</div>

## Table of contents
{:.no_toc}
* TOC goes here
{:toc}

## The fonts are massively distributed

Google Fonts is the most-used font platform. According to the [2020 Web Almanac](https://almanac.httparchive.org/en/2020/fonts#serving-with-a-service) (HTTP Archive’s annual state of the web report), 70.3% of websites using font-hosting services use Google Fonts.

As seen in [Google Fonts Analytics](https://fonts.google.com/analytics), the sum of the total views for the fonts in the Catalog increases every day and is currently above 60 trillion views per week (by June of 2022), where many fonts have over a hundred of millions views per week.

Getting a font family published on the website means it has to be included in the GF API for them to be served to websites at that range of views per font. Therefore, GF requires all families to pass a range of checks that ensure that they work well under a wide range of different environments and for a high proportion of users.

**Google treats fonts with the same level of care as they do software.**

## Scalable font production

Google Fonts is doing its best to ensure that publishing or updating fonts are unlikely to break existing documents or websites. Thus, you must follow some rules, which have been adapted from Joel Spolsky's classic article [*The 12 steps to better code*](https://www.joelonsoftware.com/2000/08/09/the-joel-test-12-steps-to-better-code/). Joel’s article explains the benefit of these requirements.

Fonts to be onboarded to Google Fonts are expected to abide by the following requisites:

-   **The design source files (plus scripts) are available** in your preferred font editor format.
    <br>
    The file formats most used are `UFO`, `.glyphs`, `fontforge` or `fontlab 7`. `Fontlab V` files must be converted to another format because the software runs only on older OS versions.

-   **Fonts should be built using open-source tools**.** This ensures that they can be built under the same conditions on any platform.

-   **Fonts should be built in one step.** All GF font production tools can be run from the command line. This allows to use them to generate font families by running a single command.
    <br>
    If the build process necessitates more than one step / one command, then every step needed to build the fonts should be included in a single build script. See [the chapter about building fonts](build.md) for more information.

-   **Font builds must be repeatable.** Given all of GF tools are written in Python and distributed using [pypi/pip](https://pypi.org/), this allows to use specific versions of each package, ensuring the same conditions for each build with the same quality of results.

-   **Projects are kept in a version control system.** Since GF only releases Open Source fonts, each released family is expected to be [hosted in GitHub](./hosting) and have its own [upstream repository](./upstream).

-   **CI ([Continuous Integration](https://martinfowler.com/articles/continuousIntegration.html)) should be used for build and testing purposes,** **[applied to fonts](https://simoncozens.github.io/tdd-for-otl/).** GF main repository [github.com/google/fonts](https://github.com/google/fonts) uses CI. When new fonts are pushed, the CI will run a test suite (`gftools qa`, which is a wrapper around [Fontbakery](https://github.com/googlefonts/fontbakery) and various other proofing scripts), and the results will be reviewed.

-   **Issues and reported Fails should be fixed before publishing or upgrading.**

-   **Reviewers of the [Pull Request](making-pr.md) should have knowledge about typography and font software.**

<div class="next-reading">
    Further reading:<br>
    <mark class="yellow">learn</mark> <a href="./hosting">Hosting projects on Github</a>
    <br>
    <mark class="green"><b>must&rarr;</b></mark> <a href="./upstream" style="font-weight:bold">Upstream repository structure</a>
    <br>
    <mark class="green"><b>must&rarr;</b></mark> <a href="./testing">QA - Local testing</a>
    <br>
    <mark class="yellow">learn</mark> <a href="./build">Build the fonts</a>
</div>
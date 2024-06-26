<link href="style.css" rel="stylesheet">

<a href="./index"><button class="button button-i">&larr; GF Guide Index</button></a>

# Upstream repository structure
{:.no_toc}

<div class="callout">

🐰 Font projects must be hosted on GitHub (or another VCS) and their repositories must be public. Google Fonts accepts private repositories while a project is still in progress, but they must be public once completed.
<br><br>
This guide will help users understand what and why the requested directories, files, and documents are needed in a Google Fonts project.
<br><br>
Before starting this reading, make sure that:
<ul>
    <li><a href="./culture">You have become familiar with Libre Font culture</a></li>
    <li><a href="./hosting">You already know how to use Github</a></li>
    <li><a href="./tools">You have installed all the required tools</a></li>
</ul>

</div>

<div class="context-reading">
    Background reading:<br>
    <mark class="yellow">learn</mark> <a href="./hosting">Hosting projects on Github</a>
</div>

## Table of contents
{:.no_toc}
* TOC goes here
{:toc}

## The Google Fonts Project Template repo

If you read this before you have created your project Github repo, you would like to use the [Google Fonts project template](https://github.com/googlefonts/googlefonts-project-template) repo to start with everything set up for you.

The template is based on [Raphael Bastide’s UFR](https://github.com/unified-font-repository/Unified-Font-Repository) and was adapted to meet Google Fonts' needs. Its purpose is to help type designers set up their repo of open-source fonts — especially if they want to publish them on Google Fonts. A unified structure throughout all the repositories helps GF automate the fonts' quality assurance and onboarding processes in the catalog.

But there is more: the project template incorporates [GitHub Actions](https://docs.github.com/en/actions) to provide users with many automation.

-   The actions will build the font files from the source, use Fontbakery for the Quality Analysis test of the fonts, generate HTML proof sheets, publish them with the test results to HTML files, and generate an *artifact* containing all the files that it has built.
-   You can download the latest artifact (produced fonts) by visiting the Actions tab of your repository.

This is particularly practical if you don’t want to run [gftools](https://github.com/googlefonts/gftools) by yourself: your GitHub repo is doing it for you! The downside is that it is harder to customize for GitHub beginners or people who don’t want to get their hands dirty in some code, and so it may be harder to use for a project that doesn’t follow this exact template.

But give it a try :) Simon Cozens has made a [1 minute video](https://twitter.com/simoncozens/status/1405267459028905984) to show how quick this way to start is.

## The essentials explained

Be aware that the scripts and automated actions provided by the Google Fonts project template are not mandatory, although your font repo still must follow certain requirements.

[Texturina](https://github.com/Omnibus-Type/Texturina) is a good example of a simple repo that only contains the essentials.

``` code
├── AUTHORS.txt
├── CONTRIBUTORS.txt
├── OFL.txt
├── README.md
├── documentation
│   ├── readme-images.jpg
│   └── promo.zip
├── fonts
│   ├── otf
│   │   └── FontFamily-Regular.otf
│   ├── ttf
│   │   └── FontFamily-Regular.ttf
│   ├── webfonts
│   │   └── FontFamily-Regular.woff2
│   └── variable
│       └── FontFamily-[wdth,wght].ttf
├── sources
│   ├── FontFamily.ext
│   ├── FontFamily-Italic.ext
│   └── config.yaml and/or build.sh
├── requirements.txt
└── .gitignore
```

Each file or dir has the following purpose:

*An example is provided for each file (from this Guide or other repositories). Please use these templates and modify what you need.*

-   **[AUTHORS.txt](authors.md)**
    <br>
    Includes contact information for the project's authors. Contributors must not be included in this file.

-   **[CONTRIBUTORS.txt](authors.md)**
    <br>
    Includes contact information for the project's contributors.

-   **[OFL.txt](license-file.md)**
    <br>
    The OFL license file. The first line of the license file must contain the font family's copyright string.

-   **[README.md](readmefile.md)**
    <br>
    Contains information about the font family and instructions on how to build the family. You should take particular care of this file, and you must add at least one image and a short description of your font project.

-   **[documentation](https://github.com/googlefonts/Unified-Font-Repository/tree/main/documentation)**
    <br>
    A directory that contains expanded information about the Family. Optionally, you can store in it your PDF specimen, screenshots or process definition, and the pictures you use for the README.md. This dir may also include:
    -  An `article` subdirectory with the images to be included in the [About](./article.md) section.
    -  A `social-assets` subdirectory with the promotional assets for the social media platforms.
    -  Please read more about these images in the [Promoting your font](promotion.md) section of this Guide.
    -  The `image-license.txt` file detailing the license for these images.

-   **[sources](https://github.com/Omnibus-Type/Texturina/tree/master/sources)**
    <br>
    A directory containing the design source files and scripts used to build the fonts. Sources must not be kept in another directory.

    There must be either a `config.yaml` or `build.sh` file that allows the fonts to be built in one command. For more context, you can read about the [Scalable font production](https://googlefonts.github.io/gf-guide/production.html#scalable-font-production) principle.

    -   [config.yaml](https://github.com/googlefonts/Unified-Font-Repository/blob/main/sources/config.yaml)
        <br>
        A configuration file that includes all the relevant project information for the Builder to build the font files.

    -   [build.sh](https://github.com/googlefonts/lexend/blob/main/sources/build.sh)
        <br>
        A Bash script to build the fonts in one command if the build process requires more than the single config.yaml file to build the font families of this repo.
        
-   [**fonts**](requirements.md)
    <br>
    A directory containing font binaries or subdirectories for each font format. If your project provides multiple formats, do not include them all in one folder. Create a folder for each format e.g `fonts/otf`, `fonts/ttf`, `fonts/webfonts`. The [Builder](build.md) told does that by default.

-   **[requirements.txt](https://github.com/googlefonts/Unified-Font-Repository/blob/main/requirements.txt)**
    <br>
    File listing the Python packages (and their version if necessary) used for a project so that any user can easily install the necessary packages and replicate the production process.

-   **[.gitignore](https://github.com/googlefonts/Unified-Font-Repository/blob/main/.gitignore)**
    <br>
    File specifying untracked files that Git should ignore. Since [the tools](tools.md) should be installed under a virtual environment dedicated to this repository, the `.gitignore` should include the env (or the name of your virtual environment you are using, for example, `venv` or `env`). Indeed, it is better not to push your virtual environment to Github and keep it local. You can add `.DS_Store` to the list of untracked files to keep collaboration between Mac and Windows users. If you use `.glyphs` sources, `*(Autosave)*` is also a relevant addition.

-   **Releases should be tagged**; [Montserrat does this well](https://github.com/JulietaUla/Montserrat/releases).

The files and directories listed above are mandatory. However, we don't mind if you include further docs and dirs, but they should have a clear purpose (such as a `scripts` directory, for example).

------------------------------------------------------------------------

## Useful links

-   [Github release explained](https://docs.github.com/en/repositories/releasing-projects-on-github/managing-releases-in-a-repository)
-   [How to use requirements.txt files](https://pip.pypa.io/en/stable/user_guide/#requirements-files)

<div class="next-reading">
    Further reading:<br>
    <mark class="green"><b>must&rarr;</b></mark> <a href="./readmefile" style="font-weight:bold">README file</a>
  <br>
    <mark class="yellow">learn</mark> <a href="./maintaining">Maintaining your font repo</a>
</div>

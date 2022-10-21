<link href="style.css" rel="stylesheet">

<a href="./index"><button class="button button-i">&larr; GF Guide Index</button></a>

# google/fonts repository explained
{:.no_toc}

<div class="callout">

🦉 <a href="https://github.com/google/fonts">google/fonts</a> is the GitHub repository that is used as a staging area to upload font families to <a href="https://fonts.google.com/">Google Fonts</a>. 
<br><br>
Once your project is ready, and you are sure it meets all the font and production requirements; as well as you have located your files in a GitHub repository that follows the required structure, then the definitive step to contributing your font to Google Fonts is to submit it as a Pull Request to google/fonts repository.
<br><br>
This section will help users understand which are the directories, files, and python modules included in the Google/Fonts repository and how they are related.

</div>

<div class="context-reading">
    Background reading:<br>
    <mark class="green"><b>must&rarr;</b></mark> <a href="./upstream" style="font-weight:bold">Upstream repository structure</a>
</div>

## Table of contents
{:.no_toc}
* TOC goes here
{:toc}

## google/fonts repository explained

### Repository structure

``` code
.
├── AUTHORS
├── CODE_OF_CONDUCT.md
├── CONTRIBUTING.md
├── CONTRIBUTORS
├── README.md
├── TRIVIA.md
├── apache
├── axisregistry
├── catalog
├── knowledge
├── lang
├── ofl
├── ufl
├── to_production.txt
└── to_sandbox.txt
```

### Family directories

The `ofl`, `ufl` and `apache` directories contain font families. There is a directory per family published by GF and each directory has the following structure:

``` code
.
├── DESCRIPTION.en_us.html
├── METADATA.pb
├── License (OFL.txt, UFL.txt, License.txt)
├── FontFamily-Regular.ttf
└── upstream.yaml
```

Each file has the following purpose:

-   [DESCRIPTION.en_us.html](description.md): describes the font family
-   [METADATA.pb](metadata.md): contains metadata related to the family
-   [License](license-file.md): License for the font family. Valid choices are OFL.txt, UFL.txt, License.txt. If you're unsure what license to use, we recommend OFL.txt
-   [.ttf](requirements.md): Family font files.
-   [upstream.yaml](package.md): file linking the font files with the upstream. It is used by the [Packager](package.md) (our onbaording tool) to facilitate the font upgrading process.

If the family is a variable font family, another directory called `static` can be included to contain the static (non-variable) fonts for the family:

``` code
.
├── DESCRIPTION.en_us.html
├── METADATA.pb
├── License (OFL.txt, UFL.txt, License.txt)
├── FontFamily[axis].ttf
├── static
│   ├── FontFamily-Regular.ttf
│       └── FontFamily-Bold.ttf
└── upstream.yaml
```

This static directory is mandatory *if the static fonts are manually hinted;* otherwise, it should not be added at all.

### Designers catalog

``` code
.
├── info.pb
├── bio.html
└── image.png
```

Each credited entity on Google Fonts should have a registered profile in [google/fonts/catalog/designers](https://github.com/google/fonts/tree/main/catalog/designers). This profile appears in the [about](https://fonts.google.com/specimen/Praise?sort=date#about) section of the specimen page.

You can request the addition or modification of your name, bio, and image using [this form](https://docs.google.com/forms/d/e/1FAIpQLSeMwHN8J213ZaxHrr5lHCrX56HY_NjGrWB8o604g98YxuMrdA/viewform).

Find more information about the requirements for these files in [the designer profile chapter](profile.md).

### Axis registry

```code
.
├── axisregistry
```

Google Fonts supports all the [Microsoft registered axes](https://docs.microsoft.com/en-us/typography/opentype/spec/dvaraxisreg) for variable fonts, but it has its own [Axis Registry](https://github.com/googlefonts/axisregistry), which defines the names, ranges, and defaults of additional axes supported by the API. This registry is used to generate the static instances of each variable family (which you can find in the downloadable zip file); the API will generate only those locations registered in the registry.

This directory is a git subtree that is automatically updated with changes in the [googlefonts/axisregistry](https://github.com/googlefonts/axisregistry) repository.  The contents of this directory should not be changed in commits that are pushed to the [google/fonts](https://github.com/google/fonts) repository.  Rather, make edits in a pull request on the [googlefonts/axisregistry](https://github.com/googlefonts/axisregistry) repository.  [google/fonts](https://github.com/google/fonts) repository maintainers can then pull the git subtree changes in to the `axisregistry` directory by executing the following command from the root of [google/fonts](https://github.com/google/fonts):

```code
git subtree pull --prefix=axisregistry https://github.com/googlefonts/axisregistry.git main
```

**Important:** When merging a pull request in the google/fonts repo which contains a subtree pull, merge it using the "Create a merge commit" button and not the "Squash and merge" button. If we squash and merge, the subtree's history is squashed into a single commit which will cause merge conflicts for the next person who has to do a subtree pull. 


### Lang directory

```code
.
├── lang
```

This Python module provides the API with data about [languages](https://github.com/felipesanches/gflanguages/tree/main/Lib/gflanguages/data/languages)/[regions](https://github.com/felipesanches/gflanguages/tree/main/Lib/gflanguages/data/regions)/[scripts](https://github.com/felipesanches/gflanguages/tree/main/Lib/gflanguages/data/scripts) for use in the language-support categorization of the font families in the Google Fonts collection.

This directory is a git subtree that is automatically updated with changes in the [googlefonts/lang](https://github.com/googlefonts/lang) repository.  The contents of this directory should not be changed in commits that are pushed to the [google/fonts](https://github.com/google/fonts) repository.  Rather, make edits in a pull request on the [googlefonts/lang](https://github.com/googlefonts/lang) repository.  [google/fonts](https://github.com/google/fonts) repository maintainers can then pull the git subtree changes in to the `lang` directory by executing the following command from the root of [google/fonts](https://github.com/google/fonts):

```code
git subtree pull --prefix=lang https://github.com/googlefonts/lang.git main
```

**Important:** When merging a pull request in the google/fonts repo which contains a subtree pull, merge it using the "Create a merge commit" button and not the "Squash and merge" button. If we squash and merge, the subtree's history is squashed into a single commit which will cause merge conflicts for the next person who has to do a subtree pull. 

### Push lists

-   `to_sandbox.txt` is a list of font directories or designer directories to be pushed to sandbox.
-   `to_production.txt` is a list of fonts directories or designer directories to be pushed to production. Once the elements (fonts, bio, etc) have been checked and validated in sandbox, they can be sent to the API so users can have access to them. We can only push to production something that was first pushed to sandbox.

<div class="next-reading">
    Further reading:<br>
    <mark class="brown">team&nbsp;</mark> <a href="./description">Description file</a>
  <br>
    <mark class="brown">team&nbsp;</mark> <a href="./profile">Designer profile</a>
  <br>
    <mark class="brown">team&nbsp;</mark> <a href="./metadata">METADATA file</a>
</div>

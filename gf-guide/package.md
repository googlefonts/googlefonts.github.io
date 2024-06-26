<link href="style.css" rel="stylesheet">

<a href="./index"><button class="button button-i">&larr; GF Guide Index</button></a>

# Package the fonts
{:.no_toc}

<div class="callout">

🦦  <a href="https://github.com/googlefonts/gftools/tree/main/docs/gftools-packager">gftools packager</a> is the tool team members use to package fonts from the upstream repo to ship then to <a href="https://github.com/google/fonts">google/fonts</a> repo. It basically replaces <a href="./making-pr">Making a PR to GF</a> process. It saves a lot of time, and prevent lots of human mistakes.
<br><br>
Note that Packager will create a branch on <code>google/fonts</code> directly. 
</div>

<div class="context-reading">
    Background reading:<br>
    <mark class="purple">nerd&nbsp;</mark> <a href="./googlefonts">google/fonts repository explained</a>
    <br>
    <mark class="brown">team&nbsp;</mark> <a href="./metadata.md">METADATA file</a> 
    <br>
    <mark class="purple">nerd&nbsp;</mark> <a href="./making-pr">Making a PR to Google Fonts</a>
</div>

## Table of contents
{:.no_toc}
* TOC goes here
{:toc}

## What the Packager does

### When used on a font family for the first time

This is the process tha Packager allows to automate:

1.  Takes elements from the upstream repo: fonts, OFL.txt, eventually the Article file if available. It can also package fonts from a `tag release`, which is quite practical.
2.  Creates a local branch of your local clone of google/fonts It should follow this scheme: `gftools_packager_ofl_fontname`.
3.  If the font is new, it creates a new font family directory in the `ofl` directory. If the font is an upgrade, it updates the existing directory with the new elements.
4.  Runs [gftools add-fonts](making-pr.md) on the fonts. That script creates or update [METADATA.pb](metadata.md). Packager also create a link to the source repo and commits at which the elements where taken to facilitates any updates. It also adds an empty [ARTICLE.en_us.html file](article.md) if not part of the upstream linked elements.
5.  Commits and pushes that package (step 1-4) onto the branch made at step 2.
6.  Makes a Pull Request to `google/fonts` on a branch of the same name, and write the required description in comment:

    ``` code
    Taken from the upstream repo <repo-url> at commit <commit-url>.
    ```

### When already used before on that font family

Once the font family has been packaged once with the Packager (and that PR has been merged), packager will be able to update the font in `google/fonts` repo very easily. It will use the `source` information included in the `METADATA.pb` file and an endpoint location in google/fonts repo to speed up the entire process.

Note that the font has to be in the same location as before, otherwise you would have to correct `METADATA.pb` first.

## Adding a new fonts with Packager

1.  The Packager needs information about the dont project as well as to know where to find the necessary files (fonts, OFL etc), so we need to provide it in the `METADATA.pb` file to provide such info. Open your terminal and run:

    ``` code
    gftools packager "Font Name" path/to/local/google/fonts
    ```

    This will create a `gftools_packager_ofl_fontname` branch; the `ofl/fontname` directory for the project with a `METADATA.pb` file draft. You will have to fill up all needed informations indirectly from the Terminal using vim or your favorite code editor.
    <br>
    To fill out the Metadata file, it is not necessary to checkout to the gftools branch, do it from the main branch of your local copy of the `google/fonts` repo.
    <br>
    Otherwise, if you are going to modify any of the files included in the package, please checout first to the `gftools_packager_ofl_fontname` branch and modify the files from there.
    <br>
    At the end, you should have this kind of information (refer to the [Metadata](metadata.pb) section of this Guide to fin more details about the required fields):

    ``` code
    name: "Font Name"
    designer: "Foundry Name, Designer Name 1, Designer Name 2"
    license: "OFL"
    category: "MONOSPACE" # Make sure to type the right category for the font project
    date_added: "2024-06-13" # It is automatically added by the tool.
    source {
    repository_url: "https://github.com/MyAccount/MyProject"
    files {
        source_file: "OFL.txt"
        dest_file: "OFL.txt"
    }
    files {
        source_file: "fonts/variable/FontName.ttf"
        dest_file: "FontName.ttf"
    }
    files {
        source_file: "documentation/article/ARTICLE.en_us.html"
        dest_file: "article/ARTICLE.en_us.html"
    }
    files {
        source_file: "documentation/about/font-image1.png"
        dest_file: "arti/font-image1.png"
    }
    branch: "main"
    }

    subsets: "latin"
    subsets: "math"
    subsets: "menu" # This subset is mandatory for all the fonts and it's automatically added by the tool.

    stroke: "SANS_SERIF" # Make sure to type the right stroke for the font project
    classifications: "DISPLAY" # Make sure to type the right classification for the font project
    ```

    → In `files` field the `source_file` is the file path for the files in the upstream repo, and the `dest_file` is the target file and location in `ofl/fontname` directory of `google/fonts` repository.

    → This example above works if the upstream repository in having a `fonts` directory where the binaries are stored. If the fonts are in a zip file of a **tagged release**, and not in a font directory, you should use the `archive_url` field this way:

    ``` code
    repository_url: https://github.com/owner/Font-Name

    archive_url: https://github.com/{owner}/{repo}/releases/download/{version}/project-name.zip

    branch: main
    ```

    → You obtain the link of the zip by right-clicking on it from the upstream repo.

2.  Once the `METADATA.pb` file has been filled out with all the required information, you can run the tool again adding the `-p` otion thatmakes a pull request to google fonts:

    ``` code
    gftools packager "Font Name" path/to/local/google/fonts -p
    ```

The Packager will package all the files from the font upstream repository, commit and push them onto a new branch in the google/fonts repo. 

## Upgrading an existing font with Packager

- If you upgrade an existing font, first check in the font directory in the `ofl` folder (of the main branch) if the `METADATA.pb` already contains the required information well set up. If not, update it following the above specifications. 
  - The informations are correct: make sure the branch and file paths are still up to date.
  - The source URL (or the archive URL) located in [METADATA.pb](metadata.md) is still correct.

If yes, run the command for a to create the PR `gftools packager "Font Name" path/to/local/google-fonts-repo -p`.

- If you need to modify any file included in the package, checkout to the `gftools_packager_ofl_fontname` branch and modify them from there. For example, if you haven't done it directly in the upstream repo, update the [DESCRIPTION.en_us.html or ARTICLE.en_us.html](./article.md), commit in the branch that the Packager created.

- Checkout to the `main` branch of your local copy of the `google/fonts` repo and run the command ``gftools packager "Font Name" path/to/local/google-fonts-repo -p` again to update the PR with the added changes.

### Method that allows editing before PR

If you use the previous method, and if you want to modify your PR, every time you run `-p` argument in conjunction with a “font name”, you will actually re-package and override the PR (because it will ask you to do a force-push). This means that all your manual commits you may have done in between will be lost.

To avoid that, you can first run it without `-p` to package and in a second step, use `-p`. 

Also, keep in mind that every push you make on a google/fonts PR, will trigger the Continuous Integration CI workflow which generate QA reports. If the CI is triggerred multiple times at once, it can happens that it breaks. It is therefore wise to make all modifications to [METADATA.pb](metadata.md) and [ARTICLE.html](article.md) beforehand, and push all the changes at once.

<div class="next-reading">
    Further reading:<br>
    <mark class="brown">team&nbsp;</mark> <a href="./onboarder-workflow">Onboarder workflow guide</a>
</div>

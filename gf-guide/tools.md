<link href="style.css" rel="stylesheet">

<a href="./index"><button class="button button-i">&larr; GF Guide Index</button></a>

# **Tools and Dependencies**
{:.no_toc}

<div class="callout">

Fonts published in Google Fonts comply with the Libre Fonts standards. Therefore, it is required that the fonts can be produced in a single step with open source tools. This ensures compliance with at least the first of the four <a href="./culture">freedoms</a> on which the Movement is based.
<br><br>
Before starting your project, you should set up a working environment with all the tools you will need in development. This guide will help users set up their environment to build the fonts with open source tools that Google Fonts is helping to develop.

</div>

<div class="context-reading">
    Background reading:<br>
    <mark class="blue">start</mark> <a href="./culture" style="font-weight:bold">Libre Font Culture</a>
</div>

## Table of contents
{:.no_toc}
* TOC goes here
{:toc}

## Required knowledge

Font developers are expected to understand the following:

-   Shell scripting (usually `bash`).
-   How to manage Python packages/tools using `pip`, and virtual environments.
-   A basic understanding of the command-line. Users should be able to traverse directories and understand the commands `cd`, `ls`, `mv`, `cp`.

See the useful links section at the bottom of this page to bring you up to speed.

**Note:** If you are not familiar with the concepts listed above, and do not wish to learn about them, we recommend you to try following the [github repository requirements](https://googlefonts.github.io/gf-guide/upstream.html) as closely as possible, as well as the [font file requirements](https://googlefonts.github.io/gf-guide/requirements.html), and a GF Team Member will help you with the tooling and building process of your font.

## Setting up a working environment

Most of these tools are Python-based, but you may need to install some other tools before. *Each OS's specificities* *can’t be detailed here; therefore, it is your responsibility to search the Internet to find the right way to install and use these tools according to your own environment.*

To work with Google Fonts, you would need to install at least:

-   [**Python 3.10**](https://www.python.org/downloads/) or above — to be able to run all the other tools
-   [**gftools**](https://github.com/googlefonts/gftools) — a set of tools used for working with the Google Fonts collection
-   [**Fontbakery**](https://github.com/googlefonts/fontbakery) — a command-line tool for checking the quality of font projects.

### Shell and command-line

A shell is a computer program that makes it possible to interact with an operating system and often is accessible through a text interface, the command-line. The most common shells are the Bourne Again Shell (known as Bash) and Zsh (an extended Bash). The built-in command-line prompts to run the commands are *Terminal* in OS X and *CMD* in Windows. You will need it to install the required tools.

A terminal prompt often looks like this:

``` code
YourUserName:~$
```

`~` being the root of the user directory.

`$` a customizable command prompt, which also indicates your type of shell ($ is the default for bash)

### Homebrew

Homebrew is a package manager for Unix utilities that you can use in macOS so you can install some utilities safely. It uses its own directory to install the packages without messing with the native files of the operative system.

[Install Homebrew](https://brew.sh/#install), and don’t forget to run the two commands at the end of the installation, which will set your PATH environment variable.

On macOS, you will need the Apple developer tools: either Xcode, which is optional and requires a lot of space (\~20Gb) or the light version of it, the [Command Line Tools](https://developer.apple.com/download/all/). These tools are needed to install the GCC (GNU Compiler Collection). Homebrew is supposed to install the XCode Command Line Tools directly, so at this stage, check if it successfully installed them by running: `xcode-select -p`.

### Python 3

Typically, a version of Python is already installed with the Operating System. However, in some cases, this could be still version 2. GF tools requires at least version `3.10`.

You can verify which Python version is installed by running: `python --version`. You may find Python 3 under `python3 --version`. (Same applies for `pip`/`pip3`)

If you already find a Python 3 version installed, you could first confirm its location by running `which python`. The resulting path will help identify whether it was installed using Homebrew or from the package downloaded from the Python site and so you can consult the best way to update it if needed.

There are many implementations of Python. CPython is the reference one written in C, which provides a high level of compatibility with Python packages. PyPy is an interpreter focused on optimization as it runs generally faster, but it does not guarantee compatibility with all Python packages, so we recommend using the former.

To install the **CPython** implementation:

-   you can use Homebrew:

``` code
brew install python
```

-   Or you can use the latest release package from [python downloads](https://www.python.org/downloads/). Don’t forget to double click on `Install Certificates.command` and `Update Shell Profile.command` to add the python path to your bash profile.

Installing python usually comes with `pip` (the standard package manager for Python), allowing you to install and uninstall or freeze the packages. If you work on Mac with an Apple M1 chip, you must first upgrade `pip` to the latest version using `pip install --upgrade pip`.

### Virtual Environments

It is strongly suggested to create and work under a [Python Virtual Environment](https://docs.python.org/3/library/venv.html). This allows you to install and manage packages and modules in an isolated directory for a particular project instead of installing them globally (as part of a system-wide Python). Doing this stops you from creating conflicts with the global site-packages directory (Operating System version) while allowing you to use specific versions of packages for a given project.

1.  To **create** a virtual environment, go to the directory where you want to install it and run the command:

    ``` code
    python3 -m venv myenv
    ```

    The last part of the command is the name you want to give to the virtual environment. Usually, it is only `venv`, or `myenv` if you specifically want to differentiate it from the Python Module "venv" name.
2.  Once you have created your virtual environment, you need to **activate** it.

    On Unix or macOS run:

    ``` code
    source myenv/bin/activate
    ```

    On Windows:

    ``` code
    myenv\Scripts\activate.bat
    ```
3.  After you have activated the virtual environment, the command prompt will display the name of the virtual environment that you are using in parentheses:

    ``` code
    (myenv) userName directoryName $
    ```
3.  To deactivate the virtual environment, just type `deactivate`. Just so you know, closing the Terminal window will also deactivate the environment, and you will have to reactivate it every time you want to work on your project.

You can install as many virtual environments as you want; in each project directory or your user home directory if you intend to use the same virtual environment for all your projects. Command-line tools often have settings to run a command automatically when a new window opens; you could activate one virtual environment this way and avoid having to type it every time.

It is *not* recommended to install virtual environments in clouds, drives, dropbox, etc.

## Installing the required tools

Once you have installed Python, and created and activated your virtual environment, you can install the required tools to produce and test your fonts for Google Fonts.

A [requirements.txt](upstream.md) file listing all the needed tools and dependencies to run a project is required for each project. If you already have one, you can install all the listed tools in it by running one command:

``` code
pip install -r requirements.txt
```

### Fontbakery

Fontbakery is a quality assurance (QA) testing tool. It runs a series of checks on the technical correctness of the exported fonts based on a vendor’s profile. You can find more documentation about it in the GitHub repository [googlefonts/fontbakery](https://github.com/googlefonts/fontbakery).

To install Fontbakery, run the command:

``` code
pip3 install -U fontbakery'[googlefonts]'
```

Run `fontbakery --help` to get an overview of the usage of the fontbakery tool.

### Google Fonts Tools (gftools)

`gftools` is a collection of scripts and tools to modify, build and package fonts for Google Fonts. You can find more documentation about them in the GitHub repository [googlefonts/gftools](https://github.com/googlefonts/gftools).

To install gftools run the command:

``` code
pip install gftools
```

Run the command `gftools --help` to overview all the scripts and [their usage](build.md).

### gftools qa

`gftools qa` is a tool intended for more experienced users that wraps several font QA tools, including Fontbakery, with the `googlefonts` profile. It allows to check fonts against a version already distributed by Google Fonts and create HTML pages that proof the fonts in different environments.

To use `gftools qa`, you will need to generate a [Google Fonts API key](https://developers.google.com/fonts/docs/developer_api#identifying_your_application_to_google). You will then need to create a new text file located on your system at `~/.gf-api-key` (where \~ is your home directory), containing the following:

``` code
[Credentials]
key = your-newly-generated-googlefonts-api-key
```

You will need to install `Harfbuzz`, `Cairo`, `FreeType` and `pkg-config`:

``` code
brew install cairo freetype harfbuzz pkg-config
```

Finally, you can install `gftools qa`:

``` code
pip install 'gftools[qa]'
```

Run `gftools qa --help` to have an overview of the usage of the tool.

For Google Fonts team members, `gftools qa` uses [Browserstack](https://www.browserstack.com) to generate images of the HTML proof pages on different rendering environments (web browsers and operating systems). *This requires additional credentials; if you are a new team member, you need to ask for credentials by email.* The HTML pages can be opened in different web browsers for external users to proof the fonts.

Run the command `gftools qa --help` to overview all the scripts and [their usage](qa.md).

## Recap of your .bash_profile

The `bash profile` (or `z profile` according to your shell script), is loaded before your Command Line Interface (CLI) loads your shell environment and contains all the startup configuration and preferences for your CLI. In Mac OSX, the file is hidden (starts with a `.`) in your home directory. You can display the hidden files (`shift`+`fn`+`cmd`+`.`) and open the file in a code editor. Otherwise, check on the Internet how to find and edit it.

Once you have set up `git` and all the other tools, your bash profile (or z profile according to your shell script) should look like this:

``` code
# PATH for Python3
PATH="path/to/python3/directory:${PATH}"
export PATH

# PATH for homebrew
eval "$(path/to/homebrew/directory shellenv)"

# GF API KEY
export GF_API_KEY="your_gf_api_key_here"

# GITHUB TOKEN
export GH_TOKEN="your_github_token_here"

## Following only applies to team members using gftools qa:

# GF REGRESSION TOKEN
export GFR_TOKEN="token"

# Browserstack credentials
export BSTACK_USERNAME="username"
export BSTACK_ACCESS_KEY="key"
```

------------------------------------------------------------------------

## Useful Links

-   [Bash shell comands cheat-sheet](https://www.educative.io/blog/bash-shell-command-cheat-sheet)
-   [What is a virtual environment](https://realpython.com/python-virtual-environments-a-primer/)
-   [What is a CLI](https://www.w3schools.com/whatis/whatis_cli.asp)
-   [What is shell](https://www.tutorialspoint.com/unix/unix-what-is-shell.htm)
-   [What is Pip](https://realpython.com/what-is-pip/)
-   [Where is my bash profile](https://www.codecademy.com/courses/learn-the-command-line/lessons/learn-command-line-environment/exercises/configuring-environment-bash-profile)
-   [Terminal command shortcuts in Mac](https://support.apple.com/fr-fr/guide/terminal/trmlshtcts/mac)
-   [Python Tutorials](https://realpython.com)

<div class="next-reading">
    Further reading:<br>
    <mark class="yellow">learn</mark> <a href="./hosting">Hosting projects on Github</a>
  <br>
    <mark class="green"><b>must&rarr;</b></mark> <a href="./upstream" style="font-weight:bold">Upstream repository structure</a>
</div>

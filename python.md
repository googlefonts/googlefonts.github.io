This page is meant to capture guidelines for Google Fonts Python projects.

It is written primarily based on the setup for [picosvg](https://github.com/googlefonts/picosvg), [nanoemoji](https://github.com/googlefonts/nanoemoji), [gftools](https://github.com/googlefonts/gftools), and other projects.

## pyproject.toml

We encourage the use of `pyproject.toml` files rather than `setup.py` to store project metadata, dependencies and tooling configuration. Become familiar with the [Writing your pyproject.toml](https://packaging.python.org/en/latest/guides/writing-pyproject-toml/) section of the Python packaging guide.

Here is an example `pyproject.toml`, with reasoning for each section:


```toml
[build-system]
requires = [
   # We continue to use `setuptools` rather than any "fancy" alternative
   # package building/installation library
   "setuptools>=45",
   # We also want to use dynamic versioning, so that git tags become
   # package versions.
   "setuptools_scm[toml]>=6.2"
]
build-backend = "setuptools.build_meta"

# This section is optional; use it if you need to access the version number
# in your package for some reason.
[tool.setuptools_scm]
write_to = "src/mypackage/version.py"

[tool.setuptools.packages.find]
# Package files should be stored in the `src` directory.
# (Despite this recommendation, `Lib` is also commonly used.)
where = ["src"]

[project]
# This picks up the version number from git.
dynamic = ["version"]

name = "mypackage"
description = "Some clever fonts thing"

# Packages should have a README.md, which should be used for the pypi
# long description.
readme = "README.md"

authors = [ 
   # { name = "You", email = "you@google.com" }
]

dependencies = [
   # ... list runtime dependencies here ...
]

[project.optional-dependencies]
dev = [
   # ... list dev dependencies here
]
# And any other optional extras

[project.scripts]
mypackage = "mypackage.__main__:main"
```

## Releases and Versions

Key points:

1. Packages should use [semantic versioning](https://semver.org). This means: *Breaking API changes require a major version bump*. For packages which are still on version 0.x.y, breaking API changes should change the minor (`x`) version number. (But you should also think carefully about what it would take for you to release 1.0.0...)

2. Releases should be automated through GitHub actions.

3. When declaring dependencies on packages we control, use both inclusive and exclusive [ordered comparisons](https://packaging.python.org/en/latest/specifications/version-specifiers/#inclusive-ordered-comparison) to ensure that (a) the latest version is always compatible but (b) you do not install a version with a different API profile. For example, if `gftools` is currently at version `0.6.13`, declare a dependency on `gftools >= 0.6.13, < 0.7`.

### Setting up for releases

To automate the release with GitHub actions, use an action configuration
called `.github/workflows/publish-release.yml`. (Copy the [example action](https://github.com/googlefonts/gftools/blob/main/.github/workflows/publish-release.yml) from `gftools` and modify as appropriate.) In addition to the basic build/test, this action will:

* Create a new GitHub release every time a tag is pushed
* Deploy the new release to Pypi.

In order to make this work, you will need to enable "Trusted publishing" for the repository in [Pypi](https://pypi.org/manage/projects/). This enables the release automation to publish the package.

### Make a release

Use `git tag -a` to make a new annotated tag, or `git tag -s` for a GPG-signed annotated tag, if you prefer.

Name the new tag with with a leading 'v' followed by three MAJOR.MINOR.PATCH digits, using [semantic versioning](https://semver.org/). Look at the existing tags for examples.

In the tag message write some short release notes describing the changes since the previous tag.

Finally, push the tag to the remote repository (e.g. assuming upstream is called `origin`):

```
$ git push origin v0.4.3
```

This will trigger the CI to build the distribution packages and upload them to the [Python Package Index](https://pypi.org/project/gftools/) automatically, if all the tests pass successfully. 

## Code testing and standards

All projects should:

* Be formatted with `black`; ideally this should be tested on PR/commit.
* Follow the [Google Python style guide](https://google.github.io/styleguide/pyguide.html).
* Pass (almost) all `pylint`/`ruff` checks.
* Have a `pytest` test suite, tested by the CI. 

### CI checks

TODO

### pytype

Type hints are your friend. Use them liberally. Fail CI when pytype fails.

`pyproject.toml` configures pytype. At least:

```toml
[tool.pytype]
inputs = ['mypackage']
```

You should also enable inline type hints:

```toml
[tool.setuptools.package-data]
mypackage = ["py.typed"]
```

### Formatting

Use [Black](https://github.com/psf/black)

## Source organization

```
src/module_name/file.py
tests/file_tests.py
# also acceptable
tests/module_name/file_tests.py

.github/workflows/ci.yml  # CI config (see comments in picosvg's example)
tox.ini                   # Config to tox test runner (TODO: why tox?)
pyproject.toml
```

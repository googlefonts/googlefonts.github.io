This page is meant to capture guidelines for Google Fonts Python projects.

It is written primarily based on the setup for https://github.com/googlefonts/picosvg and https://github.com/googlefonts/nanoemoji.

The main capabilities are described along with the file(s) that control them:

## Release automation

Automate releases, tied to tags using semver. Push to PyPI and make corresponding
GitHub releases.

### Make a release

Use `git tag -a` to make a new annotated tag, or `git tag -s` for a GPG-signed annotated tag,
if you prefer.

Name the new tag with with a leading 'v' followed by three MAJOR.MINOR.PATCH digits, like in
[semantic versioning](https://semver.org/). Look at the existing tags for examples.

In the tag message write some short release notes describing the changes since the previous
tag.

Finally, push the tag to the remote repository (e.g. assuming upstream is called `origin`):

```
$ git push origin v0.4.3
```

This will trigger the CI to build the distribution packages and upload them to the
[Python Package Index](https://pypi.org/project/picosvg/) automatically, if all the tests
pass successfully. 

### Release config

*.travis.yml* ([example](https://github.com/googlefonts/picosvg/blob/master/.travis.yml))
```
# In addition to the basic build/test this should
# - deploy to PyPi on tag (see releases section)
# - update GitHub releases on tag
```

*setup.py*  ([example](https://github.com/googlefonts/picosvg/blob/master/setup.py)) indicates we want to use `setuptools_scm`:

```
    name="picosvg",
    use_scm_version={"write_to": "src/picosvg/_version.py"},
    ...
    setup_requires=["setuptools_scm"],
```


## pytype

Type hints are your friend. Use them liberally. Fail CI when pytype fails.

*setup.cfg* configures pytype. At least:

```
[pytype]
inputs = src/SOME_MODULE
```

*setup.py* enables inline type hints:

```
    # this is for type checker to use our inline type hints:
    # https://www.python.org/dev/peps/pep-0561/#id18
    package_data={"picosvg": ["py.typed"]},
```

## Formatting

Use [Black](https://github.com/psf/black)

## Source organization


```
src/module_name/file.py
tests/file_tests.py
# also acceptable
tests/module_name/file_tests.py

.travis.yml             # CI config
dev-requirements.in     # Additional tools for development
dev-requirements.txt    # Generated: pip-compile dev-requirements.in
requirements.txt        # Direct and indirect requirements for automated testing
                        # Generated: pip-compile setup.py
setup.cfg               # pytype config
setup.py                # Establish CLI tools, declare direct dependencies
                        # Do not declare transitive dependencies
                        # Do not declare dependencies that are only for development
                        # Use setuptools
```
This page is meant to capture guidelines for setup and use of Google Fonts Python projects.

It is written primarily based on the setup for https://github.com/googlefonts/picosvg and https://github.com/googlefonts/nanoemoji.

The basic files in the repo are described along with their usage and purpose.

## `.travis.yml`

In addition to the basic build/test this should

 - deploy to PyPi on tag (see releases section)
 - update GitHub releases on tag

See the deploy section of picosvg [.travis.yml](https://github.com/googlefonts/picosvg/blob/master/) for reference.

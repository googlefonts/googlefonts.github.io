<link href="style.css" rel="stylesheet">

<a href="./index"><button class="button button-i">&larr; GF Guide Index</button></a>

# License file
{:.no_toc}

<div class="callout">

🐰 Google initially accepted several libre licenses such as <mark class="grey">OFL</mark>, <mark class="grey">UFL</mark> and <mark class="grey">Apache</mark>.
But today only the OFL is accepted, and that has been the case for many years now.
<br><br>
This page flags some important requirements about the <mark class="grey">OFL</mark> license, as well as a template to copy-paste into your repo.

</div>

<div class="context-reading">
    Background reading:<br>
    <mark class="green"><b>must&rarr;</b></mark> <a href="./upstream" style="font-weight:bold">Upstream repository structure</a>
</div>

## Table of contents
{:.no_toc}
* TOC goes here
{:toc}

## Requirements

-   **The projects submitted must be wholly licensed under the [SIL Open Font License v1.1](http://scripts.sil.org/OFL).**

    This means that there are no proprietary/restricted-license versions of the project available elsewhere (such as additional weights/styles).

-   **First line is the copyright string**

    It must follow this scheme:

    `Copyright { year } The { family } Project Authors ({ git_url })`

    [Project Authors](authors.md) links to a `.txt` file at the root of the repository, which lists all the copyright holders.

-   **There is no Reserved Font Name (RFN) mention.**

    The RFN is an optional element of the Open Font License that forbids a user to fork and modify an open-source font under the *same name*. Only the original version of the font can bear this name. This apply to the design as well as the metadata or the glyphset.

    Since GF distributes a *subsetted* version of the font through the API, the font is not legally considered the same as the original one. Therefore GF wouldn’t be able to publish the font without renaming it. Certainly as a designer you would rather see GF use your preferred font name, rather than be forced to name it something else for the exact same design.

    Sometimes an RFN is necessary:

    -   Typically when the original RFN is respected; the font is itself based on a previous libre font, which had an RFN, and had to be renamed to start with—even though its new name is not under RFN license terms. In that case, the OFL text should mention the original RFN. See the [Lexend](https://github.com/googlefonts/lexend/blob/main/OFL.txt) project as an example.
 
    -   The RFN should be included in the first line of the file, although if it is the second line that is acceptable.
 
    -   An RFN should only state the unique parts of the **family** name only, since reserving (prohibiting) "Sans" or "Mono" or such generic parts from any derivative project is overreaching.

If updated, the RFN should be updated everywhere (source files, OFL.txt, and anywhere else)
    
    -   In other cases, a legal agreement needs to be made between Google and the copyright holders. This is the case for all Adobe and SIL fonts, for example. In that case you should get in contact with your Google Fonts point of contact to start the legal process of allowing GF to use the font name despite the RFN. This is usually done by a simple email from an authorized representative of the RFN holder:

``` code
To: fonts@google.com
Subject: Permission to use Reserved Font Name 

Hi,

I hereby grant permission in perpetuity to Google LLC and affiliates to use the following 
trademarks and Reserved Font Names declared in my SIL Open Font Licence notices 
for fonts served via Google Fonts:

- Unique part of family names
- Unique part of family names

Best Regards,
Firstname Last-name
Company Name 
```

Once the authorisation has been given, the font names should be added to [Fontbakery's exception list](https://github.com/googlefonts/fontbakery/blob/main/Lib/fontbakery/data/googlefonts/reserved_font_name_exceptions.txt) to avoid to fail the font.

-   **All info between the font, the source, and the license should match.**
-   **The OFL.txt file must use the same template as the rest of the Google Fonts Library.**

    You can find that template in the [GF Template Project repo](https://github.com/googlefonts/Unified-Font-Repository/blob/main/OFL.txt), or copy the text below and paste it in a file called `OFL.txt`. You should only modify the first line to match your font project.

## Template

``` code
Copyright 20** The My Font Project Authors (https://github.com/googlefonts/My-Font-Repository)

This Font Software is licensed under the SIL Open Font License, Version 1.1.
This license is copied below, and is also available with a FAQ at:
https://openfontlicense.org


-----------------------------------------------------------
SIL OPEN FONT LICENSE Version 1.1 - 26 February 2007
-----------------------------------------------------------

PREAMBLE
The goals of the Open Font License (OFL) are to stimulate worldwide
development of collaborative font projects, to support the font creation
efforts of academic and linguistic communities, and to provide a free and
open framework in which fonts may be shared and improved in partnership
with others.

The OFL allows the licensed fonts to be used, studied, modified and
redistributed freely as long as they are not sold by themselves. The
fonts, including any derivative works, can be bundled, embedded, 
redistributed and/or sold with any software provided that any reserved
names are not used by derivative works. The fonts and derivatives,
however, cannot be released under any other type of license. The
requirement for fonts to remain under this license does not apply
to any document created using the fonts or their derivatives.

DEFINITIONS
"Font Software" refers to the set of files released by the Copyright
Holder(s) under this license and clearly marked as such. This may
include source files, build scripts and documentation.

"Reserved Font Name" refers to any names specified as such after the
copyright statement(s).

"Original Version" refers to the collection of Font Software components as
distributed by the Copyright Holder(s).

"Modified Version" refers to any derivative made by adding to, deleting,
or substituting -- in part or in whole -- any of the components of the
Original Version, by changing formats or by porting the Font Software to a
new environment.

"Author" refers to any designer, engineer, programmer, technical
writer or other person who contributed to the Font Software.

PERMISSION & CONDITIONS
Permission is hereby granted, free of charge, to any person obtaining
a copy of the Font Software, to use, study, copy, merge, embed, modify,
redistribute, and sell modified and unmodified copies of the Font
Software, subject to the following conditions:

1) Neither the Font Software nor any of its individual components,
in Original or Modified Versions, may be sold by itself.

2) Original or Modified Versions of the Font Software may be bundled,
redistributed and/or sold with any software, provided that each copy
contains the above copyright notice and this license. These can be
included either as stand-alone text files, human-readable headers or
in the appropriate machine-readable metadata fields within text or
binary files as long as those fields can be easily viewed by the user.

3) No Modified Version of the Font Software may use the Reserved Font
Name(s) unless explicit written permission is granted by the corresponding
Copyright Holder. This restriction only applies to the primary font name as
presented to the users.

4) The name(s) of the Copyright Holder(s) or the Author(s) of the Font
Software shall not be used to promote, endorse or advertise any
Modified Version, except to acknowledge the contribution(s) of the
Copyright Holder(s) and the Author(s) or with their explicit written
permission.

5) The Font Software, modified or unmodified, in part or in whole,
must be distributed entirely under this license, and must not be
distributed under any other license. The requirement for fonts to
remain under this license does not apply to any document created
using the Font Software.

TERMINATION
This license becomes null and void if any of the above conditions are
not met.

DISCLAIMER
THE FONT SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO ANY WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT
OF COPYRIGHT, PATENT, TRADEMARK, OR OTHER RIGHT. IN NO EVENT SHALL THE
COPYRIGHT HOLDER BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY,
INCLUDING ANY GENERAL, SPECIAL, INDIRECT, INCIDENTAL, OR CONSEQUENTIAL
DAMAGES, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING
FROM, OUT OF THE USE OR INABILITY TO USE THE FONT SOFTWARE OR FROM
OTHER DEALINGS IN THE FONT SOFTWARE.
```


<div class="next-reading">
    Further reading:<br>
    <mark class="grey">templ</mark> <a href="./authors">Authors and Contributors</a>
    <br>
    <mark class="green"><b>must&rarr;</b></mark> <a href="./readme" style="font-weight:bold">README file</a>
</div>

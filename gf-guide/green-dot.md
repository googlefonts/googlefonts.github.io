# The Google Fonts 'Green Dot Algorithm', for instancing the opsz axis

By [Evan Adams](https://github.com/evanwadams)  
Apr 19, 2021

# Background

In the Google Fonts’ definition of variable font axes, there is a notion of *'fallback positions'* which are static instances intended to be returned to browsers that don’t support VFs.
Say a page requests `wght=621` and is viewed by a browser without VF support, then we’ll return a `wght=600` instance.

Because there are multiple axes and each axis has its own set of fallback positions, we generate the cross-product of all fallback positions.
Weight and width both have 9 positions and opsz currently has 21 positions.
A font that fully supports all three axes will have 1701 instances.

This approach works well for the original problem of requests coming from a browser without VF support.

Download ZIPs have a similar problem, that is, most design tools don’t currently support VFs so, while we include the VF file, we also include static instances.
Originally, we included the same cross-product of instances that were generated for the non-VF browsers, however, in some cases, this resulted in way too many instances and they can take over a design tools’ Fonts menu.

It’s clear we need to limit the number of instances that are included in the Download ZIPs.
The opsz axis is the most troublesome axis as it can have up to 21 fallback positions (two of which were recently added so it’s still growing). 

[Dave Crossland (DC)](https://github.com/davelab6) brought [David Berlow (DB))](https://github.com/dberlow) into the discussion and DB developed a **"Green Dot"** algorithm for the opsz axis that produces 5 or fewer positions on the opsz axis.

# Green Dot Algorithm

## Goals

* To use a maximum of 5 positions on the opsz axis (down from the current 21).  
* Select the positions to best demonstrate the font’s capabilities.

## Approach

The approach is purely algorithmic based on the opsz range supported by the font combined with an understanding of how sizes are used in typography.

The overall size range of interest is 6-144 and it’s divided it into groups:

* 6-12: Small text  
* 12-18: Medium text  
* 18-32: Small headline  
* 31-54: Medium headline  
* 54-144: Large headline

Within each range, the lower bound (min) is inclusive and the upper bound (max) is exclusive.

Equations compute the opsz positions and then they are biased to a set of well-known values, coming primarily from the values offered in the Google Docs fonts size control.
That control goes from 8-96, so 6 and 7 were added on the low end and 120 and 144 were added on the high end.
All these values map to static instances that are created for the non-VF capable browsers, except for size=30 which Docs offers and is not a Google Fonts fallback position.
To simplify implementation, size 30 is replaced with size 28.

This results in the following set of sizes for biasing:

6, 7, 8, 9, 10, 11,  
12, 14,  
18, 24, 28,  
36, 48,  
60, 72, 96, 120, 144

## Algorithm

The basic approach includes:

1. If possible, avoid using a font’s min or max opsz
2. Do some math (details below) to compute five positions
3. Refine the positions by removing duplicates, ensuring a minimum distance between positions, etc
4. Bias each of the positions to the nearest size from the Docs sizes mentioned above

### Details

The following examples use Imbue which has an opsz range of `10..100`.

The first (lowest) green dot position is obtained by finding the smallest range group from the list above that is fully covered by the font’s opsz axis and using that group’s midpoint.
The smallest range Imbue covers is Medium Text and its midpoint is 15.

The fifth (highest) green dot position is obtained by finding the largest range group from the list above that is fully covered by the font’s opsz axis taking that group’s midpoint and then using the midpoint between the group’s midpoint and the font’s maximum.
The largest range Imbue covers is Medium Headline and its midpoint is 36.
Imbue’s maximum is 100, so 68 is used.

To determine the third green dot position, five positions are equally spaced over the font’s opsz range where none of them are the min or max, splitting the range into 6 equal-sized segments and the midpoint of the second segment is used.
Imbue has a range of 90 and 90/6 = 15, making the second segment `25..40` with a midpoint of 32.5

The second green position is the midpoint between the first and third.
For Imbue this is 23.75.

The fourth green position is the midpoint between the third and fifth.
For Imbue this is 50.25.

For Imbue, this yields `[15, 23.75, 32.5, 50.25, 68]`.

Biasing these to the Docs sizes yields `[14, 24, 36, 48, 72]`.

## Refinements

Some edge cases are handled:

1. Redundant positions are removed.  
2. A minimum distance of three between positions is required. (Three is an arbitrary number.)
3. Occasionally a position ends up outside the font’s opsz range; the font’s min or max is then used.
4. Finally, a minimum of two positions are required.  Combined with the minimum distance in \#2 above, this means any font with a range of less than three must be special-cased by using its min and max. Google Sans is an example of such a font as its min is 17 and max is 18.

# Results

| Bodoni-Moda (6-96) | Fraunces (9-144) | Imbue (10-100) | Literata (7-72) |
| :---- | :---- | :---- | :---- |
| 9 | 14 | 14 | 14 |
| 18 | 28 | 24 | 18 |
| 28 | 48 | 36 | 24 |
| 48 | 72 | 48 | 36 |
| 72 | 120 | 72 | 60 |

| Newsreader (6-72) | Piazzolla (8-30 | Texturina (12-72) | Google Sans (17-18) |
| :---- | :---- | :---- | :---- |
| 9 | 14 | 14 | 17 |
| 14 | 18 | 18 | 18 |
| 24 | 24 | 28 |  |
| 36 |  | 48 |  |
| 60 |  | 60 |  |

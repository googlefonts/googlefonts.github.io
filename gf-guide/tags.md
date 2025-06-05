<link href="style.css" rel="stylesheet">

<a href="./index"><button class="button button-i">&larr; GF Guide Index</button></a>

# Tagging process
{:.no_toc}

<div class="callout">

Since 2024, you can find different typographic categories on <a href="https://fonts.google.com/">Google Fonts</a> , making it easier to sort fonts and allowing users to refine their search.

A new step has therefore been added to the font onboarding process, managed by the font onboarders, involving the use of a specially designed tool (*GF Tagger*, written by Marc Foley ✌️) to facilitate the addition of tags.

</div>

<div class="context-reading">
Background reading:<br />
<ul>
    <li><mark class="blue">start→</mark> [Libre Fonts Culture](./culture)</li>
    <li><mark class="blue">nerd→</mark> [Project Prioritization](./prioritization)</li>
</ul>
</div>

## Table of contents
{:.no_toc}
* TOC goes here
{:toc}

## How do Tags work?

Users can now select tags from various filter categories, which are grouped into main sections:

- **Feeling** 
- **Appearance**
- **Calligraphy**
- **Serif**
- **Sans Serif**
- **Technology**
- **Seasonal**

The chosen categories and the number of fonts matching these criteria are displayed at the top of the selection panel.

<br>
<figure>
<img src="./images/onboarder-workflow/gf-tags.png" style="width:2568px" alt="Screenshot of an issue from google/fonts issue tracker." />
<figcaption aria-hidden="true">Google Fonts homepage (March 2025)</figcaption>
</figure>
<br>



## The process


Tagging a new font takes place when the pull request (PR) for that font is ready in the Google Fonts repository, similar to designer profile submissions. Typically, each font receives between 2 and 6 tags, ensuring a variety of tag types. Each font should have at least one or two tags related to appearance or feeling, along with a tag for structural elements such as serifs.

After selecting a tag (e.g., `Cute`), a percentage value must be assigned to rank the font relative to others in the same category. **GF Tagger** provides a list of fonts associated with each tag, allowing for accurate comparison and value assignment.

**How to define tags for a new font?**


1. Open [GF Tagger](https://google.github.io/fonts/tags.html), and keep the font visible to reference its design.
2. In `Add Family`, add the name of the new font family you are tagging.
3. Select a tag that best describes the font and assign a value next to the font family name. Once added, the tag will appear in the `History` section. Repeat this step for each necessary tag.
<br>
<figure>
<img src="./images/onboarder-workflow/tags-process1.png" style="width:2568px" alt="Screenshot of an issue from google/fonts issue tracker." />
<figcaption aria-hidden="true">GF Tagger (March 2025)</figcaption>
</figure>
<br>
4. In GF Tagger, click on `Open PR`, delete all previous entries, and paste the new data. The updated CSV data is automatically copied to your clipboard.
<br>
<figure>
<img src="./images/onboarder-workflow/tags-process3.png" style="width:2568px" alt="Screenshot of an issue from google/fonts issue tracker." />
<figcaption aria-hidden="true">CSV file to update</figcaption>
</figure>
<br>
5. Commit your changes and open a pull request. Make sure to include relevant details for the reviewer, such as the corresponding font PR, an image of the font, and any other useful information.
<br>
<figure>
<img src="./images/onboarder-workflow/tags-process4.png" style="width:2568px" alt="Screenshot of an issue from google/fonts issue tracker." />
<figcaption aria-hidden="true">PR to open on the GF repo</figcaption>
</figure>
<br>


## Collection-Wide Tagging


Onboarders may be asked to add and populate a new tag category. This involves reviewing each family to determine if it fits the new category and creating a tag if applicable.

**How to Create and Populate a New Category?**

1. In `Add Tag`, enter the new tag name, which should include both the category and subcategory, starting with a `/` (e.g., `/Expressive/Funky`), then click the `Add` button.

2. Click `Edit > Insert Placeholder Tags`. A placeholder tag will appear for each family in the collection.

3. Review each placeholder tag and either delete irrelevant ones or assign a percentage score.

To speed up the process, use the up/down arrow keys to navigate between tags or press "!/@" to blur inactive tags (Zen mode). Press "Esc" to exit Zen mode.

4. Once tagging is complete, remove placeholder tags by clicking `Edit > Remove Placeholder Tags`.

5. Open a PR as described in Step 4 of the previous section.

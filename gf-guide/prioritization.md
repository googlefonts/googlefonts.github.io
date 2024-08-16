<link href="style.css" rel="stylesheet">

<a href="./index"><button class="button button-i">&larr; GF Guide Index</button></a>

# Prioritization of Adding & Upgrading Fonts to Google Fonts
{:.no_toc}

<div class="context-reading">
  
  Background reading:  
     <mark class="blue">start</mark> **[Adding & Upgrading Fonts to Google Fonts](./onboarding)**
     
</div>

## Table of contents
{:.no_toc}
* TOC goes here
{:toc}

## Priority Definitions

| Tag | Label | Meaning | Qualifier(s) | Expected Frequency | Target Schedule |
|---|---|---|---|---|---|
| P0 | Top Priority | Our top priority. | <li>A large Google Product is blocked from achieving some goal, or soon to be blocked. | Very rare on an annual basis. | To be fully completed ASAP: As Soon As Possible, to the exclusion of other tasks/projects. |
| P1 | High Priority | Our top priority, given no active P0 projects. | <li>A large Google Product wants to use this project, but won't be blocked (so, the Google Fonts team has some time)<li> A significant Google customer (e.g. a large organization using Workspace) is blocked, soon to be blocked, or is unhappy enough to consider leaving<li> A negative PR event could result, such as missing a major industry deadline (e.g. an upcoming Unicode release). | Rare per quarter, but are expect a few times a year. | Defined timeline from the customer. |
| P2 | Important | Expected completion with the annual quaterly planning period, given no pending P0 or P1 projects. | <li>A small Google Product, or paying customer, or a non-paying significant customer/user, needs it<li> A minor PR event could be negatively impacted<li> An existing high usage family has a bug, and the fix will improve pages/documents already using it in a meaningful way. | A small share of activity per quarter. | Quarterley, but can slip. |
| P3 | Desirable | Accepted with gusto, but without urgency. | <li>An especially nice project that Google employees would like to ship sooner than later<li> An existing low usage family has a bug, and the fix will improve existing documents in a meaningful way | A large share of activity per quarter. | Quarterley, but can slip. |
| P4 | Accepted | Evaluated as worthy of onboarding, but without urgency. | <li>A nice project that Google employees would like to ship. | The majority of projects submitted to Google Fonts by the public, trumped by higher priorities as defined above. | As we have capacity, after completing higher priority projects. |

## Prioritization FAQs

### Why does this prioritization framework exist?

This prioritization framework exists to created shared understanding of how Google Fonts allocates finite resource - and in proportion to the amount of work available, very limited resources - for onboarding new and updated font projects to Google Fonts.
This shared understanding is primarily between the people active on this public repo, and the internal Google Fonts team members who are rarely or never seen on the public Github repos.

It is refreshed during a quarterly planning process, led by a Google Fonts team [Program Manager](https://www.google.com/search?q=Program+Manager).
The quarerly plan surfaces all known deadline-driven onboarding work as early as possible to the Google Fonts team, so that it is factored into internal quarterly resource allocation planning.

Concretely: The Program Manager will directly track, communicate and coordinate as needed, including maintaining an internal spreadsheet of priority P1 and P2 projects that is shared with the wider Google Fonts team at the beginning of each quarter, based on Github Issues tags.
If the list requires updates during the current quarter, the Program Manager will communicate changes to the Google Fonts internal leadership team within one week of the plan update.

### What distinguishes P1 vs P2?

Generally speaking, distinguishing P1 vs P2 is informed by product-area user-base volume.
So, the flagship billion-user products will take priority over smaller products with fewer users, if the two are in competition in a given quarter.
Realistically this rarely happens, but in such cases, we communicate the prioritized push queue status to everyone involved, and allow for negotiations.

### What does “high usage” mean?

It depends.
An issue can move from P3 to P2 to P1 based on the severity of the problem, combined with the popularity in context (eg, popularity in CSS API, or Android Downloadable Fonts, within Workspace editors, etc).
This is a judgment call when evaluating the issue: If the answer isn't obvious, whoever is assigning priorities should consult with their manager.

<link href="style.css" rel="stylesheet">

<a href="./index"><button class="button button-i">&larr; GF Guide Index</button></a>

# Prioritization of Adding & Upgrading Fonts to Google Fonts
{:.no_toc}

<div class="context-reading">
  
  Background reading:  
     <mark class="blue">start</mark> **[Adding & Upgrading Fonts to Google Fonts](./onboarding)**</a>
     
</div>

## Table of contents
{:.no_toc}
* TOC goes here
{:toc}

## Priority Definitions

### P0: Top Priority

A large Google Product is blocked from achieving some goal, or soon to be blocked?

This will get a "P0" tag, and is our top priority.
These are (and should be) very rare on an annual basis.

Target schedule: ASAP (As Soon As Possible, to the exclusion of other tasks/projects.)

### P1: High Priority

A large Google Product wants to use this project, but won't be blocked (so, the Google Fonts team has some time)?

A significant Google customer (e.g. a large organization using Workspace) is blocked, soon to be blocked, or is unhappy enough to consider leaving?

A negative PR event could result, such as missing a major industry deadline (e.g. an upcoming Unicode release)?

This will get a "P1" tag, and is our top priority given no active P0 projects.
These are (and should be) rare per quarter, but are expect a few times a year.

Target schedule: Defined timeline from the customer.

### P2: Important Priority

A small Google Product, or paying customer, or a non-paying significant customer/user, needs it?

A minor PR event could be negatively impacted?

An existing high usage family has a bug, and the fix will improve pages/documents already using it in a meaningful way?

This will get a "P2" tag, and is given priority to be completed within the planned quarter, given no pending P0 or P1 projects.
These are expected to make up a small share of activity per quarter.

Target schedule: Quarterley, but can slip.

### P3: General Priority

A nice project that Google employees would like to ship sooner than later?

An existing low usage family has a bug, and the fix will improve existing documents in a meaningful way?

This will get a "P3" tag, and is including in quarterly planning, but may slip into future quarters.
These are expected to make up a large share of activity per quarter.

Target schedule: Quarterley, but can slip.

### P4: No Priority

Worthy of onboarding, but no urgency?

This will get a "P4" tag, and the majority of projects submitted to Google Fonts by the public likely land here.

Target schedule: When we have capacity, after completing higher priority projects.

## Prioritization FAQs

### What distinguishes P1 vs P2?

Generally speaking, distinguishing P1 vs P2 is informed by product-area user-base volume.
So, the flagship billion-user products will take priority over smaller products with fewer users, if the two are in competition in a given quarter.
Realistically this rarely happens, but in such cases, we communicate the prioritized push queue status to everyone involved, and allow for negotiations.

### What does “high usage” mean?

It depends.
An issue can move from P3 to P2 to P1 based on the severity of the problem, combined with the popularity in context (eg, popularity in CSS API, or Android Downloadable Fonts, within Workspace editors, etc).
This is a judgment call when evaluating the issue: If the answer isn't obvious, whoever is assigning priorities should consult with their manager.

### How will we communicate onboarding priorities and known deadlines during our quarterly planning process?

A Google Fonts team [Program Manager](https://www.google.com/search?q=Program+Manager) will directly track, communicate and coordinate as needed, including maintaining an internal spreadsheet of priority P1 and P2 projects that is shared with the wider Google Fonts team at the beginning of each quarter, based on Github Issues tags.
If the list requires updates during the current quarter, the Program Manager will communicate changes to the Google Fonts internal leadership team within one week of the plan update.
One of the primary goals of this communication plan is to surface all known deadline driven onboarding work as early as possible to the team.

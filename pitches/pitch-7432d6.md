---
id: pitch-7432d6
kind: pitch
title: The form says what it means
parent: proj-3a84fc
status: done
owner: claude
assignees: [claude]
reviewers: [jcanton]
priority: medium
cycle: 1
start_date: 2026-09-04
end_date: '2026-09-04'
prs: ['plantbutler/backend#21', 'plantbutler/app#14']
tags:
- app
- backend
created_schema_version: 5
person_weeks: 0.5
---
## Problem
The pot form is seventeen boxes labelled in wire names, and three of them are worse than unclear.

`plant_type` is free text keyword-matched against eight words, and it is the only thing that picks
the base moisture band — an unlabelled plant starts at 35–55%, a succulent at 15–30%. So typing
"basil" looks saved, matches nothing, and costs twenty points silently. `pot_size` and `plant_size`
are free text too: `pot_size` reads only the words *small* and *large*, so the README's own
`pot_size=14cm` example and the `"3"` in the live garden move the band by nothing at all, and
`plant_size` is read by nothing whatsoever. And nothing on the screen says what a target percentage
is measured against, that dose/cooldown/daily cap are three limits, or that disabling a pot leaves
its hose claimable.

## Appetite
Half a person-week, one backend PR and one app PR. No new screens.

## Solution
An ⓘ beside every field, opening one sentence. `plant_type` becomes a closed set of six kinds plus
*not sure*, refused on write and still tolerated on read. The two sizes become measurements —
`pot_diameter_cm` and `plant_height_cm` — and the band reads the pot as a water buffer: the shift
is linear in the log of the volume, not the volume, so 10 cm and 24 cm land where the old keywords
sat and everything between finally means something. Height is read over diameter. A species lookup
pre-selects the kind from GBIF's family, into an empty field only.

## Rabbit holes
The cube. Volume goes as d³, but a 40 cm pot holds 23× a 14 cm one and no band survives being
multiplied by 23 — see decision 21. And the family table: it is a guess and will be wrong, which is
only affordable because it fills a visible dropdown a tap can change.

## No-gos
No care source ever sets a watering number; none of them has one. No new wire concept for clearing
a field — picking *not sure* over a stored kind still says "cannot clear", like every other field.

## Progress
Both PRs merged 2026-09-04. Backend 0.15.0 deployed and verified live: `add_columns()` ran on the
NAS database, carrying the live garden's `"10"` and `"3"` into `plant_height_cm` and
`pot_diameter_cm`, and that pot's offer went from `flower` to `flower, 3 cm pot, 10 cm plant` —
the first time either size has moved a band. 399 backend tests, 302 app tests.

---
id: pitch-6ded95
kind: pitch
title: Three samples, not one
parent: proj-3a84fc
status: done
owner: claude
assignees: [claude]
reviewers: [jcanton]
priority: low
cycle: 1
start_date: 2026-09-03
end_date: '2026-09-03'
prs: ['plantbutler/app#9']
tags:
- app
created_schema_version: 5
person_weeks: 0.25
---
## Problem
The calibration wizard captures one reading per endpoint, so a single noisy sample sets a pot's
whole scale for as long as nobody recalibrates. The app's own notes already flag this as the thing
to revisit once a real probe is in soil.

## Appetite
A quarter person-week: a change to the wizard's reducer, and its tests.

## Solution
Each endpoint takes the median of the last three fresh readings, and the wizard shows how many it
has. Tapping on with fewer than three is allowed and says so.

## Rabbit holes
- Freshness is already judged on the phone clock against the reading's arrival. Three samples must
  be three distinct reports, not one report counted three times.

## Progress
Done 2026-09-03. Each endpoint is the median of up to three reports, and the wizard says how many
it has.

The rabbit hole it named was already closed: `remember` has always kept readings distinct by
`readTs`. There is a test for it now so it stays closed.

Review found a regression the change itself introduced, in the wet direction. The speed-up step
proves the board obeyed by seeing two reports close together, and it handed those reports to the
air step — harmless when only the newest was used, but a median folds them in, and they were taken
before "hold it in the AIR" was ever shown. A dry endpoint calibrated against soil makes a pot at
half moisture read as parched, and the rules water it. The air step starts empty now.

## No-gos
No change to the arming and restore dance around the interval knob.

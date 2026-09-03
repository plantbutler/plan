---
id: pitch-6ded95
kind: pitch
title: Three samples, not one
parent: proj-3a84fc
status: ready
owner: claude
assignees: [claude]
reviewers: [jcanton]
priority: low
cycle: 1
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

## No-gos
No change to the arming and restore dance around the interval knob.

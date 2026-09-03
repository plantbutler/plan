---
id: pitch-64815f
kind: pitch
title: Something to look at off the tailnet
parent: proj-3a84fc
status: ready
owner: claude
assignees: [claude]
reviewers: [jcanton]
priority: medium
cycle: 1
tags:
- app
created_schema_version: 5
person_weeks: 0.5
---
## Problem
The app holds nothing between launches. Off the tailnet, or with the NAS down, every screen is the
Trouble screen. v1 said no offline mode on purpose; the cost turns out to be that the app is blank
exactly when you are away from home and wondering about the plants.

## Appetite
Half a person-week. A read-only cache, not offline editing.

## Solution
The last good `/pots` and `/health` are written to disk and shown immediately on launch, stamped
with how old they are, while a refresh runs behind them. Actions stay disabled against stale data;
nothing is queued to send later.

## Rabbit holes
- A stale reading shown without its age is worse than showing nothing. The age has to be as
  prominent as the number.
- Percentages are derived from calibration, so the calibration they were read with has to be cached
  alongside them or the cached curve lies after a recalibration.

## No-gos
No queued writes, no conflict resolution, no cached history curves in this pitch.

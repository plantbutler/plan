---
id: pitch-64815f
kind: pitch
title: Something to look at off the tailnet
parent: proj-3a84fc
status: done
owner: claude
assignees: [claude]
reviewers: [jcanton]
priority: medium
cycle: 1
start_date: 2026-09-03
end_date: '2026-09-03'
prs: ['plantbutler/app#8']
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

## Progress
Done 2026-09-03. The last good `/pots` and `/health` in one JSON file, shown at launch, stamped
with its age, every write refused while it is up and nothing queued for later.

Both rabbit holes were real. The second — cache the calibration or the curve lies — is answered by
storing whole pots and no derived value at all; `pct` is stripped on the way to disk and derived
back from the cached raw, so a recalibration reinterprets the cached numbers exactly as it does
live ones.

Review found the cache could lose the race that matters: it only filled a screen still Loading,
but off the tailnet the network fails fast and beats the disk, so the failed fetch put up Trouble
and the cache gave up — blank in the one case the pitch exists for. It fills anything that is not
already a Ready now.

## No-gos
No queued writes, no conflict resolution, no cached history curves in this pitch.

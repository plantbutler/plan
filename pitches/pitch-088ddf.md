---
id: pitch-088ddf
kind: pitch
title: Water now and a chart
parent: proj-8fb1fc
status: shaping
priority: medium
depends_on: [pitch-7ca138, pitch-1b1e91, pitch-cd0f19]
tags:
- app
created_schema_version: 5
person_weeks: 1
---
## Problem
From the sofa: see one pot's curve and tap to water it — the moment the project exists for.

## Appetite
One person-week.

## Solution
One detail screen: the pot's moisture history and a water-now button that queues a command through
the hand-off, with status queued/done from the log, honestly labelled "up to about three minutes".

## Rabbit holes
- Charting in Compose: pick one library or a fifty-line Canvas polyline on the first evening.

## No-gos
No duration picker, no push, no watering-history view, one confirmation dialog at most.

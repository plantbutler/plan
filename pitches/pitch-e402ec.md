---
id: pitch-e402ec
kind: pitch
title: Rules that water
parent: proj-81a6d7
status: shaping
priority: medium
depends_on: [pitch-1b1e91, pitch-553c1b, pitch-28a903]
tags:
- backend
created_schema_version: 5
person_weeks: 1
---
## Problem
Every watering is still a manual command; the butler should water when a pot is dry and refuse when
it is not safe.

## Appetite
One person-week.

## Solution
Smooth over a window, N consecutive dry readings, per-pot cooldown, daily cap, quiet hours; never
enqueue on a stale heartbeat or an empty reservoir. Testable offline against the fake device. Done
means one pot watered automatically in the flat during a supervised week.

## Rabbit holes
- Rule tuning on noisy sensors.

## No-gos
No weather, no ML, no per-species profiles, no closed loop during a dose.

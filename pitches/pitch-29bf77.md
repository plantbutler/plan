---
id: pitch-29bf77
kind: pitch
title: Manifold that knows where it is
parent: proj-226479
status: shaping
priority: high
depends_on: [pitch-cd0f19]
tags:
- firmware
- hardware
created_schema_version: 5
person_weeks: 1
---
## Problem
`reset()` backs up one valve-width and declares home, so from valve 5 it lies by about eighty
seconds; dead reckoning drifts and the wrong pot gets watered.

## Appetite
One person-week.

## Solution
First evening: is there a hard stop? Then full-travel homing or a microswitch on a spare pin, and a
fifty-cycle endurance loop. If it still mis-indexes, the bet converts into a cad pitch.

## Rabbit holes
- Redesigning the mechanism instead of indexing it.

## No-gos
No stepper or positional-servo conversion, no rotor redesign, no parallel watering.

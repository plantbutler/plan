---
id: pitch-cd0f19
kind: pitch
title: Pump on command
parent: proj-226479
status: shaping
priority: high
depends_on: [pitch-d338ac, pitch-1b1e91, pitch-9f9267]
tags:
- firmware
created_schema_version: 5
person_weeks: 1
---
## Problem
The pump has never been driven from software. "Water valve V for S seconds" must become home, move,
pump on, pump off under hard caps — and today's boot runs a three-minute manifold test.

## Appetite
One person-week.

## Solution
Execute the command from the hand-off: max seconds per dose, minimum gap, pump off on boot, and the
test-at-boot stripped. Blocking moves are accepted; every long delay becomes a watchdog-fed bounded
wait that checks the pump cap. Bucket only, user present.

## Rabbit holes
- The non-blocking rewrite. Not now.

## No-gos
No position feedback, no queue deeper than one, no schedule in firmware, no PWM.

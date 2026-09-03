---
id: pitch-cd0f19
kind: pitch
title: Bench sketch
parent: proj-226479
status: ready
owner: claude
assignees: [claude]
reviewers: [jcanton]
review_waived: false
priority: high
depends_on: [pitch-1b1e91, pitch-819142]
cycle: 1
tags:
- firmware
created_schema_version: 5
person_weeks: 1.5
---
## Problem
Nothing has ever pumped water under software control, and the bench cannot be brought up at all
without firmware to drive it: the wiring package's bring-up 0-7d assumes nine serial commands that
do not exist. Meanwhile the board still reads A0-A3 onto two screens and talks to a dead PHP page.
Splitting this across "Readings up the wire" and "Pump on command" would mean three passes over the
same files.

## Appetite
One and a half person-weeks — the two pitches it replaces, plus the safety work that the missing
hardware interlock forces into firmware.

## Solution
One sketch: the nine bring-up commands over serial, five raw channels posted once a minute with one
bounded water command executed and acked, both screens kept, and the three measures that stand in
for the interlock DECISIONS #10 removed — watchdog, a hard cap in the same code path that asserts
the pump pin, and a no-flow abort. A float that says full while the meter sees nothing latches
watering off until a human clears it; refusing means refusing to water, never stopping the
readings. Host-side tests for the logic and a fake-hardware mode so the commands can be exercised
off the rig. Spec: `firmware/docs/superpowers/specs/2026-09-03-bench-sketch-design.md`.

## Rabbit holes
- The non-blocking rewrite of the manifold. Bounded, watchdog-fed waits are enough.

## No-gos
No TLS, no JSON, no OTA, no offline buffering, no queue deeper than one, no schedule in firmware,
no PCB. `pos=unknown` is forced until the bench has passed bring-up 7d, so the backend's watering
rules stay dark.

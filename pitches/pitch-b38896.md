---
id: pitch-b38896
kind: pitch
title: Manifold in OpenSCAD with ball gates
parent: proj-4622e7
status: in_progress
owner: claude
assignees: [claude]
reviewers: [jcanton]
priority: high
depends_on: []
cycle: 2
start_date: 2026-09-02
tags:
- cad
- openscad
created_schema_version: 5
person_weeks: 1
---
## Problem
The manifold exists as a FreeCAD assembly (valveV2) whose parameters do not derive cleanly, and
its nail gates are being replaced by 8 mm balls on O-ring seats. A broken cart, cage or gear is
a restart without a source that can be edited and re-rendered.

## Appetite
One person-week.

## Solution
Rebuild all nine printed parts in OpenSCAD from the valveV2 geometry, fully parametric: the
internal height derives from the ball, the O-ring and the lift needed to pass the outlet bore
area; the gears sit outboard of the servo plate; the cart nut is captured. Every part prints on
the P2S flat on the bed without supports. Renders and sections checked, README with the numbers
to measure on the bench.

## Rabbit holes
- Redesigning the mechanism instead of re-sourcing it: the lead screw, cart, magnet and ball
  gate stay as decided.
- Hall-sensor and float mounts: separate pitch once the parts exist.

## No-gos
No FreeCAD edits, no stepper or positional-servo conversion, no solenoid alternative.

---
id: pitch-b38896
kind: pitch
title: Manifold and mounts in OpenSCAD
parent: proj-4622e7
status: shaping
priority: low
depends_on: [pitch-29bf77]
tags:
- cad
- openscad
created_schema_version: 5
person_weeks: 0.5
---
## Problem
The manifold exists only physically; a broken rotor is a restart, and the homing switch and the
float switch need mounts.

## Appetite
Half a person-week.

## Solution
Model the rotor, the body and the mounts in OpenSCAD, parametric only where a dimension is known
to change. If the part was printed from an STL you have, commit the STL and stop.

## Rabbit holes
- Redesigning the mechanism while "just modelling it".

## No-gos
No FreeCAD, no redesign until the homing pitch says the mechanism is the problem.

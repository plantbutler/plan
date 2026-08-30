---
id: pitch-357f85
kind: pitch
title: Sensor stakes and sealing
parent: proj-4622e7
status: shaping
priority: medium
depends_on: [pitch-24c5b3]
tags:
- cad
- hardware
created_schema_version: 5
person_weeks: 0.25
---
## Problem
Uncoated capacitive sensors corrode at the top edge and drift when they move in the pot; history
collected before they are fixed is worth less.

## Appetite
A quarter of a person-week.

## Solution
Seal the edges, print stakes that hold each sensor at a fixed depth, do it before the NAS starts
storing history that matters.

## Rabbit holes
- Per-soil or temperature compensation curves.

## No-gos
No new sensor type, no wireless nodes.

---
id: pitch-9f9267
kind: pitch
title: Bench rig
parent: proj-4622e7
status: shaping
priority: high
depends_on: [pitch-24c5b3]
tags:
- cad
- hardware
created_schema_version: 5
person_weeks: 0.5
---
## Problem
Nothing has ever pumped water under software control: no driver, no pump supply, no float switch,
no wiring diagram, no ml/s figure, and nobody knows whether the manifold seals or has a hard stop.

## Appetite
Half a person-week, once the parts have arrived and the bench is available.

## Solution
Pump, driver, own supply, a one-litre reservoir and a float switch on a bench, driven from a serial
command. Deliverables: ml/s per output, verdicts on seal, head, servo torque and hard stop, a KiCad
schematic and a BOM.

## Rabbit holes
- Precise dosing, or a custom PCB. Neither.

## No-gos
No PCB, no flow meter, no enclosure. The servo and pump never draw from the board's 5 V pin.

---
id: pitch-9f9267
kind: pitch
title: Bench rig
parent: proj-4622e7
status: shaping
priority: high
depends_on: [pitch-24c5b3, pitch-819142, pitch-cd0f19]
tags:
- cad
- hardware
created_schema_version: 5
person_weeks: 0.5
---
## Problem
Nothing has ever pumped water under software control, and the magnet-ball manifold hangs on four
unknowns: does the neodymium magnet lift the ball against pump pressure (~0.6 bar at dead head),
does the caged ball reseat and seal on its o-ring, does the hall count screw revolutions reliably
(gear torque is already proven on the printed reduction gears), and do the cheap capacitive
sensors drift or corrode when powered 24/7.

## Appetite
Half a person-week, once the bench is available.

## Solution
One manifold, five outlets: pump, relay, a one-litre reservoir, the inline flow meter and the hall
float sensor on a bench, driven from a serial command. Wiring, pin map and bring-up order are in
cad/wiring. Deliverables: ml/s per outlet, a verdict
on flow-meter accuracy (ml dosing, or fall back to seconds), verdicts on the four unknowns, a
KiCad schematic and a BOM.

## Rabbit holes
- Precise dosing, or a custom PCB. Neither.

## No-gos
No PCB, no enclosure. The pump never draws from a 5 V rail; the servo does, on the R4's buck, fed
from the barrel jack and with its bulk cap at the plug.

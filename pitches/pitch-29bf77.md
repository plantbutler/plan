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
The old driver dead-reckoned with delays and lied about home by eighty seconds. The real
mechanism is now decided: a continuous SG90 drives a lead screw through 3D-printed reduction gears,
the screw moves a cart carrying a neodymium magnet along the manifold, and the magnet lifts a caged
ball off an o-ring seat to open one outlet. Nothing measures where the cart is yet.

## Appetite
One person-week.

## Solution
A hall sensor counting screw revolutions plus a hall at the cart's home position, per manifold
(halls in hand: 8). Move-to-outlet-k = confirm home hall, then signed revolution count; refuse to
water while position is unknown. One manifold (5 outlets) first — M=3 comes only after this one
survives a fifty-cycle endurance loop.

## Rabbit holes
- Redesigning the mechanism instead of instrumenting it.
- Parking precision beyond "ball fully seated or fully lifted".

## No-gos
No stepper or positional-servo conversion, no second or third manifold yet, no parallel watering.

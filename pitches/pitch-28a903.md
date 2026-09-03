---
id: pitch-28a903
kind: pitch
title: Don't flood the flat
parent: proj-226479
status: shaping
priority: high
depends_on: [pitch-cd0f19]
tags:
- firmware
- safety
created_schema_version: 5
person_weeks: 0.5
---
## Problem
Automation is about to be switched on. A wedged MCU, an empty reservoir or a stale command can run
the pump dry or onto the floor, and nobody would know.

## Appetite
Half a person-week. Automation is gated on this.

## Solution
Float sensor as a hall switch: magnet on the tank float, hall outside; a stop caps the float's
travel at the trip level so magnet present means water above the line and every sensor failure
reads as refuse. The bench has it on a sense pin only; this pitch puts the hardware gate back
between the pump pin, the float and the relay's input, so a hung sketch cannot pump. Until then
the firmware carries it: watchdog, a hard run-time cap beside the line that asserts the pump pin,
refuse when cart position is unknown, and flow sanity from the inline flow meter — pump on with no
pulses within seconds cuts the pump and flags a fault, pulses with the pump off flag a leak;
status fields (float, outlet, uptime, last command result) in every report. Acceptance: the MCU
held in reset mid-dose, a hung sketch with the pump pin asserted, a stuck-on command, a hose
pulled off a pot — water stays in the tray.

## Rabbit holes
- Float and hall placement.

## No-gos
No leak sensors, no closable valves, no battery backup.

## For later
An MCU-independent run-time limiter; a tray leak sensor.

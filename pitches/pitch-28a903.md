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
Float switch both in the driver circuit and on a sense pin, watchdog, refuse when the manifold
position is unknown, and status fields (float, valve, uptime, last command result) in every report.
Acceptance: MCU held in reset with the driver pin high, a stuck-on command, a hose pulled off a
pot — water stays in the tray.

## Rabbit holes
- Float switch placement.

## No-gos
No leak sensors, no flow meter, no closable valves, no battery backup.

## For later
An MCU-independent run-time limiter; a tray leak sensor; a flow meter.

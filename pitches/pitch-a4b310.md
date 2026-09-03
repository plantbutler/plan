---
id: pitch-a4b310
kind: pitch
title: The watchdog that survives a stopped clock
parent: proj-226479
tags:
- firmware
- hardware
created_schema_version: 5
person_weeks: 0.25
status: shaping
priority: low
depends_on: [pitch-cd0f19]
---
## Problem
DECISIONS #10 and the wiring README both promise the IWDT, and the bench firmware ships the core's
register-start WDT instead — a different dog, on PCLKB rather than its own oscillator, dead in the
window between reset and `setup()`. On a bench with no hardware interlock the watchdog is the only
thing between a hung sketch and a running pump, so the gap between the word and the code matters.

## Appetite
A quarter of a person-week. Small, but it touches flash option bytes, so the recovery path is most
of the work.

## Solution
Write `.option_setting_ofs0` so the independent watchdog auto-starts from flash and covers a
stopped PCLKB and the reset-to-`setup()` window. First deliverable is a documented, tested DFU
recovery path, because a wrong option byte can lock the board out of USB uploads. Amend DECISIONS
#10 to say which watchdog is actually running.

## Rabbit holes
- Chasing a bricked board without having written the recovery down first.

## No-gos
Not part of the bench sketch. Nothing ships here until the DFU path has been proven on this board.

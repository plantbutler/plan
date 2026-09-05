---
id: pitch-d155fe
kind: pitch
title: Trust the tank
parent: proj-81a6d7
tags:
- backend
created_schema_version: 5
person_weeks: 0.5
status: in_progress
owner: claude
assignees: [claude]
reviewers: [jcanton]
priority: medium
depends_on: [pitch-cd0f19, pitch-43c9b2]
cycle: 1
start_date: 2026-09-05
---
## Problem
The float can fail in one direction the wiring cannot catch: the magnet comes off the float or
sticks to the hall's housing, and D5 reads "water above the line" forever, including on an empty
tank. The board cannot detect it — "the float never moved across a refill" needs to know a refill
happened, and the board has no way to know that.

## Appetite
Half a person-week.

## Solution
Three things the backend can do and the board cannot. Record refills as human events, so a float
that has not moved across ten refills is provably stuck rather than merely idle. Read the board's
`ch204` (seconds since D5 last changed, a stored channel rather than an ignored key) and raise when
a float has been frozen across refills and doses. And hold the durable half of the float/flow contradiction latch: when the board reports
that the float said full and the meter saw nothing, stop queuing commands until a human confirms,
because a board reset clears the firmware's own latch. Refusing means refusing to water; readings
keep arriving and keep being stored throughout.

Also here, because it is the same file and the same afternoon: a way to retire a controller, so an
id that posts once does not page the phone hourly forever.

Amended 2026-09-05, from the bench-sketch firmware's list (backend#24), four small things in the
same file: store the board's `err=` so a refusal is legible instead of surfacing as "reservoir
empty"; charge the daily cap for acked water only, so a lost response does not starve a pot for
the day (Jacopo's call); one dose ceiling — 250 ml, the board's own — refused at `/command` and at
pot save, because a pot above it is refused, acked and paged forever, never watered; and no
`pos:` page until a board has ever said `pos=ok`, so the flag that ships dark stays quiet.
Design: `backend/docs/superpowers/specs/2026-09-05-trust-the-tank-design.md`.

## Rabbit holes
- Guessing tank volume from flow totals. The refill is a human event; keep it one.

## No-gos
No firmware changes: the board's whole contribution is `ch204` (seconds since the float last
moved, a stored channel) and `ch207`/`err=contra` for the contradiction. The float going empty
does not latch: the rules already refuse on it, and a refill is the human event for that.

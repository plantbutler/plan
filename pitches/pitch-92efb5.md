---
id: pitch-92efb5
kind: pitch
title: Latches on the wire
parent: proj-81a6d7
status: done
owner: claude
assignees: [claude]
reviewers: [jcanton]
start_date: 2026-09-07
end_date: '2026-09-07'
priority: medium
depends_on: [pitch-890768]
cycle: 1
tags:
- firmware
- backend
- app
prs: [plantbutler/firmware#5, plantbutler/backend#30, plantbutler/app#20, 
    plantbutler/plantbutler#23]
created_schema_version: 5
person_weeks: 0.25
---
## Problem
The board has three latches and the wire carried one. The contradiction latch rides `ch207`; the flap (three consecutive float refusals, cleared only by a granted dose) and the dry latch (a reset with a dose in flight, cleared only by `dry off`) were folded into `float=0` and a sticky `err=` token. The backend could not tell a flap from an empty tank, so its page told the person to water from the phone; and it latched a reset board on `err=resetmid` changing, which it never does again until a dose ends, so a second reset never latched and the rules queued water the board refused, forever.

## Appetite
Half a day, before bring-up: no board runs this firmware yet, so the wire changes for free.

## Solution
`ch210` = flap, `ch211` = dry, in every report beside `ch207`. The backend latches on levels (reason `dry`, step `dry off`), keeps the `resetmid` edge beside them so `dry off` typed before the first report cannot hide a reset, tells the flap apart on the page, and lets a tap after the flap buy one dose: the board's own float check runs at dose time and either clears the flap or refuses again. The app says `float check tripped` and gives the dry latch its words.
Design: `backend/docs/superpowers/specs/2026-09-07-latches-on-the-wire-design.md`.

## Rabbit holes
- Ignoring the refusal's own cooldown for the tap's try was the trap the review found: without it the try waited six hours while the dead page fired first.

## No-gos
No change to the tank's counter or samples. No new UI beyond the words.

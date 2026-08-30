---
id: pitch-1b1e91
kind: pitch
title: Command hand-off
parent: proj-a0ce3a
status: ready
owner: claude
assignees: [claude]
reviewers: [jcanton]
review_waived: false
priority: medium
depends_on: [pitch-e982b9]
cycle: 1
tags:
- backend
created_schema_version: 5
person_weeks: 0.5
---
## Problem
The app has no way to ask for water and the board no way to learn it should. Heartbeat and
last-seen do not exist.

## Appetite
Half a person-week. The stretch bet of cycle 1: software only, first to cut.

## Solution
A one-shot, expiring "water valve V for S seconds" (or "stop") queued in the backend, handed to the
board in the response to its next report, acknowledged by the report after that. The response also
carries the next report interval. A fake-device script makes the backend testable without hardware.

## Rabbit holes
- Delivery semantics. It is not a job system: one slot, one command, it expires.

## No-gos
No scheduler, no rules, no queue deeper than one, no command types beyond water and stop.

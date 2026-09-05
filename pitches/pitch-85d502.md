---
id: pitch-85d502
kind: pitch
title: I refilled the tank
parent: proj-8fb1fc
tags:
- app
created_schema_version: 5
person_weeks: 0.25
status: in_progress
owner: claude
assignees: [claude]
reviewers: [jcanton]
priority: medium
depends_on: [pitch-d155fe]
cycle: 1
start_date: 2026-09-05
---
## Problem
Two things the butler needs from a human have nowhere to be said: that the tank was refilled, and
that a stopped system may resume.

## Appetite
A quarter of a person-week.

## Solution
A refill button on the garden screen that posts the event, and a confirmation card for a latched
system that shows why it stopped — float said full, meter saw nothing — and resumes only on a
deliberate tap. Both are one call each against the backend.

## Rabbit holes
- A refill wizard. It is a button.

## No-gos
No tank-level display, no volume entry, no history screen for refills.

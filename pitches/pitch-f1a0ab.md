---
id: pitch-f1a0ab
kind: pitch
title: Manage the garden
parent: proj-8fb1fc
status: in_progress
owner: claude
assignees: [claude]
reviewers: [jcanton]
priority: medium
depends_on: [pitch-7ca138, pitch-e402ec]
cycle: 2
start_date: 2026-09-02
prs: ['plantbutler/backend#6', 'plantbutler/app#2']
tags:
- app
created_schema_version: 5
person_weeks: 1
---
## Problem
Names, thresholds, the channel-valve-plant mapping, recalibration and controller health are still
curl edits.

## Appetite
One person-week.

## Solution
One list, one detail, one wizard: edit a pot and its plant, set thresholds, remap channels and
outlets, capture calibration hardware-in-the-loop (sensor in air, tap; in water, tap) using the
next-interval knob; approve a learning-mode proposal and verdict the dose; flip a pot
manual → learning → auto.

## Rabbit holes
- Forms and state management ballooning into an architecture exercise.

## No-gos
No multi-user, no photos, no widgets, no offline editing, no Play Store.

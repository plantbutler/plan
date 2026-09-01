---
id: pitch-553c1b
kind: pitch
title: Pots, plants and calibration
parent: proj-81a6d7
status: in_progress
owner: claude
assignees: [claude]
reviewers: [jcanton]
priority: medium
depends_on: [pitch-e982b9]
cycle: 2
start_date: 2026-09-01
tags:
- backend
created_schema_version: 5
person_weeks: 0.5
---
## Problem
Readings are raw counts keyed by controller and channel; there is no notion of outlet, pot, plant,
or what "dry" means for each sensor.

## Appetite
Half a person-week.

## Solution
Channel → outlet → pot → plant mapping in the backend, so repotting or swapping a hose is an edit.
Two calibration numbers per channel, overwritten on recalibration; % computed at read time and
never stored, so recalibrating reinterprets history instead of losing it. Until the app exists,
edits are a seed file or curl.

## Rabbit holes
- Drift compensation.

## No-gos
No species database, no photos, no settings history, no rewriting of stored raw readings.

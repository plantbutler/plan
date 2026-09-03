---
id: proj-3a84fc
kind: project
title: App, second pass
parent: prod-d37da8
tags:
- app
created_schema_version: 5
---
## Problem
The v1 app shipped and its own `AGENTS.md` lists what it knowingly left out: a pot cannot be
renamed, the watering history sits in the backend unread, the chart shows one hard-coded day with
no way to look further back, opening the app off the tailnet shows nothing at all, and the
calibration wizard captures a single sample. None of these need hardware.

## Appetite
Five small pitches, a fraction of a person-week each, taken in order.

## Solution
Give a pot a stable identity first, because everything else keys on it; then the watering history
screen, longer chart windows, a last-known cache so the app is not blank off-tailnet, and a median
capture in the wizard.

## No-gos
Still no Play Store, no login, no widgets, no photos, no theming. This project deliberately
revisits "no offline mode" from **Phone in the loop**: a read-only cache of the last good fetch is
not offline editing.

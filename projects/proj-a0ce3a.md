---
id: proj-a0ce3a
kind: project
title: NAS stores and queues
parent: prod-2e840d
tags:
- backend
created_schema_version: 5
---
## Problem
Nothing on the NAS receives a reading, and the app has no way to ask for water.

## Appetite
Cycle 1, alongside the firmware slice.

## Solution
A container that stores raw readings, then a one-shot command hand-off riding on the board's
report/response round trip.

## No-gos
No rules, no schedules, no auth beyond one static token, no TLS, no bought dashboards.

---
id: proj-81a6d7
kind: project
title: The butler decides
parent: prod-2e840d
tags:
- backend
created_schema_version: 5
---
## Problem
Every watering is a manual command; nothing knows which channel is which plant or what "dry" means
for each sensor, and fail-dry unattended is fail-silent.

## Appetite
Cycles 3-4, once a curl command waters a pot on the bench.

## Solution
Pots, plants and calibration in the backend; rules that water; alerts when it goes wrong.

## No-gos
No weather, no ML, no species database, no notification history.

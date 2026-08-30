---
id: pitch-24c5b3
kind: pitch
title: Org, repos, decisions, shopping list
parent: proj-73f0f3
status: ready
owner: jcanton
assignees: [jcanton]
reviewers: [claude]
review_waived: false
priority: high
cycle: 1
tags:
- umbrella
- chore
created_schema_version: 5
person_weeks: 0.25
---
## Problem
Code lives in `jcanton/plant_butler`, the architecture decisions live in a chat, and the parts the
bench needs in cycles 2-3 are not on order.

## Appetite
A quarter of a person-week: it is a chore, not a bet.

## Solution
GitHub org `plantbutler` (`plant-butler` was taken); transfer `plant_butler` as-is to become `firmware` (its history is
clean — `secrets.h` was never committed); README-only `app`, `cad`, `backend`; the umbrella pins
all five — firmware, backend, app, cad, this plan — as submodules and holds DECISIONS.md. Revoke the Gmail app password in
`../arduino`, which is never pushed. Pin the PlatformIO platform version. Order pump, driver,
supply, float switch and sealed sensors.

## Rabbit holes
- CI, badges, templates and README polish. None of it now.

## No-gos
No CI, no history rewrite, no code in the new repos.

---
id: pitch-24c5b3
kind: pitch
title: Org, repos, decisions, shopping list
parent: proj-73f0f3
status: in_progress
start_date: 2026-08-30
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
Code lived in `jcanton/plant_butler`, the architecture decisions lived in a chat, and the parts the
bench needs in cycles 2-3 are not on order.

## Appetite
A quarter of a person-week: it is a chore, not a bet.

## Solution
GitHub org `plantbutler` (`plant-butler` was taken); `plant_butler` transferred as-is to become
`firmware` (its history is clean — `secrets.h` was never committed); README-only `app`, `cad`,
`backend`; the umbrella pins all five — firmware, backend, app, cad, this plan — as submodules and
holds DECISIONS.md; an `AGENTS.md` in every repo. Revoke the Gmail app password in `../arduino`,
which is never pushed. Pin the PlatformIO platform version. Order pump, driver, supply, float
switch and sealed sensors.

## Progress
- [x] org `plantbutler`, the five repos, `.github` profile — 2026-08-30
- [x] `jcanton/plant_butler` → `plantbutler/firmware`, umbrella submodules — 2026-08-30
- [x] DECISIONS.md, AGENTS.md everywhere — 2026-08-30
- [x] Gmail app password revoked and deleted from the sketch — 2026-08-30
- [ ] pin the PlatformIO platform version (`platform = renesas-ra@1.6.0`, the installed one)
- [ ] order pump, driver, supply, float switch, sealed sensors

## Rabbit holes
- CI, badges, templates and README polish. None of it now.

## No-gos
No CI, no history rewrite, no code in the new repos.

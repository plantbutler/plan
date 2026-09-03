---
id: pitch-a1f82d
kind: pitch
title: What does this plant want?
parent: proj-6de564
status: shaping
owner: claude
assignees: [claude]
reviewers: [jcanton]
priority: medium
depends_on: [pitch-f82abf]
tags:
- backend
- app
created_schema_version: 5
person_weeks: 1.5
---
## Problem
Every care number in the pots table is a guess, and the system cannot say that the same plant wants
less water in December than in June.

## Appetite
One and a half person-weeks. Most of it is the honest mapping from care advice onto our sensor
scale, not the HTTP call.

## Solution
On adding a plant, normalise the species name through a taxonomy service, then query the
highest-ranked care API that is currently answering, cache the answer on the NAS forever with its
source and fetch date, and fall back to typing the numbers in when every source fails. A local table
maps watering regime, soil and pot size onto a target band. Season and the environment channels then
raise recommendations the app asks you to approve.

## Rabbit holes
- **Blocked on a key.** The 2026-09-03 re-probe (see the note) found Perenual and Trefle both
  alive and both requiring one, and keys never enter a repository. Nothing can call a care source
  until Jacopo has signed up. The taxonomy hop, the cache, the mapping and the type-it-in fallback
  do not need one and can be built first.
- Our percentage is a two-point calibration between air and tap water, not volumetric water content.
  Any code that treats a published percentage as ours is wrong; care sources give regimes, and the
  numbers stay local.
- A recommendation with no dismissed state re-proposes itself every hour. The alerts table's
  re-raise throttling is the precedent to copy.
- A mistyped species name mints a junk cache row unless the taxonomy hop runs first.

## No-gos
No scrapers. No mixing or averaging sources: one source wins per plant. No automatic change to a
watering number without a human approving it. No ML, no weather, no photos.

## For later
Fitting the dose against the verdict log — the adaptive dosing the "Plant care data, Planta-style"
note has been waiting for a season of readings to make possible.

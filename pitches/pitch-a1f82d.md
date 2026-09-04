---
id: pitch-a1f82d
kind: pitch
title: What does this plant want?
parent: proj-6de564
status: in_progress
start_date: 2026-09-04
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
On adding a plant, normalise the species name through GBIF, then ask Trefle — the only online
source, decided 2026-09-04 after both were probed with real keys — and cache the answer on the NAS
forever with its fetch date. If Trefle is offline or has nothing for that species, the numbers are
typed in. No ranking, no second source to fall back to, nothing to reconcile.

GBIF knows scientific names and nothing else, so a name it cannot place goes to Trefle's own
search, which matches common names, survives a typo, and answers with the species' photograph.
That picture is how somebody confirms they found their plant: "peace lily" is two species and no
spelling settles which one is on the windowsill.

Trefle carries no watering regime at all (`soil_humidity` was empty for every species sampled), so
the target band does not come from it and never did: a local table over soil, pot size and plant
type proposes one, and the user adjusts it. What Trefle usefully adds is light and atmospheric
humidity on 0-10 scales, which is context for the sunlight-hours ambition rather than a watering
number. Season and the environment channels then raise recommendations the app asks you to
approve.

## Rabbit holes
- The Trefle token is a secret: `deploy.env` beside the butler's own, never a repository. With no
  token configured the lookup is simply unavailable and every pot is typed in, which has to be a
  working path rather than an error.
- Trefle's houseplant coverage is empty, not thin — Monstera, Dracaena, Spathiphyllum and
  Chlorophytum all resolve and carry nothing; Ficus lyrata is absent. A pot that finds nothing is
  the normal case, not the sad one, and the screen has to read that way.
- Our percentage is a two-point calibration between air and tap water, not volumetric water content.
  Any code that treats a published percentage as ours is wrong; care sources give regimes, and the
  numbers stay local.
- A recommendation with no dismissed state re-proposes itself every hour. The alerts table's
  re-raise throttling is the precedent to copy.
- A mistyped species name mints a junk cache row unless the taxonomy hop runs first.

## No-gos
No scrapers. No Perenual, and no ranking or fallback chain: Trefle or the user's own typing. No
automatic change to a watering number without a human approving it. No ML, no weather. No
photographs of your own plants — that is its own pitch; the care source's picture of the species
is shown, because a search by common name is confirmed by eye.

## For later
Fitting the dose against the verdict log — the adaptive dosing the "Plant care data, Planta-style"
note has been waiting for a season of readings to make possible.

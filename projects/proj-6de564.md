---
id: proj-6de564
kind: project
title: The butler knows the plant
parent: prod-2e840d
tags:
- backend
created_schema_version: 5
---
## Problem
Every care number in the pots table — the target band, the dose, the cooldown — is typed in from
guesswork. Nothing in the system knows what is actually potted, so nothing can tell you that a
basil in December wants less water than the same basil in June.

## Appetite
One cycle, after pot identity lands. The lookup is the small part; the honest mapping from care
advice to our own sensor scale is the work.

## Solution
A `species` field per pot, separate from its nickname. On adding a plant, one on-demand lookup
against the highest-ranked care API that is currently answering, normalised through a taxonomy
service first and cached on the NAS forever, with manual entry as the fallback when every source
fails. Care sources speak in regimes, not percentages, so a local table maps regime, soil and pot
size onto a target band. Season and the environment channels produce **recommendations the app asks
you to approve**, never a silent change to how much water a pot gets.

## No-gos
No scrapers — APIs with terms that permit caching only. No mixing or averaging sources: one source
wins per plant and is recorded with its fetch date. No automatic change to a watering number
without a human approving it. No photos, no ML, no weather.

This project overturns the "no species database" no-go in **The butler decides**; the reasoning
lives in the note "Plant care data, Planta-style".

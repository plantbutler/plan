---
id: note-8ff0a5
kind: note
title: Plant care data, Planta-style
status: thinking
created_schema_version: 5
written_on: '2026-08-31'
---
Inspiration: <https://getplanta.com>. Each pot carries pot size, soil type, plant type, plant
size and an ideal soil-moisture range — descriptive columns in the pots table, edited from
"Manage the garden".

Beyond soil moisture, measure air temperature and sunlight duration (the sensor kit has both a
temperature/humidity and a light module; they ride the same report as extra channels, raw as
ever) and derive season from the date. The ambition: adapt the water QUANTITY per dose from
moisture range, temperature, light and season — what Planta actually sells.

That collides with "Rules that water" no-gos (no weather, no per-species profiles) on purpose:
v1 waters on thresholds. Adaptive dosing needs a season of readings to tune against, and the
cycle-1 pipeline is what collects them — so let the data pile up and shape an "adaptive dosing"
pitch when there is something to fit. The descriptive fields cost nothing now and make the app
worth looking at.

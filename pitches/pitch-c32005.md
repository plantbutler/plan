---
id: pitch-c32005
kind: pitch
title: A plant can die
parent: proj-3a84fc
status: in_progress
owner: claude
assignees: [claude]
reviewers: [jcanton]
priority: medium
cycle: 1
start_date: 2026-09-04
tags:
- backend
- app
created_schema_version: 5
person_weeks: 1
---
## Problem
A plant can die, and the app has no way to say so. There is no delete anywhere — the only lever is
the `enabled` toggle, which turns the proposals off and leaves the pot wired: its `pot_mappings`
window stays open, so the hose it is not using still belongs to it. To reuse that outlet you must
type over the dead plant's row and inherit its name, its photographs and its watering log.

And the readings would follow the wire, not the plant. `readings` and `commands` carry only
`(controller, channel)` and `(controller, outlet)`, and `GET /history` asks for a channel, so a new
plant on a dead one's socket opens its chart onto somebody else's moisture curve. The dose history
already derives the pot from the mapping window; the chart never did.

Two smaller things landed in the same form. `soil` is still free text keyword-matched, the last
field where a typo is worth five points of band, and the plant kind is a set of six when the six do
not cover an orchid, a palm or a Venus flytrap.

## Appetite
One person-week across a backend PR and an app PR. The database is emptied on deploy rather than
migrated: it holds one test pot, and a rework of this size does not deserve a backfill written for
a single row nobody wants.

## Solution
`enabled` becomes `status`, a closed set that is `alive` or `graveyard` and has room for a third
word. Graveyard means no proposals, no doses, no alerts, and the mapping window closed — which is
what frees the channel and the outlet. Coming back is one tap and leaves the pot unwired, because
the plant that comes back is not in the socket the old one left.

Delete is separate and total: the pot, its wiring, its photographs and their files, its readings,
its doses and their verdicts. A confirmation names the plant and says what goes.

`readings` and `commands` gain `pot_id`, stamped as the row lands from the mapping window in force,
and the chart asks for a pot instead of a channel. A pot that never existed when a reading arrived
cannot claim it, and a socket reused after a death starts empty.

The plant kinds go from six to twelve, soil becomes seven values plus unset, and both are refused
on the wire when they are not in the set. Soil's keyword matcher — the word-start rule, the
negation rule, the phrase-shortening — is deleted rather than tightened: a closed set cannot be
misspelled.

## Rabbit holes
Stamping the pot at write time is a reversal of "attribution is derived at read time" (decisions 6
and 16), and it has a real cost: a mis-typed channel corrected later leaves its readings stamped
with the mistake. It is worth an entry in DECISIONS.md that says so rather than a comment.

Deleting readings and commands contradicts the schema's own "rows are never deleted". That rule
was written for pruning, not for a plant the owner asked to erase; the comment needs changing where
the code does.

## No-gos
No undo for delete. No migration of the existing database. No third status word invented now
because one might be wanted later. No free-text escape on soil or kind: a value that is not in the
list is a value that does not move the band, and adding one is a code change on purpose.

## For later
A paused-but-wired status, for a pot that is going away for a month rather than dying. Readings
that arrived while nothing was mapped are kept and orphaned; a screen that adopts them into a pot
would be its own pitch.

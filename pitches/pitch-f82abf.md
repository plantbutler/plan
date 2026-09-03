---
id: pitch-f82abf
kind: pitch
title: A pot has an identity
parent: proj-3a84fc
status: in_progress
owner: claude
assignees: [claude]
reviewers: [jcanton]
priority: high
cycle: 1
start_date: 2026-09-03
tags:
- backend
- app
created_schema_version: 5
person_weeks: 1
---
## Problem
A pot's name is its key on the wire, so renaming one means disabling it and creating another. Worse,
nothing else in the database knows a pot exists: readings key on (controller, channel) and commands
on (controller, outlet). History is therefore attributed by whatever the mapping happens to be right
now, so a mistyped channel misfiles a month of readings with no way to correct it.

## Appetite
One person-week across backend and app. It is the largest of the second-pass pitches and the
foundation the other four sit on, so the table is worth rebuilding properly rather than bolting a
second id beside the old one.

## Solution
Every pot gets a random id in the plan's own style (`pot-3f9a21`), stable for life, and the API keys
on it; the name becomes a mutable nickname. The physical wiring moves out of `pots` into its own
table with a validity window per row, so the current mapping is the open row and history is
attributed by joining on time — remapping reinterprets history instead of misfiling it, the same way
recalibration already reinterprets percentages. `species` arrives in the same rebuild, because the
table is open anyway.

## Rabbit holes
- SQLite cannot retype a primary key in place, so this is a one-time table rebuild, which
  `schema.sql`'s own header forbids. Take the exception deliberately, back the database up first,
  and write it into DECISIONS.md.
- `POST /pot` is a partial upsert by name that the app's form diffs a draft against. Moving the
  mapping out changes that contract on both sides at once.
- Deriving attribution at read time touches `/history`, `/pots` and the dose list. Getting the
  open-row join wrong shows up as a silently empty chart, not as an error.

## No-gos
No migrations framework. No mapping UI beyond what "Manage the garden" already has. No change to
what the board sends: raw counts keyed on (controller, channel) stay exactly as they are.

## For later
A pot's history across being repotted into a different vessel — the id survives, the pot does not —
is not modelled. If it ever matters it is a field on the mapping row.

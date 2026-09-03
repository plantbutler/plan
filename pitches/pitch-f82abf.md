---
id: pitch-f82abf
kind: pitch
title: A pot has an identity
parent: proj-3a84fc
status: done
owner: claude
assignees: [claude]
reviewers: [jcanton]
priority: high
cycle: 1
start_date: 2026-09-03
end_date: '2026-09-03'
prs: ['plantbutler/backend#8', 'plantbutler/backend#9', 'plantbutler/plantbutler#1', 'plantbutler/app#4']
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

## Progress
Done 2026-09-03. Backend plantbutler/backend#8 and #9, umbrella plantbutler/plantbutler#1
(decision 16), app plantbutler/app#4. Backend 0.8.0 is deployed on the NAS; the one-time rebuild
ran against a copy of the live database first and then for real, and left `butler.db.pre-identity.bak`
beside it.

Four rounds of adversarial review found eighteen defects a green suite did not, including two
wet-direction ones the branch introduced itself in the dose-attribution rework, and two ways the
nickname could still move on its own after the app was rekeyed. Two known limits ship with it: a
dose can escape both halves of the watering gate when attribution has failed and the pot has since
been remapped, and a `POST /pot` with no id and a name that already exists still upserts onto that
pot rather than refusing. The second is a wire-contract decision, not a bug, and is written up for
its own pitch if it ever matters.

Not done: the app has never been driven on the phone against the deployed backend — that needs the
adb port over the tailnet.

## For later
A pot's history across being repotted into a different vessel — the id survives, the pot does not —
is not modelled. If it ever matters it is a field on the mapping row.

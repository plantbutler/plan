---
id: pitch-02db12
kind: pitch
title: A create is not an edit
parent: proj-a0ce3a
status: ready
owner: claude
assignees: [claude]
reviewers: [jcanton]
priority: medium
cycle: 1
depends_on: [pitch-f82abf]
tags:
- backend
created_schema_version: 5
person_weeks: 0.25
---
## Problem
`POST /pot` with no `id=` looks the pot up by name, so a body meant to create one silently edits the
pot that already has that name. The app checks for the clash first, but only against the garden it
last fetched: a pot added from another phone, or while the list sat idle, slips past it. Since the
identity pitch the backend refuses a *rename* onto a taken name — it is only the create that still
overwrites, which makes the pair indefensible rather than merely lax.

## Appetite
A quarter person-week. The change itself is small; the cost is that name-keyed upsert is how the
backend's own tests write pots, so the churn is in the suite, not the code.

## Solution
An id-less `POST /pot` always creates. If the name is taken it is refused, in the same words the
rename already uses, and the caller is told to open that pot instead. Editing an existing pot needs
its id — which is what every caller has had since the identity pitch.

## Rabbit holes
- Roughly fifty posts in the backend suite edit a pot by name. They have to become id-keyed, and
  each one is a chance to assert the wrong thing while making it pass.
- The fake device and any script that seeds a database by name break the same way.

## No-gos
No general "upsert" flag to opt back in. No change to how the app builds a create — it already
sends no id.

## For later
Whether a create should also refuse a wiring that a *disabled* pot holds, rather than displacing it
as the mapping write now does.

---
id: pitch-3c33ab
kind: pitch
title: The watering history
parent: proj-3a84fc
status: ready
owner: claude
assignees: [claude]
reviewers: [jcanton]
priority: medium
depends_on: [pitch-f82abf]
cycle: 1
tags:
- app
- backend
created_schema_version: 5
person_weeks: 0.5
---
## Problem
The commands table has never been pruned and is the complete watering history. The app shows one row
of it: the last dose. Everything about whether the rules are behaving is in there, unread.

## Appetite
Half a person-week: one endpoint and one screen.

## Solution
A dose list, per pot and for the garden, each row carrying what was asked, what the flow meter
counted, the state it ended in and its verdict — attributed through the pot's mapping so a remapping
does not relabel the past. Reachable from the pot screen.

## Rabbit holes
- The interesting row is the one that expired, was never acked, or flowed short. It has to read
  differently from a clean dose rather than being filtered out of the list.

## No-gos
No editing history, no export, no charts of it in this pitch.

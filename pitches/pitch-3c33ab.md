---
id: pitch-3c33ab
kind: pitch
title: The watering history
parent: proj-3a84fc
status: done
owner: claude
assignees: [claude]
reviewers: [jcanton]
priority: medium
depends_on: [pitch-f82abf]
cycle: 1
start_date: 2026-09-03
end_date: '2026-09-03'
prs: ['plantbutler/backend#10', 'plantbutler/backend#11', 'plantbutler/app#5']
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

## Progress
Done 2026-09-03. `GET /doses` on the backend (0.9.0, deployed), the history screen on the app,
reachable from the pot form and from the list.

Three adversarial reviews found four defects the green suites did not. The worst was not in the new
endpoint at all: disabling a pot never closed its mapping window, and the collision check only
looked at enabled pots, so a second pot on the same hose opened a window under the first. The same
dose then belonged to two pots — and answered a different owner depending on which query you asked.
Reproduced through the HTTP API alone. Fixed in the mapping write, where the untrue record was made,
not in the endpoint that exposed it; it had been quietly corrupting cooldown and daily-cap
attribution since the windows arrived.

Also fixed: stops were listed as unattributable doses, burying the rows that matter; the endpoint
promised a history it could not page past 200, so it grew a two-part cursor; and on the app, leaving
a pot form for its history mid-save stranded the form with its buttons greyed out for good — worse
over the wizard's arming POST, which could have left the board reporting every 5 s with no wizard
on screen.

Not done: no paging in the app (the cursor exists on the wire, no screen uses it), and nothing has
been driven on the phone — that needs the adb port over the tailnet.

## No-gos
No editing history, no export, no charts of it in this pitch.

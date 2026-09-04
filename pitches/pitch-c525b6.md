---
id: pitch-c525b6
kind: pitch
title: The controller is a number
parent: proj-3a84fc
status: done
owner: claude
assignees: [claude]
reviewers: [jcanton]
priority: medium
cycle: 1
start_date: 2026-09-05
end_date: '2026-09-05'
prs: ['plantbutler/backend#23', 'plantbutler/app#16', 'plantbutler/firmware#1']
tags:
- backend
- app
- firmware
created_schema_version: 5
person_weeks: 0.5
---
## Problem
`c=` was the last free-text identifier on the wire, and it was the one a typo could turn into a
whole second garden. A report from `bench1 `, or `Bench1`, opens its own row in `controllers`, its
own heartbeat, its own alerts — and nothing anywhere says the two are the same board. Every other
identifier the backend joins on is either a minted `pot-xxxxxx` or an integer; this one was
whatever the firmware's `secrets.h` happened to say, spelled again by hand in the app's form.

Separately: the garden list is a column of names. A plant is a thing you recognise by looking at
it, and the pot already keeps a strip of its own photographs.

## Appetite
Half a person-week, across three repositories at once, because the wire is shared and a board
sending a word to a backend expecting a number is a 400 on every report.

## Solution
The controller is an integer, 0..255, in every parser, every column and every model —
`MAX_CONTROLLER` in the backend, `PB_CONTROLLER` in the firmware, `Int` in the app. Reading stays
where it is: the alert keys still embed it as text, because a key is a string and always was.

Board 0 is the whole trap. It is falsy in Python and in Kotlin, and it is the number a new pot's
form fills in, so every `if not controller` refuses the commonest board there is. Four of those in
the backend, each with a test that fails without the fix.

`GET /pots` also carries `photo`, the id of each pot's newest picture, and the app draws it beside
the name. The id only: the bytes come from the same cached `GET /photo/<id>` the strip uses.

## Rabbit holes
The firmware is where this costs more than a rename. `sizeof(PB_CONTROLLER)` stopped meaning
"length of the identifier", two static_asserts had to change shape rather than value, and the
tests juxtaposed the macro against string literals at compile time. The one nothing would have
caught: `test_cli.cpp` built its fixture with a hardcoded `"bench1"`, independent of the macro, so
it would have gone on passing while asserting a shape that can no longer exist. That was found by
the session working on the bench sketch, not by the compiler and not by me.

## No-gos
No migration: the database was recreated, because `CREATE TABLE IF NOT EXISTS` cannot retype a
column and TEXT affinity would have stored the integer as `'0'` and answered the app a string it
refuses to decode. No placeholder thumbnail for a pot with no picture. No stat() of the photo file
in `/pots` — that is the strip's job, once, not the list's on every screen open.

## For later
More than one board. The column is wide enough and the app renders `boardName()` everywhere, but
nothing has been tried with two.

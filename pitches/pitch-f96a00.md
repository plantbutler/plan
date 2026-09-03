---
id: pitch-f96a00
kind: pitch
title: Look further back
parent: proj-3a84fc
status: done
owner: claude
assignees: [claude]
reviewers: [jcanton]
priority: medium
cycle: 1
start_date: 2026-09-03
end_date: '2026-09-03'
prs: ['plantbutler/backend#13', 'plantbutler/backend#14', 'plantbutler/app#7']
tags:
- app
created_schema_version: 5
person_weeks: 0.25
---
## Problem
`/history` already takes an hours window and a bucket size. The app asks for one day, offers no way
to change it, and the curve cannot be read at a point.

## Appetite
A quarter person-week, app only. The wire does not change.

## Solution
Day, week and month windows on the pot's chart, with the bucket size chosen to keep the point count
sane, and a scrub that reads out the value and the time under the finger.

## Rabbit holes
- The pen-lift rule for gaps is written against a day's buckets. Over a month of hourly buckets the
  gap threshold has to scale with the bucket, or an outage disappears into one unbroken line.

## Progress
Done 2026-09-03. Day, week and month chips on the pot chart, a scrub that reads out the sample
under the finger, and — added at Jacopo's request, not in the original shaping — "Load older" on
the watering history.

This pitch was wrong about itself: "the wire does not change" was not true, because `/history`
capped `hours` at 168 and the month window it asks for was unreachable. Backend 0.11.0 raised the
cap to 744, leaving the bucket cap as the bound that actually bites.

The rabbit hole it names was already handled — `chartGapS` is max(2 buckets, the silence
threshold), so an outage still breaks the line at hourly buckets. There is now a test per window
saying so rather than leaving it to be rediscovered.

Review found the pager racing pull-to-refresh in a way that could drop a row of history for good;
the two now share one flight. A generation counter written alongside that fix was removed once
mutation testing showed it unreachable.

## No-gos
No zoom gestures, no panning, no second series on the same axes.

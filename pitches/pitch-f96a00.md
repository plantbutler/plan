---
id: pitch-f96a00
kind: pitch
title: Look further back
parent: proj-3a84fc
status: ready
owner: claude
assignees: [claude]
reviewers: [jcanton]
priority: medium
cycle: 1
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

## No-gos
No zoom gestures, no panning, no second series on the same axes.

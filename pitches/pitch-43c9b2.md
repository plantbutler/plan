---
id: pitch-43c9b2
kind: pitch
title: Tell me when it's wrong
parent: proj-81a6d7
status: in_progress
owner: claude
assignees: [claude]
reviewers: [jcanton]
priority: medium
depends_on: [pitch-e402ec]
cycle: 2
start_date: 2026-09-01
prs: ['plantbutler/backend#5']
tags:
- backend
created_schema_version: 5
person_weeks: 0.5
---
## Problem
Fail-dry unattended is fail-silent: nobody learns the controller went quiet, the reservoir is
empty, or a dose did not raise moisture.

## Appetite
Half a person-week.

## Solution
Three or four rules posting to a public ntfy.sh topic, which is push to the phone for free and
works off the LAN, plus a dead-man ping for the butler container itself.

## Rabbit holes
- Building push into the app (FCM, tokens, a service).

## No-gos
No FCM, no email, no notification history, no per-plant tuning.

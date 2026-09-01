---
id: pitch-7ca138
kind: pitch
title: Hello, pots
parent: proj-8fb1fc
status: in_progress
owner: claude
assignees: [claude]
reviewers: [jcanton]
priority: medium
depends_on: [pitch-553c1b]
cycle: 2
start_date: 2026-09-01
tags:
- app
created_schema_version: 5
person_weeks: 1
---
## Problem
No Android toolchain exists on the machine and no app; the first bet must end with something on the
phone.

## Appetite
One person-week, most of it toolchain.

## Solution
Android Studio, JDK and device setup; Hello World on the phone; then one list of pots with % and
last-seen, read from the backend over the LAN with cleartext explicitly allowed. URL and token from
an untracked local file.

## Rabbit holes
- Architecture ceremony: DI, MVI, offline cache. None of it.

## No-gos
No offline, no login, no Play Store, no theming, no charts.

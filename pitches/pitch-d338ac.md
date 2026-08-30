---
id: pitch-d338ac
kind: pitch
title: Readings up the wire
parent: proj-226479
status: ready
owner: jcanton
assignees: [jcanton, claude]
reviewers: [claude]
review_waived: false
priority: high
depends_on: [pitch-24c5b3]
cycle: 1
tags:
- firmware
created_schema_version: 5
person_weeks: 0.75
---
## Problem
A0-A3 raw counts reach two screens and nothing else. The WiFiS3 path is eighteen months unproven
and the old Network lib spins forever on a lost connection.

## Appetite
Three quarters of a person-week. It carries the biggest firmware unknown: does the idle board
still talk.

## Solution
Drop both screens (A4 becomes channel 5), pick 14-bit once, post five raw channels once a minute
as `k=v` lines over plain HTTP to a stub on the laptop, then to the NAS. Reconnect on drop, retry
once, discard the reading. Done when the board survives a WiFi drop, a router reboot and 48 hours
unattended.

## Rabbit holes
- WiFiS3 reconnect and the ESP32-S3 firmware updater: one-evening timebox.

## No-gos
No TLS, no JSON, no OTA, no offline buffering, no commands, no manifold changes.

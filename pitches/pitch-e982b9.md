---
id: pitch-e982b9
kind: pitch
title: Readings land on the NAS
parent: proj-a0ce3a
status: ready
owner: claude
assignees: [claude]
reviewers: [jcanton]
review_waived: false
priority: high
depends_on: [pitch-24c5b3]
cycle: 1
tags:
- backend
- nas
created_schema_version: 5
person_weeks: 0.75
---
## Problem
Nothing on the NAS receives a reading; deploying a container to the Synology is an unproven path
and the first row has nowhere to land.

## Appetite
Three quarters of a person-week; the unknown is the Synology, not the code.

## Solution
One Python container with SQLite on a bind-mounted volume. One endpoint takes a report of raw
counts keyed by controller and channel, stamps the arrival time, stores it. Done when `curl` from
the LAN returns 200 and the row is in the database; Hyper Backup covers the volume.

## Rabbit holes
- Container Manager friction: image architecture, volume permissions, the port. Build on the
  laptop, ship the image.

## No-gos
No Postgres, no migrations framework, no auth beyond one static token, no TLS, no reverse proxy, no
Grafana. One report a minute, raw kept forever.

---
id: pitch-f9cff1
kind: pitch
title: Where is the butler?
parent: proj-3a84fc
status: shaping
owner: claude
assignees: [claude]
reviewers: [jcanton]
priority: medium
tags:
- app
created_schema_version: 5
person_weeks: 0.5
---
## Problem
The server address and the token are compiled into the APK from `butler.properties`. A second phone
therefore needs a rebuild, a moved NAS needs a new build, and every artifact ever produced carries
the token inside it. None of that is how an app is installed.

## Appetite
Half a person-week. The screen is small; the care is in where the token rests and what happens to
everything that assumed the address could not change.

## Solution
First start asks. One setup screen takes the address and the token, proves them with a real call
before it accepts them, and keeps them on the device; every later start goes straight to the
garden. Settings can change them afterwards. The build-time properties stay as the default for
development builds — no longer the only source.

## Rabbit holes
- The token is a secret at rest on a phone: the encrypted store, not plain preferences, and never
  in a log line or a crash report.
- The offline cache belongs to one backend. Point the app somewhere else and the cache has to go,
  or the new server shows the old server's plants.
- "Wrong address" and "wrong token" are different failures and the user can fix only one of them.
  Telling them apart, in words, is most of the value here.
- The laptop backend is plain HTTP on a LAN address. Cleartext has to keep working, so the field
  cannot insist on https.
- The address stops being a build constant, so whatever constructs the backend client can no longer
  do it once, at start-up, from a default argument.

## No-gos
No accounts. No discovery scan of the network. No holding several servers at once. No change to the
single static token the backend already has.

## For later
A QR code the NAS can show, carrying address and token, so setting up the next phone is a scan.

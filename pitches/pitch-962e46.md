---
id: pitch-962e46
kind: pitch
title: A picture of the plant, over time
parent: proj-6de564
status: shaping
owner: claude
assignees: [claude]
reviewers: [jcanton]
priority: medium
depends_on: [pitch-a1f82d]
tags:
- app
- backend
created_schema_version: 5
person_weeks: 1
---
## Problem
The app knows a plant as a number and a name. Whether a month of watering actually did it any good
is a question a photograph answers and a moisture chart does not, and there is nowhere to put one.

## Appetite
One person-week. Most of it is the upload path and where the bytes live, not the camera.

## Solution
Photos hang off the pot id the way readings do. The backend takes an upload, keeps the file on the
bind-mounted volume with a row pointing at it, and serves it back behind the same token. The pot
screen gets a strip in date order, a camera button, and a full-size view on tap — so the pot carries
its own growth history. Trefle's picture for the species, when it has one, sits beside them as the
reference: what this plant is supposed to look like.

## Rabbit holes
- Photos are the first thing in this system that is not small. A phone photo is several megabytes
  and the NAS volume and its backup were never sized for hundreds of them; downscale on the phone
  and cap the long edge before anything is uploaded.
- Bytes on the volume, rows in SQLite. A row whose file is gone, and a file no row knows about, are
  both reachable — the delete path and the backup story have to say which one is the truth.
- Tailnet only, like everything else: served through the existing token, no public URL, nothing
  port-forwarded.
- A pot outlives its plant. Replant it and the strip becomes two plants in one history unless
  something marks the break.
- Trefle's image is per species, licensed, and as absent for houseplants as the rest of its data.
  It is a reference, never a stand-in for the user's own picture.

## No-gos
No editing, cropping or filters. No cloud storage and no sharing off the tailnet. No ML on the
pictures. No time-lapse video — a strip is a strip.

## For later
A time-lapse from the strip, and pinning one photo per pot as its face in the garden list.

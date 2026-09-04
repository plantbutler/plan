---
id: pitch-962e46
kind: pitch
title: A picture of the plant, over time
parent: proj-6de564
status: done
start_date: 2026-09-04
end_date: '2026-09-04'
prs: ['plantbutler/backend#19', 'plantbutler/backend#20', 'plantbutler/app#13']
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

## Progress
Done 2026-09-04, backend 0.14.0 on the NAS and driven on the phone.
Backend 0.14.0 keeps the bytes under `BUTLER_PHOTOS` beside the database, one directory per pot,
with the row as the truth: a picture is listed, served and deleted by its row and the directory is
never read to decide what exists. That settles the rabbit hole about files and rows coming apart in
opposite directions — a file no row knows about is invisible and harmless, and a row whose file has
gone is reported as missing rather than served as a broken image. Keeping writes the file then the
row; deleting removes the row then the file.

The app caps the long edge at 1600 before anything is uploaded, which is the difference between a
decade of weekly pictures being a couple of hundred megabytes and a couple of dozen gigabytes. The
break where one plant ended and the next began is drawn from the species each picture was taken
under, which the backend stamps on the row — no replant event was invented, and the strip is honest
that basil replanted with basil leaves no trace.

One thing found while building: a phone writes the sensor's orientation into EXIF rather than into
the pixels, and re-encoding drops the tag. Without turning the picture first, every portrait
photograph would have come back on its side for good — and the pitch's own no-go says there is no
editing here to fix it with. Confirmed with the camera: a picture taken in portrait came back
1200x1600 and upright, 306 KB, right in the band the 1600-pixel cap was chosen for.

The break drew itself correctly too, including the case it is meant to keep quiet about. A
photograph taken before the pot had a species opens no break — "nobody said" is not "a different
plant" — and the marker appeared only where the species actually changed. Deleting a picture took
the row, the file and the marker with it.

## For later
A time-lapse from the strip, and pinning one photo per pot as its face in the garden list.

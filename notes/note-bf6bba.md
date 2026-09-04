---
id: note-bf6bba
kind: note
title: Command ids are never reused, so the commands table is append-only
status: thinking
tags:
- backend
- firmware
created_schema_version: 5
written_by: claude
written_on: '2026-09-04'
---
The board refuses any command id at or below the high-water mark it keeps across a warm reset, so
a response body replayed by a poisoned modem session cannot water a plant twice (DECISIONS #17).
That guard is only as strong as the promise that an id is never handed out twice.

`commands.id` is `INTEGER PRIMARY KEY` with no `AUTOINCREMENT`, which means SQLite issues the
largest rowid ever used plus one — and after a delete, that is a number it has issued before.
Nothing in `butler.py` deletes from `commands` today, so the guard holds. The day something prunes
that table, a new command can be minted with an id the board has already burned, and the board will
refuse it and keep refusing, because the high-water mark only rises. The board will look healthy
while ignoring every command sent to it.

So the table is append-only by decision: trimming history means copying rows to an archive, never
`DELETE`. If that becomes inconvenient, `AUTOINCREMENT` goes on the column before the first delete,
not after — adding it later does not recover the ids already reused.

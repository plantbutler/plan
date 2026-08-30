---
id: prod-9178ff
kind: product
title: firmware
tags:
- firmware
- arduino
created_schema_version: 5
---
Today's `jcanton/plant_butler`, moved to the org as-is. PlatformIO, Arduino UNO R4 WiFi: reads the
raw sensor channels and the float switch, reports them, executes one bounded water command at a time
and enforces the safety invariants that must hold even when the backend is wrong.

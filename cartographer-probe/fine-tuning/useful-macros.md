---
description: >-
  This page features some community suggested useful macros that work well with
  the Cartographer probe.
---

# Useful Macros

### Smart Quad Gantry Level

If your gantry has a tendancy to sag after a power cyclle, it is advisable to use a Macro like this to replace your standard Quad Gantry Level Macro. \
\
This will do a single round where it adjusts the gantry to make it reasonably level, before then performing a more optimum QGL.&#x20;

```gcode
[gcode_macro Carto_QGL] # safer and faster QGL for Cartographer
gcode:
    G28 # or use a conditional or safe homing
    QUAD_GANTRY_LEVEL horizontal_move_z=10 retries=0 retry_tolerance=1.000
    QUAD_GANTRY_LEVEL horizontal_move_z=3
    G28 Z
```


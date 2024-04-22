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

### Bed mesh without Heater&#x20;

If you have problems with interference in your bed mesh scans, add this macro, it will turn off the heater while you're scanning.&#x20;

```gcode
[gcode_macro BED_MESH_CALIBRATE]
rename_existing: _BED_MESH_CALIBRATE
gcode:
    {% raw %}
{% set TARGET_TEMP = printer.heater_bed.target %}
{% endraw %}
    M140 S0
    _BED_MESH_CALIBRATE {rawparams}
    M140 S{TARGET_TEMP}
```

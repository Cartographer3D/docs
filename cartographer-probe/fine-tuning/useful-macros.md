---
description: >-
  This page features some community suggested useful macros that work well with
  the Cartographer probe.
---

# Useful Macros

### Bed mesh without Heater&#x20;

If you have problems with interference in your bed mesh scans, add this macro, it will turn off the heater while you're scanning.&#x20;

```gcode
[gcode_macro BED_MESH_CALIBRATE]
rename_existing: _BED_MESH_CALIBRATE
gcode:
    {% set TARGET_TEMP = printer.heater_bed.target %}
    M140 S0
    _BED_MESH_CALIBRATE {rawparams}
    M140 S{TARGET_TEMP}
```

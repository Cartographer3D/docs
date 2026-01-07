# PRINT\_START template

Here is a template print start. You will need to adjust it to fit your printer, but this will show where the `CARTOGRAPHER_TOUCH_HOME` belongs compared to the other usual bed levelling macros.

```gcode
[gcode_macro PRINT_START]
gcode:
  ("Check preconditions and get print temperatures") ; Replace with your real macro
  SET_GCODE_OFFSET Z=0 ; Reset Z offset
  G28 ; Home all axes
  G90 ; Set to absolute positioning
  
  M104 S150 ; Heat nozzle to soften filament leftovers
  ("Heat bed to print temperature, M190 S{target_bed}") ; Replace with your real macro
  
  ("QUAD_GANTRY_LEVEL or Z_TILT_ADJUST") ; Replace with your real macro
  M109 S150 ; Ensure nozzle is at 150C, in case it was hot when print started.
  CARTOGRAPHER_TOUCH_HOME ; Home for real Z0

  ("Do BED_MESH_CALIBRATE ADAPTIVE=1") ; Replace with your real macro

  ("Do the rest - heat to print temperature and prime") ; Replace with your real macro
```

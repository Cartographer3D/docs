---
description: Auto-generated from plugin source.
---

# Macro Reference

## PROBE

Probe the bed to get the height offset at the current position.

*This macro accepts no parameters.*

## PROBE_ACCURACY

Probe the bed multiple times to measure the accuracy of the probe.

```
  LIFT_SPEED (float, required): Lift speed in mm/s
    Constraints: minimum: 1
  SAMPLE_RETRACT_DIST (float, default: 1.0): Retract distance between samples
    Constraints: minimum: 1.0
  SAMPLES (int, default: 10): Number of probe samples
    Constraints: minimum: 3
```

## QUERY_PROBE

Return the status of the z-probe

*This macro accepts no parameters.*

## Z_OFFSET_APPLY_PROBE

Adjust the probe's z_offset

*This macro accepts no parameters.*

## BED_MESH_CALIBRATE

Gather samples across the bed to calibrate the bed mesh.

```
  METHOD (str, default: 'scan'): Calibration method
  MESH_MIN (str | None, default: None): Minimum mesh coordinate (x,y)
  MESH_MAX (str | None, default: None): Maximum mesh coordinate (x,y)
  PROBE_COUNT (str | None, default: None): Number of probe points (x,y)
  ADAPTIVE (int, default: 0): Enable adaptive meshing (0 or 1)
  ADAPTIVE_MARGIN (float, default: 0.0): Margin for adaptive mesh
    Constraints: minimum: 0
  PROFILE (str, default: 'default'): Mesh profile name
  DIRECTION (MeshDirection, default: 'x'): Primary scan direction
    Allowed values: x, y
  PATH (MeshPath, default: 'snake'): Scan path pattern
    Allowed values: snake, alternating_snake, spiral, random
  SPEED (float, default: 50.0): Scan speed
    Constraints: minimum: 50
  HEIGHT (float, default: 5.0): Scan height
    Constraints: minimum: 0.5, maximum: 5
  RUNS (int, default: 1): Number of scan passes
    Constraints: minimum: 1
```

## CARTOGRAPHER_QUERY

Query current cartographer state

```
  FIELD (QueryField, default: 'all'): Field to query
    Allowed values: touch, scan, mcu, all
```

## CARTOGRAPHER_STREAM

Controls a data stream of the cartographer readings to a file.

```
  ACTION (StreamAction, default: 'status'): Stream action
    Allowed values: start, stop, cancel, status
  FILE (str | None, default: None): Output file path
```

## CARTOGRAPHER_TEMPERATURE_CALIBRATE

Calibrate temperature compensation for frequency drift

```
  MIN_TEMP (int, default: 40): Minimum coil temperature
    Constraints: minimum: 40, maximum: 50
  MAX_TEMP (int, default: 60): Maximum coil temperature
    Constraints: minimum: 60, maximum: 90
  BED_TEMP (int, default: 90): Bed temperature target
    Constraints: minimum: 90, maximum: 120
  Z_SPEED (int, default: 5): Z movement speed
    Constraints: minimum: 1
```

## CARTOGRAPHER_SCAN_CALIBRATE

Run the scan calibration

```
  MODEL (str, default: 'default'): Model name
  METHOD (ScanCalibrateMethod, default: 'manual'): Calibration method
    Allowed values: touch, manual
```

## CARTOGRAPHER_SCAN_ACCURACY

Collect samples from the probe and calculate statistics on the results.

```
  READINGS (int, default: 20): Readings per sample
    Constraints: minimum: 1
  SAMPLES (int, default: 100): Number of samples to collect
    Constraints: minimum: 10
```

## CARTOGRAPHER_SCAN_MODEL

Manage saved scan models

```
  LOAD (str | None, default: None): Model name to load
  REMOVE (str | None, default: None): Model name to remove
```

## CARTOGRAPHER_ESTIMATE_BACKLASH

Do a series of moves to estimate backlash on the Z axis.

```
  CALIBRATE (bool, default: No): Run calibration and save result
  ITERATIONS (int, default: 10): Number of measurement iterations
    Constraints: minimum: 1
  DELTA (float, default: 0.2): Movement delta in mm
    Constraints: minimum: 0.2, maximum: 1
```

## CARTOGRAPHER_TOUCH_CALIBRATE

Run the touch calibration

```
  MAX_VERIFY_RANGE (float, required): Maximum verification range
  MODEL (str, default: 'default'): Model name
  SPEED (int, default: 2): Probing speed
    Constraints: minimum: 1, maximum: 5
  START (int, default: 500): Starting threshold
    Constraints: minimum: 100
  MAX (int, default: 5000): Maximum threshold
    Constraints: minimum: 100
  VERIFICATION_SAMPLES (int, default: 10): Verification sample count
    Constraints: minimum: 3, maximum: 20
```

## CARTOGRAPHER_TOUCH_MODEL

Manage saved touch models

```
  LOAD (str | None, default: None): Model name to load
  REMOVE (str | None, default: None): Model name to remove
```

## CARTOGRAPHER_TOUCH_PROBE

Touch the bed to get the height offset at the current position.

*This macro accepts no parameters.*

## CARTOGRAPHER_TOUCH_ACCURACY

Touch the bed multiple times to measure the accuracy of the probe.

```
  LIFT_SPEED (float, required): Lift speed in mm/s
    Constraints: minimum: 1
  SAMPLE_RETRACT_DIST (float, default: 1.0): Retract distance between samples
    Constraints: minimum: 1.0
  SAMPLES (int, default: 5): Number of probe samples
    Constraints: minimum: 3
```

## CARTOGRAPHER_TOUCH_HOME

Touch the bed to home Z axis

```
  EXPERIMENTAL_RANDOM_RADIUS (float, required): Random homing radius
    Constraints: minimum: 0
```

## CARTOGRAPHER_AXIS_TWIST_COMPENSATION

Scan and touch to calculate axis twist compensation values.

```
  USE_TOUCH_BOUNDARIES (bool, default: No): Use touch boundaries for calibration range
  AXIS (str, default: 'x'): Axis to compensate (x or y)
  SAMPLE_COUNT (int, default: 5): Number of sample points
  START (float | None, default: None): Override start position
  END (float | None, default: None): Override end position
  LINE (float | None, default: None): Override line position
```

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
  LIFT_SPEED (float, default: config 'cartographer.lift_speed'): Lift speed in mm/s
    Constraints: minimum: 1
  SAMPLE_RETRACT_DIST (float, default: 1.0): Retract distance between samples
    Constraints: minimum: 1.0
  SAMPLES (int, default: 10): Number of probe samples
    Constraints: minimum: 3
```

**Example:**
```
PROBE_ACCURACY LIFT_SPEED=<lift_speed> SAMPLE_RETRACT_DIST=1.0 SAMPLES=10
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
  ADAPTIVE_MARGIN (float, default: config 'bed_mesh.adaptive_margin'): Margin for adaptive mesh
    Constraints: minimum: 0
  PROFILE (str, default: 'default'): Mesh profile name
  DIRECTION (MeshDirection, default: config 'scan.mesh_direction'): Primary scan direction
    Allowed values: x, y
  PATH (MeshPath, default: config 'scan.mesh_path'): Scan path pattern
    Allowed values: snake, alternating_snake, spiral, random
  SPEED (float, default: config 'bed_mesh.speed'): Scan speed
    Constraints: minimum: 50
  HEIGHT (float, default: config 'scan.mesh_height'): Scan height
    Constraints: minimum: 0.5, maximum: 5
  RUNS (int, default: config 'scan.mesh_runs'): Number of scan passes
    Constraints: minimum: 1
```

**Example:**
```
BED_MESH_CALIBRATE METHOD=scan ADAPTIVE=0 ADAPTIVE_MARGIN=<adaptive_margin> PROFILE=default DIRECTION=<direction> PATH=<path> SPEED=<speed> HEIGHT=<height> RUNS=<runs>
```

## CARTOGRAPHER_QUERY

Query current cartographer state

```
  FIELD (QueryField, default: 'all'): Field to query
    Allowed values: touch, scan, mcu, all
```

**Example:**
```
CARTOGRAPHER_QUERY FIELD=all
```

## CARTOGRAPHER_STREAM

Controls a data stream of the cartographer readings to a file.

```
  ACTION (StreamAction, default: 'status'): Stream action
    Allowed values: start, stop, cancel, status
  FILE (str | None, default: None): Output file path
```

**Example:**
```
CARTOGRAPHER_STREAM ACTION=status
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

**Example:**
```
CARTOGRAPHER_TEMPERATURE_CALIBRATE MIN_TEMP=40 MAX_TEMP=60 BED_TEMP=90 Z_SPEED=5
```

## CARTOGRAPHER_SCAN_CALIBRATE

Run the scan calibration

```
  MODEL (str, default: 'default'): Model name
  METHOD (ScanCalibrateMethod, default: 'manual'): Calibration method
    Allowed values: touch, manual
```

**Example:**
```
CARTOGRAPHER_SCAN_CALIBRATE MODEL=default METHOD=manual
```

## CARTOGRAPHER_SCAN_ACCURACY

Collect samples from the probe and calculate statistics on the results.

```
  READINGS (int, default: 20): Readings per sample
    Constraints: minimum: 1
  SAMPLES (int, default: 100): Number of samples to collect
    Constraints: minimum: 10
```

**Example:**
```
CARTOGRAPHER_SCAN_ACCURACY READINGS=20 SAMPLES=100
```

## CARTOGRAPHER_SCAN_MODEL

Manage saved scan models

```
  LOAD (str | None, default: None): Model name to load
  REMOVE (str | None, default: None): Model name to remove
```

**Example:**
```
CARTOGRAPHER_SCAN_MODEL
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

**Example:**
```
CARTOGRAPHER_ESTIMATE_BACKLASH CALIBRATE=no ITERATIONS=10 DELTA=0.2
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

**Example:**
```
CARTOGRAPHER_TOUCH_CALIBRATE MAX_VERIFY_RANGE=<max_verify_range> MODEL=default SPEED=2 START=500 MAX=5000 VERIFICATION_SAMPLES=10
```

## CARTOGRAPHER_TOUCH_MODEL

Manage saved touch models

```
  LOAD (str | None, default: None): Model name to load
  REMOVE (str | None, default: None): Model name to remove
```

**Example:**
```
CARTOGRAPHER_TOUCH_MODEL
```

## CARTOGRAPHER_TOUCH_PROBE

Touch the bed to get the height offset at the current position.

*This macro accepts no parameters.*

## CARTOGRAPHER_TOUCH_ACCURACY

Touch the bed multiple times to measure the accuracy of the probe.

```
  LIFT_SPEED (float, default: config 'cartographer.lift_speed'): Lift speed in mm/s
    Constraints: minimum: 1
  SAMPLE_RETRACT_DIST (float, default: 1.0): Retract distance between samples
    Constraints: minimum: 1.0
  SAMPLES (int, default: 5): Number of probe samples
    Constraints: minimum: 3
```

**Example:**
```
CARTOGRAPHER_TOUCH_ACCURACY LIFT_SPEED=<lift_speed> SAMPLE_RETRACT_DIST=1.0 SAMPLES=5
```

## CARTOGRAPHER_TOUCH_HOME

Touch the bed to home Z axis

```
  EXPERIMENTAL_RANDOM_RADIUS (float, default: config 'touch.EXPERIMENTAL_home_random_radius'): Random homing radius
    Constraints: minimum: 0
```

**Example:**
```
CARTOGRAPHER_TOUCH_HOME EXPERIMENTAL_RANDOM_RADIUS=<experimental_random_radius>
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

**Example:**
```
CARTOGRAPHER_AXIS_TWIST_COMPENSATION USE_TOUCH_BOUNDARIES=no AXIS=x SAMPLE_COUNT=5
```

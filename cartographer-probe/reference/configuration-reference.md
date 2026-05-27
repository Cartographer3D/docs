---
description: Auto-generated from plugin source.
---

# Configuration Reference

## Cartographer

```ini
[cartographer]
mcu:
#   The name of the Cartographer MCU, as defined by your [mcu cartographer] section.
x_offset:
#   The distance (in mm) between the probe and the nozzle along the x-axis.
y_offset:
#   The distance (in mm) between the probe and the nozzle along the y-axis.
#travel_speed: 50
#   The speed (in mm/s) of all travel moves.
#   Constraints: minimum: 1
#lift_speed: 5
#   The speed (in mm/s) of all Z lift moves.
#   Constraints: minimum: 1
#verbose: False
#   Set to yes to enable debug output.
#macro_prefix: None
#   A prefix to register a second set of Cartographer macros using, alongside 'CARTOGRAPHER_'. E.g. 'CARTO' would result in 'CARTO_TOUCH_HOME'.
```

## Scan

```ini
[cartographer scan]
#probe_speed: 5
#   Speed (in mm/s) of the Z axis when probing.
#   Constraints: minimum: 0.1
#mesh_runs: 1
#   Number of runs when doing a scan mesh. Consecutive runs will trace back the way it came from.
#mesh_height: 3
#   The height (in mm) of the head when doing a mesh run.
#   Constraints: minimum: 1
#mesh_direction: 'x'
#   Axis of which to do the most moves along.
#   Allowed values: x, y
#mesh_path: 'snake'
#   The path to use when calibrating a scan mesh.
#   Allowed values: snake, alternating_snake, spiral, random
```

## Touch

```ini
[cartographer touch]
#samples: 3
#   The number of samples to use when doing a touch.
#   Constraints: minimum: 3
#max_samples: 10
#   The maximum number of samples to do before giving up.
#max_noisy_samples: 2
#   The number of noisy samples tolerated within the sliding window. The window size is calculated as samples + max_noisy_samples. A smaller value prevents cherry-picking good samples from a noisy sequence.
#   Constraints: minimum: 0
#UNSAFE_max_touch_temperature: 150
#   The maximum allowed nozzle temperature to use when touching the plate. This is set to 150C to avoid damaging your plate. Change this AT YOUR OWN RISK.
#EXPERIMENTAL_home_random_radius: 0.0
#   Radius around the Z home position to do touch.
#   Constraints: minimum: 0.0
#retract_distance: 2.0
#   Retract distance (in mm) between touch samples.
#   Constraints: minimum: 1.0
#sample_range: 0.01
#   Acceptable range (in mm) between touch samples.
#   Constraints: minimum: 0.001, maximum: 0.015
```

## Bed Mesh

```ini
[bed_mesh]
mesh_min:
#   Minimum coordinates of the mesh area.
mesh_max:
#   Maximum coordinates of the mesh area.
probe_count:
#   Number of probe points in X and Y.
zero_reference_position:
#   Position used as zero reference for the mesh.
faulty_regions:
#   Regions to exclude from mesh probing.
#speed: 50
#   Travel speed during mesh probing.
#   Constraints: minimum: 1
#horizontal_move_z: 5
#   Z height for horizontal moves during mesh.
#   Constraints: minimum: 1
#adaptive_margin: 5
#   Margin for adaptive mesh boundaries.
#   Constraints: minimum: 0
```

## Coil

```ini
[cartographer coil]
#name: 'cartographer_coil'
#   The name of the coil temperature sensor.
#min_temp: 0
#   The minimum temperature of the coil, below this will trigger a warning.
#   Constraints: minimum: -273.15
#max_temp: 105
#   The maximum temperature of the coil, above this will trigger a warning.
```

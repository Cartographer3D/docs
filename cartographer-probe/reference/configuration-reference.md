# Configuration Reference

### [cartographer]

```
[cartographer]
mcu:
#   The name of the Cartographer MCU, as defined by your [mcu cartographer]
#   section.
x_offset:
#   The distance (in mm) between the probe and the nozzle along the x-axis.
y_offset:
#   The distance (in mm) between the probe and the nozzle along the y-axis.
#travel_speed: 50
#   The speed (in mm/s) of all travel moves.
#   The default is 50.
#   Minimum value is 1.
#lift_speed: 5
#   The speed (in mm/s) of all Z lift moves.
#   The default is 5.
#   Minimum value is 1.
#verbose: no
#   Set to yes to enable debug output.
#   The default is no.
#macro_prefix:
#   A prefix to register a second set of Cartographer macros using,
#   alongside 'CARTOGRAPHER_'. E.g. 'CARTO' would result in
#   'CARTO_TOUCH_HOME'.
```

### [cartographer scan]

```
[cartographer scan]
#probe_speed: 5
#   Speed (in mm/s) of the Z axis when probing.
#   The default is 5.
#   Minimum value is 0.1.
#mesh_runs: 1
#   Number of runs when doing a scan mesh. Consecutive runs will trace back
#   the way it came from.
#   The default is 1.
#mesh_height: 3
#   The height (in mm) of the head when doing a mesh run.
#   The default is 3.
#   Minimum value is 1.
#mesh_direction: x
#   Axis of which to do the most moves along.
#   The default is 'x'.
#   Allowed values: 'x', 'y'.
#mesh_path: snake
#   The path to use when calibrating a scan mesh.
#   The default is 'snake'.
#   Allowed values: 'snake', 'alternating_snake', 'spiral', 'random'.
```

### [cartographer touch]

```
[cartographer touch]
#samples: 3
#   The number of samples to use when doing a touch.
#   The default is 3.
#   Minimum value is 3.
#max_samples: 10
#   The maximum number of samples to do before giving up.
#   The default is 10.
#UNSAFE_max_touch_temperature: 150
#   The maximum allowed nozzle temperature to use when touching the plate.
#   This is set to 150C to avoid damaging your plate. Change this AT YOUR
#   OWN RISK.
#   The default is 150.
#EXPERIMENTAL_home_random_radius: 0.0
#   Radius around the Z home position to do touch.
#   The default is 0.0.
#   Minimum value is 0.0.
#retract_distance: 2.0
#   Retract distance (in mm) between touch samples.
#   The default is 2.0.
#   Minimum value is 1.0.
#sample_range: 0.01
#   Acceptable range (in mm) between touch samples.
#   The default is 0.01.
#   Must be between 0.001 and 0.015.
```

### [cartographer coil]

```
[cartographer coil]
#name: cartographer_coil
#   The name of the coil temperature sensor.
#   The default is 'cartographer_coil'.
#min_temp: 0
#   The minimum temperature of the coil, below this will trigger a warning.
#   The default is 0.
#   Minimum value is -273.15.
#max_temp: 105
#   The maximum temperature of the coil, above this will trigger a warning.
#   The default is 105.
```

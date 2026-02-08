# Configuration Reference

#### General config

```
[cartographer]
x_offset:
#   The distance (in mm) between the probe and the nozzle along the
#   x-axis.
y_offset:
#   The distance (in mm) between the probe and the nozzle along the
#   y-axis.
#travel_speed: 50
#   The speed of all travel moves (in mm/s). The default is 50mm/s.
#macro_prefix:
#   A prefix to register a second set of Cartographer macros using,
#   alongside 'CARTOGRAPHER_'.
#   E.g. 'CARTO' would result in 'CARTO_TOUCH_HOME'.
#verbose: no
#   Set to yes to enable debug output. The default is no.
```

#### Scan config

```
[cartographer scan]
#probe_speed: 5
#   Speed (in mm/s) of the Z axis when probing. The default is 5mm/s.
#mesh_runs: 1
#   Number of runs when doing a scan mesh.
#   Consecutive runs will trace back the way it came from.
#   The default is 1 run.
#mesh_direction: x
#   Axis of which to do the most moves along - either 'x' or 'y'.
#   The default is the x-axis
#mesh_height: 3
#   The height (in mm) of the head, when doing a mesh run.
#   The default is 3 mm.
#mesh_path: snake
#   The path to use when calibrating a scan mesh - either 'snake',
#   'alternating_snake', 'spiral' or 'random'.
#   The default is snake.
```

#### Touch config

```
[cartographer touch]
#samples: 3
#   The number of samples to use when doing a touch.
#   The default is 3.
#max_samples: 10
#   The maximum number of samples to do before giving up.
#   The default is samples * 2, but minimum 10.
#sample_range: 0.01
#retract_distance: 5
#    Retract distance between touch samples
#    The default is 2.
#UNSAFE_max_touch_temperature: 150
#   The maximum allowed nozzle temperature to use when touching the plate.
#   This is set to 150C to avoid damaging your plate.
#   Change this AT YOUR OWN RISK.
#   The default is 150C.
#EXPERIMENTAL_home_random_radius: 0
#    Radius around the Z home position to do touch.
```

#### Coil sensor config

```
[cartographer coil]
#name: cartographer_coil
#   The name of the coil temperature sensor.
#   The default is 'cartographer_coil'.
#min_temp: 0
#   The minimum temperature of the coil, below this will trigger a warning.
#   The default is 0.
#max_temp: 105
#   The maximum temperature of the coil, above this will trigger a warning.
#   The default is 105.
```

---
description: >-
  THIS HASNT FULLY LAUNCHED YET, IT WILL BE LAUNCHED IN THE NEXT 48 hours
  (hopefully)
---

# 👇 Touch (WIP)

## <mark style="color:red;">Requirements</mark>

***

## Firmware Update

[Follow the guide ](firmware/firmware-updating/)on updating your firmware. Select <mark style="color:green;">WITH SURVEY.</mark>

***

## Installation

[Follow the guide for probe installation first.](installation-and-setup/probe-installation/)

***

## Configuration

<details>

<summary>Printer.cfg</summary>

```python
[scanner]
canbus_uuid: 0ca8d67388c2        #adjust to suit your scanner
#serial: 
x_offset: 0                      #adjust for your offset
y_offset: 15                     #adjust for your offset
touch_location: 125,125          # set to center of bed

############# DEFAULT VALUES BELOW

speed: 40
lift_speed: 5
backlash_comp: 0.5

# BED MESHING SETTINGS
mesh_main_direction: x
mesh_cluster_size: 1
mesh_runs: 2

# TOUCH SETTINGS
calibration_method: touch 
probe_speed: 2.0
sensor: cartographer
sensor_alt: carto ## allows use of shorter commands. ie CARTO_TOUCH instead of CARTOGRAPHER_TOUCH
scanner_touch_accel:100
scanner_touch_max_speed:10
scanner_touch_speed:3
scanner_touch_retract_dist:2
scanner_touch_retract_speed:10
scanner_touch_sample_count:3
scanner_touch_tolerance:0.008
scanner_touch_max_retries:3
scanner_touch_move_speed:50
scanner_touch_z_offset: 0.05
detect_threshold_Z: 2500
```



</details>

<details>

<summary>Print Start Macro</summary>

Adding the `CARTOGRAPHER_TOUCH` command to your print start macro ensures that the printer performs a precise touch probe <mark style="color:red;">**BEFORE**</mark> executing the `BED_MESH_CALIBRATE` command and <mark style="color:red;">**AFTER**</mark> your nozzle reaches 150c. This sequence helps to achieve an accurate bed leveling by accounting for any variations or offsets before the mesh calibration.

```gcode
[gcode_macro PRINT_START]
gcode:
    G28                               ; Home all axes
    M104 S{BED_TEMP}                  ; Set bed temperature
    M109 S150                         ; Wait for extuder to reach 150°C (intermediate step)
    M140 S{BED_TEMP}                  ; Set final bed temperature
    G28 Z                             ; Home Z axis again to account for thermal expansion
    QGL/Z_TILT                        ; Perform quad gantry leveling or Z tilt adjustmen
    CARTOGRAPHER_TOUCH                ; Perform touch probe
    BED_MESH_CALIBRATE                ; Calibrate the bed mesh
    M190 S{EXTRUDER_TEMP}             ; Wait for extruder to reach target temperature

```



</details>

## Initial Calibration

{% hint style="danger" %}
Touch is best calibrated for use with a clean install. We ask you remove your existing `[scanner]` or `[cartographer]` model if you have one and any other `[scanner]` or `[cartographer]` settings from the bottom of <mark style="color:yellow;">**printer.cfg**</mark>
{% endhint %}

### Quick Calibration - Default Threshold 2500 (Good for Most)

```gcode
G28 X Y
CARTOGRAPHER_TOUCH METHOD=manual   # initiates paper test we all know and love
G28 Z
QUAD_GANTRY_LEVEL / Z_TILT        
CARTOGRAPHER_TOUCH CALIBRATE=1     # starts touch test and calibration
SAVE_CONFIG                        # saves new model
```

### Threshold Test Method

```gcode
G28 X Y
CARTOGRAPHER_TOUCH METHOD=manual   # initiates paper test we all know and love
G28 Z
QUAD_GANTRY_LEVEL / Z_TILT
CARTOGRAPHER_THRESHOLD_SCAN 
CARTOGRAPHER_TOUCH CALIBRATE=1 THRESHOLD=whatever scan said     # starts touch test and calibration 
SAVE_CONFIG                        # saves model and threshold
```

***

## Available Commands

### `CARTOGRAPHER_TOUCH`

The `CARTOGRAPHER_TOUCH` command is designed to initiate a probing process. This will then attempt to bring the nozzle to the bed and measure this for repeatability. This ensures a perfect first layer if configured correctly.

<details>

<summary>Detailed Explanation</summary>

**Key Functions:**

* **Configuration and Initialization:**
  * The command starts by pulling various parameters either from the command itself, or falling back on default values defined in the printer's configuration (**`printer.cfg`**).
  * Parameters include speed, acceleration, retraction distances, number of samples, tolerance levels, and the specific location (X and Y coordinates) where the probing will occur.

<!---->

* **Mode Selection:**
  * The command operates in **Touch Mode**, which uses a physical touch sensor to detect contact with the surface.
  * The mode is determined by the `calibration_method` configuration in **printer.cfg**, and the command ensures that touch mode is selected.

<!---->

* **Safety and Validation Checks:**
  * Before proceeding, the command ensures that the X and Y axes are homed (i.e., the machine knows their precise positions).
  * If the axes are not homed, the command raises an error, preventing the probing process from proceeding.

<!---->

* **Probing Process:**
  * The toolhead is moved to the specified touch location (X, Y coordinates).
  * The probing process begins, collecting multiple samples to determine the exact position.
  * The process accounts for factors such as acceleration, speed, retraction distance, and retries if the tolerance levels are not met.
  * If the `manual` method is specified, a manual calibration process (paper test) is initiated instead of the automated touch process.

<!---->

* **Result Handling:**
  * Once the probing process is completed, the results (e.g., final position, standard deviation of the samples) are logged and displayed.
  * If the probing is successful, the results are used to calibrate the system, adjusting the Z-offset or other calibration parameters as needed.
  * If the probing fails, an error message is provided, and no calibration is applied.

<!---->

* **Logging and Debugging:**
  * The command supports a debug mode that logs detailed information about the probing process, including all the parameters used and the results obtained.
  * This is useful for troubleshooting and ensuring the probing process is functioning correctly.

#### Use Cases:

* **Bed Leveling:** Ensures that the print bed is perfectly level by detecting any variations in height across different points on the bed.

<!---->

* **Z-Offset Calibration:** Adjusts the Z-axis offset to ensure the nozzle is at the correct distance from the print bed for optimal printing.

<!---->

* **Probing Accuracy:** Verifies the precision and repeatability of the probing process, ensuring consistent results.



</details>

<details>

<summary>Available Parameters</summary>

#### `CALIBRATE = 1`

* Starts the touch test BUT also creates a model upon success.

#### `METHOD = MANUAL`

* Initiates the manual paper test for creating an initial scanner mode.

#### `SPEED =`

* Specifies the speed at which the probing move is executed.
* **Default**: 3
* **Constraints**: Cannot exceed 5.

#### `ACCEL =`

* Sets the acceleration used during the touch operation.
* **Default**: 100
* **Constraints**: Must be above 0 and at least 100.

#### `RETRACT =`

* Determines the distance the toolhead retracts after a probe.
* **Default**: 2
* **Constraints**: Must be at least 1.

#### `RETRACT_SPEED =`

* **Sets the speed for the retraction move after probing.**
* **Default: 10**
* **Constraints: Must be at least 1.**

#### `SAMPLES =`&#x20;

* Defines the number of samples to take during the touch operation.
* **Default**: 3
* **Constraints**: Must be at least 1.

#### `TOLERANCE =`&#x20;

* Sets the tolerance level for the touch samples.
* **Default**: 0.008
* **Constraints**: Must be above 0.0.

#### `RETRIES =`&#x20;

* Specifies the maximum number of retries allowed if samples exceed the tolerance.
* **Default**: 3
* **Constraints**: Must be at least 0.

#### `TOUCH_LOCATION_X =`&#x20;

#### `TOUCH_LOCATION_Y =`&#x20;

* Specifies the X or Y coordinate of the touch location where the probing will occur.
* **Default Value**: 100
* **Constraints**: None explicitly stated, but should correspond to a valid X or Y coordinate within the machine's range.

#### `THRESHOLD =`&#x20;

* Defines the threshold value used for detecting a touch during probing.
* **Default**: 2500
* **Constraints**: Must be at least 100; can be found via `CARTOGRAPHER_THRESHOLD_SCAN`

#### `DEBUG = 1`

* Enables or disables debug mode, which controls the verbosity of logging and information output during the touch operation.
* **Default**: 0 (debugging off)
* **Constraints**: 0 if off, 1 is on.
* This will enabled debugging information. Its useful for showing information relevant to how touch height is calculated. If you encounter issues, this is what you should provide in discord alongside <mark style="color:red;">klippy.log</mark>

</details>

***

### `CARTOGRAPHER_THRESHOLD_SCAN`

#### Available Parameters

#### MIN=

MAX=



***

### `CARTOGRAPHER_THRESHOLD_TEST`

#### Available Parameters


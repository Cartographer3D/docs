---
layout:
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: false
---

# 👇 Survey Touch

{% hint style="danger" %}
We **DO NOT** 100% guarantee compatibility with ALL printers. It is your responsibility to read this entire guide prior to use and to research whether this is right for you. Please contact us on [DISCORD ](https://discord.gg/yzazQMEGS2)if you have questions.
{% endhint %}

***

## Firmware Update

[Follow the guide ](firmware/firmware-updating/)on updating your firmware. Select <mark style="color:green;">WITH SURVEY TOUCH.</mark>

{% hint style="info" %}
**Did You Know?**\
Even with Survey Touch firmware you can run in scan only mode if you dont want to use Touch.\
Just set`calibration_method:scan` in <mark style="color:yellow;">printer.cfg</mark>
{% endhint %}

***

## Installation

[Follow the guide for probe installation first.](installation-and-setup/probe-installation/)

***

## Configuration

{% hint style="danger" %}
Please remove all of your existing \[cartographer] or \[scanner] sections from your printer.cfg and other configurations before proceeding.
{% endhint %}

<details>

<summary>Printer.cfg Configuration <mark style="color:red;">IMPORTANT</mark></summary>

{% code overflow="wrap" %}
```yaml
[scanner]
canbus_uuid: 0ca8d67388c2            #adjust to suit your scanner 
x_offset: 0                          #adjust for your offset
y_offset: 15                         #adjust for your offset
calibration_method: touch 
sensor: cartographer
sensor_alt: carto

[bed_mesh]
zero_reference_position: 125, 125    # set this to your touch_location or middle of your bed
```
{% endcode %}

These are <mark style="color:red;">REQUIREMENTS</mark>. Including the `zero_reference_position` in your `[bed_mesh]` section.&#x20;

</details>

<details>

<summary>Print Start Macro Example <mark style="color:red;">IMPORTANT</mark></summary>

Adding the `CARTOGRAPHER_TOUCH` command to your print start macro ensures that the printer performs a precise touch probe <mark style="color:red;">**AFTER**</mark> executing the `BED_MESH_CALIBRATE` command and <mark style="color:red;">**AFTER**</mark> your nozzle reaches a steady 150c. This sequence helps to achieve an accurate bed leveling by accounting for any variations or offsets after the mesh calibration.

```gcode
[gcode_macro PRINT_START_EXAMPLE]
gcode:
    G28                               ; Home all axes
    M104 S{BED_TEMP}                  ; Set bed temperature
    M109 S150                         ; Wait for extuder to reach 150°C (intermediate step)
    M140 S{BED_TEMP}                  ; Set final bed temperature
    G28 Z                             ; Home Z axis again to account for thermal expansion
    QUAD_GANTRY_LEVEL / Z_TILT_ADJUST ; Perform quad gantry leveling or Z tilt adjustmen
    G28 Z                             ; Home Z axis again to account for thermal expansion
    BED_MESH_CALIBRATE                ; Calibrate the bed mesh
    CARTOGRAPHER_TOUCH                ; Perform touch probe
    M109 S{EXTRUDER_TEMP}             ; Wait for extruder to reach target temperature

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
QUAD_GANTRY_LEVEL / Z_TILT_ADJUST
G28 Z        
CARTOGRAPHER_TOUCH CALIBRATE=1     # starts touch test and calibration
SAVE_CONFIG                        # saves new model
```

### Threshold Test Method

```gcode
G28 X Y
CARTOGRAPHER_TOUCH METHOD=manual   # initiates paper test we all know and love
G28 Z
QUAD_GANTRY_LEVEL / Z_TILT_ADJUST
G28 Z
CARTOGRAPHER_THRESHOLD_SCAN 
CARTOGRAPHER_TOUCH CALIBRATE=1     # starts touch test and calibration 
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
  * The command starts by pulling various parameters either from the command itself, or falling back on default values defined in the printer's configuration (printer.cfg).
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
* **Constraints**: Must be greater than or equal to 100.

#### `RETRACT =`

* Determines the distance the toolhead retracts after a probe.
* **Default**: 2
* **Constraints**: Must be at least 1.

#### `RETRACT_SPEED =`

* Sets the speed for the retraction move after probing**.**
* **Default:** 10
* **Constraints:** Must be at least 1.

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

* Specifies the X coordinate of the touch location where the probing will occur.

<!---->

* **Default Value**: Detects middle of your bed specified by your \[**STEPPER\_X] POSITION\_MAX**

<!---->

* **Constraints**: None explicitly stated, but should correspond to a valid X coordinate within the machine's range.

#### `TOUCH_LOCATION_Y =`&#x20;

* Specifies the Y coordinate of the touch location where the probing will occur.
* **Default Value**: Detects middle of your bed specified by your \[**STEPPER\_Y] POSITION\_MAX**
* **Constraints**: None explicitly stated, but should correspond to a valid Y coordinate within the machine's range.

#### `THRESHOLD =`&#x20;

* Defines the threshold value used for detecting a touch during probing.
* **Default**: 2500 or <mark style="color:green;">scanner\_touch\_threshold</mark> in <mark style="color:red;">printer.cfg</mark>
* **Constraints**: Must be at least 100; can be found via `CARTOGRAPHER_THRESHOLD_SCAN`

#### `DEBUG = 1`

* Enables or disables debug mode, which controls the verbosity of logging and information output during the touch operation.
* **Default**: 0 (debugging off)
* **Constraints**: 0 if off, 1 is on.
* This will enabled debugging information. Its useful for showing information relevant to how touch height is calculated. If you encounter issues, this is what you should provide in discord alongside <mark style="color:red;">klippy.log</mark>

</details>

***

### `CARTOGRAPHER_THRESHOLD_SCAN`

The `CARTOGRAPHER_THRESHOLD_SCAN` command is used to scan a range of threshold values to find the most consistent and reliable threshold for the touch sensor. This function performs a series of probe tests across different threshold values, evaluating the consistency of each threshold until it finds the best one that meets the specified criteria.

<details>

<summary>Detailed Explanation</summary>

**Process**

1. **Threshold Scanning**
   * The scan starts by setting the trigger method to touch and initializing the current threshold to the minimum value (`MIN`).
   * The function then enters a loop where it tests each threshold value, increasing by the step size (`STEP`) until the maximum threshold (`MAX`) is reached.
2. **Threshold Qualification**
   * For each threshold value, a series of probe tests (`QUALIFY_SAMPLES`) are conducted.
   * The results are evaluated to see if they meet the acceptable range value (`RANGE_VALUE`).
3. **Threshold Verification**
   * If a threshold value shows promising consistency during qualification, it is further verified with an additional set of probe tests (`VERIFY_SAMPLES`).
   * The threshold is evaluated for quality based on the consistency of the results.
4. **Finalization**
   * If a threshold value is found that meets or exceeds the target consistency (`TARGET`), it is considered the best threshold.
   * If this threshold is different from the original, it is saved for future use.
5. **Logging Results**
   * Throughout the process, the function logs information about the testing of each threshold, including whether it passed qualification and verification.
   * At the end of the scan, the best threshold value is logged along with its quality level and range.

</details>

<details>

<summary>Available Parameters</summary>

#### **`MIN =`**

* Purpose: Defines the minimum threshold value for starting the scan.
* **Default:** 500
* **Constraints:** Must be atleast 100 and less than MAX.

#### **`MAX =`**

* Defines the maximum threshold value for ending the scan.
* **Default:** 5000
* **Constraints:** Must be greater than MIN.

#### **`STEP =`**

* Specifies the increment by which the threshold is increased during the scan.
* **Default:** 500
* **Constraints:** Must be a positive number.

#### **`SKIP =`**

* Indicates the number of initial samples to skip when evaluating thresholds.
* **Default:** 0
* **Constraints:** Must be a positive number.

#### **`QUALIFY_SAMPLES =`**

* The number of samples used to initially qualify a threshold.
* **Default:** 3
* **Constraints:** Must be greater than or equal to SKIP.

#### **`VERIFY_SAMPLES =`**

* The number of samples used to verify a threshold that shows promise during qualification.
* **Default:** 5
* **Constraints:** Must be a positive number.

#### **`TARGET =`**

* The desired maximum range value for a threshold to be considered acceptable.
* **Default:** 0.08
* **Constraints:** Must be a positive number.

#### **`RANGE_VALUE =`**

* Specifies the maximum acceptable range value for a threshold to be considered during scanning.
* **Default:** 0.05
* **Constraints:** Must be a positive number, with a minimum value of 0.0125.

</details>

***

### `CARTOGRAPHER_THRESHOLD_TEST`

The `CARTOGRAPHER_THRESHOLD_TEST` command is used to home using a touch sensor and check the consistency of the sensor's response. The function performs a series of probe tests at a specified threshold to determine the reliability of the sensor across multiple samples. The results are evaluated for maximum, minimum, range, average, median, and standard deviation of the probe results.

<details>

<summary>Detailed Explanation</summary>

* **Threshold Testing**
  * The test begins by setting the trigger method to 1 (touch method) and adjusting the threshold to the provided value.
  * The function then executes a series of probe tests, collecting the specified number of samples (`SAMPLES`), while skipping the specified number of initial samples (`SKIP`).
* **Probe Accuracy Check**
  * This function adjusts the probe position, performs the probe test, and measures the consistency of the results.
* **Result Evaluation**
  * The results are evaluated for:
    * Maximum value
    * Minimum value
    * Range (difference between max and min)
    * Average value
    * Median value
    * Standard deviation (sigma)
    * Number of samples within a 0.1 range
    * Number of early and late probe events
  * The quality of the threshold is then assessed based on the calculated range.
* **Finalization**
  * After the test, the threshold is restored to its original value.
  * The results are logged, and information about the test's success and the quality of the threshold is provided.

</details>

<details>

<summary>Available Parameters</summary>



**`THRESHOLD =`**&#x20;

* The threshold value to use for the test.
* **Default**: The current `scanner_touch_threshold` value.

**`SAMPLES =`**

* The number of probe samples to take during the test.
* **Default**: 5
* **Constraint**: min 1

**SKIP =**

* The number of initial samples to skip before recording results.
* **Default**: 0
* **Constraint**: min 0

</details>

***

## Available Printer.cfg Settings

{% hint style="info" %}
These shouldn't be needed to changed, however they are available.
{% endhint %}

<details>

<summary>Available Settings</summary>

* **sensor**
  * Default: cartographer
* **sensor\_alt**
  * Default: carto
* **speed**
  * Default: 5.0
  * Constraint: above 0.0
* **lift\_speed**
  * Default: Value of `speed`
  * Constraint: above 0.0
* **backlash\_comp**
  * Default: 0.5

<!---->

* **probe\_speed**
  * Default: 5.0
* **touch\_location**
  * Default:  defaults to the center of the bed if not specified
  * Example: 125, 125
* **samples**
  * Default: 5
  * Constraint: above 0.0
* **samples\_retract\_dist**
  * Default: 5.0
  * Constraint: above 0.0
* **samples\_tolerance**
  * Default: 0.2
  * Constraint: min 0.0
* **samples\_tolerance\_retries**
  * Default: 4
  * Constraint: min 0
* **samples\_result**
  * Default: "median"
  * Available Options: median or average
* **x\_offset**
  * Default: 0.0
* **y\_offset**
  * Default: 0.0

<!---->

* **z\_hop\_dist**
  * Default: 5.0
  * Constraint: above 0.0
* **z\_hop\_speed**
  * Default: 5.0
  * Constraint: above 0.0

<!---->

* **calibration\_method**
  * Default: "scan"
  * Available options: touch or scan
* **trigger\_distance**
  * Default: 2.0
* **trigger\_dive\_threshold**
  * Default: 1.5
* **trigger\_hysteresis**
  * Default: 0.006
* **z\_settling\_time**
  * Default: 5 seconds
  * Constraint: min 0
* **scanner\_touch\_accel**
  * Default: 100
  * Constraint: above 0, min 100
* **scanner\_touch\_max\_speed**
  * Default: 10
  * Constraint: above 0, max 30
* **scanner\_touch\_speed**
  * Default: 3
  * Constraint: max scanner\_touch\_max\_speed
* **scanner\_touch\_retract\_dist**
  * Default: 2
  * Constraint: min 1
* **scanner\_touch\_retract\_speed**
  * Default: 10
  * Constraint: min 1
* **scanner\_touch\_sample\_count**
  * Default: 3
  * Constraint: min 1
* **scanner\_touch\_tolerance**
  * Default: 0.008
  * Constraint: above 0.0
* **scanner\_touch\_max\_retries**
  * Default: 3
  * Constraint: min 0
* **scanner\_touch\_move\_speed**
  * Default: 50
  * Constraint: min 1
* **scanner\_touch\_calibrate**
  * Default: 0
* **scanner\_touch\_z\_offset**
  * Default: 0.05
* **scanner\_touch\_max\_temp**
  * Default: 150
  * Nozzle touching temperature must be below this limit. In Celsius
* **scanner\_touch\_threshold**
  * Default: 2500

</details>

***

## Frequently Asked Questions

#### What do I need to add or change in my print start macro?

See [Print Start Macro](survey-touch.md#print-start-macro-example). But bascially, you just need to make sure your nozzle is at **maximum 150c** and then do a `CARTOGRAPHER_TOUCH` after you do a `BED_MESH_CALIBRATE`

#### I'm getting weird errors after updating my scanner.py, what do I do?

Firstly make sure you have hit the **RESTART KLIPPER** button in your Fluid/Mainsail UI, this will force the refresh of scanner.py to the updated version.

<figure><img src="../.gitbook/assets/Screenshot 2024-08-21 210954.png" alt="" width="356"><figcaption><p>Always RESTART KLIPPER after an update.</p></figcaption></figure>

#### Does touch work with glass or garolite beds?

It **CAN SOMETIMES** work depending on the thickness of your glass or garolite bed. However we can't say for certain. If its less than 2mm thick theres a good chance however we **accept no responsibility** if it **doesn't** work!&#x20;

#### Option 'X' is not valid in section 'scanner'

&#x20;You have a parameter within your `[scanner]` section in printer.cfg that isnt valid. Remove X from your printer.cfg or check its written correctly. You can see [valid parameters here](survey-touch.md#available-printer.cfg-settings)

#### Is it guaranteed that this will work on my printer?&#x20;

As with a lot of things in life, we **can't guarantee 100% compatibility**, it should be compatible with most well built printers, there are obviously some exceptions, the biggest impacting factor is the quality of the Z axis motion. If there is any binding or lack of consistency, then you may find that you will not be able to use this feature. You can still use **regular cartographer scan mode** though!

#### I was in the beta, how do I switch back to regular to continue using touch?

```bash
cd ~
sudo rm -rv Carto_TAP
cd ~/klipper/klippy/extras
sudo rm -rv scanner.py
cd ~/cartographer-klipper
git fetch
git pull
chmod +x install.sh
./install.sh
sudo service klipper restart
```

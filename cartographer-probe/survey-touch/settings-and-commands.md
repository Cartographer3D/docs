# Settings & Commands

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
* **Default:** 250
* **Constraints:** Must be a positive number.

#### **`SKIP =`**

* Indicates the number of initial samples to skip when evaluating thresholds.
* **Default:** 1
* **Constraints:** Must be a positive number.

#### **`QUALIFY_SAMPLES =`**

* The number of samples used to initially qualify a threshold.
* **Default:** 5
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
* **Default**: 1
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


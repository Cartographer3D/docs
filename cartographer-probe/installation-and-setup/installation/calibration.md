---
description: Cartographer Calibration
---

# Calibration

<mark style="color:purple;">Last Updated: March 2, 2025</mark>

## Initial Calibration

{% hint style="info" %}
Calibration can be done <mark style="color:red;">HOT</mark> or <mark style="color:blue;">COLD.</mark>
{% endhint %}

***

{% hint style="danger" %}
### Touch Specific

If you want to use cartographer for auto z offset, you will need to follow any extra **TOUCH** specific instructions.

First, make sure you're in TOUCH mode

```gcode
PROBE_SWITCH MODE=touch
```

Then make sure you save

```gcode
SAVE_CONFIG
```
{% endhint %}

***

Home the machine in X and Y:

```gcode
G28 X Y
```

Position the nozzle in the center of the bed. You will need to adjust the coordinates for your machine.

```gcode
G0 X125 Y125
```

{% hint style="warning" %}
At this point,  you might note that your Endstop Z is TRIGGERED, this is normal, and will be resolved once you run the next command.

![](<../../../.gitbook/assets/image (6) (1) (1) (1) (1).png>)
{% endhint %}

Start the calibration process:

```gcode
CARTOGRAPHER_CALIBRATE METHOD=manual
```

You can either use the web interface to adjust the nozzle height from the bed, or `TESTZ Z=-0.01` to lower it. \
\
Use a piece of paper  or a feeler gauge to measure the offset. Once finished remove the paper/gauge and accept the position.

```gcode
ACCEPT
```

Save the results to your config file.

```gcode
SAVE_CONFIG
```

Home your printer.&#x20;

```gcode
G28
```

You can test the accuracy of the scanner coil.

```gcode
PROBE_ACCURACY
```

{% hint style="warning" %}
This will not TOUCH the bed. It will use the scanner to measure the accuracy of the probe coil.
{% endhint %}

You can also measure the backlash of your Z axis

```gcode
CARTOGRAPHER_ESTIMATE_BACKLASH
```

To make use of the backlash estimation that is given. You will get results spit out starting with &#x20;

```
Median distance moving up
```

In this line will be a measurement called "delta" Take note of the value. Locate the configuration section marked:

```gcode
backlash_comp: 2.01
```

Update this section with your new estimated backlash compensation. It is a good idea to do this compensation test at all 4x corners of your build plate and then again at middle of build plate. If you are on a printer with belted Z and the values in each corner deviate heavily compared to other corners results,  this would indicate a loose belt on that corner.&#x20;

If you are using a printer which supports either `Z_TILT` or `QUAD_GANTRY_LEVEL` you will need to ensure that your probe is positioned above the bed when performing this, open up your `printer.cfg` and find the appropriate section, for example your QUAD\_GANTRY\_LEVEL section may look like this:

<pre class="language-django"><code class="lang-django">[quad_gantry_level]
gantry_corners:
   -60,-10
   410,420
#  Probe points
points:
   50,25   # Point 1
   50,275  # Point 2
   300,275 # Point 3
   300,25  # Point 4
#--------------------------------------------------------------------
<strong>
</strong>speed: 100
horizontal_move_z: 10
retries: 5
retry_tolerance: 0.0075
max_adjust: 10
</code></pre>

You should in your console navigate to each point to ensure that your probe is not hanging off the edge, you can do this using a `G0` command such as `G0 X50 Y25` for point 1, or `G0 X50 Y275` for point 2. &#x20;

If at all points, Cartographer is safely over the bed, you should be good to go for running a `QUAD_GANTRY_LEVEL` or `Z_TILT` .

You can now run a Bed Mesh Calibration (I would advise doing either a `Z_TILT` or `QUAD_GANTRY_LEVEL` before.

```gcode
BED_MESH_CALIBRATE
```
{% hint style="info" %}
When Cartographer is installed, `BED_MESH_CALIBRATE` defaults to `METHOD=scanner`, you do not need to add a method.  For compatibility reasons, `METHOD=scan` and `METHOD=rapid_scan` will not work with Cartographer, so just omit the method.
{% endhint %}
***

### If you are <mark style="color:red;">NOT</mark> using TOUCH you should now [continue with this guide](first-print.md#scan-mode-first-print).

***

## Setting up Touch

Perform a homing.

```gcode
G28
```

If using a printer that requires Quad Gantry Level or Z Tilt Adjust, perform that.

```gcode
QUAD_GANTRY_LEVEL
```

or

```gcode
Z_TILT_ADJUST
```

Once that is finished, do another home or G28 Z

```gcode
G28 Z
```

Initiate a threshold scan. This will determine your threshold for cartographer. The threshold will determine how much force is required to touch your bed consistently.

Start by doing the generic scan

{% hint style="info" %}
[ Visit here for an explanation of `CARTOGRAPHER_THRESHOLD_SCAN`](../../settings-and-commands.md#cartographer_threshold_scan)
{% endhint %}

{% hint style="warning" %}
Prior to doing the threshold scan,  please ensure that the following is true.&#x20;

* Your nozzle is clean
* Your bed is clean, there are no dents or bubbles in the location you're probing.&#x20;
* Your probe is between 2.6 and 3mm above the nozzle.&#x20;
* Your kinematics are rigid.&#x20;
{% endhint %}

```gcode
CARTOGRAPHER_THRESHOLD_SCAN 
```

This should start a touch process that will move the toolhead into a starting position and then lower until it touches the bed, repeating itself. Its okay if at first it doesnt touch the bed at all, this is completely normal. It will eventually start touching.&#x20;

{% hint style="info" %}
`CARTOGRAPHER_THRESHOLD_SCAN SPEED=2` is also available if the initial scan fails.
{% endhint %}

If however you get a final Optimal result and it didnt touch the bed, start the process again OR adjust the parameters as follows where MIN= the found threshold value of the false positive.

```gcode
CARTOGRAPHER_THRESHOLD_SCAN MIN=500 
```

Once it finds an optimal threshold and you've seen the nozzle touching the bed. It will stop this process.&#x20;

{% hint style="info" %}
You can stop here but for most people, fine tuning can be beneficial. Re-run this command with the MIN value set slightly higher (+250) than the previous Optimal result and let it run again.
{% endhint %}

Now do a touch calibration with the new threshold.

```gcode
CARTOGRAPHER_CALIBRATE
```

If everything went correctly the touch test should pass and you can now finish by saving these variables to your config.

```gcode
SAVE_CONFIG                        
```

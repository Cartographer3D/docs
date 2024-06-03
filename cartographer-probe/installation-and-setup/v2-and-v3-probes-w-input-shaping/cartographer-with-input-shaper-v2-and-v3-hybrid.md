# Calibration

Home the machine in X and Y:

```
G28 X Y
```

Position the nozzle in the center of the bed. You will need to adjust the coordinates for your machine.

```
G0 X125 Y125
```

{% hint style="warning" %}
At this point,  you might note that your Endstop Z is TRIGGERED, this is normal, and will be resolved once you run the next command.

![](<../../../.gitbook/assets/image (6) (1).png>)
{% endhint %}

Start the calibration process:

{% hint style="info" %}
If you regularly print with a hot chamber (60oC+) it is worth calibrating with a hot chamber.
{% endhint %}

```
CARTOGRAPHER_CALIBRATE
```

You can either use the web interface to adjust the nozzle height from the bed, or `TESTZ Z=-0.01` to lower it. \
\
Use a piece of paper  or a feeler gauge to measure the offset. Once finished remove the paper/gauge and accept the position.

```
ACCEPT
```

Save the results to your config file.

```
SAVE_CONFIG
```

#### Initial Tests

Home your printer.&#x20;

```
G28
```

You can test the accuracy.

```
PROBE_ACCURACY
```

You can also measure the backlash of your Z axis

```
CARTOGRAPHER_ESTIMATE_BACKLASH
```

To make use of the backlash estimation that is given. You will get results spit out starting with &#x20;

```
Median distance moving up
```

In this line will be a measurement called "delta" Take note of the value. Locate the configuration section marked:

```
backlash_comp: 2.01
```

Update this section with your new estimated backlash compensation. It is a good idea to do this compensation test at all 4x corners of your build plate and then again at middle of build plate. If you are on a printer with belted Z and the values in each corner deviate heavily. This would indicate a loose belt on that corner.&#x20;

If youa re using a printer which supports either `Z_TILT` or `QUAD_GANTRY_LEVEL` you will need to ensure that your probe is positioned above the bed when performing this, open up your `printer.cfg` and find the appropriate section, for example your Z\_TILT section may look like this:



<pre class="language-yaml"><code class="lang-yaml">[quad_gantry_level]
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

```
BED_MESH_CALIBRATE
```

#### Setting Z Offset

Before modifying your Z Offset, make sure that you have set your Z position to 0, to do this you can run the following command.&#x20;

```
G1 Z0 F1500
```

Once you have done all of the above, it is worth re-calibrating the Z-Offset. This can be done in Mainsail or Fluidd using the graphical interface. \
\
OR you can use G-Code in the window to console to do so

```gcode
SET_GCODE_OFFSET Z_ADJUST=+0.01 MOVE=1
SET_GCODE_OFFSET Z_ADJUST=-0.01 MOVE=1
```

Once the offset has been perfectly calibrated apply that offset using the following command

```
Z_OFFSET_APPLY_PROBE
```

And now save your config.

{% hint style="warning" %}
If you are regularly changing your bed, please look at creating different models for your different beds, more information can be found [here ](../../fine-tuning/cartographer-models.md)
{% endhint %}

# Cartographer with Input Shaper (v2 & v3 hybrid)

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
If you are regularly changing your bed, please look at creating different models for your different beds, more information can be found [here ](../../advanced-features/cartographer-models.md)
{% endhint %}

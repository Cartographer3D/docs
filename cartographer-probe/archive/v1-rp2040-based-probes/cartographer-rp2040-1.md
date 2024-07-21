# Cartographer (rp2040)

Home the machine in X and Y:

```
G28 X Y
```

Position the nozzle in the center of the bed. You will need to adjust the coordinates for your machine.

```
G0 X125 Y125
```

Start the calibration process:

```
IDM_CALIBRATE
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
IDM_ESTIMATE_BACKLASH
```

You can now run a Bed Mesh Calibration (I would advise doing either a `Z_TILT` or `QUAD_GANTRY_LEVEL` before.

```
BED_MESH_CALIBRATE
```

Your Cartographer is now calibrated and ready to go.&#x20;

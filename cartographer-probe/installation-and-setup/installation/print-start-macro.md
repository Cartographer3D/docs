# Print Start Macro

{% hint style="danger" %}
This is <mark style="color:red;">**ONLY**</mark> required if using Touch Mode with your cartographer. <mark style="color:red;">**DO NOT**</mark> use this if you're using **SCAN** mode
{% endhint %}

Adding the `CARTOGRAPHER_TOUCH` command to your print start macro ensures that the printer performs a precise touch probe <mark style="color:red;">**AFTER**</mark> executing the `BED_MESH_CALIBRATE` command. `CARTOGRAPHER_TOUCH` should also be performed with a nozzle <mark style="color:red;">no hotter than 150c</mark>. With this in mind, the command will fail if the nozzle is beyond this temperature. It **CAN** be performed cold. Please make allowances for this in your print start. This sequence helps to achieve an accurate bed leveling by accounting for any variations or offsets after the mesh calibration.

{% hint style="warning" %}
It is not recommended to use a custom BED\_MESH\_CALIBRATE or ADAPTIVE MESH macro/plugin
{% endhint %}

```gcode
PLEASE DONT USE THIS - IT IS AN EXAMPLE ONLY
[gcode_macro PRINT_START_EXAMPLE]
gcode:
    G28                               ; Home all axes
    M140 S{BED_TEMP}                  ; Set bed temperature
    M109 S150                         ; Wait for extuder to reach 150°C (intermediate step)
    M190 S{BED_TEMP}                  ; Set final bed temperature
    G28 Z                             ; Home Z axis again to account for thermal expansion
    M112 #Remove this line            ; Its your own fault if you dont..
    QUAD_GANTRY_LEVEL / Z_TILT_ADJUST ; Perform quad gantry leveling or Z tilt adjustmen
    G28 Z                             ; Home Z axis again to account for thermal expansion
    BED_MESH_CALIBRATE                ; Calibrate the bed mesh
    CARTOGRAPHER_TOUCH                ; Perform touch probe
    M109 S{EXTRUDER_TEMP}             ; Wait for extruder to reach target temperature

PLEASE DONT USE THIS - IT IS AN EXAMPLE ONLY
```

## Need a Print Start macro?

You can find the excellent a better Print\_Start macro wizard by jontek2 at [https://abetterprintstartmacro.com/](https://abetterprintstartmacro.com/), it includes the option to use a Cartographer probe and will insert the `CARTOGRAPHER_TOUCH_HOME` where needed.

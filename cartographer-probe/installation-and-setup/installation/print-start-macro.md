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

The following is a modified version of [Jontek2's Better Print Start Macro](https://github.com/jontek2/A-better-print_start-macro) which incorporates Cartographer\_Touch commands for use with Voron printers and can be adapted for others.

```gcode
#####################################################################
#   A better print_start macro for v2/trident
#####################################################################

## *** THINGS TO UNCOMMENT: ***
## Bed mesh (2 lines at 2 locations)
## Nevermore (if you have one)
## Z_TILT_ADJUST (For Trident only)
## QUAD_GANTRY_LEVEL (For V2.4 only)

[gcode_macro PRINT_START]
gcode:
  # This part fetches data from your slicer. Such as bed, extruder, and chamber temps and size of your printer.
  {% raw %}
{% set target_bed = params.BED|int %}
  {% set target_extruder = params.EXTRUDER|int %}
  {% set target_chamber = params.CHAMBER|default("45")|int %}
  {% set x_wait = printer.toolhead.axis_maximum.x|float / 2 %}
  {% set y_wait = printer.toolhead.axis_maximum.y|float / 2 %}

  SET_GCODE_OFFSET Z=0                                 # Set offset to 0

  # Home the printer, set absolute positioning and update the Stealthburner LEDs.
  STATUS_HOMING                                         # Set LEDs to homing-mode
  G28                                                   # Full home (XYZ)
  G90                                                   # Absolute position

  ##  Uncomment for bed mesh (1 of 2 for bed mesh)
  #BED_MESH_CLEAR                                       # Clear old saved bed mesh (if any)

  # Check if the bed temp is higher than 90c - if so then trigger a heatsoak.
  {% if params.BED|int > 90 %}
    SET_DISPLAY_TEXT MSG="Bed: {target_bed}c"           # Display info on display
    STATUS_HEATING                                      # Set LEDs to heating-mode
    M106 S255                                           # Turn on the PT-fan

    ##  Uncomment if you have a Nevermore.
    #SET_PIN PIN=nevermore VALUE=1                      # Turn on the nevermore

    G1 X{x_wait} Y{y_wait} Z15 F9000                    # Go to center of the bed
    M190 S{target_bed}                                  # Set the target temp for the bed
    SET_DISPLAY_TEXT MSG="Heatsoak: {target_chamber}c"  # Display info on display
    TEMPERATURE_WAIT SENSOR="temperature_sensor chamber" MINIMUM={target_chamber}   # Waits for chamber temp

  # If the bed temp is not over 90c, then skip the heatsoak and just heat up to set temp with a 5 min soak
  {% else %}
    SET_DISPLAY_TEXT MSG="Bed: {target_bed}c"           # Display info on display
    STATUS_HEATING                                      # Set LEDs to heating-mode
    G1 X{x_wait} Y{y_wait} Z15 F9000                    # Go to center of the bed
    M190 S{target_bed}                                  # Set the target temp for the bed
    SET_DISPLAY_TEXT MSG="Soak for 5 min"               # Display info on display
    G4 P300000                                          # Wait 5 min for the bedtemp to stabilize
  {% endif %}
{% endraw %}

  # Heat hotend to 150c. This helps with getting a correct Z-home.
  SET_DISPLAY_TEXT MSG="Hotend: 150c"                   # Display info on display
  M109 S150                                             # Heat hotend to 150c

  ##  Uncomment for Trident (Z_TILT_ADJUST)
  #SET_DISPLAY_TEXT MSG="Leveling"                      # Display info on display
  #STATUS_LEVELING                                      # Set LEDs to leveling-mode
  #Z_TILT_ADJUST                                        # Level the printer via Z_TILT_ADJUST
  #G28 Z                                                # Home Z again after Z_TILT_ADJUST

  ##  Uncomment for V2.4 (Quad gantry level AKA QGL)
  #SET_DISPLAY_TEXT MSG="Leveling"                      # Display info on display
  #STATUS_LEVELING                                      # Set LEDs to leveling-mode
  #QUAD_GANTRY_LEVEL                                    # Level the printer via QGL
  #G28 Z                                                # Home Z again after QGL

  ##  Uncomment for bed mesh (2 of 2 for bed mesh)
  SET_DISPLAY_TEXT MSG="Bed mesh"                      # Display info on display
  STATUS_MESHING                                       # Set LEDs to bed mesh-mode
  BED_MESH_CALIBRATE                                   # Start the bed mesh (add ADAPTIVE=1) for adaptive bed mesh

  CARTOGRAPHER_TOUCH                                    # Calibrate z offset only with hot nozzle

  # Heat up the hotend up to target via data from slicer
  SET_DISPLAY_TEXT MSG="Hotend: {target_extruder}c"     # Display info on display
  STATUS_HEATING                                        # Set LEDs to heating-mode
  G1 X{x_wait} Y{y_wait} Z15 F9000                      # Go to center of the bed
  M107                                                  # Turn off partcooling fan
  M109 S{target_extruder}                               # Heat the hotend to set temp

  # Get ready to print by doing a primeline and updating the LEDs
  SET_DISPLAY_TEXT MSG="Printer goes brr"               # Display info on display
  STATUS_PRINTING                                       # Set LEDs to printing-mode
  G0 X{x_wait - 50} Y4 F10000                           # Go to starting point
  G0 Z0.4                                               # Raise Z to 0.4
  G91                                                   # Incremental positioning 
  G1 X100 E20 F1000                                     # Primeline
  G90                                                   # Absolute position
```


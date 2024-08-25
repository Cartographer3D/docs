# Klipper Configuration

{% hint style="info" %}
If you want to use Survey Touch, our contact probing solution skip this section and go [here](../survey-touch/)
{% endhint %}

## Finding the Serial or UUID

{% hint style="warning" %}
A small number of probes which shipped directly from Cartographer3D between mid and late February may have been pre-flashed with the incorrect firmware. If you cannot find a serial number or UUID, please follow this [guide on how to re-flash](../firmware/manual-methods/re-flashing-firmware.md) with the correct firmware. \
\
We are sorry for any inconvenience caused.&#x20;
{% endhint %}

Note, you need to replace the serial path  or UUID with your probes serial path or UUID, this can be found by running the following commands&#x20;

For USB based probes&#x20;

```bash
ls /dev/serial/by-id/
```

For CAN based probes

```bash
~/klippy-env/bin/python ~/klipper/scripts/canbus_query.py can0
```

## Config File&#x20;

{% hint style="danger" %}
if you are using an existing printer config, make sure you remove any previous reference to `[cartographer]` or `[probe]` in the saved section at the bottom.&#x20;
{% endhint %}

```yaml
[cartographer]
serial:
#   Path to the serial port for the Cartographer device. Typically has the form
#   /dev/serial/by-id/usb-cartographer_cartographer_...
#   
#   If you are using the CAN Bus version, replace serial: with canbus_uuid: and add the UUID.
#   Example: canbus_uuid: 1283as878a9sd
#
speed: 40.
#   Z probing dive speed.
lift_speed: 5.0
#   Z probing lift speed.
backlash_comp: 0.5
#   Backlash compensation distance for removing Z backlash before measuring
#   the sensor response.
# 
#   Offsets are measured from the centre of your coil, to the tip of your nozzle 
#   on a level axis. It is vital that this is accurate. 
#
x_offset: 0.0
#   X offset of cartographer from the nozzle.
y_offset: 21.1
#   Y offset of cartographer from the nozzle.
trigger_distance: 2.0
#   cartographer trigger distance for homing.
trigger_dive_threshold: 1.5
#   Threshold for range vs dive mode probing. Beyond `trigger_distance +
#   trigger_dive_threshold` a dive will be used.
trigger_hysteresis: 0.006
#   Hysteresis on trigger threshold for untriggering, as a percentage of the
#   trigger threshold.
cal_nozzle_z: 0.1
#   Expected nozzle offset after completing manual Z offset calibration.
cal_floor: 0.1
#   Minimum z bound on sensor response measurement.
cal_ceil: 5.0
#   Maximum z bound on sensor response measurement.
cal_speed: 1.0
#   Speed while measuring response curve.
cal_move_speed: 10.0
#   Speed while moving to position for response curve measurement.
default_model_name: default
#   Name of default cartographer model to load.
mesh_main_direction: x
#   Primary travel direction during mesh measurement.
#mesh_overscan: -1
#   Distance to use for direction changes at mesh line ends. Omit this setting
#   and a default will be calculated from line spacing and available travel.
mesh_cluster_size: 1
#   Radius of mesh grid point clusters.
mesh_runs: 2
#   Number of passes to make during mesh scan.
```

{% hint style="warning" %}
NOTE - The \[cartographer] section needs to be above any other reference to either cartographer or probe within your Klipper config, for this reason I advise adding it near the top of your config file.&#x20;
{% endhint %}

If you want to use the probe for Input Shaper, please add the following to your config.

{% tabs %}
{% tab title="adxl345 based probes" %}
```yaml
[adxl345]
cs_pin: cartographer:PA3
spi_bus: spi1

[resonance_tester]
accel_chip: adxl345
probe_points:
    125, 125, 20
```
{% endtab %}

{% tab title="lis2dw based probes" %}
```yaml
[lis2dw]
cs_pin: cartographer:PA3
spi_bus: spi1

[resonance_tester]
accel_chip: lis2dw
probe_points:
    125, 125, 20
```
{% endtab %}
{% endtabs %}

You then need to remove, or comment out your `[probe]` section.

Now add a safe\_z\_home section with the following inforamation.

```yaml
[safe_z_home]
home_xy_position: [your x-axis center coordinate], [your y-axis center coordinate]
# Example home_xy_position: 175,175 - This would be for a 350 * 350mm bed. 
z_hop: 10
```

You will also need to update your Z configuration settings, this will involve removing or commenting out your `position_endstop:` configuration.&#x20;

```yaml
[stepper_z]
endstop_pin: probe:z_virtual_endstop # use cartographer as virtual endstop
homing_retract_dist: 0 # cartographer needs this to be set to 0
```

If you are running Klipper Screen, add this Macro to your G-Code, this stops klipper screen doing a random bedmesh when you press Z Calibrate on it. &#x20;

```gcode
[gcode_macro PROBE_CALIBRATE]
gcode:
    CARTOGRAPHER_CALIBRATE
```

{% hint style="danger" %}
You will now need to ensure that you update your Z-Tilt or QGL settings to ensure that Cartographer is over the bed when performing these actions.  We will be checking these during the calibration phase.&#x20;
{% endhint %}

Finally, you need to ensure you have a suitable `bed_mesh` section. Information can be found [here](https://www.klipper3d.org/Bed\_Mesh.html)



{% hint style="warning" %}
It is vital you complete the Calibration steps, without doing so the probe will not work properly and is likely to show TRIGGERED.&#x20;
{% endhint %}




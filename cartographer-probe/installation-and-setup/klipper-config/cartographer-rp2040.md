# Cartographer (rp2040)

Add the following configuration to the top of your Printer.cfg file. Note, you need to replace the serial path with your probes serial path, this can be found by running the following command. `ls /dev/serial/by-id/`

```yaml
[idm]
serial:
#   Path to the serial port for the idm device. Typically has the form
#   /dev/serial/by-id/usb-idm_idm_...
speed: 40.
#   Z probing dive speed.
lift_speed: 5.
#   Z probing lift speed.
backlash_comp: 0.5
#   Backlash compensation distance for removing Z backlash before measuring
#   the sensor response.
x_offset: 0.
#   X offset of idm from the nozzle.
y_offset: 21.1
#   Y offset of idm from the nozzle.
trigger_distance: 2.
#   idm trigger distance for homing.
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
cal_ceil:5.
#   Maximum z bound on sensor response measurement.
cal_speed: 1.0
#   Speed while measuring response curve.
cal_move_speed: 10.
#   Speed while moving to position for response curve measurement.
default_model_name: default
#   Name of default idm model to load.
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

You then need to remove, or comment out your `[probe]` section.

Now add a safe\_z\_home section with the following inforamation.

```yaml
[safe_z_home]
home_xy_position: [your x-axis center coordinate], [your y-axis center coordinate]
# Example home_xy_position: 175,175 - This would be for a 350 * 350mm bed. 
z_hop: 10
```

You will also need to update your Z configuration settings.

```yaml
[stepper_z]
endstop_pin: probe:z_virtual_endstop # use cartographer as virtual endstop
homing_retract_dist: 0 # cartographer needs this to be set to 0
```

Finally, you need to ensure you have a suitable `bed_mesh` section. Information can be found [here](https://www.klipper3d.org/Bed\_Mesh.html)

{% hint style="warning" %}
It is vital you complete the Calibration steps, without doing so the probe will not work properly and is likely to show TRIGGERED.&#x20;
{% endhint %}

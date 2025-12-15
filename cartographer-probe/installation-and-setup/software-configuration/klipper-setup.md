---
description: Quick overview of the steps needed to setup the Cartographer3D Klipper plugin
---

# Klipper Setup

{% hint style="danger" %}
If you are updating to the NEW Cartographer plugin, then it is necessary to remove parts of your old config to avoid Klipper errors. **Therefore it is recommend to back-up your config to reference later.**
{% endhint %}

It is necessary to remove all instances of \[scanner] from your printer.cfg, this INCLUDES any from the SAVE\_CONFIG section at the bottom of the printer.cfg. Once you have done this save the file and you will return to the file directory.

Now open the moonraker.conf file, here you want to remove the old Cartographer Plugin update section, you added when you installed the old plugin.

Once you save and restart you will get a Klipper error for Unkown Pin Probe, this is normal and you can proceed to installation of the Klipper plugin below.

## Installation Klipper plugin

A script has been made to simplify the process of installing the plugin.

The defaults assumes that klipper is in `~/klipper` and the klippy-env is in `~/klippy-env`.\
This should be standard on [KIAUH](https://github.com/dw-0/kiauh) and [MainsailOS](https://docs-os.mainsail.xyz/).

Run this command to install, customizing the paths if needed.

{% code overflow="wrap" %}
```sh
curl -s -L https://raw.githubusercontent.com/Cartographer3D/cartographer3d-plugin/refs/heads/main/scripts/install.sh | bash -s -- --klipper ~/klipper --klippy-env ~/klippy-env
```
{% endcode %}

## Configure Moonraker Update Manager

```yaml
[update_manager cartographer_plugin]
type: python
channel: stable
virtualenv: ~/klippy-env
project_name: cartographer3d-plugin
is_system_service: False
managed_services: klipper
info_tags: desc=Cartographer Plugin
```

## Configure Klipper

Below are the minimum, required, options listed. Except for the `temperature_sensor` blocks, you can omit those if you don't want to monitor temperature.

You will need to adjust this config for your printer and your probe, this is done by modifying the sections labeled \`\<blank>\`

{% hint style="warning" %}
We recommend configuring [safe\_z\_home](https://www.klipper3d.org/Config_Reference.html#safe_z_home).
{% endhint %}

```yaml
[stepper_z]
endstop_pin: probe:z_virtual_endstop
homing_retract_dist: 0

[mcu cartographer] # See https://www.klipper3d.org/Config_Reference.html#mcu
# Remove either the serial or canbus_uuid line dependant on your setup.
serial: <blank>
canbus_uuid: <blank>
restart_method: command # Not needed for probes using CAN. 

[cartographer]
mcu: cartographer
x_offset: <blank> # This is the offset of your probe from the nozzle tip, to the centre of the coil.
y_offset: <blank> # This is the offset of your probe from the nozzle tip, to the centre of the coil.
verbose: yes # For extra output

[bed_mesh]
zero_reference_position: <blank>, <blank> # The centre of your bed. 
speed: 300
horizontal_move_z: 3
mesh_min: <blank>, <blank> # The first probed coordinate, nearest to the origin. This coordinate is relative to the probe's location.
mesh_max: <blank>, <blank> # The probed coordinate farthest from the origin. This is not necessarily the last point probed, as the probing process occurs in a zig-zag fashion. As with mesh_min, this coordinate is relative to the probe's location.
probe_count: 20, 20
adaptive_margin: 10
mesh_pps: 0,0 # Disable interpolation - mesh is probably dense enough

[temperature_sensor cartographer]
sensor_type: temperature_mcu
sensor_mcu: cartographer
min_temp: 5
max_temp: 105

[adxl345]
# Select 1 of the cs_pin below depending on the probe you have. 
# Having the wrong one selected will cause an Endless Bootloop
cs_pin: cartographer:PA3 # For Cartographer V3
cs_pin: cartographer:PA0 # For Cartographer V4
spi_bus: spi1

[resonance_tester]
accel_chip: adxl345
probe_points:
    <blank>, <blank>, 20 # Fill out the blank with x and y coordinates where you want to run the resonance test.
```

## Calibration

Cartographer provides two methods of homing.\
We recommend always using the default scan method for general homing and using `CARTOGRAPHER_TOUCH_HOME` after all leveling has been done, just before your print starts.

Continue with [scan-calibration.md](scan-calibration.md "mention") and [touch-calibration.md](touch-calibration.md "mention").

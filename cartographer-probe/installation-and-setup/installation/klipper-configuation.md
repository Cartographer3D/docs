---
description: Klipper Configuration for Touch Mode
---

# Klipper Configuation

<mark style="color:purple;">Last Updated: December 11th 2024</mark>

{% hint style="warning" %}
We **DO NOT** 100% guarantee TOUCH compatibility with ALL printers. It is your responsibility to read this entire guide prior to use and to research whether this is right for you. Please contact us on [DISCORD ](https://discord.gg/yzazQMEGS2)if you have questions.
{% endhint %}

{% hint style="info" %}
If you're changing from classic to touch, make sure you remove or comment out \[cartographer] sections from your existing klipper configuration files.\
\
[A note about this can be found here.](../../troubleshooting.md#command-mismatch)
{% endhint %}

For Cartographer to receive usable readings for touch to be accurate, you **MUST** place cartographer between <mark style="color:red;">**2.6 and 3mm ABOVE**</mark> the nozzle. Print or put something 2.5-2.6mm but no more than 3mm in height under or next to the cartographer coil to measure where it needs to be.

\
Your toolhead & gantry/carriage **MUST** be <mark style="color:red;">**RIGID**</mark>. If there is movement and flex it can also create undesired results in the touch process.

<pre class="language-yaml"><code class="lang-yaml">[mcu scanner]
canbus_uuid: 0ca8d67388c2 
<strong>#serial: /dev/serial/by-id/usb-cartographer_cartographer_
</strong>#    adjust to suit your scanner, if using usb change to serial

[scanner]
mcu: scanner            
#   Offsets are measured from the centre of your coil, to the tip of your nozzle 
#   on a level axis. It is vital that this is accurate. 
x_offset: 0                          
#    adjust for your cartographers offset from nozzle to middle of coil
y_offset: 15                         
#    adjust for your cartographers offset from nozzle to middle of coil
backlash_comp: 0.5
#   Backlash compensation distance for removing Z backlash before measuring
#   the sensor response.
sensor: cartographer
#    this must be set as cartographer unless using IDM etc.
sensor_alt: carto
#    alternate name to call commands. CARTO_TOUCH etc      
mesh_runs: 2
#    Number of passes to make during mesh scan.

[bed_mesh]
zero_reference_position: 125, 125    
#    set this to the middle of your bed
speed: 200
#    movement speed of toolhead during bed mesh
horizontal_move_z: 5
#    height of scanner during bed mesh scan
mesh_min: 35, 6
#    start point of bed mesh [X, Y]
mesh_max: 240, 198
#    end point of bed mesh [X, Y]
probe_count: 30, 30
algorithm: bicubic

[temperature_sensor Cartographer_MCU]
sensor_type: temperature_mcu
sensor_mcu: scanner
min_temp: 0
max_temp: 105

</code></pre>

{% hint style="warning" %}
NOTE - The \[scanner] section needs to be above any other reference to either cartographer/scanner or probe within your Klipper config, for this reason I advise adding it near the top of your config file.&#x20;
{% endhint %}

If you want to use the probe for Input Shaper, please add the following to your config.

{% hint style="info" %}
By default the `[adxl345]` and `[lis2dw]` sections are commented out. This is so you don't encounter errors if you already have these sections in your config.\
\
You can add them and use them by switching them for existing sections however <mark style="color:red;">**DO NOT**</mark> combine them!
{% endhint %}

{% tabs %}
{% tab title="adxl345 based probes" %}
```yaml
#[adxl345]
#cs_pin: scanner:PA3
#spi_bus: spi1

#[resonance_tester]
#accel_chip: adxl345
#probe_points:
#    125, 125, 20
```
{% endtab %}

{% tab title="lis2dw based probes" %}
```yaml
#[lis2dw]
#cs_pin: scanner:PA3
#spi_bus: spi1

#[resonance_tester]
#accel_chip: lis2dw
#probe_points:
#    125, 125, 20
```
{% endtab %}
{% endtabs %}

You then need to remove, or comment out your `[probe]` section.

Now add a safe\_z\_home section with the following information.

```yaml
[safe_z_home]
home_xy_position: [your x-axis center coordinate], [your y-axis center coordinate]
# Example home_xy_position: 175,175 - This would be for a 350 * 350mm bed. 
z_hop: 10
```

You will also need to update your Z configuration settings, this will involve removing or commenting out your `position_endstop:` configuration. `Homing_retract_dist`  must also be set to 0

{% hint style="info" %}
Don't get confused, "endstop\_pin" should contain probe and NOT cartographer/scanner.
{% endhint %}

```yaml
[stepper_z]
endstop_pin: probe:z_virtual_endstop # uses cartographer as virtual endstop
homing_retract_dist: 0 # cartographer needs this to be set to 0
#position_endstop: 5 # cartographer needs this to be commented out
```

{% hint style="danger" %}
You will now need to ensure that you update your Z-Tilt or QGL settings to ensure that Cartographer is over the bed when performing these actions.  We will be checking these during the calibration phase.&#x20;
{% endhint %}

Finally, you need to ensure you have a suitable `bed_mesh` section. Information can be found [here](https://www.klipper3d.org/Bed_Mesh.html)

{% hint style="warning" %}
It is vital you complete the Calibration steps, without doing so the probe will not work properly and is likely to show TRIGGERED.&#x20;
{% endhint %}


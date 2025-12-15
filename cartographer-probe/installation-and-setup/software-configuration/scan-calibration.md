---
description: Go through calibration of your Cartographer
---

# Scan Calibration

{% hint style="danger" %}
## Verify zero reference position!



Ensure that your `zero_reference_position` is set to a sensible value, usually the middle of your bed.

Verify this by issuing the `G0 X<blank> Y<blank>` command with the values from your configuration.

```
[bed_mesh]
zero_reference_position: <blank>, <blank>        
```
{% endhint %}

## Scan calibration

{% stepper %}
{% step %}
### Home your printer's X and Y axes

```
G28 X Y
```
{% endstep %}

{% step %}
### Start calibration

This will move your toolhead to the zero reference position and start calibration

<pre><code><strong>CARTOGRAPHER_SCAN_CALIBRATE
</strong></code></pre>
{% endstep %}

{% step %}
### Move nozzle to 0.1mm above the bed

Use the `TESTZ Z=-0.01` macro to slowly lower your nozzle. Use `ABORT` if you wish to abort.

{% hint style="info" %}
You can use Mainsail or Fluidd to have a nice interface to support you during these moves.
{% endhint %}

We want to get our nozzle to as close to 0.1mm off the bed as we can. You can use a feeler gauge or a piece of paper, simply stop once it catches.

{% hint style="warning" %}
Visually ensure that there is still a gap between your nozzle and the bed.
{% endhint %}

```
TESTZ Z=-0.01
```
{% endstep %}

{% step %}
### Accept manual homing

Now press accept, or run the `ACCEPT` macro to continue calibration. The nozzle will move up above the bed and slowly lower while recording the frequency response. Make sure the printer is _stable_ and do not touch the bed or gantry.

```
ACCEPT
```
{% endstep %}

{% step %}
### Save the calibrated model

Once done, you will be prompted to run `SAVE_CONFIG`. The Klipper firmware should restart and you will be able to home using `G28`.

```
SAVE_CONFIG
```
{% endstep %}

{% step %}
### Next Steps (Touch Calibration)

You have now created a model for all of the scan operations (`G28`, `BED_MESH_CALIBRATE`, `Z_TILT_ADJUST` / `QUAD_GANTRY_LEVEL` etc) to use the physical touch commands, you will now need to calibrate touch, please move to the next page.&#x20;
{% endstep %}
{% endstepper %}

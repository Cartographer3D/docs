# Touch calibration

{% hint style="warning" %}
This calibration will enable Survey Touch macros. A misconfigured touch model or printer can cause physical damage to your printer. It is _important_ that you verify that everything is rigid, that all bolts are tightened. This should be checked frequently.
{% endhint %}

{% hint style="danger" %}
## Verify zero reference position!

Ensure that your `zero_reference_position` is set to a sensible value, usually the middle of your bed.

Verify this by issuing the `G0 X<blank> Y<blank>` command with the values from your configuration.

```
[bed_mesh]
zero_reference_position: <blank>, <blank>
```
{% endhint %}

{% hint style="info" %}
You _can_ calibrate Survey Touch without homing Z. This means we can calibrate Survey Touch first and then use `CARTOGRAPHER_SCAN_CALIBRATE METHOD=touch` to skip the manual adjustments _and_ get a more precise scan model.
{% endhint %}

{% stepper %}
{% step %}
### Home your printer's X and Y axes

```
G28 X Y
```
{% endstep %}

{% step %}
### Prepare to run touch calibration

{% hint style="warning" %}
**Ensure that your nozzle and bed is clean.**

**Ensure that your probe is between 2.6mm and 3mm above the nozzle.**

**Double check that your gantry and kinematics are rigid.**

**It is helpful to have a level bed.** Prefer running `QUAD_GANTRY_LEVEL` or `Z_TILT_ADJUST` if possible. This would usually require scan being calibrated.
{% endhint %}
{% endstep %}

{% step %}
### Start calibration routine

{% hint style="danger" %}
Keep your finger on the emergency stop button in case it does not stop at your bed.
{% endhint %}

Start the calibration by running

{% code fullWidth="false" %}
```
CARTOGRAPHER_TOUCH_CALIBRATE
```
{% endcode %}

Observe your nozzle to make sure it touches on the bed.

If it never touches the bed, refer to [#nozzle-never-touches-the-bed](touch-calibration.md#nozzle-never-touches-the-bed "mention")
{% endstep %}

{% step %}
### Save the calibrated model

Once done, you will be prompted to run `SAVE_CONFIG`. The Klipper firmware should restart and you will be able to use `CARTOGRAPHER_TOUCH_*`.

```
SAVE_CONFIG
```
{% endstep %}
{% endstepper %}

### Troubleshooting

#### Nozzle never touches the bed

You should ensure that your Z motion is smooth and clean. Gunk and noise that is not evident while moving up and down may be detected by Cartographer and make it believe it touched the bed. After checking everything, run `CARTOGRAPHER_TOUCH_CALIBRATE` again.&#x20;

If it is still a problem, you can pass in a `START` parameter. `CARTOGRAPHER_TOUCH_CALIBRATE START=123` where 123 is above the threshold it previously stopped at.\
If it stops without ever touching the bed and never finds a threshold you can increase the max threshold with the `MAX` parameter, `CARTOGRAPHER_TOUCH_CALIBRATE MAX=5000`.

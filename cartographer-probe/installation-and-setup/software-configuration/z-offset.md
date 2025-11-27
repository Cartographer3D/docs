# Z Offset

{% hint style="info" %}
If you are using `CARTOGRAPHER_TOUCH_HOME`, you shouldn't have to care about your scan offset. Everything that scan is used for, is relative to itself and the Z-offset is a constant that is applied to every measurement. Thus it _only_ has an impact, if you start printing without using `CARTOGRAPHER_TOUCH_HOME`.
{% endhint %}

We implement Klipper's `Z_OFFSET_APPLY_PROBE` , this will apply the offset to the _last_ homed mode used. This means if the last mode you used was `G28`, it will apply the offset to your scan model. If the last mode you used was `CARTOGRAPHER_TOUCH_HOME` it will apply to your touch model.&#x20;

### Babystep adjusting Z offset

We recommend you follow [Ellis' Print Tuning Guide](https://ellis3dp.com/Print-Tuning-Guide/articles/first_layer_squish.html).

This is easiest to do through Mainsail or Fluidd. These will show a button to adjust your z offset "live", during a print. You must use the save icon that appears next to the adjustment controls AS WELL as a SAVE\_CONFIG.

Short version is to run the following macros to adjust gcode while printing a bunch of first layer squares, until you achieve the perfect first layer.

To move **up**, use `SET_GCODE_OFFSET Z_ADJUST=+0.01 MOVE=1`

To move **down**, use `SET_GCODE_OFFSET Z_ADJUST=-0.01 MOVE=1`&#x20;

To finalize, use `Z_OFFSET_APPLY_PROBE`, you can then see what changed

> cartographer: touch default z\_offset: -0.1

Remember to run `SAVE_CONFIG` to persist the change to your configuration.

{% hint style="info" %}
A smaller number means a larger distance between the bed and the nozzle. This can seem counterintuitive, but this is to keep it in line with Klipper's virtual probe, and makes sense from a technical point of view.

The user should never change the number manually in the config, as that can risk causing issues.
{% endhint %}

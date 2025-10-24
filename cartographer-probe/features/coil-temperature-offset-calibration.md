---
icon: temperature-low
---

# Coil Temperature Offset Calibration

{% hint style="info" %}
This calibration is not necessary when using [Broken link](broken-reference "mention")
{% endhint %}

This calibration aims to optimize the temperature compensation parameters and reduce the temperature drift of the coil.

It usually takes **between one and three hours** to gather the necessary samples. It can take longer.

During this calibration, your bed will heat up and move close to the nozzle, it will stay in still until the coil has reached target temperature. The bed will then lower to a cooling position and your part cooling fan will turn on to assist in cooling the coil.

We recommend tuning the parameters to fit your printer, as that will allow the calibration to complete faster. A bed temperature of 110 or above is usually required to reach a coil temperature of 70.

{% hint style="info" %}
Your hotend cooling fan may start during this process. This may impact the ability to heat your coil.\
If possible, please adjust the trigger for the hotend cooling fan to keep it off during this calibration.

```
[heater_fan hotend_fan]
heater: extruder
heater_temp: 100
# Increase this, remember to revert!
```
{% endhint %}

Home your printer using `G28` then start the macro by executing the below, changing the parameters to fit your setup.

```
CARTOGRAPHER_TEMPERATURE_CALIBRATE MIN_TEMP=40 MAX_TEMP=<60|70> BED_TEMP=<90|110> Z_SPEED=5
```

Wait for the calibration to complete. It will inform you that calibration is complete and that you should `SAVE_CONFIG` to save the model to your config.

{% hint style="info" %}
If you changed your `hotend_fan` configuration, remember to revert this _after_ saving the calibration!
{% endhint %}

{% hint style="info" %}
It would be amazing if you can grab the raw data files that are written during the calibration sequence and upload them to the dedicated Discord channel [https://discord.com/channels/1165274913624572014/1421909399286448350](https://discord.com/channels/1165274913624572014/1421909399286448350)\
This will help us gather data and improve further calibrations and features!
{% endhint %}

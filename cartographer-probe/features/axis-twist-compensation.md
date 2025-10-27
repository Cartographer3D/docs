---
icon: chart-scatter-3d
---

# Axis Twist Compensation

\


{% hint style="warning" %}
This requires Scan Calibration AND Touch Calibration&#x20;
{% endhint %}



We can automate axis twist compensation calibration using touch to get the nozzle offset. Simply run `CARTOGRAPHER_AXIS_TWIST_COMPENSATION` and let Cartographer do the rest. Remember to run `SAVE_CONFIG` to persist the change.

You MUST ensure that your Twist Axis is within your probe boundaries.\


{% hint style="success" %}
You can pass an axis to compensate along both axes, using `AXIS=Y`.
{% endhint %}

{% hint style="success" %}
If your axis twist is dependent on chamber temperature, you can run `CARTOGRAPHER_AXIS_TWIST_COMPENSATION` as part of your start print macro. \
\
Just remember to run it _after_ leveling your bed and _before_ bed mesh calibrate.
{% endhint %}



**Unknown command "CARTOGRAPHER\_AXIS\_TWIST\_COMPENSATION"**

You will need to enable the `axis_twist_compensation` function by adding the below section in your printer config. For [Klipper](https://www.klipper3d.org/Config_Reference.html?h=axis_#axis_twist_compensation) it can be empty, for [Kalico](https://docs.kalico.gg/Config_Reference.html#axis_twist_compensation) you need to define some fields.\[axis\_twist\_compensation]​\

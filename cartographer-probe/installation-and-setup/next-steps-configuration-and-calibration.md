# Next Steps - Configuration and Calibration

## Finding the Serial or UUID

Note, you need to replace the serial path  or UUID with your probes serial path or UUID, this can be found by running the following commands&#x20;

For USB based probes&#x20;

```bash
ls /dev/serial/by-id/
```

For CAN based probes

```bash
~/klippy-env/bin/python ~/klipper/scripts/canbus_query.py can0
```

Take note of either the Serial ID or the UUID.&#x20;

## New Firmware

Since late August, most probes shipping from directly from Cartographer3D, and a majority of our resellers have pre-flashed with the Cartographer Survey Firmware.&#x20;

If your box or antistatic bag states "Survey Touch Ready", please go here

{% content-ref url="../survey-touch/" %}
[survey-touch](../survey-touch/)
{% endcontent-ref %}

If it doesnt, don't worry. You can update your probe using our flashing tool. If you want to configure it as is,  please go to the next page.

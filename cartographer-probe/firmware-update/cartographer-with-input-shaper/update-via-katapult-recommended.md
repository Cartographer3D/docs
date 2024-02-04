# Update via Katapult (recommended)

Your probe will come pre-flashed with Katapult (formally CanBoot), this is on both the USB, CAN and Hybrid USB/CAN Probes.&#x20;

I advise only flashing via Katapult when using a probe in CAN mode, as DFU Mode or STLink are both easier and more reliable methods for flashing USB Probes. &#x20;

### Firmware

The best place to get the probes firmware is from our  [GitHub](https://github.com/Cartographer3D/cartographer-klipper/tree/master/firmware). These have been tested thoroughly, and are known to work perfectly.&#x20;

You can also build your own firmware, our GitHub organisation has both a custom build of [Klipper](../../../) and [Katapult](https://github.com/Cartographer3D/katapult) that you can build yourself.&#x20;

{% hint style="danger" %}
Untested Firmware could brick your probe - it is advisable if this is the case, you have a STLink handy in order to easily re-flash the probe.
{% endhint %}

The files labelled 'Katapult' are the bootloader, NOT the firmware themselves. Use the firmware labelled \`Cartographer\`

### CAN

Updating via Katapult and CAN is super easy, all you need is to know your probes UUID (available in your Klippers printer.cfg and which firmware you need to flash.&#x20;

SSH into your printer, and navigate to the folder where the firmware you want to flash is located and run the following command replacing `<firmware.bin>` with the fimware  file name and `<uuid>` with your probes UUID.&#x20;

```
python3 ~/katapult/scripts/flash_can.py -i can0 -f <firmware.bin> -u <myuuid>
```

Example of fully structured command.&#x20;

```
python3 ~/katapult/scripts/flash_can.py -i can0 -f Cartographer_CAN_1000000_8kib_offset.bin -u 389sc3889snc
```


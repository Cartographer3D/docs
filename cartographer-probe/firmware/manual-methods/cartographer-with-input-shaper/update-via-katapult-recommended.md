# Update via Katapult (recommended)

Your probe will come pre-flashed with Katapult (formally CanBoot), this is on both the USB, CAN and Hybrid USB/CAN Probes.&#x20;

### Firmware

The best place to get the probes firmware is from our [GitHub](https://github.com/Cartographer3D/cartographer-klipper/tree/master/firmware). These have been tested thoroughly, and are known to work perfectly.&#x20;

You can also build your own firmware, our GitHub organisation has both a custom build of [Klipper](../../../../) and [Katapult](https://github.com/Cartographer3D/katapult) that you can build yourself.&#x20;

{% hint style="danger" %}
Untested Firmware could brick your probe - it is advisable if this is the case, you have a STLink handy in order to easily re-flash the probe.
{% endhint %}

The files labelled 'Katapult' are the bootloader, NOT the firmware themselves. Use the firmware labelled \`Cartographer\`

### Updating a CAN probe via Katapult

Updating via Katapult and CAN is super easy, all you need is to know your probes UUID (available in your Klippers printer.cfg and which firmware you need to flash.&#x20;

SSH into your printer, and navigate to the folder where the firmware you want to flash is located and run the following command replacing `<firmware.bin>` with the fimware  file name and `<uuid>` with your probes UUID.&#x20;

{% hint style="danger" %}
CHECK THE FIRMWARE YOU ARE FLASHING IS THE CORRECT FIRMWARE.\
\
<mark style="color:red;">Any firmware labelled Katapult, or Full CANNOT be flashed using this method.</mark>&#x20;
{% endhint %}

```
python3 ~/katapult/scripts/flash_can.py -i can0 -f <firmware.bin> -u <myuuid>
```

Example of fully structured command.&#x20;

```
python3 ~/katapult/scripts/flash_can.py -i can0 -f Cartographer_CAN_1000000_8kib_offset.bin -u 379702c36ad1
```

Klipper will then require a Firmware restart, and if you did it correctly it will all work.&#x20;

<figure><img src="../../../../.gitbook/assets/image (17).png" alt=""><figcaption><p>Example of full process of Firmware Update</p></figcaption></figure>

### Updating a USB Probe via Katapult

Updating via USB is just as easy, just requires a couple more steps.&#x20;

The initial step is noting down the probes Serial ID, you do this by typing the following command

```
ls -l /dev/serial/by-id/
```

<figure><img src="../../../../.gitbook/assets/image (10) (1).png" alt=""><figcaption></figcaption></figure>

You now need to load the probe into the Katapult bootloader, to do this you simply replace \<serialID> with your own serial ID and path  as found in the above step.

```
cd ~/klipper/scripts
~/klippy-env/bin/python -c 'import flash_usb as u; u.enter_bootloader("<serialID>")'
```

Example of full command;

```
cd ~/klipper/scripts
~/klippy-env/bin/python -c 'import flash_usb as u; u.enter_bootloader("/dev/serial/by-id/usb-Cartographer_614e_060004001443303856303820-if00")'
```

<figure><img src="../../../../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

After the command runs, repeat step 1, and run a `ls -l /dev/serial/by-id/` and note down the new ID, this should have changed to usb-katapult, rather than usb-cartographer.

Now navigate to the folder where your firmware is located, for the example I will be using, I will be updating a v2 probe.&#x20;

Now, run the following command, replacing \<firmware> with the firmware you are flashing, and \<serial> with the serial ID and path.&#x20;

```
~/klippy-env/bin/python ~/klipper/lib/canboot/flash_can.py -f <firmware> -d <serial>
```

Again, an example of a full command

```
~/klippy-env/bin/python ~/klipper/lib/canboot/flash_can.py -f Cartographer_USB_8kib_offset.bin -d /dev/serial/by-id/usb-katapult_stm32f042x6_060012001643565537353020-if00
```

If successful, you should have the following output.&#x20;

<figure><img src="../../../../.gitbook/assets/image (2) (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

Restart your printer firmware, and everything should work as normal.&#x20;

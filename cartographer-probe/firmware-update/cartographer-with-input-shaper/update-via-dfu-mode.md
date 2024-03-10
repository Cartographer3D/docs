---
description: Update or reflash your Cartographer Probe via DFU Mode.
---

# Update via DFU Mode

### Compatibility

The following method is compatible with MOST Cartographer probes, please check the compatibility chart listed below.&#x20;

| Probe                                                       | Interface | Compatible                                                      |
| ----------------------------------------------------------- | --------- | --------------------------------------------------------------- |
| Cartographer V1 (RP2040)                                    | USB       | [Click Here](../cartographer-rp2040/dfu-u2f-bootloader-mode.md) |
| Cartographer with Input Shaper (v2)                         | USB       | Yes                                                             |
|                                                             | CAN       | No                                                              |
| Cartographer Probe v3 with Input Shaping (Hybrid USB & CAN) | USB       | Yes                                                             |
|                                                             | CAN       | Yes                                                             |

### Pre-requirements

Prior to flashing, you will need to following tools

* 2 x Ferrous Tweezers (or any conductive tool to bridge the two pads)
* 1 x Compatible Cartographer Probe (see above)
* 1 x USB Cable terminated to work w/ Catographer

### Firmware

The best place to get the probes firmware is from our  [GitHub](https://github.com/Cartographer3D/cartographer-klipper/tree/master/firmware). These have been tested thoroughly, and are known to work perfectly.  If you want to find a link to the latest firmware for each of your probes, please check [here](https://docs.cartographer3d.com/firmware-update/which-firmware).

You can also build your own firmware, our GitHub organisation has both a custom build of [Klipper](../../../) and [Katapult](https://github.com/Cartographer3D/katapult) that you can build yourself.&#x20;

{% hint style="danger" %}
Untested Firmware could brick your probe - it is advisable if this is the case, you have a STLink handy in order to easily re-flash the probe.
{% endhint %}

### Entering DFU Mode

To enter DFU Mode, it can be a bit fiddly, but once you get the knack of it, it's fairly simple.&#x20;

Plug your USB cable into the device you will be flashing from and your Cartographer probe, this can be either a seprate Windows PC, Mac, or a Linux machine, or the device you run your 3D Printer off. &#x20;

Using your ferrous tweezers, or similar use one to bridge pads 1 (boot0), once you have a solid contact on those tap pad 2 (reset) with your other ferrous tool.&#x20;

<figure><img src="../../../.gitbook/assets/DFUModePointsv3.png" alt=""><figcaption></figcaption></figure>

If you have done this correctly, your device should have entered DFU Mode.&#x20;

To check,&#x20;

* Linux - follow the following steps
  * SSH in, or load a termanal shell.&#x20;
  * type `lsusb` in your bash shell, it should list a device in DFU Mode
  * One of the options should be `Bus 001 Device 004: ID 0483:df11 STMicroelectronics STM Device in DFU Mode` - This (as long as you don't have any other devices in DFU Mode) should be your Cartographer Probe in DFU Mode.
* Windows - follow the following steps
  * Start Menu
  * Search and open "Device Manager"
  * Scroll down to Universal Serial Bus Devices&#x20;
  * You should see STM32 BOOTLOADER as an option\
    &#x20;<img src="../../../.gitbook/assets/image (7) (1).png" alt="Device Manager view of Cartographer in Bootloader mode." data-size="original">
* Mac - TBC

### Flashing via STM32CubeProgrammer (Windows & MacOS)

Download and Install STM32CubeProgrammer from [here](https://www.st.com/en/development-tools/stm32cubeprog.html), I warn you it requires you to sign up for an account.

Open the application, and on the RIGHT side, select the following options and press **Connect**.&#x20;

<figure><img src="../../../.gitbook/assets/image (8) (1).png" alt=""><figcaption><p>STM32CubeProgrammer Settings</p></figcaption></figure>

Once you have connected, Click Open File - you will need to select both the Katapult Bootloader for your board, and your Cartographer Firmware that you have downloaded.&#x20;

<figure><img src="../../../.gitbook/assets/image (10) (1).png" alt=""><figcaption><p>Firmwares Loaded</p></figcaption></figure>

For your Cartographer Firmware, you need to set the address to `0x08002000` This provides the 8KiB offset for the firmware. Katapult firmware can be flashed at the default `0x08000000.`

<figure><img src="../../../.gitbook/assets/STLink (1).png" alt=""><figcaption><p>How to change the address in STM32CubeProgrammer</p></figcaption></figure>

If in doubt about what address to use, please check the relevent tables [here](https://docs.cartographer3d.com/firmware-update)

On each of the firmware's press "Download", starting with Katapult, then with Cartographer. \
\
Now press Disconnect in the TOP RIGHT corner.&#x20;

If your BLUE LED is Flashing, you have not fully flashed your Firmware, and you should start again, If you now Power Cycle your probe, or simply hit the RESET (2) pads from earlier, your probe should react when it has anything solid metal put under it.&#x20;

### Flashing via DFU Util (Linux Terminal).&#x20;

SSH into your linux host MCU, ensuring that your Cartographer is plugged in and in DFU Mode.&#x20;

Navigate into the correct folder, so if you want to update your v3 run the following command.&#x20;

```
cd ~/cartographer-klipper/firmware/v3 - Carto with Input Shaper Hybrid
```

Once in the folder, simply check that your probe is still in DFU Mode by running `lsusb`, and if you still get a result stating it is in DFU Mode, run the following command.&#x20;

```
dfu-util -R -a 0 -s 0x08000000:leave -D firmware.bin
```

NOTE - REPLACE the address (`0x08000000`) with what ever is listed in the table here for the specific firmware you are using, and rename `firmware.bin` to what ever the firmware file you are using is called.&#x20;

Example:

```
dfu-util -R -a 0 -s 0x08000000:leave -D Full_Cartographer_USB_v3.bin
```

Once compelte, it shoudl exit out of DFU mode, and you should be able to find your probe using either CAN or USB.&#x20;

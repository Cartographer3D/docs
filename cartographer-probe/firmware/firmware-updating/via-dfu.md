---
layout:
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: false
---

# via DFU

### Should You Be Using DFU?

* No use KATAPULT! Yes, this is the first point of call when you do a cartographer firmware update. Only if you have issues with this method, should you attempt the others.
* If you ordered a USB flashed cartographer, you use the [USB Katapult Method](via-katapult/usb-flash.md)
* If you ordered a CAN flashed cartographer, you use the [CANBUS Katapult Me](via-katapult/canbus-flash.md)[thod](via-katapult/canbus-flash.md)

### Whats Required?

* Cartographer Probe
* Two pairs of conductive (Metal) Tweezers
*   USB-A to JST-PH Cable

    <figure><img src="https://github.com/user-attachments/assets/1c082c5d-44ff-43e1-b1bf-f70b4249a490" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
Using the scripts below, you may need to use the **Install Prerequisites** option first to make sure everything is configured prior to flashing.
{% endhint %}

## DFU Updating

### What is DFU

* This should be seen as a last resort and should only be neccasary when Katapult flashing is unavailable for whatever reason.
* DFU Mode (Device Firmware Upgrade Mode) is STM's bootloader thats apart of the STM32 chip included on cartographer probes. Its next to impossible to make this mode fail. However getting the chip into DFU mode can be a challenge as it requires touching the **BOOT0** and **RESET** pads on the cartographer PCB in the correct manner.

![image](https://github.com/user-attachments/assets/b9d2581f-9b64-4e61-bc7f-e3382b0155ad)

### Step 1. Enter DFU Mode

* Entering DFU mode is simple in theory but a bit more fiddly in practice. With the cartographer plugged in via USB, first short the two pads of the **BOOT0** set (marked 1 on the photo). With **BOOT0** still shorted, briefly short the RESET pads (marked 2). This will put the device in DFU mode.
* This process can be tricky and take some time, so listed below are two ways to make it simpler.

{% hint style="danger" %}
No LEDs will be on when in DFU mode. If the blue LED is lit, even intermittently, the device is in runtime mode and this isnt what we want. Continue touching those pads till it works!
{% endhint %}

{% hint style="info" %}
Via SSH, use the command `lsusb | grep "DFU"` to determine whether the device is in **DFU Mode**&#x20;
{% endhint %}

<figure><img src="https://github.com/user-attachments/assets/5996588d-1049-458f-8aa4-82894c26168f" alt=""><figcaption></figcaption></figure>

#### Make-it-easier option #1: printed tweezer guide

* You can use the PCB cover designed by [MakerMylo](https://www.youtube.com/@makermylo) to help with the fine-motor work of shorting pads. It clips onto the PCB and helps you to align tweezers accurately for shorting pads.

{% file src="../../../.gitbook/assets/PadPusher3000.stl" %}

#### Make-it-easier option #2: solder-bridging the **BOOT0** pads

* Soldering a bridge on the **BOOT0** pads can make this process much easier. You will still need to briefly short the **RESET** pads, but you won't have to coordinate two sets of tweezers.

* Once you've flashed by using DFU mode, remember to de-solder the bridge.

### Step 2. SSH into Host &  Run Script

```bash
bash <(wget -qO - firmware.cartographer3d.com/firmware.sh)
```

![Screen #1](https://github.com/user-attachments/assets/b49c213b-cd06-44aa-8fb4-9989e4994957)

![Screen #2](https://github.com/user-attachments/assets/1a93eb97-8dff-446b-af7b-1fdf8dd7e38f)

{% hint style="info" %}
Choose FULL\_CARTOGRAPHER\_CANBUS for using Cartographer via  CANBUS.

Choose FULL\_CARTOGRAPHER\_USB for using Cartographer via USB
{% endhint %}

![Screen #3](https://github.com/user-attachments/assets/6c187585-f4c2-4de6-965b-f12d873a9f6c)

### Step 3. Done

Once flashed, you will see the image below. This is a successful flash and youre all finished.&#x20;

<figure><img src="https://github.com/user-attachments/assets/3c2caf92-916d-4180-a885-cbb6964a3133" alt=""><figcaption><p>Screen #4</p></figcaption></figure>

### Step 4. Now What?

* If you flashed for canbus, unplug cartographer and plug in via canbus
* If you flashed for usb, power cycle your device.

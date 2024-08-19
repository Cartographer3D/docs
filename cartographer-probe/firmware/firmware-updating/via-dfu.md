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

* Last Updated 11/08/2026
* Maintained by KrauTech

### Should You Be Using DFU?

* No use KATAPULT! Yes, this is the first point of call when you do a cartographer firmware update. Only if you have issues with this method, should you attempt the others.
* If you ordered a USB flashed cartographer, you use the [USB Katapult Method](via-katapult/usb-flash.md)
* If you ordered a CAN flashed cartographer, you use the [CANBUS Katapult Me](via-katapult/canbus-flash.md)[thod](via-katapult/canbus-flash.md)

### Whats Required?

* Cartographer Probe
* Conductive (Metal) Tweezers
*   USB-A to JST-PH Cable

    <figure><img src="https://github.com/user-attachments/assets/1c082c5d-44ff-43e1-b1bf-f70b4249a490" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
Using the scripts below, you may need to use the **Install Prerequisites** option first to make sure everything is configured prior to flashing.
{% endhint %}

## DFU Updating

### What is DFU

* This should be seen as a last resort and should only be neccasary when Katapult flashing is unavailable for whatever reason.
* DFU Mode (Device Firmware Upgrade Mode) is STM's bootloader thats apart of the STM32 chip included on cartographer probes. Its next to impossible to make this mode fail. However getting the chip into DFU mode can be a challenge as it requires touching the **boot0** and **reset** pads on the cartographer PCB in the correct manner.

![image](https://github.com/user-attachments/assets/b9d2581f-9b64-4e61-bc7f-e3382b0155ad)

### Step 1) Enter DFU Mode

* DFU mode is relatively simple to enter, but harder in practice. With cartographer plugged in via USB, touch the **boot0** (1) and **reset** (2) pads. This will put the device in DFU mode.
* This can be quite fiddly and take some time, so listed below is 2 convenient ways to make this more simple.

{% hint style="danger" %}
No LEDs will be on when in DFU mode. If the blue LED is lit, the device is in runtime mode and this isnt what we want. Continue touching those pads till it works!
{% endhint %}

{% hint style="info" %}
via SSH use command `lsusb | grep "DFU"` to find if the device is in **DFU Mode**&#x20;
{% endhint %}

<figure><img src="https://github.com/user-attachments/assets/5996588d-1049-458f-8aa4-82894c26168f" alt=""><figcaption></figcaption></figure>

#### PCB Cover

* Use the new PCB cover made by [MakerMylo](https://www.youtube.com/@makermylo) to clip onto the PCB, it will help align tweezers for touching the pads.

{% file src="../../../.gitbook/assets/PadPusher3000.stl" %}

#### Solder Boot0 Method

* Soldering a bridge on the **boot0** pads can make this process, much easier. All you need to then do is plug in the USB cable and the probe will enter DFU mode.
* Once youve flashed via DFU mode, remember to de-solder the bridge.

### Step 2) SSH into Host &  Run Script

```bash
bash <(wget -qO - firmware.cartographer3d.com/firmware.sh)
```

![Screen #1](https://github.com/user-attachments/assets/b49c213b-cd06-44aa-8fb4-9989e4994957)

![Screen #2](https://github.com/user-attachments/assets/1a93eb97-8dff-446b-af7b-1fdf8dd7e38f)

{% hint style="info" %}
Choose #1 if faced with the image below to use cartographer via canbus at 1M bitrate.

Choose #2 if you will be using cartographer via USB
{% endhint %}

![Screen #3](https://github.com/user-attachments/assets/6c187585-f4c2-4de6-965b-f12d873a9f6c)

### Step 3) Done

Once flashed, you will see the image below. This is a successful flash and youre all finished.&#x20;

<figure><img src="https://github.com/user-attachments/assets/3c2caf92-916d-4180-a885-cbb6964a3133" alt=""><figcaption><p>Screen #4</p></figcaption></figure>

### Step 4) Now What?

* If you flashed for canbus, unplug cartographer and plug in via canbus
* If you flashed for usb, power cycle your device.

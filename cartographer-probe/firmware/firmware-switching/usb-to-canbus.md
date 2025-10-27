# USB to CANBUS

## Currently Using USB?

Looking at using Cartographer via CANBUS instead of USB? Follow the steps below to make the change!

***

## Step 1. Plug In Cartographer via USB

## Step 2.  SSH Into Your Host Device & Run The Script

```bash
git clone https://github.com/Cartographer3D/cartographer_firmware.git
~/cartographer_firmware/scripts/firmware.py -f usb -t
```

<figure><img src="../../../.gitbook/assets/usb-menu.png" alt="" width="557"><figcaption></figcaption></figure>

## Step 3. Find Your Device

<figure><img src="../../../.gitbook/assets/usb-devices.png" alt="" width="551"><figcaption></figcaption></figure>

## Step 4. Select Which Firmware/Bitrate You Want

<figure><img src="../../../.gitbook/assets/usb-katapult.png" alt="" width="551"><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/usb2can.png" alt="" width="551"><figcaption></figcaption></figure>

## Step 5. Flash Katapult Firmware

<figure><img src="../../../.gitbook/assets/usb-flashed-1.png" alt="" width="551"><figcaption></figcaption></figure>

## Step 6. Unplug USB and plug into CANBUS

## Step 7. Re-run Script

```bash
~/cartographer-klipper/scripts/firmware.py -f can
```

## Step 8. Find Your Device

<figure><img src="../../../.gitbook/assets/can-menu.png" alt="" width="557"><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/can-find-device.png" alt="" width="551"><figcaption></figcaption></figure>

## Step 9. Select Firmware & Flash

<figure><img src="../../../.gitbook/assets/can-firmware-latest.png" alt="" width="551"><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/can-confirm.png" alt="" width="551"><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/can-flashed-1.png" alt="" width="551"><figcaption></figcaption></figure>

## Step 10. Done

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

# USB to CANBUS

## Currently Using USB?

Looking at using Cartographer via CANBUS instead of USB? Follow the steps below to make the change!

***

## Step #1) Plug In Cartographer via USB

## Step #2)  SSH Into Your Host Device & Run The Script

```bash
bash <(wget -qO - firmware.cartographer3d.com/firmware.sh) -t katapult -s canbus
```

<figure><img src="../../../.gitbook/assets/image (29).png" alt=""><figcaption></figcaption></figure>

## Step #3) Select Which Firmware/Bitrate You Want

<figure><img src="../../../.gitbook/assets/image (31).png" alt=""><figcaption></figcaption></figure>

## Step #4) Flash Katapult Firmware

## Step #5) Unplug USB and plug into CANBUS

## Step #6) Re-run Script

```
bash <(wget -qO - firmware.cartographer3d.com/firmware.sh)
```

## Step #7 Choose If You Want Survey/Touch

<figure><img src="../../../.gitbook/assets/image (30).png" alt=""><figcaption></figcaption></figure>

## Step #8 Select Firmware & Flash

## Step #9 Done

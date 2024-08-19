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

## Step #3) Choose if you want Survey or not

<figure><img src="../../../.gitbook/assets/image (30).png" alt=""><figcaption></figcaption></figure>

## Step #4) Select Which Firmware/Bitrate You Want

<figure><img src="../../../.gitbook/assets/image (31).png" alt=""><figcaption></figcaption></figure>

## Step #5) Done, Unplug and Plug into CANBUS

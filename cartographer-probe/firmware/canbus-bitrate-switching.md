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

# CANBUS Bitrate Switching

## Do You Need To Switch Bitrate?

Are you running CANBUS at a different bitrate? If you arent using the default 1M (1000000) go ahead and use the steps below to swap to whatever version you need.

***

## Step #1) Plug In Cartographer via CANBUS

## Step #2) SSH Into Your Host Device & Run The Script

```bash
bash <(wget -qO - firmware.cartographer3d.com/firmware.sh) -t katapult -s canbus
```

<figure><img src="../../.gitbook/assets/image (25).png" alt=""><figcaption></figcaption></figure>

## Step #3) Choose if you want Survey or not

<figure><img src="../../.gitbook/assets/image (26).png" alt=""><figcaption></figcaption></figure>

## Step #4) Select Which Firmware/Bitrate You Want

<figure><img src="../../.gitbook/assets/image (31).png" alt=""><figcaption></figcaption></figure>

## Step #5) Done

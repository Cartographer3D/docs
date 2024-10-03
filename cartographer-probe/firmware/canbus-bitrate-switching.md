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

## Step 1. Plug In Cartographer via CANBUS

## Step 2. SSH Into Your Host Device & Run The Script

```bash
bash <(wget -qO - firmware.cartographer3d.com/firmware.sh) -t katapult -s canbus
```

<figure><img src="../../.gitbook/assets/image (25).png" alt=""><figcaption></figcaption></figure>

## Step 3. Select Which Firmware/Bitrate You Want

<figure><img src="../../.gitbook/assets/image (31).png" alt=""><figcaption></figcaption></figure>

## Step 4. Flash Firmware

## Step 5. Re-Run Script

```bash
bash <(wget -qO - firmware.cartographer3d.com/firmware.sh)
```

## Step 6. Choose If You Want Survey/Touch

<figure><img src="../../.gitbook/assets/image (26).png" alt=""><figcaption></figcaption></figure>

## Step 7. Select Firmware & Flash

## Step 8. Done

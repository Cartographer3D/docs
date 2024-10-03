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

# CANBUS to USB

## Currently Using CANBUS?

Looking at using Cartographer via USB instead of CANBUS? Follow the steps below to make the change!

***

## Step 1. Plug In Cartographer via CANBUS

## Step 2. SSH Into Your Host Device & Run The Script

```bash
bash <(wget -qO - firmware.cartographer3d.com/firmware.sh) -t katapult -s usb
```

<figure><img src="../../../.gitbook/assets/image (25).png" alt=""><figcaption></figcaption></figure>

## Step 3. Select The USB Firmware

<figure><img src="../../../.gitbook/assets/image (27).png" alt=""><figcaption></figcaption></figure>

## Step 4. Flash Katapult Firmware

## Step 5. Unplug CANBUS and plug into USB

## Step 6. Re-run Script

```
bash <(wget -qO - firmware.cartographer3d.com/firmware.sh)
```

## Step 7. Choose If You Want Survey/Touch

<figure><img src="../../../.gitbook/assets/image (26).png" alt=""><figcaption></figcaption></figure>

## Step 8.Select Firmware & Flash

## Step 9. Done

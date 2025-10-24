# CANBUS Bitrate Switching

## Do You Need To Switch Bitrate?

Are you running CANBUS at a different bitrate? If you arent using the default 1M (1000000) go ahead and use the steps below to swap to whatever version you need.

***

## Step 1. Plug In Cartographer via CANBUS

## Step 2. SSH Into Your Host Device & Run The Script

```bash
cd ~/cartographer-klipper/scripts
./firmware.py -f can -k
```

<figure><img src="../../.gitbook/assets/can-menu.png" alt="" width="557"><figcaption></figcaption></figure>

## Step 3. Find Your Device

<figure><img src="../../.gitbook/assets/can-find-device.png" alt="" width="551"><figcaption></figcaption></figure>

## Step 4. Select Which Firmware/Bitrate You Want

<figure><img src="../../.gitbook/assets/can-katapult.png" alt="" width="551"><figcaption></figcaption></figure>

## Step 5. Flash Firmware

<figure><img src="../../.gitbook/assets/can-flashed-1.png" alt="" width="551"><figcaption></figcaption></figure>

## Step 6. Re-Run Script

```bash
cd ~/cartographer-klipper/scripts
./firmware.py -f can
```

<figure><img src="../../.gitbook/assets/can-menu.png" alt="" width="557"><figcaption></figcaption></figure>

## Step 7. Find Your Device

<figure><img src="../../.gitbook/assets/can-find-device.png" alt="" width="551"><figcaption></figcaption></figure>

## Step 8. Select Firmware & Flash

<figure><img src="../../.gitbook/assets/can-firmware-latest.png" alt="" width="551"><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/can-confirm.png" alt="" width="551"><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/can-flashed-1.png" alt="" width="551"><figcaption></figcaption></figure>

## Step 9. Done

# Broken Katapult Bootloader

There are some Cartographer V3 ADXL probes that were shipped with a broken version of katapult. Unfortunately this means that when you go to update firmware via Katapult, the device wont be able to enter katapult mode for flashing.\
\
Fixing it is quite simple.

## Step 1. [Visit Here for the DFU flashing guide.](../../original-plugin/firmware-archive/firmware-updating/via-dfu.md)

## Step 2. Once Flashed

If you chose FULL CANBUS, unplug the cable and plug Cartographer into your CANBUS cable.

If you chose FULL USB, unplug and re-plug into USB cable.

## Step 3. All Done

## Optional Step: Survey Touch

If you want to use **Survey Touch you will need to do some extra steps.**

* For USB, [Check out this guide on updating firmware to Survey Touch mode.](../../original-plugin/firmware-archive/firmware-updating/via-katapult/usb-flash.md)
* For CANBUS, [Check out this guide on updating firmware to Survey Touch mode.](../../original-plugin/firmware-archive/firmware-updating/via-katapult/canbus-flash.md)

### Katapult Bootloader will now be fixed for future flashing and DFU will not be required unless another issue arises with Katapult.

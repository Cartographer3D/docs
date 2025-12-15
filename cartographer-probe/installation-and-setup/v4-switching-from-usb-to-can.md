# V4 - Switching from USB to CAN

{% hint style="info" %}
This information only applies to Cartographer V4&#x20;
{% endhint %}

All Cartographer V4 units will ship with USB Firmware on them by default, meaning that if you want to use it for CAN Bus, you will need to switch the firmware. This information will be repeated in the [firmware](../firmware/ "mention") section of the documentation in far more detail, but these are the basic quick steps to get you setup in CAN mode. \
\
This will set your probe up with a Baudrate of 1,000,000. If you wish to have a baudrate of 500,000 or 250,000 you will need to manually flash it with the firmware for now.

### Step 1 - Plug in your probe to USB

Plug your probe in to your Pi via the USB Cable. You should see the USB Status LED light up on the probe.&#x20;

<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption><p>The USB Status LED. </p></figcaption></figure>

### Step 2 - Install the Cartographer Firmware Repository

SSH into your Pi, and run the following script.

```bash
cd ~
if [ -d ~/cartographer_firmware/ ]; then
    echo "Directory Exists - Starting Firmware Script"
    cd ~/cartographer_firmware/
    git pull
else
    git clone https://github.com/Cartographer3D/cartographer_firmware.git
fi
./v4_switch.sh
```

You should see the following screen come up.

<figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

### Step 3 - Follow the On Screen Guide

Confirm you are running a Cartographer V4 (this is the single PCB probe) and press Y

it will then run through and flash the Katapult Deployer firmware, this will switch the probe from USB to CAN Bus.&#x20;

<figure><img src="../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

Once this screen comes up, you will notice the LED on your probe will have changed from the USB Status LED to the CAN Status LED.

<figure><img src="../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

### Step 4 - Select the CAN Firmware you want.

You will be prompted to select from two firmware options, Full or Lite.&#x20;

Lite Firmware sends reduced instructions from the MCU to your Pi, reducing the load on your system as a whole. This is recommended if you have a lower powered Pi or other MCUs, or get connection losses.

In general, we recommend running the Full firmware, so select the option you want to run.

<figure><img src="../../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

This will now give you a command (in green) for you to run once you have plugged your Cartographer V4 in to your CAN network. Some people don't mind doing this while the printer is powered on, but we could never recommend that... becuase you know.. safety, so you do you...&#x20;

If you are powering off your printer, copy the command into a notepad document or similar, power off the machine and then connect the probe to the CAN port. \
\
Once you power back on, reconnect via SSH and paste in the commands you copied over.&#x20;

If you do live on the edge, and plugged in your probe to CAN without powering off, you can press Y now and the command should automatically run for you.&#x20;

### Step 5 - Finished :smile:

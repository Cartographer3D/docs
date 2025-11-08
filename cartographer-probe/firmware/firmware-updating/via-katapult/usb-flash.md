# USB Flash

### CANBUS or USB

* If you ordered a USB flashed cartographer, you use the [USB Katapult Method](usb-flash.md)
* If you ordered a CAN flashed cartographer, you use the [CANBUS Katapult Me](canbus-flash.md)[thod](canbus-flash.md)

### Whats Required?

* Cartographer Probe
*   USB-A to JST-PH Cable

    <figure><img src="https://github.com/user-attachments/assets/1c082c5d-44ff-43e1-b1bf-f70b4249a490" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
Using the scripts below, you may need to use the **Install Prerequisites** option first to make sure everything is configured prior to flashing.
{% endhint %}

## USB Katapult Updating

## Step 1. Plug Cartographer in via USB

## Step 2. SSH into Device & Run Script

```bash
cd ~
if [ -d ~/cartographer_firmware/ ]; then
    echo "Directory Exists - Starting Firmware Script"
    cd ~/cartographer_firmware/
    git pull
else
    git clone https://github.com/Cartographer3D/cartographer_firmware.git
fi
~/cartographer_firmware/scripts/firmware.py
```

## Step 3. Select Katapult - USB Menu

<figure><img src="../../../../.gitbook/assets/main-menu-basic (1).png" alt="" width="543"><figcaption></figcaption></figure>

## Step 4. Find Your Device

<figure><img src="../../../../.gitbook/assets/usb-menu.png" alt="" width="557"><figcaption></figcaption></figure>

## Step 5. Select Your Device

<figure><img src="../../../../.gitbook/assets/usb-devices.png" alt="" width="551"><figcaption></figcaption></figure>

## Step 6. Find Latest Firmware

<figure><img src="../../../../.gitbook/assets/usb-firmware-latest.png" alt="" width="551"><figcaption></figcaption></figure>

## Step 7. Flash Firmware

<figure><img src="../../../../.gitbook/assets/usb-confirm.png" alt="" width="551"><figcaption></figcaption></figure>

## Step 8. Device Flashing

<figure><img src="../../../../.gitbook/assets/usb-flashed-1.png" alt="" width="551"><figcaption></figcaption></figure>

## Step 9. All Done

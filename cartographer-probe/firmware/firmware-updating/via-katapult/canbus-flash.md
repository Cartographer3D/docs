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

# CANBUS Flash

### CANBUS or USB

* If you ordered a USB flashed cartographer, you use the [USB Katapult Method](usb-flash.md)
* If you ordered a CAN flashed cartographer, you use the [CANBUS Katapult Me](canbus-flash.md)[thod](canbus-flash.md)

### Whats Required?

* Cartographer Probe
* Canbus to JST-PH Cable (For Katapult Canbus Flashing)

{% hint style="info" %}
Using the scripts below, you may need to use the **Install Prerequisites** option first to make sure everything is configured prior to flashing.
{% endhint %}

## CANBus Katapult Updating

### Step 1. Plug Cartographer in via CANBUS

### Step 2. SSH into Device & Run Script

```bash
bash <(wget -qO - firmware.cartographer3d.com/firmware.sh)
```

### Step 3. Get Your UUID

This method requires prior knowledge of your **CANBUS UUID**.

This should have been supplied to you in your hardware box if purchased (insert date).

If you do not have your UUID. Visit [HERE](broken-reference) to get it.

The script will detect your UUID if your UUID is inside your **printer.cfg** somewhere under `[scanner]` if it doesnt detect, you can manually enter it.

![Screen #1 - Canbus Detected](https://github.com/user-attachments/assets/612dec98-50ab-4ab6-9d61-bc465a7cf411)

### Step 4. Choose Firmware to Flash

{% hint style="info" %}
Your CANBUS bitrare (if configured on your host device) should be detected and displayed. You should flash your cartographer with MATCHING bitrate firmware.
{% endhint %}

You can pick any of these, however to remain detected you should match your bitrate. You can flash USB if youd like to use cartographer via USB however, as bitrate doesnt matter.&#x20;

<figure><img src="https://github.com/user-attachments/assets/6ad85f9a-3aba-466b-b483-e2ff23550a71" alt=""><figcaption><p>Screen #2 - Select Firmware</p></figcaption></figure>

## Step 5. Done

![Screen #3 - Flash Success](https://github.com/user-attachments/assets/0fb24c99-d36d-4ce2-9846-48c99d4eb952)

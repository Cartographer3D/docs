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

# USB Flash

* Last Updated 11/08/2026
* Maintained by KrauTech

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

### Step 1) Plug Cartographer in via USB

### Step 2) SSH into Device & Run Script

```bash
bash <(wget -qO - firmware.cartographer3d.com/firmware.sh)
```

<figure><img src="https://github.com/user-attachments/assets/b06e734b-d335-4073-9407-be60ec8bd17b" alt=""><figcaption><p>Screen #1 - USB Device Found</p></figcaption></figure>

### Step 3) Choose Firmware to Flash

{% hint style="info" %}
If you plan on using CANBUS, Your CANBUS bitrate (if configured on your host device) should be detected and displayed. You should flash your cartographer with MATCHING bitrate firmware.
{% endhint %}

You can pick any of these, however to remain detected you should match your bitrare. You can flash USB if youd like to use cartographer via USB however, as bitrate doesnt matter.&#x20;

<figure><img src="https://github.com/user-attachments/assets/dfb64682-28c7-4a4c-a9fe-67649d70bfff" alt=""><figcaption><p>Screen #2 - Choose Firmware</p></figcaption></figure>

## Step 4) Done

![Screen #3 - Flash Success](https://github.com/user-attachments/assets/6920bdbd-2ee7-4947-97f1-c5a623471898)

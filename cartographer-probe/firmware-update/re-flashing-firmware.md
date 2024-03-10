# Re-Flashing Firmware

A number of probes unfortunatly shipped miss-flashed with the incorrect firmware, this guide will go through how to re-flash them with the correct firmware.

### Equipment / Parts Required

For this, you will need the following items / tools, though it does vary depending on the configuration you recieved, or if you have any existing equipment.&#x20;

If you recieved a USB Cable with your order, OR have a USB Cable terminated with a JST-PH connector then continue from **here**

If you have a ST-Link Flasher ([like this](https://www.amazon.com/Sumklin-ST-Link-Emulator-Downloader-Connect/dp/B0CHWKJQYB/ref=sr\_1\_6?crid=S6B8HWUSRC0Z\&dib=eyJ2IjoiMSJ9.qqFD5Om07FWVxJ7mURnZvPq709MTcuqoA3fE0gXiF\_SWEFG9f1NUd634THxfckI76D\_hZ3arbsDiW-Db1xTIEOza\_to4Idw50g0wqw8NlTEQcTI\_alwxI6Vlp09baxGXlMWWQvW8BoursvDtdmAKY7ExUxOwyWdp-R7b-9ekncnwAIKpE0SS1KY7FmNICg4GXiJzwnURM0ze\_dw8vLbUXr2P1rsvtNRHpObpiPAhdS4.usA91wnACoc6mryl4h5GOt6De85Z-hRVX8W9dbaCDLc\&dib\_tag=se\&keywords=ST+Link\&qid=1710043006\&sprefix=st+l%2Caps%2C874\&sr=8-6)) click [here](cartographer-with-input-shaper/update-via-stlink.md)

There are two solutions;

* Method 1 - Modifying a USB cable to connect with the CAN cable&#x20;
* Method 2 - Create a USB Cable with a JST-PH Connector&#x20;

**Method 1  Equipment**

* A old USB cable, any old USB2 cable which does data (not a charge only USB-C Cable)&#x20;
* Your fastener pack that came with your probe
* Your CAN cable
* Some cutters / strippers.&#x20;
* 1 or 2 Tweezers (or something to bridge the BT0 and RESET pad)

Method 2 Equipment

* A old USB cable, any old USB2 cable which does data (not a charge only USB-C Cable)&#x20;
* Your fastener pack that came with your probe
* Some cutters / strippers.&#x20;
* A crimp tool for JST-PH
* 1 or 2 Tweezers (or something to bridge the BT0 and RESET pad)

### Method 1

Step 1 - Cut the end off your doner USB cable

<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption><p>Remove the end of the USB Cable</p></figcaption></figure>

Step 2 - Remove the outer plastic, revealing the 4 pairs of cables

<figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption><p>Remove the outer plastic</p></figcaption></figure>

Remove any outer sheilding

<figure><img src="../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

Use your snippers / strippers to expose about 6 - 8 mm at the end of your wires

<figure><img src="../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

Step 3 - Feed the exposed wires into the DuPont connectors, and use the right angle dupont mail connectors to plug the cable in and force contact

Typically the following cables will be matched with each other&#x20;

| USB Cable   | CAN Cable      |
| ----------- | -------------- |
| Red - 5v    | Red - 5v       |
| Black - GND | Black - GND    |
| Green (D+)  | Yellow (Can H) |
| White (D-)  | White (Can L)  |

<figure><img src="../../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (5).png" alt=""><figcaption><p>Notice the DuPont 2.54mm RA connectors plugging the cable in.</p></figcaption></figure>

You should be able to connect your USB Cable to your computer now, as the probe will have accidently been flashed with USB Firmware rather than CAN, so if you plug into a Windows PC, you should hear that new device connected chime.&#x20;

If you plug it into your Pi, or a linux PC it shouild appear under `lsusb` as OpenMoko, and if you recieved your probe in mid-march, and it has the USB firmware on it, if you do:

`ls /dev/serial/by-id/`

It should appear as a serial device there. Any issues, please join our Discord and ping me (RichardTHF) for help and support.&#x20;

### Method 2

Crimping your own JST-PH - USB cable, this is a useful cable to have, and can be done with the crimps and connector incldued with the probe.&#x20;



#### Step 1

Cut the end off your doner USB cable. This needs to be a cable which works for data, there seem to be a lot of USB cables which are power only, these will not work.&#x20;

<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

#### Step 2&#x20;

Strip the cable back to reveal the internal cables.&#x20;

<figure><img src="../../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

#### Step 3&#x20;

Crimp the JST PH connectors onto the cable.&#x20;

I found this video for how to crimp JST connectors, check it out its very well done.&#x20;

{% embed url="https://youtube.com/watch?v=jHfYzrSF4pY" %}

<figure><img src="../../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

Step 4 - Rehouse the connector

Notice the order - of the cable and connector.&#x20;

<figure><img src="../../.gitbook/assets/image (9).png" alt=""><figcaption><p>Notice the order of the cables.</p></figcaption></figure>

You should be able to connect your USB Cable to your computer now, as the probe will have accidently been flashed with USB Firmware rather than CAN, so if you plug into a Windows PC, you should hear that new device connected chime.&#x20;

If you plug it into your Pi, or a linux PC it shouild appear under `lsusb` as OpenMoko, and if you recieved your probe in mid-march, and it has the USB firmware on it, if you do:

`ls /dev/serial/by-id/`

It should appear as a serial device there. Any issues, please join our Discord and ping me (RichardTHF) for help and support. &#x20;

Now you have compelted this section, let's move on and put the probe into[ DFU mode. ](cartographer-with-input-shaper/update-via-dfu-mode.md)

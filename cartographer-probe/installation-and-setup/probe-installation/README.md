# Probe Installation

## Mount Cartographer

Note there are two different versions of Cartographer, a USB and a CAN version. These will be clearly defined in the section titles when they differentiate. Please make sure you follow the correct guide for the instllation of yours. &#x20;

### Location

Cartographer is designed to use the existing mounts available for similar products on the market. The hole spacing is 31.6mm and it takes M3 bolts.

There should be no metal directly above the Cartographer Coil, this is refered too as the keep out zone. There are three STEP files available on our GitHub ([here](https://github.com/Cartographer3D/cartographer-probe/tree/main/STEP)) that highlight this area.&#x20;

The probe can be installed in any orentation, you just need to ensure you set the X and Y offset in the config relative to the probes location to the nozzle.&#x20;

Ensure when you are mounting Cartographer that you recess the probe approximatly 3 mm from the Nozzles Z height.

### Cable Routing

#### USB (both RP2040 and STM32 based probes)

{% hint style="danger" %}
Routing the USB cable correctly is essential, <mark style="color:red;">**the provided cable is NOT rated for being routed through cable chains**</mark>, please mount either along your Bowden or Umbilical path.
{% endhint %}

During installation, try to ensure that the cable will not snag or get caught on anything as this could cause damage to your probe.&#x20;

It is adviseable to plug your USB Cable directly into a USB Port, using a hub may cause performance limitations.&#x20;

#### CAN (STM32 based)

Currently we advise that the CAN probe is used with BigTreeTech Toolboards, this is due to their easy addition of a spur.&#x20;

When install up your CAN probe, please ensure that you add a twist to your white and yellow wires every 24mm.

{% hint style="danger" %}
<mark style="color:red;">**NOTE**</mark> <mark style="color:red;"></mark><mark style="color:red;">- Cartographer3D Operates at 5v, and requires a 5v input. 24v will not work and will damage your probe beyond repair.</mark>&#x20;
{% endhint %}

### **CAN Termination**

#### Cartographer w/ Input Shaper (v2)

There are many differing opinions on where and how to terminate your CANBUS setup, if you want to fully meet with spec, you are supposed to terminate on the last device in the chain. \
\
When setting up your probe, this is fairly difficult to do, in this case it can purely be treated like a spur, and you can terminate on your toolhead. With this method, we have not seen any detremental performance or issues.&#x20;

IF you want to terminate on your Cartographer, this requires two solder points to be bridged together (see below)&#x20;

<figure><img src="../../../.gitbook/assets/v2-can-120termination.png" alt=""><figcaption><p>Cartographer v2 Pads to enable 120 Ohm Resistor</p></figcaption></figure>

#### **Cartographer w/ Input Shaper (USB/CAN Hybrid)**

This version of the probe is terminated with a 120ohm resistor by default. if you want to remove the 120 Ohm resistor, use a soldering iron to remove the resistor that can be seen below.&#x20;

<figure><img src="../../../.gitbook/assets/V3-120Ohm-Resistor.png" alt=""><figcaption><p>Position of 120Ohm Resistor</p></figcaption></figure>




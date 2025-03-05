# Hardware Setup

{% hint style="info" %}
If you bought a Flat Pack and need to assemble your probe, please visit [assembly](../../assembly/ "mention") for instructions. The correct orientation of the MCU and Coilboard is vital.&#x20;
{% endhint %}



## Mount Cartographer

Note there are two different versions of Cartographer, a USB and a CAN version. These will be clearly defined in the section titles when they differentiate. Please make sure you follow the correct guide for the installation of yours. &#x20;

{% hint style="warning" %}
Make sure carto is the range of 2.6 to 3mm to the nozzle
{% endhint %}

To ensure accuracy, we recommend using the measurement jig developed by Esoterical.

This jig also enables easy viewing of the Y offset; simply print it, mount as illustrated below, and you’ll be able to verify your probe’s Z height in relation to the nozzle.

<figure><img src="../../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

{% embed url="https://www.printables.com/model/1060868-cartographer-probe-nozzle-offset-tool" %}

### Location

Cartographer is designed to use the existing mounts available for similar products on the market. The hole spacing is 31.6mm and it takes M3 bolts.

There should be no metal directly above the Cartographer Coil, this is refered too as the keep out zone. There are three STEP files available on our GitHub ([here](https://github.com/Cartographer3D/cartographer-probe/tree/main/STEP)) that highlight this area.&#x20;

The probe can be installed in any orentation, you just need to ensure you set the X and Y offset in the config relative to the probes location to the nozzle. The probe also needs to be perfectly flat, if it is at an angle you will get inconsistant results.&#x20;

Ensure when you are mounting Cartographer that you recess the probe approximatly 3 mm from the Nozzles Z height.

{% hint style="danger" %}
If you use a nozzle brush, ensure that the routing to use that doesnt have your Cartographer travelling over it. I would HIGHLY advise switching to a silicon brush.&#x20;
{% endhint %}

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

<figure><img src="../../../.gitbook/assets/V3-120Ohm-Resistor.png" alt=""><figcaption><p>Position of 120 Ohm Resistor</p></figcaption></figure>




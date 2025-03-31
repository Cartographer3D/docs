# Wiring Diagrams

***

{% hint style="danger" %}
## Cartographer Probes and AFC Lite MMU boards

Currently Carto is not compatible with the current version of AFC-Lite, from our expereince it will fry Cartographers mux chips as from our testing, it seems to spike to 24v on boot, this goes way above our recommended voltage of 5v or maximum of 6.2v. &#x20;

![](../../../.gitbook/assets/image.png)
{% endhint %}

Below are some wiring diagrams for some common CAN boards used with Klipper. Currently we only recommend BigTreeTech boards if you are a novice user.&#x20;

We will expand out the wiring diagrams as time goes on and more boards are released.

{% hint style="warning" %}
You may not be able to flash your EBB36 or EBB42 over CanBus while Cartographer is connected, simply unplug the CAN H and CAN L pin, flash it and then re-connect after.&#x20;
{% endhint %}

## BigTreeTech EBB36

### Standard & Low Profile

<figure><img src="../../../.gitbook/assets/Cartographer3D_CAN_Wiring_EBB36.webp" alt=""><figcaption><p>EBB36 &#x26; Cartographer CAN Probe (Low Profile / Standard)</p></figcaption></figure>

{% hint style="info" %}
You should apply a twist to your CAN H and CAN L cables every 24mm
{% endhint %}



### Right Angle

<figure><img src="../../../.gitbook/assets/EBB36.png" alt=""><figcaption><p>EBB36 &#x26; Cartographer CAN Probe (Right Angle)</p></figcaption></figure>

{% hint style="info" %}
You should apply a twist to your CAN H and CAN L cables every 24mm
{% endhint %}

## BigTreeTech EBB42

### Standard & Low Profile

<figure><img src="../../../.gitbook/assets/Cartographer3D_CAN_Wiring_EBB42.webp" alt=""><figcaption><p>EBB42 &#x26; Cartographer CAN Probe (Low Profile / Standard)</p></figcaption></figure>

{% hint style="info" %}
You should apply a twist to your CAN H and CAN L cables every 24mm
{% endhint %}

### Right Angle

<figure><img src="../../../.gitbook/assets/Cartographer3D_CAN_Wiring_EBB42_Reversed.webp" alt=""><figcaption><p>EBB42 &#x26; Cartographer CAN Probe (Right Angle)</p></figcaption></figure>

{% hint style="info" %}
You should apply a twist to your CAN H and CAN L cables every 24mm
{% endhint %}

## SB2209/SB2240 (via SB0000 breakout board)

### Standard & Low Profile

<figure><img src="../../../.gitbook/assets/Cartographer3D_CAN_Wiring_SB0000.webp" alt=""><figcaption><p>SB0000 &#x26; Cartographer CAN Probe (Standard / Low Profile)</p></figcaption></figure>

{% hint style="info" %}
You should apply a twist to your CAN H and CAN L cables every 24mm
{% endhint %}

### Right Angle

<figure><img src="../../../.gitbook/assets/SB.png" alt=""><figcaption><p>SB0000 &#x26; Cartographer CAN Probe (Right Angle)</p></figcaption></figure>

{% hint style="info" %}
You should apply a twist to your CAN H and CAN L cables every 24mm
{% endhint %}

## USB Wiring

<figure><img src="https://github.com/user-attachments/assets/1c082c5d-44ff-43e1-b1bf-f70b4249a490" alt=""><figcaption></figcaption></figure>

Wiring for the USB connector is in order

* Ground
* DATA +
* DATA -
* 5V

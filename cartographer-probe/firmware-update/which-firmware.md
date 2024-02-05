---
description: Guide to flashing your Cartographer probe with new or updated firmware.
---

# Which Firmware?

Which firmware should I use?&#x20;

Selecting the correct firwmare is essential for the operation of the probe, please check which probe you have, and which mode it is being used in and cross reference the table below.&#x20;

### Cartographer v1 RP2040

<table><thead><tr><th width="123">Mode</th><th width="176">Firmware</th><th width="89">Link</th><th>Notes</th></tr></thead><tbody><tr><td>USB</td><td>carto-rp2040.uf2</td><td><a href="https://github.com/Cartographer3D/cartographer-klipper/tree/master/firmware/v1">GitHub</a></td><td>Only USB Compatible - No Katapult bootloader required</td></tr></tbody></table>

### Cartographer v2 w/ Input Shaper (USB or CAN)

With Cartographer v2, the device will only work in the mode that it was purchased. This is a hardware limitation. The CAN Probe can be forced to work in USB Mode, but is unreliable and requires hardware modifications, this is not something we recommend right now.&#x20;

{% hint style="info" %}
You need to use both a bootloader, and firmware. When updating, it is currently only neccessary to flash the Firmware.
{% endhint %}

#### USB Version (for Klipper pre-version v0.12.0-85)&#x20;

[Link to folder with Firmware](https://github.com/Cartographer3D/cartographer-klipper/tree/master/firmware/v2/for%20Klipper%20older%20than%20v0-12-0-85)

<table><thead><tr><th width="216">Firmware</th><th width="127">Type</th><th width="140">Address</th><th>Notes</th></tr></thead><tbody><tr><td><h4>Katapult_USB.bin</h4></td><td>Bootloader (Katapult)</td><td>0x08000000</td><td></td></tr><tr><td><h4>Cartographer_USB.bin</h4></td><td>Firmware (Klipper)</td><td>0x08002000</td><td>8KiB Offset required, so needs ot 0x08002000</td></tr></tbody></table>

#### USB Version (for Klipper pre-version v0.12.0-85 and later)

[Link to folder with Firmware](https://github.com/Cartographer3D/cartographer-klipper/tree/master/firmware/v2)

#### USB Version

<table><thead><tr><th width="213">Firmware</th><th width="127">Type</th><th width="140">Address</th><th>Notes</th></tr></thead><tbody><tr><td><h4>Katapult_USB.bin</h4></td><td>Bootloader (Katapult)</td><td>0x08000000</td><td></td></tr><tr><td><h4>Cartographer_USB.bin</h4></td><td>Firmware (Klipper)</td><td>0x08002000</td><td>8KiB Offset required, so needs ot 0x08002000</td></tr></tbody></table>

#### CAN Version  (for Klipper pre-version v0.12.0-85)&#x20;

[Link to folder with Firmware](https://github.com/Cartographer3D/cartographer-klipper/tree/master/firmware/v2/for%20Klipper%20older%20than%20v0-12-0-85)

<table><thead><tr><th width="229">Firmware</th><th>Type</th><th>Address</th><th width="95" align="center">Baudrate</th><th>Notes</th></tr></thead><tbody><tr><td>Katapult_CAN_100000.bin </td><td>Bootloader (Katapult)</td><td>0x08000000</td><td align="center">1M</td><td></td></tr><tr><td>Cartographer_CAN_1000000_8kib_offset.bin </td><td>Firmware (Klipper)</td><td>0x08002000</td><td align="center">1M</td><td>8KiB Offset required, so needs ot 0x08002000</td></tr><tr><td>Cartographer_CAN_250000_8kib_offset.bin </td><td>Firmware (Klipper)</td><td>0x08002000</td><td align="center">250K</td><td>8KiB Offset required, so needs ot 0x08002000</td></tr><tr><td>Cartographer_CAN_500000_8kib_offset.bin</td><td>Firmware (Klipper)</td><td>0x08002000</td><td align="center">500K</td><td>8KiB Offset required, so needs ot 0x08002000</td></tr></tbody></table>

#### CAN Version (for Klipper pre-version v0.12.0-85 and later)

[Link to folder with Firmware](https://github.com/Cartographer3D/cartographer-klipper/tree/master/firmware/v2)

<table><thead><tr><th width="229">Firmware</th><th>Type</th><th>Address</th><th width="95" align="center">Baudrate</th><th>Notes</th></tr></thead><tbody><tr><td>Katapult_CAN_100000.bin</td><td>Bootloader (Katapult)</td><td>0x08000000</td><td align="center">1M</td><td></td></tr><tr><td>Cartographer_CAN_1000000_8kib_offset.bin</td><td>Firmware (Klipper)</td><td>0x08002000</td><td align="center">1M</td><td>8KiB Offset required, so needs ot 0x08002000</td></tr><tr><td>Cartographer_CAN_250000_8kib_offset.bin</td><td>Firmware (Klipper)</td><td>0x08002000</td><td align="center">250K</td><td>8KiB Offset required, so needs ot 0x08002000</td></tr><tr><td>Cartographer_CAN_500000_8kib_offset.bin</td><td>Firmware (Klipper)</td><td>0x08002000</td><td align="center">500K</td><td>8KiB Offset required, so needs ot 0x08002000</td></tr></tbody></table>



### Cartographer v3 w/ Input Shaper (USB/CAN)

Cartographer v3 by default will come pre-flashed for CAN. You can switch between both USB and CAN modes via firmware with no hardware modification required.&#x20;

{% hint style="info" %}
You need to use both a bootloader, and firmware. When updating, it is currently only neccessary to flash the Firmware.
{% endhint %}

#### USB / CAN Version  (for Klipper pre-version v0.12.0-85)

[Link to folder with Firmware](https://github.com/Cartographer3D/cartographer-klipper/tree/master/firmware/v3/for%20Klipper%20older%20than%20v0-12-0-85)

<table><thead><tr><th>Firmware</th><th width="125">Type</th><th width="137">Address</th><th width="105" align="center">Baudrate</th><th>Note</th></tr></thead><tbody><tr><td>Full_Cartographer_USB_v3.bin</td><td>Bootloader &#x26; Firmware Combined</td><td>0x08000000</td><td align="center">USB</td><td>This is the only firmware you need, you don't need to flash the bootloader or firmware seperately. <br><br><strong>DO NOT FLASH VIA KATAPULT.</strong></td></tr><tr><td>Full_Cartographer_CAN_1M_v3.bin</td><td>Bootloader &#x26; Firmware Combined</td><td>0x08000000</td><td align="center">1M</td><td>This is the only firmware you need, you don't need to flash the bootloader or firmware seperately. <br><br><strong>DO NOT FLASH VIA KATAPULT.</strong></td></tr><tr><td>Katapult_250k_withSwitch.bin </td><td>Bootloader (Katapult)</td><td>0x08000000</td><td align="center">250K</td><td>This is the Katapult bootloader, do not flash this via Katapult.</td></tr><tr><td>Katapult_500k_withSwitch.bin </td><td>Bootloader (Katapult)</td><td>0x08000000</td><td align="center">500K</td><td>This is the Katapult bootloader, do not flash this via Katapult.</td></tr><tr><td>Katapult_USB.bin</td><td>Bootloader (Katapult)</td><td>0x08000000</td><td align="center">USB</td><td>This is the Katapult bootloader, do not flash this via Katapult.</td></tr><tr><td>Cartographer_CAN_250000_8kib_offset.bin </td><td>Firmware (Klipper)</td><td>0x08002000</td><td align="center">250K</td><td>8KiB Offset required, so needs ot 0x08002000</td></tr><tr><td>Cartographer_CAN_500000_8kib_offset.bin </td><td>Firmware (Klipper)</td><td>0x08002000</td><td align="center">500K</td><td>8KiB Offset required, so needs ot 0x08002000</td></tr><tr><td>Cartographer_CAN_1000000_8kib_offset.bin </td><td>Firmware (Klipper)</td><td>0x08002000</td><td align="center">1M</td><td>8KiB Offset required, so needs ot 0x08002000</td></tr><tr><td>Cartographer_USB_v3_8kib_offset.bin </td><td>Firmware (Klipper)</td><td>0x08002000</td><td align="center">USB</td><td>8KiB Offset required, so needs ot 0x08002000</td></tr></tbody></table>

#### USB / CAN Version (for Klipper pre-version v0.12.0-85 and later)

[Link to folder with Firmware](https://github.com/Cartographer3D/cartographer-klipper/tree/master/firmware/v3)

<table><thead><tr><th>Firmware</th><th width="125">Type</th><th width="137">Address</th><th width="105" align="center">Baudrate</th><th>Note</th></tr></thead><tbody><tr><td>Full_Cartographer_USB_v3.bin</td><td>Bootloader &#x26; Firmware Combined</td><td>0x08000000</td><td align="center">USB</td><td>This is the only firmware you need, you don't need to flash the bootloader or firmware seperately. <br><br><strong>DO NOT FLASH VIA KATAPULT.</strong></td></tr><tr><td>Full_Cartographer_CAN_1M_v3.bin</td><td>Bootloader &#x26; Firmware Combined</td><td>0x08000000</td><td align="center">1M</td><td>This is the only firmware you need, you don't need to flash the bootloader or firmware seperately. <br><br><strong>DO NOT FLASH VIA KATAPULT.</strong></td></tr><tr><td>Katapult_250k_withSwitch.bin </td><td>Bootloader (Katapult)</td><td>0x08000000</td><td align="center">250K</td><td>This is the Katapult bootloader, do not flash this via Katapult.</td></tr><tr><td>Katapult_500k_withSwitch.bin </td><td>Bootloader (Katapult)</td><td>0x08000000</td><td align="center">500K</td><td>This is the Katapult bootloader, do not flash this via Katapult.</td></tr><tr><td>Katapult_USB.bin</td><td>Bootloader (Katapult)</td><td>0x08000000</td><td align="center">USB</td><td>This is the Katapult bootloader, do not flash this via Katapult.</td></tr><tr><td>Katapult_1m_withSwitch.bin</td><td>Bootloader (Katapult)</td><td>0x08000000</td><td align="center">1M</td><td>This is the Katapult bootloader, do not flash this via Katapult.</td></tr><tr><td>Cartographer_CAN_250000_8kib_offset.bin </td><td>Firmware (Klipper)</td><td>0x08002000</td><td align="center">250K</td><td>8KiB Offset required, so needs ot 0x08002000</td></tr><tr><td>Cartographer_CAN_500000_8kib_offset.bin </td><td>Firmware (Klipper)</td><td>0x08002000</td><td align="center">500K</td><td>8KiB Offset required, so needs ot 0x08002000</td></tr><tr><td>Cartographer_CAN_1000000_8kib_offset.bin </td><td>Firmware (Klipper)</td><td>0x08002000</td><td align="center">1M</td><td>8KiB Offset required, so needs ot 0x08002000</td></tr><tr><td>Cartographer_USB_v3_8kib_offset.bin </td><td>Firmware (Klipper)</td><td>0x08002000</td><td align="center">USB</td><td>8KiB Offset required, so needs ot 0x08002000</td></tr></tbody></table>

as

---
description: Guide to flashing your Cartographer probe with new or updated firmware.
---

# Which Firmware?

Which firmware should I use?&#x20;

Selecting the correct firwmare is essential for the operation of the probe, please check which probe you have, and which mode it is being used in and cross reference the table below.&#x20;

### Cartographer v2 w/ Input Shaper (USB or CAN)

{% hint style="info" %}

{% endhint %}

#### USB Version (for Klipper pre-version v0.12.0-85)&#x20;

[Link to folder with Firmware](https://github.com/Cartographer3D/cartographer-klipper/tree/master/firmware/v2/for%20Klipper%20older%20than%20v0-12-0-85)

<table><thead><tr><th width="213">Firmware</th><th width="127">Type</th><th width="140">Address</th><th>Notes</th></tr></thead><tbody><tr><td><h4>Katapult_USB.bin</h4></td><td>Bootloader (Katapult)</td><td>0x08000000</td><td></td></tr><tr><td><h4>Cartographer_USB.bin</h4></td><td>Firmware (Klipper)</td><td>0x08002000</td><td>8KiB Offset required, so needs ot 0x08002000</td></tr></tbody></table>

#### USB Version (for Klipper pre-version v0.12.0-85 and later)

[Link to folder with Firmware](https://github.com/Cartographer3D/cartographer-klipper/tree/master/firmware/v2)

#### USB Version

<table><thead><tr><th width="334">Firmware</th><th width="127">Type</th><th width="140">Address</th><th>Notes</th></tr></thead><tbody><tr><td><h4>Katapult_USB.bin</h4></td><td>Bootloader (Katapult)</td><td>0x08000000</td><td></td></tr><tr><td><h4>Cartographer_USB.bin</h4></td><td>Firmware (Klipper)</td><td>0x08002000</td><td>8KiB Offset required, so needs ot 0x08002000</td></tr></tbody></table>

#### CAN Version  (for Klipper pre-version v0.12.0-85)&#x20;

[Link to folder with Firmware](https://github.com/Cartographer3D/cartographer-klipper/tree/master/firmware/v2/for%20Klipper%20older%20than%20v0-12-0-85)

<table><thead><tr><th width="229">Firmware</th><th>Type</th><th>Address</th><th width="95" align="center">Baudrate</th><th>Notes</th></tr></thead><tbody><tr><td>Katapult_CAN_100000.bin </td><td>Bootloader (Katapult)</td><td>0x08000000</td><td align="center">1M</td><td></td></tr><tr><td>Cartographer_CAN_1000000_8kib_offset.bin </td><td>Firmware (Klipper)</td><td>0x08002000</td><td align="center">1M</td><td>8KiB Offset required, so needs ot 0x08002000</td></tr><tr><td>Cartographer_CAN_250000_8kib_offset.bin </td><td>Firmware (Klipper)</td><td>0x08002000</td><td align="center">250K</td><td>8KiB Offset required, so needs ot 0x08002000</td></tr><tr><td>Cartographer_CAN_500000_8kib_offset.bin</td><td>Firmware (Klipper)</td><td>0x08002000</td><td align="center">500K</td><td>8KiB Offset required, so needs ot 0x08002000</td></tr></tbody></table>

#### CAN Version (for Klipper pre-version v0.12.0-85 and later)

[Link to folder with Firmware](https://github.com/Cartographer3D/cartographer-klipper/tree/master/firmware/v2)

<table><thead><tr><th width="229">Firmware</th><th>Type</th><th>Address</th><th width="95" align="center">Baudrate</th><th>Notes</th></tr></thead><tbody><tr><td>Katapult_CAN_100000.bin</td><td>Bootloader (Katapult)</td><td>0x08000000</td><td align="center">1M</td><td></td></tr><tr><td>Cartographer_CAN_1000000_8kib_offset.bin</td><td>Firmware (Klipper)</td><td>0x08002000</td><td align="center">1M</td><td>8KiB Offset required, so needs ot 0x08002000</td></tr><tr><td>Cartographer_CAN_250000_8kib_offset.bin</td><td>Firmware (Klipper)</td><td>0x08002000</td><td align="center">250K</td><td>8KiB Offset required, so needs ot 0x08002000</td></tr><tr><td>Cartographer_CAN_500000_8kib_offset.bin</td><td>Firmware (Klipper)</td><td>0x08002000</td><td align="center">500K</td><td>8KiB Offset required, so needs ot 0x08002000</td></tr></tbody></table>



###

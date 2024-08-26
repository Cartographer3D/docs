# Cartographer v2 or v3 w/ Input Shaper (USB/CAN)

### Firmware

Cartographer v3 by default will come pre-flashed for CAN. You can switch between both USB and CAN modes via firmware with no hardware modification required.&#x20;

{% hint style="info" %}
You need to use both a bootloader, and firmware. When updating, it is currently only neccessary to flash the Firmware.
{% endhint %}

Firmware Build 4.0.0 is compatible with both lis2dw and ADXL345 based probes. and is available from the GitHub repository. If you have cloned the firmware down to your Pi, it is already available.

### Bootloaders

Using the correct bootloader is essential for this the probe to work in the correct mode. The bootloader used is Katapult, this also allows for easy updating of your firmware.&#x20;

<mark style="color:red;">**Note: These files should only be written using**</mark> [<mark style="color:red;">**DFU Mode**</mark>](../../cartographer-with-input-shaper/update-via-dfu-mode.md) <mark style="color:red;">**or a**</mark> [<mark style="color:red;">**ST-Link**</mark>](../../cartographer-with-input-shaper/update-via-stlink.md)

To navigate to these on your Pi, they are located in the following directory - \
\
&#x20;`/cartographer-klipper/firmware/v2-v3/`

| Firmware                                                                                                                   | Type                  | Address    | Baudrate | Note                                                             |
| -------------------------------------------------------------------------------------------------------------------------- | --------------------- | ---------- | :------: | ---------------------------------------------------------------- |
| [Katapult\_250k.bin](https://github.com/Cartographer3D/cartographer-klipper/blob/master/firmware/v2-v3/Katapult\_250k.bin) | Bootloader (Katapult) | 0x08000000 |   250K   | This is the Katapult bootloader, do not flash this via Ka        |
| [Katapult\_500k.bin](https://github.com/Cartographer3D/cartographer-klipper/blob/master/firmware/v2-v3/Katapult\_500k.bin) | Bootloader (Katapult) | 0x08000000 |   500K   | This is the Katapult bootloader, do not flash this via Katapult. |
| [Katapult\_1m.bin](https://github.com/Cartographer3D/cartographer-klipper/blob/master/firmware/v2-v3/Katapult\_1m.bin)     | Bootloader (Katapult) | 0x08000000 |    1M    | This is the Katapult bootloader, do not flash this via Katapult. |
| [Katapult\_USB.bin](https://github.com/Cartographer3D/cartographer-klipper/blob/master/firmware/v2-v3/Katapult\_USB.bin)   | Bootloader (Katapult) | 0x08000000 |    USB   | This is the Katapult bootloader, do not flash this via Katapult. |

### Cartographer Firmware

The following firmware files must be flashed at 0x08002000 if using DFU mode, or written directly via Katapult. These will not work without a Bootloader. \


To navigate to these on your Pi, they are located in the following directory - \
\
&#x20;`/cartographer-klipper/firmware/v2-v3/`

<table><thead><tr><th width="269">Firmware</th><th width="75">Type</th><th width="140">Address</th><th width="78" align="center">Baudrate</th><th>Note</th></tr></thead><tbody><tr><td><a href="https://github.com/Cartographer3D/cartographer-klipper/blob/master/firmware/v2-v3/Cartographer_CAN_250000_8kib_offset.bin">Cartographer_CAN_250000_8kib_offset.bin</a></td><td>Firmware Pre Survey</td><td>0x08002000</td><td align="center">250K</td><td>Firmware Build 4.0.0 - Compatible with ADXL &#x26; lis2dw Hybrid Probes.</td></tr><tr><td><a href="https://github.com/Cartographer3D/cartographer-klipper/blob/master/firmware/v2-v3/Cartographer_CAN_500000_8kib_offset.bin">Cartographer_CAN_500000_8kib_offset.bin</a></td><td>Firmware Pre Survey</td><td>0x08002000</td><td align="center">500K</td><td>Firmware Build 4.0.0 - Compatible with ADXL &#x26; lis2dw Hybrid Probes.</td></tr><tr><td><a href="https://github.com/Cartographer3D/cartographer-klipper/blob/master/firmware/v2-v3/Cartographer_CAN_1000000_8kib_offset.bin">Cartographer_CAN_1000000_8kib_offset.bin</a></td><td>Firmware Pre Survey</td><td>0x08002000</td><td align="center">1M</td><td>Firmware Build 4.0.0 - Compatible with ADXL &#x26; lis2dw Hybrid Probes.</td></tr><tr><td><a href="https://github.com/Cartographer3D/cartographer-klipper/blob/master/firmware/v2-v3/Cartographer_USB_4_0_0_8kib_offset.bin">Cartographer_USB_4_0_0_8kib_offset.bin</a></td><td>Firmware Pre Survey</td><td>0x08002000</td><td align="center">USB</td><td>Firmware Build 4.0.0 - Compatible with ADXL &#x26; lis2dw Hybrid Probes.</td></tr><tr><td><a href="https://github.com/Cartographer3D/cartographer-klipper/blob/master/firmware/v2-v3/survey/Survey_Cartographer_CAN_250000_8kib_offset.bin">Survey_Cartographer_CAN_250000_8kib_offset.bin</a></td><td>Survey Firmware</td><td>0x08002000</td><td align="center">250k</td><td>Cartographer Survey Firmware (uses scanner.py)</td></tr><tr><td><a href="https://github.com/Cartographer3D/cartographer-klipper/blob/master/firmware/v2-v3/survey/Survey_Cartographer_CAN_500000_8kib_offset.bin">Survey_Cartographer_CAN_500000_8kib_offset.bin</a></td><td>Survey Firmware</td><td>0x08002000</td><td align="center">500k</td><td>Cartographer Survey Firmware (uses scanner.py)</td></tr><tr><td><a href="https://github.com/Cartographer3D/cartographer-klipper/blob/master/firmware/v2-v3/survey/Survey_Cartographer_CAN_1000000_8kib_offset.bin">Survey_Cartographer_CAN_1000000_8kib_offset.bin</a></td><td>Survey Firmware</td><td>0x08002000</td><td align="center">1M</td><td>Cartographer Survey Firmware (uses scanner.py)</td></tr><tr><td><a href="https://github.com/Cartographer3D/cartographer-klipper/blob/master/firmware/v2-v3/survey/Survey_Cartographer_USB_8kib_offset.bin">Survey_Cartographer_USB_8kib_offset.bin</a></td><td>Survey Firmware</td><td>0x08002000</td><td align="center">USB</td><td>Cartographer Survey Firmware (uses scanner.py)</td></tr></tbody></table>

### &#x20;



### Combined Firmwares

These firmware files contain both the Katapult Bootloader, and Cartographer Firmware.  \
\
These WILL NOT work if they are flashed via Katapult mode, please either use [STLink ](../../cartographer-with-input-shaper/update-via-stlink.md)or [DFU Mode](../../cartographer-with-input-shaper/update-via-dfu-mode.md). \
\
To navigate to these on your Pi, they are located in the following directory - \
\
&#x20;`/cartographer-klipper/firmware/v2-v3/combined-firmware`

<table><thead><tr><th>Firmware</th><th width="149">Type</th><th width="155">Address</th><th align="center">Baudrate</th><th>Note</th></tr></thead><tbody><tr><td><a href="https://github.com/Cartographer3D/cartographer-klipper/blob/master/firmware/v2-v3/combined-firmware/Full_Cartographer_CAN_1M_4_0_1.bin">Full_Cartographer_CAN_1M_4_0_1.bin</a></td><td>Katapult Bootloader + Cartographer Firmware.</td><td>0x08000000</td><td align="center">1M</td><td>Firmware Build 4.0.0 - Compatible with ADXL &#x26; lis2dw Hybrid Probes.</td></tr><tr><td><a href="https://github.com/Cartographer3D/cartographer-klipper/blob/master/firmware/v2-v3/combined-firmware/Full_Cartographer_USB_4_0_0.bin">Full_Cartographer_USB_4_0_0.bin</a></td><td>Katapult Bootloader + Cartographer Firmware.</td><td>0x08000000</td><td align="center">USB</td><td>Firmware Build 4.0.0 - Compatible with ADXL &#x26; lis2dw Hybrid Probes.</td></tr></tbody></table>

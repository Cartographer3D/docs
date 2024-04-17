# Cartographer v3 w/ Input Shaper (USB/CAN)

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
&#x20;`/cartographer-klipper/firmware/v3/`

| Firmware                                                                                                                                                        | Type                  | Address    | Baudrate | Note                                                             |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------- | ---------- | :------: | ---------------------------------------------------------------- |
| <h4><a href="https://github.com/Cartographer3D/cartographer-klipper/blob/master/firmware/v3/Katapult_250k_withSwitch.bin">Katapult_250k_withSwitch.bin</a></h4> | Bootloader (Katapult) | 0x08000000 |   250K   | This is the Katapult bootloader, do not flash this via Katapult. |
| <h4><a href="https://github.com/Cartographer3D/cartographer-klipper/blob/master/firmware/v3/Katapult_500k_withSwitch.bin">Katapult_500k_withSwitch.bin</a></h4> | Bootloader (Katapult) | 0x08000000 |   500K   | This is the Katapult bootloader, do not flash this via Katapult. |
| <h4><a href="https://github.com/Cartographer3D/cartographer-klipper/blob/master/firmware/v3/Katapult_1m_withSwitch.bin">Katapult_1m_withSwitch.bin</a></h4>     | Bootloader (Katapult) | 0x08000000 |    1M    | This is the Katapult bootloader, do not flash this via Katapult. |
| <h4><a href="https://github.com/Cartographer3D/cartographer-klipper/blob/master/firmware/v3/Katapult_USB.bin">Katapult_USB.bin</a></h4>                         | Bootloader (Katapult) | 0x08000000 |    USB   | This is the Katapult bootloader, do not flash this via Katapult. |

### Cartographer Firmware

The following firmware files must be flashed at 0x08002000 if using DFU mode, or written directly via Katapult. These will not work without a Bootloader. \


To navigate to these on your Pi, they are located in the following directory - \
\
&#x20;`/cartographer-klipper/firmware/v3/`

<table><thead><tr><th>Firmware</th><th>Type</th><th width="155">Address</th><th align="center">Baudrate</th><th>Note</th></tr></thead><tbody><tr><td><h4>COMING SOON</h4></td><td>Bootloader (Katapult)</td><td>0x08002000</td><td align="center">250K</td><td>Firmware Build 4.0.0 - Compatible with ADXL &#x26; lis2dw Hybrid Probes.</td></tr><tr><td><h4>COMING SOON</h4></td><td>Bootloader (Katapult)</td><td>0x08002000</td><td align="center">500K</td><td>Firmware Build 4.0.0 - Compatible with ADXL &#x26; lis2dw Hybrid Probes.</td></tr><tr><td><h4><a href="https://github.com/Cartographer3D/cartographer-klipper/blob/master/firmware/v3/Cartographer_CAN_1000000_8kib_offset.bin">Cartographer_CAN_1000000_8kib_offset.bin</a></h4></td><td>Bootloader (Katapult)</td><td>0x08002000</td><td align="center">1M</td><td>Firmware Build 4.0.0 - Compatible with ADXL &#x26; lis2dw Hybrid Probes.</td></tr><tr><td><h4><a href="https://github.com/Cartographer3D/cartographer-klipper/blob/master/firmware/v3/Cartographer_USB_4_0_0_8kib_offset.bin">Cartographer_USB_4_0_0_8kib_offset.bin</a></h4></td><td>Bootloader (Katapult)</td><td>0x08002000</td><td align="center">USB</td><td>Firmware Build 4.0.0 - Compatible with ADXL &#x26; lis2dw Hybrid Probes.</td></tr></tbody></table>

### Deployer Firmware

These firmware files contain both the Katapult Bootloader, and Cartographer Firmware.  \
\
These WILL NOT work if they are flashed via Katapult mode, please either use [STLink ](../../cartographer-with-input-shaper/update-via-stlink.md)or [DFU Mode](../../cartographer-with-input-shaper/update-via-dfu-mode.md). \
\
To navigate to these on your Pi, they are located in the following directory - \
\
&#x20;`/cartographer-klipper/firmware/v3/DEPLOYER FIRMWARE - DFU MODE ONLY NOT KATAPULT`

<table><thead><tr><th>Firmware</th><th width="149">Type</th><th width="155">Address</th><th align="center">Baudrate</th><th>Note</th></tr></thead><tbody><tr><td><h4><a href="https://github.com/Cartographer3D/cartographer-klipper/blob/master/firmware/v3/DEPLOYER%20FRIMWARE%20-%20DFU%20MODE%20ONLY%20NOT%20KATAPULT/Full_Cartographer_CAN_1M_4_0_0.bin">Full_Cartographer_CAN_1M_4_0_0.bin</a></h4></td><td>Katapult Bootloader + Cartographer Firmware.</td><td>0x08000000</td><td align="center">1M</td><td>Firmware Build 4.0.0 - Compatible with ADXL &#x26; lis2dw Hybrid Probes.</td></tr><tr><td><h4><a href="https://github.com/Cartographer3D/cartographer-klipper/blob/master/firmware/v3/DEPLOYER%20FRIMWARE%20-%20DFU%20MODE%20ONLY%20NOT%20KATAPULT/Full_Cartographer_USB_4_0_0.bin">Full_Cartographer_USB_4_0_0.bin</a></h4></td><td>Katapult Bootloader + Cartographer Firmware.</td><td>0x08000000</td><td align="center">USB</td><td>Firmware Build 4.0.0 - Compatible with ADXL &#x26; lis2dw Hybrid Probes.</td></tr></tbody></table>

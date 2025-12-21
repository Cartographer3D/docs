---
description: Guide to flashing your Cartographer probe with new or updated firmware.
---

# ⬆️ Firmware

### Which Firmware Should I use? <a href="#which-firmware-should-i-use" id="which-firmware-should-i-use"></a>

Selecting the correct firmware is essential for the operation of the probe, please check which probe you have, and which mode it is being used in and cross reference the table below.

#### Cartographer v1 RP2040 <a href="#cartographer-v1-rp2040" id="cartographer-v1-rp2040"></a>

| Mode | Firmware         | Link                                                                                                  | Notes                                                 |
| ---- | ---------------- | ----------------------------------------------------------------------------------------------------- | ----------------------------------------------------- |
| USB  | carto-rp2040.uf2 | [GitHub](https://github.com/Cartographer3D/cartographer-klipper/tree/master/firmware/v1%20-%20rp2040) | Only USB Compatible - No Katapult Bootloader Required |

#### Cartographer v2 w/ Input Shaper (USB or CAN) <a href="#cartographer-v2-w-input-shaper-usb-or-can" id="cartographer-v2-w-input-shaper-usb-or-can"></a>

With Cartographer v2, the device will only work in the mode that it was purchased. This is a hardware limitation. The CAN Probe can be forced to work in USB Mode, but is unreliable and requires hardware modifications, this is not something we recommend right now.

**USB Version**

| Firmware                                                                                                                                                                              | Type                  | Address    | Notes                                           |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------- | ---------- | ----------------------------------------------- |
| [Katapult\_USB.bin](https://github.com/Cartographer3D/cartographer-klipper/blob/master/firmware/v2-v3/Katapult_USB.bin)                                                               | Bootloader (Katapult) | 0x08000000 |                                                 |
| [Survey\_Cartographer\_USB\_8kib\_offset.bin](https://github.com/Cartographer3D/cartographer-klipper/blob/master/firmware/v2-v3/survey/5.1.0/Survey_Cartographer_USB_8kib_offset.bin) | Firmware (Klipper)    | 0x08002000 | 8KiB Offset required, so needs to be 0x08002000 |

**CAN Version**

| Firmware                                                                                                                                                                                               | Type                  | Address    | Baudrate | Notes                                           |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | --------------------- | ---------- | -------- | ----------------------------------------------- |
| [Katapult\_1m.bin](https://github.com/Cartographer3D/cartographer-klipper/blob/master/firmware/v2-v3/Katapult_1m.bin)                                                                                  | Bootloader (Katapult) | 0x08000000 | 1M       |                                                 |
| [Katapult\_250k.bin](https://github.com/Cartographer3D/cartographer-klipper/blob/master/firmware/v2-v3/Katapult_250k.bin)                                                                              | Bootloader (Katapult) | 0x08000000 | 250k     |                                                 |
| [Katapult\_500k.bin](https://github.com/Cartographer3D/cartographer-klipper/blob/master/firmware/v2-v3/Katapult_500k.bin)                                                                              | Bootloader (Katapult) | 0x08000000 | 500k     |                                                 |
| [Survey\_Cartographer\_CAN\_1000000\_8kib\_offset.bin](https://github.com/Cartographer3D/cartographer-klipper/blob/master/firmware/v2-v3/survey/5.1.0/Survey_Cartographer_CAN_1000000_8kib_offset.bin) | Firmware (Klipper)    | 0x08002000 | 1M       | 8KiB Offset required, so needs to be 0x08002000 |
| [Survey\_Cartographer\_CAN\_250000\_8kib\_offset.bin](https://github.com/Cartographer3D/cartographer-klipper/blob/master/firmware/v2-v3/survey/5.1.0/Survey_Cartographer_CAN_250000_8kib_offset.bin)   | Firmware (Klipper)    | 0x08002000 | 250K     | 8KiB Offset required, so needs to be 0x08002000 |
| [Survey\_Cartographer\_CAN\_500000\_8kib\_offset.bin](https://github.com/Cartographer3D/cartographer-klipper/blob/master/firmware/v2-v3/survey/5.1.0/Survey_Cartographer_CAN_500000_8kib_offset.bin)   | Firmware (Klipper)    | 0x08002000 | 500K     | 8KiB Offset required, so needs to be 0x08002000 |

#### Cartographer v3 w/ Input Shaper (USB/CAN) <a href="#cartographer-v3-w-input-shaper-usb-can" id="cartographer-v3-w-input-shaper-usb-can"></a>

Cartographer v3 by default will come pre-flashed for CAN. You can switch between both USB and CAN modes via firmware with no hardware modification required.

**USB / CAN Version**

| Firmware                                                                                                                                                                                               | Type                            | Address    | Baudrate | Note                                                                                               |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------- | ---------- | -------- | -------------------------------------------------------------------------------------------------- |
| [Full\_Survey\_Cartographer\_USB\_5\_1\_0.bin](https://github.com/Cartographer3D/cartographer-klipper/blob/master/firmware/v2-v3/combined-firmware/5.1.0/Full_Survey_Cartographer_USB_5_1_0.bin)       | Bootloader & Firmware Combined  | 0x08000000 | N/A      | This is the only firmware you need, you don't need to flash the bootloader or firmware seperately. |
| [Full\_Survey\_Cartographer\_CAN\_1M\_5\_0\_0.bin](https://github.com/Cartographer3D/cartographer-klipper/blob/master/firmware/v2-v3/combined-firmware/5.1.0/Full_Survey_Cartographer_USB_5_1_0.bin)   | Bootloader & Firmware Combined  | 0x08000000 | 1M       | This is the only firmware you need, you don't need to flash the bootloader or firmware seperately. |
| [Katapult\_250k.](https://github.com/Cartographer3D/cartographer-klipper/blob/master/firmware/v2-v3/Katapult_250k.bin)                                                                                 | Bootloader (Katapult)           | 0x08000000 | 250K     |                                                                                                    |
| [Katapult\_500k.bin](https://github.com/Cartographer3D/cartographer-klipper/blob/master/firmware/v2-v3/Katapult_500k.bin)                                                                              | Bootloader (Katapult)           | 0x08000000 | 500K     |                                                                                                    |
| [Katapult\_1m.bin](https://github.com/Cartographer3D/cartographer-klipper/blob/master/firmware/v2-v3/Katapult_1m.bin)                                                                                  | <p>Bootloader<br>(Katapult)</p> | 0x08000000 | 1M       |                                                                                                    |
| [Katapult\_USB.bin](https://github.com/Cartographer3D/cartographer-klipper/blob/master/firmware/v2-v3/Katapult_USB.bin)                                                                                | <p>Bootloader<br>(Katapult)</p> | 0x08000000 | N/A      |                                                                                                    |
| [Survey\_Cartographer\_CAN\_250000\_8kib\_offset.bin](https://github.com/Cartographer3D/cartographer-klipper/blob/master/firmware/v2-v3/survey/5.1.0/Survey_Cartographer_CAN_250000_8kib_offset.bin)   | Firmware (Klipper)              | 0x08002000 | 250K     | 8KiB Offset required, so needs to be 0x08002000                                                    |
| [Survey\_Cartographer\_CAN\_500000\_8kib\_offset.bin](https://github.com/Cartographer3D/cartographer-klipper/blob/master/firmware/v2-v3/survey/5.1.0/Survey_Cartographer_CAN_500000_8kib_offset.bin)   | Firmware (Klipper)              | 0x08002000 | 500K     | 8KiB Offset required, so needs to be 0x08002000                                                    |
| [Survey\_Cartographer\_CAN\_1000000\_8kib\_offset.bin](https://github.com/Cartographer3D/cartographer-klipper/blob/master/firmware/v2-v3/survey/5.1.0/Survey_Cartographer_CAN_1000000_8kib_offset.bin) | Firmware (Klipper)              | 0x08002000 | 1M       | 8KiB Offset required, so needs to be 0x08002000                                                    |
| [Survey\_Cartographer\_USB\_8kib\_offset.bin](https://github.com/Cartographer3D/cartographer-klipper/blob/master/firmware/v2-v3/survey/5.1.0/Survey_Cartographer_USB_8kib_offset.bin)                  | Firmware (Klipper)              | 0x08002000 | N/A      | 8KiB Offset required, so needs to be 0x08002000                                                    |
| [Survey\_Cartographer\_K1\_USB\_8kib\_offset.bin](https://github.com/Cartographer3D/cartographer-klipper/blob/master/firmware/v2-v3/survey/5.1.0/Survey_Cartographer_K1_USB_8kib_offset.bin)           | <p>Firmware<br>(Klipper)</p>    | 0x08002000 | N/A      | Creality K1 Printers ONLY                                                                          |


---
description: Guide to flashing your Cartographer probe with new or updated firmware.
layout:
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: false
  pagination:
    visible: false
---

# ⬆️ Firmware

### Which Firmware Should I use? <a href="#which-firmware-should-i-use" id="which-firmware-should-i-use"></a>

Selecting the correcet firwmare is essential for the operation of the probe, please check which probe you have, and which mode it is being used in and cross reference the table below.

#### Cartographer v1 RP2040 <a href="#cartographer-v1-rp2040" id="cartographer-v1-rp2040"></a>

| Mode | Firmware         | Link                                                                                                  | Notes                                                 |
| ---- | ---------------- | ----------------------------------------------------------------------------------------------------- | ----------------------------------------------------- |
| USB  | carto-rp2040.uf2 | [GitHub](https://github.com/Cartographer3D/cartographer-klipper/tree/master/firmware/v1%20-%20rp2040) | Only USB Compatible - No Katapult Bootloader Required |

#### Cartographer v2 w/ Input Shaper (USB or CAN) <a href="#cartographer-v2-w-input-shaper-usb-or-can" id="cartographer-v2-w-input-shaper-usb-or-can"></a>

With Cartographer v2, the device will only work in the mode that it was purchased. This is a hardware limitation. The CAN Probe can be forced to work in USB Mode, but is unreliable and requires hardware modifications, this is not something we recommend right now.

**USB Version**

| Firmware                                                                                                                                        | Type                  | Address    | Notes                                        |
| ----------------------------------------------------------------------------------------------------------------------------------------------- | --------------------- | ---------- | -------------------------------------------- |
| [**Katapult\_USB.bin**](https://github.com/Cartographer3D/cartographer-klipper/blob/master/firmware/v2/Katapult\_USB.bin)                       | Bootloader (Katapult) | 0x08000000 |                                              |
| [**Cartographer\_USB.bin**](https://github.com/Cartographer3D/cartographer-klipper/blob/master/firmware/v2/Cartographer\_USB\_8kib\_offset.bin) | Firmware (Klipper)    | 0x08002000 | 8KiB Offset required, so needs ot 0x08002000 |

**CAN Version**

| Firmware                                                                                                                                                                           | Type                  | Address    | Baudrate | Notes                                        |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------- | ---------- | -------- | -------------------------------------------- |
| Katapult\_CAN\_100000.bin ([Link](https://github.com/Cartographer3D/cartographer-klipper/blob/master/firmware/v2/Katapult\_CAN\_1000000.bin))                                      | Bootloader (Katapult) | 0x08000000 | 1M       |                                              |
| Cartographer\_CAN\_1000000\_8kib\_offset.bin ([Link](https://github.com/Cartographer3D/cartographer-klipper/blob/master/firmware/v2/Cartographer\_CAN\_1000000\_8kib\_offset.bin)) | Firmware (Klipper)    | 0x08002000 | 1M       | 8KiB Offset required, so needs ot 0x08002000 |
| Cartographer\_CAN\_250000\_8kib\_offset.bin ([Link](https://github.com/Cartographer3D/cartographer-klipper/blob/master/firmware/v2/Cartographer\_CAN\_500000\_8kib\_offset.bin))   | Firmware (Klipper)    | 0x08002000 | 250K     | 8KiB Offset required, so needs ot 0x08002000 |
| Cartographer\_CAN\_500000\_8kib\_offset.bin ([Link](https://github.com/Cartographer3D/cartographer-klipper/blob/master/firmware/v2/Cartographer\_CAN\_500000\_8kib\_offset.bin))   | Firmware (Klipper)    | 0x08002000 | 500K     | 8KiB Offset required, so needs ot 0x08002000 |

#### Cartographer v3 w/ Input Shaper (USB/CAN) <a href="#cartographer-v3-w-input-shaper-usb-can" id="cartographer-v3-w-input-shaper-usb-can"></a>

Cartographer v3 by default will come pre-flashed for CAN. You can switch between both USB and CAN modes via firmware with no hardware modification required.

**USB / CAN Version**

| Firmware                                                                                                                                                                           | Type                           | Address    | Baudrate | Note                                                                                               |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------ | ---------- | -------- | -------------------------------------------------------------------------------------------------- |
| Full\_Cartographer\_USB\_v3.bin ([Link](https://github.com/Cartographer3D/cartographer-klipper/blob/master/firmware/v3/Full\_Cartographer\_USB\_v3.bin))                           | Bootloader & Firmware Combined | 0x08000000 | n/a      | This is the only firmware you need, you don't need to flash the bootloader or firmware seperately. |
| Full\_Cartographer\_CAN\_1M\_v3.bin ([Link](https://github.com/Cartographer3D/cartographer-klipper/blob/master/firmware/v3/Full\_Cartographer\_CAN\_1M\_v3.bin))                   | Bootloader & Firmware Combined | 0x08000000 | 1M       | This is the only firmware you need, you don't need to flash the bootloader or firmware seperately. |
| Katapult\_250k\_withSwitch.bin ([Link](https://github.com/Cartographer3D/cartographer-klipper/blob/master/firmware/v3/Katapult\_250k\_withSwitch.bin))                             | Bootloader (Katapult)          | 0x08000000 | 250K     | 8KiB Offset required, so needs ot 0x08002000                                                       |
| Katapult\_500k\_withSwitch.bin ([Link](https://github.com/Cartographer3D/cartographer-klipper/blob/master/firmware/v3/Katapult\_500k\_withSwitch.bin))                             | Bootloader (Katapult)          | 0x08000000 | 500K     | 8KiB Offset required, so needs ot 0x08002000                                                       |
| Cartographer\_CAN\_250000\_8kib\_offset.bin ([Link](https://github.com/Cartographer3D/cartographer-klipper/blob/master/firmware/v3/Cartographer\_CAN\_250000\_8kib\_offset.bin))   | Firmware (Klipper)             | 0x08002000 | 250K     | 8KiB Offset required, so needs ot 0x08002000                                                       |
| Cartographer\_CAN\_500000\_8kib\_offset.bin ([Link](https://github.com/Cartographer3D/cartographer-klipper/blob/master/firmware/v3/Cartographer\_CAN\_500000\_8kib\_offset.bin))   | Firmware (Klipper)             | 0x08002000 | 500K     | 8KiB Offset required, so needs ot 0x08002000                                                       |
| Cartographer\_CAN\_1000000\_8kib\_offset.bin ([Link](https://github.com/Cartographer3D/cartographer-klipper/blob/master/firmware/v3/Cartographer\_CAN\_1000000\_8kib\_offset.bin)) | Firmware (Klipper)             | 0x08002000 | 1M       | 8KiB Offset required, so needs ot 0x08002000                                                       |
| Cartographer\_USB\_v3\_8kib\_offset.bin ([Link](https://github.com/Cartographer3D/cartographer-klipper/blob/master/firmware/v3/Cartographer\_USB\_v3\_8kib\_offset.bin))           | Firmware (Klipper)             | 0x08002000 | n/a      | 8KiB Offset required, so needs ot 0x08002000                                                       |


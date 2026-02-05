# Re-Flashing

## Prerequisites

You must have the Cartographer Firmware repository, for future updates you will also need Katapult on your Pi, if you do not have these please connect via SSH and run the following command.&#x20;

```bash
cd ~
if [ -d ~/cartographer_firmware/ ]; then
    echo "Cartographer Firmware Exists - Updating Repository"
    cd ~/cartographer_firmware/
    git pull
else
    git clone https://github.com/Cartographer3D/cartographer_firmware.git
fi
cd ~
if [ -d ~/katapult/ ]; then
    echo "Katapult Exists - Updating Repository"
    cd ~/katapult/
    git pull
else
    git clone https://github.com/Arksine/katapult.git
fi
```

### Updating Cartographer via DFU

Prior to flashing, you will need to following tools

* 2 x Ferrous Tweezers (or any conductive tool to bridge the two pads)
* 1 x USB Cable terminated to work w/ Catographer

**Entering DFU Mode**

{% tabs %}
{% tab title="Cartographer V3" %}
To enter DFU Mode, it can be a bit fiddly, but once you get the knack of it, it's fairly simple.

Plug your USB cable into the device you will be flashing from and your Cartographer probe, this can be either a seprate Windows PC, Mac, or a Linux machine, or the device you run your 3D Printer off.

Using your ferrous tweezers, or similar use one to bridge pads 1 (boot0), once you have a solid contact on those tap pad 2 (reset) with your other ferrous tool.

<figure><img src="../../.gitbook/assets/image (70).png" alt=""><figcaption></figcaption></figure>

If you have done this correctly, your device should have entered DFU Mode.
{% endtab %}

{% tab title="Cartographer V4" %}
To enter DFU Mode, it can be a bit fiddly but with V4 due to the use of holes rather than pads it is considerably easier, but once you get the knack of it, it's fairly simple.

<figure><img src="../../.gitbook/assets/image (71).png" alt=""><figcaption></figcaption></figure>

Firstly using the supplied USB cable, plug this into the Cartographer (Molex Sherlock) connector.

Then using your ferrous tweezers or similar, bridge the holes in box 1 (BT0 & 3V3) and then while still bridging those holes plug in your Cartographer V4 via the USB connector of the cable into the device you will be flashing from this can be either a separate Windows PC, Mac, or a Linux machine, or the device you run your 3D Printer off such as a Raspberry Pi. \
\
This should then show the V4 in DFU mode.
{% endtab %}
{% endtabs %}

If you have done this correctly, your device should have entered DFU Mode.

To check,

* Linux - follow the following steps
  * SSH in, or load a terminal shell.
  * type `lsusb` in your bash shell, it should list a device in DFU Mode
  * One of the options should be `Bus 001 Device 004: ID 0483:df11 STMicroelectronics STM Device in DFU Mode` - This (as long as you don't have any other devices in DFU Mode) should be your Cartographer Probe in DFU Mode.
* Windows - follow the following steps
  * Start Menu
  * Search and open "Device Manager"
  * Scroll down to Universal Serial Bus Devices
  * You should see STM32 BOOTLOADER as an option
  * &#x20;![Device Manager view of Cartographer in Bootloader mode.](https://docs.cartographer3d.com/~gitbook/image?url=https%3A%2F%2F3044346320-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FjpCp1KnR8izt0cnWQfZF%252Fuploads%252FlAqyGG4GHQ1siPPWLzpx%252Fimage.png%3Falt%3Dmedia%26token%3Dd24fa98a-010d-4c07-8f63-ed19242d41df\&width=300\&dpr=4\&quality=100\&sign=51e83bcb\&sv=2)

#### Flashing via STM32CubeProgrammer (Windows & MacOS) <a href="#flashing-via-stm32cubeprogrammer-windows-and-macos" id="flashing-via-stm32cubeprogrammer-windows-and-macos"></a>

Download and Install STM32CubeProgrammer from [here](https://www.st.com/en/development-tools/stm32cubeprog.html), I warn you it requires you to sign up for an account.

Version 2.14.0 is recommended due to a known bug in 2.16.0 which causes issues when flashing via STMCubeProgammer - this can be selected from the version 'drop down' on the site.

Open the application, and on the RIGHT side, select the following options and press **Connect**.

<figure><img src="https://docs.cartographer3d.com/~gitbook/image?url=https%3A%2F%2F3044346320-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FjpCp1KnR8izt0cnWQfZF%252Fuploads%252FaSRhGvDO9drIBODQy5Ka%252Fimage.png%3Falt%3Dmedia%26token%3Dc2a1319b-0f86-46ff-ba99-7219d28871f7&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=d19cdb30&#x26;sv=2" alt=""><figcaption><p>STM32CubeProgrammer Settings</p></figcaption></figure>

Once you have connected, Click Open File - you will need to select the Complete Firmware

for V3 this is at `cartographer_firmware/firmware/v2-v3/combined-firmware`

for V4 this is located at `cartographer_firmware/firmware/v4/combined-firmware/6.0.0`

Select the firmware you want to use&#x20;

i.e. `Katapult_plus_CartographerV4_6.0.0__CAN_1M.bin` if you wanted V4, Firmware 6.0.0 for CAN networks with a Baudrate of 1,000,000.&#x20;

<figure><img src="https://docs.cartographer3d.com/~gitbook/image?url=https%3A%2F%2F3044346320-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FjpCp1KnR8izt0cnWQfZF%252Fuploads%252FDZn6JTnVsZ2PPPgG9gvj%252Fimage.png%3Falt%3Dmedia%26token%3D6d63fff9-ea16-4f8b-9a1f-a51905a3992f&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=7fbcbe29&#x26;sv=2" alt=""><figcaption><p>Firmwares Loaded</p></figcaption></figure>

For the Complete (Katapult + Cartographer) Firmware, you need to keep it at the default address of `0x08000000`&#x20;

On each of the firmware's press "Download", starting with Katapult, then with Cartographer. Now press Disconnect in the TOP RIGHT corner.

#### Flashing via DFU Util (Linux Terminal). <a href="#flashing-via-dfu-util-linux-terminal" id="flashing-via-dfu-util-linux-terminal"></a>

SSH into your linux host MCU, ensuring that your Cartographer is plugged in and in DFU Mode.

{% tabs %}
{% tab title="Cartographer V3" %}
Navigate into the correct folder, so if you want to update your v2 or v3 run the following command.

```
cd ~/cartographer_firmware/firmware/v2-v3/combined-firmware/5.0.0
```

Once in the folder, simply check that your probe is still in DFU Mode by running `lsusb`, and if you still get a result stating it is in DFU Mode, run the following command.

```
sudo dfu-util -R -a 0 -s 0x08000000:leave -D firmware.bin -d 0483:df11
```

NOTE - REPLACE the address (`0x08000000`) with what ever is listed in the [table here](https://docs.cartographer3d.com/cartographer-probe/firmware/manual-methods/firmware-update) for the specific firmware you are using, and rename `firmware.bin` to what ever the firmware file you are using is called.

**Example to flash V3 USB Full Firmware**

{% code overflow="wrap" %}
```bash
sudo dfu-util -R -a 0 -s 0x08000000:leave -D Full_Survey_Cartographer_USB_5_0_0.bin -d 0483:df11
```
{% endcode %}

**Example to flash V3 USB  lite (k1) Firmware**

{% code overflow="wrap" %}
```bash
sudo dfu-util -R -a 0 -s 0x08000000:leave -D Full_Survey_Cartographer_CrealityK1_USB_5_0_0.bin -d 0483:df11
```
{% endcode %}

**Example to flash V3 CAN 1m Full Firmware**

{% code overflow="wrap" %}
```bash
sudo dfu-util -R -a 0 -s 0x08000000:leave -D Full_Survey_Cartographer_CAN_1M_5_0_0.bin -d 0483:df11
```
{% endcode %}
{% endtab %}

{% tab title="Cartographer V4" %}
Navigate into the correct folder, so if you want to update your 4run the following command.

```
cd ~/cartographer_firmware/firmware/v4/combined-firmware/6.0.0
```

Once in the folder, simply check that your probe is still in DFU Mode by running `lsusb`, and if you still get a result stating it is in DFU Mode, run the following command.

```
sudo dfu-util -R -a 0 -s 0x08000000:leave -D firmware.bin
```

NOTE - REPLACE the address (`0x08000000`) with what ever is listed in the [table here](https://docs.cartographer3d.com/cartographer-probe/firmware/manual-methods/firmware-update) for the specific firmware you are using, and rename `firmware.bin` to what ever the firmware file you are using is called.

**Example to flash V4 USB Full Firmware**

{% code overflow="wrap" %}
```bash
sudo dfu-util -R -a 0 -s 0x08000000:leave -D Katapult_plus_CartographerV4_6.0.0__USB.bin -d 0483:df11
```
{% endcode %}

**Example to flash V4 USB  liteFirmware**

{% code overflow="wrap" %}
```bash
sudo dfu-util -R -a 0 -s 0x08000000:leave -D Katapult_plus_CartographerV4_6.0.0__USB_lite.bin -d 0483:df11
```
{% endcode %}

**Example to flash V4 CAN 1m Full Firmware**

{% code overflow="wrap" %}
```bash
sudo dfu-util -R -a 0 -s 0x08000000:leave -D Katapult_plus_CartographerV4_6.0.0__CAN_1M.bin -d 0483:df11
```
{% endcode %}

**Example to flash V4 CAN 1m lite Firmware**

{% code overflow="wrap" %}
```bash
sudo dfu-util -R -a 0 -s 0x08000000:leave -D Katapult_plus_CartographerV4_6.0.0__CAN_1M_lite.bin -d 0483:df11
```
{% endcode %}

Once compelte, it should exit out of DFU mode, and you should be able to find your probe on  USB or CAN, which ever you have selected.
{% endtab %}
{% endtabs %}

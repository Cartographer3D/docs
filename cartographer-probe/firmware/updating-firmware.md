# Updating Firmware

To update your probes firmware, the simplest method is to use Katapult, though you can also use DFU via USB.&#x20;

## Prerequisites

You must have both the Cartographer Firmware repository, and Katapult on your Pi, if you do not have these please connect via SSH and run the following command.&#x20;

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

## Updating via USB

### Updating Cartographer via Katapult

You should know which version of the Cartographer Probe you have in order to be able to do this, please refer to the diagrams below to identify your version.&#x20;

<figure><img src="../../.gitbook/assets/image (65).png" alt="Cartographer V3 - Standard, Low Profile and Right Angle"><figcaption><p>Cartographer V3 - Standard, Low Profile, RIght Angle</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (69).png" alt=""><figcaption><p>Cartographer V4 - Standard / Low Profile*</p></figcaption></figure>

\*Cartographer V4 has a different connector on it, but the PCB is the same design.&#x20;

#### Step 1 - Enter Bootloader Mode

The following steps can be done on both Cartographer V3 and Cartographer V4

{% tabs %}
{% tab title="Automatic Method" %}
We need to get our probe into the Katapult bootloader mode, to do so you can simply run this script

{% code overflow="wrap" %}
```bash
CARTO=$(ls /dev/serial/by-id/ 2>/dev/null | grep -i cartographer | head -n 1)

if [ -z "$CARTO" ]; then
    echo -e "\e[31mERROR: No Cartographer probe found in /dev/serial/by-id/. Is it plugged in via USB?\e[0m "
fi

cd ~/klipper/scripts || exit 1
~/klippy-env/bin/python -c "import flash_usb as u; u.enter_bootloader('/dev/serial/by-id/$CARTO')"

```
{% endcode %}
{% endtab %}

{% tab title="Manual Method" %}
The initial step is noting down the probes Serial ID, you do this by typing the following command

```bash
ls -l /dev/serial/by-id/
```

<figure><img src="../../.gitbook/assets/image (66).png" alt=""><figcaption></figcaption></figure>

You now need to load the probe into the Katapult bootloader, to do this you simply replace with your own serial ID and path as found in the above step.

```bash
cd ~/klipper/scripts
~/klippy-env/bin/python -c 'import flash_usb as u; u.enter_bootloader("<serialID>")'
```

Example of the full command

```bash
cd ~/klipper/scripts
~/klippy-env/bin/python -c 'import flash_usb as u; u.enter_bootloader("/dev/serial/by-id/usb-Cartographer_614e_060004001443303856303820-if00")'
```

<figure><img src="../../.gitbook/assets/image (67).png" alt=""><figcaption></figcaption></figure>
{% endtab %}
{% endtabs %}

Once your probe is in Bootloader mode, move onto the next step.&#x20;

#### Step 2 - Flash Firmware

{% tabs %}
{% tab title="Cartographer V3" %}
Now your Cartographer is in Katapult Mode, you now need to navigate to the correct firmware to flash it.

**Automatic Full V3 USB Firmware**

{% code overflow="wrap" fullWidth="false" %}
```bash
KATAPULT=$(ls /dev/serial/by-id/ 2>/dev/null | grep -i katapult | head -n 1)
cd ~/cartographer_firmware/firmware/v2-v3/survey/5.0.0/
~/klippy-env/bin/python ~/klipper/lib/canboot/flash_can.py -f Survey_Cartographer_USB_8kib_offset.bin -d /dev/serial/by-id/$KATAPULT
```
{% endcode %}

Your probe should now have the latest Cartographer Firmware installed on it. This page will be updated to include the command for the latest version available for this probe

**Manual - Full V3 USB Firmware**

Navigate to the folder where your firmware is located, for the example I will be using, I will be updating a v2 probe.

Now, run the following command, replacing \<firmware> with the firmware you are flashing, and \<serial> with the serial ID and path.

```
~/klippy-env/bin/python ~/klipper/lib/canboot/flash_can.py -f <firmware> -d <serial>
```

Again, an example of a full command

```
~/klippy-env/bin/python ~/klipper/lib/canboot/flash_can.py -f Cartographer_USB_8kib_offset.bin -d /dev/serial/by-id/usb-katapult_stm32f042x6_060012001643565537353020-if00
```

If successful, you should have the following output.

<figure><img src="../../.gitbook/assets/image (68).png" alt=""><figcaption></figcaption></figure>

If successful, you should have the following output.
{% endtab %}

{% tab title="Cartographer V4" %}
Now your Cartographer is in Katapult Mode, you now need to navigate to the correct firmware to flash it.

**Automatic V4 Full USB Firmware**

{% code overflow="wrap" fullWidth="false" %}
```bash
KATAPULT=$(ls /dev/serial/by-id/ 2>/dev/null | grep -i katapult | head -n 1)
cd ~/cartographer_firmware/firmware/v4/firmware/6.0.0
~/klippy-env/bin/python ~/klipper/lib/canboot/flash_can.py -f CartographerV4_6.0.0_USB_full_8kib_offset.bin -d /dev/serial/by-id/$KATAPULT
```
{% endcode %}

Your probe should now have the latest Cartographer Full Firmware installed on it. This page will be updated to include the command for the latest version available for this probe

**Automatic V4 Lite USB Firmware**

{% code overflow="wrap" fullWidth="false" %}
```bash
KATAPULT=$(ls /dev/serial/by-id/ 2>/dev/null | grep -i katapult | head -n 1)
cd ~/cartographer_firmware/firmware/v4/firmware/6.0.0
~/klippy-env/bin/python ~/klipper/lib/canboot/flash_can.py -f CartographerV4_6.0.0_USB_lite_8kib_offset.bin -d /dev/serial/by-id/$KATAPULT
```
{% endcode %}

Your probe should now have the latest Cartographer Lite Firmware installed on it. This page will be updated to include the command for the latest version available for this probe

**Manual - Full V4 USB Firmware**

Navigate to the folder where your firmware is located, for the example I will be using, I will be updating a v2 probe.

Now, run the following command, replacing \<firmware> with the firmware you are flashing, and \<serial> with the serial ID and path.

```
~/klippy-env/bin/python ~/klipper/lib/canboot/flash_can.py -f <firmware> -d <serial>
```

Again, an example of a full command

```
~/klippy-env/bin/python ~/klipper/lib/canboot/flash_can.py -f Cartographer_USB_8kib_offset.bin -d /dev/serial/by-id/usb-katapult_stm32f042x6_060012001643565537353020-if00
```

If successful, you should have the following output.

<figure><img src="../../.gitbook/assets/image (68).png" alt=""><figcaption></figcaption></figure>

If successful, you should have the following output.
{% endtab %}
{% endtabs %}

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

Once you have connected, Click Open File - you will need to select both the Katapult Bootloader for your board, and your Cartographer Firmware that you have downloaded.

<figure><img src="https://docs.cartographer3d.com/~gitbook/image?url=https%3A%2F%2F3044346320-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FjpCp1KnR8izt0cnWQfZF%252Fuploads%252FDZn6JTnVsZ2PPPgG9gvj%252Fimage.png%3Falt%3Dmedia%26token%3D6d63fff9-ea16-4f8b-9a1f-a51905a3992f&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=7fbcbe29&#x26;sv=2" alt=""><figcaption><p>Firmwares Loaded</p></figcaption></figure>

For your Cartographer Firmware, you need to set the address to `0x08002000` This provides the 8KiB offset for the firmware. Katapult firmware can be flashed at the default `0x08000000.`

<figure><img src="https://docs.cartographer3d.com/~gitbook/image?url=https%3A%2F%2F3044346320-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FjpCp1KnR8izt0cnWQfZF%252Fuploads%252FZnj7xVR2WpgS2s9lgaEK%252FSTLink.png%3Falt%3Dmedia%26token%3Deeccdbc6-9766-46a7-a5d7-f35bfae98922&#x26;width=768&#x26;dpr=4&#x26;quality=100&#x26;sign=380cc3d1&#x26;sv=2" alt=""><figcaption><p>How to change the address in STM32CubeProgrammer</p></figcaption></figure>

On each of the firmware's press "Download", starting with Katapult, then with Cartographer. Now press Disconnect in the TOP RIGHT corner.

If your BLUE LED is Flashing, you have not fully flashed your Firmware, and you should start again, If you now Power Cycle your probe, or simply hit the RESET (2) pads from earlier, your probe should react when it has anything solid metal put under it.

#### Flashing via DFU Util (Linux Terminal). <a href="#flashing-via-dfu-util-linux-terminal" id="flashing-via-dfu-util-linux-terminal"></a>

SSH into your linux host MCU, ensuring that your Cartographer is plugged in and in DFU Mode.

{% tabs %}
{% tab title="Cartographer V3" %}
Navigate into the correct folder, so if you want to update your v2 or v3 run the following command.

```
cd ~/cartographer_firmware/firmware/v2-v3/survey/5.0.0
```

Once in the folder, simply check that your probe is still in DFU Mode by running `lsusb`, and if you still get a result stating it is in DFU Mode, run the following command.

```
sudo dfu-util -R -a 0 -s 0x08002000:leave -D firmware.bin
```

NOTE - REPLACE the address (`0x08000000`) with what ever is listed in the [table here](https://docs.cartographer3d.com/cartographer-probe/firmware/manual-methods/firmware-update) for the specific firmware you are using, and rename `firmware.bin` to what ever the firmware file you are using is called.

Example to install the latest stable V3 Firmware:

```bash
sudo dfu-util -R -a 0 -s 0x08002000:leave -D Survey_Cartographer_USB_8kib_offset.bin
```

Once compelte, it should exit out of DFU mode, and you should be able to find your probe on  USB.
{% endtab %}

{% tab title="Cartographer V4" %}
Navigate into the correct folder, so if you want to update your v4 run the following command.

```bash
cd ~/cartographer_firmware/firmware/v4/firmware/6.0.0
```

Once in the folder, simply check that your probe is still in DFU Mode by running `lsusb`, and if you still get a result stating it is in DFU Mode, run the following command.

```bash
sudo dfu-util -R -a 0 -s 0x08002000:leave -D firmware.bin
```

NOTE - REPLACE the address (`0x08000000`) with what ever is listed in the [table here](https://docs.cartographer3d.com/cartographer-probe/firmware/manual-methods/firmware-update) for the specific firmware you are using, and rename `firmware.bin` to what ever the firmware file you are using is called.

Example to install the latest stable V3 Firmware:

```bash
sudo dfu-util -R -a 0 -s 0x08002000:leave -D CartographerV4_6.0.0_USB_full_8kib_offset.bin
```

Once compelte, it should exit out of DFU mode, and you should be able to find your probe on  USB.
{% endtab %}
{% endtabs %}

{% embed url="https://youtu.be/casMZXMRWNs" %}

# Switching Protocols

To switch your probe from CAN to USB or USB to CAN, the simplest method is to use Katapult and flash the Katapult Deployer file, though you can also use [DFU](re-flashing.md) via USB.&#x20;

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

## Switching Protocol

### Switching to CAN (1M) from USB

You should know which version of the Cartographer Probe you have in order to be able to do this, please refer to the diagrams below to identify your version.&#x20;

<figure><img src="../../.gitbook/assets/image (65).png" alt="Cartographer V3 - Standard, Low Profile and Right Angle"><figcaption><p>Cartographer V3 - Standard, Low Profile, RIght Angle</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (69).png" alt=""><figcaption><p>Cartographer V4 - Standard / Low Profile*</p></figcaption></figure>

\*Cartographer V4 Low Profile has a different connector on it, but the PCB is the same design.&#x20;

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
Now your Cartographer is in Katapult Mode, you now need to navigate to the correct katapult deployer file to flash it.

**Automatic Katapult Deployer  CAN (1,000,000)**

{% code overflow="wrap" fullWidth="false" %}
```bash
KATAPULT=$(ls /dev/serial/by-id/ 2>/dev/null | grep -i katapult | head -n 1)
cd ~/cartographer_firmware/firmware/v2-v3/katapult-deployer/
~/klippy-env/bin/python ~/klipper/lib/canboot/flash_can.py -f katapult-deployer-1m.bin -d /dev/serial/by-id/$KATAPULT
```
{% endcode %}

Your probe should now have the latest Cartographer Firmware installed on it. This page will be updated to include the command for the latest version available for this probe

**Manual - Katapult Deployer  CAN (1,000,000)**

Navigate to the folder where your katapult deployer is located&#x20;

```
cd ~/cartographer_firmware/firmware/v2-v3/katapult-deployer/
```

Now, run the following command, replacing \<firmware> with the firmware you are flashing, and \<serial> with the serial ID and path.

```
~/klippy-env/bin/python ~/klipper/lib/canboot/flash_can.py -f <firmware> -d <serial>
```

Again, an example of a full command

{% code overflow="wrap" %}
```
~/klippy-env/bin/python ~/klipper/lib/canboot/flash_can.py -f katapult-deployer-1m.bin -d /dev/serial/by-id/usb-katapult_stm32f042x6_060012001643565537353020-if00
```
{% endcode %}

If successful, you should have a similar output

<figure><img src="../../.gitbook/assets/image (68).png" alt=""><figcaption></figcaption></figure>

If successful, you should have the following output.
{% endtab %}

{% tab title="Cartographer V4" %}
Now your Cartographer is in Katapult Mode, you now need to navigate to the correct katapult deployer file to flash it.

**Automatic - Katapult Deployer  CAN (1,000,000)**

{% code overflow="wrap" fullWidth="false" %}
```bash
KATAPULT=$(ls /dev/serial/by-id/ 2>/dev/null | grep -i katapult | head -n 1)
cd ~/cartographer_firmware/firmware/v4/katapult-deployer
~/klippy-env/bin/python ~/klipper/lib/canboot/flash_can.py -f katapult_deployer_v4_CAN_1M.bin -d /dev/serial/by-id/$KATAPULT
```
{% endcode %}

Your probe should now have the latest Cartographer Full Firmware installed on it. This page will be updated to include the command for the latest version available for this probe

**Manual - Katapult Deployer  CAN (1,000,000)**

Navigate to the folder where your katapult-deployer is located

Now, run the following command, replacing \<firmware> with the firmware you are flashing, and \<serial> with the serial ID and path.

```
~/klippy-env/bin/python ~/klipper/lib/canboot/flash_can.py -f <firmware> -d <serial>
```

Again, an example of a full command

{% code overflow="wrap" %}
```
~/klippy-env/bin/python ~/klipper/lib/canboot/flash_can.py -f katapult_deployer_v4_CAN_1M.bin -d /dev/serial/by-id/usb-katapult_stm32f042x6_060012001643565537353020-if00
```
{% endcode %}

If successful, you should look something like this:

<figure><img src="../../.gitbook/assets/image (68).png" alt=""><figcaption></figcaption></figure>

If successful, you should have the following output.
{% endtab %}
{% endtabs %}

#### Step 3 - Flashing the Firmware

{% tabs %}
{% tab title="Cartographer V3" %}
You now need to plugin your Cartographer into your CAN network.

{% hint style="danger" %}
DO NOT HOT PLUG ANYTHING IN YOUR PRINTER, ENSURE IT IS POWERED OFF.
{% endhint %}

You now need to flash your CAN firmware to the probe, so navigate to the directory the firmware is located&#x20;

```bash
cd ~/cartographer_firmware/firmware/v2-v3/survey/5.0.0/
```

You will now need to check that your probe can be recognised by your CAN network, to do this we will do a CAN query. You should see a device which has Katapult listed next to it.  Note down the UUID it provides you.&#x20;

```bash
~/klippy-env/bin/python ~/klipper/scripts/canbus_query.py can0    
```

Now, you will need to run the following command, replacing the UUID with what ever the UUID is for your probe.&#x20;

{% code overflow="wrap" %}
```bash
python3 ~/katapult/scripts/flash_can.py -i can0 -f Survey_Cartographer_CAN_1000000_8kib_offset.bin -u UUID
```
{% endcode %}

Example

{% code overflow="wrap" %}
```bash
python3 ~/katapult/scripts/flash_can.py -i can0 -f Survey_Cartographer_CAN_1000000_8kib_offset.bin -u 379702c36ad1
```
{% endcode %}

Once complete, your probe will reboot into the Cartographer Firmware, and you can continue to use your probe as normal.<br>
{% endtab %}

{% tab title="Cartographer V4" %}
You now need to plugin your Cartographer into your CAN network.

{% hint style="danger" %}
DO NOT HOT PLUG ANYTHING IN YOUR PRINTER, ENSURE IT IS POWERED OFF.
{% endhint %}

You now need to flash your CAN firmware to the probe, so navigate to the directory the firmware is located&#x20;

```bash
cd ~/cartographer_firmware/firmware/v4/firmware/6.0.0/
```

You will now need to check that your probe can be recognised by your CAN network, to do this we will do a CAN query. You should see a device which has Katapult listed next to it.  Note down the UUID it provides you.&#x20;

```bash
~/klippy-env/bin/python ~/klipper/scripts/canbus_query.py can0    
```

Now, you will need to run the following command, replacing the UUID with what ever the UUID is for your probe.&#x20;

{% code overflow="wrap" %}
```bash
python3 ~/katapult/scripts/flash_can.py -i can0 -f CartographerV4_6.0.0_USB_full_8kib_offset.bin -u UUID
```
{% endcode %}

Example

{% code overflow="wrap" %}
```bash
python3 ~/katapult/scripts/flash_can.py -i can0 -f CartographerV4_6.0.0_USB_full_8kib_offset.bin -u 379702c36ad1
```
{% endcode %}

Once complete, your probe will reboot into the Cartographer Firmware, and you can continue to use your probe as normal.
{% endtab %}
{% endtabs %}

### Switching to USB from CAN

To switch from CAN to USB, you will need to flash the Katapult Deployer Firmware to overwrite the existing bootloader and firmware to load it in USB mode.&#x20;

**Step 1 - Plug Cartographer in via CANBUS**

Your Cartographer will already need to have CAN firmware on the probe, to change from USB to CAN, please follow [Re-Flashing](https://docs.cartographer3d.com/cartographer-probe/firmware/re-flashing).

**Step 2 - SSH into your printer**

**Step 3 - Get Your UUID**

You will need to get your probes UUID, this should be in your printer.cfg if you have already setup the probe, it will either be under `[mcu cartographer]`, `[cartographer]`, or `[scanner]`

If you have not set it up already, search for the UUID either in the mainsail device finder menu, or by using the command `~/klippy-env/bin/python ~/klipper/scripts/canbus_query.py can0` (note, if the device is in your printer.cfg or similar, it will not find it.

#### Step 4 - Flash the Katapult Deployer

You now need to flash the Katapult Deployer USB Firmware

{% hint style="danger" %}
You will need to replace with your UUID found in step3.
{% endhint %}

{% tabs %}
{% tab title="Cartographer V3" %}
**Switch Cartographer V3 from CAN to USB**

{% code overflow="wrap" %}
```bash
~/cartographer_firmware/firmware/v2-v3/katapult-deployer
python3 ~/katapult/scripts/flash_can.py -i can0 -f katapult-deployer-usb.bin -u <myuuid>
```
{% endcode %}
{% endtab %}

{% tab title="Cartographer V4" %}
**Switch Cartographer V4 from CAN to USB**

{% code overflow="wrap" %}
```bash
cd ~/cartographer_firmware/firmware/v4/katapult-deployer/
python3 ~/katapult/scripts/flash_can.py -i can0 -f katapult_deployer_v4_USB.bin -u <myuuid>
```
{% endcode %}
{% endtab %}
{% endtabs %}

#### Step 5 - Switch to USB

Power down your printer, and re-connect your probe via USB.&#x20;

#### Step 6 - Flash the Cartographer Firmware

{% tabs %}
{% tab title="Cartographer V3" %}
Now your Cartographer is in Katapult Mode, you now need to navigate to the correct firmware to flash it.

**Automatic Full V3 USB Firmware**

{% code overflow="wrap" %}
```
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

![](https://docs.cartographer3d.com/~gitbook/image?url=https%3A%2F%2F3044346320-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FjpCp1KnR8izt0cnWQfZF%252Fuploads%252FsLbQEYhc75evn1hikPXb%252Fimage.png%3Falt%3Dmedia%26token%3Dae2854a2-1833-4aed-9907-9d32c152fb10\&width=768\&dpr=3\&quality=100\&sign=1c515908\&sv=2)

If successful, you should have the following output.
{% endtab %}

{% tab title="Cartographer V4" %}
Now your Cartographer is in Katapult Mode, you now need to navigate to the correct firmware to flash it.

**Automatic V4 Full USB Firmware**

```
KATAPULT=$(ls /dev/serial/by-id/ 2>/dev/null | grep -i katapult | head -n 1)
cd ~/cartographer_firmware/firmware/v4/firmware/6.0.0
~/klippy-env/bin/python ~/klipper/lib/canboot/flash_can.py -f CartographerV4_6.0.0_USB_full_8kib_offset.bin -d /dev/serial/by-id/$KATAPULT
```

Your probe should now have the latest Cartographer Full Firmware installed on it. This page will be updated to include the command for the latest version available for this probe

**Automatic V4 Lite USB Firmware**

```
KATAPULT=$(ls /dev/serial/by-id/ 2>/dev/null | grep -i katapult | head -n 1)
cd ~/cartographer_firmware/firmware/v4/firmware/6.0.0
~/klippy-env/bin/python ~/klipper/lib/canboot/flash_can.py -f CartographerV4_6.0.0_USB_lite_8kib_offset.bin -d /dev/serial/by-id/$KATAPULT
```

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

![](https://docs.cartographer3d.com/~gitbook/image?url=https%3A%2F%2F3044346320-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FjpCp1KnR8izt0cnWQfZF%252Fuploads%252FsLbQEYhc75evn1hikPXb%252Fimage.png%3Falt%3Dmedia%26token%3Dae2854a2-1833-4aed-9907-9d32c152fb10\&width=768\&dpr=3\&quality=100\&sign=1c515908\&sv=2)

If successful, you should have the following output.
{% endtab %}
{% endtabs %}

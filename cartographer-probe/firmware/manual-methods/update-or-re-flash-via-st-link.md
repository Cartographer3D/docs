# Update or Re-Flash via ST-Link

pdating via the ST-Link provides a reliable and easy way to flash any STM based MCU's especially if you have issues entering DFU mode, the only time where it becomes problematic is when older/fake ST-Links are used, please see the notes and ways of identifying below.&#x20;

### Requirements&#x20;

* ST-Link v2 (Below is a table of the most common ST-Link v2s. There are obviously more available on the market.&#x20;



| STLink                 | ST-Link V2 Mini (Fake MCU)                                                                      | ST-Link V2 Mini                                                                 | ST-Link V2                                                                      |
| ---------------------- | ----------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------- | ------------------------------------------------------------------------------- |
| Image                  | <img src="../../../.gitbook/assets/image (37).png" alt="" data-size="original">                 | <img src="../../../.gitbook/assets/image (33).png" alt="" data-size="original"> | <img src="../../../.gitbook/assets/image (35).png" alt="" data-size="original"> |
| Note                   | Uses fake STM Chip, Pin order is different and isnt always recognised via STM Cube Programmer.  | Occasional Issues, depending on age / firmware.                                 | Most Reliable                                                                   |
| STMCubeProg Compatible | <p>❌ </p><p>May not work</p>                                                                    | ✅                                                                               | ✅[^1]                                                                           |

* STM Cube Programmer - (recommended version v2.15.0) **- if using Windows or MacOS**
* 4x DuPont M-M or M-F Cables
* Cartographer V3 Probe

{% embed url="https://www.st.com/en/development-tools/stm32cubeprog.html#st-get-software" %}

### Step 1 - Wire up your probe

Connect the following pins based upon the different ST-Links.&#x20;

| Hardware                        | Pinout                                                                          | Connections (STLink - Probe)                                                                                                               |
| ------------------------------- | ------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------ |
| **ST-Link V2**                  | <img src="../../../.gitbook/assets/image (38).png" alt="" data-size="original"> | <p>SWDIO - SWD<br>SWCLK - SCL<br>GND - GND<br>VCC - 5V</p>                                                                                 |
| **ST-Link V2 Mini (Fake Chip)** | <img src="../../../.gitbook/assets/image (39).png" alt="" data-size="original"> | <p>SWDIO - SWD<br>SWCLK - SCL<br>GND - GND<br>3.3V*- 5V<br><br>* 5v may also work , but on some mini's it can cause stability issues. </p> |
| **ST-Link V2 Mini**             | <img src="../../../.gitbook/assets/image (40).png" alt="" data-size="original"> | <p>SWDIO - SWD<br>SWCLK - SCL<br>GND - GND<br>3.3V*- 5V<br><br>* 5v may also work , but on some mini's it can cause stability issues. </p> |

Connect your probe to the STLink connectors to the left and the right of the JST connector.&#x20;

<figure><img src="../../../.gitbook/assets/image (41).png" alt=""><figcaption><p>Pinout on Cartgorapher V2 and V3</p></figcaption></figure>

{% hint style="warning" %}
You do NOT need to solder in the connector, pressure fit is fine.&#x20;
{% endhint %}

<figure><img src="../../../.gitbook/assets/image (43).png" alt=""><figcaption><p>Connected on ST-Link V2</p></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (63).png" alt=""><figcaption><p>Connected to a ST-Link v2 Mini (with a Genuine STM Chip)</p></figcaption></figure>

### If using Windows follow the next steps, if you are using Linux (Pi) [click here](update-or-re-flash-via-st-link.md#flashing-via-linux-pi)

Open STM32CubeProg

<figure><img src="../../../.gitbook/assets/image (44).png" alt=""><figcaption></figcaption></figure>

Select **Open File** and select the file you want to open. For this, I recommend flashing the FULL complete firmware files, which include both **bootloader** and **Cartographer firmware.**&#x20;

<figure><img src="../../../.gitbook/assets/image (47).png" alt=""><figcaption><p>Select the file you need</p></figcaption></figure>

### Step 3 - Check the Settings

Ensure that you are writing to the correct memory location&#x20;

If your firmware is from the **`combined-firmware`** folder or starts with the words `Katapult`**,**  ensure that the address is set to `0x08000000`

<figure><img src="../../../.gitbook/assets/image (51).png" alt=""><figcaption></figcaption></figure>

Ensure that you have ST-LINK slelected on the right (this can default to DFU mode if you havnt used this before)&#x20;

<figure><img src="../../../.gitbook/assets/image (52).png" alt=""><figcaption></figcaption></figure>

Now press Connect and the screen should indicate that the probe is Connected&#x20;

<figure><img src="../../../.gitbook/assets/image (54).png" alt=""><figcaption></figcaption></figure>



### Flash and Confirm Firmware&#x20;

Press download to Download the firmware to your Cartographer&#x20;

<figure><img src="../../../.gitbook/assets/image (55).png" alt=""><figcaption></figcaption></figure>

The output should look something like this&#x20;

<figure><img src="../../../.gitbook/assets/image (56).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../.gitbook/assets/image (57).png" alt=""><figcaption></figcaption></figure>

Press Disconnect and unplug the probe.&#x20;

### Flashing via Linux (Pi)

1. SSH into your 3D Printer using your client of choice&#x20;
2. Run the following command (this may take a little while)

```bash
sudo apt-get update
sudo apt-get upgrade
sudo apt-get -y install stlink-tools
```

3. Navigate to the folder where your firmware is stored, usually&#x20;

```bash
cd ~/cartographer-klipper/firmware/v2-v3/combined-firmware
```

4. Check if the ST-Link has been detected using `lsusb` if it is not visable, unplug and re-plug it back in.&#x20;

<figure><img src="../../../.gitbook/assets/image (61).png" alt=""><figcaption><p>Original lsusb not being able to see the ST-Link, second one able to see it. </p></figcaption></figure>

4. run the following command replacing firmware.bin and the memory address with the correct address for the firmware that you are using.&#x20;

```
st-flash write firmware.bin 0x080000000
```

For example to flash the Survey CAN firmware&#x20;

```
st-flash write Full_Survey_Cartographer_CAN_1M_5_0_0.bin 0x08000000
```

Upon completion, you should see something like this&#x20;

<figure><img src="../../../.gitbook/assets/image (62).png" alt=""><figcaption><p>Successful Flash</p></figcaption></figure>

### Reconnect your probe to your printer

Reconnect your probe to your 3D Printer, and it should work perfectly :)



[^1]: 

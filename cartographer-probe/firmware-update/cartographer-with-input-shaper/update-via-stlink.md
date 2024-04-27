# Update via STLink

Flashing via a STLink is super simple, and requires a STLink v2 (or similar). Unfortunatly you cannot use a standard TTL-USB adaptor.&#x20;

This method only works on V2 and V3 probes with the STLink connection points next to the USB Port.&#x20;

{% hint style="info" %}
I have only personally tested this on a ST-LINK/V2 Mini with modern firmware on it - some older V2's will not work with STM32CubeProgrammer.
{% endhint %}

### Step 1 - Wiring

Wiring is super simple (diagram will be added soon), connect the following to each other&#x20;

<figure><img src="../../../.gitbook/assets/image (1) (1) (1).png" alt="" width="188"><figcaption></figcaption></figure>



| ST-LINK/V2 | Cartographer v2 / v3 | Notes                                                                                          |
| ---------- | -------------------- | ---------------------------------------------------------------------------------------------- |
| 3.3v       | 5v                   | 5v-5v will work, but seems less reliable, could have been my ST-LINK, but 3.3v works perfectly |
| GND        | GND                  |                                                                                                |
| SWDIO      | SWD                  |                                                                                                |
| SWCLK      | SCL                  |                                                                                                |

### Flashing via STM32CubeProgrammer (Windows & MacOS)

Download and Install STM32CubeProgrammer from [here](https://www.st.com/en/development-tools/stm32cubeprog.html), I warn you it requires you to sign up for an account.

{% hint style="warning" %}
Version 2.14.0 is recommended due to a known bug in 2.16.0 which causes issues when flashing via STMCubeProgammer - this can be selected from the version 'drop down' on the site.&#x20;
{% endhint %}

Open the STMCubeProgrammer, and on the RIGHT side, select select STLink from the drop down menu and press **Connect**.&#x20;

<figure><img src="../../../.gitbook/assets/image (2) (1) (1).png" alt=""><figcaption></figcaption></figure>

Once you have connected, Click Open File - you will need to select both the Katapult Bootloader for your board, and your Cartographer Firmware that you have downloaded.&#x20;

<figure><img src="../../../.gitbook/assets/image (10) (1).png" alt=""><figcaption><p>Firmwares Loaded (Note same screenshots used for USB version, yours will say STLink on ther right)</p></figcaption></figure>

For your Cartographer Firmware, you need to set the address to `0x08002000` This provides the 8KiB offset for the firmware. Katapult firmware can be flashed at the default `0x08000000.`

<figure><img src="../../../.gitbook/assets/STLink (1).png" alt=""><figcaption><p>How to change the address in STM32CubeProgrammer  (Note same screenshots used for USB version, yours will say STLink on ther right)</p></figcaption></figure>

If in doubt about what address to use, please check the relevent tables [here](https://docs.cartographer3d.com/firmware-update)

On each of the firmware's press "Download", starting with Katapult, then with Cartographer. \
\
Now press Disconnect in the TOP RIGHT corner.&#x20;

If your BLUE LED is Flashing, you have not fully flashed your Firmware, and you should start again, If you now Power Cycle your probe, or simply hit the RESET (2) pads from earlier, your probe should react when it has anything solid metal put under it.&#x20;

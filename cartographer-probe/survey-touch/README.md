---
layout:
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: false
---

# 👇 Survey Touch

{% hint style="info" %}
[If youre coming from BETA go here first.](survey-faq.md#i-was-in-the-beta-how-do-i-switch-back-to-regular-to-continue-using-touch)
{% endhint %}

{% hint style="danger" %}
We **DO NOT** 100% guarantee compatibility with ALL printers. It is your responsibility to read this entire guide prior to use and to research whether this is right for you. Please contact us on [DISCORD ](https://discord.gg/yzazQMEGS2)if you have questions.\
\
This guide is only intended for use if you plan on using <mark style="color:green;">TOUCH</mark>. Otherwise,[ use the normal guide](../installation-and-setup/cartographer-with-input-shaping-v2-and-v3-hybrid.md) and [calibration](../installation-and-setup/cartographer-with-input-shaper-v2-and-v3-hybrid.md) which retains `[cartographer]`
{% endhint %}

{% hint style="danger" %}
Before proceeding, make a back-up of any existing `[cartographer]` or `[scanner]` sections in your printer.cfg especially`x_offset` **,** `y_offset` and `canbus_UUID` or `serial`\
\
Then, please **REMOVE** all of your existing `[cartographer]` or `[scanner]` sections from your <mark style="color:yellow;">**printer.cfg**</mark> and other configurations before proceeding.\
\- Including `[cartographer model default]` or `[scanner model default`] and any other models from the bottom of <mark style="color:yellow;">**printer.cfg**</mark>
{% endhint %}

***

## Installation

* [Follow the guide for probe installation first.](../installation-and-setup/probe-installation/)

{% hint style="danger" %}
For Cartographer to receive usable readings for touch to be accurate, you **MUST** place cartographer between <mark style="color:red;">**2.6 and 3mm ABOVE**</mark> the nozzle. Print or put something 2.5-2.6mm but no more than 3mm in height under or next to the cartographer coil to measure where it needs to be.

\
Your toolhead & gantry/carriage **MUST** be <mark style="color:red;">**RIGID**</mark>. If there is movement and flex it can also create undesired results in the touch process.
{% endhint %}

* [Follow the Klipper Setup guide.](../installation-and-setup/klipper-setup.md)
* SSH into your machine and run the following code

```bash
cd ~/cartographer-klipper
git fetch
git reset --hard HEAD
git clean -xffd
git pull
./install.sh
sudo service klipper restart
```

## Firmware Update

[Follow the guide ](../firmware/firmware-updating/)on updating your firmware. Select <mark style="color:green;">WITH SURVEY TOUCH.</mark>

{% hint style="info" %}
Creality K-series Users, [please visit this link to flash your firmware.](https://github.com/pellcorp/creality/wiki/Flashing-Carto-Firmware-on-Ubuntu)
{% endhint %}

{% hint style="info" %}
**Did You Know?**\
Even with Survey Touch firmware you can run in scan only mode if you dont want to use Touch.\
Just set`calibration_method:scan` in <mark style="color:yellow;">**printer.cfg**</mark>
{% endhint %}

***

## Command format mistmatch? Do not fear!!

If you are greeted with the following error, **DO NOT** worry. Its normal and just apart of the configuration process. If you dont see it, **GOOD!**

<figure><img src="../../.gitbook/assets/image (12).png" alt="" width="375"><figcaption></figcaption></figure>

***

## Configuration

<details>

<summary>Printer.cfg Configuration <mark style="color:red;">REQUIRED - PLEASE EXPAND</mark></summary>

Before proceeding, make a back-up of any existing `[cartographer]` or `[scanner]` sections in your <mark style="color:yellow;">**printer.cfg**</mark> like `x_offset` **,** `y_offset` and `canbus_UUID` or `serial`\
\
Then, please **REMOVE** all of your existing `[cartographer]`  or `[scanner]` sections from your <mark style="color:yellow;">**printer.cfg**</mark> and other configurations before proceeding.\
\
These are <mark style="color:red;">REQUIREMENTS</mark>. Including the `zero_reference_position` in your `[bed_mesh]` section.&#x20;

```yaml
[scanner]
canbus_uuid: 0ca8d67388c2            
#adjust to suit your scanner 
#serial: /dev/serial/by-id/usb-cartographer_cartographer_
x_offset: 0                          
#adjust for your offset
y_offset: 15                         
#adjust for your offset
calibration_method: touch 
sensor: cartographer
sensor_alt: carto
#alternate name to call commands. CARTO_TOUCH etc
scanner_touch_z_offset: 0.05         
#this is the default and will be overwritten and added to the DO NOT SAVE area by using UI to save z offset

[bed_mesh]
zero_reference_position: 125, 125    
# set this to themiddle of your bed


```

</details>

{% hint style="info" %}
If you want to use the probe for Input Shaper, please add the following to your config.

{% tabs %}
{% tab title="adxl345 based probes" %}
```yaml
[adxl345]
cs_pin: scanner:PA3
spi_bus: spi1

[resonance_tester]
accel_chip: adxl345
probe_points:
    125, 125, 20
```
{% endtab %}

{% tab title="lis2dw based probes" %}
```yaml
[lis2dw]
cs_pin: scanner:PA3
spi_bus: spi1

[resonance_tester]
accel_chip: lis2dw
probe_points:
    125, 125, 20
```
{% endtab %}
{% endtabs %}
{% endhint %}

<details>

<summary>Print Start Macro Example <mark style="color:red;">REQUIRED - PLEASE EXPAND</mark></summary>

Adding the `CARTOGRAPHER_TOUCH` command to your print start macro ensures that the printer performs a precise touch probe <mark style="color:red;">**AFTER**</mark> executing the `BED_MESH_CALIBRATE` command. `CARTOGRAPHER_TOUCH` should also be performed with a nozzle <mark style="color:red;">no hotter than 150c</mark>. With this in mind, the command will fail if the nozzle is beyond this temperature. It **CAN** be performed cold. Please make allowances for this in your print start. This sequence helps to achieve an accurate bed leveling by accounting for any variations or offsets after the mesh calibration.

```gcode
PLEASE DONT USE THIS - IT IS AN EXAMPLE ONLY
[gcode_macro PRINT_START_EXAMPLE]
gcode:
    G28                               ; Home all axes
    M140 S{BED_TEMP}                  ; Set bed temperature
    M109 S150                         ; Wait for extuder to reach 150°C (intermediate step)
    M190 S{BED_TEMP}                  ; Set final bed temperature
    G28 Z                             ; Home Z axis again to account for thermal expansion
    M112 #Remove this line            ; Its your own fault if you dont..
    QUAD_GANTRY_LEVEL / Z_TILT_ADJUST ; Perform quad gantry leveling or Z tilt adjustmen
    G28 Z                             ; Home Z axis again to account for thermal expansion
    BED_MESH_CALIBRATE                ; Calibrate the bed mesh
    CARTOGRAPHER_TOUCH                ; Perform touch probe
    M109 S{EXTRUDER_TEMP}             ; Wait for extruder to reach target temperature

PLEASE DONT USE THIS - IT IS AN EXAMPLE ONLY
```



</details>

***

## Initial Calibration

{% hint style="danger" %}
Touch is best calibrated for use with a clean install. We ask you remove your existing `[scanner]` or `[cartographer]` model if you have one and any other `[scanner]` or `[cartographer]` settings from the bottom of <mark style="color:yellow;">**printer.cfg**</mark>
{% endhint %}

{% hint style="info" %}
Calibration can be done <mark style="color:red;">HOT</mark> or <mark style="color:blue;">COLD.</mark>
{% endhint %}

```gcode
G28 X Y
CARTOGRAPHER_TOUCH METHOD=manual   # initiates paper test we all know and love
G28 Z
QUAD_GANTRY_LEVEL / Z_TILT_ADJUST
G28 Z or G28                       # G28 if your G28 Z doesnt move to homing position
CARTOGRAPHER_THRESHOLD_SCAN 
CARTOGRAPHER_TOUCH CALIBRATE=1     # starts touch test and calibration 
SAVE_CONFIG                        # saves model and threshold
```

{% hint style="info" %}
The "**PAPER TEST**" method [can be found here](https://www.klipper3d.org/Bed\_Level.html#the-paper-test). \
\
[Visit here](settings-and-commands.md#cartographer\_threshold\_scan) for an explanation of `CARTOGRAPHER_THRESHOLD_SCAN`\
\
[Visit here](./#cartographer\_touch)[ ](settings-and-commands.md#cartographer\_touch)for an explanation of `CARTOGRAPHER_TOUCH`
{% endhint %}

## First Print

You might notice your z-offset is a little wrong, this is hugely dependent on too many things, however its simple to fix. Just use the video below as an example.\
\
`scanner_touch_z_offset` is the distance between nozzle and bed after a `CARTOGRAPHER_TOUCH`

Default `scanner_touch_z_offset` is 0.05

{% embed url="https://youtu.be/OoZ2fcD3zlA" %}
video courtesy of Yell on Cartographer Discord
{% endembed %}

{% hint style="success" %}
This is the end of the setup and calibration process.&#x20;

The rest of this page just explains the commands and available advanced parameters and are not required unless **NEEDED.**&#x20;
{% endhint %}

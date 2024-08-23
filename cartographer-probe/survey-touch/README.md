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
We **DO NOT** 100% guarantee compatibility with ALL printers. It is your responsibility to read this entire guide prior to use and to research whether this is right for you. Please contact us on [DISCORD ](https://discord.gg/yzazQMEGS2)if you have questions.
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
For Cartographer to receive usable readings for touch to be accurate, you **MUST** place cartographer between <mark style="color:red;">**2.6 and 3mm ABOVE**</mark> the nozzle.

\
Your toolhead & gantry/carriage **MUST** be <mark style="color:red;">**RIGID**</mark>. If there is movement and flex it can also create undesired results in the touch process.
{% endhint %}

* [Follow the Klipper Setup guide.](../installation-and-setup/klipper-setup.md)
* SSH into your machine and run the following code

```bash
cd ~/cartographer-klipper
git fetch
git pull
chmod +x install.sh
./install.sh
sudo service klipper restart
```

## Firmware Update

[Follow the guide ](../firmware/firmware-updating/)on updating your firmware. Select <mark style="color:green;">WITH SURVEY TOUCH.</mark>

{% hint style="info" %}
**Did You Know?**\
Even with Survey Touch firmware you can run in scan only mode if you dont want to use Touch.\
Just set`calibration_method:scan` in <mark style="color:yellow;">**printer.cfg**</mark>
{% endhint %}

***

## Do not fear!!

If you are greeted with the following error, **DO NOT** worry. Its normal and just apart of the configuration process. If you dont see it, **GOOD!**

<figure><img src="../../.gitbook/assets/image (2).png" alt="" width="375"><figcaption></figcaption></figure>

***

## Configuration

<details>

<summary>Printer.cfg Configuration <mark style="color:red;">IMPORTANT</mark></summary>

Before proceeding, make a back-up of any existing `[cartographer]` or `[scanner]` sections in your <mark style="color:yellow;">**printer.cfg**</mark> like `x_offset` **,** `y_offset` and `canbus_UUID` or `serial`\
\
Then, please **REMOVE** all of your existing `[cartographer]`  or `[scanner]` sections from your <mark style="color:yellow;">**printer.cfg**</mark> and other configurations before proceeding.\
\
These are <mark style="color:red;">REQUIREMENTS</mark>. Including the `zero_reference_position` in your `[bed_mesh]` section.&#x20;

```yaml
[scanner]
canbus_uuid: 0ca8d67388c2            #adjust to suit your scanner 
x_offset: 0                          #adjust for your offset
y_offset: 15                         #adjust for your offset
calibration_method: touch 
sensor: cartographer
sensor_alt: carto

[bed_mesh]
zero_reference_position: 125, 125    # set this to themiddle of your bed

[adxl345]
cs_pin: scanner:PA3
spi_bus: spi1
```

</details>

<details>

<summary>Print Start Macro Example <mark style="color:red;">IMPORTANT</mark></summary>

Adding the `CARTOGRAPHER_TOUCH` command to your print start macro ensures that the printer performs a precise touch probe <mark style="color:red;">**AFTER**</mark> executing the `BED_MESH_CALIBRATE` command and <mark style="color:red;">**AFTER**</mark> your nozzle reaches a steady 150c. This sequence helps to achieve an accurate bed leveling by accounting for any variations or offsets after the mesh calibration.

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

{% hint style="success" %}
This is the end of the setup and calibration process.&#x20;

The rest of this page just explains the commands and available advanced parameters and are not required unless **NEEDED.**&#x20;
{% endhint %}

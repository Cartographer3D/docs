# Migrating from Cartographer to Scanner

If you've been using **\[cartographer]** its time to update to **\[scanner]**

### Moonraker.conf Changes

```yaml
[update_manager cartographer]
type: git_repo
path: ~/cartographer-klipper
channel: stable
origin: https://github.com/Cartographer3D/cartographer-klipper.git
is_system_service: False
managed_services: klipper
info_tags:
  desc=Cartographer Probe
```

### Printer.cfg Changes

1. The **\[cartographer]** section needs to be renamed to **\[scanner]**
2. The following lines need to be added under \[scanner]

```yaml
sensor: cartographer
#    this must be set as cartographer unless using IDM etc.
sensor_alt: carto
#    alternate name to call commands. CARTO_TOUCH etc  
```

3. Update your \[adxl345] or \[lis2dw] sections

```yaml
[adxl345]
cs_pin: scanner:PA3
spi_bus: spi1

OR

[lis2dw]
cs_pin: scanner:PA3
spi_bus: spi1
```

4. Add to your existing \[bed\_mesh] section

```yaml
[bed_mesh]
zero_reference_position: 125, 125 # center of your bed
```

5. Remove the following macro

```yaml
[gcode_macro PROBE_CALIBRATE]
gcode:
    CARTOGRAPHER_CALIBRATE
```

6. Scroll down to the SAVE\_CONFIG portion of printer.cfg and remove the following

{% hint style="danger" %}
MAKE SURE YOU LEAVE NO BLANK/EMPTY LINES

Empty lines should contain nothing other than #\*#
{% endhint %}

```markup
#*# [cartographer model default]
#*# model_coef = 1.2756087614398297,
#*# 	1.7032235919205718,
#*# 	0.7549615279585394,
#*# 	0.33053182696977934,
#*# 	0.49230277115342924,
#*# 	0.603864368037255,
#*# 	-0.4286306328139887,
#*# 	-0.6071391058450671,
#*# 	0.4556606647261048,
#*# 	0.4209032930645854
#*# model_domain = 3.1397176509462183e-07,3.3604013404235566e-07
#*# model_range = 0.100000,5.000000
#*# model_temp = 23.255185
#*# model_offset = 0.00000
```



### What else?

1. Run the following script via SSH

```bash
cd ~/cartographer-klipper
./install.sh
```

2. Update your firmware to 5.0.0 or higher, using one of the [firmware updating guides found here](../../firmware/firmware-updating/)
3. Restart klipper by entering the following code via SSH

```bash
sudo service klipper restart
```

## All done!

## Now just follow either the [TOUCH](touch-based-calibration.md) or [SCAN ](scan-based-calibration.md)guides on re-calibrating.


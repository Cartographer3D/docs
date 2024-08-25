# Survey Troubleshooting

## Troubleshooting

### SAVE\_CONFIG section 'scanner' option 'scanner\_touch\_z\_offset' conflicts with included value

<figure><img src="../../.gitbook/assets/image.png" alt="" width="375"><figcaption></figcaption></figure>

A common cause for this is having you `[scanner]` section in an included config file and not in <mark style="color:yellow;">**printer.cfg**</mark>. \
\
To work around this klipper limitation, remove `scanner_touch_z_offset` from your included config and add it to <mark style="color:yellow;">**printer.cfg**</mark>. \
\
Below is an example of what to have in <mark style="color:yellow;">**printer.cfg**</mark>. \
\
This will allow klipper to save new offsets using the UI.

<figure><img src="../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

### Unknown pin chip name "cartographer"

<figure><img src="../../.gitbook/assets/image (1) (1).png" alt="" width="375"><figcaption></figcaption></figure>

This occurs when there is old references to cartographer in your <mark style="color:yellow;">**printer.cfg**</mark>\
Please check your <mark style="color:yellow;">**printer.cfg**</mark> and make sure "cartographer" only appears next to `sensor:` and `[adxl] cs_pin:`&#x20;

### Unknown pin chip name "scanner"

<figure><img src="../../.gitbook/assets/image (10).png" alt="" width="375"><figcaption></figcaption></figure>

This can happen when the symlink between klipper and scanner is broken. You can check your symlinks with the following command.

```bash
find  ~/klipper/klippy/extras/  -maxdepth 1 -type l -ls
```

If they dont look right or youre just not sure, run the following again.

```bash
cd ~/cartographer-klipper
chmod +x install.sh
./install.sh
```

And then check your symlinks again. You should see scanner.py pointed to the cartographer-klipper folder.

### Mcu 'scanner': command format mismatch: query\_lis2dw

<figure><img src="../../.gitbook/assets/image (1) (1) (1).png" alt="" width="375"><figcaption></figcaption></figure>

This happens when youre using an older version of klipper. If you for whatever reason cannot update to the latest version of klipper, you need to **REMOVE** the following sections from <mark style="color:yellow;">**printer.cfg**</mark> completely.

```yaml
[lis2dw]
cs_pin
spi_bus:

[resonance_tester]
accel_chip: lis2dw
```

### I'm getting weird errors after updating my scanner.py, what do I do?

Firstly make sure you have hit the **RESTART KLIPPER** button in your Fluid/Mainsail UI, this will force the refresh of scanner.py to the updated version.

<figure><img src="../../.gitbook/assets/Screenshot 2024-08-21 210954.png" alt="" width="356"><figcaption><p>Always RESTART KLIPPER after an update.</p></figcaption></figure>

### Option 'X' is not valid in section 'scanner'

&#x20;You have a parameter within your `[scanner]` section in printer.cfg that isnt valid. Remove X from your <mark style="color:yellow;">**printer.cfg**</mark> or check its written correctly. You can see [valid parameters here](settings-and-commands.md#available-parameters)

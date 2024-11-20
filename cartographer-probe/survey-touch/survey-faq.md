# Survey FAQ

## Frequently Asked Questions

### Can I use cartographer without touch without changing firmware?

Yes, you sure can. All you need to do is head into printer.cfg and under \[scanner] change `calibration_method: touch` to `calibration_method: scan` and then remove the `CARTOGRAPHER_TOUCH` line from your print start macro.\
\
You will ofcourse need to create a new model by [following this guide.](../classic-installation/calibration.md)

### Do I need to run the calibration while hot or cold?

It doesnt matter! Thats the point of touch! Do what works best for you.

### Does my nozzle need to be clean when doing a touch?

Yes it does, we recommend a silicone nozzle brush, <mark style="color:yellow;">which is now included with all cartographer purchases</mark>. However you can also adjust your retries, heat your nozzle to 150c in your print start and then do the touch. It should smoosh the filament off of the nozzle for you to get a successful touch. Nozzle brush is 100% better however.

### My bed mesh is scanning in Y direction and not X, how do i fix it?

In your `[scanner]` section add `mesh_main_direction: x` to your <mark style="color:yellow;">**printer.cfg**</mark>

### What do I need to add or change in my print start macro?

See [Print Start Macro](../installation-and-setup/installation/print-start-macro.md). But bascially, you just need to make sure your nozzle is no hotter than <mark style="color:red;">**maximum 150c**</mark> and then do a `CARTOGRAPHER_TOUCH` after you do a `BED_MESH_CALIBRATE`

### Does touch work with glass or garolite beds?

It **CAN SOMETIMES** work depending on the thickness of your glass or garolite bed. However we can't say for certain. If its less than 2mm thick theres a good chance however we **accept no responsibility** if it **doesn't** work!&#x20;

### Is it guaranteed that this will work on my printer?&#x20;

As with a lot of things in life, we **can't guarantee 100% compatibility**, it should be compatible with most well built printers, there are obviously some exceptions, the biggest impacting factor is the quality of the Z axis motion. If there is any binding or lack of consistency, then you may find that you will not be able to use this feature. You can still use **regular cartographer scan mode** though!

### I was in the beta, how do I switch back to regular to continue using touch?

```bash
cd ~
sudo rm -rv Carto_TAP
cd ~/klipper/klippy/extras
sudo rm -rv scanner.py
cd ~/cartographer-klipper
git reset --hard HEAD
git clean -xffd
git pull
chmod +x install.sh
./install.sh
sudo service klipper restart
```

Also make sure to edit and remove the cartographer beta `[update manager]` sections of <mark style="color:yellow;">**moonraker.conf**</mark>

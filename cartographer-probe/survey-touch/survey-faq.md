# Survey FAQ

## Frequently Asked Questions

### What do I need to add or change in my print start macro?

See [Print Start Macro](survey-faq.md#print-start-macro-example). But bascially, you just need to make sure your nozzle is at **maximum 150c** and then do a `CARTOGRAPHER_TOUCH` after you do a `BED_MESH_CALIBRATE`

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

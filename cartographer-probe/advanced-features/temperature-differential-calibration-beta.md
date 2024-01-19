# Temperature Differential Calibration (BETA)



{% hint style="danger" %}
After doing any form of Temperature Calirbation, it is essential you re-complete the setup calibration on EVERY model.\
\
IF YOU DO NOT DO THIS, YOU MIGHT DO DAMAGE TO YOUR PRINT SURFACE.
{% endhint %}

This tutorial aims to optimize the temperature compensation parameters and reduce the temperature drift, which takes a long time (sometimes more than 3 hours) to carry out this optimization.

{% hint style="warning" %}
If you are happy with the current performance, and it meets your requirements, this does not need to be run.
{% endhint %}

### Update your printer config file in Klipper.

Modify your printer.cfg, adding the following macro. This should be added to the bottom of your printer.cfg file.&#x20;

{% hint style="danger" %}
This Macro will take your bed up to 110oC, if your printers bed is not capable of that temperature, please lower the M140 commands to a safe temperature for you. \
\
M140 S110 = 110oC\
M140 S95 = 95oC&#x20;
{% endhint %}

```gcode
[gcode_macro DATA_SAMPLE]
gcode:
  M106 S255
  TEMPERATURE_WAIT SENSOR='temperature_sensor Cartographer_coil' MAXIMUM=40
  M106 S0
G28
  G0 Z1
  M104 S250
  M140 S110
  G4 P1000
  CARTOGRAPHER_STREAM FILENAME=data1
  TEMPERATURE_WAIT SENSOR='temperature_sensor Cartographer_coil' MINIMUM=70
  CARTOGRAPHER_STREAM FILENAME=data1
  M104 S0
  M140 S0
  M106 S255
  G0 Z80
  TEMPERATURE_WAIT SENSOR='temperature_sensor Cartographer_coil' MAXIMUM=40
  M106 S0
  G28 Z0
  G0 Z2
  M104 S250
  M140 S110
  G4 P1000
  CARTOGRAPHER_STREAM FILENAME=data2
  TEMPERATURE_WAIT SENSOR='temperature_sensor Cartographer_coil' MINIMUM=70
  CARTOGRAPHER_STREAM FILENAME=data2
  M104 S0
  M140 S0
  M106 S255
  G0 Z80
  TEMPERATURE_WAIT SENSOR='temperature_sensor Cartographer_coil' MAXIMUM=40
  M106 S0
  G28 Z0
  G0 Z3
  M104 S250
  M140 S110
  G4 P1000
  CARTOGRAPHER_STREAM FILENAME=data3
  TEMPERATURE_WAIT SENSOR='temperature_sensor Cartographer_coil' MINIMUM=70
  CARTOGRAPHER_STREAM FILENAME=data3
  M104 S0
  M140 S0
  M106 S255
  G0 Z80
  TEMPERATURE_WAIT SENSOR='temperature_sensor Cartographer_coil' MAXIMUM=40
  M106 S0
  G28 Z0
  G0 Z5
  M104 S250
  M140 S110
  G4 P1000
  CARTOGRAPHER_STREAM FILENAME=data4
  TEMPERATURE_WAIT SENSOR='temperature_sensor Cartographer_coil' MINIMUM=70
  CARTOGRAPHER_STREAM FILENAME=data4
  M104 S0
  M140 S0
```

The macro is then executed, and then the data1, data2, data3, and data4 files are generated in the Klipper folder, note, this can take a very long time.

Once complete, move the files (data1, data2, data3 and data4) to your cartographer-klipper folder.&#x20;

```bash
mv ~/klipper/data1 ~/klipper/data2 ~/klipper/data3 ~/klipper/data4 ~/cartographer-klipper/
```

You will need to ensure your host OS has the libraries and dependancies in it.

```
~/klippy-env/bin/pip install pandas
~/klippy-env/bin/pip install matplotlib
sudo apt-get install libopenblas-dev
~/klippy-env/bin/pip install -v numpy
~/klippy-env/bin/pip install scipy
```

Once installed, run the following script, this will analyse the data from the files that you have moved. You need to ensure that you are on the latest version of our firmware, if you get an error about file not existing, go to our Klipper Setup page and re-run that initial script.&#x20;

```
~/klippy-env/bin/python ~/cartographer-klipper/arg_fit.py
```

After running the script, you will be asked to enter a threshold value. \
\
The default recommendation is`1000`.  if you find there is a lot of deviation from the orange line _**example 1**_, increase the threshold by `500` each time until you get a chart that looks more like _**example 2.**_

After running, four parameters will be generated and a picture will be generated in your bash window and a image in your `cartographer-klipper` folder.&#x20;

(This process is very computationally intensive and takes a while) Please check the picture named fit.png and judge the fitting effect. The picture example is as follows:

<figure><img src="../../.gitbook/assets/fit.png" alt=""><figcaption><p>Example 1</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (16).png" alt=""><figcaption><p>Example 2</p></figcaption></figure>

Once complete, it will generate an image called fit.png as well as show some values in your terminal window.

```
tc_a_a:5.367848131964879e-06
tc_a_b:1.7559290784042338
tc_b_a:0.0007546669217813525
tc_b_b:-343.290029518937
```

Copy the results at the end of the `[cartographer]` section of your config,

**Example below**

```yaml
[cartographer]
serial:
    canbus_uuid: 39df93ji34
speed: 40.
#   Z probing dive speed.
lift_speed: 5.
#   Z probing lift speed.

#   REST OF THE CONFIG REMOVED TO MAKE THIS LESS CLUNKY.

#   End of config section. 
tc_a_a:5.367848131964879e-06
tc_a_b:1.7559290784042338
tc_b_a:0.0007546669217813525
tc_b_b:-343.290029518937
```

Once added, save and restart your config.&#x20;

You will now have to re-calibrate your probe, to do this

```
CARTOGRAPHER_CALIBRATE    
```

Once compelete, SAVE & RESTART your config.&#x20;

{% hint style="danger" %}
After doing any form of Temperature Calirbation, it is essential you re-complete the setup calibration on EVERY model.\
\
IF YOU DO NOT DO THIS, YOU MIGHT DO DAMAGE TO YOUR PRINT SURFACE.
{% endhint %}

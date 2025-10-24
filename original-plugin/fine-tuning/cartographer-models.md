# Cartographer Models

{% hint style="info" %}
Models are not required if you are using Cartographer Survey Touch.&#x20;
{% endhint %}

### Why use models??

There are many different reasons to why you would want to use different models with your probe, these vary from person to person, but they could be as follows:

* Using different print surfaces, such as different PEI / Spring Steel sheets
* Printing at a wide range of temperatures or materials&#x20;

Cartographer models can help manage this, allowing you to essentially have different offsets and different profiles for the different temperatures and build surfaces that you print on.&#x20;

### Using the `default` model.&#x20;

When performing a calibration with the `CARTOGRAPHER_CALIBRATE` command a model is created called `default`. This will be saved to your printer.cfg after you compelte a `SAVE_CONFIG`, this could either be via running the command or performing a save and restart from your webUI.

The `default` model will be loaded automatically when your machine turns on.&#x20;

### Available Commands

* **Viewing Available Models** - `CARTOGRAPHER_MODEL_LIST` - Shows your available models, it also indicates which model is active.\
  \
  Example:&#x20;

```gcode
$ CARTOGRAPHER_MODEL_LIST
// List of loaded CARTOGRAPHER models:
// - default [active]
// - hot
// - cold
// - fysetcpei-hot
// - fysetcpei-cold
```

* **Changing Active Model** - `CARTOGRAPHER_MODEL_SELECT NAME=model` - This command will select and load the model with the name you have selected. \
  \
  Example:&#x20;

```gcode
$ CARTOGRAPHER_MODEL_SELECT NAME=hot 
// Selected CARTOGRAPHER model 'hot'
```

* **Saving New Models** - `CARTOGRAPHER_MODEL_SAVE NAME=model` - command can save the current active model as a new model. This will overwrite any existing model with that given name. \
  \
  You must perform a `SAVE_CONFIG` in order to commit the changes to the config file. \
  \
  Example:&#x20;

```gcode
CARTOGRAPHER_MODEL_SAVE NAME=fysetc-pei-cold
// Cartographer calibration for model 'fysetc-pei-cold' has been updated
// for the current session. The SAVE_CONFIG command will
// update the printer config file and restart the printer
```

* **Deleting Models** - `CARTOGRAPHER_MODEL_REMOVE NAME=model` command will delete the cartographer model with `model` as the name from your config file. \
  \
  You must perform a `SAVE_CONFIG` in order to commit the changes to the config file. \
  \
  Example:&#x20;

```gcode
$ CARTOGRAPHER_MODEL_REMOVE NAME=hot
// Model 'hot' was removed for the current session.
// Run SAVE_CONFIG to update the printer configurationand restart Klipper.
```

# Before You Begin

Before you begin your journey into Cartographer, we've assembled a small list of things to check and be aware of before you start. These will be continued to be mentioned throughout this guide but this is a summary.\
\
If you see the following sections, please take care to READ these as they can be crucial and beneficial to you. As such, please read the entire guide.

{% hint style="info" %}
This box will contain hints and tips that may help with the process.
{% endhint %}

{% hint style="warning" %}
This box contains warnings about the next paragraph/section
{% endhint %}

{% hint style="danger" %}
These boxes contain information that MUST BE FOLLOWED.
{% endhint %}

{% hint style="success" %}
We're you asked to do something? This box will ask you to check if it was successful.
{% endhint %}

* Make sure Cartographer is the mounted within a range of 2.6 to 3mm above the tip of the nozzle.
* Do **NOT** update klipper as soon as a new update is available.
* The Cartographer repo is not dirty, don't press clean.
* Don't use metal brushes.
* Reboot if command not found / option is invalid.
* Cartographer is currently not compatible with beds with embedded magnets such as the Original Prusa Bed, or Mandella Roseworks beds.

## Cartographer Classic vs Survey Touch

Whats the difference you might ask? Check out the[ detailed descriptions here!](../classic-vs-survey-touch.md)

If you received a Cartographer probe that looks like below, you have received a probe pre-flashed with Survey Touch. You should [follow the guide here](touch-installation/).

The box cartographer arrives in will also say "Touch Ready" if it has the latest touch firmware pre-flashed.

Otherwise, you should follow this guide to [classic installation](classic-installation/). If you'd like to use touch, follow [this guide](../firmware/) to update the firmware before following the [Touch Installation Guide](touch-installation/).\


<table data-view="cards"><thead><tr><th></th><th></th><th></th></tr></thead><tbody><tr><td></td><td><img src="../../.gitbook/assets/image (3) (1).png" alt="" data-size="original"></td><td></td></tr><tr><td></td><td><img src="../../.gitbook/assets/image (5) (1).png" alt="" data-size="original"></td><td></td></tr></tbody></table>

## Standard vs Right Angle vs Low Profile

For the majority of users, Cartographer assembled in the Standard orientation will work. This is dependent on your printer however. You can always de-solder the board and switch orientations if you're confident with soldering **(However, damaged caused by this process will void your warranty.)**

## What to do if you get stuck

If you get stuck at any point in this guide. Please visit us on discord ([available here](https://discord.gg/yzazQMEGS2))

If you're having issues within klipper/mainsail, please create a thread in the[ Help & Support ](https://discord.com/channels/1165274913624572014/1229798364514750596)section on discord and PLEASE include the following.

* Printer.cfg
* Klippy.log
* Screenshots of the issue if available.
* A detailed description of what you were doing at the time of this issue.

### Using Touch?

Heres a quick check list of things to check prior to asking for assistance if youre having inconsistent touch results or failures.

* [ ] Is cartographer mounted approx within a range of 2.6-3mm **ABOVE** the nozzle tip?
* [ ] Is your toolhead completely rigid?
* [ ] Checked toolhead for loose screws?
* [ ] Checked toolhead for bad wiring?
* [ ] Checked A/B or  X/Y and Z belt tension?
* [ ] Checked lead screws?
* [ ] Is your nozzle clean?

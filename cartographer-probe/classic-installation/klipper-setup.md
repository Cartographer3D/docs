---
description: Klipper Setup for Classic Mode
---

# Klipper Setup

## Installation of the Cartographer Klipper Module

Clone the Klipper module from GitHub using the following commands, you then need to run our installation script.

```bash
cd ~
git clone https://github.com/Cartographer3D/cartographer-klipper.git
./cartographer-klipper/install.sh
```

This step will automatically create a link to the script and place it in the klipper/klippy/extra directory.

{% hint style="info" %}
If you are in Mainland China, use the following commands instead:

<pre class="language-bash"><code class="lang-bash"><strong>cd ~
</strong><strong>git clone https://gitee.com/NBTP/cartographer-klipper.git
</strong>./cartographer-klipper/install.sh
</code></pre>
{% endhint %}

### Remember to update cartographer via the mainsail/fluidd UI

{% hint style="warning" %}
Legacy Klipper environements running on Python2 will need updating to Python 3.9 or later. The easiest way to do that is a complete fresh install, though we do have a guide that can help that is linked [here  ](https://docs.cartographer3d.com/cartographer-probe/troubleshooting#klipper-environement-running-on-python-2)
{% endhint %}

## Managing Updates via Moonraker

In order to keep up to date with our latest Klipper software, please add the following config to the bottom of your `moonraker.conf` file.

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

{% hint style="info" %}
**Are you from Mainland China?**\
\
Use this alternate moonraker.conf instead.

```yaml
[update_manager cartographer]
type: git_repo
path: ~/cartographer-klipper
channel: stable
origin: https://gitee.com/NBTP/cartographer-klipper.git
requirements: requirements.txt
is_system_service: False
managed_services: klipper
info_tags:
  desc=Cartographer Probe (Gitee)
```
{% endhint %}

upon completion, press SAVE & RESTART and it should now display in the update section of either Mainsail or Fluidd.&#x20;

<figure><img src="../../.gitbook/assets/image (5) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption><p>Cartographer Software updates managed via Moonraker.</p></figcaption></figure>

If you get "Repo is dirty. Detected the following modified files: \['install.sh']", a soft Recovery should fix it.&#x20;

<figure><img src="../../.gitbook/assets/image (4) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

## Finding the Serial or UUID

Note, you need to replace the serial path  or UUID with your probes serial path or UUID, this can be found by running the following commands&#x20;

For USB based probes&#x20;

```bash
ls /dev/serial/by-id/
```

For CAN based probes

```bash
~/klippy-env/bin/python ~/klipper/scripts/canbus_query.py can0
```

Take note of either the Serial ID or the UUID.&#x20;

## New Firmware

Since late August, most probes shipping from directly from Cartographer3D, and a majority of our resellers have pre-flashed with the Cartographer Survey Firmware.&#x20;

If your box or antistatic bag states "Survey Touch Ready", please go here

{% content-ref url="../installation-and-setup/installation/klipper-configuation.md" %}
[klipper-configuation.md](../installation-and-setup/installation/klipper-configuation.md)
{% endcontent-ref %}

If it doesnt, don't worry. You can update your probe using our flashing tool. If you want to configure it as is,  please go to the next page.

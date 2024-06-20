# Klipper Setup

## Installation of the Cartographer Klipper Module

Clone the Klipper module from GitHub using the following commands, you then need to run our installation script.

```
cd ~
git clone https://github.com/Cartographer3D/cartographer-klipper.git
chmod +x cartographer-klipper/install.sh
./cartographer-klipper/install.sh
```

This step will automatically create a link to the script and place it in the klipper/klippy/extra directory.

If you are in Mainland China, use the following command:

<pre><code><strong>cd ~
</strong><strong>git clone https://gitee.com/NBTP/cartographer-klipper
</strong>chmod +x cartographer-klipper/install.sh
./cartographer-klipper/install.sh
</code></pre>

{% hint style="warning" %}
Legacy Klipper environements running on Python2 will need updating to Python 3.9 or later. The easiest way to do that is a complete fresh install, though we do have a guide that can help that is linked [here  ](https://docs.cartographer3d.com/cartographer-probe/troubleshooting#klipper-environement-running-on-python-2)
{% endhint %}

## Managing Updates via Moonraker

In order to keep up to date with our latest Klipper software, please add the following config to the bottom of your `moonraker.conf` file.

```yaml
[update_manager cartographer]
type: git_repo
path: ~/cartographer-klipper
channel: dev
origin: https://github.com/Cartographer3D/cartographer-klipper.git
env: ~/klippy-env/bin/python
requirements: requirements.txt
install_script: install.sh
is_system_service: False
managed_services: klipper
info_tags:
  desc=Cartographer Probe
```

For Mainland China:

```yaml
[update_manager cartographer]
type: git_repo
path: ~/cartographer-klipper
channel: dev
origin: https://github.com/Cartographer3D/cartographer-klipper.git
env: ~/klippy-env/bin/python
requirements: requirements.txt
install_script: install.sh
is_system_service: False
managed_services: klipper
info_tags:
  desc=Cartographer Probe (Gitee)
```

upon completion, press SAVE & RESTART and it should now display in the update section of either Mainsail or Fluidd.&#x20;

<figure><img src="../../.gitbook/assets/image (5) (1) (1) (1).png" alt=""><figcaption><p>Cartographer Software updates managed via Moonraker.</p></figcaption></figure>

If you get "Repo is dirty. Detected the following modified files: \['install.sh']", a soft Recovery should fix it.&#x20;

<figure><img src="../../.gitbook/assets/image (4) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>


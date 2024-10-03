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

# Tweaking the Z offset

Tweaking the Z offset is done slightly differently with Cartographer compared to using a standard probe, for example, with Cartographer you can't use \`PROBE\_CALIBRATE\` to fine tune the offset, as that will reset the 0 point, so you need to tweak it manually.&#x20;

### Klipper Screen

Unfortunatly, due to the way Cartographer works, we advise against doing this via Klipper Screen, as we have seen some sporadic outputs.&#x20;

### Mainsail

If you are using more than just the `default` cartographer model, you will have to load which ever model you want to make the adjustment too,  you do this using the following command, replacing the NAME=hot, with what ever model you are selecting i.e. NAME=sparklybed

`CARTOGRAPHER_MODEL_SELECT NAME=hot`&#x20;

You can adjust your Z Offset in Mainsail using the Z-Offset section of the Toolhead pane.&#x20;

<figure><img src="../../.gitbook/assets/image (5) (1) (1).png" alt=""><figcaption></figcaption></figure>

after making the neccessary adjustments press the `SAVE` button

<figure><img src="../../.gitbook/assets/image (4) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

And then press `SAVE CONFIG`

<figure><img src="../../.gitbook/assets/image (3) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

Once complete, your Z offset change should be evident under model\_offset: under the specific model which was loaded. \
\
NOTE - You will have to adjust the offset for each model you use.&#x20;



###

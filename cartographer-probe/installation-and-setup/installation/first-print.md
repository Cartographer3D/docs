# First Print

<mark style="color:purple;">Last Updated: December 7th 2024</mark>

{% hint style="danger" %}
For SCAN based instructions, see below.
{% endhint %}

## Touch Mode First Print

You might notice your z-offset is a little wrong, this is hugely dependent on too many things, however its simple to fix. Just use the video below as an example.\
\
`scanner_touch_z_offset` is the distance between nozzle and bed after a `CARTOGRAPHER_TOUCH`

Default `scanner_touch_z_offset` is 0.05

{% embed url="https://youtu.be/OoZ2fcD3zlA" %}
video courtesy of Yell on Cartographer Discord
{% endembed %}

***

## Scan Mode First Print

Tweaking the Z offset is done slightly differently with Cartographer compared to using a standard probe, for example, with Cartographer you can't use \`PROBE\_CALIBRATE\` to fine tune the offset, as that will reset the 0 point, so you need to tweak it manually.

#### Klipper Screen <a href="#klipper-screen" id="klipper-screen"></a>

Unfortunatly, due to the way Cartographer works, we advise against doing this via Klipper Screen, as we have seen some sporadic outputs.

#### Mainsail <a href="#mainsail" id="mainsail"></a>

If you are using more than just the `default` cartographer model, you will have to load which ever model you want to make the adjustment too, you do this using the following command, replacing the NAME=hot, with what ever model you are selecting i.e. NAME=sparklybed

`CARTOGRAPHER_MODEL_SELECT NAME=hot`

You can adjust your Z Offset in Mainsail using the Z-Offset section of the Toolhead pane.

![](https://docs.cartographer3d.com/~gitbook/image?url=https%3A%2F%2F3044346320-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FjpCp1KnR8izt0cnWQfZF%252Fuploads%252FLfCgSpSNOdMFzaBFkGg8%252Fimage.png%3Falt%3Dmedia%26token%3D942394ea-51a7-418f-a0e6-fb0e82d9f287\&width=768\&dpr=4\&quality=100\&sign=d9492914\&sv=2)

after making the neccessary adjustments press the `SAVE` button

![](https://docs.cartographer3d.com/~gitbook/image?url=https%3A%2F%2F3044346320-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FjpCp1KnR8izt0cnWQfZF%252Fuploads%252FWKl1xE9jQ8TfH4Zjx9zx%252Fimage.png%3Falt%3Dmedia%26token%3D4e3a3323-1379-448a-a989-67c94c5177bd\&width=768\&dpr=4\&quality=100\&sign=346d8dc2\&sv=2)

And then press `SAVE CONFIG`

![](https://docs.cartographer3d.com/~gitbook/image?url=https%3A%2F%2F3044346320-files.gitbook.io%2F%7E%2Ffiles%2Fv0%2Fb%2Fgitbook-x-prod.appspot.com%2Fo%2Fspaces%252FjpCp1KnR8izt0cnWQfZF%252Fuploads%252FN2OA0cBYSieQwR9NlHpU%252Fimage.png%3Falt%3Dmedia%26token%3Df093ff3c-53cb-43aa-8c50-ce51a91449f2\&width=768\&dpr=4\&quality=100\&sign=83a6205e\&sv=2)

Once complete, your Z offset change should be evident under model\_offset: under the specific model which was loaded. NOTE - You will have to adjust the offset for each model you use.

{% hint style="success" %}
This is the end of the setup and calibration process.&#x20;
{% endhint %}

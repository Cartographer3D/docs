# Classic vs Survey Touch

## Short Version?

Classic uses the regular scanning mode to use cartographer as a Z endstop. Survey Touch does exactly what it sounds like, it touches the nozzle to the bed at print run-time giving you a perfect first layer everytime.

## Long Version?

### Classic

Cartographer is based around an LDC1612 Inductance converter chip. This chip creates an oscillating electric field which then induces a corresponding field in the metal of the steel sheet (or bed itself if close enough) and can read the resonance frequency of this field, and then converts this reading into a digital signal to be processed upstream by the MCU. The resonance frequency changes with a change in distance between the coil and the bed (or spring steel sheet, or whatever metal it is triggering off). As the coil gets closer, the frequency gets higher.

In SCAN mode (AKA Cartographer Classic), we calibrate the Cartographer model (via CARTOGRAPHER\_CALIBRATE and the paper test) so that Carto knows that at a specific frequency reading it is exactly a certain distance from the bed, and it knows the distance between this trigger point and the nozzle tip. So using this logic, Cartographer knows that whenever it reads this specific frequency it knows where the nozzle is.

There is an issue with this however, in that the frequency is affected by both distance to bed and the temperature of the coil/LDC chip. So even if you had the cartographer at the exact same height but changed the temperature of the system, it would read a different frequency.

To fix this we use Temperature Compensation. Temp Comp reads the temperature of the coil board and is then able to adjust the frequency value at which it "Triggers" so that the trigger point is still at the same actual Z height every time.

Now, that's old cartographer. Boo. How does the new hotness work?

### Survey Touch

Cartographer Survey doesn't care about absolute frequency values and what Z height that corresponds to. Survey is all based around the change of signal, specifically it detects when the rate of change of the frequency... changes.

As the Cartographer gets closer to the bed, the frequency value increases at a predictable rate, which we can see as a slope on a graph. When Cartographer stops (because the nozzle has now touched the bed) this slope changes angle and flattens out. The Cartographer Survey software detects this change and stops and now knows that the nozzle has touched the bed. Note that the cartographer is still inducing the electric field into the closes metal body, usually the spring steel sheet or the bed itself. For Cartographer Survey to work it needs to be able to induce this field which means it needs metal beneath it, within a few mm.

The real neat thing about this is that because we are just looking at this change of slope, we don't care that this happens at the exact same frequency every time we run a nozzle probing action. This means that even if the frequency values are different (because of different coil temperatures) we can still detect when the slope changes and therefore know when the nozzle touches the bed. So we don't even need any temperature compensation as we don't care about absolute numbers. Neat!

Finally, to tie all this together. We do a SCAN Z homing, which triggers at a certain frequency (FREQ). Then we can do a SCAN bed mesh which will generate a mesh based around the frequency (and therefore distance) variation from the first trigger FREQ. Same with QGL/Z-Tilt, it's based off of the FREQ. At this point we may not know exactly how far this FREQ trigger distance is to the nozzle, so we do a Survey nozzle probing action and now the system knows the Z difference between the FREQ height, and the nozzle height. The bed mesh will be based off of this new "nozzle is here" value and everything works.

Now, because we work in the real world and each printer is different it is common that there is still an additional fixed offset applied even after the nozzle probing action figures out the bed location. This is due to many factors including thermal expansion between nozzle probing temp and printing temp, flex in the toolhead, flex in the bed, inherent noise, etc. The good news is this offset should be a representation of the "system" as a whole and therefore you can change nozzles/sheets and this offset won't change.

<figure><img src="../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

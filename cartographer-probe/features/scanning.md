---
icon: nfc-directional
---

# Scanning

Cartographer implements a Klipper [probe](https://www.klipper3d.org/Config_Reference.html#probe) interface and exposes functionality similar to what you'd expect from an induction probe, with the benefit of eddy current for accurate measurements.

This means that homing, `QUAD_GANTRY_LEVEL` and `Z_TILT_ADJUST`, simply works as expected, but looks slightly different. Cartographer will lower until the trigger point of 2 mm and will then take 20 readings of the frequency to determine the exact distance.\
This means there is on reason to lift the probe and run a probing move again.

#### Measure probe accuracy

We can check the accuracy of the scan by running `PROBE_ACCURACY`.\
This will run a few probes and output some statistics, like seen below.

> probe accuracy results: maximum 2.000898, minimum 1.999665, range 0.001233, average 2.000008, median 1.999758, standard deviation 0.000449

## Bed mesh calibrate

We can make use of the probes ability to take rapid measurements by scanning as we move quickly across the bed.

After setting up Cartographer, your `BED_MESH_CALIBRATE` macro will by default do this.

To take full advantage, we should increase the density of the mesh. We should be able to move across the bed with a speed of at least 300 mm/s.

To fall back to the default Klipper behavior, run `BED_MESH_CALIBRATE METHOD=automatic` .

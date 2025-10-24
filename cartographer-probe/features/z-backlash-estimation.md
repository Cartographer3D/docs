---
icon: arrow-down-up-across-line
---

# Z Backlash Estimation

We can measure any backlash on the z movements.\
This is useful to increase the precision on any moves done by the Cartographe3D plugin, but also useful to diagnose problems in Z motions, like belt tension and lead screws.

You can run `CARTOGRAPHER_ESTIMATE_BACKLASH CALIBRATE=1`  to calibrate the backlash at your zero reference position.

Can move your toolhead to anywhere on the plate and run `CARTOGRAPHER_ESTIMATE_BACKLASH`  for that position. Your backlash should be similar on all spots on your plate.\
A good test is to run backlash estimation close by your mounting points for whatever drives your Z.

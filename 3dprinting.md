# 3D Printing

### Calibrating Z axis
https://3dprint.wiki/reprap/anet/a8/improvement/autobedleveling

How to calibrate the Z axis

1) Use Pronterface software
2) Use `G28` to home the machine
3) Place a sheet of paper on bed and lower z axis until it is just grabbing the paper
4) Check the height of the extruder by using the command `M114`
5) Once you find the appropriate zero and know what the machine thinks the height is we need to adjust the z axis sensor offset. This is done using the M851 command, your Z height when the extruder is zero will be the parameter, so for 0.6mm z heigh when zerod use `M851 Z0.6`

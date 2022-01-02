# 3D Printing

### Calibrating Z axis
https://3dprint.wiki/reprap/anet/a8/improvement/autobedleveling

Use Pronterface software

1) Heat your printer up to your printing temperature and allow a few minutes for it to expand and settle
    Reset the existing Z-offset to zero

     ```M851 Z0```

2) Home all axes

    ```G28```

3) Move the nozzle to the middle of the bed

    ```G1 X110 Y110```

    (if your bed is 220 x 220)
    
4) Turn off the software endstops with

    ```M211 S0```

5) Move the nozzle down so it is just gripping a piece of standard printer paper
    Set the Z-offset to the displayed value. E.g. if the printer displays a Z-Value of -1.23 enter

    ```M851 Z-1.23```

6) Store it to the EEPROM

    ```M500```

7) Important notice! Enable the endstops again with

    ```M211 S1```

    or the printer head will collide with the bed on the next ```G28``` command
    
### GCode to display location
    m114


### Hole offsets for screws
M2 = 2mm OD of screw. M3 = 3mm OD of screw.

If you want to make it smaller use these sizes and tap. Make sure there is 3 or 4 layers in wall
https://www.boltdepot.com/fastener-information/Metric-Tap-Drill-Size.aspx

However if you want to make it bigger use the following fits:
```
Desired Fit     Clearance Gap (mm)
Press Fit 	    Line to Line
Tight Fit 	    0.127
Normal Fit 	    0.254
Loose Fit 	    0.508
```

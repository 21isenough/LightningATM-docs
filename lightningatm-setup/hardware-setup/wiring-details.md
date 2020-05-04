# Wiring Details

![](../../.gitbook/assets/img_20200209_151632.jpeg)

### Wiring Details

1. USB power cable to supply 5V power to the step up converter (standard USB micro cable can be cut in half and the `USB type A` part use for this).

2. USB micro cable to provide 5V power to the Raspberry Pi Zero (second half of the cable cut in half in step 1).

3. If you are using a step up transformer, that can supply a variable amount of voltage, make sure it is set properly to 12V with a multimeter (by twisting and adjusting the tiny screw).

4. The output of the step up transformer (set to 12V) supplies to coin acceptor with 12V power.

5. The ground connection of the step up transformer must also be connected to a ground pin of the Raspberry Pi Zero (see pin out details below).

6. Attach the Pi camera to the CSI camera port of the Raspberry Pi.

7. To detect button presses, these two cables need to be connected to the button (normally closed connection (NC)).

8. (Optional) Two cables that can be used if your button has an LED inside.

9. Cables that connect the Papirus E-Ink display to the Raspberry Pi Zero. 

fireflies
=========

More at http://tinkerlog.com/howto/synchronizing-firefly-how-to/

Gather all needed parts and tools. From left to right:

    Atmel ATtiny13V-10PU, Digikey ATTINY13V-10PU-ND
    8 pin socket, Digikey A24807-ND
    Capacitor 100u, 6V, electrolyt, Digikey P904-ND
    Capacitor 100n, Digikey 399-4151-ND
    RGB LED, common cathode, ~4000mcd, Lucky Light, LL-509RGBC2E-006
    Phototransistor, OSRAM SFH3310
    3 * 1/4 Watt 100 Ohm (brown, black, black, black, brown) (or brown, black, brown, gold for 4 band resistor)
    2 * 1/4 Watt 100k Ohm (brown, black, black, orange, brown) (or brown, black, yellow, gold for 4 band resistor)
    6 pin header, 2×3
    2 pin header and socket
    Firefly PCB, Tinker Store Firefly
    Ping pong ball (not shown)

The follwing tools are needed:

    Soldering iron and solder
    Diagonal cutters
    Sanding paper
    Drill, 4mm
    Third hand

Solder it

Insert the 100 Ohm resistors R1, R2 and R3 (brown, black, black, black, brown) and the 100k Ohm resistors R4 and R5(brown black, black, orange, brown).

Bend the legs a bit, so that they don’t fall off, if you flip the PCB. Solder them.

Next insert the power connectors. If you have more than one firefly and want them to stick together, take care on which side you put the header and the socket.

Insert the small 100n capacitor and solder it. The orientation does not matter.

Take care when you insert the phototransistor. The short leg (collector) has to be inserted in the upper (+) hole. Now solder it.

Insert the socket. It has a small notch, which must point up.

Solder it.

The 100u capacitor has a long (+) and a short leg (-). On the PCB is a tiny + sign to show, how to insert the capacitor. Now solder it.

Next comes the ISP header. Insert and solder it, if you want to modify the firmware without having to flip out the controller.

If you want to use the LED with a ping pong ball, you may want to use sanding paper to diffuse the LED. Without that, the LED will emit its light only upwards and that doesn’t look nice.

Diffuse LED

It is sufficient if the upper third of the LED is diffuse.

Inserting the RGB LED is a bit tricky. The pins are numbered (in the photo from bottom to top):

    green (short)
    blue (longer)
    GND, common cathode (longest)
    red (shortest)

Pin 1 must be inserted into the square pad. Pin 2 and 3 are going into the pads to the right.

Bend the two inner legs (2 and 3) a bit up.

Solder the RGB LED

That’s how it should look, when you flip the PCB. Now solder the LED.

Insert the ATtiny13V controller. You may have to bend the legs slightly to fit into the socket. Place the controller with one side on a flat surface and bend it slightly. Now turn it around and bend the other 4 legs.

Drill a 4mm hole into the ping pong ball. Use a file to widen the hole a bit until it fits on the LED. Don’t use a 5mm drill or the ball will not stick on the LED.
Program it

This is an optional step and not needed if you have a kit.

Attach your programmer to the six pin ISP header. Check for the orientation. Then download the source code rgb_firefly22.zip and unzip it. Adjust the Makefile to your needs, e.g. configure your programmer. Then simply type make, make fuse and make flash.
Power it up

The circuit is designed for a 5V power supply. I am using 4 rechargeable AA batteries with 4.8V. Please double check how to attach the batteries as there is no reverse voltage protection. The circuit starts with 5 fast red flashes. If you don’t see them immediately, pull the plug and recheck.

If the LED shines in constant green, then it is too bright. Darken the room a bit more. If you put two Fireflies close together, you should be able to see, how they interfere with each other and how they synchronize.

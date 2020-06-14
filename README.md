# fireflies

All credit to Alex Weber from tinkerlog.com.

[Original guide](http://tinkerlog.com/howto/synchronizing-firefly-how-to/)

## Schematics

## Fabicate PCBs

I used DirtyPCB to manufactor the boards. No complaints and pretty cheap for bulk printing.

## Order components

* Atmel ATtiny13V-10PU, Digikey ATTINY13V-10PU-ND
* 8 pin socket, Digikey A24807-ND
* Capacitor 100u, 6V, electrolyt, Digikey P904-ND
* Capacitor 100n, Digikey 399-4151-ND
* RGB LED, common cathode, ~4000mcd, Lucky Light, LL-509RGBC2E-006
* Phototransistor, OSRAM SFH3310
* 3 x 1/4 Watt 100 Ohm (brown, black, black, black, brown) (or brown, black, brown, gold for 4 band resistor)
* 2 x 1/4 Watt 100k Ohm (brown, black, black, orange, brown) (or brown, black, yellow, gold for 4 band resistor)
* 6 (2x3) pin header
* 2 pin header and socket
* Ping pong ball

## Build

The follwing tools are needed:

* Soldering iron and solder
* Diagonal cutters
* Sanding paper
* Drill, 4mm
* Third hand

1. **Solder resistors:** Insert the 100 Ohm resistors R1, R2 and R3 (brown, black, black, black, brown) and the 100k Ohm resistors R4 and R5(brown black, black, orange, brown). Bend the legs a bit, so that they don’t fall off, if you flip the PCB. Solder them.

2. **Solder power connections:** If you have more than one firefly and want them to stick together, take care on which side you put the header and the socket.

3. **Solder small capacitor:** Insert the small 100n capacitor and solder it. The orientation does not matter.

4. **Solder Phototransistor:** Take care when you insert the phototransistor. The short leg (collector) has to be inserted in the upper (+) hole.

5. **Solder the microchip socket:** Insert the socket. It has a small notch, which must point up.

6. **Solder the larger capacitor:** The 100u capacitor has a long (+) and a short leg (-). On the PCB is a tiny + sign to show, how to insert the capacitor. Now solder it.

7. (Optional) **Solder ISP header:** Insert and solder it, if you want to modify the firmware without having to flip out the controller. This step is necessary on your first board you build if you are making a few of these.

8. **Disfuse LED:** Use sandpaper to diffuse the LED. Without that, the LED will emit its light only upwards and that doesn’t look nice. It is sufficient if the upper third of the LED is diffuse.

9. **Solder LED:** This is a bit tricky. The pins are numbered (in the photo from bottom to top):

    * green (short)
    * blue (longer)
    * GND, common cathode (longest)
    * red (shortest)

    Pin 1 must be inserted into the square pad. Pin 2 and 3 are going into the pads to the right, so bend the two inner legs (2 and 3) in one direction.

10. **Insert the ATtiny13V controller:** You may have to bend the legs slightly to fit into the socket. Place the controller with one side on a flat surface and bend it slightly. Now turn it around and bend the other 4 legs.

11. **Insert Pingpong ball:** Drill a 4mm hole into the ping pong ball. Use a file or sharp knife to widen the hole a bit until it fits on the LED. Don’t use a 5mm drill or the ball will not stick on the LED.

## Programming the chip

### Dependencies

* **GCC make**
  _windows 10:_
  1. Install [chocolatey](https://chocolatey.org/docs/installation)
  2. `choco install make`

* **avrdude**
  _windows 10:_
  1. Download & install winavr
* **usbasp programmer** (alternatives will exist, this is just the one I used)
  _windows 10:_
  1. Download and extract USBasp-win-driver-x86-x64.zip
  2. Run installDriver.exe from within
* **git bash**

### Test ISP connection

This is the most difficult part. We are going to build and flash the chip, using the programmer connected to the ISP (6pin (2x3) pin on board). The most important aspect is to get the ISP connection the right way around. Any problems will be a software problem more than a hardware one! Compare the number on the PCB next to the ISP header with the schematics to get the correct orientation.

Once connected, you can test a commmand in order to see if the you have made a connection to the microcontroller.

```bash
avrdude -F -c usbasp -p t13 -B 10
```

**Expected output:**
> avrdude.exe: set SCK frequency to 93750 Hz
> avrdude.exe: AVR device initialized and ready to accept instructions
>
> Reading | ################################################## | 100% 0.00s
>
> avrdude.exe: Device signature = 0x1e9007
>
> avrdude.exe done.  Thank you.

### Configure

Depending on your programmer (usbasp), and any devations from the ATtiny13V controller, you may need to change the Makefile to suit your setup.

### Flash

1. `make`
2. `make fuse`
3. `make flash`

## Power On

The circuit is designed for a 5V power supply. To test, you can use 5v from a Raspberry Pi. It also is possible to use 4 rechargeable AA batteries with 4.8V. Please double check how to attach the batteries as there is no reverse voltage protection. The circuit starts with 5 fast red flashes. If you don’t see them immediately, pull the plug and recheck.

If the LED shines in constant green, then it is too bright. Darken the room a bit more. If you put two Fireflies close together, you should be able to see, how they interfere with each other and how they synchronize.

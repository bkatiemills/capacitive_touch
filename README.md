# A basic intro to capacitive touch sensors

Using some simple circuits, freely available arduino libraries, and a touch sensor that can be made out of readily available materials like tinfoil or even specially treated textiles, you can make a _capacitive touch sensor_ to integrate into interactive art and costuming projects. In this tutorial, we'll set up a simple circuit to accomplish this along with the basic theory on how this works, and set up a teensy microcontroller to generate a series of different effects on an LED strip based on user interactions with the touch sensor.

## Setting up the circuit

For this circuit, you'll need:

 - A teensy 2 (many, many microcontollers will work just as well, but these instructions are written for the teensy 2).
 - an X kOhm resistor
 - a capacitive touch sensing foil, like a piece of textile teated with pyrrole, or even just a piece of tinfoil
 - a ring of 16 neopixels (this is just for an example output; you can hook anything you want up to your capacitive touch sensing circuit).
 - a bunch of jumper wires
 - two double-sided alligator clips

Set up your circuit as follows:

![basic captouch circuir](basic-setup_bb.svg)

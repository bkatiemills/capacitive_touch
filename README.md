# A basic intro to capacitive touch sensors

Using some simple circuits, freely available arduino libraries, and a touch sensor that can be made out of readily available materials like tinfoil or even specially treated textiles, you can make a _capacitive touch sensor_ to integrate into interactive art and costuming projects. In this tutorial, we'll set up a simple circuit to accomplish this along with the basic theory on how this works, and set up a teensy microcontroller to generate a series of different effects on an LED strip based on user interactions with the touch sensor.

## Setting up the circuit & software

### Supplies

For this circuit, you'll need:

 - A teensy 2 (many, many other microcontollers will work just as well, but these instructions are written for the teensy 2).
 - a 100 kOhm resistor
 - a capacitive touch sensing foil, like a piece of textile teated with pyrrole, or even just a piece of tinfoil
 - a ring of 16 neopixels (this is just for an example output; you can hook anything you want up to your capacitive touch sensing circuit).
 - a bunch of jumper wires
 - two double-sided alligator clips
 - 0.1 pitch male-male header pins if they aren't already soldered to your teensy
 - a USB cable with the right connections to connect your teensy to your laptop

### Prep

Solder your header pins to your teensy, and some stripped leads to your neopixel ring. Your instructor might have already done this for you!

### Circuit construction

Set up your circuit as follows:

![basic captouch circuit](basic-setup_bb.svg)

> **How it works:** the resistor and capacitive sensor you've plugged in above form an _RC circuit_. When a voltage is applied to this circuit (in this case from the F0 pin), a charge builds up on the capacitor. When this voltage is removed, the charge discharges (in this case to pin F4); the amount of time it takes for this discharge to proceed is proportional to the product of the resistance and capacitance of the circuit - the more capacitance, the longer the discharge time. The software library we're using will apply small, rapid charges to the capacitor and measure the time it takes for them to discharge. When a grounding plane (such as your hand) gets close to the sensor, its capacitance increases, thus increasing the time it takes for the capacitor to discharge.

### Software setup

To control the details of how our microcontroller interprets capacitive touch signals and translates that to behavior on our LED ring, we're going to program it using the Arduino IDE (integrated development environment - if you've never seen something like this before, this is a tool that lets you write code and send it to your microcontroller in a form it can understand). Setup as follows:

1. Install the Arduino IDE, at least version 2.2.x.
2. We need to let the Arduino IDE know how to compile software for the teensy. Navigate **Arduino IDE -> Settings**, and under *Additional board manager URLs*, add `https://www.pjrc.com/teensy/package_teensy_index.json` to the list (separated from whatever else is in the list by a comma, if there's anything else there).
3. Click on the 'Boards Manager' icon on the left of the Arduino IDE (the left column will be titled 'BOARDS MANAGER' when you've chosen the correct one).
4. Type `teensy` in the search box in the boards manager column, and click *INSTALL* under 'Teensy (for Arduino IDE 2.0.4 or later)'. This will install what you need to communicate with your teensy.

![board manager IDE settings](arduinoIDEboards.png)

5. Next, plug your microcontroller into your laptop with a USB cable. In the Arduino IDE, navigate *Tools -> Board -> Teensy (for Arduino IDE 2.0.4 or later) -> Teensy 2.0*
6. Also in the Arduino IDE, click on *Tools -> Port*, and select the port under *teensy ports*; there should only be one, and it should be labeled (Teensy 2.0).
7. At this point, your microcontroller is connected to your computer, and your Arduino IDE knows how to compile code in a way that the microcontroller will understand. Copy the contents of [this tbd file] to the editor on the right hand side of the Arduino IDE, and click the rightward-pointing arrow near the top left to compile the code and send it to your microcontroller.
8. Finally, in the Arduino IDE, navigate *Tools -> Serial Monitor*. The serial monitor is where you can see your microcontroller sending messages back to your laptop; we'll use this feedback to understand the behavior of our capacitive touch sensor in what follows.

## Interpreting capacitive touch sensor signals

Have a look at the serial monitor output you connected to above. After the automatic calibration step completes, you should see three readings, labeled 'reading', 'mean' and 'sd' (for standard deviation). The first column is the raw reading the teensy is making that is proportional to how long it takes your RC circuit to discharge a small charge; as you can see, even just sitting on the table, it's quite _noisy_ - it jumps around all on its own, due to ambiant conditions in the room. We need a way to tell the difference between this number changing due to something interesting happening (like you touching the sensor), versus this number changing due to noise alone.

If you just watch the reading column for a few seconds, you'll see that it appears random, but still sticks to a neighborhood of values. A good first guess for something like this is that those random readings might be coming from a _bell curve_: a random distribution characterized by an average value, and a typical width. The average is the value the random numbers tend to stick close to; the width, or _standard deviation_, is how far away you can expect typical random fluctuations to get from the average.

[more explanation needed, but can this be more fun?]



[practical discussion of how we're autodetecting background, separating signal].

## Programming different LED behaviors

[walk through all the different presets]

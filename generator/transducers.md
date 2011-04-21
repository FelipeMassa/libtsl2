#TRANSDUCERS

##Introduction:

This document is meant to explain all the details known about the various
transducers used in this lab, so that the information is not lost to future
generations.


##Thermocouples:

There are six of them: 5 Type T and 1 Type K. When wiring these to the USB-DAQ,
make sure at least one of the thermocouples shares a ground with one of the
analog grounds. I did this with a short piece of extra wire. This keeps the
device from giving inaccurate readings due to static build-up.

###Type T Thermocouples (x5):

**+:** Blue
**-:** Red

###Type K Thermocouple (x1):

**+:** Yellow
**-:** Red


##Load Bank Power Transducer:

This device uses a high-precision resistor to measure the current running
through the system, which can be converted to power by multiplying by the known
voltage through the system.

**+:** White
**-:** Black

###Conversion:

    kW = 80 * volts


##Load Cells:

This device operates using strain gages internally, but lucky for us it's all
black-boxed. All you need to do is feed it 5V power from the USB-DAQ and take
analog readings!

**+5V:** Red
**Gnd:** Black
**+Out:** White
**-Out:** Brown

###Conversion:

    gallons = 4214 * volts - 10


##Flow Meters:

These devices return frequencies and not proportional voltage signals.

###Shop Water:

This device is known to be returning garbage values. It will likely be replaced,
and was not used for this lab.

**+:** White
**-:** Red

####Conversion:

    gpm = 0.002 * frequency

###Jacket Water:

This device is known to have been sized larger than ideal, and as such is best
for detecting relatively high flow rates on the part of the jacket water. It
also has enough copper particulate inside it that it may sometimes get stuck.
Tapping on the transducer usually fixes it.

**+:** White
**-:** Red

####Conversion:

    gpm = 0.1 * frequency

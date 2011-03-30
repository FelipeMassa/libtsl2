#TRANSDUCERS

##Introduction:

This document is meant to outline some basic research I did on the transducers
used in this lab, so that a future student or faculty member may have direction
on how to replace instrumentation for the pump performance lab if they choose
to do so.

## Flow Meter:

### Make/Model: Foxboro 1 1/2 - 81F5C1

This is the only transducer that requires a general DAQ tool to read. One bases
their measurement on the primary frequency of the input signal, which is within
the range of about +/- 1 V. The unit has a "meter factor" of 
245.6 pulses/gallon. In other words:

    GPM = (60/245.6)*f

This should be in the included VI.

## Pressure Transducer:

### Make/Model: Daytronic 513-75D

### Web Site: http://www.daytronic.com/products/trans/t-513PT.htm

This unit seems to return analog voltage, with the following specs, with a full-
scale range of 75 psid and an output of 2 mV/V. Therefore, it should be
relatively simple to use LabVIEW to measure it.

## Torquemeter:

### Make/Model: S. Himmelstein & Co., MCRT 48201V-2308-191

### Web Site: http://www.himmelstein.com/48200v.asp

This unit is a *digital* torquemeter, and communicates with devices through a
serial port. This is one of the primary reasons, besides time, that I decided
not to try converting this lab to use LabVIEW throughout.

An important caveat with the torquemeter: Its RPM measurements are sound and
its horsepower calculation is correct given its RPM and torque readings.
**HOWEVER**, the torque reading is about ten times too large. Reasons for this
are currently unknown.

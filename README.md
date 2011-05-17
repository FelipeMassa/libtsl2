# libtsl2

## What's this?

Remember [this gem](https://github.com/jesusabdullah/libtsl)? Well, I'm the TA
for that class now. Libtsl2, instead of being my homework, will consist of tools
and goodies used to actually *run* the labs.

## What's in it?

### /transient_convection/

#### /transient_convection.cmbl:
We used Logger Pro to do the first lab. It's
pretty trivial to set up in terms of computers, so I just went and did it.
Basically, we're just recording one (two for extra fun) temperature(s) with a
type-K thermocouple (we also have the apparatus for a type-T but the Vernier
sensors don't roll that way) every fifteen seconds over the course of 1.5--2
hours.

Perhaps interestingly, the cmbl format is "just" xml.

### /low-temp_viscosity/

#### /factor_finder.xlsx :
Our viscometer gives a non-united number, and in order
to get the actual viscosity (in centiPoise), one needs to use a "factor finder,"
which is a glorified lookup table. The factor is a function of spindle model
(either RV- or LV-, then a number 1-7---for example, LV-2) and set RPM.

Last year, I implemented a lookup table using python. However, engineers
looove Excel, so I made an analogous lookup table with Excel.  The magic is in
a function that looks like this:

    =vlookup(A2,'Factor Finder'!A4:K14,hlookup(B2,'Factor Finder'!B2:K3,2,FALSE)+1,FALSE)

The basic API for *vlookup* is like this:

    =vlookup(look_for_this_in_first_column, range_of_your_table, output_column_no, exact_numeric_answer_y_or_n)

hlookup is analogous, except it searches by row and not by column. The "lookup"
family of functions can't look for two things at once, so we use an intermediate
hlookup to get the correct column number.

Alternately, just use the cardboard slidey-thing. It's your time. ;)

### /temp_rods/

#### /temp_rods.vi :
This is a LabVIEW VI that takes measurements from 10 thermocouples using our
National Instruments USB DAQ box. Essentially, this is all it does. It has a lot
of bells and whistles, but could definitely use some fine-tuning.
Note that the box doesn't have a cold-junction compensator built-in, so we
simply use a constant for room temperature and hope that the inaccuracy this
introduces isn't important.

**It should be noted that this lab had issues with the DAQ box returning garbage
values after roughly two minutes of use. This may be solved by grounding at
least one of the thermocouples with the "AI_GND" plug on the NI DAQ box, as
later shown to work in the case of the generator lab.**

#### /temp_rods.pdf :
This is a print-out of the associated VI.

#### /boiler_directions/ :
This folder contains a LaTeX document describing how to use the boiler required
for this experiment. It includes a picture!


### /needle_probes/ :

I ran out of time to fix the Guarded Hot Plate apparatus. Reportedly, it has a
busted flux sensor. It actually has three of them, so one should be able to fix
it by disconnecting them and reconnecting them until some combination of 2/3 of
them behaves as expected. Alternately, one could dig up a replacement HFS
somewhere and use that.

Anyways: The measurement stuff for
[my thesis](http://github.com/jesusabdullah/anisotropy_testtools) is pretty
much ready to go, so we're going to have students do the isotropic version of
this instead.

The code used to actually run the experiment is *not* included, because it's not
mine.  Look into Matthew Sturm's research if you are interested. Some details:
It uses a Campbell CR10X data logger, a hand-made needle, some D-cell batteries
and a relay switch to heat the needle, and a thermocouple or two and a voltmeter
for measurements. The original code used for analysis was written for
[IGOR Pro](https://secure.wikimedia.org/wikipedia/en/wiki/IGOR_Pro), but the
[stuff I wrote](https://github.com/jesusabdullah/anisotropy_testtools/blob/master/testtools.py)
uses python, and I expect that the students will just use Excel.

####/equations.tex :

This is the source code for the corresponding pdf file that describes the
equations necessary to use with this lab.

####/equations.pdf :

This is the compiled version of the corresponding LaTeX file that describes the
equations nessary to use with this lab.


### /pump/

#### /rpm_meter.vi

Only one of the transducers for the pump performance lab was measured with
LabVIEW. This VI reads in voltage over an overkill sampling window, finds the
fundamental frequency, and converts the result to GPM.

#### /transducers.md

This document details some research I did on the transducers used for this lab,
for future reference. It includes important information about gross inaccuracy
in one of the sensors, so if you are doing this lab, *please* read it.


### /generator/

#### /generator.vi

This is the VI that gathers all the data from the generator. There is a lot of
stuff to measure!

#### /generator.pdf

I was proud of the front panel, so I made a .pdf printout to share this VI with
my friends!

#### /transducers.md

This document details most of what's known about the transducers used for this
lab. It includes which wires are which, the conversion factors, and more.

### /inventory.xls (WORK IN PROGRESS)

This is an Excel spreadsheet detailing what equipment we have and where it is located/stored.

### /extras/

This folder contains some sub-VIs written for various labs. They tend to be
the sort of VIs that should have room for reuse.

#### /range.vi

This VI implements the range function as seen in such languages as python.
It looks something like this:

                              _______________
                             |               |
    O---[from (default 0)]-->|   R A N G E   |
                             |---------------|
    O---[to (required)]----->|               |O==[1-D array (from, from+every...to-1)]==>
                             |               |
    O---[every (default 1)]->|    *  *  *    |
                             |_______________|


and is roughly equivalent to range(from, to, every).

#### /push.vi

This VI makes pushing data to the end of an array easy:

                              _______________
                             |               |
                             |               |
    O===[Original Array]====>|     *PUSH*    |
                             |               |O==[New array w/ pushed element]==>
                             |               |
    O---[New element]------->|               |
                             |_______________|


Note that, unlike many things called "push," in LabVIEW you hardly ever modify
an actual variable in-place. This is no exception; it's pretty much a new array
coming out.

#### /pop.vi

`push.vi`'s brother:
                              _______________
                             |               |
                             |               |
                             |     *POP*     |O==[New array w/ missing element]==>
    O===[Original Array]====>|               |
                             |               |
                             |               |O---[Popped element]------->
                             |_______________|


Like `push.vi`, this doesn't really modify the original array in-place; it just
gives you the last element of the array, plus an array without that last
element.

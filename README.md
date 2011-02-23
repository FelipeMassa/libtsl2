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

#### /temp_rods.pdf :
This is a print-out of the associated VI.

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

### /extras/

This folder contains some helper tools that aren't associated with any
particular lab. Over time, I may add these to a legit LabVIEW library.

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
                             |               |
                             |_______________|


and is roughly equivalent to range(from, to, every).

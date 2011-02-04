# libtsl2

## What's this?

Remember [this gem](https://github.com/jesusabdullah/libtsl)? Well, I'm the TA
for that class now. Libtsl2, instead of being my homework, will consist of tools
and goodies used to actually *run* the labs.

## What's in it?

### /transient_convection/

#### /transient_convection.cmbl (*COMING SOON!*):
We used Logger Pro to do the first lab. It's
pretty trivial to set up in terms of computers, so I just went and did it.
Basically, we're just recording one (two for extra fun) temperature(s) with a
type-K thermocouple (we also have the apparatus for a type-T but the Vernier
sensors don't roll that way) every fifteen seconds over the course of 1.5--2
hours.

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

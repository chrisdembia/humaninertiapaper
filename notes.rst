=======
Outline
=======

Title: Object oriented implementation of Yeadon's human inertial model

Introduction
============

- What human inertia calcs are
- Why you need them
- How people use them
- How they obtain
- Review of existing software
- Winter text book on biomechanics (compare height and mass)
- Intro to Yeadon's model and citations to him.
- Why we use Yeadon's model.
  ** CHRIS: goal is also to clear up some of the implementation details of the method, that are not clear from the paper alone. therefore promoting consistent use of the method

Find papers that use this model:
- Alison Sheet's work
- compare to her matlab code

Yeadon's Method
---------------

Brief explanation
FIGURE - measurements
FIGURE - cfg

Since not all levels "lengths" are not measured, etc, we average some, the corresponding perimeter must be measured at the correct mid-arm point, etc.

There are x segments: (1).. (2) , (3)... say how many solids thye have each.

There are x degrees of freedom: (1), (2)...etc.

There are segments, composed of solids lofted between parallel stadia.

Location of hip joint centres with respect to pelvis: unspecified in yeadon papers?

segments are rigid bodies, composed of solids.

see comment in yeadon-ii about trapezium when t = 0

solids comprising a segment have coincident longitudinal axis.

we also use dempster's densities.

intended purpose was aerial movements: twisting somersaults on a trampoline.

Software Design
===============

- Utility
- proven advantage
- long term advantage
- mainenance and potential for growth
- algorithms
- object model (pylint may generate UML diagrams)
- modularity
- open source
- how does this software make it easy to integrate with anaylysis
- software license

Verification - chris
============

- demonstrate that it achvies purpose
- prove improvement over existing
- proof of principle example
- Jason will look at diss but for now compare to Yeadon's code.
- Show comparison numeric tables.
- test data
- direct link

How to install the software
===========================

cross platform

How to use the software - chris
=======================
- Command line
- UI
- ??GUI!!
- show basic usage then a bigger example
- FIGURE spinning ice skater example
- input file format description
- code snippets

SYMMETRY IS ON BY DEFAULT

Example
=======

- (Results)
- Person sitting on bicycle.
- Reference the software where this is implemented.
- Show numerical numbers of benchamrk bicycle and then the examples after
- can we show something that goes beyond just calculating the numbers and the images?
- compare easy of generating inertia for different models (rigid rider vs multisegment rider)
- FIGURE 

crtl-v, select rows, ctrl-i to insert on each row, esc

Given measurements
------------------
talk about how the data for female1, male1, etc. was gathered.


 *** DONE
notes on measurementS:
-reorder PTC to CTP
-change lineweights or move labels of P T C on the actual guy
- or make a note about what the colors mean
  ^^^ DONE

Style
-----
Chris: I try to type numbers out as numerals rather than as words whenever possible; I think it's easier to read. However, I understand it's conventional to write out small numbers so I'm fine with us doing that.

we vs passive

Chris todo 121226
-clean up figures again
    centre
    <s> is not the name of the segment, more just a body part.
-write about measurements
-write about object model
    finish with validation.

    -departures (read papers over again)
    -software design
    -verification: outline the section
    -finish writing tests
    -write usage


yeadon's model
implementation
software design
validation
usage


Chris decided to use joint centre but center of mass in some attempt to be
consistent with Yeadon's naming.


Departures
----------

yeadon - i
    concerned with using cinematography to back out orientation angles
        external somersault, tilt, twist
        internal angles as well

        we are not concerned with this

yeadon - iv

Chris says: I'm starting to come off as Yeadon's only academic contribution is his 1990 ii paper. I want to be careful that we don't have that tone.

Figures
-------

Chris 121228


    -umldiagram include
    -explain the object model, etc.


    -finish writing human tests so i can write the verification portion of the
    paper.

    -if Jason doesn't get to it first, take care of coordinate transformation
    stuff.

    add language about body fixed vs space fixed.


    ISEG does nothing with configuration

    when describing what inertia for human, segment,solid is: make sure i specify what it is with respect to: that a segment's inertia is with respect to its own com, not the human's, but is in the human's frame.

    give an example of the usage of translate coord system, since the language is confusing.

    translate coordiante system does not affect the inertia tensor since it's still about the center of mass.

    line 313 of test_solid, says we found a minor erro rin yeadon's paper, make sure we mention this in our paper.

    - explain how we fixed the formulae for a truncated cone, etc. choosing b = 0.

    (1) finish testing truncated solid assumption. DONE
    (1.5) figure out the difference between ISEG computations and ours.
        The difference is mostly in the densities (10%), though there's still error in total mass after using Chandler's density in yeadon (1%)
    (2) finish testing human: transformations, etc.
        1- ISEG comparison
        2- translate
        3- rotate
        4- combine
    (5) new interface for rotating, translating the system.
    (3) finish GUI.
    (4) write paper.

    do an internal write-up of the issue i hit: degenerate if t0 = 0, so swap the situation. put this in the source code.
    say in the paper that we do not do the thin trapezium thing.

    130209
        Just realized that for symmetry, we average the measurements. ISEG averages the inertial properties after they're calculated.
        used a precise PI everywhere in ISEG
        changed thicknesses to be 0.00000001 * r or something: made the discrepancy worse
            the issue is with the limbs, across multiple segments. the way i do symmetry is NOT an issue
                i'll just go solid by solid in the arms...

        the meas 's i give to yeadon are already averaged. so that's why yeadon gives the same results...for the symmetry...

        ADD TO THE DOCUMENTATION that the inertia tensor is about the center of mass.
        INTRODUCE REFERENCE FRAMES INTO EVERYTHING.

        ah so i'm not sure it makes sense to have the
        translate/rotate/transform functions, since translate is trivial, and
        rotate can be done by altering the somersault, twist, etc. though that's
        not quite as simple. alternatively, the user can apply their own
        rotation afterwards.


                    ****
        130320: Jason said that we should at least compare our masses/
        inertias***/ ("can just measure the masses of a person), and list what
        Yeadon returns, and explain away any discrepancies.

            make a table that compares our output to HIS output, don't fit his
            to ours, just calculate results using ours that match his.

            there was a difference of default density set.

                    ****


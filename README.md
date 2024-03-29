## Historical Record: Original gdtoa-tests

The [Embedded Artistry gdtoa](https://github.com/embeddedartistry/gdtoa) library includes modernized test cases based on the test applications originally used with the archive. The original tests and test data is kept as a reference within this repository.

Please note that this repository is archived.

## Original README

This directory contains source for several test programs:

dt is for conversion to/from double; it permits input of pairs of
32-bit hex integers as #hhhhhhhh hhhhhhhh (i.e., the initial '#'
indicates hex input).  No initial # ==> decimal input.
After the input number is an optional : mode ndigits
(colon, and decimal integers for parameters "mode" and "ndigits"
to gdtoa).

Qtest, ddtest, dtest, ftest, xLtest and xtest are for conversion to/from

	f	IEEE single precision
	d	IEEE double precision
	xL	IEEE extended precision, as on Motorola 680x0 chips
	x	IEEE extended precision, as on Intel 80x87 chips or
			software emulation of Motorola 680x0 chips
	Q	quad precision, as on Sun Sparc chips
	dd	double double, pairs of IEEE double numbers
		whose sum is the desired value

They're all similar, except for the precision.  They test both
directed roundings and interval input (the strtoI* routines).
Lines that begin with "r" specify or interrogate the desired rounding
direction:

	0 = toward 0
	1 = nearest (default)
	2 = toward +Infinity
	3 = toward -Infinity

These are the FPI_Round_* values in gdota.h.  The "r" value is sticky:
it stays in effect til changed.  To change the value, give a line that
starts with r followed by 0, 1, 2, or 3.  To check the value, give "r"
by itself.

Lines that begin with n followed by a number specify the ndig
argument for subsequent calls to the relevant g_*fmt routine.

Lines that start with # followed by the appropriate number of
hexadecimal strings (see the comments) give the big-endian
internal representation of the desired number.

When routines Qtest, xLtest, and xtest are used on machines whose
long double is of type "quad" (for Qtest) or "extended" (for x*test),
they try to print with %Lg as another way to show binary values.

Program ddtest also accepts (white-space separated) pairs of decimal
input numbers; it converts both with strtod and feeds the result
to g_ddfmt.

Program dItest exercises strtodI and strtoId.

Programs dItestsi and ddtestsi are for testing the sudden-underflow
logic (on double and double-double conversions).

Program strtodt tests strtod on some hard cases (in file testnos3)
posted by Fred Tydeman to comp.arch.arithmetic on 26 Feb. 1996.
To get correct results on Intel (x86) systems, the rounding precision
must be set to 53 bits.  This can be done, e.g., by invoking
fpinit_ASL(), whose source appears in
http://www.netlib.org/ampl/solvers/fpinit.c .

These are simple test programs, not meant for exhaustive testing,
but for manually testing "interesting" cases.  Paxson's testbase
is good for more exhaustive testing, in part with random inputs.
See ftp://ftp.ee.lbl.gov/testbase-report.ps.Z .

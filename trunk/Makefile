/************************************************************************
  DISCLAIMER:
  This software was produced by the National Institute of Standards
  and Technology (NIST), an agency of the U.S. government, and by statute
  is not subject to copyright in the United States.  Recipients of this
  software assume all responsibility associated with its operation,
  modification, maintenance, and subsequent redistribution.

  See NIST Administration Manual 4.09.07 b and Appendix I.
************************************************************************/

# This Makefile uses five compiler flags. 
# -DAA means the interpreter should be able to handle an A-axis. 
# -DBB means the interpreter should be able to handle a  B-axis. 
# -DCC means the interpreter should be able to handle a  C-axis.
# -DAXIS_ERROR means reading NC code referencing an axis the interpreter
#    cannot handle should cause the interpreter to signal an error.
#    Without this flag, if the interpreter cannot handle an axis, any
#    syntactially valid NC code word starting with the axis letter is
#    read and ignored.
# -DALL_AXES means the interpreter should print canonical commands
#    that include all six axes, regardless of whether the interpreter
#    can handle those axes. Values put into the canonical command calls
#    for non-handled axes are always zero.

# This Makefile includes code for making six executables out of a
# possible 29. The others can be made similarly.

COMPILE = g++ -c -v -g
LINK = g++ -v

canon.o: canon_pre.cc canon.hh
	$(COMPILE) -o canon.o canon_pre.cc

canon_abc.o: canon_pre.cc canon.hh
	$(COMPILE) -DAA -DBB -DCC -o canon_abc.o canon_pre.cc

canon_ac.o: canon_pre.cc canon.hh
	$(COMPILE) -DAA -DCC -o canon_ac.o canon_pre.cc

canon_b.o: canon_pre.cc canon.hh
	$(COMPILE) -DBB -o canon_b.o canon_pre.cc

driver.o: driver.cc canon.hh rs274ngc.hh rs274ngc_return.hh
	$(COMPILE) -o driver.o driver.cc

rs274: rs274.o canon.o driver.o
	$(LINK) -o rs274 rs274.o canon.o driver.o -lm

rs274.o: rs274ngc_pre.cc canon.hh  rs274ngc.hh rs274ngc_errors.cc
	$(COMPILE) -o rs274.o rs274ngc_pre.cc

rs274abc: rs274abc.o canon_abc.o driver.o
	$(LINK) -o rs274abc rs274abc.o canon_abc.o driver.o -lm

rs274abc.o: rs274ngc_pre.cc canon.hh rs274ngc.hh rs274ngc_errors.cc
	$(COMPILE) -DAA -DBB -DCC -o rs274abc.o rs274ngc_pre.cc

rs274ac: rs274ac.o canon_ac.o driver.o
	$(LINK) -o rs274ac rs274ac.o canon_ac.o driver.o -lm

rs274ac.o: rs274ngc_pre.cc canon.hh rs274ngc.hh rs274ngc_errors.cc
	$(COMPILE) -DAA -DCC -o rs274ac.o rs274ngc_pre.cc

rs274b: rs274b.o canon_b.o driver.o
	$(LINK) -o rs274b rs274b.o canon_b.o driver.o -lm

rs274b.o: rs274ngc_pre.cc canon.hh rs274ngc.hh rs274ngc_errors.cc
	$(COMPILE) -DBB -o rs274b.o rs274ngc_pre.cc

rs274_all.o: rs274ngc_pre.cc canon.hh rs274ngc.hh rs274ngc_errors.cc
	$(COMPILE) -DALL_AXES -o rs274_all.o rs274ngc_pre.cc

rs274_all: rs274_all.o canon_abc.o driver.o
	$(LINK) -o rs274_all rs274_all.o canon_abc.o driver.o -lm

rs274_no.o: rs274ngc_pre.cc canon.hh rs274ngc.hh rs274ngc_errors.cc
	$(COMPILE) -DAXIS_ERROR -o rs274_no.o rs274ngc_pre.cc

rs274_no: rs274_no.o canon.o driver.o
	$(LINK) -o rs274_no rs274_no.o canon.o driver.o -lm

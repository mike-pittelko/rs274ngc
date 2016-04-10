This is the RS274 (G-code) Interpreter developed for the Next Generation Controller project.

It reads numerical control code and produces calls to a set of canonical machining functions. The interpreter is a software system written in the C++ programming language. The output of the interpreter may be used to drive 3-axis to 6-axis machining centers. Input to the interpreter is RS274 code in the dialect defined by the Next Generation Controller (NGC) project, with modifications. The interpreter may be compiled as a stand-alone computer program or may be integrated with the NIST Enhanced Machine Controller (EMC) control system. Input can come from a file or from a user typing on a computer keyboard. Output commands can either be printed for future use or be executed directly on a machining center.


---

This is the **last NIST release** of the interpreter that is now used by EMC2 and some commercial software. EMC2 is available at [http://linuxcnc.org](http://linuxcnc.org). The interpreter in EMC2 includes [a number of changes](http://www.linuxcnc.org/docview/html/gcode_main.html#r8).

If you are interested in **STEP-NC**, take a look at http://code.google.com/p/iso-14649-toolkit/
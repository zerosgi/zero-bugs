# zero-bugs

This is the source code for a C++ debugger. It is designed to debug
applications (not kernel) written in C/C++ under Linux.

At its core is an engine that the user can interact with in a console,
somewhat like GDB. It also has a Gtk UI.

BUILDING THE SOURCE:
	Use the build script in this directory, type ./build --help for help
	DO NOT run "./configure; make" by hand!

BUILD ENVIRONMENT:
The following are required:
	g++
	libelf
	boost
	boost-python (dev)
	flex
	bison
	python 2.x (dev)
	libgtkmm-2.4 (dev)
	libgtksourceview-1.0 or 2.0 (dev)
	libgtksourceviewmm 2.0 (dev)
	libgtkhtml-3.x (dev)


SOURCE CODE LAYOUT:
engine: the debugger engine code

typez: an implementation of the DebugSymbol interface, used by the stabs and
        dwarf plug-ins, implementation of the type-system

dharma: from the Sanskrit word "that which supports": miscellaneous support
        code, such as C++ wrappers around libc and system calls, code for
        detecting and loading shared objects at runtime (plug-in support).

dwarfz: C++ wrapper library around libdwarf

elfz:   C++ wrapper library around libelf

interp: builtin C/C++ interpretor for one-liner expressions

zero_python: a library that exposes the ZDK to the Python programming language.
		Built on top of Boost.Python

zdk:    some abstract classes that serve as bases for most of the
        interfaces in the Zero debugger project: Unknown, RefCounted,
        EnumCallback<>;
        also contains some helper code such as the RefPtr<> smart pointer, 
        designed to work with RefCounted objects, and a RefCountedImpl<>
        template implementation;
        some support code for atomically incrementing/decrementing reference
        counters;
        and some architecture/platform-specific definitions 

zdk/generic: miscellaneous C++ templates, with generic support for the visitor
        pattern, smart ptrs, etc.

stabz:  library for reading STAB debug info

symbolz:library to read symbol tables, etc

plugin: contains the GUI plug-in, the DWARF and STABS readers, etc.

zui:	bootstraps an EXPERIMENTAL GUI written in Python, I use it every once in a blue moon
		for prototyping purposes.

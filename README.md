
This is a reference implementation of the paper
["Interference Aware Geometric Modeling"](http://cs.nyu.edu/~dharmon/papers/iagm.pdf)
published in Transactions on Graphics (Proceedings of SIGGRAPH Asia 2011).

The implementation is in an included, standalone library called "iagm" and comes
with a basic [cubic B-spline](http://en.wikipedia.org/wiki/B-spline) editor that uses this library.


Building Instructions
=====================

There are two pieces to be built: the iagm library and the spline editor.

iagm library
------------

The only dependency for the iagm library is the Eigen math library, available for
free at [http://eigen.tuxfamily.org](http://eigen.tuxfamily.org).

To build on a Unix-based system, change to the iagm library directory

    cd iagm/

Copy the make include file to a file called make.inc:

    cp make.inc.copyme make.inc

This file contains user-specific settings. Open it and change the directory
where you have Eigen installed.

Also, set the extension for the dynamic library (dylib for Mac OS X systems,
so for Unix/Linux/etc.). You may also change usual build flags, such as CXX
for the compiler, CXXFLAGS for special flags, etc.

To build the first time, type

    make rebuild

This generates a dependency file, compiles the source, and creates a library
located in lib/.

If you make any changes, simply type

    make

to build again. If you add/remove files, type

    make rebuild

to regenerate dependency information.


spline editor
-------------

Besides the iagm library, the spline editor has 4 dependencies:

* Eigen [http://eigen.tuxfamily.org](http://eigen.tuxfamily.org)
* AntTweakBar [http://www.anttweakbar.com](http://www.anttweakbar.com)
* OpenGL [http://www.opengl.org](http://www.opengl.org)
* GLUT [http://www.glut.org](http://www.glut.org)

Build instructions are similar to the iagm library.

    cp make.inc.copyme make.inc

Open make.inc and change variables to point to your locations for the
necessary libraries and their header files. Building is initiated with

    make rebuild

This builds a dependency file and compiles the source into a binary
called spline2d.


Running the Spline Editor
=========================

To run the spline editor, type

    ./spline2d

at the command line. You may have to specify where the dynamic library
loader can find libiagm with something like

    export DYLD_LIBRARY_PATH=/path/to/iagm/lib

Check your operating system's documentation for the specifics.

A large window should appear, with options on one side provided by AntTweakBar.
spline2d is a modal editor with modes chosen by key presses. Here is a short
description of each key press and its mode:

*   q: New spline mode

    Press 'q' to initialize creating a new spline, then proceed to click to
    introduce control points of the spline. Pressing 'q' again starts a new
    spline with the next click.

*   w: Select mode

    This mode allows you to click and drag to select control vertices for editing.
    Selected vertices are highlighted in blue.

*   e: Add control point mode

    This mode allows you to add control point to the current spline.

*   a: Translate mode

    This model allows you to click and drag the left mouse button to move
    the selected control vertices.

*   d: Delete mode

    This key deletes the currently selected control points.


As the spline is edited, interference between the limit curves is automatically
removed by the iagm library. A few options can be set using AntTweakBar. The
response mode has three options: 0, 1, and 2

* 0: Everything responds to interference
* 1: Only selected vertices may be moved to remove interference
* 2: Only unselected vertices can move to remove interference.

Various other display options can be set using AntTweakBar.

Enjoy, and feel free to email me with questions or bug reports!

David Harmon
dharmon@cs.nyu.edu


Acknowledgements
================

Thanks to Daniele Panozzo for writing the spline editing software.

Thanks to Jun Saito for finding an early bug that prevented editing multiple
splines, and thanks to Libin Lu for finding a bug in the interference volume
gradient computation.


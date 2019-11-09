Ulendo Software (Smart 3D printing)
**********

``Ulendo`` can be used for any low cost embeded systems. We coded the method in C and shared the libraries, you can used them in any distrubutions or you ransfer them into any program language to use them in your own systems. 

The software contains two parts: 

- A software with the vabrition compensent method runs on an embeded system; 
- A modified Marlin firmware. 




::

  	@misc{
    		Author = {Smart and Sustainable Automation Research Lab, UM},
    		Title = {Ulendo Software},
    		Year = {2019},
    		Email = {luxiang@umich.edu (Xiang Lu)}
  	}



.. contents:: **Contents of this document**
   :depth: 2

Preparation 
============

- Hardware:
	 + Raspberry Pi 3 Model B+
	 + USB Printer Cable 
	 + Monitor, Mouse and Keyboard for the Raspberry
	 
 
Architectures
============

::

    ├── Marlin                              // Modified Marlin firmware 
    └── RPI                                 // Software runs in the Raspberry Pi
        ├── Readme.rst                      // help
        ├── Gcodes                          // Put all your Gcodes in this folder
	│   ├── Printing
	│   │      └── Groot.gcode          // Put the Gcode that you are going to print in this folder (delete others)
        │   └── Samples
	│          └── Cal_cube.gcode       // All sampling Gcodes
        ├── main.c                          // Main script, all algorithms are in this script
        ├── Makefile                        // Makefile 
        └── Libs                            // All libraries (.h .so, etc.)
            ├── Ulendo_libs.h               // Header file 
            ├── Ulendo_libs.so.0.0.1        // Shared object file    
            └── Ulendo_libs.so.0            // Soft link of Ulendo_libs.so.0.0.1

Configuration
============

- Marlin Firmware:
	 + Flash the modified Marlin firmware to the board on the printer.
	 + You can follow the instruction from http://marlinfw.org/docs/basics/install_arduino.html

- Ulendo Software:
	 + Download the “Raspbian Buster with desktop” from https://www.raspberrypi.org/downloads/raspbian/
	 + Flash the IMG file into the Raspberry Pi
	 + Download the Ulendo Software with Github, and you will find the software in your home folder:

.. code:: shell

	$ git clone https://github.com/luxiangnk/Ulendo_Release.git
	


Run the code
============

- Make sure the Raspberry Pi is connected with the internet.


- Make sure the printer's board appears as /dev/ttyACM0, you can check it with:

.. code:: shell

	$ ls -l /dev/ttyACM*


- Modify the Makefile based on your own system especially the path and version (python3.5 in our case) of Python as:

.. code:: shell

	-I/usr/include/python3.5m/ -L/usr/lib/ -lpython3.5m


- Then you can build the project and make sure there are no errors after typing:

.. code:: shell

	$ cd ~/Ulendo/Ulendo-Software-for-Taz6/RPI
	$ make


- Run the code by typing:

.. code:: shell

	$ ./main

- Push the button of your printer, and select "Print with Ulendo->Start".

- The code will check the license first and it will takes several seconds before printing.

- You can read the comments in the codes if you want to call the APIs from the shared object file.

- If you want to change the Gcode, you can put your Gcode in the "RPI/Gcodes/Printing/" and make sure there is only one Gcode file in the folder.

- If you want to change the printing parameters, you can push the printer's button and select "Print with Ulendo->Setting".


About LPFBS
============

**The limited-preview filtered B-spline (LPFBS) approach minimizes errors in tracking long-duration desired trajectories which may or may not be entirely known a priori.** 

You can read the MECH17 paper or contact me (Xiang Lu)
if you want to learn more about the LPFBS algorithm.

You can download the paper from `<https://www.researchgate.net/publication/320114918_A_limited-preview_filtered_B-spline_approach_to_tracking_control_-_With_application_to_vibration-induced_error_compensation_of_a_3D_printer>`_


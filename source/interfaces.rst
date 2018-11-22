Interfaces in Embedded Software Development
===========================================

This chapter takes a closer look at interfaces commonly needed for
embedded software development.
Not every interface is needed for every embedded system. May ask your
software developer if you are in doubt :-)


Boot Mode Selection
-------------------

A modern embedded CPU is able to boot in many different ways.
In a final product there is usually only a single boot mode used.
This fixed boot mode can be (depending on the CPU) set via external
resistors and / or internal fuses.


But during development this boot mode usually needs to be changed from
boot to boot.
Thus it is important that on a development-version of the embedded system the
boot mode is not fixed by external wiring or burned fuses.
The boot-mode signals need to be available via test points, defined pads on
resistors or - at best - as a pin-header.
During development the defaults on this signals will be overridden by external
switches or resistors to force a device into a specific boot mode.

If a boot mode is fixed (via fuses or external wiring) for a production version
of an embedded system this may make debugging of returns hard or impossible!

Special care has to be taken if the essential boot mode pins are used to
connect other hardware:
Developers and automated testing systems are usually not able to only
manipulate the level of a line during the sampling of the boot mode.
Thus an essential boot mode signal must be considered stuck at a specific level
most of the time during development.
And thus making it impossible to connect external hardware to this pins.

Serial Interface: UART
----------------------

Even if communication in the final product is done via network a
serial interface is needed to control and monitor the early stages of the
boot process.

This interface is usually used in 8-Bit mode with a speed of 115200 Baud.
There is no need for a specific level-shifter: usually the CPU's IO-voltage
(1.8 V or 3.3 V or even 5.0 V) are fine. The `Rx` and `Tx` lines are usually
sufficient. There is no need for handshake lines.

The serial interface needs to be available via test points, defined pads on
resistors or - at best - as a pin-header.

For some CPUs not all serial interfaces can be used during development.
For some i.MX - for example - only a few serial ports and pin-mux settings can
be used to run the vendor's RAM-calibration tool. Ask your software developer
for specific restrictions for your CPU.

GND for Measurement
-------------------

Even during software development there is a need to measure the level of
pins on a device.

.. todo::

   Add more details

USB for Serial Download via ROM-Code
------------------------------------

For some embedded CPUs it is possible to use the ROM-code to download a piece
of software (usually the bootloader) into the SRAM, setup peripherals of the
CPU and start the software.
This software can afterwards be used to write the bootloader to some
non-volatile memory.

On some CPUs the download can be done via USB. USB is convenient because it
features a relatively high bandwidth and does not need expensive external
components to be used.

While the ROM-Code is running the CPU's USB-port is in device mode.
The device is connected to the USB host on a test-server or the developers
computer.
If the CPU's USB-port is switched into host port during boot there will be two
USB hosts connected to the same bus.
Such situations usually lead to non-trivial errors on the bus can lead to an
inoperable bus.

Care has to be taken that this port can be kept in device mode e.g. by using
the OTG feature of an USB-port.
If the used port is needed as a host-port the test infrastructure needs some
way to control the mode of the port.

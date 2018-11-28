# MiniMon Driver for Bosch Motronic 7.8 M95320 EEPROM

Version: 1.1

## Background

MiniMon is a very small monitor program for any C16x/XC16x microcontroller based system.  MiniMon is loaded into RAM on the target system by the C16x bootstrap loader ("boot mode") and can then communicate with a Windows hosted program that provides functionality to interact with memory ROM/RAM/other from the target system.  Once downloaded to the Windows program, it is possible to save the memory to .bin files, compare, modify, disassemble code, etc.  In addition to these memory functions, MiniMon can be used to download and execute arbitrary code on the C16x.  Downloads and more info: http://www.perschl.at/minimon/

A monitor program like MiniMon is especially useful when working with automotive ECUs where there is little or no technical information available about the OEM firmware.  Accessing the firmware and other ROM areas is typically very difficult if not impossible, because there are typically protections to guard against "unauthorized" access on top of the slim technical reference information.  Running MiniMon give full access to the hardware.

The specific purpose of this driver is to provide access to the M95320 4KB EEPROM on the Bosch Motronic 7.8 DME (ECU).  There are some EEPROM drivers provided with MiniMon and the actual SPI interface is close enough that some of them may have worked with the M95320/Motronic 7.8, except that they use the wrong pin for the chip select signal.

The Bosch Motronic 7.8 uses P4.5 for the M95320 chip select and all of the MiniMon provided drivers use P2.8 for the chip select.  I suspect that other Bosch Motronic units may be similar and this driver may work even if the smaller M95160 (2KB) EEPROM is used.  However I don't know this with any certainty.

## Deployment

The binaries are provided in the repo, so there is no need to build the source code if you just want to use the driver as supplied.  All that is really required is to create a directory in the existing MiniMon Driver directory, e.g. <MiniMon_Home>/Driver/M95320, and copy m95320.hex into that directory.  It is conventional to copy at least the source file, m95320.a66, and possibly other files such as the .bin or listing files.

## Usage 

<details to be provided>

## Building from Source

The driver was built (and this repo is intended for use) by Keil uVision V5.25.3.0, Copyright (C) 2018 ARM Ltd and ARM Germany Gmbh.  Fortunately, since the driver is so small, it can be successfully built by the evaluation version. The uVision files are checked-in to the repo so it should be possible to open the project directly and build and/or modify the source and build.  The only external dependency is REG167.INC which is provided with uVision.  The project is configured to locate the driver at 0xE000 and generate the Intel hex file automatically.  The default uVision hex file will be named m95320.H86.  I have been manually copying that file to m95320.hex to follow the MiniMon convention, but either file should work fine.












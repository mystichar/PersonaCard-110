	      

Copyright (C) NATIONAL SEMICONDUCTOR, 1995
Release DNLDCMD_1.1
All Rights Reserved.

PersonaCard Token Support Diskette
========================================================
The contents of this diskette contain programs and data 
that are copyrighted by National Semiconductor, 1995, 
All Rights Reserved.


NOTICE!

DO NOT INSTALL THE PROGRAMS ON THIS DISKETTE UNLESS 
REQUESTED TO BY A TECHNICAL SUPPORT REPRESENTATIVE.  
THESE PROGRAMS ARE DESIGNED TO BE USED FOR THE 
DIAGNOSIS OF PROBLEMS BY THE TECHNICAL SUPPORT 
REPRESENTATIVE.                                  





Table of Contents
=================

1. Purpose of this Support Diskette

2. Platform Compatibility Information

3. PersonaCard PCMCIA Client Driver Detailed Information

4. Installing the PCDIAG utility

5. Other information


1. Purpose of this Support Diskette
===================================

This diskette is intended for diagnostic and information uses ONLY.
The platform compatibility information and PersonaCard PCMCIA
Client Driver information can be of value to users to make
the PersonaCard accessible through the user's PCMCIA adapter.

The installation on this diskette will install a diagnostic utility
on a PC that is to be used only in conjunction with the Technical
Support staff.  The information in this file is useful for properly 
setting up the PCMCIA (PCCARD) controller for working with 
the PersonaCard 100 and 110.



2. Platform Compatibility Information
=====================================

The PersonaCard has been extensively tested with a large number of
PCMCIA card drives and PCMCIA-enable notebook computers.  The 
following is the current list of tested platforms.

Recommended Platforms
=====================

SCM Card reader (all models)

HP OmniBook 425

TOSHIBA (models using Toshiba Card Manager 3) 

IBM ThinkPad (single and dual PCMCIA card models)

Altima Virage
	
ATT Safari 3151
	
COMPAQ Aero 4/33

COMPAQ Elite LTE 4/40cx

COMPAQ Contura 400

Dell Lattitude XP Series

Gateway 2000 ColorBook CB486SX33

AST Ascentia 900

NCR 3150

NEC UltraLite Versa 486/25

Zenith Z-Star

Zenith Z-Lite models

REFER ALSO TO  SETUPS FOR SPECIFIC PLATFORMS FOR COMPATIBLE
SOCKET AND CARD SERVICES.


Non-recommended Platforms
=========================

DataBook-based Controllers/Drivers

PersonaCard has not been found to work with any Notebooks and Card drives 
that use the DataBook PCMCIA controller and drivers.  This includes but is 
not limited to:  
	
	PREMAX CardDrive
	Altima Traveller (note: the Virage model does not use DataBook)
	Sharp  8660

Data IO CardPro (TM) 2

Although the Data IO CardPro 2 can be made to work with the PersonaCard, it 
has problems working with two cards where one of the cards is not a 
PersonaCard. Also, insertion of PersonaCards can cause the PC to halt all
of its operations until the CardPro 2 becomes READY (this can take from
10 to 60 seconds or more).



3. PersonaCard PCMCIA Client Driver Detailed Information
========================================================

Command line options for PersonaCard driver
===========================================
The PersonaCard driver requires the following default entry in config.sys:

	DEVICE=[path]\pcdriver.exe [/WINSIZE XXX] [/POWERON] [/ONEWIN] [/EXCL]

[path] stands for any path where the PersonaCard driver is installed. 
For example, [path]=C:\PERSONA.

/WINDSIZE       This option specifies a memory window size.
		The default memory window is 4096 bytes.
		The window size must be specified in bytes using 
		decimal numbers only.

/POWERON        This option keeps the power on across close calls,
		while a card is inserted into a socket. 
		By default, power is turned off to a PersonaCard
		on a close call.

/ONEWIN         This option forces the PersonaCard driver to keep only 
		one memory window open all the time. 
		By default, one memory window is allocated for each
		socket to access the card.

/EXCL           This option allows the card to be exclusively owned by 
		the PersonaCard driver. By default, the card is not 
		exclusively owned by the PersonaCard driver.



Special Handling for using Flash or SRAM PCMCIA Memory Cards
========================================================

If any MTD Driver, Flash Driver or SRAM Driver are loaded in config.sys 
then you should manually add the /options for PCDRIVER as follows :
       	DEVICE=PCDRIVER.EXE /POWERON /EXCL
In addition, PCDRIVER should be loaded before any MTD Driver, Flash 
Driver and SRAM Driver in config.sys, preferably to right after the card 
services memory manager.  
After making these changes, make sure to insert PersonaCard into card 
reader before rebooting the computer.  This slot will be exclusively owned 
by the PersonaCard driver.  However, Flash or SRAM PCMCIA memory 
cards can be used in the second slot.


Special Setups for Specific Platforms
=====================================

The following instructions have been found to correct for the differences
between different platforms.  In many cases, the installation performed
by the application which is enabled for PersonaCard usage will make all
necessary adjustments to the CONFIG.SYS file.  However, for those times
when the PersonaCard is still not accessible after running the installation
these instructions can be very important.  Please try the instructions
appropriate to your platform before calling technical support.


SCM Card reader

   Card/Socket Services
     
	SystemSoft Socket Service 2.1, Vadem Version 1.01 (2188-04)
	SystemSoft Card Service 2.1, Version 2.06 (2036-09)
	SystemSoft Card Service Allocation Utility Version 2.06 (2137-11)

   Optional CONFIG.SYS Setup

	In order to insure proper operation when multiple PersonaCards 
	are inserted, it is suggested that the /POWERON parameter be
	added to the PCDRIVER.EXE line in the CONFIG.SYS file.  This will
	cause the power to be kept on when a PersonaCard is in the socket.

	Example of line in CONFIG.SYS file.

	DEVICE=[path]PCDRIVER.EXE  /POWERON


HP OmniBook (newest models ONLY)
	
   Card/Socket Services

	SystemSoft Socket Services 2.1 OmniBook Version 1.0
	SystemSoft Card Service 2.1 Version 2.06 (2256-10)
	System Card Service Allocation Utility Version 2.06 (2137-11)

   Required CONFIG.SYS Setup

	Because of unique aspects of the OmniBook platforms, the /WINSIZE
	and /POWERON options should be used with the PCDRIVER.EXE line
	in the CONFIG.SYS file.  These options will force the memory window 
	size to be fixed to 16384 bytes and the PCMCIA socket power to be 
	kept on as much as possible.

	Example of line in CONFIG.SYS file:

	DEVICE=[path]PCDRIVER.EXE  /WINSIZE  16384  /POWERON

TOSHIBA

   Card/Socket Services

	PCMCIA 2.1 compliant Card service and Socket service
	Toshiba Card Manager Version 3.0

   Required CONFIG.SYS Setup

	Before the PersonaCard driver is loaded, the PCM utility must 
	configure the PersonaCard. After the card is configured, add the 
	PCDRIVER.EXE to CONFIG.SYS.

IBM ThinkPad

   Card/Socket Services

	Phoenix PCMCIA Compliant Socket Services for Intel 82365SL.
	Version 1.0
	PCMCIA Card Services  1993 Phoenix Technologies Ltd, Version 1.0
	Card Service Release 2.01
	Phoenix Super Client Driver, Version 1.0

	or

	SystemSoft Socket Service 2.1 82365SL Version 2.02 (2059-03)
	SystemSoft Card Services 2.1 Version 2.06 (2036-09)
	SystemSoft Card Service Allocation Utility Version 2.06 (2137-11).

Altima Virage

   Card/Socket Services
	
	Phoenix CardMan 3.0 Card and Socket Services

ATT Safari 3151

   Card/Socket Services
	
	CARDSOFT 3.1 Card and Socket Services

COMPAQ Aero 4/33

   Card/Socket Services

	COMPAQ/CARDSOFT Card and Socket Services

COMPAQ Elite LTE 4/40cx

   Card/Socket Services

	COMPAQ/CARDSOFT Card and Socket Services

COMPAQ Contura 400

   Card/Socket Services

	COMPAQ/CARDSOFT Card and Socket Services

Dell Lattitude XP Series

   Card/Socket Services

	CARDSOFT 3.1 Card and Socket Services

Gateway 2000 ColorBook CB486SX33

   Card/Socket Services

	CARDSOFT 3.1 Card and Socket Services 

AST Ascentia 900

   Card/Socket Services

	CARDSOFT 3.1 Card and Socket Services 

NCR 3150

   Card/Socket Services

	Phoenix Card Manager V2.22

NEC UltraLite Versa 486/25

   Card/Socket Services

	CARDSOFT 3.1 Card and Socket Services 
	[When using a LAN card with the PersonaCard,
	 the PersonaCard must be inserted ONLY after
	 the LAN Drivers are enabled.]

Zenith Z-Star

   Card/Socket Services

	CARDWARE SSL 2.10 REL 1.04


Zenith Z-Lite models

   Card/Socket Services

	CARDWARE SSL 2.10 REL 1.04


Data IO CardPro (TM) 2

Although the Data IO CardPro 2 is not a recommended platform to work with the
PersonaCard, the following approach can be used to make the CardPro 2 work 
with the PersonaCard.

   Card/Socket Services

	CP2SS CardPro 2 Universal PC Card Driver Socket Service Version 1.00
	SystemSoft Card Service 2.01 Version 4.15
	CPCM CardPro Universal PC Card Driver Manager, Version 1.00

   Optional CONFIG.SYS Setup

	The CardPro 2 may work without any changes to the CONFIG.SYS file;
	however, if there are problems accessing the card, the /ONEWIN
	option can be used on the PCDRIVER.EXE line.  This will insure that
	only one memory window can be active at a time. However, when the 
	PersonaCard is used with any other PCMCIA card, access to the 
	other cards may fail.

	Example of PCDRIVER.EXE line in the CONFIG.SYS file:

	DEVICE=[path]PCDRIVER.EXE /ONEWIN



4. Installing the PCDIAG utility

When instructed by a Technical Support, follow these instructions:

	1. Back up the CONFIG.SYS file in the root directory.
	2. Place this diskette in an appropriate diskette drive.  
	3. Run Microsoft Windows
	4. Select File Run
	5. Enter A:\SETUP.EXE or B:\SETUP.EXE (depending on your 
		configuration and where the diskette was placed) 
		into the text box.  
	6. Press OK.  
	7. The installation will run, asking only a minimum 
		number of questions.

The Installation program will automatically copy PCDRIVER.EXE and 
CAAPI.DLL to the hard disk if they are needed or they are newer versions
than those already on the hard disk.  If CAAPI.DLL is copied, it will
most probably be found in the SYSTEM directory below the WINDOWS directory. 



5. Other information

Additional information will be included in this section as it becomes
available.

# Romulator
Final Year Capstone
Introduction 
This document entails the hardware requirements of a Romulator device designed for our capstone project. Intended audience are EE majors and hobbyists in memory embedded systems who need to design their own board or the electronic parts that contain a ROM.
Scope
Our emulator has the ability to simulate specified components in the target system, and the simulated behavior is very similar to the behavior of the real system and used as a ROM replacement for the target system.
Overview
This document covers the overall system interface, product description and specific hardware and software functionality required for a full integrated romulator.
Product Perspective
Dual port the RAM by making the host write files into the RAM using the Arduino controller, and the target should read and write from the RAM. 
System Interface
The romulator is connected to the arduino through a USB interface, and the target system through a 40 pin DIP socket. Below is a figure describing different levels of the romulator connection.
User Interface 
We need some method of controlling the read and write instruction from both the arduino and target system. Our romulator uses a command-line program inorder for the end user to operate the romulation process. 
Operating system requirements
Minimum system requirement for the host PC connected to the arduino is Java 8.0 and  a Pentium 2 266 MHz processor. On Windows 64-bit operating systems, in 32- or 64-bit mode, the Java runtime requires a minimum of 128MB of memory. 
Software Interface
Our main user interface would be through the command line, but we structure it as the following. The menu shows options such as readData from the target files such as S-record or Intel Hex, writeData to the RAM and emulate the target system ROM. Where each option has sub-commands to further run your specific needs, each sub-command is discussed in the software function. 
Communication Interface. 
Our romulator uses a USB to communicate with the arduino and depending on the type of ROM used,  you can choose a 24, 28, and 32 cable pin. 
Memory Constraints. 
We are limited by our arduino SRAM with a 8 KB and EEPROM of 4 KB, data storage from the target system can be saved in a file on the PC. Otherwise, the 17 address inputs select one of the 131,072 x 8-bit words in the RAM.
Theory of operation.
There is a continuous need to change between read, write and emulate processes inside the romulator RAM and other connected interfaces.

Arduino 
Has complete control of both data and addresses both to and from the host and the romulators RAM. 
   It's also connected to the PC via a USB and the romulator via the 8 data pins and 17 address pins. 




The RAM 
       It is the center point of the target and the host system via the arduino microcontroller and 32 pin DIP socket connected to the romulator interface. Contains 1MB of data storage, 8 data pins and 17 address pins. 
DIP Socket 
It connects the interface between the romulator and the guest system. Depending on the ROM configuration we may use other types of Pins. The current pin configuration for our romulator is 32 pins. When the system is in emulation mode the RAM uses the socket connection to act as the guest systems RAM. 

Address Buffers 
Controls the address bus to and from the RAM of the romulator, it has a pair of three buffers since each buffer can handle 17 bus addresses. 

Data Bus 
This buffers control data bus to and from the RAM of the romulator. It had a pair of buffers: one gets data to the ROM of the romulator and the other to the host and the guest system.

RAM access Time
Our system access time is 3ns delay from the guest system to DIP 32 pin socket, 0.9ns delay from the romulator interface with the guest to the buffer, 20ns for the buffer switch and hold times, 0.6ns delay from the address buffer to the RAM, 0.9ns from the RAM to the data buffer, 20ns delay data buffer switch times, 0.6ns from data buffer to the emulators interface with the guest system and 55ns-RAM access time. 
Power Usage


The voltage to the board is mainly from the microcontroller (ATmega2560) with an Operating Voltage of 7V with the help of the voltage regulator reduced it to 5V, since our romulator RAM operates from a wide range of  2.4V to 5.5V supply voltages. Current per I/O pin is 20mA, and clock speed of 16Mhz. There are 16 analog input pins, 4 UARTs (hardware serial ports), 16Mhz crystal oscillator, USB connection, ICSP header, power jack, and reset button.


Operational temperature range.
The Operating Ambient Temperature Range for our system is a minimum of 25°C to a maximum of 54°C derived mainly from the RAM of the system because of its low temperature range comparison with the other peripherals within the device.
Physical dimensions.
The total approximate surface area for 8 buffers, a RAM and 32 pin DIP socket would  be around (50mmx50mm) when the RAM (8mmx20mm ) plus buffer are (12.65mmx12.95mm) plus DIP socket are sound (12mmx4mm)
Software Functions.
The command line function has the following software helper instructions to use the romulator:
readData commands such as:
enableReadRAM - allows read access to the emulator’s RAM.
disableWriteRAM - disables write access to the emulator’s RAM.
disableAccessTarget - which disable access for the target system,
readDataRAM - copies data to an intermediary file on PC. 
writeData command has commands such as 
validateData - so that right data is sent to the emulator,
disableReadRAM - disables read access to the emulator’s RAM.
enableWriteRAM - enables write access to the emulator’s RAM.
disableAccessTarget - denies romulator access to the target system, 
clearRAM - erases data on emulator RAM and last but not least 
writeToRAM - writes the data to the RAM.
User Characteristics
Our main users are students of electrical engineering who want to use an external RAM to troubleshoot their programs before they can integrate it in their systems. 
Constraints. 
The design and build of the hardware in the simulator will take us from anywhere between 14 weeks to 10 weeks. Testing and making it available for use would take about another 14 weeks. Making the whole build to two quarters, also the team members will be building their codes and testing remotely.
Specific Requirements
The romulator must have the right pins that are used for the specific RAM pinout the target system uses, although there are different RAM that have different pin requirements, our romulator uses a 32 pin DIP socket. Hence, the cabling must match. 
Should read S-record or Intel Hex file, decode and put the data into the RAM.
 Command line interface should be simple enough, and have a menu that can be navigated with ease. 

Product Functions. 
The host system should be able to write data to the RAM.
Our Romulator should take data and extract each byte of data.
Should write data to our emulators.
Verify incoming data.
Stop if an exit command is issued. 

Performance requirements.
The minimum target access time for the ROM access is approximately  101.6ns. Thus for the target system to be able to match the romulator RAM access time it should be within the range of the RAM access time.
Design Constraints. 
Our romulator will be using the following parts in its building block:
Arduino Mega 2560
8 Buffers(7x 74LS541 and 1x 74LS245)
RAM(Random Access Memory) [BS62LV1027]
DIP (36 pins) and a cable to Target 
Software Reliability. 
Our romulator should continuously run unless there is a user interrupt through the command line or through the designated power switches. 
You should be able to rewrite to and from the ROM emulator as many times as needed.
Testing programs and debugging should be a matter of uploading a corrected program to the emulator.




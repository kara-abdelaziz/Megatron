# Megatron
Megatron is the little sister of Gigatron, it is an attempt to modify/minimise some Hardware/Software aspects of Gigatron.

# Description
Megatron is based upon Gigatron which is a project consisting of the construction of a computer/console upon a bunch of elementary TTL 74 series logic chips, without using any advanced complex chip, like processors, microcontrollers, alu, graphic/sound controllers...etc. The project really consists of two parts, Hardware and Software. Megatron is an attempt to do some modifications and minimisations of the chip number and the display device (from where the name Megatron). Megatron is intended to be used with small handheld tft screens, thus adding higher resolution and more color depth instead of VGA in Gigatron. Megatron also adds special input/output unit to manage more input/output devices, which allows to add a native keyboard to Megatron. The software is meant to be compatible with Gigatron despite some mandatory code modification to manage the input/output unit. More details can be found below.

# Simulation
First of all was the simulation, everything was done primary on Logisim to fully understand how Gigatron works, and to test if it is possible to implement the different modifications. 3 different simulations were done on Logisim that can be downloaded below or on Github:

* first is Gigatron.circ used primarely for acadimic and teaching purposes, it is a simplified logic version of Gigatron, in whitch the 74 series were not used, but a simplified logical equivalents were utilized instead. This version is stuffed with debugging and monitoring mechanisms.
* second is GigatronTTL.circ is a more accurate simulation were the same 74 series logic chips were used, nevertheless some parts in Gigatron can not be simulated under Logisim due to their analogic nature, like resistrors/diods grid used in the Control Unit (UC), they were replaced by some logic ccircuits equivalent. Also, in some situations Gigatron mixed up the bits order in some registers, for clarity the simulation holds the natural order of bits.
* third MegatronTTL.circ, an accurate simulation of Megatron using 74 series chips.

For the simulation to work properly, GigatronTTL.circ and MegatronTTL.circ needs in the same directory 74xx Library.circ file to work. Also MegatronTTL.circ needs that the 3 ROMs (27c512) under CU circuit must be loaded consecutively from up to down with CU-datapath.ROM, CU-registers.ROM, CU-ALU.ROM in the case where that was not done automatically.

Two proof-of-concept programs can be executed on both Gigatron and Megatron, Fibonacci and Factorial programs. To execute them, the binary machine code of one of them must be loaded in the ROM of the machine, the binary machine code for Fibonacci is saved in Fibonnaci.ROM file and Factorial is saved in Factorial.ROM file. Two other files, Fibonnaci.txt and Factorial.txt are used to contain the assembly language for the two programs, mainly for explaining them.

Both programs have input values for execution, the input value (example 3) has to be put inside the register BUS-IN in Gigatron, and KEYBOARD-IN in Megatron, IOC register also in Megatron must contain 0x11 (or 00010001b) to choose the keyboard to be the primary input device. The result of the programs is shown in output register at the end of the execution. Step-by-step execution can also be done by using the mode "manual" of the clock, all the componants informations can be monitored by the associated 7 display segments, plus the contents of the RAM by show it's appropriate window.

# Modifications
The modifications done upon Megatron in comparison to Gigatron are mainly intended to reduce the number of components for the ease of use and implementation, and secondly to enhance some hardware aspects, like to bring more flexibility  for adding and managing more devices.

The list of all the modifications done to Megatron is as below :

* Removing the VGA and replacing it by small more intelligent handheld screens, with higher resolution and higher color depth. In fact the VGA imposes some heavy constraints to the architecture, like most of the time spent by Gigatron is for rendering VGA signals, and the constraint to use 6.25 MHz clock, which (i guess) leaded to apply a non desirable pipeline, and some additional hardware non trivial manipulation to comply timing constraints.
* Removing the pipeline.
* Doubling the RAM capacity from 32 KB to 64 KB.
* Using 74181 ALU to have faster arithmetic/logic calculation and to reduce the number of chips.
* Replacing the CU (Control Unit) complex logic by 3 ROMs (used like look-up tables), which leads to a smaller simpler circuit and more flexible programmable Control Unit.
* Adding a proper Input/Output Unit implementing a real device manager allowing the addition of more input and output devices.
* Adding a native keyboard to Megatron and potentially other devices.

# Software
Some additions are made to the Instructions Set, especially the instructions responsible for the Input/Output Unit, more details about those instructions and how to use them can be found in the PDF Instructions Set.

The code should be compatible with the two machines Megatron and Gigatron, except for the input/output instructions, they should be removed for Gigatron and added for Magatron. The NOP instruction after every jump instruction is no more mandatory in Megatron, cause the pipeline has been removed.

It is not the case for now, but in the future the use of an assembler and a different software stack would be envisageable.

# Links
- My personal website [el-kalam.com](https://www.el-kalam.com)
- [Megatron](https://hackaday.io/project/168635-megatron) on HackADay
- Gigatron project [website](https://gigatron.io/)

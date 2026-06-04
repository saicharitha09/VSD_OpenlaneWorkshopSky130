Digital VLSI SoC Design and Planning

 👩‍💻 Author

**SAICHARITHA**

This repository documents my implementation and learning journey through
the Digital VLSI SoC Design and Planning workshop. The project covers
the complete RTL-to-GDSII ASIC design flow using open-source EDA tools
and the Sky130 Process Design Kit (PDK).

------------------------------------------------------------------------

📌 Project Overview

The project demonstrates the complete ASIC design cycle, including:

-   RTL Design and Synthesis
-   Floorplanning
-   Placement
-   Clock Tree Synthesis (CTS)
-   Routing
-   Static Timing Analysis (STA)
-   Physical Verification (DRC & LVS)
-   Standard Cell Design using Magic Layout
-   OpenLANE RTL-to-GDSII Flow
-   Sky130 Open-Source PDK


------------------------------------------------------------------------

 🛠️ Tools Used

  Tool         Purpose
  ------------ ---------------------
  OpenLANE     RTL-to-GDSII Flow
  Yosys        Logic Synthesis
  OpenROAD     Physical Design
  OpenSTA      Timing Analysis
  Magic        Layout Design & DRC
  Netgen       LVS Verification
  Ngspice      Circuit Simulation
  Sky130 PDK   Process Technology

------------------------------------------------------------------------

 🎯 Learning Outcomes

-   ASIC Design Flow
-   RTL-to-GDSII Implementation
-   Physical Design Concepts
-   Standard Cell Characterization
-   Timing Closure Techniques
-   DRC and LVS Verification
-   Open-Source VLSI Design Tools

------------------------------------------------------------------------

## 🚀 Key Highlights

 Complete RTL-to-GDSII Flow Implementation

 OpenLANE-Based Physical Design

 Custom Standard Cell Design

 Timing Analysis using OpenSTA

 Layout Verification using Magic

 DRC Rule Debugging and Fixes

------------------------------------------------------------------------

📜 Acknowledgements

This project was completed as part of the Digital VLSI SoC Design and
Planning workshop conducted by VSD in collaboration with NASSCOM. The
repository reflects my implementation, observations, simulations, and
documentation throughout the learning process.

Section 1 - Inception of open-source EDA, OpenLANE and Sky130 PDK 
## Section 1 - Inception of open-source EDA, OpenLANE and Sky130 PDK (14/03/2024 - 15/03/2024)

### Theory

<details>
  <summary>
Expand or Collapse
  </summary>

#### Package

* In any embedded board we have seen, the part of the board we consider as the chip is only the ***PACKAGE*** of the chip which is nothing but a protective layer or packet bound over the actual chip and the actual manufatured chip is usually present at the center of a package wherein, the connections from package is fed to the chip by ***WIRE BOUND*** method which is none other than basic wired connection.

313255858-d19f6d0f-16f8-4e79-aa5a-f2a34b9fb203.png
synthesis.png

#### Chip

* Now, taking a look inside the chip, all the signals from the external world to the chip and vice versa is passed through ***PADS***. The area bound by the pads is ***CORE*** where all the digital logic of the chip is placed. Both the core and pads make up the ***DIE*** which is the basic manufacturing unit in regards to semiconductor chips.

floorplan1.png

* ***FOUNDRY*** is the place where the semiconductor chips are manufactured and ***FOUNDRY IP's*** are Intellectual Properties based on a specific foundry and these IP's require a specific level of intelligence to be produced whereas, repeatable digital logic blocks are called ***MACROS***.

floorplan2.png

#### ISA (Intruction Set Architecture)

* A C program which has to be run on a specific hardware layout which is the interior of a chip in your laptop, there is certain flow to be followed.
* Initially, this particular C program is compiled in it's assembly language program which is nothing but ***RISC-V ISA (Reduced Instruction Set Compting - V Intruction Set Architecture)***.
* Following this, the assembly language program is then converted to machine language program which is the binary language logic 0 and 1 which is understood by the hardware of the computer.
* Directly after this, we've to implement this RISC-V specification using some ***RTL (a Hardware Description Language)***. Finally, from the RTL to ***Layout*** it is a standard PnR or RTL to GDSII flow.

flopratio.png

* For an application software to be run on a hardware there are several processes taking place. To begin with, the apps enters into a block called system software and it converts the application program to binary language. There are various layers in system software in which the major layers or components are OS (Operating System), Compiler and Assembler.
* At first the OS outputs are small function in C, C++, VB or Java language which are taken by the respective compiler and converted into instructions and the syntax of these instructions varies with the hardware architecture on which the system is implemented.
* Then, the job of the assembler is to take these instructions and convert it into it's binary format which is basically called as a machine language program. Finally, this binary language is fed to the hardware and it understands the specific functions it has to perform based on the binary code it receives.

flopratio2.png

* For example, if we take a stopwatch app on RISC-V core, then the output of the OS could be a small C function which enters into the compiler and we get output RISC-V instructions following this, the output of the assembler will be the binary code which enters into your chip layout.

floorplan3.png

* For the above stopwatch the following are the input and output of the compiler and assembler.

floorplan4.png

* The output of the compiler are instructions and the output of the assembler is the binary pattern. Now, we need some RTL (a Hardware Description Language) which understands and implements the particular instructions. Then, this RTL is synthesised into a netlist in form of gates which is fabricated into the chip through a physical design implementation.

areafloor1.png

* There are mainly 3 different parts in this course. They are:
1. RISC-V ISA
2. RTL and synthesis of RISC-V based CPU core - picorv32
3. Physical design implementation of picorv32
4. ![Area Floorplan](https://raw.githubusercontent.com/saicharitha09/VSD_OpenlaneWorkshopSky130/ac264cf004e5fbbfa1a9dc25ef686f86d3a8e23d/areafloor1.png)


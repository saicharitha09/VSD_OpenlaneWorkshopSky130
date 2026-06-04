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
![](https://raw.githubusercontent.com/saicharitha09/VSD_OpenlaneWorkshopSky130/009431be56f58194dbe99f9fe78e011340dcf9c9/openlane.png)
![](https://raw.githubusercontent.com/saicharitha09/VSD_OpenlaneWorkshopSky130/ac264cf004e5fbbfa1a9dc25ef686f86d3a8e23d/areafloor1.png313255858-d19f6d0f-16f8-4e79-aa5a-f2a34b9fb203.png)
![synthesis.png](https://github.com/saicharitha09/VSD_OpenlaneWorkshopSky130/blob/main/synthesis.png?raw=true)

#### Chip

* Now, taking a look inside the chip, all the signals from the external world to the chip and vice versa is passed through ***PADS***. The area bound by the pads is ***CORE*** where all the digital logic of the chip is placed. Both the core and pads make up the ***DIE*** which is the basic manufacturing unit in regards to semiconductor chips.

![floorplan1.png](https://github.com/saicharitha09/VSD_OpenlaneWorkshopSky130/blob/main/floorplan1.png?raw=true)

* ***FOUNDRY*** is the place where the semiconductor chips are manufactured and ***FOUNDRY IP's*** are Intellectual Properties based on a specific foundry and these IP's require a specific level of intelligence to be produced whereas, repeatable digital logic blocks are called ***MACROS***.

![floorplan2.png](https://github.com/saicharitha09/VSD_OpenlaneWorkshopSky130/blob/main/floorplan2.png?raw=true)

#### ISA (Intruction Set Architecture)

* A C program which has to be run on a specific hardware layout which is the interior of a chip in your laptop, there is certain flow to be followed.
* Initially, this particular C program is compiled in it's assembly language program which is nothing but ***RISC-V ISA (Reduced Instruction Set Compting - V Intruction Set Architecture)***.
* Following this, the assembly language program is then converted to machine language program which is the binary language logic 0 and 1 which is understood by the hardware of the computer.
* Directly after this, we've to implement this RISC-V specification using some ***RTL (a Hardware Description Language)***. Finally, from the RTL to ***Layout*** it is a standard PnR or RTL to GDSII flow.

![flopratio.png](https://github.com/saicharitha09/VSD_OpenlaneWorkshopSky130/blob/main/flopratio.png?raw=true)

* For an application software to be run on a hardware there are several processes taking place. To begin with, the apps enters into a block called system software and it converts the application program to binary language. There are various layers in system software in which the major layers or components are OS (Operating System), Compiler and Assembler.
* At first the OS outputs are small function in C, C++, VB or Java language which are taken by the respective compiler and converted into instructions and the syntax of these instructions varies with the hardware architecture on which the system is implemented.
* Then, the job of the assembler is to take these instructions and convert it into it's binary format which is basically called as a machine language program. Finally, this binary language is fed to the hardware and it understands the specific functions it has to perform based on the binary code it receives.

![flopratio2.png](https://github.com/saicharitha09/VSD_OpenlaneWorkshopSky130/blob/main/flopratio2.png?raw=true)

* For example, if we take a stopwatch app on RISC-V core, then the output of the OS could be a small C function which enters into the compiler and we get output RISC-V instructions following this, the output of the assembler will be the binary code which enters into your chip layout.

![floorplan3.png](https://github.com/saicharitha09/VSD_OpenlaneWorkshopSky130/blob/main/floorplan3.png?raw=true)

* For the above stopwatch the following are the input and output of the compiler and assembler.

![floorplan4.png](https://github.com/saicharitha09/VSD_OpenlaneWorkshopSky130/blob/main/floorplan4.png?raw=true)

* The output of the compiler are instructions and the output of the assembler is the binary pattern. Now, we need some RTL (a Hardware Description Language) which understands and implements the particular instructions. Then, this RTL is synthesised into a netlist in form of gates which is fabricated into the chip through a physical design implementation.

![areafloor1.png](https://github.com/saicharitha09/VSD_OpenlaneWorkshopSky130/blob/main/areafloor1.png?raw=true)




3. Load generated floorplan def in magic tool and explore the floorplan.

Commands to load floorplan def in magic in another terminal

# Change directory to path containing generated floorplan def
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/17-03_12-06/results/floorplan/

# Command to load the floorplan def in magic tool
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def &

![](https://raw.githubusercontent.com/saicharitha09/VSD_OpenlaneWorkshopSky130/4d5bab9c54d4dc79b958a54ad4e7ba36e54a1a2e/MAGIC.png)
Equidistant placement of ports
![](https://raw.githubusercontent.com/saicharitha09/VSD_OpenlaneWorkshopSky130/4d5bab9c54d4dc79b958a54ad4e7ba36e54a1a2e/MAGIC2.png)
Port layer as set through config.tcl
![](https://raw.githubusercontent.com/saicharitha09/VSD_OpenlaneWorkshopSky130/4d5bab9c54d4dc79b958a54ad4e7ba36e54a1a2e/MAGIC3.png)

Decap Cells and Tap Cells
![](https://raw.githubusercontent.com/saicharitha09/VSD_OpenlaneWorkshopSky130/9ac3990269cd812ff69852f1f4308fe688865df2/DECAP.png)
Diogonally equidistant Tap cells
![](https://raw.githubusercontent.com/saicharitha09/VSD_OpenlaneWorkshopSky130/9ac3990269cd812ff69852f1f4308fe688865df2/DECAP2.png)
Unplaced standard cells at the origin
![](https://raw.githubusercontent.com/saicharitha09/VSD_OpenlaneWorkshopSky130/9ac3990269cd812ff69852f1f4308fe688865df2/UNPLACED.png)

4. Run 'picorv32a' design congestion aware placement using OpenLANE flow and generate necessary outputs.

Command to run placement

# Congestion aware placement by default
run_placement
![](https://raw.githubusercontent.com/saicharitha09/VSD_OpenlaneWorkshopSky130/9ac3990269cd812ff69852f1f4308fe688865df2/UNPLACED2.png)
![](https://raw.githubusercontent.com/saicharitha09/VSD_OpenlaneWorkshopSky130/9ac3990269cd812ff69852f1f4308fe688865df2/UNPLACED3.png)

5. Load generated placement def in magic tool and explore the placement.

Commands to load placement def in magic in another terminal

# Change directory to path containing generated placement def
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/17-03_12-06/results/placement/

# Command to load the placement def in magic tool
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def &

Screenshots of floorplan def in magic
![](https://raw.githubusercontent.com/saicharitha09/VSD_OpenlaneWorkshopSky130/b1a9c12f87557e257500241bda9dab83775b0360/MAGICTOOL.png)
Standard cells legally placed
![](https://raw.githubusercontent.com/saicharitha09/VSD_OpenlaneWorkshopSky130/b1a9c12f87557e257500241bda9dab83775b0360/STANDARD.png)
Commands to exit from current run

# Exit from OpenLANE flow
exit

# Exit from OpenLANE flow docker sub-system
exit

Section 3 - Design library cell using Magic Layout and ngspice characterization (18/03/2024 - 21/03/2024)
Theory
Implementation

    Section 3 tasks:-

    Clone custom inverter standard cell design from github repository: Standard cell design and characterization using OpenLANE flow.
    Load the custom inverter layout in magic and explore.
    Spice extraction of inverter in magic.
    Editing the spice model file for analysis through simulation.
    Post-layout ngspice simulations.
    Find problem in the DRC section of the old magic tech file for the skywater process and fix them.

    Section 3 - Tasks 1 to 5 files, reports and logs can be found in the following folder:

Section 3 - Tasks 1 to 5 (vsdstdcelldesign)

    Section 3 - Task 6 files, reports and logs can be found in the following folder:

Section 3 - Task 6 (drc_tests)
1. Clone custom inverter standard cell design from github repository

# Change directory to openlane
cd Desktop/work/tools/openlane_working_dir/openlane

# Clone the repository with custom inverter design
git clone https://github.com/nickson-jose/vsdstdcelldesign

# Change into repository directory
cd vsdstdcelldesign

# Copy magic tech file to the repo directory for easy access
cp /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech .

# Check contents whether everything is present
ls

# Command to open custom inverter layout in magic
magic -T sky130A.tech sky130_inv.mag &

Screenshot of commands run
![](https://raw.githubusercontent.com/saicharitha09/VSD_OpenlaneWorkshopSky130/b1a9c12f87557e257500241bda9dab83775b0360/COMMAND.png)
2. Load the custom inverter layout in magic and explore.

Screenshot of custom inverter layout in magic
![](https://raw.githubusercontent.com/saicharitha09/VSD_OpenlaneWorkshopSky130/b1a9c12f87557e257500241bda9dab83775b0360/LOAD.png)
NMOS and PMOS identified
![](https://raw.githubusercontent.com/saicharitha09/VSD_OpenlaneWorkshopSky130/b1a9c12f87557e257500241bda9dab83775b0360/PMOS.png)
Output Y connectivity to PMOS and NMOS drain verified
![](https://raw.githubusercontent.com/saicharitha09/VSD_OpenlaneWorkshopSky130/b1a9c12f87557e257500241bda9dab83775b0360/OUTPUT.png)
PMOS source connectivity to VDD (here VPWR) verified
![](https://raw.githubusercontent.com/saicharitha09/VSD_OpenlaneWorkshopSky130/b1a9c12f87557e257500241bda9dab83775b0360/PMOSOP.png)
NMOS source connectivity to VSS (here VGND) verified
![](https://raw.githubusercontent.com/saicharitha09/VSD_OpenlaneWorkshopSky130/b1a9c12f87557e257500241bda9dab83775b0360/NMOSOP.png)

3. Spice extraction of inverter in magic.

Commands for spice extraction of the custom inverter layout to be used in tkcon window of magic

# Check current directory
pwd

# Extraction command to extract to .ext format
extract all

# Before converting ext to spice this command enable the parasitic extraction also
ext2spice cthresh 0 rthresh 0

# Converting to ext to spice
ext2spice
Screenshot of tkcon window after running above commands
![](
Screenshot of created spice file
![](
4. Editing the spice model file for analysis through simulation.

Measuring unit distance in layout grid
![](


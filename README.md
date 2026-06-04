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
## Section 1 - Inception of open-source EDA, OpenLANE and Sky130 PDK 

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

 Change directory to path containing generated floorplan def
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/17-03_12-06/results/floorplan/

Command to load the floorplan def in magic tool
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

Congestion aware placement by default
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

Exit from OpenLANE flow
exit

 Exit from OpenLANE flow docker sub-system
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

 Change directory to openlane
cd Desktop/work/tools/openlane_working_dir/openlane

Clone the repository with custom inverter design
git clone https://github.com/nickson-jose/vsdstdcelldesign

 Change into repository directory
cd vsdstdcelldesign

 Copy magic tech file to the repo directory for easy access
cp /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech .

 Check contents whether everything is present
ls

 Command to open custom inverter layout in magic
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

 Check current directory
pwd

extraction command to extract to .ext format
extract all

 Before converting ext to spice this command enable the parasitic extraction also
ext2spice cthresh 0 rthresh 0

 Converting to ext to spice
ext2spice
Screenshot of tkcon window after running above commands
![](https://raw.githubusercontent.com/saicharitha09/VSD_OpenlaneWorkshopSky130/b4c74b52af588672aaef6ac6957243d502bcaac9/TK.png)
Screenshot of created spice file
![](https://raw.githubusercontent.com/saicharitha09/VSD_OpenlaneWorkshopSky130/b4c74b52af588672aaef6ac6957243d502bcaac9/SPICE.png)
4. Editing the spice model file for analysis through simulation.


Final edited spice file ready for ngspice simulation
![](https://raw.githubusercontent.com/saicharitha09/VSD_OpenlaneWorkshopSky130/b4c74b52af588672aaef6ac6957243d502bcaac9/FINAL.png)
5. Post-layout ngspice simulations.

Commands for ngspice simulation

 Command to directly load spice file for simulation to ngspice
ngspice sky130_inv.spice

 Now that we have entered ngspice with the simulation spice file loaded we just have to load the plot
plot y vs time a

Screenshots of ngspice run
![](https://raw.githubusercontent.com/saicharitha09/VSD_OpenlaneWorkshopSky130/b4c74b52af588672aaef6ac6957243d502bcaac9/NGSPICE.png)
Screenshot of generated plot
![](https://raw.githubusercontent.com/saicharitha09/VSD_OpenlaneWorkshopSky130/b4c74b52af588672aaef6ac6957243d502bcaac9/PLOT.png)

Rise transition time calculation
 R i s e   t r a n s i t i o n   t i m e = T i m e   t a k e n   f o r   o u t p u t   t o   r i s e   t o   80 % − T i m e   t a k e n   f o r   o u t p u t   t o   r i s e   t o   20 %
20 %   o f   o u t p u t = 660   m V
80 %   o f   o u t p u t = 2.64   V 

20% Screenshots
![](https://raw.githubusercontent.com/saicharitha09/VSD_OpenlaneWorkshopSky130/e700157be7e3130117fb25a473f6069d445d469a/20ss.png)
80% Screenshots
![](https://raw.githubusercontent.com/saicharitha09/VSD_OpenlaneWorkshopSky130/e700157be7e3130117fb25a473f6069d445d469a/80ss.png)
 R i s e   t r a n s i t i o n   t i m e = 2.24638 − 2.18242 = 0.06396   n s = 63.96   p s

Fall transition time calculation
F a l l   t r a n s i t i o n   t i m e = T i m e   t a k e n   f o r   o u t p u t   t o   f a l l   t o   20 % − T i m e   t a k e n   f o r   o u t p u t   t o   f a l l   t o   80 %
20 %   o f   o u t p u t = 660   m V
80 %   o f   o u t p u t = 2.64   V 
 F a l l   t r a n s i t i o n   t i m e = 4.0955 − 4.0536 = 0.0419   n s = 41.9   p s

Rise Cell Delay Calculation
R i s e   C e l l   D e l a y = T i m e   t a k e n   f o r   o u t p u t   t o   r i s e   t o   50 % − T i m e   t a k e n   f o r   i n p u t   t o   f a l l   t o   50 %
50 %   o f   3.3   V = 1.65   V

50% Screenshots
![](https://raw.githubusercontent.com/saicharitha09/VSD_OpenlaneWorkshopSky130/e700157be7e3130117fb25a473f6069d445d469a/50ss.png)
6. Find problem in the DRC section of the old magic tech file for the skywater process and fix them.

Link to Sky130 Periphery rules: https://skywater-pdk.readthedocs.io/en/main/rules/periphery.html

Commands to download and view the corrupted skywater process magic tech file and associated files to perform drc corrections

 Change to home directory
cd

 Command to download the lab files
wget http://opencircuitdesign.com/open_pdks/archive/drc_tests.tgz

 Since lab file is compressed command to extract it
tar xfz drc_tests.tgz

Change directory into the lab folder
cd drc_tests

 List all files and directories present in the current directory
ls -al

 Command to view .magicrc file
gvim .magicrc

 Command to open magic tool in better graphics
magic -d XR &

Screenshots of commands run
![](https://raw.githubusercontent.com/saicharitha09/VSD_OpenlaneWorkshopSky130/e700157be7e3130117fb25a473f6069d445d469a/5sv.png)
Screenshot of .magicrc file
![](https://raw.githubusercontent.com/saicharitha09/VSD_OpenlaneWorkshopSky130/e700157be7e3130117fb25a473f6069d445d469a/magicrc.png)
Incorrectly implemented poly.9 simple rule correction

Screenshot of poly rules
![](https://raw.githubusercontent.com/saicharitha09/VSD_OpenlaneWorkshopSky130/e700157be7e3130117fb25a473f6069d445d469a/polyrule.png)
![](https://raw.githubusercontent.com/saicharitha09/VSD_OpenlaneWorkshopSky130/e700157be7e3130117fb25a473f6069d445d469a/poly2.png)
New commands inserted in sky130A.tech file to update drc
![](https://raw.githubusercontent.com/saicharitha09/VSD_OpenlaneWorkshopSky130/e700157be7e3130117fb25a473f6069d445d469a/newcommands.png)
Commands to run in tkcon window

 Loading updated tech file
tech load sky130A.tech

 Must re-run drc check to see updated drc errors
drc check

 Selecting region displaying the new errors and getting the error messages 
drc why
Screenshot of magic window with rule implemented
![](https://raw.githubusercontent.com/saicharitha09/VSD_OpenlaneWorkshopSky130/e700157be7e3130117fb25a473f6069d445d469a/nc.png)
Section 4 - Pre-layout timing analysis and importance of good clock tree 
Theory
Implementation

    Section 4 tasks:-

    Fix up small DRC errors and verify the design is ready to be inserted into our flow.
    Save the finalized layout with custom name and open it.
    Generate lef from the layout.
    Copy the newly generated lef and associated required lib files to 'picorv32a' design 'src' directory.
    Edit 'config.tcl' to change lib file and add the new extra lef into the openlane flow.
    Run openlane flow synthesis with newly inserted custom inverter cell.
    Remove/reduce the newly introduced violations with the introduction of custom inverter cell by modifying design parameters.
    Once synthesis has accepted our custom inverter we can now run floorplan and placement and verify the cell is accepted in PnR flow.
    Do Post-Synthesis timing analysis with OpenSTA tool.
    Make timing ECO fixes to remove all violations.
    Replace the old netlist with the new netlist generated after timing ECO fix and implement the floorplan, placement and cts.
    Post-CTS OpenROAD timing analysis.
    Explore post-CTS OpenROAD timing analysis by removing 'sky130_fd_sc_hd__clkbuf_1' cell from clock buffer list variable 'CTS_CLK_BUFFER_LIST'.

    Section 4 - Tasks 1 to 4 files, reports and logs can be found in the following folder:

Section 4 - Tasks 1 to 4 (vsdstdcelldesign)

    Section 4 - Task 4 files, reports and logs can be found in the following folder:

Section 4 - Task 4 (src)

    Section 4 - Task 5 files, reports and logs can be found in the following folder:

Section 4 - Task 5 (picorv32a)

    Section 4 - Tasks 6 to 8 & 11 to 13 logs, reports and results can be found in following run folder:

Section 4 - Tasks 6 to 8 & 11 to 13 Run (24-03_10-03)

    Section 4 - Tasks 9 to 11 logs, reports and results can be found in following run folder:

Section 4 - Tasks 9 to 11 Run (25-03_18-52)
1. Fix up small DRC errors and verify the design is ready to be inserted into our flow.

Conditions to be verified before moving forward with custom designed cell layout:

    Condition 1: The input and output ports of the standard cell should lie on the intersection of the vertical and horizontal tracks.
    Condition 2: Width of the standard cell should be odd multiples of the horizontal track pitch.
    Condition 3: Height of the standard cell should be even multiples of the vertical track pitch.

Commands to open the custom inverter layout

 Change directory to vsdstdcelldesign
cd Desktop/work/tools/openlane_working_dir/openlane/vsdstdcelldesign

 Command to open custom inverter layout in magic
magic -T sky130A.tech sky130_inv.mag &

Screenshot of tracks.info of sky130_fd_sc_hd

![](https://raw.githubusercontent.com/saicharitha09/VSD_OpenlaneWorkshopSky130/c9bca00abaaab4fa1d83cbfd21b2c790570d6ac0/prelayout.png)
Commands for tkcon window to set grid as tracks of locali layer

 Get syntax for grid command
help grid

 Set grid values accordingly
grid 0.46um 0.34um 0.23um 0.17um

Screenshot of commands run

![](https://raw.githubusercontent.com/saicharitha09/VSD_OpenlaneWorkshopSky130/c9bca00abaaab4fa1d83cbfd21b2c790570d6ac0/prelayout2.png)
Condition 1 verified

![](https://raw.githubusercontent.com/saicharitha09/VSD_OpenlaneWorkshopSky130/c9bca00abaaab4fa1d83cbfd21b2c790570d6ac0/condition1.png)
Condition 2 verified
H o r i z o n t a l   t r a c k   p i t c h = 0.46   u m

![](https://raw.githubusercontent.com/saicharitha09/VSD_OpenlaneWorkshopSky130/c9bca00abaaab4fa1d83cbfd21b2c790570d6ac0/condition2.png)
 W i d t h   o f   s t a n d a r d   c e l l = 1.38   u m = 0.46 ∗ 3

Condition 3 verified
V e r t i c a l   t r a c k   p i t c h = 0.34   u m 
![](https://raw.githubusercontent.com/saicharitha09/VSD_OpenlaneWorkshopSky130/c9bca00abaaab4fa1d83cbfd21b2c790570d6ac0/condition3.png)
H e i g h t   o f   s t a n d a r d   c e l l = 2.72   u m = 0.34 ∗ 8
2. Save the finalized layout with custom name and open it.

Command for tkcon window to save the layout with custom name

 Command to save as
save sky130_vsdinv.mag

Command to open the newly saved layout

 Command to open custom inverter layout in magic
magic -T sky130A.tech sky130_vsdinv.mag &

Screenshot of newly saved layout
![](https://raw.githubusercontent.com/saicharitha09/VSD_OpenlaneWorkshopSky130/c9bca00abaaab4fa1d83cbfd21b2c790570d6ac0/newlayout.png)
3. Generate lef from the layout.

Command for tkcon window to write lef

lef command
lef write

Screenshot of command run

![](https://raw.githubusercontent.com/saicharitha09/VSD_OpenlaneWorkshopSky130/c9bca00abaaab4fa1d83cbfd21b2c790570d6ac0/leflayout.png)
4. Copy the newly generated lef and associated required lib files to 'picorv32a' design 'src' directory.

Commands to copy necessary files to 'picorv32a' design 'src' directory

 Copy lef file
cp sky130_vsdinv.lef ~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/

 List and check whether it's copied
ls ~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/

 Copy lib files
cp libs/sky130_fd_sc_hd__* ~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/

 List and check whether it's copied
ls ~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/



5. Edit 'config.tcl' to change lib file and add the new extra lef into the openlane flow.

Commands to be added to config.tcl to include our custom cell in the openlane flow

set ::env(LIB_SYNTH) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__typical.lib"
set ::env(LIB_FASTEST) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__fast.lib"
set ::env(LIB_SLOWEST) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__slow.lib"
set ::env(LIB_TYPICAL) "$::env(OPENLANE_ROOT)/designs/picorv32a/src/sky130_fd_sc_hd__typical.lib"

set ::env(EXTRA_LEFS) [glob $::env(OPENLANE_ROOT)/designs/$::env(DESIGN_NAME)/src/*.lef]

Edited config.tcl to include the added lef and change library to ones we added in src directory
![](https://raw.githubusercontent.com/saicharitha09/VSD_OpenlaneWorkshopSky130/c9bca00abaaab4fa1d83cbfd21b2c790570d6ac0/configtcl.png)
6. Run openlane flow synthesis with newly inserted custom inverter cell.

Commands to invoke the OpenLANE flow include new lef and perform synthesis

 Change directory to openlane flow directory
cd Desktop/work/tools/openlane_working_dir/openlane

 alias docker='docker run -it -v $(pwd):/openLANE_flow -v $PDK_ROOT:$PDK_ROOT -e PDK_ROOT=$PDK_ROOT -u $(id -u $USER):$(id -g $USER) efabless/openlane:v0.21'
 Since we have aliased the long command to 'docker' we can invoke the OpenLANE flow docker sub-system by just running this command
docker

 Now that we have entered the OpenLANE flow contained docker sub-system we can invoke the OpenLANE flow in the Interactive mode using the following command
./flow.tcl -interactive

 Now that OpenLANE flow is open we have to input the required packages for proper functionality of the OpenLANE flow
package require openlane 0.9

 Now the OpenLANE flow is ready to run any design and initially we have to prep the design creating some necessary files and directories for running a specific design which in our case is 'picorv32a'
prep -design picorv32a

 Adiitional commands to include newly added lef to openlane flow
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs

 Now that the design is prepped and ready, we can run synthesis using following command
run_synthesis
![](https://raw.githubusercontent.com/saicharitha09/VSD_OpenlaneWorkshopSky130/c9bca00abaaab4fa1d83cbfd21b2c790570d6ac0/runsyn.png)
7. Remove/reduce the newly introduced violations with the introduction of custom inverter cell by modifying design parameters.

Noting down current design values generated before modifying parameters to improve timing
![](https://raw.githubusercontent.com/saicharitha09/VSD_OpenlaneWorkshopSky130/c9bca00abaaab4fa1d83cbfd21b2c790570d6ac0/runtiming.png)
Commands to view and change parameters to improve timing and run syn
 Now once again we have to prep design so as to update variables
prep -design picorv32a -tag 24-03_10-03 -overwrite

 Addiitional commands to include newly added lef to openlane flow merged.lef
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs

 Command to display current value of variable SYNTH_STRATEGY
echo $::env(SYNTH_STRATEGY)

 Command to set new value for SYNTH_STRATEGY
set ::env(SYNTH_STRATEGY) "DELAY 3"

 Command to display current value of variable SYNTH_BUFFERING to check whether it's enabled
echo $::env(SYNTH_BUFFERING)

 Command to display current value of variable SYNTH_SIZING
echo $::env(SYNTH_SIZING)

 Command to set new value for SYNTH_SIZING
set ::env(SYNTH_SIZING) 1

 Command to display current value of variable SYNTH_DRIVING_CELL to check whether it's the proper cell or not
echo $::env(SYNTH_DRIVING_CELL)

 Now that the design is prepped and ready, we can run synthesis using following command
run_synthesis
Screenshot of merged.lef in tmp directory with our custom inverter as macro
![](https://raw.githubusercontent.com/saicharitha09/VSD_OpenlaneWorkshopSky130/c9bca00abaaab4fa1d83cbfd21b2c790570d6ac0/tmp.png)
8. Once synthesis has accepted our custom inverter we can now run floorplan and placement and verify the cell is accepted in PnR flow.

Now that our custom inverter is properly accepted in synthesis we can now run floorplan using following command

 Now we can run floorplan
run_floorplan

Screenshots of command run
![](https://raw.githubusercontent.com/saicharitha09/VSD_OpenlaneWorkshopSky130/c9bca00abaaab4fa1d83cbfd21b2c790570d6ac0/FLOORPLAN.png)
![](https://raw.githubusercontent.com/saicharitha09/VSD_OpenlaneWorkshopSky130/c9bca00abaaab4fa1d83cbfd21b2c790570d6ac0/FLOORPLAN2.png)
![](https://raw.githubusercontent.com/saicharitha09/VSD_OpenlaneWorkshopSky130/c9bca00abaaab4fa1d83cbfd21b2c790570d6ac0/FLOORPALN3.png)
Commands to load placement def in magic in another terminal

 Change directory to path containing generated placement def
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/24-03_10-03/results/placement/

 Command to load the placement def in magic tool
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def &

Screenshot of placement def in magic

![](https://raw.githubusercontent.com/saicharitha09/VSD_OpenlaneWorkshopSky130/c9bca00abaaab4fa1d83cbfd21b2c790570d6ac0/INVERTER.png)
![](https://raw.githubusercontent.com/saicharitha09/VSD_OpenlaneWorkshopSky130/c9bca00abaaab4fa1d83cbfd21b2c790570d6ac0/inverter2.png)
Abutment of power pins with other cell from library clearly visible

9. Do Post-Synthesis timing analysis with OpenSTA tool.

Since we are having 0 wns after improved timing run we are going to do timing analysis on initial run of synthesis which has lots of violations and no parameters were added to improve timing

Commands to invoke the OpenLANE flow include new lef and perform synthesis
 Change directory to openlane flow directory
cd Desktop/work/tools/openlane_working_dir/openlane

 alias docker='docker run -it -v $(pwd):/openLANE_flow -v $PDK_ROOT:$PDK_ROOT -e PDK_ROOT=$PDK_ROOT -u $(id -u $USER):$(id -g $USER) efabless/openlane:v0.21'
Since we have aliased the long command to 'docker' we can invoke the OpenLANE flow docker sub-system by just running this command
docker

 Now that we have entered the OpenLANE flow contained docker sub-system we can invoke the OpenLANE flow in the Interactive mode using the following command
./flow.tcl -interactive

 Now that OpenLANE flow is open we have to input the required packages for proper functionality of the OpenLANE flow
package require openlane 0.9

 Now the OpenLANE flow is ready to run any design and initially we have to prep the design creating some necessary files and directories for running a specific design which in our case is 'picorv32a'
prep -design picorv32a

Adiitional commands to include newly added lef to openlane flow
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs

 Command to set new value for SYNTH_SIZING
set ::env(SYNTH_SIZING) 1

 Now that the design is prepped and ready, we can run synthesis using following command
run_synthesis

Commands run final screenshot
![](https://raw.githubusercontent.com/saicharitha09/VSD_OpenlaneWorkshopSky130/8c87d7d14e2d9a5f376dcc96576ed66a7fee7747/final.png)
10. Make timing ECO fixes to remove all violations.

OR gate of drive strength 2 is driving 4 fanouts
![](https://raw.githubusercontent.com/saicharitha09/VSD_OpenlaneWorkshopSky130/8c87d7d14e2d9a5f376dcc96576ed66a7fee7747/0r.png)
11. Replace the old netlist with the new netlist generated after timing ECO fix and implement the floorplan, placement and cts.

Now to insert this updated netlist to PnR flow and we can use write_verilog and overwrite the synthesis netlist but before that we are going to make a copy of the old old netlist

Commands to make copy of netlist
 Change from home directory to synthesis results directory
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/25-03_18-52/results/synthesis/

 List contents of the directory
ls

 Copy and rename the netlist
cp picorv32a.synthesis.v picorv32a.synthesis_old.v

List contents of the directory
ls
Screenshot of commands run
![](https://raw.githubusercontent.com/saicharitha09/VSD_OpenlaneWorkshopSky130/8c87d7d14e2d9a5f376dcc96576ed66a7fee7747/command12.png)
12. Post-CTS OpenROAD timing analysis.

Commands to be run in OpenLANE flow to do OpenROAD timing analysis with integrated OpenSTA in OpenROAD
 Command to run OpenROAD tool
openroad

 Reading lef file
read_lef /openLANE_flow/designs/picorv32a/runs/24-03_10-03/tmp/merged.lef

 Reading def file
read_def /openLANE_flow/designs/picorv32a/runs/24-03_10-03/results/cts/picorv32a.cts.def

 Creating an OpenROAD database to work with
write_db pico_cts.db

Loading the created database in OpenROAD
read_db pico_cts.db
 Read netlist post CTS
read_verilog /openLANE_flow/designs/picorv32a/runs/24-03_10-03/results/synthesis/picorv32a.synthesis_cts.v

 Read library for design
read_liberty $::env(LIB_SYNTH_COMPLETE)

 Link design and library
link_design picorv32a

 Read in the custom sdc we created
read_sdc /openLANE_flow/designs/picorv32a/src/my_base.sdc

 Setting all cloks as propagated clocks
set_propagated_clock [all_clocks]

 Check syntax of 'report_checks' command
help report_checks

# Generating custom timing report
report_checks -path_delay min_max -fields {slew trans net cap input_pins} -format full_clock_expanded -digits 4

 Exit to OpenLANE flow
exit
![](https://raw.githubusercontent.com/saicharitha09/VSD_OpenlaneWorkshopSky130/8c87d7d14e2d9a5f376dcc96576ed66a7fee7747/openroad.png)
![](https://raw.githubusercontent.com/saicharitha09/VSD_OpenlaneWorkshopSky130/8c87d7d14e2d9a5f376dcc96576ed66a7fee7747/openroad2.png)
13. Explore post-CTS OpenROAD timing analysis by removing 'sky130_fd_sc_hd__clkbuf_1' cell from clock buffer list variable 'CTS_CLK_BUFFER_LIST'.

Commands to be run in OpenLANE flow to do OpenROAD timing analysis after changing C
 Checking current value of 'CTS_CLK_BUFFER_LIST'
echo $::env(CTS_CLK_BUFFER_LIST)

 Removing 'sky130_fd_sc_hd__clkbuf_1' from the list
set ::env(CTS_CLK_BUFFER_LIST) [lreplace $::env(CTS_CLK_BUFFER_LIST) 0 0]

 Checking current value of 'CTS_CLK_BUFFER_LIST'
echo $::env(CTS_CLK_BUFFER_LIST)

 Checking current value of 'CURRENT_DEF'
echo $::env(CURRENT_DEF)

 Setting def as placement def
set ::env(CURRENT_DEF) /openLANE_flow/designs/picorv32a/runs/24-03_10-03/results/placement/picorv32a.placement.def

 Run CTS again
run_cts

 Checking current value of 'CTS_CLK_BUFFER_LIST'
echo $::env(CTS_CLK_BUFFER_LIST)

 Command to run OpenROAD tool
openroad

 Reading lef file
read_lef /openLANE_flow/designs/picorv32a/runs/24-03_10-03/tmp/merged.lef

 Reading def file
read_def /openLANE_flow/designs/picorv32a/runs/24-03_10-03/results/cts/picorv32a.cts.def

 Creating an OpenROAD database to work with
write_db pico_cts1.db

 Loading the created database in OpenROAD
read_db pico_cts.db

 Read netlist post CTS
read_verilog /openLANE_flow/designs/picorv32a/runs/24-03_10-03/results/synthesis/picorv32a.synthesis_cts.v

 Read library for design
read_liberty $::env(LIB_SYNTH_COMPLETE)

 Link design and library
link_design picorv32a

 Read in the custom sdc we created
read_sdc /openLANE_flow/designs/picorv32a/src/my_base.sdc

 Setting all cloks as propagated clocks
set_propagated_clock [all_clocks]

 Generating custom timing report
report_checks -path_delay min_max -fields {slew trans net cap input_pins} -format full_clock_expanded -digits 4

 Report hold skew
report_clock_skew -hold

 Report setup skew
report_clock_skew -setup

 Exit to OpenLANE flow
exit

 Checking current value of 'CTS_CLK_BUFFER_LIST'
echo $::env(CTS_CLK_BUFFER_LIST)

 Inserting 'sky130_fd_sc_hd__clkbuf_1' to first index of list
set ::env(CTS_CLK_BUFFER_LIST) [linsert $::env(CTS_CLK_BUFFER_LIST) 0 sky130_fd_sc_hd__clkbuf_1]

 Checking current value of 'CTS_CLK_BUFFER_LIST'
echo $::env(CTS_CLK_BUFFER_LIST)
Section 5 - Final steps for RTL2GDS using tritonRoute and openSTA (25/03/2024 - 26/03/2024)
Theory
Implementation

    Section 5 tasks:-

    Perform generation of Power Distribution Network (PDN) and explore the PDN layout.
    Perfrom detailed routing using TritonRoute.
    Post-Route parasitic extraction using SPEF extractor.
    Post-Route OpenSTA timing analysis with the extracted parasitics of the route.

    All section 5 logs, reports and results can be found in following run folder:

Section 5 Run - 26-03_08-45
1. Perform generation of Power Distribution Network (PDN) and explore the PDN layout.

Commands to perform all necessary stages up until now

# Change directory to openlane flow directory
cd Desktop/work/tools/openlane_working_dir/openlane

 alias docker='docker run -it -v $(pwd):/openLANE_flow -v $PDK_ROOT:$PDK_ROOT -e PDK_ROOT=$PDK_ROOT -u $(id -u $USER):$(id -g $USER) efabless/openlane:v0.21'
 Since we have aliased the long command to 'docker' we can invoke the OpenLANE flow docker sub-system by just running this command
docker

 Now that we have entered the OpenLANE flow contained docker sub-system we can invoke the OpenLANE flow in the Interactive mode using the following command
./flow.tcl -interactive

 Now that OpenLANE flow is open we have to input the required packages for proper functionality of the OpenLANE flow
package require openlane 0.9

 Now the OpenLANE flow is ready to run any design and initially we have to prep the design creating some necessary files and directories for running a specific design which in our case is 'picorv32a'
prep -design picorv32a

# Addiitional commands to include newly added lef to openlane flow merged.lef
set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
add_lefs -src $lefs

 Command to set new value for SYNTH_STRATEGY
set ::env(SYNTH_STRATEGY) "DELAY 3"

 Command to set new value for SYNTH_SIZING
set ::env(SYNTH_SIZING) 1

 Now that the design is prepped and ready, we can run synthesis using following command
run_synthesis

 Following commands are alltogather sourced in "run_floorplan" command
init_floorplan
place_io
tap_decap_or

Now we are ready to run placement
run_placement

 Incase getting error
unset ::env(LIB_CTS)

 With placement done we are now ready to run CTS
run_cts

 Now that CTS is done we can do power distribution network
gen_pdn 
Screenshots of power distribution network run
![](https://raw.githubusercontent.com/saicharitha09/VSD_OpenlaneWorkshopSky130/8c87d7d14e2d9a5f376dcc96576ed66a7fee7747/pdn.png)
![](https://raw.githubusercontent.com/saicharitha09/VSD_OpenlaneWorkshopSky130/8c87d7d14e2d9a5f376dcc96576ed66a7fee7747/pdn2.png)
Commands to load PDN def in magic in another terminal
# Change directory to path containing generated PDN def
cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/26-03_08-45/tmp/floorplan/

# Command to load the PDN def in magic tool
magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read 14-pdn.def &
Screenshots of PDN def
![](https://raw.githubusercontent.com/saicharitha09/VSD_OpenlaneWorkshopSky130/8c87d7d14e2d9a5f376dcc96576ed66a7fee7747/pdndef1.png)
![](https://raw.githubusercontent.com/saicharitha09/VSD_OpenlaneWorkshopSky130/8c87d7d14e2d9a5f376dcc96576ed66a7fee7747/pdndef2.png)
2. Perfrom detailed routing using TritonRoute and explore the routed layout.

Command to perform routing
# Check value of 'CURRENT_DEF'
echo $::env(CURRENT_DEF)

# Check value of 'ROUTING_STRATEGY'
echo $::env(ROUTING_STRATEGY)

# Command for detailed route using TritonRoute
run_routing
Screenshots of routing run
![](https://raw.githubusercontent.com/saicharitha09/VSD_OpenlaneWorkshopSky130/8c87d7d14e2d9a5f376dcc96576ed66a7fee7747/routingrun1.png)
![](https://raw.githubusercontent.com/saicharitha09/VSD_OpenlaneWorkshopSky130/8c87d7d14e2d9a5f376dcc96576ed66a7fee7747/rountingrun2.png)
![](https://raw.githubusercontent.com/saicharitha09/VSD_OpenlaneWorkshopSky130/8c87d7d14e2d9a5f376dcc96576ed66a7fee7747/routingrun3316819525-b1900c55-7470-41b2-8b4f-3af871494d99.png)
3. Post-Route parasitic extraction using SPEF extractor.

Commands for SPEF extraction using external tool
# Change directory
cd Desktop/work/tools/SPEF_EXTRACTOR

# Command extract spef
python3 main.py /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/26-03_08-45/tmp/merged.lef /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/26-03_08-45/results/routing/picorv32a.def
4. Post-Route OpenSTA timing analysis with the extracted parasitics of the route.

Commands to be run in OpenLANE flow to do OpenROAD timing analysis with integrated OpenSTA in OpenROAD
# Command to run OpenROAD tool
openroad

 Reading lef file
read_lef /openLANE_flow/designs/picorv32a/runs/26-03_08-45/tmp/merged.lef

Reading def file
read_def /openLANE_flow/designs/picorv32a/runs/26-03_08-45/results/routing/picorv32a.def

 Creating an OpenROAD database to work with
write_db pico_route.db

 Loading the created database in OpenROAD
read_db pico_route.db

 Read netlist post CTS
read_verilog /openLANE_flow/designs/picorv32a/runs/26-03_08-45/results/synthesis/picorv32a.synthesis_preroute.v

Read library for design
read_liberty $::env(LIB_SYNTH_COMPLETE)

Link design and library
link_design picorv32a

Read in the custom sdc we created
read_sdc /openLANE_flow/designs/picorv32a/src/my_base.sdc

 Setting all cloks as propagated clocks
set_propagated_clock [all_clocks]
 Read SPEF
read_spef /openLANE_flow/designs/picorv32a/runs/26-03_08-45/results/routing/picorv32a.spef

 Generating custom timing report
report_checks -path_delay min_max -fields {slew trans net cap input_pins} -format full_clock_expanded -digits 4

# Exit to OpenLANE flow
exit
Screenshots of commands run and timing report generated
![](https://raw.githubusercontent.com/saicharitha09/VSD_OpenlaneWorkshopSky130/8c87d7d14e2d9a5f376dcc96576ed66a7fee7747/timingreport.png)





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

<p align="center">
  <img src="https://github.com/saicharitha09/soc-design-and-planning-nasscom-vsd/assets/63997454/92eb860b-7a88-4c6f-8143-ad3e09fd9c5b" alt="Digital_VLSI_SoC_Design_ _Planning_(RTL2GDSII_Flow)1" width="900">
</p>
#### Chip

* Now, taking a look inside the chip, all the signals from the external world to the chip and vice versa is passed through ***PADS***. The area bound by the pads is ***CORE*** where all the digital logic of the chip is placed. Both the core and pads make up the ***DIE*** which is the basic manufacturing unit in regards to semiconductor chips.


<p align="center">
  <img src="https://github.com/saicharitha09/soc-design-and-planning-nasscom-vsd/assets/63997454/d65a0ddf-2f86-4bbc-8d36-b02e09a1483e" alt="image" width="900">
</p>


* ***FOUNDRY*** is the place where the semiconductor chips are manufactured and ***FOUNDRY IP's*** are Intellectual Properties based on a specific foundry and these IP's require a specific level of intelligence to be produced whereas, repeatable digital logic blocks are called ***MACROS***.


<p align="center">
  <img src="https://github.com/saicharitha09/soc-design-and-planning-nasscom-vsd/assets/63997454/ed1cd25e-6270-4b84-8f0d-f0ea7c8a7ef8" alt="image" width="900">
</p>


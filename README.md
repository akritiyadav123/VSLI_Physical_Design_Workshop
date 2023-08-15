![Screenshot from 2023-08-14 16-08-26 (1)](https://github.com/akritiyadav123/VSLI_Physical_Design_Workshop/assets/126105656/459accd4-8c08-44da-b17b-f2d4803c81a3)# VSLI_Physical_Design_Workshop
# Workshop Day wise Content :
## Day1 – Inception of open-source EDA, OpenLANE and Sky130 PDK
How to talk to computers
SoC design and OpenLANE
Starting RISC-V SoC Reference design
Get familiar to open-source EDA tools
## Day 2 - Understand importance of good floorplan vs bad floorplan and introduction to library cells
Chip Floor planning considerations
Library Binding and Placement
Cell design and characterization flows
General timing characterization parameters
## Day 3 - Design and characterize one library cell using Magic Layout tool and ngspice
Labs for CMOS inverter ngspice simulations
Inception of Layout – CMOS fabrication process
Sky130 Tech File Labs
## Day 4 - Pre-layout timing analysis and importance of good clock tree
Timing modelling using delay tables
Timing analysis with ideal clocks using openSTA
Clock tree synthesis TritonCTS and signal integrity
Timing analysis with real clocks using openSTA
## Day 5 - Final steps for RTL2GDS
Routing and design rule check (DRC)
PNR interactive flow tutorial




# OVERVIEW
OpenLANE is an open-source tool or flow designed for open-source tape-outs. It incorporates a range of tools like Yosys, ABC, OpenSTA, Fault, OpenROAD app, Netgen, and Magic. These tools collectively serve the purpose of chip and macro hardening, essentially transforming design RTL into the final GDSII format. The central objective of OpenLANE is to achieve a seamless GDSII generation process devoid of human intervention. Notably, OpenLANE has been optimized to operate within the Google-Skywater130 Opensource Process Design Kit framework.
day1- Inception of open-source EDA, OpenLANE and Sky130 PDK
## 1.1 - How to talk to computers
Sure! Talking to computers is like giving them a set of instructions using a special language called RISC-V ISA. To run a program, you write it in a regular programming language like C or Java. Then, a compiler translates your program into specific computer instructions. These instructions are turned into binary code by an assembler, which the computer's hardware understands. The computer's hardware, made up of tiny switches, follows these instructions to perform the tasks you want, just like following a recipe to cook a meal.
## 1.2-SoC design and OpenLANE
The objective of the ASIC flow is to generate a GDSII file from an RTL design, which is then used for final layout. This flow is essentially a software that automates the place and route (PnR) process.
.
## ASIC design requires RTL IPs, EDA tools, and PDK data.
- RTL IPs: These are reusable blocks of logic that can be used to create complex circuits.
- EDA tools: These are software programs that automate the design process, such as place and route.
- PDK data: This is information about the manufacturing process, such as the transistor sizes and power consumption.


## Openlane ASIC Flow


.

- Opensource RTL Designs: github, librecores, opencores
- Opensource EDA tools: QFlow, OpenROAD, OpenLANE
- Opensource PDK data: Google Skywater130 PDK
The ASIC flow objective is to convert RTL design to GDSII format used for final layout. The flow is essentially a software also known as automated PnR (Place & route)


## Simplified RTL2GDS FLOW
RTL2GDS is the process of converting a Register Transfer Level (RTL) design into a GDSII file. GDSII is a file format that is used to represent the physical layout of an integrated circuit (IC). The RTL2GDS flow is a complex process that involves a number of steps, including:




## RTL to GDSII Flow
- Synthesis: Convert the RTL code into a gate-level netlist using a standard cell library.
- Floorplanning and Power Planning: Plan the silicon area to ensure robust power distribution.
- Placement: Place the cells on the floorplan rows, aligned with sites.
- Global Placement: Find the optimal position of the cells.
- Detailed Placement: Place the cells in legal positions.
- Routing: Create valid patterns for the wires.
- Signoff: Verify the physical design (DRC, LVS) and timing (STA).


![why-to-adopt-the-asic-design-flow-1](https://github.com/akritiyadav123/VSLI_Physical_Design_Workshop/assets/126105656/6a240b02-3d98-4870-83a1-49ffe7fc79d0)






## Openlane Design Flow

![openlane](https://github.com/akritiyadav123/VSLI_Physical_Design_Workshop/assets/126105656/76e7c630-115f-4a73-bc11-1e2cf0ed9b0f)






## Stages of  Openlane Design Flow
The process of creating an Application Specific Integrated Circuit (ASIC) involves several stages, and it's important to understand that it's not a fixed, one-size-fits-all process. The steps can vary based on specific needs and requirements, but the core concepts remain consistent. Here's a simplified breakdown of the ASIC design flow:

- Architectural Design- A system engineer defines the specifications for the chip, considering physical constraints. A VLSI engineer then designs a microarchitecture that meets these requirements.
- RTL Design/Behavioral Modeling- Using a hardware description language (HDL) like Verilog or VHDL, the engineer creates a high-level design description. This step involves defining the logic and how components interact.
- RTL Verification- The designed logic is tested and verified using simulations to ensure it behaves as intended.
- DFT Insertion: -Design-for-Test (DFT) circuitry is added to facilitate testing of the chip's functionality.
- Logic Synthesis:- The high-level RTL description is converted into a gate-level netlist, optimizing for logic and area.
- Standard Cells-: The gate-level netlist is mapped to standard cells from the Process Design Kit (PDK), forming the building blocks of the chip.
- Post-Synthesis STA Analysis:- Setup analysis is performed on different paths to ensure proper timing.
- Floorplanning:-The chip's area is planned, considering power distribution and macro placement. A power distribution network (PDN) is created, and macro placement and blockages are defined.
- Placement:- Standard cells are placed on the chip's floorplan, considering alignment with rows and sites. Global and detailed placement steps are performed.
- CTS (Clock Tree Synthesis): -A clock distribution network is synthesized to deliver the clock signal to different parts of the chip with minimal skew.
- Routing: -The interconnects between standard cells are established using metal layers. Global and detailed routing steps ensure proper connectivity.
- GDSII Generation-The final layout in GDSII format is generated, which is the file used for manufacturing.
## OpenLANE design stages
- Synthesis
  - yosys - Performs RTL synthesis
  - abc - Performs technology mapping
  - OpenSTA - Performs static timing analysis on the resulting netlist to generate timing reports
- Floorplan and PDN
  - init_fp - Defines the core area for the macro as well as the rows (used for placement) and the tracks (used for routing)
  - ioplacer - Places the macro input and output ports
  - pdn - Generates the power distribution network
  - tapcell - Inserts welltap and decap cells in the floorplan
- Placement
  - RePLace - Performs global placement
  - Resizer - Performs optional optimizations on the design
  - OpenDP - Perfroms detailed placement to legalize the globally placed components
- CTS
  - TritonCTS - Synthesizes the clock distribution network (the clock tree)
- Routing
  - FastRoute - Performs global routing to generate a guide file for the detailed router
  - CU-GR - Another option for performing global routing.
  - TritonRoute - Performs detailed routing
  - SPEF-Extractor - Performs SPEF extraction
- GDSII Generation
  - Magic - Streams out the final GDSII layout file from the routed def
  - Klayout - Streams out the final GDSII layout file from the routed def as a back-up
- Checks
  - Magic - Performs DRC Checks & Antenna Checks
  - Klayout - Performs DRC Checks
  - Netgen - Performs LVS Checks
  - CVC - Performs Circuit Validity Checks
## OpenLANE Files
The openLANE file structure looks something like this:
- skywater-pdk: contains PDK files provided by foundry
- open_pdks: contains scripts to setup pdks for opensource tools
- sky130A: contains sky130 pdk files






## Running OpenLANE and Preparing a Design
To initiate OpenLANE, execute the Docker command and enter an interactive session. The flow.tcl script is responsible for defining the specific parameters of the OpenLANE flow. This script outlines the configuration details for the entire design process.
<br />
docker
<br \>
./flow.tcl -interactive
<br \>
package require openlane 0.9
<br />

prep -design picorv32a

![Screenshot from 2023-08-14 16-08-26 (1)](https://github.com/akritiyadav123/VSLI_Physical_Design_Workshop/assets/126105656/d0b939e5-d138-4000-8c59-38d0c0a3f2e5)


SS


### Review of files & Synthesis step
- A "runs" folder is generated within the picorv32a folder.
- The merged file is created during the merging operation in the pircorv32a design preparation (it merges lef and techlef files)
- Next, we run the synthesis of picorv32a design in the openlane interactive terminal:


### Run synthesis


### SS

- The yosys and ABC tools are utilised to convert RTL to gate level netlist.
- Calcuation of Flop Ratio:<br \>
<b> Flop ratio = Number of D Flip flops / Total Number of cells
</b>

<b>dfxtp_4 = 1613,
Number of cells = 14876,
Flop ratio = 1613/14876 = 0.1084 = 10.84%</b>
- We may check the success of the synthesis step by checking the synthesis folder for the synthesized netlist file (.v file)
- The synthesis statistics report can be accessed within the reports directory. It is usually the last yosys file since files are listed chronologically by date of modification.
- The synthesis timings report are as follows:

### Day 2 Floorplanning & Placement and library cells
### Floorplanning considerations
## Utilization Factor & Aspect Ratio
Two parameters are of importance when it comes to floorplanning namely, Utilisation Factor and Aspect Ratio. They are defined as follows:
Utilisation Factor =  <br /> Area occupied by netlist / Total area of core


Aspect Ratio =  <br /> Height / Width
A Utilisation Factor of 1 signifies 100% utilisation leaving no space for extra cells such as buffer. However, practically, the Utilisation Factor is 0.5-0.6. Likewise, an Aspect ratio of 1 implies that the chip is square shaped. Any value other than 1 implies rectanglular chip.

Creating a unique and well-formatted version of your provided text to avoid plagiarism and make it more reader-friendly:

### Pre-Placed Cells Allocation

Once the Utilization Factor and Aspect Ratio have been determined, the initial placements of pre-placed cells become the next crucial step. These pre-placed cells consist of IPs containing extensive combinational logic that remains fixed in position once placed. As they are established before the placement and routing stages, they are aptly called pre-placed cells.

### Decoupling Capacitors Integration

To ensure proper functionality, pre-placed cells are encircled by decoupling capacitors (decaps). These capacitors counteract the detrimental effects of resistance and capacitance within long interconnects. The attenuation of power supply voltage along these paths can significantly impact the voltage reaching the logic circuits. Such voltage drops can result in signal values entering undefined regions beyond the acceptable noise margin. Decaps, substantial capacitors charged to match the power supply voltage, are positioned in proximity to the logic circuit. Their primary role involves decoupling the circuit from the power supply by furnishing the requisite current. In addition to averting crosstalk, decaps facilitate localized communication.

### Effective Power Planning

Although each block on the chip cannot have individual decaps like the pre-placed macros, meticulous power planning ensures that every block has dedicated VDD and VSS pads. These pads connect to both horizontal and vertical power and ground lines, forming a comprehensive power mesh.

### Strategic Pin Placement

The connectivity of logic gates is outlined by the netlist. The area between the core and die accommodates pin placement. Connectivity details, scripted in VHDL or Verilog, dictate the positions of I/O pads for various pins. Subsequently, a logical placement process segregates the pre-placed macro area from the pin zone.

### Executing Picorv32a Floorplan in OpenLANE

To run the floorplan for the picorv32a design using OpenLANE, follow these steps:

1. Begin by adjusting the following floorplan environment variables in order of increasing priority:

   a. `floorplan.tcl` – This file houses system default environment variables.
   b. `config.tcl` – Modify settings in this file as needed.
   c. `sky130A_sky130_fd_sc_hd_config.tcl` – Make any necessary configurations here.

2. Tweak the following floorplan environment variables or switches to fine-tune the process:

   a. `FP_CORE_UTIL` – Control the core utilization.
   b. `FP_ASPECT_RATIO` – Define the aspect ratio for the floorplan.
   c. `FP_CORE_MARGIN` – Specify the margin area between the core and die.
   d. `FP_IO_MODE` – Set pin configurations (1 for equidistant, 0 for non-equidistant).
   e. `FP_CORE_VMETAL` – Choose the vertical metal layer.
   f. `FP_CORE_HMETAL` – Select the horizontal metal layer. Typically, these values are one more than specified in the files.

With these steps and adjustments, you can effectively execute the picorv32a floorplan using OpenLANE. This strategic process sets the foundation for successful chip design and integration.

.
### Run_floorplan



After the completion of the floorplan run, you will find a `.def` file within the `results/floorplan` directory. To review the floorplan files, you can examine the `floorplan.tcl` script. Please note that the system defaults will have been superseded by switches specified in the `config.tcl` file, which, in turn, can be further overridden by switches set in `sky130A_sky130_fd_sc_hd_config.tcl`.




<b>To visualize the floorplan, you can follow these steps:</b>


1. Navigate to the `results/floorplan` directory.
2. Invoke the Magic layout tool by typing `magic` in the terminal and pressing Enter.
Magic provides an intuitive environment for viewing and manipulating integrated circuit layouts, including floorplans. By following these steps, you can effectively examine and analyze the floorplan layout using Magic.
<br />
magic -T /home/vsduser/OpenLane/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.min.lef def read picorv32a.def &

- One can zoom into Magic layout by selecting an area with left and right mouse click followed by pressing "z" key.
- Various components can be identified by using the what command in tkcon window after making a selection on the component.
- Zooming in also provides a view of decaps present in picorv32a chip.
- The standard cell can be found at the bottom left corner.






### Placement Phase
Following the floorplan, the subsequent crucial step in the OpenLANE ASIC flow is placement. The synthesized netlist is strategically positioned onto the defined floorplan. This phase of placement unfolds in two distinct stages:
- Global Placement:-
This stage involves identifying an optimal position for all cells, regardless of legality, which might lead to cell overlaps. Optimization endeavors are focused on minimizing a parameter called "half-parameter wire length."
- Detailed Placement:
Subsequent to the global placement, detailed placement takes the reins. This stage dynamically adjusts the positions of cells that were initially positioned during global placement. The primary objective here is to rectify any legality issues that might have arisen.
The process of ensuring the legality of cell positions holds significant importance, particularly from a timing perspective.
Legalisation of cells is important from timing point of view.
#### Placement run on OpenLANE & view in Magic

<b> Command: </b>
run_placement

##### Placement Aim: Converging Overflow
The primary objective of placement is to achieve the convergence of the overflow value. Gradual reduction in the overflow value throughout placement indicates successful convergence and a favorable placement outcome.

Design Visualization in Magic -Once placement is completed, visualize the design using the Magic layout tool in the `results/placement` directory. This step allows you to assess the design layout and evaluate the placement results..

magic -T /home/vsduser/OpenLane/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.max.lef def read picorv32a.def &

#### Zoomed-in views of the standard cell placement:

## standard cell design flow 
### Inputs
- Process design kit (PDK)
- Design rule check (DRC) and layout versus schematic (LVS) rules
### SPICE models
- Libraries
- User-defined specifications
### Design steps
- Circuit design
- Layout design
  - Art of layout: Euler's path and stick diagram
- Extraction of parasitics
- Characterization (timing, noise, power)
### Outputs
- Circuit description language (CDL)
- Library exchange format (LEF)
- GDS II
- Extracted SPICE netlist (.cir)
- Timing, noise, and power .lib files
### Standard cell characterization flow
- Read in the models and tech files
- Read extracted spice netlist
- Recognize behavior of the cell
- Read the subcircuits
- Attach power sources
- Apply stimulus to characterization setup
- Provide necessary output capacitance loads
- Provide necessary simulation commands
### GUNA characterization
The open source software called GUNA can be used for characterization. Steps 1-8 are fed into the GUNA software which generates timing, noise, and power models.
## Day3  Design Librery call
OpenLANE allows users to make changes to environment variables on the fly. For instance, if we wish to change the pin placement from equidistant to some other style of placement we may do the following in the openLANE flow:
<br />
set ::env(FP_IO_MODE) 2


### SPICE Deck creation & Simulation
A SPICE deck includes information about the following:
- Model description
- Netlist description
- Component connectivity
- Component values
- Capacitance load
- Nodes
- Simulation type and parameters
- Libraries included
### CMOS inverter Switching Threshold Vm
The sitching threshold of a CMOS inverter is the point on the transfer characteristic where Vin equals Vout (=Vm). At this point both PMOS and NOMOS are in ON state which gives rise to a leakage current
### 16 Mask CMOS Fabrication
The 16-mask CMOS process consists of the following steps:
- Selection of subtrate: Secting the body/substrate material
- Creating active region for transistors: Isolation between active region pockets by SiO2 and Si3N4 deposition followed by photolithography and etching
- N-well and P-well formation: Ion implanation by Boron for P-well and by Phosphorous for N-well formation
- Formation of gate terminal: NMOS and PMOS gates formed by photolithography techniques
- LDD (lightly doped drain) formation: LDD formed to prevent hot electron effect
- Source & drain formation: Screen oxide added to avoid channelling during implants followed by Aresenic implantation and annealing
- Local interconnect formation: Removal of screen oxide by HF etching. Deposition of Ti for low resistant contacts
- Higher level metal formation: CMP for planarization followed by TiN and Tungsten deposition. Top SiN layer for chip protection




### Inverter Standard Cell Layout & SPICE Extraction
1. Obtaining Inverter Magic Layout:
   - Integrate the CMOS inverter's Magic layout into the picorv32a design.
   - Clone the inverter Magic file from `vsdstdcelldesign` by executing git clone https://github.com/nickson-jose/vsdstdcelldesign
 - This operation creates a `vsdstdcelldesign` folder within the `openlane_working_dir/openlane` directory.


2. Simplifying Magic Invocation:
 - For viewing the `sky130_inv.mag` file in Magic, include the `sky130A.tech` file in the command along with its path.
   -To streamline this command, copy the `tech` file from the Magic folder to the vsdstdcelldesign` folder.


3. Invoking `sky130_inv.mag` in Magic:
    View the `sky130_inv.mag` file in Magic effortlessly using.
    magic -T sky130A.tech sky130_inv.mag &

In Sky130 the first layer is called the local interconnect layer or Locali.
To verify whether the layout is that of CMOS inverter, verification of P-diffusiona nd N-diffusion regions with Polysilicon can be observed.
Other verification steps are to check drain and source connections. The drains of both PMOS and NMOS must be connected to output port (here, Y) and the sources of both must be connected to power supply VDD (here, VPWR).
<br />
LEF or library exchange format: A format that tells us about cell boundaries, VDD and GND lines. It contains no info about the logic of circuit and is also used to protect the IP.
<br />
SPICE extraction: Within the Magic environment, following commands are used in tkcon to achieve .mag to .spice extraction:
<br />
extract all
<br />
ext2spice cthresh 0 rethresh 0
<br />
Ext2spice
<b>
This generates the sky130_in.spice file. This SPICE deck is edited to include pshort.lib and nshort.lib which are the PMOS and NMOS libraries respectively. In addition, the minimum grid size of inverter is measured from the magic layout and incorporated into the deck as: .option scale=0.01u. The model names in the MOSFET definitions are changed to pshort.model.0 and nshort.model.0 respectively for PMOS and NMOS.
Finally voltage sources and simulation commands are defined as follows:
<br />
VDD VPWR 0 3.3V
<br />
VSS VGND 0 0
<br />
Va A VGND PUSLE(0V 3.3V 0 0.1ns 0.1 ns 2ns 4ns)
<br />
.tran 1n 20n
<br />
.control
<br />
run 
<br />
.endc
<br />
.end
<br />
The final sky130_inv.spice file is modified to:

<br />
For simulation, ngspice is invoked in the terminal:
<br />
ngspice sky130_inv.spice


<br />
The output "y" is to be plotted with "time" and swept over the input "a":
<br />
plot y vs time a 
</b>



The waveform obtained is as shown:



The spikes in the output at switching points is due to low capacitance loads. This can be taken care of by editing the spice deck to increase the load capacitance value.
### Inverter Standard cell characterization
Four timing parameters are used to characterize the inverter standard cell:
- Rise transition: Time taken for the output to rise from 20% of max value to 80% of max value
- Fall transition- Time taken for the output to fall from 80% of max value to 20% of max value
- Cell rise delay = time(50% output rise) - time(50% input fall)
- Cell fall delay = time(50% output fall) - time(50% input rise)
Rise transition = (2.23843 - 2.17935) = 59.08ps
Fall transition = (4.09291 - 4.05004) = 42.87ps
Cell rise delay = (2.20636 - 2.15) = 56.36ps
Cell fall delay = (4.07479 - 4.05) = 24.79ps
### Magic Features & DRC rules
The technology file is a setup file that declares layer types, colors, patterns, electrical connectivity, DRC, device extraction rules and rules to read LEF and DEF files. Magic layouts can be sourced from opencircuitdesign.com using the command:
<br />
wget http://opencircuitdesign.com/open_pdks/archive/drc_tests.tgz
<br />
tar xfz drc_tests.tgz
### Day 4: Pre layout Timing Analysis & CTS
A requirement for ports as specified in tracks.info is that they should be at intersection of horizontal and vertical tracks. The CMOS Inverter ports A and Y are on li1 layer. It needs to be ensured that they're on the intersection of horizontal and vertical tracks. We access the tracks.info file for the pitch and direction information
<br />
Technology LEF
<br />
Technology LEF part contains the information regarding all the metal interconnects, via information and related design rules whereas cell LEF part contains information related to the geometry of each cell. A sample snapshot is given below to show the information under technology LEF part.


<br />
Port Definition Setup
After completing the layout, the subsequent task involves extracting a LEF file for the cell. However, it's essential to establish specific properties and definitions for the cell's pins, which substantially assist the placer and router tool. In the context of LEF files, a cell housing ports is presented as a macro cell, where these ports are duly declared as the macro's PINs. Our primary goal is to extract a LEF file from a given layout, such as that of a simple CMOS inverter, adhering to the standard format. To achieve this, defining ports and accurately configuring class and use attributes for each port serves as the initial step.
<br />
To streamline the process of port definition, the Magic Layout window proves to be invaluable. Here's how you can proceed:
- Launch the Magic Layout window.
-  Source the designated `.mag` file for your design (in this case, the inverter layout).
-   Navigate to the menu: Edit >> Text. This action opens a dialogue box.

### Standard Cell LEF generation
Before the CMOS Inverter standard cell LEF is extracted, the purpose of ports must be defined: Select port A in magic:
<br />
port class input
port use signal

<br />
Select Y area
port class output
port class signal
<br />


Select VPWR area
port class inout
port use power

<br />

Select VGND area
port class inout
port use ground


<br />
LEF extraction can be carried out in tkcon as follows:
lef write


<br />
This generates sky130_vsdinv.lef file.

<br />
#### Post-synthesis timing analysis
Timing analysis is carried out outside the openLANE flow using OpenSTA tool. For this, a new file pre_sta.conf is created. This file would be reqiured to carry out the STA analysis. Invoke OpenSTA outside the openLANE flow as follows:
sta pre_sta.conf
<br />
#### Clock Tree Synthesis
Clock Tree Synthesis is a technique for distributing the clock equally among all sequential parts of a VLSI design. The purpose of Clock Tree Synthesis is to reduce skew and delay.
The purpose of building a clock tree is enable the clock input to reach every element and to ensure a zero clock skew. H-tree is a common methodology followed in CTS. Before attempting a CTS run in TritonCTS tool, if the slack was attempted to be reduced in previous run, the netlist may have gotten modified by cell replacement techniques. Therefore, the verilog file needs to be modified using the write_verilog command. Then, the synthesis, floorplan and placement is run again. To run CTS use the below command:
run_cts

### Day 5: Final steps in RTL2GDS
#### Power Distribution Network generation
Unlike the general ASIC flow, Power Distribution Network generation is not a part of floorplan run in OpenLANE. PDN must be generated after CTS and post-CTS STA analyses:
<br />
gen_pdn
<br />

We can confirm the success of PDN by checking the current def environment variable: echo $::env(CURRENT_DEF)
#### Routing
OpenLANE uses the TritonRoute tool for routing. There are 2 stages of routing:
- Global routing: Routing region is divided into rectangle grids which are represented as course 3D routes (Fastroute tool)
- Detailed routing: Finer grids and routing guides used to implement physical wiring (TritonRoute tool)
Features of TritonRoute:
- Honouring pre-processed route guides
- Assumes that each net satisfies inter guide connectivity
- Uses MILP based panel routing scheme
- Intra-layer parallel and inter-layer sequential routing framework
<br />
Running routing step in TritonRoute as part of openLANE flow:
<br />
run_routing
<br />
#### Differences from older OpenLANE versions
Recent OpenLANE versions exhibit advancements in optimization algorithms, standard cell libraries, power planning, and automation, contributing to improved chip performance and design efficiency compared to older versions.
##Future Scope
- Design of custom standard cells such as NAND, OR, clock buffers and integrating them in the openLANE flow.
- Detailed IP characterization for all corner models





























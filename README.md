# StrongARM-Latch-based-Analog-Comparator
This repository presents the design of a StrongARM Latch based Analog Comparator implemented using Synopsis Custom Compiler on 28nm CMOS Technology.
# Table of Contents
 * [Introduction](#Introduction)
 * [The StrongARM Latch](#The-StrongARM-Latch)
 * [RS Latch](#RS-Latch)
 * [Tools Used](#Tools-Used)
 * [Pre-Layout Schematics and Simulations](#Pre-Layout-Schematics-and-Simulations)
 * [Netlist of the Circuit](#Netlist-of-the-Circuit)
 * [Observations](#Observations)
 * [Author](#Author)
 * [Acknowledgements](#Acknowledgements)
 * [References](#References)

# Introduction:
A differential Comparator is an integral part of analog to
digital converters where it is used to perform quantisation and
sampling. A standard opamp as a comparator is not preferred
for these applications as it reduces the maximum sampling
frequency that could be attained. In this design, a strongArm
latch is used as the comparator core and is chosen as the core
for this circuit because it consumes zero static power, produces
full swing rail to rail outputs, requires single clock phase and
provides higher sampling bandwidth. The strongArm latch
stage is followed by a RS latch which is used to hold the
output data during precharge phase of the strongArm latch.

# The StrongARM Latch:
The StrongARM latch topology finds wide usage as a sense amplifier, a comparator, or simply a robust
latch with high sensitivity.The latch consists of 5 NMOS and 5 PMOS transistors. Transistor M1 and M2 form the input differential pair, transistor M3-M6 form the cross coupled inverters, S1-S4 are the charging transistors and M7 is the tail current transistor. Operation of the latch consists of three phases, Reset, Amplification, and Regeneration.

During the reset phase, input clock is low which turns of the tail current transistor M7 and the input differential pair M1 and M2 is disconnected. Nodes P,Q,X,Y charge to Vdd through the charging transistors S1,S2,S3,S4 which are on when clock is low. The entire circuit draws no current during reset phase as the cross coupled inverter are turned off.

The amplification phase begins as soon as clock goes from low to high turning off the charging transistors S1,S2,S3,S4 and
turning on the tail current transistor M7, thereby activating the input differential pair M1,M2 which draws current
proportional to the input provided at gate terminals of M1 and M2. The current drawn by M1 and M2 discharges the nodes P and Q which were precharged to Vdd.

The regeneration phase begins when nodes P and Q discharge to Vdd-Vthn , turning M3 and M4 (NMOS transistors of cross coupled inverters) on. Nodes X and
Y then begins discharging from Vdd. Since they form a cross
coupled inverter with positive feedback, the node which discharges faster (i.e the one which draws higher current) and falls down to zero while the other node regenerates back to Vdd, depending on the polarity of input differential votalge. Hence it effectively performs the action of a comparator.
<p align="center">
<img src="/Images/StrongARM Latch Reference Diagram.png"></br>
  Fig. 1: StrongARM Latch 
</p>

# RS Latch
During the reset phase , the output nodes of the StrongArm Latch is precharged to Vdd, hence erasing its previous output which leads to the current output not representing a valid logic level, which confuses the subsequent stages. This issue is resolved by the addition of a reset-set latch connected to the output terminals of the StrongARM latch. The RS latch can change its state only if one of the output of the previous stage falls to zero. This latch then retains the state as the StrongARM latch enters reset phase. 
<p align="center">
<img src="/Images/StrongARM Latch followed by RS Latch.png"></br>
  Fig. 2: StrongARM Latch followed by RS Latch 
</p>

# Tools Used:

Cadence Virtuoso: </br> The Cadence Virtuoso® design platform is a modern solution for full-custom analog, custom digital, and mixed-signal IC design. As the core of the Cadence Custom IC Design Platform, Virtuoso provides design entry, simulation management and analysis, and advanced custom layout editing features. This tool was used to design the circuit at the transistor level.

Cadence ADE Explorer / Assembler: </br> The Cadence Virtuoso® ADE Explorer and ADE Assembler provide a comprehensive and flexible environment for simulation setup, analysis, and verification of analog, RF, mixed-signal, and custom digital designs. These tools facilitated various types of simulations for the circuit designed above, supporting a range of analyses from basic to advanced verification workflows.

UMC 180nm PDK:</b></br>
The UMC 180nm PDK Process Design Kit(PDK) was used in creation and simulation of the above designed circuit.

# Pre-Layout Schematics and Simulations:

## Schematics:
### StrongARM Latch:
Implementation of StrongARM Latch Cell:
<p align="center">
<img src="/Images/StrongARM Latch Schematic.png"></br>
  Fig. 3: StrongARM Latch Schematic 
</p>
<p align="center">
<img src="/Images/StrongARM Latch Symbol.png"></br>
  Fig. 4: StrongARM Latch Symbol 
</p>

### RS Latch:
Implementation of RS Latch Cell:
<p align="center">
<img src="/Images/RS Latch Schematic.png"></br>
  Fig. 5: RS Latch Schematic 
</p>
<p align="center">
<img src="/Images/RS Latch Symbol.png"></br>
  Fig. 6: RS Latch Symbol 
</p>

### Comparator Testbench:
<p align="center">
<img src="/Images/Comparator Testbench.png"></br>
  Fig. 7: Testbench 
</p>

## Simulations:
### Transient Analysis:
Input Parameters:
Fclk = 2GHz; Vdd = 1.8V; Vcm = 1V; Vdiff = 1mV
<p align="center">
<img src="/Images/2GHz1mv.png"></br>
  Fig. 8: Voltage vs time waveforms
</p>

Input Parameters:
Fclk = 2GHz; Vdd = 1.8V; Vcm = 1V; Vdiff = 100mV
<p align="center">
<img src="/Images/2Ghz100mv.png"></br>
  Fig. 9: Voltage vs time waveforms 
</p>

Input Parameters:
Fclk = 2GHz; Vdd = 1.8V; Vcm = 0.5V; Vdiff = 100mV
<p align="center">
<img src="/Images/2Ghz100mv2.png"></br>
  Fig. 10: Voltage vs time waveforms 
</p>

Input Parameters:
Fclk = 2GHz; Vdd = 1.8V; Vcm = 0.5V; Vdiff = 1mV
<p align="center">
<img src="/Images/2GHz1mv2.png"></br>
  Fig. 11: Voltage vs time waveforms 
</p>

# Netlist of the circuit

Final Netlist of the circuit is as follows,


# Observations:


# Author:
• Ashutosh Sharma, MS SSIs, Aalto University, USN Norway, BME Budapest

# Acknowledgements:
• 

# References:
[1] B. Razavi, “The StrongARM Latch [a circuit for all seasons],” IEEE Solid State Circuits Mag., vol. 7, no. 2, pp. 12–17, Spring 2015. doi: 10.1109/MSSC.2015.2418155.

[2] B. Razavi, ”The Design of a Comparator [The Analog Mind],” in IEEE Solid-State Circuits Magazine, vol. 12, no. 4, pp. 8-14, Fall 2020, doi: 10.1109/MSSC.2020.3021865.

[3] A. Almansouri, A. Alturki, A. Alshehri, T. Al-Attar and H. Fariborzi, ”Improved StrongARM latch comparator: Design, analysis and performance evaluation,” 2017 13th Conference on Ph.D. Research in Microelectronics and Electronics (PRIME), 2017, pp. 89-92, doi: 10.1109/PRIME.2017.7974114.

[4] R vinoth, S Ramasamy, ”Design and Implementation of High Speed Latched Comparator using gm/Id Sizing Method


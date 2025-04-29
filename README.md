# StrongARM-Latch-based-Analog-Comparator
This repository presents the design of a StrongARM Latch based Analog Comparator implemented using Cadence on 180nm CMOS Technology.
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
A differential comparator is a crucial component in analog-to-digital converters (ADCs), where it plays a vital role in quantization and sampling operations. Utilizing a standard operational amplifier (op-amp) as a comparator in these applications is generally suboptimal because it limits the achievable maximum sampling frequency. In this work, a StrongARM latch has been employed as the core comparator architecture. The StrongARM latch is selected due to its zero static power consumption, rail-to-rail output swing, single-phase clock operation, and superior sampling bandwidth. To maintain the output state during the precharge phase of the StrongARM latch, an RS latch is cascaded at the output, ensuring data retention and stability.

# The StrongARM Latch:
The StrongARM latch topology is widely recognized for its use in sense amplifiers, comparators, and robust latch circuits requiring high sensitivity. Structurally, it incorporates five NMOS and five PMOS transistors. Transistors M1 and M2 form the input differential pair, M3–M6 constitute the cross-coupled inverter network, S1–S4 serve as the precharge devices, and M7 functions as the tail current source.

The operation of the latch can be divided into three distinct phases: Reset, Amplification, and Regeneration.

Reset Phase: When the clock signal is low, the tail transistor (M7) is turned off, isolating the differential input pair (M1, M2). Simultaneously, nodes P, Q, X, and Y are precharged to the supply voltage (Vdd) via the charging transistors (S1–S4), which are activated during this phase. Since the cross-coupled inverters are off, the circuit draws negligible static current.

Amplification Phase: As the clock transitions from low to high, the charging transistors (S1–S4) are disabled, and the tail current source M7 is activated. This enables M1 and M2 to start conducting based on the input differential voltage, causing a differential discharge of nodes P and Q that were initially at Vdd.

Regeneration Phase: When nodes P and Q discharge down to approximately Vdd–Vth (where Vth is the NMOS threshold voltage), NMOS transistors M3 and M4 in the cross-coupled inverter pair turn on. Nodes X and Y then start discharging from Vdd. Due to the positive feedback provided by the cross-coupled configuration, the node discharging faster (corresponding to the higher input voltage) will be pulled to ground, while the complementary node will regenerate towards Vdd. This mechanism effectively produces a digital output representing the sign of the input differential voltage.

<p align="center"> <img src="Images/StrongARM latch topology.png"></br> Fig. 1: StrongARM Latch </p>


# RS Latch
During the reset phase, the outputs of the StrongARM latch are precharged to Vdd, which momentarily erases the stored data and can cause ambiguity for subsequent digital stages. To overcome this, an RS latch is introduced after the StrongARM latch. The RS latch updates its state only when one of the outputs of the StrongARM latch transitions to logic low (0). After capturing the output, the RS latch retains the logic state during the StrongARM latch's reset phase, thereby ensuring stable and valid output levels for the next stages in the circuit.

<p align="center"> <img src="Images/The StrongARM latch followed by the RS latch.png"></br> Fig. 2: StrongARM Latch followed by RS Latch </p>

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

### RS Latch:
Implementation of RS Latch Cell:
<p align="center">
<img src="/Images/RS Latch Schematic.png"></br>
  Fig. 4: RS Latch Schematic 
</p>

### Comparator Testbench:
<p align="center">
<img src="/Images/Comparator Testbench.png"></br>
  Fig. 5: Testbench 
</p>

## Simulations:
### Transient Analysis:
Input Parameters:
Fclk = 0.625GHz; Vdd = 1.8V; Vcm = 1V; Vdiff = 1mV
<p align="center">
<img src="/Images/0.625GHz1mv.png"></br>
  Fig. 8: Voltage vs time waveforms
</p>

Input Parameters:
Fclk = 0.625GHz; Vdd = 1.8V; Vcm = 0.5V; Vdiff = 1mV
<p align="center">
<img src="/Images/0.625GHz1mv2.png"></br>
  Fig. 9: Voltage vs time waveforms 
</p>

Input Parameters:
Fclk = 0.625GHz; Vdd = 1.8V; Vcm = 1V; Vdiff = 100mV
Fclk = 0.625GHz; Vdd = 1.8V; Vcm = 0.5V; Vdiff = 100mV
<p align="center">
<img src="/Images/0.625GHz100mv0p5V1V.png"></br>
  Fig. 10: Voltage vs time waveforms 
</p>



# Netlist of the circuit

Final Netlist of the circuit is as follows,


# Observations:


# Author:
• Ashutosh Sharma, MS SSIs, Aalto University, USN Norway, BME Budapest

# Acknowledgements:
• Template from Satish Kumar L, B.Tech(EEE), NIT, Tiruchirappalli

# References:
[1] B. Razavi, “The StrongARM Latch [a circuit for all seasons],” IEEE Solid State Circuits Mag., vol. 7, no. 2, pp. 12–17, Spring 2015. doi: 10.1109/MSSC.2015.2418155.

[2] B. Razavi, ”The Design of a Comparator [The Analog Mind],” in IEEE Solid-State Circuits Magazine, vol. 12, no. 4, pp. 8-14, Fall 2020, doi: 10.1109/MSSC.2020.3021865.

[3] A. Almansouri, A. Alturki, A. Alshehri, T. Al-Attar and H. Fariborzi, ”Improved StrongARM latch comparator: Design, analysis and performance evaluation,” 2017 13th Conference on Ph.D. Research in Microelectronics and Electronics (PRIME), 2017, pp. 89-92, doi: 10.1109/PRIME.2017.7974114.

[4] R vinoth, S Ramasamy, ”Design and Implementation of High Speed Latched Comparator using gm/Id Sizing Method



<img width="1079" height="241" alt="Image" src="https://github.com/user-attachments/assets/86d44504-f751-4f4d-ac27-96e0bae2ac32" />


## 1. Introduction

Bandgap Reference(Voltage ref) is one of important building block of any analog IC which provides constant ref voltage, independent of supply voltage and temperature changes, which is expected to change in real world   



### Band Gap Reference Classifications
#### Architecture Based :
* Self Biased
* Operational Amplifier

#### Applications :
1.	Data Converters - ADCs,DACs
2.	Power Management - Voltage Regulators(LDOs-Low Drop), Power Supply Monitoring
3.	Integrated Systems and Sensors - On-Chip Temperature Sensors, Oscillators and PLLs
4.	Digital and Mixed-Signal ICs - Biasing for High-Speed Logic , Memory Circuits
5.	Application-Specific Fields - RF and Mixed-Signal Systems, Portable IoT Devices

### Typical Integrated Circuit / System on Chip (SoC) - "Vref" Point Of View :

The below diagram shows how "Vef" is connected/distributed to various blocks (ADC,DAC, Digital System..etc) 

<img width="718" height="423" alt="Image" src="https://github.com/user-attachments/assets/63bff87e-962a-45d8-ad65-7fe8f81d8fe8" />

## 2. Working Principle
Below are ways we can realize voltage references in integrated circuits. 

1. Making use of a zener diode that breaks down at a known voltage when reverse biased.
2. Making use of the difference in the threshold voltage between an enhancement transistor and a depletion transistor.
3. Cancelling the negative temperature dependence of a pn junction with a positive temperature dependence
from a PTAT (proportional-to-absolute-temperature) circuit.

CTAT-PTAT is most popular for both bipolar and CMOS technologies,

Bandgap voltage reference is based on subtracting the voltage of a forward-biased diode (or
base-emitter junction) having a negative temperature coefficient from a voltage proportional to absolute temperature (PTAT). This PTAT voltage is realized by amplifying the voltage difference of two forward-biased
base-emitter (or diode) junctions. A bandgap voltage reference system is shown below

Simplified Circuit of a Bandgap Voltage Reference

<img width="381" height="184" alt="Image" src="https://github.com/user-attachments/assets/3fa24a97-17db-4994-b59a-29996ef69bf8" />

## 3. Requirements

## 4. Sky130 Lab Setup

## 4. Simulation

##...

Ref:
1. https://www.seas.ucla.edu/brweb/papers/Journals/BR_SSCM_3_2021.pdf
2. 

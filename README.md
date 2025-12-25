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
3. Cancelling the negative temperature dependence of a pn junction with a positive temperature dependence from a PTAT (proportional-to-absolute-temperature) circuit.

CTAT-PTAT is most popular for both bipolar and CMOS technologies,Bandgap voltage reference is based on subtracting the voltage of a forward-biased diode (or base-emitter junction) having a negative temperature coefficient from a voltage proportional to absolute temperature (PTAT). This PTAT voltage is realized by amplifying the voltage difference of two forward-biased base-emitter (or diode) junctions. A bandgap voltage reference system is shown below

Base-emitter voltage as a funcion of collector current and temperature

<img width="347" height="41" alt="Image" src="https://github.com/user-attachments/assets/a6b9f4b2-22f2-4c65-8bfd-79bab7f7f383" />

Simplified Circuit of a Bandgap Voltage Reference

<img width="766" height="220" alt="Image" src="https://github.com/user-attachments/assets/aec87451-742e-430f-b229-989509c986b5" />

Proportional to Absolute Temperature(PTAT) circuit cancels the temperature coefficient of the Vbe

<img width="391" height="62" alt="Image" src="https://github.com/user-attachments/assets/4563a39e-3fb8-48e7-a60c-87ef47efdf2a" />

## 3. Requirements and Design

### 3.1 Design Requirements

⦁	Supply voltage = 1.8V

⦁	Temperature: -40 to 125 Deg Cent.

⦁	Power Consumption < 60uW

⦁	Off current < 2uA

⦁	Start-up time < 2us

⦁	Tempco. Of Vref < 50 ppm


### 3.2 The Self-biased current mirror based constitute of the following components.

1.	CTAT voltage generation circuit
2.	PTAT voltage generation circuit
3.	Self-biased current mirror circuit
4.	Reference branch circuit
5.	Start-up circuit

<img width="694" height="468" alt="Image" src="https://github.com/user-attachments/assets/08bb369e-deee-4e9b-a44c-01c53fec9408" />

### 3.3 Design

1. Current Calculation

   * Max. power Consumption < 60uW
   
   * Max Total Current = 60 uW/1.8V=33.33uA
   
   * So, we have chosen 10uA/branch, (3*10=30uA)
   
   * Start-up current 1-2 uA

3. Choosing Number of BJT in parallel in Branch2

    * Less number of BJT: require less resistance value but matching hampers
   
    * More number of BJT: requires higher resistance value but gives good matching
   
    * So a moderate number have chosen (8 BJT) for better layout matching and moderate resistance value.

5. Calculation of R1

    * R1= Vt* ln (8)/I =26 mv *ln(8)/10.7uA=5 KOhm
   
    * R1 size: W=1.41um, L=7.8um, Unit res value: 2k Ohm
   
    * Number of resistance needed: 2 in series and 2 in parallel (2+2+(2||2))

7. Calculation of R2

    * Current through ref branch:I3=I2=Vt*ln(8)/R1
   
    * Voltage across R2: R2I3=R2/R1(Vtln(8))
   
    * Slope of VR2= R2/R1 (ln(8)*115uv)/Deg Cent.
   
    * Slope of VQ3=-1.6mV/Deg cent
   
    * Adding both and equating to zero, R2 will be around 33k Ohm
   
    * Number of resistance needed: 16 in series and 2 in parallel (2+2...+2+ (2||2))

9. SBCM Design (Self-biased Current Mirror)

   A. PMOS Design in SBCM
  
      * Make both the MP1 and MP2 well in Saturation
  
      * To reduce channel length modulation used L=2um
  
      * Finally the size is L=2u, W=5u and M=4

   B. NMOS Design in SBCM

     * Make both the MN1 and MN2 either in Saturation or in deep sub-threshold
 
     * We have made it in deep sub-threshold
 
     * To reduce channel length modulation used L=1um
 
     * Finally the size is L=1u, W=5u and M=8


### Final Circuit

<img width="779" height="458" alt="Image" src="https://github.com/user-attachments/assets/b2b36fd2-6414-4543-acd5-e766c520f23d" />

## 4. Sky130 Lab Setup

## 4. Simulation

##...

Ref:
1. 
2. 

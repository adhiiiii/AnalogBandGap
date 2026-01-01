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

### 3.1 Design Requirements (VSD Workshop Specific Requirements)

⦁	Supply voltage = 1.8V

⦁	Temperature: -40 to 125 Deg Cent.

⦁	Power Consumption < 60uW

⦁	Off current < 2uA

⦁	Start-up time < 2us

⦁	Tempco. Of Vref < 50 ppm

MOSFET

<img width="457" height="112" alt="Image" src="https://github.com/user-attachments/assets/68b80c81-1a9b-4eb0-b9fc-b2e912be6cea" />

BJT

<img width="355" height="125" alt="Image" src="https://github.com/user-attachments/assets/5118c5b5-33e7-47ba-b8b1-af64382c8f84" />

RESISTOR

<img width="374" height="106" alt="Image" src="https://github.com/user-attachments/assets/f788264a-d568-4348-b294-f374eda8f28a" />

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

## 4. Lab Setup - Analog Design Flow - Sky130

### Magic, Ngspice & Netgen setup

<img width="637" height="344" alt="Image" src="https://github.com/user-attachments/assets/29c5f218-c8e5-4ded-8116-a19e188fb505" />

Analog Design Flow (Opensource Tools & PDK)

<img width="414" height="666" alt="Image" src="https://github.com/user-attachments/assets/a3dee4da-3f06-4993-ace5-a0b473ee4781" />

## 5. Simulation
### 5.1 CTAT Simulation

<img width="930" height="481" alt="Image" src="https://github.com/user-attachments/assets/e3f59395-4a65-436d-89ca-6b681ce9e9a8" />

Spice Execution / Plot

<img width="1264" height="519" alt="Image" src="https://github.com/user-attachments/assets/206091e2-3bdb-49cb-9d03-0576dc3fd109" />

Multiple Current Sources

<img width="828" height="381" alt="Image" src="https://github.com/user-attachments/assets/90326b70-b477-42dd-b308-7643328ef376" />

Spice Execution / Plot

<img width="1403" height="539" alt="Image" src="https://github.com/user-attachments/assets/b1d73925-fb4d-4a68-9807-7971125ebb9f" />

### 5.2 PTAT Simulation

<img width="933" height="783" alt="Image" src="https://github.com/user-attachments/assets/7dedbc9d-078a-4f01-86b2-9f46b9e6619c" />

Spice Execution / Plot

<img width="1904" height="540" alt="Image" src="https://github.com/user-attachments/assets/14aaaa73-631e-4ba3-b62e-1e8cb92b9a17" />
<img width="1346" height="536" alt="Image" src="https://github.com/user-attachments/assets/c2ba1c9d-8d54-4edc-820d-5f1b9cc746ef" />

### 5.3 BGR (ideal) Simulation and prelayout simulation

<img width="860" height="958" alt="Image" src="https://github.com/user-attachments/assets/7b01c8fd-fe53-4b6d-8614-037fe0e136ce" />
<img width="838" height="431" alt="Image" src="https://github.com/user-attachments/assets/546b57ce-076a-43ae-bb11-2c51f25b8df4" />
<img width="1343" height="555" alt="Image" src="https://github.com/user-attachments/assets/b928b3d4-60bc-4cb5-b925-27589679a7b6" />
<img width="705" height="532" alt="Image" src="https://github.com/user-attachments/assets/a997c37a-3196-4917-aa39-507ad3fbd42f" />

### 5.4 Complete BGR (ideal) Simulation and prelayout simulation

<img width="841" height="951" alt="Image" src="https://github.com/user-attachments/assets/c2da8e9d-f65f-4203-865f-11868147b933" />
<img width="765" height="538" alt="Image" src="https://github.com/user-attachments/assets/22b11140-7ce3-4f05-b8de-3b3b99f72ecf" />
<img width="668" height="466" alt="Image" src="https://github.com/user-attachments/assets/9bffb364-93da-411e-9068-baa037fa9505" />
<img width="1408" height="530" alt="Image" src="https://github.com/user-attachments/assets/3ef4fc5c-15cf-4fb1-bd40-799acc2041bf" />

### 5.5 Detailed Startup Circuit Simulation 

<img width="840" height="959" alt="Image" src="https://github.com/user-attachments/assets/28782d9e-6f4e-4834-9011-38ec59cac0aa" />
<img width="777" height="614" alt="Image" src="https://github.com/user-attachments/assets/47c4a74f-b484-40b3-a180-7f1334be1e01" />
<img width="719" height="681" alt="Image" src="https://github.com/user-attachments/assets/efab0a2d-92a3-4673-a9f0-c6f4ff2a2ca6" />
<img width="1919" height="1055" alt="Image" src="https://github.com/user-attachments/assets/e6eab47c-926c-49b4-8497-72197e1983f5" />
<img width="1917" height="1053" alt="Image" src="https://github.com/user-attachments/assets/be137cc8-b91f-4cbb-937d-842aa4efa65b" />
<img width="1916" height="1051" alt="Image" src="https://github.com/user-attachments/assets/ae217352-ba5d-4c92-a051-b4df4c1d13b4" />
<img width="1915" height="1053" alt="Image" src="https://github.com/user-attachments/assets/97b80cc3-8100-4631-adff-312c83cb7789" />
<img width="1914" height="1055" alt="Image" src="https://github.com/user-attachments/assets/74ad714b-86bb-450d-90fa-0a9522d09eac" />
<img width="1918" height="1053" alt="Image" src="https://github.com/user-attachments/assets/0c59f368-dc05-47a5-bde3-db9c8e8f89ae" />

## 6. Layout of the components

<img width="853" height="488" alt="Image" src="https://github.com/user-attachments/assets/e52dbaad-3679-46c5-a62a-4b808e1361cf" />
<img width="1011" height="929" alt="Image" src="https://github.com/user-attachments/assets/b07e0562-a1f1-4d0e-8c13-d3820e5f152c" />
<img width="708" height="337" alt="Image" src="https://github.com/user-attachments/assets/0ff2c4f8-ba0a-4507-92fe-2c2dd58b7963" />
<img width="1593" height="940" alt="Image" src="https://github.com/user-attachments/assets/ee70cd40-6ef9-4a7c-899d-b3da30bbd17e" />
<img width="1463" height="950" alt="Image" src="https://github.com/user-attachments/assets/a53bf623-3b93-41fb-844e-f3518d8b5d73" />
<img width="1487" height="966" alt="Image" src="https://github.com/user-attachments/assets/084c0bdf-f040-4f75-89fb-d3d8cbe1d7ea" />
<img width="1020" height="919" alt="Image" src="https://github.com/user-attachments/assets/056108ca-4916-46b8-a3f2-eeffe39d18e8" />
<img width="1489" height="514" alt="Image" src="https://github.com/user-attachments/assets/e7354f95-a7b9-46af-a5db-d97bdd1b544d" />
<img width="1426" height="764" alt="Image" src="https://github.com/user-attachments/assets/1a4d51b2-6ab6-4eab-8a8c-9b89d5678615" />
<img width="1441" height="837" alt="Image" src="https://github.com/user-attachments/assets/7e7623a0-0940-4861-a815-d23e88330de4" />




## 7. Top-level extraction lvs postlayout -

<img width="948" height="979" alt="Image" src="https://github.com/user-attachments/assets/0d999de4-7ad5-4b2a-8f23-afc6d2ed1ab3" />
<img width="591" height="210" alt="Image" src="https://github.com/user-attachments/assets/88bcbcf7-270f-4a30-a848-a25f96518180" />


In Progress....

##...

### _References_
```
1. Analog Circuit Design
2. Ref Repo - https://github.com/vsdip/vsd-bandgap
```
### _Acknowledgement_

_* Prof. Santunu Sarangi   * Kunal Ghosh, Founder VSD Corportation_ 

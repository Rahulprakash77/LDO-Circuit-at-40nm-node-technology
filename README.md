# LDO-Circuit-at-40nm-node-technology
I chose to design an LDO because it is crucial for providing stable, noise-free voltage in sensitive circuits, ensuring efficient power management. LDOs are vital for minimizing ripple and enhancing system reliability, especially in analog and RF applications. Their simplicity and low cost make them indispensable in modern electronic devices.


## Introduction to Low Dropout Regulator (LDO) Design
A Low Dropout Regulator (LDO) is a crucial analog circuit used to provide a stable and noise-free DC output voltage from a fluctuating input voltage. Unlike traditional linear regulators, LDOs operate efficiently with a small difference between input and output voltages, making them ideal for low-power and portable applications.

LDO circuits are widely employed in systems requiring low noise, fast transient response, and precise voltage regulation, such as smartphones, wearable devices, and sensitive analog circuits. Their simplicity, small footprint, and low quiescent current make them a preferred choice for battery-powered devices.

................................................................................................![image](https://github.com/user-attachments/assets/38ea891a-5653-40ac-bdd9-0b95c65accb2)


The core components of an LDO include an error amplifier, a pass transistor (often PMOS or NMOS), and a feedback network. The error amplifier compares the output voltage to a reference voltage and adjusts the pass transistor to maintain a constant output.

Key design challenges in LDO circuits involve optimizing dropout voltage, load regulation, line regulation, and power supply rejection ratio (PSRR). Additionally, achieving stability under varying load conditions requires careful selection of compensation techniques.

This project focuses on designing an efficient and stable LDO circuit using HDL or analog design tools, aiming for high performance in modern electronic systems. The design will address low dropout, minimal noise, and robust performance across diverse operating conditions.



## Important LDO Parameters:

### 1. **Dropout Voltage (V_Drop)**
   - **Definition**: Dropout voltage is the minimum difference between the input and output voltages at which the LDO can still maintain a regulated output. It is crucial in determining how low the input voltage can go while ensuring proper regulation at the output.

Dropout voltage is the input-to-output differential voltage at which the circuit ceases to regulate
against further reductions in input voltage; this point occurs when the input voltage approaches
the output voltage. Figure 1 shows a typical LDO regulator circuit. In the dropout region, the
PMOS pass element is simply a resistor, and dropout is expressed in terms of its on-resistance
(Ron).

........................![Screenshot 2025-01-01 120304](https://github.com/user-attachments/assets/76e960d9-6889-4cff-a4f5-c67fc7b08c34)

   - **Formula**:
     
     ...............![image](https://github.com/user-attachments/assets/4d7f5fc6-6f2a-42e5-bca9-fa233cf643a3)

     where Vin is the input voltage and Vout is the output voltage.

### 2. **Quiescent Current (I_Q)**
   - **Definition**: Quiescent current is the current drawn by the LDO itself in no-load conditions, meaning it is the current consumed to power the internal circuitry of the regulator. It is important in low-power designs since it contributes to the overall power consumption.

Quiescent, or ground current, is the difference between input and output currents. Low quiescent
current is necessary to maximize the current efficiency. Figure 3 shows the quiescent current
that is defined by Iq = Ii-Io
                                  
Quiescent current consists of bias current (such as band-gap reference, sampling resistor, and
error amplifier currents) and the gate drive current of the series pass element, which do not
contribute to output power. The value of quiescent current is mostly determined by the series
pass element, topologies, ambient temperature, etc.

................![image](https://github.com/user-attachments/assets/7c3b1a80-b5aa-428d-8a7c-87d30b75f90b)


   - **Formula**:

.....................................![image](https://github.com/user-attachments/assets/c96646e9-383f-4a0f-ad61-5d8cddec8766)

  where Iin is the input current and Iout is the output current (which is zero in no-load conditions).

### 3. **Standby Current (I_SB)**
   - **Definition**: Standby current refers to the small current drawn by the LDO when it is in standby mode (not providing power to a load). It is an important consideration for power management, especially in battery-operated devices where every bit of power consumption matters.

Standby current is the input current drawn by a regulator when the output voltage is disabled by
a shutdown signal. The reference and the error amplifier in an LDO regulator are not loaded
during the standby mode, as shown in Figure 4.

................................![image](https://github.com/user-attachments/assets/ca3e15e5-64a0-41b1-a6e7-28ab23e2508a)


### 4. **Efficiency (η)**
   - **Definition**: Efficiency measures how effectively the LDO converts input power to output power. It is a key factor in power-sensitive applications, where high efficiency is crucial to minimize energy waste.

To have a high efficiency, drop out voltage and quiescent current must be minimized. In addition,
the voltage difference between input and output must be minimized, since the power dissipation
of LDO regulators accounts for the efficiency. (Power Dissipation = (Vi – Vo)Io). The input/output
voltage difference is an intrinsic factor in determining the efficiency, regardless of the load
conditions.

   - **Formula**:

     ........................![image](https://github.com/user-attachments/assets/ac5a9950-f878-4376-b057-bbb4d68bf2a3)


     where Pout and Pin are the output and input power, respectively.

### 5. **Transient Response**
   - **Definition**: Transient response refers to how quickly and accurately the LDO can adjust its output voltage in response to a sudden change in load current or input voltage. Fast transient response is vital for applications with dynamic power demands.

................................![image](https://github.com/user-attachments/assets/066cf160-452c-4e96-8258-9818038cd23c)


   - **Formula**: Transient response is typically measured through time-domain simulations, focusing on overshoot, settling time, and response to step changes.

### 6. **Line Regulation (V_LR)**
   - **Definition**: Line regulation measures the LDO’s ability to maintain a constant output voltage despite variations in the input voltage. It is crucial in systems where input voltage can fluctuate.

Line regulation is a measure of the circuit’s ability to maintain the specified output voltage with
varying input voltage. Line regulation is defined as

............................![image](https://github.com/user-attachments/assets/d63115dc-f7ad-4dd3-b112-676d497eba94)


   - **Formula**:
     
...............![image](https://github.com/user-attachments/assets/bfb03aa9-c61f-4c04-b232-7d0ba8bdc26c)

where Vo and Vi are the Change in output voltage and Change in input voltages, respectively.

### 7. **Load Regulation (V_Load)**
   - **Definition**: Load regulation measures the LDO’s ability to maintain a constant output voltage as the load current varies. A good LDO should provide stable voltage across a wide range of load currents.

Load regulation is a measure of the circuit’s ability to maintain the specified output voltage under
varying load conditions. Load regulation is defined as

.....................![image](https://github.com/user-attachments/assets/1f8332ba-afb1-4343-aec5-b7e456da25c6)


   - **Formula**:
     
................................![image](https://github.com/user-attachments/assets/e5bb4747-8e89-4e97-a38a-7fa8f6d483e5)

where Vo and Io are Change in output Voltage and Change in load currents, respectively.

### 8. **Power Supply Rejection Ratio (PSRR)**
   - **Definition**: PSRR indicates how well the LDO can suppress noise or fluctuations from the input power supply. It’s a critical parameter in low-noise applications like audio equipment or RF circuits.

Power supply rejection ratio (PSRR), also known as ripple rejection, measures the LDO
regulator’s ability to prevent the regulated output voltage fluctuating caused by input voltage
variations. The same relation for line regulation applies to PSRR except that the whole
frequency spectrum is considered.

........................![image](https://github.com/user-attachments/assets/531457e3-b216-4d12-92b9-5a99ef1884a8)

    
   - **Formula**: 

............................![image](https://github.com/user-attachments/assets/d334ea5f-4cb1-487e-80da-159db4c7a251)

where Vin_ripple and Vout_ripple are the ripple voltages at the input and output, respectively.

### 9. **Output Noise Voltage (V_{noise})**
   - **Definition**: Output noise voltage refers to the fluctuations or unwanted noise at the LDO’s output due to various internal factors like thermal, shot, and flicker noise. It is important to measure this in sensitive analog applications.
   - **Formula**: Output noise is generally measured in terms of voltage spectral density (V/sqrt(Hz)) or RMS value.


### 10. **Accuracy**
   - **Definition**: Accuracy indicates how closely the LDO’s output voltage matches the desired or target voltage. High accuracy is essential for systems requiring precise voltage levels, such as ADCs and sensitive analog circuitry.
   - **Formula**: 

....................................![image](https://github.com/user-attachments/assets/2b0b6ae8-136f-4d45-ba93-02908dadb525)

where Vout_measured is the actual output voltage, and Vout_desired is the target output voltage.





# (A) LDO with Single Stage OPAMP
## 1. Declaring design specifications.
𝟭. 𝗧𝗼𝗼𝗹 𝗨𝘀𝗲𝗱: 𝗖𝗮𝗱𝗲𝗻𝗰𝗲 𝗩𝗶𝗿𝘁𝘂𝗼𝘀𝗼 𝘄𝗶𝘁𝗵 𝗧𝗦𝗠𝗖 𝟰𝟬𝗻𝗺 𝗡𝗼𝗱𝗲 𝗧𝗲𝗰𝗵𝗻𝗼𝗹𝗼𝗴𝘆
𝗜𝗻𝗽𝘂𝘁 𝗩𝗼𝗹𝘁𝗮𝗴𝗲 (𝗩_𝗶𝗻)

𝟮.(𝗡𝗼𝗺𝗶𝗻𝗮𝗹 𝗶𝗻𝗽𝘂𝘁 𝘃𝗼𝗹𝘁𝗮𝗴𝗲 𝘀𝘂𝗽𝗽𝗹𝗶𝗲𝗱 𝘁𝗼 𝘁𝗵𝗲 𝗟𝗗𝗢)
𝗢𝘂𝘁𝗽𝘂𝘁 𝗩𝗼𝗹𝘁𝗮𝗴𝗲 (𝗩_𝗼𝘂𝘁):  𝟭.𝟭 𝗩 

𝟯. (𝗥𝗲𝗴𝘂𝗹𝗮𝘁𝗲𝗱 𝗼𝘂𝘁𝗽𝘂𝘁 𝘃𝗼𝗹𝘁𝗮𝗴𝗲 𝗱𝗲𝗹𝗶𝘃𝗲𝗿𝗲𝗱 𝘁𝗼 𝘁𝗵𝗲 𝗹𝗼𝗮𝗱)
𝗥𝗲𝗳𝗲𝗿𝗲𝗻𝗰𝗲 𝗩𝗼𝗹𝘁𝗮𝗴𝗲 (𝗩_𝗿𝗲𝗳): 𝟬.𝟵 𝗩 

𝟰. (𝗥𝗲𝗳𝗲𝗿𝗲𝗻𝗰𝗲 𝘃𝗼𝗹𝘁𝗮𝗴𝗲 𝘂𝘀𝗲𝗱 𝗳𝗼𝗿 𝗳𝗲𝗲𝗱𝗯𝗮𝗰𝗸 𝗿𝗲𝗴𝘂𝗹𝗮𝘁𝗶𝗼𝗻 𝗶𝗻 𝘁𝗵𝗲 𝗟𝗗𝗢)
𝗠𝗮𝘅𝗶𝗺𝘂𝗺 𝗟𝗼𝗮𝗱 𝗖𝘂𝗿𝗿𝗲𝗻𝘁 (𝗜_𝗺𝗮𝘅): 𝟬.𝟳𝟱 𝗩 

𝟱. (𝗠𝗮𝘅𝗶𝗺𝘂𝗺 𝗰𝘂𝗿𝗿𝗲𝗻𝘁 𝘁𝗵𝗮𝘁 𝘁𝗵𝗲 𝗟𝗗𝗢 𝗰𝗮𝗻 𝘀𝘂𝗽𝗽𝗹𝘆 𝘁𝗼 𝘁𝗵𝗲 𝗹𝗼𝗮𝗱)
𝗤𝘂𝗶𝗲𝘀𝗰𝗲𝗻𝘁 𝗖𝘂𝗿𝗿𝗲𝗻𝘁 (𝗜_𝗤): 𝟭𝟬 𝗺𝗔 

𝟲. (𝗖𝘂𝗿𝗿𝗲𝗻𝘁 𝗱𝗿𝗮𝘄𝗻 𝗯𝘆 𝘁𝗵𝗲 𝗟𝗗𝗢 𝗶𝘁𝘀𝗲𝗹𝗳 𝘂𝗻𝗱𝗲𝗿 𝗻𝗼-𝗹𝗼𝗮𝗱 𝗰𝗼𝗻𝗱𝗶𝘁𝗶𝗼𝗻𝘀 𝗳𝗼𝗿 𝗶𝗻𝘁𝗲𝗿𝗻𝗮𝗹 𝗼𝗽𝗲𝗿𝗮𝘁𝗶𝗼𝗻) 𝟭𝟬 μ𝗔 


## 2. Designing full circuit and make proper wire connection

![S_stageLDO_BasicCkt](https://github.com/user-attachments/assets/0cd65aa3-622c-4da8-9ea4-b8c336fe510b)

## 3.DC Response

![s2](https://github.com/user-attachments/assets/a8be4a19-3e4d-4157-9648-d8ad9b4db11e)

![image](https://github.com/user-attachments/assets/efeb058f-590a-4cf7-b5c1-8e8f8878ca96)


## 4. Stability Analysis
**DCGain=34.8dB , GBW = 9.2MHz and Phase Margin = 88.65 , Bandwidth=162.1kHz**

![S_stageLDO_stb](https://github.com/user-attachments/assets/80d259f8-aff7-46d5-95ad-62af5945d6d0)

![stb1](https://github.com/user-attachments/assets/3cf4bce1-2bd8-4be9-ab3d-2ae9731e9872)



## 5. Transient Response:

![S_stageLDO_tran](https://github.com/user-attachments/assets/c66bbbc6-aa5e-411d-a601-87644b02e040)

![trans1](https://github.com/user-attachments/assets/75aab684-3277-46b6-8a3b-10eee21224b9)


![trans11](https://github.com/user-attachments/assets/ada76cf3-4081-4328-bbba-b6afa9888309)



## 6. Line Regulation 
**0.029 mV/V**

![S_stageLDO_lineRegu](https://github.com/user-attachments/assets/7f501f7a-6251-44f7-a770-656adba50568)


![lineregu1](https://github.com/user-attachments/assets/26d6345e-88ff-4532-83e7-f70f17ddbd04)

## 7. Load Regulation 
**3.57 mV/mA**

![S_stageLDO_loadRegu](https://github.com/user-attachments/assets/9741e752-52af-4814-a176-1ddfac4f28f4)


![Loadregu1](https://github.com/user-attachments/assets/274bff3f-f9b7-4bd1-8b24-c923a5faba6a)

## 8. PSRR Plot


![S_stageLDO_psrr](https://github.com/user-attachments/assets/b1a5678f-b62f-4ea6-8b0a-9aa0bbc799c3)

![psrr1](https://github.com/user-attachments/assets/f653ea25-c550-46d0-bdf4-4604e3d063cb)

## 9. Noise Plot

![S_stageLDO_noise](https://github.com/user-attachments/assets/0c13d035-6c32-40cb-b83a-28458f81669a)


![noise1](https://github.com/user-attachments/assets/a2555052-18d9-467b-9e04-8f473ec79cf8)








# Design and Analysis of 3-Phase Inverter Using Sinusoidal ePWM Modulation Technique

## Introduction
This project focuses on the design and analysis of a three-phase inverter using the Sinusoidal Pulse Width Modulation (SPWM) technique. The inverter plays a crucial role in converting DC power into three-phase AC power and is widely used in motor drives, renewable energy applications, and uninterruptible power supplies (UPS).

<p align="center">
  <img src="https://github.com/vandemataram15aug1947/Design_and_Analysis_of_3_Phase_Inverter_Using_Sinusoidal_ePWM_Modulation_Technique/blob/829a5234077cdaf1ea7eb9cbc2068bc538f7fa20/Photos/Sine%20Compare%20with%20Triangular%20Wave.png" width="500">
</p>  

<p align="center"><b>Figure 1:</b> Sine Compare with Triangular Wave</p>  

## Sinusoidal Pulse Width Modulation (SPWM)
SPWM is the most commonly used PWM technique for controlling inverters. It generates gating signals by comparing a sinusoidal control signal with a triangular carrier waveform. The frequency of the sinusoidal control signal determines the desired inverter output frequency.

<p align="center">
  <img src="https://github.com/vandemataram15aug1947/Design_and_Analysis_of_3_Phase_Inverter_Using_Sinusoidal_ePWM_Modulation_Technique/blob/3fcad04b6156f3dbe938ac160a95234b6a028c2a/Photos/Three-Phase%20Inverter%20Circuit.png" width="500">
</p>  

<p align="center"><b>Figure 1:</b> Three-Phase Inverter Circuit</p>  

### Working Principle
- When `VcontrolA > Vtri`, `S1` is ON, and `VAN = Vd`.
- When `VcontrolA < Vtri`, `S2` is ON, and `VAN = 0`.
- When `VcontrolB > Vtri`, `S3` is ON, and `VBN = Vd`.
- When `VcontrolB < Vtri`, `S4` is ON, and `VBN = 0`.
- When `VcontrolC > Vtri`, `S5` is ON, and `VCN = Vd`.
- When `VcontrolC < Vtri`, `S6` is ON, and `VCN = 0`.

<p align="center">
  <img src="https://github.com/vandemataram15aug1947/Design_and_Analysis_of_3_Phase_Inverter_Using_Sinusoidal_ePWM_Modulation_Technique/blob/5d0571e88ccee716accb8d8f1b00c4db5c63d833/Photos/SPWM%20Three-Phase%20Inverter%20Waveforms.png" width="500">
</p>  

<p align="center"><b>Figure 1:</b> SPWM Three-Phase Inverter Waveforms</p>  

### Voltage Equations
The line-to-line voltages are computed as follows:
```math
V_{AB} = V_{AN} - V_{BN},
V_{BC} = V_{BN} - V_{CN},
V_{CA} = V_{CN} - V_{AN}
```

For the linear range of `m_a`, the fundamental component in `VAN` is:
```math
V_{AN} = \frac{m_a V_d}{2}
```

RMS value of `VAN`:
```math
V_{AN} = \frac{1}{\sqrt{2}} \frac{m_a V_d}{2}
```

RMS line-to-line voltage:
```math
V_{LL} = \sqrt{3} \frac{1}{\sqrt{2}} \frac{m_a V_d}{2} \approx 0.612 \, m_a V_d
```

Solving for `Vd`:
```math
V_d = \frac{V_{LL}}{0.612 \, m_a}
```

Example Calculation (for `V_{LL} = 110V` and `m_a = 0.8`):
```math
V_d = \frac{110}{0.612 \times 0.8} = 224.67V
```

The nominal power rating `P` is:
```math
P = \sqrt{3} \, V_{LL} \, I_L
```
Given `R = 10Ω`, the RMS line current `I_L`:
```math
I_L = \frac{V_{LL}}{3R} = \frac{110}{3 \times 10} = 3.67A
```
Nominal Power:
```math
P = \sqrt{3} \times 110 \times 3.67 = 700W
```

## Key System Specifications
| SL. NO. | Parameter                  | Specifications          |
|---------|---------------------------|-------------------------|
| 1       | DC Bus Voltage             | 230V                    |
| 2       | IGBT Rating                | IHW25N120E1XKSA1, 1200V 25A |
| 3       | Output Line Voltage        | 110V RMS                |
| 4       | Output Current             | 3.67A RMS               |
| 5       | Controller                 | TMS320F28379D           |
| 6       | PWM Switching Frequency    | 10kHz                   |
| 7       | Nominal Power Rating       | 700W                    |

## Repository Contents
- **Documentation:** Contains the detailed analysis of the inverter design and SPWM technique.
- **Code:** Implementation of SPWM using TMS320F28379D.
- **Simulations:** MATLAB/Simulink and hardware implementation details.
- **Results:** Experimental waveforms and validation.

## Getting Started
1. Clone this repository:
   ```sh
   git clone https://github.com/yourusername/3phase-inverter-SPWM.git
   ```
2. Install the necessary dependencies.
3. Compile and run the code in Code Composer Studio (CCS).
4. Verify SPWM signals and inverter output.


# Hardware Setup

## Overview
This repository documents the hardware setup for a power electronics project involving a three-leg inverter circuit controlled by a TMS320F28379D microcontroller. The setup includes gate driver circuits, power supply components, and measurement instruments.

## Hardware Components

### 1. Inverter Circuit
The inverter circuit consists of three legs, each controlled via dedicated gate driver circuits. The inverter is enclosed in an acrylic case for safety.

### 2. Microcontroller (MCU)
- **Piccolo LaunchPad TMS320F28379D**
- Used for controlling the inverter circuit through PWM signals.
- Connected to a laptop for programming and monitoring.

### 3. Gate Driver Circuits
- Three separate gate driver circuits, each corresponding to an inverter leg.
- Ensures proper switching of the inverter’s power transistors.

### 4. Power Supply and Rectifier
- **Transformer**: Provides AC voltage for rectification.
- **Bridge Rectifier Circuit**: Converts AC to DC for powering the inverter.
- **Isolated IGBT Gate Driver Flyback Power Supply**: Supplies isolated power for gate drivers.

### 5. Measurement and Debugging Instruments
- **Digital Storage Oscilloscope (DSO)**: Used for analyzing inverter waveforms.
- **Laptop with Code Composer Studio (CCS)**: For programming and debugging the TMS320F28379D.

## Connections & Wiring
- The gate driver circuits are wired to the corresponding inverter legs.
- The MCU generates PWM signals for controlling switching events.
- The rectifier and power supply provide the required voltage levels.
- Measurement probes from the DSO are connected to key points for real-time waveform observation.

# **Three-Phase Line-to-Line Voltage Analysis**

## **Overview**
This repository contains oscilloscope waveform analysis of three-phase **line-to-line voltages** measured from an inverter system. The data provides insights into the voltage characteristics and switching behavior of the system.

## **Captured Waveforms**
The following line-to-line voltages are analyzed:

- **R-Y Voltage** (Red Phase to Yellow Phase)
- **Y-B Voltage** (Yellow Phase to Blue Phase)
- **B-R Voltage** (Blue Phase to Red Phase)

### **Waveform Observations**
#### **1. R-Y Voltage (Orange Waveform)**
- Displays a **stepped structure**, indicating a **PWM-controlled inverter output**.
- The frequency measurement suggests a periodic switching operation.
- The presence of switching harmonics suggests the need for filtering.

 <p align="center">
  <img src="https://github.com/vandemataram15aug1947/Design_and_Analysis_of_3_Phase_Inverter_Using_Sinusoidal_ePWM_Modulation_Technique/blob/d02c4d3035adfe3556873c35c5fe58bc104deb8c/Photos/R-Y%20Voltage.png" width="500">
</p>  

<p align="center"><b>Figure 1:</b> R-Y Voltage</p>  


#### **2. Y-B Voltage (Green Waveform)**
- Similar stepped waveform with **PWM switching** characteristics.
- Expected phase shift observed between the line voltages.
- Some distortions indicate high-frequency switching ripples.

 <p align="center">
  <img src="https://github.com/vandemataram15aug1947/Design_and_Analysis_of_3_Phase_Inverter_Using_Sinusoidal_ePWM_Modulation_Technique/blob/d02c4d3035adfe3556873c35c5fe58bc104deb8c/Photos/Y-B%20Voltage.png" width="500">
</p>  

<p align="center"><b>Figure 1:</b> Y-B Voltagee</p>  


#### **3. B-R Voltage (Blue Waveform)**
- Follows a similar pattern to the other two voltages.
- Complements the other phase voltages to ensure proper **three-phase balance**.
- Indicates that the system is operating as a **three-phase inverter**.

 <p align="center">
  <img src="https://github.com/vandemataram15aug1947/Design_and_Analysis_of_3_Phase_Inverter_Using_Sinusoidal_ePWM_Modulation_Technique/blob/d02c4d3035adfe3556873c35c5fe58bc104deb8c/Photos/B-R%20Voltage.png" width="500">
</p>  

<p align="center"><b>Figure 1:</b> B-R Voltagee</p>  

## **Key Takeaways**
- The waveforms confirm that the system is a **three-phase inverter** generating AC voltage from a DC source.
- The **PWM switching artifacts** indicate the need for an **LC or LCL filter** to smoothen the waveform into a pure sine wave.
- The **line-to-line voltages** exhibit the expected phase relationships, ensuring balanced operation.

## **Next Steps**
- Implement **LC or LCL filters** to reduce harmonics and obtain sinusoidal output.
- Optimize **PWM switching techniques** to minimize switching losses and improve waveform quality.
- Perform **Fourier analysis (FFT)** to evaluate total harmonic distortion (THD).
- Validate phase relationships using further experimental measurements.

## **References**
- Power Electronics by Ned Mohan
- IEEE Papers on **PWM control techniques for three-phase inverters**

---
📌 **Author**: [Your Name]  
📌 **License**: MIT  
📌 **Contributions**: Open to suggestions and improvements! Feel free to submit PRs or open issues. 🚀


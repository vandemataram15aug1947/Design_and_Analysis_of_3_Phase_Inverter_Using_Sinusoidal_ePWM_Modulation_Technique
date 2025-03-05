
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


## **Implementation Steps**  

### **1. Hardware Setup**  
- **Connect all components** to their appropriate **GPIO pins** and **power supply lines** on the **TMS320F28379D**.  
- The **potentiometer output** is connected to the **ADC** to provide real-time speed control input.  
- The **MOSFET trigger module** is connected to the **PWM output** of the microcontroller.  
- The **relay module**, **LED module**, and **buzzer** are connected to dedicated GPIO pins for additional control functions.  
- A **current-limiting resistor** is placed in series with the LED to **prevent excessive current draw**.  

### **2. Software Implementation**  
- The **firmware is written in C/C++** using **Code Composer Studio (CCS)**.  
- The **PWM duty cycle** is dynamically adjusted based on the **ADC reading from the potentiometer**.  
- **GPIOs are configured** for controlling the **relay, LED, and buzzer**.  
- The **PWM signal is generated using the ePWM module** of the **TMS320F28379D**.  
- The **buzzer and LED module** provide **status indication** during operation.  

# **Code Implementation**

Below is the main loop implementation for Speed Control of a DC Motor:

```c
/*
 * Speed Control of a DC Motor Using ePWM on the TMS320F28379D Microcontroller
 *
 * Created on: Dec 5, 2023
 * Author: Vande
 */

#include "F2837xD_device.h"
#include "F28x_Project.h"
#include "driverlib.h"
#include "device.h"

/* ----------------------- Macro Definitions ----------------------- */
#define EX_ADC_RESOLUTION 12  /* ADC Resolution (12-bit) */

/* ----------------------- Function Prototypes ----------------------- */
void gpio_init(void);
void PinMux_init(void);
void initEPWM1(void);

void toggleLED(void);
void toggleBuzzer(void);
void toggleRelay(void);

void setLED(bool set);
void setBuzzer(bool set);
void setRelay(bool set);

void delayCount(void);
void ConfigADC(void);
void initADC_SOC(void);

/* ----------------------- Global Variables ----------------------- */
uint16_t Adc_Result_1, prev_Adc_Result_1, Adc_Result_2;
uint16_t delayCounter_ms, delayCounter_s;
int count;

/* ----------------------- Main Function ----------------------- */
void main(void) {
    /* Initialize Device and Peripherals */
    Device_init();
    Device_initGPIO();
    PinMux_init();
    
    Interrupt_initModule();
    Interrupt_initVectorTable();
    
    IER = 0x0000;
    IFR = 0x0000;
    
    SysCtl_disablePeripheral(SYSCTL_PERIPH_CLK_TBCLKSYNC);
    SysCtl_enablePeripheral(SYSCTL_PERIPH_CLK_TBCLKSYNC);
    
    ConfigADC();
    initADC_SOC();
    
    /* Initialize Variables */
    Adc_Result_1 = 0;
    prev_Adc_Result_1 = 0;
    delayCounter_ms = 0;
    delayCounter_s = 0;
    count = 0;
    
    EINT;
    ERTM;
    
    while (1) {
        /* ADC Conversion and Result Processing */
        // Force ADC Conversion
        // Wait for completion
        // Store ADC result
        
        /* Motor Control Logic */
        // Implement PWM control based on ADC result
        
        /* Peripheral Control Logic */
        // LED, Buzzer, and Relay Control
        
        /* Timing and Delay Handling */
        delayCount();
    }
}

/* ----------------------- Function Definitions ----------------------- */

void PinMux_init(void) {
    /* GPIO Pin Initialization for PWM, LED, Buzzer, and Relay */
}

void toggleLED(void) {
    /* Toggle LED State */
}

void toggleBuzzer(void) {
    /* Toggle Buzzer State */
}

void toggleRelay(void) {
    /* Toggle Relay State */
}

void setLED(bool set) {
    /* Set LED State */
}

void setBuzzer(bool set) {
    /* Set Buzzer State */
}

void setRelay(bool set) {
    /* Set Relay State */
}

void delayCount(void) {
    /* Delay Function Implementation */
}

void initEPWM1(void) {
    /* PWM Initialization and Configuration */
    EPwm1Regs.TBPRD = 1250;       /* Set timer period 801 TBCLKs */
    EPwm1Regs.TBPHS.bit.TBPHS = 0x0000;        /* Phase is 0 */
    EPwm1Regs.TBCTR = 0x0000;

    /* Set Compare Values */
    EPwm1Regs.CMPA.bit.CMPA = Adc_Result_1;    /* Set compare A value */

    /* Setup Counter Mode */
    EPwm1Regs.TBCTL.bit.CTRMODE = TB_COUNT_UPDOWN; /* Count up and down */
    EPwm1Regs.TBCTL.bit.PHSEN = TB_DISABLE;        /* Disable phase loading */
    EPwm1Regs.TBCTL.bit.HSPCLKDIV = TB_DIV1;       /* Clock ratio to SYSCLKOUT */
    EPwm1Regs.TBCTL.bit.CLKDIV = TB_DIV1;

    /* Configure Action Qualifier */
    EPwm1Regs.AQCTLA.bit.CAU = AQ_SET;     /* Set PWM1A on event A, up count */
    EPwm1Regs.AQCTLA.bit.CAD = AQ_CLEAR;   /* Clear PWM1A on event A, down count */
}

void ConfigADC(void) {
    /* ADC Configuration Structure */
}

void initADC_SOC(void) {
    /* ADC Start-of-Conversion Setup */
}

```


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


#### **3. R-Y Y-B and B-R Voltage**

## Overview
This project involves analyzing electrical measurements from a system under test to evaluate voltage, current, and frequency characteristics. The collected data provides insights into the behavior and performance of the circuit.

 <p align="center">
  <img src="https://github.com/vandemataram15aug1947/Design_and_Analysis_of_3_Phase_Inverter_Using_Sinusoidal_ePWM_Modulation_Technique/blob/28f2e13306f5c16a3defe625c7269231dfe297fc/Photos/R-Y%20Y-B%20AND%20B-R%20Voltage.png" width="500">
</p>  

<p align="center"><b>Figure 1:</b> R-Y Y-B and B-R Voltage</p> 

## Key Observations
- **High-Frequency Signal:** A high-frequency signal (>35 kHz) was detected on Channel 1 and Channel 3.
- **Low-Frequency Signal:** Channel 2 recorded a frequency of **34.963 Hz**.
- **Current Analysis:** The peak-to-peak current on Channel 1 was measured at **11.5 A**, indicating significant fluctuations.
- **Voltage Levels:** Recorded voltage levels were **20.0 V** and **50.0 V**, likely corresponding to different phases or circuit components (e.g., R-Y, Y-B, B-R).

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


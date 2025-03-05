
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

Below is the main loop implementation for Open Loop Control of Three Phase Inverter:

```c
/*
 * Open_Loop_Control_of_Three_Phase_Inverter
 * Master Source File
 * Created On: 31-March-2024
 * Author: Vande
 */

/*
 * Included Files
 */
#include "driverlib.h"      /* F2837xD driverlib Include File */
#include "device.h"         /* F2837xD device Include File */
#include "math.h"           /* F2837xD math Include File */

/*
 * Defines that configure the period for each timer
 * U indicates that the number is an unsigned integer. This means the value is guaranteed to be non-negative.
 */
#define EPWM1_TIMER_TBPRD  2500U /* Period register */
#define EPWM1_CMPA         1250U
#define EPWM1_CMPB         1250U

#define EPWM2_TIMER_TBPRD  2500U /* Period register */
#define EPWM2_CMPA         1250U
#define EPWM2_CMPB         1250U

#define EPWM3_TIMER_TBPRD  2500U /* Period register */
#define EPWM3_CMPA         1250U
#define EPWM3_CMPB         1250U

/*
 * DefineS Dead Band
 */
#define DEAD_BAND            250U

/*
 * Function Prototypes
 */
void initEPWM1(void);
void initEPWM2(void);
void initEPWM3(void);
__interrupt void epwm1ISR(void);
__interrupt void epwm2ISR(void);
__interrupt void epwm3ISR(void);

/*
 * Main Loop
 */
void main(void)
{
    /*
     * Initialize device clock and peripherals
     */
    Device_init();

    /*
     * Disable pin locks and enable internal pull ups.
     */
    Device_initGPIO();

    /*
     * Initialize PIE and clear PIE registers. Disables CPU interrupts.
     */
    Interrupt_initModule();

    /*
     * Initialize the PIE vector table with pointers to the shell Interrupt Service Routines (ISR).
     */
    Interrupt_initVectorTable();

    /*
     * Assign the interrupt service routines to ePWM interrupts
     */
    Interrupt_register(INT_EPWM1, &epwm1ISR);
    Interrupt_register(INT_EPWM2, &epwm2ISR);
    Interrupt_register(INT_EPWM3, &epwm3ISR);

    /*
     * Configure GPIO0/1 , GPIO2/3 and GPIO4/5 as ePWM1A/1B, ePWM2A/2B and ePWM3A/3B pins respectively
     * PinMux for eEPWM1A & eEPWM1B
     */

    /*
     * PinMux for eEPWM2A & eEPWM2B
     */

    /*
     * PinMux for eEPWM3A & eEPWM3B
     */

    /*
     * PinMux for GPIO Output
     */
    GPIO_setPadConfig(35, GPIO_PIN_TYPE_PULLUP);
    GPIO_writePin(35, 1);
    GPIO_setPinConfig(GPIO_35_GPIO35);
    GPIO_setDirectionMode(35, GPIO_DIR_MODE_OUT);

    /*
     * Disable sync(Freeze clock to PWM as well)
     */
    SysCtl_disablePeripheral(SYSCTL_PERIPH_CLK_TBCLKSYNC);

    /*
     * Initialize ePWM modules
     */
    initEPWM1();
    initEPWM2();
    initEPWM3();

    /*
     * Enable ePWM interrupts
     */
    Interrupt_enable(INT_EPWM1);
    Interrupt_enable(INT_EPWM2);
    Interrupt_enable(INT_EPWM3);

    /*
     * Enable Global Interrupt (INTM) and real-time interrupt (DBGM)
     */
    EINT; /* Enable Global interrupt INTM */
    ERTM; /* Enable Global real-time interrupt DBGM */

    /*
     * IDLE loop. Just sit and loop forever (optional):
     */
    for(;;)
    {
        NOP;
    }
}

/*
 * epwm1ISR-ePWM1 ISR
 */
__interrupt void epwm1ISR(void)
{
    /*
     * Toggle GPIO pin
     */
    GPIO_togglePin(35);

    /*
     * Update the CMPA and CMPB values
     */

    /*
     * Clear INT flag for this timer
     */
    EPWM_clearEventTriggerInterruptFlag(EPWM1_BASE);

    /*
     * Acknowledge interrupt group
     */
    Interrupt_clearACKGroup(INTERRUPT_ACK_GROUP3);
}

/*
 * epwm2ISR-ePWM2 ISR
 */
__interrupt void epwm2ISR(void)
{
    /*
     * Update the CMPA and CMPB values
     */

    /*
     * Clear INT flag for this timer
     */
    EPWM_clearEventTriggerInterruptFlag(EPWM2_BASE);

    /*
     * Acknowledge interrupt group
     */
    Interrupt_clearACKGroup(INTERRUPT_ACK_GROUP3);
}

/*
 * epwm3ISR - ePWM 3 ISR
 */
__interrupt void epwm3ISR(void)
{
    /*
     * Update the CMPA and CMPB values
     */

    /*
     * Clear INT flag for this timer
     */
    EPWM_clearEventTriggerInterruptFlag(EPWM3_BASE);

    /*
     * Acknowledge interrupt group
     */
    Interrupt_clearACKGroup(INTERRUPT_ACK_GROUP3);
}

/*
 * Initialize initEPWM1-Configure ePWM1
 */
void initEPWM1()
{
    /*
     * Set-Up TBCLK
     */
    EPWM_setTimeBasePeriod(EPWM1_BASE, EPWM1_TIMER_TBPRD);
    EPWM_setPhaseShift(EPWM1_BASE, 0U);
    EPWM_setTimeBaseCounter(EPWM1_BASE, 0U);

    /*
     * Set Compare Values
     */

    /*
     * Set-Up Counter Mode
     */
    EPWM_setTimeBaseCounterMode(EPWM1_BASE, EPWM_COUNTER_MODE_UP_DOWN);
    EPWM_disablePhaseShiftLoad(EPWM1_BASE);

    /*
     * Set-Up ePWM1 clock pre-scaler
     */
    EPWM_setClockPrescaler(EPWM1_BASE,
                           EPWM_CLOCK_DIVIDER_1,
                           EPWM_HSCLOCK_DIVIDER_1);

    /*
     * Set-Up Shadowing or Set-Up shadow register load on ZERO
     */

    /*
     * Set Action Qualifier for ePWM1A & ePWM1B
     * Clear ePWM1A on event A, UP count
     */

    /*
     * Clear ePWM1A on event A, DOWN count
     */

    /*
     * Clear ePWM1B on event B, UP count
     */

    /*
     * Clear ePWM1B on event B, DOWN count
     */

    /*
     * Interrupt where we will change the Compare Values Select INT on Time base counter zero event,
     * Enable INT, generate INT on 3rd event
     */
    EPWM_setInterruptSource(EPWM1_BASE, EPWM_INT_TBCTR_ZERO);
    EPWM_enableInterrupt(EPWM1_BASE);
    EPWM_setInterruptEventCount(EPWM1_BASE, 1U);
}

/*
 * Initialize initEPWM2 - Configure ePWM2
 */
void initEPWM2()
{
    /*
     * Set-Up TBCLK
     */
    EPWM_setTimeBasePeriod(EPWM2_BASE, EPWM2_TIMER_TBPRD);
    EPWM_setPhaseShift(EPWM2_BASE, 0U);
    EPWM_setTimeBaseCounter(EPWM2_BASE, 0U);

    /*
     * Set Compare Values
     */

    /*
     * Set-Up Counter Mode
     */
    EPWM_setTimeBaseCounterMode(EPWM2_BASE, EPWM_COUNTER_MODE_UP_DOWN);
    EPWM_disablePhaseShiftLoad(EPWM2_BASE);

    /*
     * Set-Up ePWM2 clock pre-scaler
     */
    EPWM_setClockPrescaler(EPWM2_BASE,
                           EPWM_CLOCK_DIVIDER_1,
                           EPWM_HSCLOCK_DIVIDER_1);

    /*
     * Set-Up Shadowing or Set-Up shadow register load on ZERO
     */

    /*
     * Set Action Qualifier for ePWM2A & ePWM2B
     */

    /*
     * Interrupt where we will change the Compare Values Select INT on Time base counter zero event,
     * Enable INT, generate INT on 3rd event
     */
    EPWM_setInterruptSource(EPWM2_BASE, EPWM_INT_TBCTR_ZERO);
    EPWM_enableInterrupt(EPWM2_BASE);
    EPWM_setInterruptEventCount(EPWM2_BASE, 1U);
}

/*
 * Initialize initEPWM3 - Configure ePWM3
 */
void initEPWM3()
{
    /*
     * Set-Up TBCLK
     */
    EPWM_setTimeBasePeriod(EPWM3_BASE, EPWM3_TIMER_TBPRD);
    EPWM_setPhaseShift(EPWM3_BASE, 0U);
    EPWM_setTimeBaseCounter(EPWM3_BASE, 0U);

    /*
     * Set Compare Values
     */

    /*
     * Set-Up Counter Mode
     */
    EPWM_setTimeBaseCounterMode(EPWM3_BASE, EPWM_COUNTER_MODE_UP_DOWN);
    EPWM_disablePhaseShiftLoad(EPWM3_BASE);

    /*
     * Set-Up ePWM3 clock pre-scaler
     */
    EPWM_setClockPrescaler(EPWM3_BASE,
                           EPWM_CLOCK_DIVIDER_1,
                           EPWM_HSCLOCK_DIVIDER_1);

    /*
     * Set-Up Shadowing or Set-Up shadow register load on ZERO
     */

    /*
     * Set Action Qualifier for ePWM3A & ePWM3B
     */

    /*
     * Interrupt where we will change the Compare Values Select INT on Time base counter zero event,
     * Enable INT, generate INT on 3rd event
     */
    EPWM_setInterruptSource(EPWM3_BASE, EPWM_INT_TBCTR_ZERO);
    EPWM_enableInterrupt(EPWM3_BASE);
    EPWM_setInterruptEventCount(EPWM3_BASE, 1U);
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


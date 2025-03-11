
# Design and Analysis of 3-Phase Inverter Using Sinusoidal ePWM Modulation Technique

## Introduction
This project focuses on the design and analysis of a three-phase inverter using the Sinusoidal Pulse Width Modulation (SPWM) technique. The inverter plays a crucial role in converting DC power into three-phase AC power and is widely used in motor drives, renewable energy applications, and uninterruptible power supplies (UPS).

<p align="center">
  <img src="https://github.com/vandemataram15aug1947/Design_and_Analysis_of_3_Phase_Inverter_Using_Sinusoidal_ePWM_Modulation_Technique/blob/1828af132295c7d81358624042e5dfd2d54ef2fe/Basic%20Photos/Sine%20Compare%20with%20Triangular%20Wave.png" width="500">
</p>  

<p align="center"><b>Figure 1:</b> Sine Compare with Triangular Wave</p>  

## Sinusoidal Pulse Width Modulation (SPWM)
SPWM is the most commonly used PWM technique for controlling inverters. It generates gating signals by comparing a sinusoidal control signal with a triangular carrier waveform. The frequency of the sinusoidal control signal determines the desired inverter output frequency.

<p align="center">
  <img src="https://github.com/vandemataram15aug1947/Design_and_Analysis_of_3_Phase_Inverter_Using_Sinusoidal_ePWM_Modulation_Technique/blob/e1b2b467885e3067929d8e213f332bbdff9324c4/Basic%20Photos/Three-Phase%20Inverter%20Circuit.png" width="500">
</p>  

<p align="center"><b>Figure 2:</b> Three-Phase Inverter Circuit</p>  

### Working Principle
- When `VcontrolA > Vtri`, `S1` is ON, and `VAN = Vd`.
- When `VcontrolA < Vtri`, `S2` is ON, and `VAN = 0`.
- When `VcontrolB > Vtri`, `S3` is ON, and `VBN = Vd`.
- When `VcontrolB < Vtri`, `S4` is ON, and `VBN = 0`.
- When `VcontrolC > Vtri`, `S5` is ON, and `VCN = Vd`.
- When `VcontrolC < Vtri`, `S6` is ON, and `VCN = 0`.

<p align="center">
  <img src="https://github.com/vandemataram15aug1947/Design_and_Analysis_of_3_Phase_Inverter_Using_Sinusoidal_ePWM_Modulation_Technique/blob/e1b2b467885e3067929d8e213f332bbdff9324c4/Basic%20Photos/SPWM%20Three-Phase%20Inverter%20Waveforms.png" width="500">
</p>  

<p align="center"><b>Figure 3:</b> SPWM Three-Phase Inverter Waveforms</p>  

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

# Design of Isolated Gate Driver Circuit

## Introduction
The HCPL-3120 contains a Gallium Arsenic Phosphide (GaAsP) LED, while the HCPL-J312 and the HCNW3120 contain an AlGaAs LED. The LED is optically coupled to an integrated circuit with a power output stage. These optocouplers are ideally suited for driving power IGBTs and MOSFETs used in motor control inverter applications. The high operating voltage range of the output stage provides the drive voltages required by gate-controlled devices.

The voltage and current supplied by these optocouplers make them suitable for directly driving IGBTs with ratings up to 1200 V/100 A. For IGBTs with higher ratings, the HCPL-3120 series can be used to drive a discrete power stage that controls the IGBT gate. The HCNW3120 has the highest insulation voltage of $V_{IORM}$ = 1414 $V_{peak}$ according to IEC/EN/DIN EN 60747-5-2 standards.

## Features of HCPL-3120
- 2.5 A maximum peak output current
- 2.0 A minimum peak output current
- 25 kV/$\mu$s minimum Common Mode Rejection (CMR) at $V_{CM} = 1500$ V
- 0.5 V maximum low-level output voltage ($V_{OL}$), eliminating the need for negative gate drive
- $I_{CC} = 5$ mA maximum supply current
- Under Voltage Lock-Out protection (UVLO) with hysteresis
- Wide operating $V_{CC}$ range: 15V to 30V
- 500 ns maximum switching speeds
- Industrial temperature range: $-40^\circ$C to $100^\circ$C

## Applications Information
A three-phase inverter requires six isolated gate drivers for IGBT switch control. The HCPL-3120 is used in this design due to its opto-isolated LED input stage and current-controlled operation.

### Best Practices for HCPL-3120 Integration:
- To eliminate negative IGBT gate drive, minimize $R_g$ and lead inductance from HCPL-3120 to IGBT gate/emitter.
- Mount HCPL-3120 directly above the IGBT on a small PCB.
- Avoid routing IGBT collector/emitter traces close to the HCPL-3120 input to prevent signal coupling. If unavoidable, reverse-bias the LED in the off state to prevent unwanted activation from transient signals.

## PCB Layout of HCPL-3120
Designers must pay close attention to PCB layout to achieve optimum performance for the HCPL-3120. The position of low-ESR and low-ESL capacitors near the device is crucial for noise suppression and peak current support. Minimizing loop inductance by limiting the physical area involved in high peak current transitions at transistor gates is essential. Avoiding PCB traces or copper below the driver device preserves high-voltage isolation. Additionally, implementing a PCB layout conducive to heat dissipation, prioritizing increased copper connections to VCC and VEE pins, and employing multiple vias for thermal conductivity while ensuring no overlap between traces or copper from different high-voltage planes enhances performance.

<p align="center">
  <img src="https://github.com/vandemataram15aug1947/Design_and_Analysis_of_3_Phase_Inverter_Using_Sinusoidal_ePWM_Modulation_Technique/blob/b8c9a2c337a0522620d9f58ec537891241bb0735/Harware%20Results/Top-Layer%20Traces%20and%20Copper%20of%20HCPL-3120.png" width="500">
</p>  

<p align="center"><b>Figure 4:</b> Top-Layer Traces and Copper of HCPL-3120</p>  


<p align="center">
  <img src="https://github.com/vandemataram15aug1947/Design_and_Analysis_of_3_Phase_Inverter_Using_Sinusoidal_ePWM_Modulation_Technique/blob/b8c9a2c337a0522620d9f58ec537891241bb0735/Harware%20Results/Bottom-Layer%20Traces%20and%20Copper%20of%20HCPL-3120.png" width="500">
</p>  

<p align="center"><b>Figure 5:</b> Bottom-Layer Traces and Copper of HCPL-3120</p>  


<p align="center">
  <img src="https://github.com/vandemataram15aug1947/Design_and_Analysis_of_3_Phase_Inverter_Using_Sinusoidal_ePWM_Modulation_Technique/blob/b8c9a2c337a0522620d9f58ec537891241bb0735/Harware%20Results/3-D%20PCB%20View%20of%20HCPL-3120.png" width="500">
</p>  

<p align="center"><b>Figure 6:</b> 3-D PCB View of HCPL-3120</p>  

## PCB Material
Use a standard FR-4 UL94V-0 printed circuit board. This PCB is preferred over cheaper alternatives due to its lower dielectric losses at high frequencies, reduced moisture absorption, greater strength and stiffness, and self-extinguishing flammability characteristics.


# PCB Layout of Isolated IGBT Gate-Drive Fly-Buck Power Supply

The PCB layout of an isolated IGBT gate-drive Fly-Buck power supply involves strategic considerations to ensure optimal performance and safety. Key aspects include:

- **Isolation Boundary:** Maintaining a clear separation between the primary and secondary sides for safety and noise reduction.
- **Component Placement:** Positioning the transformer and IGBT gate driver for efficient signal paths and thermal management.
- **High-Voltage Trace Routing:** Ensuring careful routing to minimize parasitic effects and enhance system reliability.
- **Grounding Scheme:** Implementing a robust grounding strategy, including separate ground planes if necessary.
- **Safety Standards Compliance:** Adhering to clearance and creepage distance requirements.
- **EMI/EMC Considerations:** Utilizing shielding and filtering techniques to mitigate noise.
- **Thermal Management:** Implementing thermal vias and copper pours to manage heat dissipation effectively.

These factors collectively contribute to the reliability and efficiency of the power supply design.

<p align="center">
  <img src="https://github.com/vandemataram15aug1947/Design_and_Analysis_of_3_Phase_Inverter_Using_Sinusoidal_ePWM_Modulation_Technique/blob/f1168b190ff3ca423b499d784347bdb3500c5ab5/Harware%20Results/Top-Layer%20Traces%20and%20Copper%20of%20Isolated%20IGBT%20Gate-Drive%20Fly-Buck%20Power%20Supply.png" width="500">
</p>  

<p align="center"><b>Figure 7:</b> Top-Layer Traces and Copper of Isolated IGBT Gate-Drive Fly-Buck Power Supply</p>  


<p align="center">
  <img src="https://github.com/vandemataram15aug1947/Design_and_Analysis_of_3_Phase_Inverter_Using_Sinusoidal_ePWM_Modulation_Technique/blob/91240a8fe3cca4f18bac834dcd7f46aca3874d62/Harware%20Results/Bottom-Layer%20Traces%20and%20Copper%20of%20Isolated%20IGBT%20Gate-Drive%20Fly-Buck%20Power%20Supply.png" width="500">
</p>  

<p align="center"><b>Figure 8:</b> Bottom-Layer Traces and Copper of Isolated IGBT Gate-Drive Fly-Buck Power Supply</p>  


<p align="center">
  <img src="https://github.com/vandemataram15aug1947/Design_and_Analysis_of_3_Phase_Inverter_Using_Sinusoidal_ePWM_Modulation_Technique/blob/91240a8fe3cca4f18bac834dcd7f46aca3874d62/Harware%20Results/3-D%20PCB%20View%20of%20Isolated%20IGBT%20Gate-Drive%20Fly-Buck%20Power%20Supply.png" width="500">
</p>  

<p align="center"><b>Figure 9:</b> 3-D PCB View of Isolated IGBT Gate-Drive Fly-Buck Power Supply</p>  

The design featuring the **HCPL-3120 optocoupler** provides a robust solution for driving Insulated-Gate Bipolar Transistors (IGBTs) in motor control inverter applications. Key features include:

- **Power Supply Rails:** Utilization of +15 V and -8 V secondary side power.
- **Bulk Capacitors:** Ensuring gate current supply stability.
- **Noise Decoupling Capacitors:** Reducing power supply noise.
- **Gate Resistor Selection:** Optimized to enhance switching performance and minimize parasitic effects.
- **Independent Control:** Enabling precise IGBT switching functionality.
- **Stable, Low-Ripple Output:** Supporting multiple gate drivers in a half-bridge configuration.

Overall, this design effectively addresses the stringent requirements of motor control inverter systems, enhancing efficiency and performance.

# **Sinusoidal Gate Driver Pulses - Oscilloscope Waveforms**

This repository contains oscilloscope captures showcasing the **Sinusoidal Pulse Width Modulation (SPWM) pulses** generated at the **gate driver output** of a grid-connected inverter. These pulses are essential for proper inverter operation, ensing efficient power conversion and synchronization with the grid.

---

## **Waveform Analysis**

### **1. Sinusoidal Pulses of First Leg**
- **Channel 1 (Orange):** High-side gate driver output.
- **Channel 2 (Green):** Low-side gate driver output.
- **Switching Frequency:** ~10 kHz.
- **Peak-to-Peak Voltage:** ~17.3V (Low-Side) and ~18.1V (High-Side).
- **Observation:** The pulses exhibit a sinusoidal pattern with varying pulse widths, characteristic of **SPWM**.

<p align="center">
  <img src="https://github.com/vandemataram15aug1947/Design_and_Analysis_of_3_Phase_Inverter_Using_Sinusoidal_ePWM_Modulation_Technique/blob/518117f414c165d830b5fbdeba2136aaa120c36b/Harware%20Results/Complementary%20Pulse%20of%20first%20Leg.png" width="500">
</p>  

<p align="center"><b>Figure 10:</b> Complementary Pulse of First Leg</p>  

---

### **2. Sinusoidal Pulses of Second Leg**
- **Channel 1 (Orange):** High-side gate driver output.
- **Channel 2 (Green):** Low-side gate driver output.
- **Switching Frequency:** ~10 kHz.
- **Peak-to-Peak Voltage:** ~16.9V (Low-Side) and ~19.9V (High-Side).
- **Observation:** The modulated pulse width varies sinusoidally, ensuring smooth operation and **low harmonic distortion**.

<p align="center">
  <img src="https://github.com/vandemataram15aug1947/Design_and_Analysis_of_3_Phase_Inverter_Using_Sinusoidal_ePWM_Modulation_Technique/blob/518117f414c165d830b5fbdeba2136aaa120c36b/Harware%20Results/Complementary%20Pulse%20of%20Second%20Leg.png" width="500">
</p>  

<p align="center"><b>Figure 11:</b> Complementary Pulse of Second Leg</p>  


---

### **3. Sinusoidal Pulses of Third Leg**
- **Channel 1 (Orange):** High-side gate driver output.
- **Channel 2 (Green):** Low-side gate driver output.
- **Switching Frequency:** ~10 kHz.
- **Peak-to-Peak Voltage:** ~17.3V (Both High-Side and Low-Side).
- **Observation:** The pulses maintain the expected phase relationship, ensuring proper **inverter operation**.

<p align="center">
  <img src="https://github.com/vandemataram15aug1947/Design_and_Analysis_of_3_Phase_Inverter_Using_Sinusoidal_ePWM_Modulation_Technique/blob/518117f414c165d830b5fbdeba2136aaa120c36b/Harware%20Results/Complementary%20Pulse%20of%20Third%20Leg.png" width="500">
</p>  

<p align="center"><b>Figure 12:</b> Complementary Pulse of Third Leg</p>  


---

## Hardware Setup

### Figure 13: Hardware Setup Overview
This image provides a complete view of the **Three Phase Inverter**. The labeled components include:

- **Debug Through CCS**: Code Composer Studio (CCS) is used for debugging and flashing firmware onto the microcontroller.
- **LaunchPad**: Texas Instruments microcontroller development board, which controls the inverter system.
- **Driver Power Supply**: Supplies power to the gate driver circuits.
- **Driver Circuit**: Interfaces between the microcontroller and power switches.
- **Inverter Power Circuit**: The power electronics stage where the DC input is converted to AC for grid connection.
- **DSO (Digital Storage Oscilloscope)**: Used for waveform monitoring and debugging switching signals.

<p align="center">
  <img src="https://github.com/vandemataram15aug1947/Design_and_Analysis_of_3_Phase_Inverter_Using_Sinusoidal_ePWM_Modulation_Technique/blob/7734b1baa1d24e3ac16bfd42fc6c65712ce04393/Harware%20Results/Figure%20Hardware%20Setup%20I.png" width="500">
</p>  

<p align="center"><b>Figure 13:</b> Figure Hardware Setup I</p>  


---

### Figure 14: Gate Driver and Power Circuit
This image provides a closer look at the **gate driver and power circuits** of the inverter system. Key labeled components include:

- **Transformer**: Steps down or isolates voltages for the power supply.
- **Bridge Rectifier**: Converts AC voltage to DC voltage for powering the circuit.
- **Isolated IGBT Gate-Drive Fly-Buck Power Supply**: Provides isolated power to the IGBT gate drivers.
- **Driver Circuit for First, Second, and Third Leg**: These circuits drive the IGBT switches for each leg of the inverter.
- **Inverter Power Circuit**: The main inverter switching stage where power conversion occurs.

<p align="center">
  <img src="https://github.com/vandemataram15aug1947/Design_and_Analysis_of_3_Phase_Inverter_Using_Sinusoidal_ePWM_Modulation_Technique/blob/7734b1baa1d24e3ac16bfd42fc6c65712ce04393/Harware%20Results/Figure%20Hardware%20Setup%20II.png" width="500">
</p>  

<p align="center"><b>Figure 14:</b> Figure Hardware Setup II</p>  

---

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
📌 **Author**: [Vande]  
📌 **License**: GPL-3.0 lisence  
📌 **Contributions**: Open to suggestions and improvements! Feel free to submit PRs or open issues. 🚀


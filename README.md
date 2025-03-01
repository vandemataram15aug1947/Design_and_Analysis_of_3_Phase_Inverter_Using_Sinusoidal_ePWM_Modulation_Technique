# Design_and_Analysis_of_3_Phase_Inverter_Using_Sinusoidal_ePWM_Modulation_Technique


# Design and Analysis of 3-Phase Inverter Using Sinusoidal ePWM Modulation Technique

## Introduction
This project focuses on the design and analysis of a three-phase inverter using the Sinusoidal Pulse Width Modulation (SPWM) technique. The inverter plays a crucial role in converting DC power into three-phase AC power and is widely used in motor drives, renewable energy applications, and uninterruptible power supplies (UPS).

## Sinusoidal Pulse Width Modulation (SPWM)
SPWM is the most commonly used PWM technique for controlling inverters. It generates gating signals by comparing a sinusoidal control signal with a triangular carrier waveform. The frequency of the sinusoidal control signal determines the desired inverter output frequency.

### Working Principle
- When `VcontrolA > Vtri`, `S1` is ON, and `VAN = Vd`.
- When `VcontrolA < Vtri`, `S2` is ON, and `VAN = 0`.
- When `VcontrolB > Vtri`, `S3` is ON, and `VBN = Vd`.
- When `VcontrolB < Vtri`, `S4` is ON, and `VBN = 0`.
- When `VcontrolC > Vtri`, `S5` is ON, and `VCN = Vd`.
- When `VcontrolC < Vtri`, `S6` is ON, and `VCN = 0`.

### Voltage Equations
The line-to-line voltages are computed as follows:
```math
V_{AB} = V_{AN} - V_{BN}
V_{BC} = V_{BN} - V_{CN}
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

## Contributing
Feel free to contribute to this project by submitting issues or pull requests.

## License
This project is licensed under the MIT License.

## Contact
For queries, contact [Your Email] or open an issue on GitHub.

---

This README provides a clear overview of your project, including technical explanations and implementation details.


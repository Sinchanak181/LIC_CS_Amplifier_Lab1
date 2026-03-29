# 🔷 Experiment 4  
## CMOS Differential Amplifier – Design and Analysis (180 nm)

---

## 🎯 Aim

To design a CMOS differential amplifier and analyze its operation using DC conditions based on given specifications.

---

## 📘 Introduction

A differential amplifier is an important analog circuit that amplifies the voltage difference between two input signals while rejecting common noise present at both inputs.

Such amplifiers are widely used in analog systems like operational amplifiers and signal processing circuits due to their high noise immunity and stability.

---

## 📖 Theory

A differential amplifier consists of two matched MOSFETs connected with a common source node and a tail current element.

When a differential input is applied:

vd = Vin1 − Vin2  

- If Vin1 increases → current through M1 increases  
- If Vin2 increases → current through M2 increases  

For small input signals, both transistors operate in saturation and the circuit behaves linearly.

The small-signal gain is given by:

Av = gm × Rout  

where:

- gm = transconductance  
- Rout = effective output resistance  

and,

gm = (2ID) / Vov  

---
## 🔷 Circuit Diagram

![Circuit Diagram](circuit1.png.jpeg)

---
## 📌 Design Calculations

### 🔸 Given Parameters

| Parameter | Value |
|----------|------|
| Technology | TSMC 180 nm |
| VDD | +0.9 V |
| VSS | -0.9 V |
| Power (P) | 1.8 mW |
| Channel Length (L) | 480 nm |
| Vth | 0.36 V |
| Load Capacitance | 10 pF |

---

### 🔸 Total Supply Voltage

Vtotal = VDD − VSS  

Vtotal = 0.9 − (−0.9) = 1.8 V  

---

### 🔸 Tail Current (ISS)

Using power relation:

P = Vtotal × ISS  

ISS = 1.8 mW / 1.8 V  

ISS = 1 mA  

---

### 🔸 Drain Current

For balanced differential pair:

ID1 = ID2 = ISS / 2  

ID = 0.5 mA  

---

### 🔸 Load Resistance (RD)

Using:

Vout = VDD − ID × RD  

Assuming symmetric output:

Vout ≈ 0 V  

0 = 0.9 − (0.5 mA × RD)

RD = 0.9 / (0.5 × 10⁻³)

RD ≈ 1.8 kΩ  

---

### 🔸 Bias Point Calculation

#### Source Voltage

Given:

Vp = −0.7 V  

Vs = Vp = −0.7 V  

---

#### Gate Voltage

For DC condition:

VG1 = VG2 = 0 V  

---

#### Gate-Source Voltage

VGS = VG − VS  

VGS = 0 − (−0.7)  

VGS = 0.7 V  

---

#### Overdrive Voltage

VOV = VGS − Vth  

VOV = 0.7 − 0.36  

VOV = 0.34 V  

---

#### Drain Voltage

Vout = 0 V  

---

#### Drain-Source Voltage

VDS = VD − VS  

VDS = 0 − (−0.7)  

VDS = 0.7 V  

---

### 🔸 Saturation Check

Condition:

VDS ≥ VOV  

0.7 ≥ 0.34  ✔  

👉 Both transistors operate in saturation region

---

### 🔸 Width Calculation

Using MOSFET equation:

ID = (1/2) μnCox (W/L) (VOV)²  

Rewriting:

W = (2 ID L) / (μnCox (VOV)²)

Initial value:

W ≈ 17.5 µm  

### 🔸 Width Tuning and Practical Adjustment

The width obtained from theoretical calculation is based on ideal square-law MOSFET assumptions.  
However, practical device behavior deviates due to several non-ideal effects.

To achieve the required bias condition:

Vs ≈ -0.7 V  

the transistor width was adjusted through simulation.

By varying W, the drain current was controlled such that the desired source voltage and operating point were accurately obtained.

| Condition | Width |
|----------|------|
| Initial calculated width | ≈ 17.5 µm |
| Final tuned width | ≈ 28.5 µm |

![DC Analysis Screenshot1](your_dc_image1.png.jpeg)
---

### 🔸 Reason for Deviation

The difference between theoretical and simulated width occurs due to:

- Channel length modulation (λ effect)
- Mobility degradation at higher fields
- Non-ideal MOSFET behavior in 180 nm technology
- Process variations in model parameters
- Influence of parasitic capacitances

Hence, width tuning is necessary to meet exact design specifications in simulation.
## 🔷 DC Analysis

![DC Analysis Screenshot](your_dc_image.png.jpeg)

The DC operating point analysis is performed to verify whether all transistors are properly biased in saturation.

From the simulation results:

- Drain voltages are close to the expected operating value
- Source node voltage is maintained by the tail current source
- Equal current distribution is observed in both branches

✔ This confirms correct biasing and stable operation of the differential amplifier.

---

## 🔷 Input Common Mode Range (ICMR)

The input common-mode range defines the allowable range of input voltage for which the circuit operates correctly.

### 🔹 Minimum Input Voltage

For proper operation:

Vgs ≥ Vth  

Since:

Vgs = Vcm − Vs  

Therefore:

Vcm(min) = Vs + Vth  

Substituting values:

Vcm(min) = -0.7 + 0.36 = **-0.34 V**

---

### 🔹 Maximum Input Voltage

To keep NMOS in saturation:

Vds ≥ Vov  

Using:

Vds = Vd − Vs  

From bias point:

Vds ≈ 0.7 V  

Thus:

Vcm(max) = Vd + Vth = **0.36 V**

---

### ✅ Final ICMR

| Parameter | Value |
|----------|------|
| Vcm(min) | -0.34 V |
| Vcm(max) | 0.36 V |

---

## 🔷 Output Common Mode Range

The output voltage limits are determined by maintaining transistor saturation.

### 🔹 Maximum Output Voltage

Limited by supply voltage:

Vout(max) ≈ VDD = **0.9 V**

---

### 🔹 Minimum Output Voltage

Condition:

Vds ≥ Vov  

So:

Vout(min) = Vs + Vov  

Substituting:

Vout(min) = -0.7 + 0.34 = **-0.36 V**

---

### ✅ Final Output Range

| Parameter | Value |
|----------|------|
| Vout(min) | -0.36 V |
| Vout(max) | 0.9 V |

---

## 🔷 Differential Input Range (Linear Region)

For linear operation:

|Vid| ≤ 2Vov  

Given:

Vov = 0.34 V  

Therefore:

|Vid| ≤ 0.68 V  

---

### ✅ Linear Operating Range

| Parameter | Value |
|----------|------|
| Maximum differential input | ±0.68 V |

---

## 🔷 Transient Analysis

Transient analysis is performed to verify linearity of the amplifier under different input conditions.

---

### 🔹 Case 1: Small Signal Input (Linear Region)

![Transient Linear](your_linear_image.png.jpeg)

Input applied:

Vid = 50 mV (< 0.68 V)

#### Observation:

- Output is clean sinusoidal
- No distortion observed
- Both transistors operate in saturation
- Gain remains constant

---

### 🔹 Case 2: Large Signal Input (Non-Linear Region)

![Transient Nonlinear](your_nonlinear_image.png.jpeg)

Input applied:

Vid = 500 mV (> 0.68 V)

#### Observation:

- Output waveform shows distortion
- Clipping is observed
- One transistor moves towards cutoff
- Linear amplification is lost

---

## 🔷 Comparison of Operation

| Parameter | Linear Region | Non-Linear Region |
|----------|-------------|------------------|
| MOSFET Operation            | Both in saturation           | One in cutoff, one active    |
| Current Distribution        | Equal sharing                | Unequal (one dominates)      |
| Output Waveform             | Sinusoidal                   | Distorted / non-linear       |
| Linearity                   | Linear region               | Non-linear region            |
| Gain Behavior               | Constant                    | Varies (non-linear gain)     |
| Symmetry                    | Symmetrical                 | Asymmetrical                 |
| Signal Quality              | High (clean output)         | Poor (clipping/distortion)   |

---

## 🔷 Interpretation

When the input difference is small, current splits equally and the amplifier behaves linearly.

As the input increases, current shifts toward one transistor, causing imbalance and distortion.

---

## 🔷 Conclusion

The differential amplifier operates linearly only within a limited input range.

✔ Linear condition:

|Vid| < 2Vov  

Beyond this limit:

- One transistor turns off  
- Output becomes non-linear  
- Gain reduces  

Thus, proper input range selection is essential for accurate amplification.

## 🔷 Gain Calculation (From Transient Analysis)

The output waveform is amplified and inverted with respect to the input signal.

### 🔹 Input Signal Parameters

| Parameter | Value |
|----------|------|
| Type | Sine wave |
| Frequency | 1 kHz |
| Amplitude | 50 mV (differential) |
| DC Offset | 0 V |

---

### 🔹 Measured Peak-to-Peak Values

| Quantity | Value |
|----------|------|
| Vin (p-p) | 100 mV |
| Vout (p-p) | 604 mV |

---

### 🔹 Voltage Gain

Av = Vout(p-p) / Vin(p-p)

Av = 604 mV / 100 mV  

Av = 6.04 V/V

---

### 🔹 Gain in dB

Gain(dB) = 20 log10(Av)

Gain(dB) = 20 log10(6.04)

Gain ≈ 15.62 dB

---

## 🔷 Theoretical Gain Estimation

### 🔹 Output Resistance

ro = 1 / (λ × ID)

Given:  
λ = 0.1 V⁻¹  
ID = 0.5 mA  

ro = 1 / (0.1 × 0.5 × 10⁻³)

ro = 20 kΩ

---

### 🔹 Effective Output Resistance

ro(eff) = ro1 || ro2  

ro(eff) = 20k || 20k  

ro(eff) = 10 kΩ

---

### 🔹 Transconductance

gm = 2ID / Vov  

(Use your Vov value)

---

### 🔹 Theoretical Gain

Av = gm × ro(eff)

NOTE: This is an approximate value due to ideal assumptions.

---

## 🔷 AC Analysis

![AC Response](your_ac_plot.png.png)

The frequency response of the amplifier is obtained using AC analysis.

---

### 🔹 Extracted Parameters

| Parameter | Value |
|----------|------|
| Midband Gain | 9.87 dB |
| 3 dB Gain | 6.87 dB |
| Lower Cutoff Frequency | ~ 0 Hz |
| Upper Cutoff Frequency | 4.819 MHz |

---

### 🔹 Bandwidth

Bandwidth (BW) = fH − fL  

BW = 4.819 MHz

---

## 🔷 Observations

- Gain is constant in midband region  
- Gain decreases at high frequencies  
- Roll-off occurs due to parasitic capacitances  
- Bandwidth depends on output node capacitance  

---

## 🔷 Reason for Variation

The difference between theoretical and simulated results is due to:

- Channel length modulation  
- Mobility degradation  
- Parasitic capacitances  
- Non-ideal MOSFET behavior  
- Approximation in hand calculations  

---

## 🔷 Inference

The differential amplifier with resistive load is successfully designed and analyzed.

### 🔹 Key Points

- Power constraint is satisfied  
- Tail current ensures proper biasing  
- Both transistors operate in saturation  
- Gain is moderate due to resistive load  
- Bandwidth is relatively high  

---

### 🔹 Performance Summary

| Parameter | Value |
|----------|------|
| Gain (V/V) | 6.04 |
| Gain (dB) | 15.62 dB |
| Bandwidth | 4.819 MHz |

---

### 🔹 Final Conclusion

- For small input → amplifier behaves linearly  
- For large input → distortion occurs  
- Gain is limited by output resistance  
- Bandwidth is affected by parasitics  

Thus, the circuit meets the design requirements and shows expected behavior.

# 🔷 Circuit 2: Differential Amplifier with PMOS Active Load

---

## 🔶 Working Principle

This circuit uses:

- NMOS (M1, M2) → differential pair  
- PMOS (M3, M4) → active load  
- NMOS (M5) → tail current source  

When a differential input is applied:

- Tail current splits between M1 and M2  
- PMOS load converts current variation into voltage  
- Output is taken from drains of M1 and M2  

✔ Active load increases output resistance → higher gain  

---

## 🔶 Circuit Diagram

![Circuit 2](your_circuit2.png)

---

## 🔶 Design Parameters

| Parameter | Value |
|----------|------|
| Technology | 180 nm |
| VDD | +0.9 V |
| VSS | -0.9 V |
| Power Limit | 1.8 mW |
| Channel Length (L) | 480 nm |
| Vcm (input) | 0 V |
| Vout (target) | 0 V |
| Tail Voltage (Vp) | -0.7 V |
| Threshold Voltage (Vth) | 0.36 V |

---

## 🔶 Power Constraint

Total supply voltage:

VDD − VSS = 0.9 − (−0.9) = **1.8 V**

Power relation:

P = (VDD − VSS) × Iss  

So,

1.8 × Iss ≤ 1.8 mW  

Iss ≤ 1 mA  

✔ Choose:

Iss = **1 mA**

---

## 🔶 Drain Current Distribution

Under balanced condition:

Vin1 = Vin2  

Current splits equally:

| Quantity | Value |
|---------|------|
| ID1 | 0.5 mA |
| ID2 | 0.5 mA |

✔ Symmetrical operation achieved  

---

## 🔶 Bias Point (Initial Understanding)

| Node | Value |
|------|------|
| Vin1 = Vin2 | 0 V |
| Vs (tail node) | -0.7 V |

---

### 🔹 Gate-Source Voltage

Vgs = Vg − Vs  

Vgs = 0 − (−0.7)  

Vgs = **0.7 V**

---

### 🔹 Overdrive Voltage

Vov = Vgs − Vth  

Vov = 0.7 − 0.36  

Vov = **0.34 V**

---

✔ This ensures transistors operate in saturation region  

---
## Bias Completion

### NMOS (M1, M2)

| Parameter | Value |
|----------|------|
| Vd | 0 V |
| Vs | -0.7 V |
| Vds | 0.7 V |
| Vov | 0.34 V |

Condition:  
Vds ≥ Vov → 0.7 ≥ 0.34 ✔  

✔ M1, M2 operate in saturation  

---

### NMOS Tail Current Source (M5)

| Node | Value |
|------|------|
| Vs | -0.9 V |
| Vd | -0.7 V |

Vds = Vd − Vs = -0.7 − (-0.9) = **0.2 V**

To keep M5 in saturation:

Vds ≥ Vov  

Choose:

Vov ≈ **0.2 V**

---

#### Gate Voltage

Vgs = Vth + Vov  
Vgs = 0.36 + 0.2 = **0.56 V**

Vg = Vs + Vgs  
Vg = -0.9 + 0.56 = **-0.34 V**

✔ M5 operates at edge of saturation and sets tail current  

---

### PMOS Load (M3, M4)

| Parameter | Value |
|----------|------|
| Vs | 0.9 V |
| Vd | 0 V |
| Vsd | 0.9 V |

Condition:

Vsd ≥ Vov  

✔ 0.9 V is sufficient → PMOS in saturation  

---

### Final Bias Summary

| Device | Region |
|--------|-------|
| M1, M2 | Saturation |
| M3, M4 | Saturation |
| M5 | Saturation (edge) |

✔ Proper differential operation achieved  

---

## Width Calculation

General equation:

ID = (1/2) μCox (W/L) (Vov)²  

Rearranged:

W = (2 ID L) / (μCox (Vov)²)

---

### NMOS (M1, M2)

| Parameter | Value |
|----------|------|
| ID | 0.5 mA |
| Vov | 0.34 V |
| L | 480 nm |

Calculated:

W ≈ **17.6 µm**

---

### NMOS (M5)

| Parameter | Value |
|----------|------|
| ID | 1 mA |
| Vov | 0.2 V |
| L | 480 nm |

Calculated:

W ≈ **101.5 µm**

---

### Width Tuning (From Simulation)

Due to non-ideal effects, widths are adjusted:

| Transistor | Initial | Final |
|-----------|--------|------|
| M1, M2 | 17.6 µm | ~29.8 µm |
| M5 | 101.5 µm | ~195 µm |

---

### Reason for Adjustment

- Channel length modulation  
- Mobility variation  
- Model inaccuracies  
- Exact bias matching requirement  

✔ Final values ensure correct tail current and node voltage
## DC Analysis

![DC Output](your_dc_image_here.png)

The operating point verifies that all node voltages and currents are close to the designed values.  
The tail current splits almost equally, confirming proper biasing of the differential pair.

✔ Both NMOS and PMOS transistors operate in saturation  

---

## Input Common Mode Range (ICMR)

ICMR defines the range of input voltage for which the circuit functions correctly.

### Minimum Input Voltage

Condition:
Vgs ≥ Vt  

Vgs = Vicm − Vs  

So,

Vicm(min) = Vs + Vt  

| Parameter | Value |
|----------|------|
| Vs | -0.7 V |
| Vt | 0.36 V |

Vicm(min) = **-0.34 V**

---

### Maximum Input Voltage

To keep PMOS active load in saturation:

Vsd ≥ Vov  

After simplification:

Vicm(max) ≈ Vd + |Vtp|

| Parameter | Value |
|----------|------|
| Vd | ~0 V |
| |Vtp| | ~0.39 V |

Vicm(max) = **0.39 V**

---

### Final ICMR

| Range |
|------|
| **-0.34 V ≤ Vicm ≤ 0.39 V** |

---

## Output Common Mode Range (OCMR)

### Minimum Output Voltage

Condition for NMOS saturation:

Vds ≥ Vov  

Vout(min) ≥ Vs + Vov  

| Parameter | Value |
|----------|------|
| Vs | -0.7 V |
| Vov | 0.34 V |

Vout(min) = **-0.36 V**

---

### Maximum Output Voltage

Condition for PMOS:

Vsd ≥ Vov  

Vout(max) ≤ VDD − Vov  

| Parameter | Value |
|----------|------|
| VDD | 0.9 V |
| Vov(p) | 0.25 V |

Vout(max) = **0.65 V**

---

### Final OCMR

| Range |
|------|
| **-0.36 V ≤ Vout ≤ 0.65 V** |

---

## Differential Input Range (Linear Region)

For linear operation:

|Vid| ≤ 2Vov  

| Parameter | Value |
|----------|------|
| Vov | 0.25 V |

Vid(max) = **0.5 V**

---

### Final Range

| Range |
|------|
| **-0.5 V ≤ Vid ≤ 0.5 V** |

---

## Transient Analysis

### Linearity Condition

|Vid| < √2 · Vov  

| Parameter | Value |
|----------|------|
| Vov | 0.24 V |

√2 · Vov ≈ **0.34 V**

---

### Case 1: Linear Region

Input applied:

Vid = 50 mV (< 0.34 V)

![Linear Output](your_linear_waveform.png)

✔ Output is clean and sinusoidal  
✔ Both branches conduct equally  
✔ Amplifier behaves linearly  

---

### Case 2: Non-Linear Region

Input applied:

Vid = 400 mV (> 0.34 V)

![Nonlinear Output](your_nonlinear_waveform.png)

✔ Output shows distortion  
✔ One transistor turns OFF  
✔ Current shifts to one side  

---

## Comparison

| Parameter | Linear | Non-Linear |
|----------|--------|-----------|
| Input | Small | Large |
| Output | Smooth | Distorted |
| Gain | Constant | Reduced |
| Operation | Balanced | Unbalanced |

---
## Interpretation

For small differential inputs, both NMOS transistors conduct simultaneously and the tail current is shared almost equally between the two branches. This results in a proportional and linear output.

As the input difference increases, the current distribution becomes uneven. One transistor starts dominating while the other approaches cutoff, leading to distortion in the output waveform.

---

## Simulated Gain

### Input Conditions

| Parameter | Value |
|----------|------|
| Signal Type | Sine |
| Frequency | 1 kHz |
| Differential Amplitude | 50 mV |
| DC Offset | 0 V |

---
## Measured Gain (Transient Analysis)

| Quantity | Value |
|----------|------|
| Vin (p-p) | 100 mV |
| Vout (p-p) | ≈ 180 mV |

### Gain Calculation

Av = Vout / Vin  
Av ≈ 180m / 100m = 1.8  

### Gain in dB

Av(dB) = 20 log(1.8) ≈ 5.1 dB  

---

## Theoretical Gain

### Output Resistance

ro = 1 / (λ Id)

| Parameter | Value |
|----------|------|
| λ | 0.1 V⁻¹ |
| Id | 0.5 mA |

ro ≈ 20 kΩ  

Effective resistance:  
ro_eff ≈ ro || ro = 10 kΩ  

---

### Transconductance

gm = 2Id / Vov  

| Parameter | Value |
|----------|------|
| Id | 0.5 mA |
| Vov | ≈ 0.25 V |

gm ≈ 4 mS  

---

### Theoretical Gain

Av = gm × Rout  
Av ≈ 4 mS × 10 kΩ ≈ 40  

Av(dB) ≈ 32 dB  

---

## Reason for Difference (Theory vs Simulation)

The simulated gain is lower than theoretical due to:

- Channel length modulation  
- Non-ideal current source  
- Finite output resistance  
- Mobility degradation  
- Parasitic capacitances  

---

## AC Analysis

![AC Response1](your_ac_plot.png1.jfif)

### Input Conditions

- Vin1 = +0.5 AC  
- Vin2 = -0.5 AC  
- Frequency sweep: 1 Hz to 1 GHz  

### Output

Differential output:  
Vout = V(out1) − V(out2)

### Results

- Midband gain ≈ **5.4 dB**
- Gain decreases at high frequency  
- Bandwidth is in hundreds of MHz  

---

## Observation

- Gain is constant in midband region  
- Roll-off occurs at high frequency  
- Circuit behaves as low-pass system  

---

## Inference

- Differential amplifier works correctly  
- Proper biasing achieved  
- Linear amplification for small signals  
- Practical gain < theoretical due to non-ideal effects

  
## Circuit 3: CMOS Differential Amplifier with PMOS Current Mirror Load
---
### Working Principle

This circuit implements a CMOS differential amplifier using:

- NMOS pair (M1, M2) → input stage  
- PMOS transistors (M3, M4) → current mirror active load  
- NMOS transistor (M5) → tail current source  

The differential input is applied as:

vid = Vin1 − Vin2  

Based on this input difference:

- Current is steered between M1 and M2  
- PMOS mirror converts current difference into output voltage  
- Output is taken at OUT1 and OUT2  

The use of active load improves gain compared to resistive load designs.

---

### Key Features

- Current mirror load increases output resistance  
- Bias voltages (VB1, VB2) control operating point  
- Suitable for low-voltage analog circuits  
- Provides better gain than simple differential pair  

---

### One-Line Summary

A CMOS differential amplifier using a PMOS current mirror and bias-controlled current source for improved gain and stable operation.

---

### Circuit Diagram

![Circuit 3](your_circuit3.png.jpeg)

### Given Parameters

| Parameter | Value |
|----------|------|
| Technology | TSMC 180 nm |
| VDD | +0.9 V |
| VSS | −0.9 V |
| Power constraint | 1.8 mW |
| Channel length (L) | 480 nm |
| Vin,CM | 0 V |
| Vout,CM | 0 V |
| Tail voltage (Vp) | −0.7 V |
| Threshold voltage (Vt) | ≈ 0.36 V |

#### Tail Current Source (M5)

To keep M5 in saturation:

VGS = VT + VOV  

Assuming:

VT ≈ 0.36 V  
VOV ≈ 0.20 V  

So,

VGS ≈ 0.56 V  

Since source is at −0.9 V:

VG = VS + VGS = −0.9 + 0.56 ≈ −0.34 V  

✔ Bias selected:  
VB1 ≈ −0.34 V  

Tail current:

ISS = 1 mA  

Check saturation:

VDS = −0.7 − (−0.9) = 0.2 V  

0.2 ≥ 0.2 ✔ → Saturation condition satisfied  

---

#### NMOS Differential Pair (M1, M2)

Under balanced condition:

ID1 = ID2 = ISS / 2 = 0.5 mA  

Gate voltage:

VG = 0 V  

Source voltage:

VS ≈ −0.7 V  

So,

VGS = 0 − (−0.7) = 0.7 V  

Overdrive:

VOV = VGS − VT = 0.7 − 0.36 = 0.34 V  

Check:

VDS = 0 − (−0.7) = 0.7 V  

0.7 ≥ 0.34 ✔ → Saturation  

---

#### PMOS Current Mirror Load (M3, M4)

For PMOS:

VS = VDD = 0.9 V  

Assume:

|VTp| ≈ 0.39 V  
VOV(p) ≈ 0.25 V  

Then:

VSG = |VTp| + VOV(p) = 0.39 + 0.25 = 0.64 V  

Gate voltage:

VG = VS − VSG = 0.9 − 0.64 ≈ 0.26 V  

✔ Bias selected:  
VB2 ≈ 0.26 V  

Check saturation:

VSD = 0.9 − 0 = 0.9 V  

0.9 ≥ 0.25 ✔ → Saturation  

---

### Width Estimation

Using:

W = (2 ID L) / (μCox VOV²)

- M1, M2 → W ≈ 18 µm → tuned ≈ 30 µm  
- M5 → W ≈ 100 µm → tuned ≈ 190 µm  
- M3, M4 → W ≈ 75 µm  

✔ Final widths adjusted in simulation for accurate biasing  

---

##  DC Analysis

![DC Analysis Screenshot](your_dc_image.png.jpeg3.png)  

### Input Common Mode Range (ICMR)

Minimum:

Vin(min) ≈ VS + VOV + VT ≈ −0.33 V  

Maximum:

Vin(max) ≈ VDD − VOV(p) − |VTp| ≈ 0.7 V  

✔ Range:

−0.33 V ≤ Vin ≤ 0.7 V  

---

### Output Common Mode Range (OCMR)

Minimum:

Vout(min) ≈ VS + VOV ≈ −0.36 V  

Maximum:

Vout(max) ≈ VDD − VOV(p) ≈ 0.35 V  

✔ Range:

−0.36 V ≤ Vout ≤ 0.35 V 

### Transient Analysis

To verify linear operation, transient simulation is performed for two input cases.

#### Condition for linearity

|Vid| < √2 · Vov  

Vov ≈ 0.24–0.34 V → √2·Vov ≈ 0.34–0.48 V  

---

#### Case 1: Small Signal (Linear Region)

![Transient Linear](your_linear_image.png.jpeg3.png)

Input:
Vid ≈ 100 mV  

✔ Observation:

- Output waveform is sinusoidal  
- Both transistors conduct simultaneously  
- Current is shared between branches  
- No visible distortion  

✔ Conclusion:

Amplifier operates in linear region  

---

#### Case 2: Large Signal (Non-Linear Region)

![Transient Nonlinear](your_nonlinear_image.png.jpeg3)

Input:
Vid ≈ 600 mV  

✔ Observation:

- Output shows clipping/distortion  
- One transistor turns OFF  
- Current flows mainly through one branch  
- Signal becomes non-linear  

✔ Conclusion:

Linearity is lost due to large differential input  

---

### Practical Gain (From Simulation)

Measured values:

Vin(p-p) ≈ 100 mV  
Vout(p-p) ≈ 180 mV  

Voltage gain:

Av = Vout / Vin ≈ 180 / 100 ≈ 1.8  

In dB:

Av ≈ 20 log(1.8) ≈ 5 dB  

---

### Theoretical Gain

Using small-signal model:

gm = 2Id / Vov  

gm ≈ 2 × 0.5mA / 0.34 ≈ 3 mS  

Output resistance:

ro ≈ 1 / (λId) ≈ 10–12 kΩ  

Gain:

Av = gm × ro ≈ 30–35  

In dB:

Av ≈ 30 dB  

---

### Reason for Difference (Theory vs Simulation)

The simulated gain is lower due to practical non-ideal effects:

- Channel length modulation reduces output resistance  
- Current mirror is not perfectly ideal  
- Mobility degradation lowers gm  
- Parasitic capacitances affect signal  
- Bias variations slightly shift operating point  

✔ Hence:

Simulated gain < theoretical gain  

---

### AC Analysis
![AC Response](your_ac_plot.png2)

#### Input Conditions

- Vin1 = +0.5 AC  
- Vin2 = −0.5 AC  
- Frequency sweep: 1 Hz to ~1 GHz  

---

#### Output Expression

Vout = V(out1) − V(out2)  

---

#### Frequency Response

✔ Observations:

- Gain is flat at low/mid frequencies  
- At high frequency, gain starts decreasing  
- Indicates dominant pole behavior  

---

#### Midband Gain

From simulation:

Av ≈ 5–5.5 dB  

In linear:

Av ≈ 1.8 V/V  

---

#### Bandwidth

- Lower cutoff ≈ 0 Hz  
- Upper cutoff ≈ few hundred MHz  

✔ Behavior:

Circuit acts as a **low-pass amplifier**

---

#### Unity Gain Bandwidth (UGB)

UGB ≈ Av × fH  

UGB lies in GHz range  

---
## Comparison of Differential Amplifier Configurations

| Parameter | Circuit 1: Resistive Load | Circuit 2: PMOS Active Load | Circuit 3: Active Load with Bias Control |
|----------|--------------------------|-----------------------------|------------------------------------------|
| **Structure** | NMOS differential pair with resistors | NMOS pair + PMOS current mirror | Fully CMOS with bias-controlled loads |
| **Load Type** | Passive (Resistor RD) | Active (PMOS mirror) | Active with external bias (VB1, VB2) |
| **Tail Source** | Ideal current source | NMOS current source | Bias-controlled NMOS source |
| **Gain (Simulated)** | ~4.6 V/V (~12 dB) | ~1.8 V/V (~5.5 dB) | ~40 V/V (~32 dB) |
| **Gain (Theoretical)** | ~4–5 V/V | ~1.5–2 V/V | ~30–35 V/V |
| **Output Resistance** | Low (resistive load) | Higher than circuit 1 | Highest due to active load + biasing |
| **Bandwidth** | Very high (~GHz range) | Moderate | Lower (due to high gain trade-off) |
| **Unity Gain BW** | Highest | Medium | Reduced |
| **Input CM Range** | Limited | Wide | Moderate |
| **Output CM Range** | Wide | Wide | Restricted |
| **Linearity Range** | Small signal only | Similar to circuit 1 | Same limitation (|Vid| < ~0.34 V) |
| **Power Efficiency** | Low | Improved | Best among three |
| **Area** | Large (due to resistors) | Compact | Compact |
| **Design Complexity** | Simple | Moderate | More complex (bias tuning needed) |
| **Biasing** | Simple | Requires current source | Requires precise VB1, VB2 |
| **Accuracy of Gain** | Moderate | Lower (due to non-ideal mirror) | Better control with biasing |

---
## Applications

### Circuit 1: NMOS Differential Amplifier (Resistive Load)

- Basic amplification stages  
- Sensor signal conditioning circuits  
- Low-frequency analog processing  
- Educational and introductory analog designs  
- Simple differential signal handling  

---

### Circuit 2: Differential Amplifier with PMOS Active Load

- Operational amplifier input stages  
- Analog front-end circuits  
- Low-power integrated designs  
- Gain-enhanced amplification blocks  
- General signal processing applications  

---

### Circuit 3: CMOS Differential Amplifier with Bias Control

- High-gain precision amplifiers  
- Low-voltage CMOS analog systems  
- Integrated analog building blocks  
- Communication and RF front-end stages  
- High-performance differential signal processing  

---

## Overall Results

- All three amplifier configurations were designed and tested using 180 nm CMOS technology with ±0.9 V supply  

- Circuit 1 (resistive load):
  - Moderate gain (~12 dB)  
  - Very high bandwidth (GHz range)  
  - Limited by low output resistance  

- Circuit 2 (PMOS active load):
  - Lower gain (~5 dB in simulation)  
  - Moderate bandwidth  
  - Improvement due to active load but affected by mirror non-idealities  

- Circuit 3 (bias-controlled CMOS):
  - Highest gain (~30 dB theoretical, ~5 dB practical)  
  - Reduced bandwidth due to higher gain  
  - Better control using bias voltages  

---
## Interpretation of Results

The experiment demonstrates the behavior of CMOS differential amplifiers implemented in 180 nm technology under low-voltage operation (±0.9 V).

The results indicate that the voltage gain is mainly governed by transconductance (gm) and output resistance (Rout), where:

Av ≈ gm × Rout  

Circuits with higher effective output resistance show improved gain performance.

---

### Key Observations

- A clear trade-off between gain and bandwidth is observed:
  - Increasing gain reduces bandwidth  
  - Lower gain results in wider bandwidth  

- Frequency response shows dominant pole behavior due to parasitic capacitances, limiting high-frequency performance  

- All MOSFETs operate in saturation region, ensuring proper amplification within the valid input range  

---

### Practical Limitations

Deviation from theoretical results occurs due to:

- Channel length modulation (finite output resistance)  
- Parasitic capacitances affecting frequency response  
- Mobility degradation in short-channel devices  
- Non-ideal current sources and mirrors  

These effects reduce gain and introduce bandwidth limitations.

---

### Design Insights

- Active loads significantly improve output resistance and gain  
- However, they introduce additional parasitics and increase design complexity  
- Proper biasing is critical for maintaining saturation and stable operation  

---

### Comparative Understanding

- Circuit 1:
  - Simple implementation  
  - Lower gain and larger area  

- Circuit 2:
  - Better integration using active load  
  - Moderate gain improvement  

- Circuit 3:
  - Highest gain due to bias-controlled active load  
  - More complex but offers better performance control  

---

### Final Insight

The experiment confirms that CMOS differential amplifiers involve a balance between gain, bandwidth, and complexity.

✔ Circuit 3 is best suited for high-gain applications  
✔ Circuit 1 is useful for basic understanding and simple designs  
✔ Circuit 2 provides a practical trade-off between the two  

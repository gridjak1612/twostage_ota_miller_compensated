# Two-Stage Miller-Compensated Op-Amp Design

This repository contains detailed design notes, derivations, and circuit analysis for a classic **Two-Stage Operational Amplifier** using Miller Compensation. The documentation covers the transition from single-stage topologies to stable, high-gain two-stage architectures suitable for analog IC design.


## 📝 Overview

Single-stage op-amps often struggle to provide both high gain and large output swing simultaneously. This project explores the **Two-Stage Op-Amp**, which cascades a differential input stage with a common-source second stage to decouple gain requirements from output swing. The design focuses heavily on frequency compensation (Miller effect) to ensure closed-loop stability.

## 🧠 Key Concepts Covered

### 1. Topology Comparison
* **Single-Stage:** MODELED as a transconductor ($G_{m1}$) driving a load. Limited DC gain ($A_0 = G_{m1}/G_{o1}$).
* **Two-Stage:** Combination of a differential transconductor feeding a second transconductor ($G_{m2}$). High DC gain ($A_0 \approx G_{m1} R_{o1} \cdot G_{m2} R_{o2}$).

### 2. Miller Compensation & Pole Splitting
Standard two-stage amps are inherently unstable due to two dominant poles. The notes detail the use of a **Miller Capacitor ($C_c$)** to perform pole splitting:
* **Dominant Pole ($p_1$):** Pushed to a lower frequency (Miller effect), setting the dominant bandwidth.
* **Non-Dominant Pole ($p_2$):** Pushed to a higher frequency, typically beyond the Unity Gain Bandwidth (UGB), improving Phase Margin.

### 3. Circuit Implementation
* **1st Stage:** PMOS/NMOS Differential Pair with active load (High gain, differential to single-ended conversion).
* **2nd Stage:** Common Source Amplifier (High swing).
* **Feedback:** Compensation capacitor ($C_c$) placed between the output and input of the 2nd stage.


## 📐 Design Equations

The documentation derives specific design equations used for sizing components:

| Parameter | Formula (Approx) | Description |
| :--- | :--- | :--- |
| **DC Gain** | $A_0 = \frac{G_{m1}}{G_{o1}} \cdot \frac{G_{m2}}{G_{o2}}$ | Total open-loop gain. |
| **Dominant Pole** | $p_1 \approx \frac{-G_{o1}}{A_{v2} C_c}$ | Due to Miller effect on $C_c$. |
| **Second Pole** | $p_2 \approx \frac{-G_{m2}}{C_L}$ | Located at output node (moved to high freq). |
| **GBW (UGB)** | $\omega_{u} \approx \frac{G_{m1}}{C_c}$ | Gain-Bandwidth Product. |
| **RHP Zero** | $z_1 = \frac{G_{m2}}{C_c}$ | Right-Half Plane zero introduced by feedforward path. |

## 🔎 Stability Analysis

* **Open Loop vs. Closed Loop:** Analysis of the transfer function $A(s)$ and Loop Gain $L(s)$.
* **Phase Margin:** The design ensures that the second pole ($p_2$) is located sufficiently beyond the Unity Gain Bandwidth ($\omega_u$) to maintain stability (typically $>45^\circ$ or $60^\circ$ margin).

## 🛠️ Practical Considerations

The notes also address non-ideal effects found in physical silicon implementation:
* **Output Swing:** Decoupling the swing from the input common-mode range.
* **Power vs. Gain Trade-off:** How 2-stage topologies allow for high gain without excessive power consumption compared to single-stage equivalents.
* **Noise & Offset:** Basic analysis of input-referred noise and systematic offset minimization.

## 📚 References
* Analog CMOS Integrated Circuits (Razavi / Gray & Meyer topologies).


---
*This repository serves as a reference for analog circuit designers and students studying frequency compensation techniques in CMOS amplifiers.*

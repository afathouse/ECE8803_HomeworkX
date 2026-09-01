# 915 MHz Paper Clip RFID Tag Antenna Design & Characterization

An ultra-low-cost, passive UHF RFID tag antenna engineered using a folded paperclip geometry and custom PCB feed matching[cite: 2]. The design operates at **915 MHz**, utilizing the paperclip structure as both the radiating element and an integrated inductive matching loop to conjugate-match the capacitive complex impedance of the **NXP G2iM RFID IC**

The project encompasses full-wave 3D electromagnetic simulations in **Ansys HFSS**, custom PCB fabrication on **Isola FR408HR**, and experimental validation in an **RFID testing anechoic chamber** across varying dielectric loading conditions.

---

##  Key Highlights & Specs

* **Operating Frequency:** 915 MHz (North American UHF RFID band)
* **Target RFID IC:** NXP UCODE G2iM (Pin 1 RFP / Pin 3 RFN differential feed)
* **Substrate Material:** Isola FR408HR ($\epsilon_r = 3.69$)
* **Dielectric Loading Tests:** 0, 4, 8, and 16 sheets of standard office paper ($\epsilon_r = 2.8$, 0.1 mm/sheet)
* **Measured Read Range:** Up to **2.76 m** in experimental chamber testing
* **Tools Used:** Ansys HFSS, MATLAB, Vector RFID Anechoic Test Chamber

---

##  System Architecture & Impedance Matching

### 1. Folded Wire Radiator & Inductive Match
* **Electrical Length:** Folding the paperclip wire increases the effective electrical length within a compact physical footprint, lowering its natural resonance toward 915 MHz.
* **Inductive Reactance Cancellation:** The NXP G2iM IC exhibits a highly capacitive complex input impedance. The crossed-wire geometry situated above the PCB pads acts as an integrated inductive loop, neutralizing the capacitive reactance ($-\text{j}X_C$) to achieve conjugate impedance matching.

### 2. Differential Microstrip Feed
* Symmetrical differential microstrip traces extend directly from IC Pin 1 and Pin 3.
* The trace dimensions were optimized to match the real part of the IC input impedance.

---

##  Electromagnetic Simulation (Ansys HFSS)

The physical geometry was parameterized in Ansys HFSS using a 0.25 mm radius swept wire on an Isola FR408HR substrate. Dielectric loading was evaluated by inserting parameterized dielectric blocks ($\epsilon_r = 2.8$) into the 2 mm gap between the crossing arms.

### Simulated Results vs. Paper Loading

| Paper Load | Substrate / Gap Model | Peak Antenna Gain ($G_t$) | Resonant Return Loss ($S_{11}$) | Theoretical Link Read Range ($P_T = 1\text{ W}$) |
| :--- | :--- | :--- | :--- | :--- |
| **0 Sheets** | Direct short circuit | -0.67 dBi | Poor resonance (shorted) | N/A |
| **4 Sheets** | 0.4 mm dielectric box | **+0.63 dBi** | **<-35 dB @ 915 MHz** | **22.24 m** |
| **8 Sheets** | 0.8 mm dielectric box | -0.03 dBi | <-33 dB @ ~905 MHz | 20.61 m |
| **16 Sheets** | 1.6 mm dielectric box | -4.96 dBi | <-42 dB @ ~880 MHz | 11.69 m |

> **Dielectric Loading Effect:** Increasing paper sheets introduces a dielectric medium into the high near-field region between the wire arms, raising effective permittivity ($\epsilon_{\text{eff}}$), reducing local wave velocity, and causing a predictable downward shift in resonant frequency.

---

##  Experimental Validation & Anechoic Chamber Testing

Physical prototypes were fabricated, soldered to custom PCB test coupons, and evaluated inside an RFID testing chamber across 820 MHz – 1000 MHz.

### Measured vs. Simulated Performance (at 915 MHz Resonance)

| Configuration | Simulated Gain | Back-Calculated Gain (Exp.)* | Simulated Read Range | Measured Read Range (Exp.)* |
| :--- | :--- | :--- | :--- | :--- |
| **0 Sheets** | -0.67 dBi | -23.5 dBi | — | 2.196 m |
| **4 Sheets** | **+0.63 dBi** | **-21.20 dBi** | **22.24 m** | **2.506 m** |
| **8 Sheets** | -0.03 dBi | -21.45 dBi | 20.61 m | 2.305 m |
| **16 Sheets** | -4.96 dBi | -20.65 dBi | 11.69 m | **2.762 m** |

*\*Peak measured values across the operational sweep band.*

---

##  Engineering Analysis & Discrepancy Breakdown

The variance between simulated predictions and chamber measurements was analyzed across five primary engineering factors:

1. **Transmit Power Variations:** Theoretical calculations assumed an ideal $P_T = 1\text{ W}$ (30 dBm), whereas chamber transmitter output ranged from 26.0 dBm to 27.7 dBm during execution.
2. **Back-Calculation Assumptions:** Experimental antenna gain was back-calculated from Power on Tag Reverse ($\text{POTR}$) assuming an ideal differential reflection coefficient ($\Delta\Gamma = 1$). Hand-soldered impedance mismatches directly reduced backscatter power, reflecting mathematically as degraded gain.
3. **Fabrication Tolerances:** Hand-bent paper clips introduced minor deviations in the loop gap height and overall wire length relative to the idealized HFSS CAD model.
4. **Dielectric Boundary Inhomogeneity:** Microscopic air gaps and ambient humidity between paper sheets resulted in non-uniform permittivity compared to the idealized isotropic box ($\epsilon_r = 2.8$).
5. **Chamber Link Budget Penalties:** Polarization tilt and propagation path loss factors ($X, B, F$) were set to unity in the analytical model but naturally existed in experimental testing.

---

##  Contributors

* **Tiancheng Liu**
* **Nicholas Lai**
* **Mit Patel**

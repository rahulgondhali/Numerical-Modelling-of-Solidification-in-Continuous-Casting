# Numerical-Modelling-of-Solidification-in-Continuous-Casting
Numerical Modelling of Solidification in Continuous Casting
# 2D Continuous Casting Solidification & Thermal Simulation

A 2D finite-difference thermal model simulating the solidification and temperature evolution of a continuous casting steel billet using an **Alternating Direction Implicit (ADI)** scheme with the **Tri-Diagonal Matrix Algorithm (TDMA)**.

---

## 📌 Project Overview

During continuous casting, liquid steel solidifies as heat is extracted through the mould walls. This repository contains a numerical model that tracks:
- **Nonlinear temperature-dependent thermal properties** (conductivity $K$, specific heat $C_p$, latent heat release).
- **Transient heat flux** along the billet–mould interface.
- **Corner air-gap effects** (reduced heat transfer coefficients near billet corners).
- **Solid shell growth/thickness evolution** over casting residence time.

---

## ⚙️ Model Specifications & Parameters

| Parameter | Value / Equation | Unit |
| :--- | :--- | :--- |
| **Billet Dimensions** | $130 \times 130$ | mm |
| **Effective Mould Length** | $830 - 115 = 715$ | mm |
| **Casting Speed** | $2.0$ | m/min |
| **Carbon Content** | $0.42$ | wt% |
| **Superheat** | $30$ | °C |
| **Grid Resolution** | $100 \times 100$ nodes ($\Delta x = \Delta y \approx 1.313\text{ mm}$) | — |
| **Time Step ($\Delta t$)** | $0.01$ | s |
| **Mould Heat Flux ($Q$)** | $Q = 2680 - 335\sqrt{t}$ | $\text{kW/m}^2$ |

---

## 🧮 Numerical Methodology

1. **ADI Scheme (Alternating Direction Implicit):**
   - **Pass 1 (Vertical Implicit):** Implicit in the $y$-direction, explicit in $x$. Solved using TDMA.
   - **Pass 2 (Horizontal Implicit):** Implicit in the $x$-direction, explicit in $y$. Solved using TDMA.
2. **Harmonic Mean Conductivity:** Ensures energy conservation at interfaces between adjacent nodes:
   $$K_{\text{interface}} = \frac{2 K_i K_{i+1}}{K_i + K_{i+1}}$$
3. **Corner Air Gap Modeling:** The outer $10\%$ margin on each face applies a reduced heat transfer coefficient ($h_{\text{corner}} = 0.7 \times h_{\text{effective}}$) to simulate corner shrinkage and gap formation.
4. **Shell Thickness Tracking:** Evaluated at the mid-plane using both discrete grid-node evaluation and linear sub-grid interpolation at the solidus temperature ($T_{\text{sol}}$).

---

## 📊 Sample Simulation Results

For a $130 \text{ mm}$ billet with $0.42\text{ wt}\% \text{ C}$ at the end of mould dwell time:

* **Center Face Surface Temp:** $\approx 1179.4\ ^\circ\text{C}$
* **Corner Temp:** $\approx 963.7\ ^\circ\text{C}$
* **Core Center Temp:** $\approx 1512.1\ ^\circ\text{C}$
* **Solid Shell Thickness (Mould Exit):** $\approx 6.57\text{ mm}$ (Discrete) / $\approx 7.84\text{ mm}$ (Interpolated)

---

## 🚀 Getting Started

### Prerequisites

* Python 3.8+
* `numpy`
* `matplotlib`

Install dependencies via pip:
```bash
pip install numpy matplotlib

# Shell-and-Tube Heat Exchanger Design & Optimization Engine

A Python-based engineering tool developed to automate the sizing, rating, and mechanical configuration optimization of industrial Shell-and-Tube Heat Exchangers. This engine bridges core transport phenomena (Fluid Mechanics & Heat Transfer) with programmatic optimization loops to replace manual, error-prone calculations.

The script models a **Gasoline (Shell Side / Hot Fluid)** to **Kerosene (Tube Side / Cold Fluid)** industrial heat exchange system.

## 🚀 Key Programmatic Features

- **Automated Layout Optimization Loop:** Employs a dynamic while-loop that automatically tests structural variations (Tube Passes \(n_p\), Tube Length \(L_t\)) until it satisfies physical engineering constraints—specifically targeting fully turbulent tube-side flow (Re > 10,000).
- **Caloric Temperature Adjustments:** Avoids basic arithmetic mean calculations by dynamically evaluating caloric fluid temperatures via \(F_c\) parameters to account for temperature-dependent fluid property shifts.
- **Comprehensive Fluid Mechanics & Pressure Drop Suite:** Computes precise internal tube frictional drop, channel return losses, and shell-side fluid restrictions to ensure structural configurations do not violate maximum operating thresholds.
- **Design Margin Analytics:** Quantifies safety factors by continuously evaluating both **Percentage Oversurface** and **Percentage Overdesign** based on actual manufactured tube counts versus raw theoretical surfaces.

## 📊 Design Parameter Profile (Gasoline / Kerosene Case)

| Parameter | Shell Side (Hot Fluid - Gasoline) | Tube Side (Cold Fluid - Kerosene) |
| :--- | :--- | :--- |
| **Inlet / Outlet Temp** | 160°F → 120°F | 75°F → 120°F |
| **Viscosity (μ)** | 0.484 cP | 3.872 cP |
| **Fouling Factor (\(R_d\))** | 0.0005 hr⋅ft²⋅°F/Btu | 0.0010 hr⋅ft²⋅°F/Btu |
| **Max Allowable Δ P** | 7.0 psi | 10.0 psi |

## 🛠️ Tech Stack

- **Python 3.x** — Core logical framework and runtime environment.
- **NumPy** — Vectorized data handling, log-mean transformations, and optimization math.
- **Pandas** — Tabular transformation and structured serialization of final engineering metrics into printable reports.

## ⚙️ Mathematical Methodology & Correlations Implemented

### 1. Thermal Ratings & LMTD Correction
The script solves steady-state energy balances across the system to compute the total heat duty (Q):
\[Q = \dot{m}_c C_{p,c} (t_2 - t_1)\]

Sizing is calculated using the Log-Mean Temperature Difference method adjusted by multi-pass configuration factor (\(F_t\)):
\[Q = U_{assumed} \cdot A \cdot \Delta T_{lm} \cdot F_t\]

### 2. Film Coefficients (Colburn j-Factor Method)
Instead of generalized assumptions, the script evaluates convective heat transfer coefficients using the Colburn analogy:
\[h = \left(j_H \cdot \frac{k}{D}\right) \cdot \left(\frac{C_p \cdot \mu}{k}\right)^{1/3}\]

### 3. Total Resistance Pipeline
The design computes the final actual Overall Heat Transfer Coefficient (\(U_o\)) across the complete fouling and conductive boundaries:
\[\frac{1}{U_o} = \frac{1}{h_o} + R_{dg} + \left[\frac{d_o - d_i}{2k_w}\right]\left(\frac{d_o}{d_i}\right) + R_{dk}\left(\frac{d_o}{d_i}\right) + \frac{1}{h_i}\left(\frac{d_o}{d_i}\right)\]


=======================================================
              Design Calculation Summary 
=======================================================
                         Parameter        Value           Unit
          Caloric Temp (Hot Fluid)     138.2000             °F
         Caloric Temp (Cold Fluid)      95.4750             °F
                     Heat Load (Q) 3240000.0000          Btu/h
            Mass Flowrate Gasoline  142105.2632           lb/h
                              LMTD      42.4509             °F
            Correction Factor (Ft)       0.8024              -
            Heat Transfer Area (A)    2113.8468          sq ft
 Total Tube Pressure Drop (delP_T)       6.4797            psi
Total Shell Pressure Drop (delP_S)       1.3591            psi
              Percent Over Surface      10.7421              %
                Percent Overdesign       8.9466              %
```

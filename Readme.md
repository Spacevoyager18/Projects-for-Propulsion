# 🚀 Projects for Propulsion

[![Python 3.12+](https://img.shields.io/badge/Python-3.12%2B-3776AB?logo=python&logoColor=white)](https://www.python.org/)
[![Ansys Fluent & Mechanical](https://img.shields.io/badge/Ansys-Fluent%20%7C%20Mechanical-FFB71B?logo=ansys&logoColor=black)](https://www.ansys.com/)
[![GasTurb](https://img.shields.io/badge/Cycle%20Analysis-GasTurb-00599C)](#2-rolls-royce-ae3007a-turbofan-cycle-analysis)
[![CAD](https://img.shields.io/badge/CAD-Autodesk%20Fusion-0696D7?logo=autodesk&logoColor=white)](#1-bemt-propeller-design--aero-structural-optimization)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

A collection of computational propulsion engineering workflows, numerical solvers, and multidisciplinary design studies spanning **rotary-wing aerodynamics**, **gas turbine thermodynamic cycle modeling**, and **supersonic rocket nozzle CFD**.

This repository bridges theoretical propulsion mechanics with executable Python scripts and commercial CAE setups (**GasTurb**, **Ansys Fluent**, **Ansys Mechanical**, and **Autodesk Fusion**).

---

## 📌 Featured Projects

| Module | Focus Area | Primary Tools | Key Deliverables |
| :--- | :--- | :--- | :--- |
| **[01. BEMT Propeller Optimization](#1-bemt-propeller-design--aero-structural-optimization)** | Coupled Aero-Structural Rotor Sizing | Python, Autodesk Fusion, Ansys Mechanical | 10-station BEMT solver, chord/twist optimizer, aero-centrifugal FEA |
| **[02. RR AE3007A Cycle Analysis](#2-rolls-royce-ae3007a-turbofan-cycle-analysis)** | Gas Turbine Off-Design & Architecture Trade | GasTurb, Python (Post-Processing) | FAA TCDS baseline validation, mixed-flow/geared turbofan carpet plots |
| **[03. Supersonic Nozzle & SBLI CFD](#3-supersonic-nozzle--compressible-flow-cfd)** | Altitude-Compensating Aerospike & Intakes | Python (MoC), Ansys Fluent (C UDFs) | Mach 4.16 Angelino/MoC contour generator, $k\text{-}\omega$ SST URANS base-pressure maps |

---

## 🔬 Technical Breakdown

### 1. BEMT Propeller Design & Aero-Structural Optimization
A multidisciplinary workflow for designing and validating high-thrust, heavy-lift UAV propeller blades from 1D momentum theory to 3D structural finite element analysis.

* **Numerical BEMT Solver (`Python`):**
  * Discretizes the blade across **10 radial stations** incorporating **Prandtl tip and hub loss corrections**.
  * Optimizes radial chord distribution and geometric pitch/twist angles (transitioning from **50°–70° at the hub to 10°–20° at the tip**) for maximum hover and forward-flight figure of merit.
  * Evaluates aerodynamic trade-offs between **Clark-Y** and **NACA 4412** airfoil polars across Reynolds numbers.
  * Outputs dimensionless performance curves: Thrust Coefficient ($C_T$), Torque Coefficient ($C_Q$), Power Coefficient ($C_P$), and Propulsive Efficiency ($\eta$) vs. Advance Ratio ($J$).
* **3D CAD & Coupled Structural FEA (`Autodesk Fusion` & `Ansys Mechanical`):**
  * Automates 3D airfoil coordinate lofting into solid blade geometries.
  * Evaluates structural rigidity, tip deflection, and Von Mises stress distributions under simultaneous **aerodynamic pressure loads and peak rotational centrifugal loads**.

---

### 2. Rolls-Royce AE3007A Turbofan Cycle Analysis
Thermodynamic cycle deck modeling and architectural retrofitting of the **Rolls-Royce AE3007A** high-bypass turbofan engine using **GasTurb**.

* **Baseline Calibration:**
  * Anchors the design-point thermodynamic model against published **FAA Type Certificate Data Sheet (TCDS)** specifications (mass flow rate, overall pressure ratio, bypass ratio, and takeoff static thrust).
* **Architectural Modification (Mixed-Flow Variable Bypass / Geared Architecture):**
  * Investigates cycle modifications including mixed-flow exhaust nozzles, variable bypass scheduling, and geared fan integration to optimize fan pressure ratio (FPR) independently of low-pressure turbine (LPT) spool speed.
* **Parametric Carpet Plots:**
  * Maps **Thrust Specific Fuel Consumption (TSFC)** against **Specific Thrust** across varying Bypass Ratios (BPR), Overall Pressure Ratios (OPR), and Turbine Inlet Temperatures ($T_{t4}$), demonstrating measurable reductions in cruise SFC and improvements in propulsive efficiency.

---

### 3. Supersonic Nozzle & Compressible Flow CFD
High-speed compressible flow modeling focused on altitude-compensating rocket nozzles and supersonic intake shock-boundary layer interactions (SBLI).

* **Truncated Aerospike Nozzle Design & URANS CFD:**
  * **Contour Generation:** Python scripts implementing **Angelino's approximate method** and the **Method of Characteristics (MoC)** to generate plug contours targeting a design exit Mach number of **Mach 4.16**.
  * **Turbulence & Near-Wall Modeling:** High-resolution 2D planar/axisymmetric URANS simulations in **Ansys Fluent** utilizing the **$k\text{-}\omega$ SST turbulence model** with strict near-wall mesh refinement ($y^+ < 1$).
  * **Truncation & Multiphase Trade Studies:** Evaluates plug truncation lengths to quantify wake recirculation, expansion wave reflection, and base pressure thrust recovery across over-expanded, design, and under-expanded pressure ratios (including two-phase $\text{Al}_2\text{O}_3 / \text{B}_2\text{O}_3$ condensed-particle flow assessments).
* **Supersonic SBLI & Unsteady Ramp Flows:**
  * Dynamic-mesh CFD setups and custom **C-based User-Defined Functions (UDFs)** for characterizing shock-induced separation bubble dynamics over oscillating compression/expansion ramps.

---

## 📂 Repository Structure

```text
Projects-for-Propulsion/
├── 01_BEMT_Propeller_Optimization/
│   ├── src/
│   │   ├── bemt_solver.py          # Iterative BEMT solver with Prandtl tip/hub loss
│   │   ├── blade_optimizer.py      # Chord & twist radial distribution optimizer
│   │   └── airfoil_polars/         # NACA 4412 & Clark-Y Cl/Cd lookup tables
│   ├── cad_fea/                    # Lofted STEP geometries & Ansys Mechanical setups
│   └── results/                    # Ct, Cq, and Efficiency (η) vs. Advance Ratio (J) plots
│
├── 02_AE3007A_Turbofan_Cycle/
│   ├── gasturb_models/             # Baseline & modified cycle decks (.gtb / data exports)
│   ├── scripts/
│   │   └── plot_carpet.py          # Parametric TSFC vs. Specific Thrust carpet plotter
│   └── docs/                       # FAA TCDS validation & cycle trade study summary
│
├── 03_Supersonic_Nozzle_CFD/
│   ├── contour_generation/
│   │   ├── angelino_aerospike.py   # Mach 4.16 plug contour generator
│   │   └── moc_nozzle.py           # Method of Characteristics supersonic contour tool
│   ├── fluent_setups/              # Meshing parameters, case journals & C UDF scripts
│   └── post_processing/            # Mach contours, Schlieren & base-pressure recovery plots
│
├── requirements.txt
└── README.md
```

---

## ⚙️ Getting Started

### Prerequisites
To run the Python solvers, contour generators, and post-processing scripts, ensure you have **Python 3.12+** installed:

```bash
git clone [https://github.com/Spacevoyager18/Projects-for-Propulsion.git](https://github.com/Spacevoyager18/Projects-for-Propulsion.git)
cd Projects-for-Propulsion
pip install -r requirements.txt
```

*(Core Python dependencies: `numpy`, `scipy`, `matplotlib`, `pandas`)*

### Running the Solvers
1. **Run the BEMT Propeller Optimizer:**
   ```bash
   python 01_BEMT_Propeller_Optimization/src/bemt_solver.py
   ```
2. **Generate Aerospike Nozzle Coordinates:**
   ```bash
   python 03_Supersonic_Nozzle_CFD/contour_generation/angelino_aerospike.py --mach 4.16 --truncation 0.20
   ```
3. **Generate Turbofan Performance Carpet Plots:**
   ```bash
   python 02_AE3007A_Turbofan_Cycle/scripts/plot_carpet.py
   ```

---

## 📊 Key Visuals & Benchmarks

> 💡 *Tip: Drop your generated plots into an `assets/` folder and uncomment the links below to display them directly on the repository landing page.*

```markdown
<!--
![BEMT Efficiency vs Advance Ratio](assets/bemt_efficiency_curve.png)
![AE3007A TSFC Carpet Plot](assets/ae3007a_carpet_plot.png)
![Aerospike Mach 4.16 Contours](assets/aerospike_mach_contour.png)
-->
```

---

## 👤 Author

**Arghadeep Das**  
Dual Degree (B.Tech + M.Tech) in Aerospace Engineering  
Indian Institute of Technology (IIT) Kharagpur  
🔗 GitHub: [@Spacevoyager18](https://github.com/Spacevoyager18)

---

## 📄 License

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for details.
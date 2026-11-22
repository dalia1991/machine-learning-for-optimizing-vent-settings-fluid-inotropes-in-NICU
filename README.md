# Optimizing-mechanical-vent-settings-fluid-inotropes-in-NICU
# NICU Cardiopulmonary & Hemodynamic Optimization using Machine Learning

> **Project Status:** 🚧 *In Development — Pre-Data Collection & Architecture Design*

## Overview
This project aims to develop a machine learning system to optimize clinical interventions in the **Neonatal Intensive Care Unit (NICU)**. By modeling the physiological relationship between bedside interventions (**inputs**) and neonatal stability (**outputs**), the framework seeks to identify optimal treatment strategies for critically ill newborns.

## Problem Formulation: Inputs vs. Outputs
The system models patient physiology as a multi-input, multi-output (MIMO) control and optimization problem:

### 🎛️ Model Inputs (Controllable Clinical Variables)
* **Mechanical Ventilation Settings:** FiO₂, PEEP, PIP / Tidal Volume, Respiratory Rate, Mean Airway Pressure (MAP).
* **Fluid Management:** Maintenance IV fluid rates, fluid boluses, total fluid intake (mL/kg/day).
* **Cardiac & Vasoactive Medications:** Inotropes and vasopressors (e.g., Dopamine, Dobutamine, Epinephrine, Norepinephrine, Milrinone).

### 📈 Model Outputs (Target Neonatal Vital Signs)
* **Oxygenation & Ventilation:** SpO₂, PaO₂ / PaCO₂, transcutaneous CO₂.
* **Hemodynamics & Perfusion:** Heart Rate (HR), Systolic/Diastolic/Mean Arterial Blood Pressure (SBP, DBP, MBP), perfusion index, urine output / lactate (if available).

### 👶 Patient Context (Static & Baseline Covariates)
* Gestational age, birth weight, postnatal age (hours/days of life), and primary diagnosis (e.g., RDS, PPHN, neonatal sepsis, congenital heart disease).

---

## Planned Methodology
1. **Data Collection & Preprocessing:**
   * Extract time-series bedside monitor streams, ventilator logs, and infusion pump records (with weight-based normalization for neonatal dosing).
   * Align asynchronous sampling rates and filter motion/sensor artifacts common in NICU monitoring.
2. **Forward Physiological Modeling (Input → Output):**
   * Train sequence or state-space models (e.g., LSTMs, GRUs, Transformers, or Neural ODEs) to predict how vital signs respond to specific combinations of ventilator, fluid, and medication adjustments.
3. **Intervention Optimization (Finding Optimal Inputs):**
   * Use constrained optimization, Model Predictive Control (MPC), or Reinforcement Learning (RL) over the learned physiological model to recommend safe input adjustments that keep vital signs within target gestational-age-specific ranges.
4. **Validation:**
   * Evaluate prediction accuracy on held-out patient trajectories and verify that recommended actions respect neonatal clinical safety bounds.

## Repository Structure
*(Planned directory layout)*
```text
├── data/               # Raw and processed NICU datasets (gitignored for patient privacy)
├── notebooks/          # Exploratory data analysis and signal alignment tests
├── src/
│   ├── preprocessing/  # Weight normalization, resampling, and artifact removal
│   ├── models/         # Forward physiological response models (Inputs -> Vitals)
│   ├── optimization/   # Policy / inverse optimization algorithms
│   └── evaluation/     # Trajectory validation and safety constraint checks
├── docs/               # NICU variable definitions, target vital ranges, and protocols
└── README.md
```

## Roadmap
- [x] Define NICU input variables (ventilation, fluids, cardiac meds) and target vital sign outputs
- [x] Initialize repository structure
- [ ] Finalize data schema, sampling intervals, and ethical/IRB approval
- [ ] Build data extraction and time-alignment pipeline
- [ ] Train baseline Input → Vital Sign predictive models
- [ ] Implement constrained optimization to recommend optimal intervention settings

## Disclaimer
*This repository is strictly for research and educational purposes. The models and code developed here are not validated for clinical use and must not be used to guide real-time neonatal care.*

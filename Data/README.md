# Predicting Metabolic Cost During Human-in-the-Loop Optimization

## Machine Learning Mini-Project – UE24CS352A

### Team Members
- Parinitha Acharya
- [Team Member Name]

---

## 1. Project Overview

This project focuses on predicting the metabolic cost of human walking using machine learning and physiological/exoskeleton-related signals.

The project is based on the problem of **Predicting Metabolic Cost During Human-in-the-Loop Optimization**.

Human-in-the-loop optimization can be used to determine suitable exoskeleton assistance parameters that reduce the metabolic effort required for walking. However, directly measuring metabolic cost using indirect calorimetry can be time-consuming.

The objective of this project is to investigate whether metabolic cost can be predicted from signals collected during walking trials, particularly electromyography (EMG) and exoskeleton-related measurements.

---

## 2. Problem Statement

### Problem

Predict the metabolic cost of walking from physiological and exoskeleton-related signals collected during human walking trials.

### Objective

The main objectives of this project are:

1. Process metabolic and EMG walking data.
2. Determine a metabolic-cost target using walking and standing measurements.
3. Extract useful features from EMG/exoskeleton signals.
4. Train machine learning regression models.
5. Compare model performance using appropriate regression metrics.
6. Analyze the limitations of predicting metabolic cost for unseen subjects.

---

## 3. Dataset

The project uses a publicly available dataset associated with research on electromechanical ankle exoskeletons under proportional myoelectric control.

The dataset contains measurements collected during:

- Exoskeleton powered walking
- Exoskeleton unpowered walking
- Walking with boots only
- Standing baseline measurements
- Indoor treadmill trials
- Outdoor walking trials

For this machine learning project, the analysis initially focuses on the **indoor walking conditions** because they provide a consistent steady-state walking period.

### Indoor Conditions Used

| Condition | Description |
|---|---|
| `exopowin` | Exoskeleton powered, indoor treadmill walking |
| `exounpowin` | Exoskeleton worn but unpowered, indoor treadmill walking |
| `noexoin` | Boots only, indoor treadmill walking |

### Data Source

Dataset associated with:

**"Metabolic cost of walking with electromechanical ankle exoskeletons under proportional myoelectric control on a treadmill and outdoors"**

Authors:
- Rachel Hybart
- K. Siena Villancio-Wolter
- Daniel Perry Ferris

The original research dataset is available through Figshare.

EMG/Exoskeleton dataset DOI:

https://doi.org/10.6084/m9.figshare.22572868.v3

Metabolic dataset DOI:

https://doi.org/10.6084/m9.figshare.22572841.v4

---

## 4. Dataset Processing

### 4.1 Metabolic Data

The metabolic Excel files contain measurements such as:

- VO2
- VCO2
- VO2/Kg
- METS
- Heart rate
- VO2/HR

For each walking trial:

1. The metabolic Excel file was loaded.
2. The time-series data was extracted.
3. `VO2/Kg` was selected as the main oxygen-consumption measurement.
4. The final 3 minutes of the walking trial were selected to represent steady-state walking.
5. The mean `VO2/Kg` during the final 3 minutes was calculated.

### 4.2 Standing Baseline

A separate standing trial was used for each subject.

The mean standing `VO2/Kg` was calculated and used as the baseline.

The project target was calculated as:

```text
Net Metabolic Cost =
Walking VO2/Kg - Standing VO2/Kg

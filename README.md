# IMPORTANT NOTE:

This is my personal fork of this repo, utilizing Antigravity 2.0 to implement POPri, FedF1, and making a report on them for my Research project. For more details on the finding, I ran 15 rounds on alpha 0.1, 0.5 and 0.9. 0.5 and 0.9 are covered in `./EXPERIMENT_REPORT.md`. Graph and general data of all 3 alpha values can be seen in `./test/`

# SD-CSFL: A Synthetic Data-Driven Conformity Scoring Framework for Robust Federated Learning

<p align="center">
  <img src="FMW.png" width="780" alt="SD-CSFL Overview">
</p>

This repository contains the official implementation of the WACV 2026 paper:  
**“SD-CSFL: A Synthetic Data-Driven Conformity Scoring Framework for Robust Federated Learning.”**

---

## Overview

SD-CSFL is a unified defense framework that enhances the robustness of Federated Learning (FL) against:

* Gradient manipulation attacks (IPM, ALIE)
* Backdoor attacks (A3FL, F3BA, CerP)
* Heterogeneous (Non-IID) client distributions
* Privacy leakage from validation data

**Core Idea**

A clean **synthetic calibration dataset** is used to compute **entropy-based nonconformity scores** for each client model.  
These scores are evaluated using **adaptive percentile thresholds** to classify clients as benign or malicious.
Only benign updates are aggregated into the global model, enabling a unified and privacy-preserving anomaly detection mechanism.

---

## Abstract

Federated Learning remains highly vulnerable to gradient manipulation and backdoor attacks, especially under heterogeneous client data.
SD-CSFL introduces a **synthetic data–driven entropy-based conformity scoring mechanism**, combined with **adaptive percentile thresholding** and **stratified calibration**, enabling robust and privacy-preserving detection of malicious updates.
Experiments on **CIFAR-10** and **Birds-525** show up to **35% higher detection** and **80% backdoor success reduction** over existing defenses.

---

## Method Summary

### 1. Synthetic Calibration Data
* Generated using Stable Diffusion v2.
* Includes artistic, non-photorealistic, and abstract variations.
* Designed to amplify entropy sensitivity for improved anomaly detection.

### 2. Entropy-Based Nonconformity Score
* Each client model is evaluated on a shared synthetic dataset.
* Mean entropy across all samples forms the conformity (nonconformity) score.
* Higher scores indicate uncertainty or potentially malicious behavior.

### 3. Adaptive Percentile Thresholding
* Thresholds are computed using symmetric quantiles (e.g., 30%–70%).
* Maintains a controlled false-positive rate under Non-IID settings.
* Thresholds are updated every communication round to adapt to score shifts.

### 4. Aggregation
* Only benign client updates (scores within threshold bounds) are aggregated.
* Malicious clients may receive a perturbed global model to reduce attack influence.

## Datasets
* **Birds-525 Real Dataset:** [Google Drive Link](https://drive.google.com/file/d/1NvVfcrvXNOzX8mz1A-yhudegYJZXprSJ/view)
* **CIFAR-10 Real Dataset:** [Official CIFAR-10 Link](https://www.cs.toronto.edu/~kriz/cifar.html)
* **Birds-Synth and CIFAR-10-Synth (Synthetic Calibration Dataset):** [Google Drive Link](https://drive.google.com/file/d/10akkldmavU_CxsMlWacL0Lq0Nr9eQuz6/view?usp=drive_link)
* **Synthetic Dataset Generator (Stable Diffusion + Pipelines):** [https://github.com/A-Kerim/Synthetic-Data-Usability](https://github.com/A-Kerim/Synthetic-Data-Usability)

---

## Getting Started

1. Clone this repository to your local machine.
2. Install the required dependencies:
   ```bash
   pip install -r requirements.txt
   ```
3. Download the datasets using the links above.
4. Adjust experiment settings in `configs/` based on your needs.

---

## License

The SD-CSFL framework and the associated synthetic datasets are made freely available for academic and non-commercial research purposes.  
If you use the framework or the datasets, please cite our WACV 2026 paper.

---

## Acknowledgments

This work was supported by the Saudi Arabian Ministry of Education, the Saudi Arabian Cultural Bureau in London, and Umm Al-Qura University.  
We also thank the High-End Computing (HEC) facility at Lancaster University for providing essential computational resources.

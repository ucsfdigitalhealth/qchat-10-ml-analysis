# 🧠 Compact Subsets of QCHAT-10 Predict Autism Diagnoses with Machine Learning

**Authors:** Lydia J. Sollis¹, Dennis P. Wall²³⁴, Peter Y. Washington⁵
¹University of Hawaiʻi at Mānoa ²³⁴Stanford University ⁵University of California San Francisco
📧 Contact: [peter.washington@ucsf.edu](mailto:peter.washington@ucsf.edu) | [lsollis@cc.hawaii.edu](mailto:lsollis@cc.hawaii.edu)

---

## 📘 Overview

This repository contains the code used for the study
**“Compact Subsets of Autism Screening Items Predict Clinical Diagnoses with a Machine Learning Analysis of the QCHAT-10.”**
The project investigates whether **small subsets of QCHAT-10 questionnaire items** can generalize from predicting screening outcomes to predicting **clinician-established autism diagnoses** across countries.

The pipeline uses **tree-based machine-learning models** (Decision Tree, Random Forest, XGBoost) to:

1. Train models on New Zealand (n = 1,054) and Saudi Arabian (n = 506) QCHAT-10 datasets labeled by screening scores.
2. Validate across datasets to tune thresholds.
3. Test on the **Polish dataset (n = 252)** labeled by clinical diagnoses (ADOS-2, ADI-R, DSM-5).
4. Apply **Recursive Feature Elimination (RFE)** to identify minimal feature sets with high predictive power.

---

## 🧩 Key Findings

* Compact **4-item models** retained three recurring behavioral features:

  * **Eye contact**
  * **Following gaze direction**
  * **Pretend play**
* **New Zealand model:** AUROC 85 ± 13 %, Sensitivity 91 %, Specificity 50 %
* **Saudi model:** AUROC 87 ± 11 %, Sensitivity 84 %, Specificity 80 %
* **Polish (clinical) model:** AUROC 91 ± 5 %
* Demonstrates **partial label-transfer generalization** from screening to diagnosis.

---

## 🧠 Conceptual Framework

* **Goal:** Determine whether ML models trained on questionnaire scores can predict *clinical* diagnoses in independent populations.
* **Challenge:** Label-source and construct shift between screening-derived and clinically confirmed labels.
* **Approach:** Use RFE to reduce QCHAT-10 items while preserving predictive signal, optimizing for high sensitivity.

---

## ⚙️ Methods Summary

| Step                          | Description                                                                                     |
| ----------------------------- | ----------------------------------------------------------------------------------------------- |
| **1. Data Loading**           | Import QCHAT-10 datasets from New Zealand, Saudi Arabia, and Poland                             |
| **2. Preprocessing**          | Encode categorical responses, align features, remove redundant variables                        |
| **3. Model Training**         | Train DT, RF, and XGBoost models with stratified 5-fold CV and randomized hyperparameter search |
| **4. Feature Selection**      | Apply Recursive Feature Elimination to derive compact (4-item) models                           |
| **5. Threshold Optimization** | Adjust probability cutoffs to maximize sensitivity while retaining ≥ 0.5 specificity            |
| **6. External Validation**    | Test trained models on the Polish dataset containing true clinical labels                       |

---

## 📊 Datasets

| Dataset                     | Source                    | N     | Label Type                        | Access                                                                                                              |
| --------------------------- | ------------------------- | ----- | --------------------------------- | ------------------------------------------------------------------------------------------------------------------- |
| **New Zealand QCHAT-10**    | Thabtah (ASDTests App)    | 1,054 | Screening (QCHAT ≥ 4)             | [ASDTests Repository](https://www.asdtests.com/) / [UCI Repo](https://doi.org/10.24432/C5659W)                      |
| **Saudi Arabia QCHAT-10**   | Kaggle Dataset            | 506   | Screening (QCHAT ≥ 4)             | [Kaggle Link](https://www.kaggle.com/datasets/asdpredictioninsaudi/asd-screening-data-for-toddlers-in-saudi-arabia) |
| **Poland QCHAT (Clinical)** | Niedźwiecka et al. (2020) | 252   | Clinical (ADOS-2 / ADI-R / DSM-5) | [Mendeley Data](https://data.mendeley.com/datasets/tmpkt2mfkg/2)                                                    |

All datasets are **publicly available** and suitable for replication.

---

## 💻 Repository Structure

```
├── data/
│   ├── nz_qchat10.csv
│   ├── sa_qchat10.csv
│   └── pl_qchat.csv
├── src/
│   ├── preprocessing.py
│   ├── train_models.py
│   ├── feature_selection_rfe.py
│   ├── evaluate_models.py
│   └── utils/
│       ├── metrics.py
│       └── plots.py
├── notebooks/
│   └── autism_qchat10_project.ipynb
├── results/
│   ├── feature_importance.csv
│   ├── metrics_summary.csv
│   └── figures/
│       ├── rfe_nz.png
│       ├── rfe_sa.png
│       └── roc_curves.png
├── requirements.txt
└── README.md
```

---

## 🚀 Quick Start

### Installation

```bash
git clone https://github.com/<username>/autism-qchat10.git
cd autism-qchat10
pip install -r requirements.txt
```

### Usage

```bash
python src/train_models.py --dataset nz_qchat10.csv --model xgb --rfe 4
python src/evaluate_models.py --train nz --test pl --threshold 0.3
```

---

## 📈 Example Results

| Model                 | Train Data      | Test Data       | AUROC (± SD) | Sensitivity | Specificity |
| --------------------- | --------------- | --------------- | ------------ | ----------- | ----------- |
| NZ 4-feature          | NZ QCHAT-10     | Polish Clinical | 0.85 ± 0.13  | 0.91        | 0.50        |
| Saudi 4-feature       | Saudi QCHAT-10  | Polish Clinical | 0.87 ± 0.11  | 0.84        | 0.80        |
| Polish 4-feature (CV) | Polish Clinical | Cross-val       | 0.91 ± 0.05  | 0.84        | 0.90        |

---

## 📚 Citation

If you use this code or dataset in your research, please cite:

> Sollis LJ, Wall DP, Washington PY. **Compact Subsets of Autism Screening Items Predict Clinical Diagnoses with a Machine Learning Analysis of the QCHAT-10**. (Preprint, 2025).

---

## 📬 Contact

For questions or collaboration:

* 📧 [peter.washington@ucsf.edu](mailto:peter.washington@ucsf.edu)
* 📧 [lsollis@cc.hawaii.edu](mailto:lsollis@cc.hawaii.edu)

---

## ⚖️ License

This project is distributed under the **MIT License**.
All datasets are governed by their respective public data terms.

---

## 🧾 Funding

Supported by the **NIH (DP2EB035858, R01LM014342, R01LM013364)** and the **Stanford Center for Digital Health**.
The content is solely the responsibility of the authors and does not represent the official views of the NIH.


**Last Updated:** October 2024  
**Status:** Manuscript under review at Scientific Reports

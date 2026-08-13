# Emmanuel-Moemeke-3MTT-NEXTGEN-Capstone-Project
Loan Default Risk Predictor (Using the Nigerian Fintech Space as  Case Study)


# Credit Risk & Loan Default Prediction in Digital Lending
## Executive Summary
This project builds and evaluates a Machine Learning pipeline designed to tackle high Non-Performing Loan (NPL) rates in digital micro-lending. Using a imbalanced dataset mirroring real-world credit applications, this project demonstrates how standard models succumb to the **Accuracy Paradox**—approving bad loans just to maintain high overall accuracy—and how **SMOTE resampling combined with Recall optimization** restores financial utility.

## Business Problem & Context
Digital lending platforms in Nigeria rely heavily on automated credit decisioning to disburse short-term loans. The core business threat is **loan default**:
* **False Positive (Type I Error):** You mistakenly flag a trustworthy applicant as risky. This results in the customer losing interest because your process took too long or was too difficult.
* **False Negative (Type II Error):** You mistakenly approve an applicant who is going to default. This results in a severe financial loss of over $10,000 for that loan.
Standard models trained on imbalanced financial data default to approving almost everyone. This project optimizes for **Recall on Class 1 (Defaulters)** to flag high-risk applicants before funds are disbursed.

## Dataset Justification & NDPR Compliance
Under Nigerian Data Protection Regulation (NDPR) and global banking secrecy standards, actual credit default records containing identifiable user histories are strictly confidential. 

In accordance with standard financial modeling practices, this project utilizes a **synthetically generated dataset** engineered to capture real-world micro-lending dynamics:
* **Total Records:** Evaluated across train/test splits.
* **Class Imbalance:** 88% Paid (`Class 0`) vs. 12% Defaulted (`Class 1`).
* **Feature Set:** Demographic, transaction, and historical credit behavior indicators.

## Technical Workflow Pipeline

1. **Preprocessing & Leakage Prevention:** Feature scaling and categorical encoding fitted strictly on the training set.
2. **Vanilla Baseline:** Evaluated a Random Forest model on untouched imbalanced data to establish a performance floor.
3. **Resampling Strategy:** Applied Synthetic Minority Over-sampling Technique (SMOTE) strictly to $X_{train}$ to balance class distributions.
4. **Model Suite Evaluation:** Trained and benchmarked 5 distinct classifiers across both Training and Test sets:
   * Logistic Regression
   * Decision Tree
   * Random Forest
   * Gradient Boosting
   * LightGBM

---

## Benchmark Comparison & Findings

| Model | Acc (Train) | Acc (Test) | Recall (Train) | Recall (Test) | F1 (Test) | ROC-AUC (Test) | Status |
| :--- | :---: | :---: | :---: | :---: | :---: | :---: | :--- |
| **Vanilla RF (Baseline)** | - | 0.8864 | - | 0.0529 | 0.0977 | - | Baseline |
| **Logistic Regression** | **0.6930** | **0.6927** | **0.6817** | **0.6947** | **0.3443** | **0.7609** | **Selected Winner** |
| **Decision Tree** | 1.0000 | 0.7881 | 1.0000 | 0.2708 | 0.2288 | 0.5634 | Overfitted |
| **Random Forest** | 1.0000 | 0.8817 | 1.0000 | 0.1177 | 0.1877 | 0.7380 | Overfitted |
| **Gradient Boosting** | 0.8801 | 0.8804 | 0.1473 | 0.1538 | 0.2300 | 0.7499 | Suppressed |
| **LightGBM** | 0.8876 | 0.8860 | 0.0680 | 0.0588 | 0.1071 | 0.7569 | Suppressed |

### Key Observations
* **The Baseline Failure:** The Vanilla Random Forest scored **88.64% Accuracy**, but caught only **5.29%** of defaulters (missing 5,617 bad loans).
* **Tree-Based Overfitting:** Decision Tree and Random Forest memorized synthetic SMOTE data (100% Train Recall), collapsing on unseen test data.
* **Complex Model Suppression:** Gradient Boosting and LightGBM reverted to majority-class preference, ignoring SMOTE adjustments.
* **The Winner:** **Logistic Regression** generalized cleanly. Train recall (68.17%) and Test recall (69.47%) aligned, demonstrating stable learning and catching nearly 70% of potential defaults.

## Deployment Recommendation
For production deployment in a micro-lending pipeline, **Logistic Regression** is the primary choice. While overall accuracy scales down to ~69%, its capacity to reliably detect ~70% of defaulting applicants significantly reduces credit exposure and loan loss provisions.
prediction.git)
   cd loan-default-prediction

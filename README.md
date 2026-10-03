# HR Analytics: Employee Attrition Prediction

![Python](https://img.shields.io/badge/Python-3.10+-blue) ![scikit-learn](https://img.shields.io/badge/scikit--learn-ML-orange) ![SHAP](https://img.shields.io/badge/SHAP-Explainability-purple) ![Dashboard](https://img.shields.io/badge/Interactive-Dashboard-yellow)

**Author:** Ramees Fathima | Data Analyst Internship Project, Elevate Labs

> Understand why employees resign, predict who is at risk, and estimate how much money targeted retention can save.

**Live interactive dashboard:** https://rameesfathima.github.io/hr-attrition-analysis/

---

## 1. Business problem
Replacing an employee can cost about half of their annual salary. This project answers five questions:
1. Which departments, roles and pay bands lose the most people?
2. Are overtime, pay, tenure and travel *statistically* related to attrition?
3. Which model best catches real leavers? (Recall matters more than accuracy here.)
4. What drives each employee's risk? (SHAP)
5. How much can targeted retention save?

## 2. Dataset
IBM HR Analytics Employee Attrition: 1,470 employees, 35 attributes, 16.1% attrition (imbalanced). It is a fictional practice dataset created by IBM data scientists.

## 3. Key results
| Finding | Result |
|---|---|
| Overtime | **30.5%** attrition vs 10.4% without overtime (top SHAP driver) |
| Lowest income band | **29.3%** vs about 10% in higher bands |
| Highest-risk role | Sales Representative, **39.8%** |
| First 2 years at company | **29.8%** attrition |
| Best model | Logistic Regression, CV ROC-AUC **0.83** |
| Final model (threshold 0.46) | Recall **72%**, Precision 36%, ROC-AUC 0.81 |
| Risk-bucket validation | Actual attrition: High **37.7%**, Medium 11.5%, Low 4.2% |
| Estimated saving | about **$1.2M per year** (assumes replacement cost = 50% of salary, 30% retention success) |

## 4. Dashboard
**Overview page**

![Overview](overview.png)

**Employee Risk page**

![Risk](risk.png)

The same dashboard is included as `dashboard/HR_Attrition_Dashboard.html` (open it in any browser).

## 5. Model evaluation
![Confusion matrix](confusion_matrix.png)

| Model | CV ROC-AUC | Recall | F1 | Test ROC-AUC |
|---|---|---|---|---|
| **Logistic Regression** | **0.831** | 0.638 | 0.448 | 0.806 |
| XGBoost | 0.808 | 0.468 | 0.436 | 0.772 |
| Random Forest | 0.802 | 0.106 | 0.159 | 0.778 |
| Decision Tree | 0.697 | 0.532 | 0.420 | 0.723 |

Random Forest has the highest accuracy (0.82) but catches only 11% of leavers, so models were compared on recall, F1 and ROC-AUC instead of accuracy.

## 6. Explainability (SHAP)
![SHAP](shap_summary.png)

## 7. Approach
1. **Cleaning:** removed constant columns and ID, checked missing values and duplicates.
2. **Feature engineering:** income vs job-level average, promotion-gap ratio, income, age and tenure bands.
3. **Statistical tests:** chi-square (categorical) and Welch t-test (numeric).
4. **Modelling:** stratified 80/20 split, class weights, 5-fold cross-validation, 4 models compared.
5. **Threshold tuning:** maximised F2 (recall weighted higher) on out-of-fold training predictions, with no test-set leakage.
6. **SHAP:** global and individual explanations.
7. **Risk scoring:** cross-validated Low / Medium / High score for every employee, exported to Power BI.
8. **Business impact:** replacement cost and retention savings with stated assumptions.

## 8. Repository structure
```
hr-attrition-analysis/
├── README.md
├── requirements.txt
├── index.html       interactive dashboard (GitHub Pages)
├── overview.png, risk.png, confusion_matrix.png, shap_summary.png   (images used in this README)
├── data/            HR-Employee-Attrition.csv
├── notebooks/       HR_Attrition_Analysis.ipynb
├── outputs/         hr_clean_for_powerbi.csv, model_comparison.csv, shap_top_features.csv
├── charts/          EDA, ROC, confusion matrix, SHAP plots
├── dashboard/       web dashboard (HTML + screenshots), Power BI file
└── reports/         Project report, Model accuracy report, Attrition prevention suggestions (PDF)
```

## 9. How to run
```bash
pip install -r requirements.txt
jupyter notebook notebooks/HR_Attrition_Analysis.ipynb
```
Run all cells. The notebook finds the dataset in `data/` automatically.

## 10. Deliverables
| Requirement | File |
|---|---|
| Dashboard | `dashboard/` (web dashboard HTML and screenshots; Power BI `.pbix` if added) |
| Model accuracy report + confusion matrix | `reports/HR_Model_Accuracy_Report.pdf` |
| PDF of attrition prevention suggestions | `reports/HR_Attrition_Prevention_Suggestions.pdf` |
| Project report (2 pages) | `reports/HR_Attrition_Report.pdf` |

## 11. Limitations
Fictional dataset; results show association, not causation; the test set has only 47 leavers, so metrics carry uncertainty; risk scores should support, not replace, manager judgement.


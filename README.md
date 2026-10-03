# HR Analytics: Employee Attrition Prediction

**Author:** Ramees Fathima | Data Analyst Internship Project, Elevate Labs

**Live dashboard:** https://rameesfathima.github.io/hr-attrition-analysis/

## Project summary
This project analyses the IBM HR Analytics dataset (1,470 employees, 16.1% attrition) to find why employees leave, predict who is at risk, and estimate the savings from targeted retention.

## Key results
- Employees working overtime leave at **30.5%** vs 10.4% without overtime.
- Lowest income band: **29.3%** attrition vs about 10% in higher bands.
- Best model: Logistic Regression (CV ROC-AUC 0.83), catching **72%** of leavers.
- Employees flagged High risk actually left at **37.7%**, vs 4.2% in the Low bucket.
- Estimated saving from targeted retention: about **$1.2M per year** (assumes replacement cost of 50% of salary and 30% retention success).

## What was done
1. Data cleaning and feature engineering
2. EDA and statistical tests (chi-square, t-test)
3. Four models compared with 5-fold cross-validation (Logistic Regression, Decision Tree, Random Forest, XGBoost)
4. Threshold tuning for high recall
5. SHAP explainability
6. Employee risk scoring (Low / Medium / High)
7. Interactive dashboard (Overview and Employee Risk pages)

## Files
| Folder / file | Contents |
|---|---|
| `index.html` | Interactive dashboard |
| `notebooks/` | Python notebook with full analysis |
| `data/` | IBM HR dataset |
| `outputs/` | Model comparison, SHAP features, risk scores (CSV) |
| `charts/` | EDA, ROC, confusion matrix and SHAP charts |
| `reports/` | Project report, model accuracy report, attrition prevention suggestions (PDF) |
| `dashboard/` | Dashboard HTML and screenshots |

## How to run
```
pip install -r requirements.txt
jupyter notebook notebooks/HR_Attrition_Analysis.ipynb
```

## Note
The dataset is a fictional practice dataset from IBM. Results show association, not causation.

# Heart Disease Prediction

A machine-learning model that predicts whether a patient has **heart disease** from 13 routine clinical measurements, such as age, chest-pain type, blood pressure, cholesterol and maximum heart rate.

> Educational project. It is **not** a medical diagnostic tool and must not be used for clinical decisions.

---

## Results

Logistic Regression, trained on 70% of patients and tested on the held-out 30% (91 patients):

| Metric | Training | **Test** |
|---|---|---|
| Accuracy | 86.8% | **86.8%** |
| Precision (heart disease) | 0.86 | 0.87 |
| Recall (heart disease) | 0.90 | **0.90** |
| F1 (heart disease) | 0.88 | 0.88 |

**Test confusion matrix**

| | Predicted: no disease | Predicted: disease |
|---|---|---|
| **Actual: no disease** (41) | 34 | 7 |
| **Actual: disease** (50) | 5 | **45** |

- The model correctly identifies **45 of 50** patients with heart disease (90% recall). In a screening setting, catching true cases matters more than avoiding false alarms.
- Training and test accuracy are nearly identical, so the model **generalises well and is not overfitting**.

---

## Dataset

`heart.csv`: **303 patients, 13 features + 1 target**, no missing values. Classes are fairly balanced (165 with disease, 138 without).

| Feature | Meaning |
|---|---|
| `age`, `sex` | Age in years; sex (1 = male, 0 = female) |
| `cp` | Chest-pain type (0–3) |
| `trestbps` | Resting blood pressure (mm Hg) |
| `chol` | Serum cholesterol (mg/dl) |
| `fbs` | Fasting blood sugar > 120 mg/dl (1 = true) |
| `restecg` | Resting ECG result (0–2) |
| `thalach` | Maximum heart rate achieved |
| `exang` | Exercise-induced angina (1 = yes) |
| `oldpeak` | ST depression induced by exercise |
| `slope` | Slope of the peak exercise ST segment |
| `ca` | Number of major vessels coloured by fluoroscopy (0–4) |
| `thal` | Thalassemia result |
| **`target`** | **1 = heart disease, 0 = no heart disease** |

**Source:** UCI Machine Learning Repository, *Heart Disease* dataset (Cleveland subset): Janosi, A., Steinbrunn, W., Pfisterer, M. & Detrano, R. (1988), [doi.org/10.24432/C52P4X](https://doi.org/10.24432/C52P4X), licensed CC BY 4.0. This is the widely used 303-row version of that dataset.

---

## How it works

1. **Explore:** class balance, a missing-value check, distributions of every feature split by diagnosis, age vs. maximum heart rate, a correlation heatmap and each feature's correlation with the target.
2. **Prepare:** split features into categorical (10 or fewer unique values) and continuous; one-hot encode the categorical ones; standardise the continuous ones (`age`, `trestbps`, `chol`, `thalach`, `oldpeak`).
3. **Train:** 70/30 train-test split, then Logistic Regression (`liblinear` solver).
4. **Evaluate:** accuracy, a classification report and a confusion matrix on both the training and test sets.

---

## Getting started

```bash
git clone https://github.com/pruthvicodes/Heart-disease-prediction.git
cd Heart-disease-prediction
pip install -r requirements.txt
jupyter notebook heart_disease_prediction.ipynb
```

---

## Limitations and next steps

- **Scaling before the split:** the scaler was fitted on all 303 patients before splitting. Fitting it on the training set only (inside a scikit-learn `Pipeline`) avoids slight test-set leakage.
- **Small dataset, single split:** with 303 patients, k-fold cross-validation would give a more reliable estimate.
- **One model:** next, compare Random Forest, SVM and XGBoost, tune hyperparameters, save the best model and add a prediction script or a simple web form.

---

## Tech stack

Python · pandas · NumPy · scikit-learn · Matplotlib · Seaborn · Jupyter

## Author

**Prithviraj Chavan**, B.E. Artificial Intelligence & Data Science, Pune
[LinkedIn](https://www.linkedin.com/in/prithvirajshahajichavan) · [GitHub](https://github.com/pruthvicodes)

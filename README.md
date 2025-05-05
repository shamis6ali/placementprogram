# Predicting Graduate‑Program Placement Success

> **ENSF 544 • Machine‑Learning Capstone**  
> **Author:** **Shamis Ali** (30096335)

---

## 🗒️ Overview
Recruitment agency **Power Recruitment** (Bloomington, IN) wants to estimate before investing in a client, whether that applicant will ultimately secure a U.S. graduate‑program placement.  
Using the **Job Placement Dataset** from Kaggle, this project:

1. Cleans & encodes the raw CSV.  
2. Benchmarks three supervised models (Logistic Regression, Random Forest, SVM).  
3. Outputs probability scores that the agency can embed in its internal CRM.

---

---

## 📈 Dataset

| Column            | Description                                   |
|-------------------|-----------------------------------------------|
| `gender`          | Male / Female                                 |
| `age`             | Age in years                                  |
| `stream`          | Undergraduate discipline                      |
| `university`      | Undergraduate institution                     |
| `gpa`             | GPA (4‑point scale)                           |
| `work_experience` | Prior industry experience (Yes/No)            |
| `placement_status`| **Target** – Placed / Not Placed              |
| `salary`          | Starting salary in USD if placed (NaN else)   |

*Source: Kaggle — “Job Placement Dataset” (downloaded 2025‑05‑05).*
Dataset Link: https://www.kaggle.com/datasets/mahad049/job-placement-dataset/data

---

## 🚀 Quickstart

```bash
# clone & create Python env
git clone https://github.com/<your‑handle>/placement‑success.git
cd placement‑success
python -m venv .venv
source .venv/bin/activate           # (Windows: .venv\Scripts\activate)
pip install -r requirements.txt

# fetch the data
kaggle datasets download -d mahad049/job-placement-dataset -p data/ --unzip

# reproduce every figure & metric
jupyter lab notebooks/Project-544.ipynb
```

Prefer a CLI workflow?

```bash
python src/train.py --model random_forest --save reports/rf.pkl
```

---

## 🛠️ Methodology

| Stage               | Tooling / Techniques                                          |
|---------------------|---------------------------------------------------------------|
| **Cleaning & EDA**  | `pandas`, missing‑value charts, pair‑plots                    |
| **Feature Eng.**    | One‑hot encoding (`sklearn.compose.ColumnTransformer`)        |
| **Modeling**        | Logistic Regression, Random Forest, SVM (RBF kernel)          |
| **Hyper‑params**    | `GridSearchCV`, 5‑fold CV, `scoring='accuracy'`               |
| **Evaluation**      | Train vs CV vs Test accuracy, precision, recall, F1, ROC‑AUC  |
| **Visuals**         | Learning curves, ROC curves, confusion matrices (`matplotlib`)|

Full commentary lives in **`notebooks/Project‑544.ipynb`**.

---

## 📊 Results

| Model                | Train Acc | CV Acc | Test Acc | F1‑score |
|----------------------|:---------:|:------:|:--------:|:--------:|
| Logistic Regression  | 0.99 | 0.98 | 0.96 | 0.96 |
| Random Forest        | 0.99 | 0.98 | **0.97** | **0.97** |
| SVM (RBF)            | 0.98 | 0.98 | 0.96 | 0.96 |

*Random Forest produced the best generalization: **97 % test accuracy** and the top F1.*  
Confusion matrices and ROC curves are available in `reports/figures/`.

---

## 🔄 Reproducibility
* **Python 3.11**  
* Deterministic splits & model seeds (`random_state=42`)  
* Exact versions pinned in `requirements.txt`.

---

## 📅 Roadmap
- **Probability calibration** (Platt or isotonic) for better rank‑ordering.  
- **Gradient‑boosting benchmarks** (XGBoost / LightGBM).  
- **Streamlit app** to score candidates interactively.  
- **New data collection** (2024‑2025 cohort) to mitigate temporal drift.

---

## 🤝 Contributing
1. Fork → branch → PR.  
2. Follow PEP 8 & run `pytest`.  
3. Be excellent to each other (see `CODE_OF_CONDUCT.md`).

---

## 📰 License
**Code:** MIT  
**Data:** CC0 1.0 (Kaggle dataset author)

# Healthcare Readmission Risk Classification (CMS-style)

## 📌 Problem Statement
Hospital readmissions are costly and often preventable.  
The goal of this project is to **identify high-risk hospitals** for excess readmissions using hospital-level utilization and cost metrics, enabling early intervention and better care management.

This project mirrors the logic of the **CMS Hospital Readmissions Reduction Program (HRRP)** and focuses on building an **interpretable, recall-optimized classification model** suitable for healthcare decision-making.

---

## 🧠 Key Objectives
- Build a **binary classification model** to flag high-risk hospitals
- Handle **class imbalance** common in healthcare data
- Prioritize **recall** to minimize missed high-risk cases
- Use **threshold tuning** to align model decisions with real-world healthcare tradeoffs
- Maintain **interpretability** for regulated environments

---

## 📊 Dataset
- **Type:** CMS-style synthetic hospital-level dataset
- **Rows:** ~1,200 hospitals
- **Target Variable:**  
  `high_risk` (1 = excess readmissions, 0 = no excess)
- **Key Features:**
  - Number of discharges
  - Average length of stay
  - Emergency department visit rate
  - Chronic condition index
  - Average claim amount

> The dataset structure and distributions closely resemble CMS HRRP public data but contain no sensitive information.

---

## 🔍 Modeling Approach

### 1. Data Preparation
- Stratified train–test split to preserve class imbalance
- Feature scaling using `StandardScaler`
- Explicit exclusion of policy-derived metrics to avoid **target leakage**

### 2. Baseline Model
- **Logistic Regression**
- `class_weight="balanced"` to handle minority high-risk class
- Probability-based predictions (not hard labels)

### 3. Evaluation Metrics
- **Recall** (primary)
- Precision
- F1-score
- ROC-AUC
- Precision–Recall Curve

Accuracy was intentionally **not** used as the primary metric due to class imbalance.

---

## 🎯 Threshold Tuning (Key Insight)
Rather than relying on the default 0.5 threshold, multiple decision thresholds were evaluated.

### Final Operating Point
- **Threshold ≈ 0.45**
- **Recall (High-risk hospitals): ~82%**
- **Precision (High-risk hospitals): ~55%**

This threshold significantly reduced false negatives while keeping false positives operationally manageable.

A **precision–recall curve** was used to visualize and justify the final threshold selection.

---

## 🏥 Key Takeaways
- In healthcare, **missing high-risk cases is more costly than false alarms**
- Model probabilities are more important than raw predictions
- Thresholds represent **business and clinical decisions**, not model performance
- Interpretable models remain highly valuable in regulated domains

---

## 🛠️ Tech Stack
- Python
- Pandas, NumPy
- Scikit-learn
- Matplotlib, Seaborn

---

## 🚀 Future Work
- Explore other Machine learning frameworks 

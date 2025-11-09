# CTR Prediction (Click-Through Rate Modeling)

This repository contains a machine learning pipeline for predicting the probability that a user will click on an online advertisement.  
The goal is to build a scalable, efficient CTR prediction workflow using modern data processing tools and robust ML models.

---

## 📦 Dataset

- **Source:** Hugging Face → `BadrAbu/CTR_Prediction`
- **Task:** Binary classification (`click` = 1 / 0)
- **Scale:** Millions of impressions (large-scale ad dataset)
- **Columns:** Mostly anonymized categorical features (`C1`, `C14`, `C17`, …) + some numeric fields
- **Challenge:** Strong **class imbalance** (clicks << non-clicks)

> For development and experimentation, a **300K sampled subset** is used.  
> For production-level training, the pipeline supports **streaming + chunk processing** using Polars.

---

## 🧠 Problem Definition

**Goal:** Given user/context/ad characteristics, predict:

```python
P(click = 1 | features)
````

This prediction is essential in:

* Ad ranking / bidding
* Personalization systems
* Recommender pipelines

---

## 🏗 Project Workflow

| Stage                         | Description                                                        |
| ----------------------------- | ------------------------------------------------------------------ |
| **1. Data Loading**           | Loaded efficiently using **streaming** (no full RAM load).         |
| **2. Data Exploration (EDA)** | Understanding distributions, imbalance, and feature patterns.      |
| **3. Preprocessing**          | Categorical encoding, memory optimization, handling imbalance.     |
| **4. Train/Test Split**       | Stratified splitting to preserve click ratio.                      |
| **5. Model Experiments**      | CatBoost / LightGBM recommended for high-cardinality categoricals. |

---

## ⚙️ Tech Stack

| Category                | Tools                                        |
| ----------------------- | -------------------------------------------- |
| Data Loading            | `datasets`, `polars` (lazy + streaming mode) |
| Data Prep               | `pandas`, `scikit-learn`, `imbalanced-learn` |
| Modeling (current/next) | `CatBoost`, `LightGBM`, `XGBoost`            |
| Visualization           | `matplotlib`, `seaborn`, `plotly`            |
| Deployment (planned)    | `streamlit` dashboard                        |

---

## 🔥 Key Insights from EDA

* Click events are **rare** → the dataset is highly **imbalanced**.
* Feature space is **dominated by categorical IDs**, often high-cardinality.
* No severe missing-value problems detected.
* Models that support **native categorical handling** perform best (e.g., CatBoost).

---

## 🧪 Preprocessing Summary (Current Stage)

✔ Streaming-based loading (efficient for 45M+ rows)
✔ Sample extraction for feature engineering/testing
✔ Class imbalance handled using **SMOTEN**
✔ One-hot encoding applied **only on the sampled subset**
✔ **Train/Test split completed** and preprocessing pipeline saved

Next stage → full-data training using CatBoost (no one-hot needed).

---

## 📁 Project Structure

```
CTR_Prediction/
├── notebooks/
│   ├── 01_eda.ipynb
│   ├── 02_preprocessing.ipynb
├── data/
│   ├── raw/        # Original dataset streaming / sample extractions
│   └── processed/  # Preprocessed / encoded / split outputs
├── models/
│   └── (to be saved after training)
├── requirements.txt
├── README.md
└── .gitignore
```

---

## 🧭 Roadmap

| Status | Task                                    |
| :----: | --------------------------------------- |
|    ✅   | Data streaming + sample extraction      |
|    ✅   | Exploratory Data Analysis               |
|    ✅   | Preprocessing + Train/Test Split        |
|   🔜   | Train CatBoost baseline model           |
|   🔜   | Evaluate using ROC-AUC / LogLoss        |
|   🔜   | Compare with LightGBM & XGBoost         |
|   🔜   | Build interactive dashboard (Streamlit) |
|   🔜   | Model packaging + deployment option     |

---

## ▶ Run the Project

### 1. Install Dependencies

```bash
pip install -r requirements.txt
```

### 2. Launch Jupyter Notebook

```bash
jupyter notebook
```

### 3. (Optional) Run Streamlit Dashboard

```bash
streamlit run app.py
```

---

## 📚 License

For educational and research purposes only.
You are free to fork, improve, and reference in academic work.

---

## 👤 Maintainer

**Author:** *Your Name*
For questions or collaboration → *GitHub Issues / Discussions*

```

---

If you'd like, I can now also:

✅ Generate a clean `requirements.txt`  
✅ Generate project badges (stars, license, python version, etc.)  
✅ Write the Streamlit dashboard page  
✅ Write the final Presentation Script (for the TA)  



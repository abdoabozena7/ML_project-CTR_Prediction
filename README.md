# CTR Prediction Project – Team Workflow Documentation

## 🎯 Project Goal

The goal of this project is to **predict Click-Through Rate (CTR)** — whether a user will **click (1)** or **not click (0)** on an online advertisement.

This is a **binary classification problem** with:

* **Very large dataset** (tens of millions of rows)
* **Mostly categorical features** (C1, C2, C14, etc.)
* **Strong class imbalance** (clicks are rare)

Our pipeline is designed to:

1. Explore and understand the data 
2. Preprocess it efficiently (especially because of dataset size)
3. Prepare clean data for model training
4. Allow the rest of the team to plug in, test models, and compare results

---

## 📦 Dataset

Dataset used:

```
BadrAbu/CTR_Prediction   (Hugging Face)
```

### Label Column

```
click   (1 = clicked, 0 = not clicked)
```

### Feature Types

Most features are **categorical**, encoded as numerical IDs.
This means models must **treat them as categories, not numeric values**.

---

## 🧱 Week 1 – Data Exploration 

✅ Loaded a **sample of 100,000 rows** — this is intentional to protect memory.
✅ Checked:

* Column types
* Number of missing values
* Unique count per column
* Basic statistics

✅ Visualizations created:

* Class distribution plot → **Confirmed imbalance** with 83% for Not Click and 17% for Click on AD
* Category frequency distributions
* Numeric feature summaries
* Correlation overview (for numeric features)

### Key Findings

| Insight                                         | Meaning                                                     |
| ----------------------------------------------- | ----------------------------------------------------------- |
| Dataset is highly imbalanced                    | Most samples are **non-click** → must handle imbalance      |
| Features are categorical with large cardinality | Standard one-hot encoding produces **huge sparse matrices** |
| No significant missing value problems           | No strong cleaning required                                 |

---

## 🧠 Week 2 – Preprocessing Pipeline (Your Work)

### Why This Step Matters

We must **prepare the data in a reproducible and scalable way** so every teammate can train models on it.

### What Was Done

| Step                                                    | Explanation                                               | Result                                     |
| ------------------------------------------------------- | --------------------------------------------------------- | ------------------------------------------ |
| Used **Polars** instead of Pandas                       | Polars handles millions of rows efficiently               | ✅ Memory safe data loading                 |
| Converted categorical columns to `category` dtype       | Reduces memory footprint                                  | ✅ Lower RAM usage                          |
| Took a **300K sample** for balancing & pipeline testing | Safe to run locally                                       | ✅ Prototype pipeline works                 |
| Balanced classes using **Random Undersampling**         | Avoided SMOTEN (which was too heavy / caused MemoryError) | ✅ Balanced dataset without crashing        |
| One-Hot encoded categorical features                    | Prepared data for ML models                               | ✅ Sparse encoded matrix ready for training |
| Split into Train/Test                                   | Ensures fair model evaluation                             | ✅ Data is ready for modeling               |

---

## 🔥 Why We Did *Undersampling* Instead of SMOTEN

| Method            | Problem                                                | Why Undersampling Wins Here     |
| ----------------- | ------------------------------------------------------ | ------------------------------- |
| SMOTEN            | Requires pairwise distance matrix → consumes >10GB RAM | Not feasible on real hardware   |
| **Undersampling** | Simple & stable                                        | Works fast, avoids memory crash |

---

## 🧩 Finally → Data is Exported into **Train/Test** Ready Format

This means the **next team members** can directly start training models **immediately**, no preprocessing needed again.

---

## 🤝 Next Team Tasks (Model Training Phase)

### Choose and Compare Models

Recommended models to try:

| Model               | Why Try It                        | Notes                      |
| ------------------- | --------------------------------- | -------------------------- |
| **CatBoost**        | Handles categorical data natively | Strong baseline            |
| XGBoost             | Good with large sparse matrices   | Enable GPU if possible     |
| LightGBM            | Fast and memory efficient         | Works well on tabular data |
| Logistic Regression | Lightweight baseline              | After encoding only        |

### What You Need to Do

1. Import the **processed train/test data**
2. Train your model
3. Evaluate using:

   * AUC-ROC
   * Log loss
   * Precision, Recall
4. Compare model performance in a shared results sheet

---

## 📊 Final Presentation Guidance

When presenting to the instructor:

> “The main challenge was the dataset scale and imbalance.
> I handled this by using Polars for efficient loading and Random Undersampling instead of SMOTEN to avoid memory overflow.
> The output of my work is a clean, balanced, train-test ready dataset that the rest of the team can now use for model experimentation.”

---

## 🗂 Project Structure

```
CTR_Prediction/
│
├── notebooks/
│   ├── Week1_EDA.ipynb
│   └── Week2_Preprocessing.ipynb  
│
├── data/
│   ├── raw/           <-- original data
│   └── processed/     <-- balanced & encoded train/test
│
└── models/            <-- next team members will store trained models
```

---

## ✅ Summary of Your Contribution

| Abdelrahman & Renad Did                        | Why It Matters                        |
| ------------------------------ | ------------------------------------- |
| Data understanding             | Team knows what we are dealing with   |
| Efficient data loading         | Enables scaling to full dataset later |
| Balanced the dataset correctly | Prevents bias in model predictions    |
| Produced ready-to-train splits | Saves time for the modeling team      |
| Created visual diagnostics     | Supports presentation & understanding |






## 📊 EDA Highlights

| Step                | Description                                       |
| ------------------- | ------------------------------------------------- |
| 🧱 Basic Info       | Dataset structure, column types, missing values   |
| ⚖️ Label Imbalance  | `sns.countplot()` visualization of CTR ratio      |
| 🔹 Feature Analysis | Top-10 most frequent values per selected features |
| 📈 Unique Counts    | Unique value counts for all columns               |
| 🔥 Correlation      | Optional numeric-only heatmap                     |
| 🧠 Insights         | Final conclusions and recommendations             |

---

## 🧠 Key Findings

* Dataset is **imbalanced** (≈ 17 % positive class).
* All features are **categorical**, encoded as numeric IDs.
* No significant **missing values** detected.
* Future model training should address imbalance via sampling or class weights.

---

## 🛠️ Environment Setup

### Requirements

```bash
datasets
pandas
numpy
matplotlib
seaborn
```

### Install

```bash
pip install -r requirements.txt
```

### Run

```bash
jupyter notebook 01_EDA_Avazu_x1.ipynb
```

> 💡 All outputs display inline — no file or folder creation.

---

## 🧩 Project Structure

```
CTR_Prediction_ML/
├── notebooks/
│   └── 01_EDA_Avazu_x1.ipynb
├── requirements.txt
├── README.md
└── .gitignore
```

---

## 🧭 Next Steps

* [ ] Add model training pipeline (`02_Model_Training.ipynb`)
* [ ] Build Streamlit app prototype
* [ ] Save trained model for deployment

---

## 📄 License

This repository is for **academic and educational purposes only**.
Feel free to fork and adapt for learning or research use.



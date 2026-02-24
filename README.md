# 🏦 Portuguese Bank Marketing Prediction
---

##  Overview

This project builds a machine learning pipeline to predict whether a bank customer will **subscribe to a term deposit** based on historical direct marketing campaign data from a Portuguese banking institution. The goal is to help the marketing team improve conversion rates while minimizing wasted outreach efforts.

---

##  Problem Statement

Direct marketing campaigns are expensive and time-consuming. By predicting which customers are most likely to subscribe to the bank's product, we can:
- Prioritize high-value leads
- Personalize marketing strategies
- Reduce unnecessary contact with low-probability customers

---

##  Dataset

- **Source:** [UCI Bank Marketing Dataset](https://archive.ics.uci.edu/ml/datasets/Bank+Marketing) (`bank-additional-full.csv`)
- **Separator:** Semicolon (`;`)
- **Features:** Customer demographics, financial info, campaign contact history, and macroeconomic indicators
- **Target:** `y` — whether the client subscribed (`yes` / `no`)

### Key Features
| Feature | Description |
|---|---|
| `age` | Customer age |
| `job` | Type of job |
| `education` | Education level |
| `duration` | Last contact duration (seconds) |
| `campaign` | Number of contacts in current campaign |
| `pdays` | Days since last contact from previous campaign |
| `previous` | Number of contacts before this campaign |
| `emp.var.rate` | Employment variation rate |
| `euribor3m` | Euribor 3-month rate |
| `cons.conf.idx` | Consumer confidence index |

---

##  Tech Stack

- **Language:** Python 3
- **Libraries:** `pandas`, `numpy`, `matplotlib`, `seaborn`, `scikit-learn`

---

##  Project Workflow

### 1.  Data Loading & Exploration
- Loaded CSV with `;` delimiter
- Inspected shape, dtypes, and descriptive statistics
- Visualized class distribution and call duration impact on subscription

### 2.  Data Cleaning
- Detected and removed duplicate records
- Separated numerical and categorical columns for targeted preprocessing

### 3.  Exploratory Data Analysis (EDA)
- Boxplots for call duration vs subscription outcome
- Countplots for job type vs subscription
- Distribution plots and skewness analysis for all numerical features
- Correlation heatmap to detect multicollinearity among economic indicators

### 4.  Data Preprocessing
- **Skewness correction:** Square root transformation applied to `duration`
- **Binning numerical features:** Age, duration, campaign count, pdays, previous contacts, economic indicators (emp.var.rate, euribor3m, cons.conf.idx)
- **Ordinal Encoding:** Education (ordered from illiterate → university degree)
- **One-Hot Encoding:** Categorical columns (job, marital, contact, month, day_of_week, poutcome, loan, housing) and binned numerical columns

### 5.  Feature Selection
- **Chi-Square test** (`SelectKBest`) to identify top 10 features
- **Random Forest feature importance** for additional validation

### 6.  Train-Test Split
- 80/20 stratified split to preserve class distribution

### 7.  Hyperparameter Tuning
- `GridSearchCV` with 5-fold cross-validation on Random Forest
- Parameters tuned: `n_estimators`, `max_depth`

### 8.  Model Training
Three classifiers trained and compared:
- Logistic Regression
- Decision Tree
- Random Forest

### 9.  Model Evaluation

| Model | Accuracy | Precision (Class 1) | Recall (Class 1) | F1-Score (Class 1) |
|---|---|---|---|---|
| Logistic Regression | 90.60% | 0.68 | 0.32 | 0.43 |
| Decision Tree | 90.19% | 0.63 | 0.30 | 0.41 |
| **Random Forest**  | **90.36%** | **0.64** | **0.33** | **0.44** |

>  Due to class imbalance, evaluation focused on **F1-score and Recall** for the positive class rather than accuracy alone.

**Best Model: Random Forest** — selected for its best balance of precision and recall.

### 10.  Customer Segmentation & Marketing Actions

Customers were scored with subscription probabilities and segmented:

| Probability Range | Segment | Action |
|---|---|---|
| ≥ 0.70 | High Priority |  Call Immediately |
| 0.50 – 0.70 | Medium Priority | 📧 Send Email/SMS |
| < 0.50 | Low Priority |  No Campaign |

---

##  Key Insights & Recommendations

- **Call duration** is a strong indicator — longer calls correlate with subscriptions
- **Target high-probability customers** first to maximize ROI
- **Personalize offers** based on customer demographics and economic context
- **Optimize contact frequency** — excessive calls reduce conversion
- **Leverage economic indicators** (Euribor rate, employment variation) to time campaigns better
- **Explain product benefits clearly** during calls

---

##  Repository Structure

```
PRCP-1000-PortugeseBank/
│
├── Data/
│   └── bank-additional/
│       └── bank-additional-full.csv
│
├── PRCP-1000-PortugeseBank.ipynb   # Main notebook
└── README.md
```

---

##  How to Run

1. Clone the repository:
   ```bash
   git clone https://github.com/<your-username>/PRCP-1000-PortugeseBank.git
   cd PRCP-1000-PortugeseBank
   ```

2. Install dependencies:
   ```bash
   pip install pandas numpy matplotlib seaborn scikit-learn jupyter
   ```

3. Launch the notebook:
   ```bash
   jupyter notebook PRCP-1000-PortugeseBank.ipynb
   ```

4. Update the dataset path in the notebook to match your local file location.

---

##  Contact

**S K Yuvaraja** — yuvarajakannappan@gmail.com

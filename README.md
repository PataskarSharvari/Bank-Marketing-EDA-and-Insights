# 🏦 EDA in Banking Dataset using Python

## 📘 Project Overview

This project performs **Exploratory Data Analysis (EDA)** on a subset of the **Bank Marketing Dataset** from the [UCI Machine Learning Repository](https://archive.ics.uci.edu/ml/citation_policy.html).

The dataset contains information on **direct marketing campaigns (phone calls)** conducted by a Portuguese banking institution.  
The goal is to analyze client data and determine which factors influence whether a client will subscribe to a **term deposit**.

Through this EDA, we aim to uncover insights into client behavior and campaign effectiveness, helping improve future marketing strategies.

---

## 🧾 Dataset Description

### 📚 Source

- **Dataset Name:** Bank Marketing Dataset  
- **Source:** [UCI ML Repository](https://archive.ics.uci.edu/ml/citation_policy.html)  
- **Reference:** Moro et al., 2014  
- **License:** Publicly available for research and education  

### 📂 Files Used

- `bank-additional-full.csv` — Full dataset (41,188 rows × 21 columns)

---

### 📊 Features

#### Input Features

| Feature | Description | Type |
|----------|--------------|------|
| age | Client's age in years | Numeric |
| job | Type of job (admin., blue-collar, management, etc.) | Categorical |
| marital | Marital status (divorced, married, single, unknown) | Categorical |
| education | Education level (basic, high.school, university.degree, etc.) | Categorical |
| default | Has credit in default? | Categorical |
| housing | Has housing loan? | Categorical |
| loan | Has personal loan? | Categorical |
| contact | Contact communication type (cellular, telephone) | Categorical |
| month | Last contact month | Categorical |
| day_of_week | Last contact day of the week | Categorical |
| duration | Last contact duration (seconds) | Numeric |
| campaign | Number of contacts during this campaign | Numeric |
| pdays | Days since last contact from previous campaign (999 = not previously contacted) | Numeric |
| previous | Number of contacts before this campaign | Numeric |
| poutcome | Outcome of previous marketing campaign | Categorical |
| emp.var.rate | Employment variation rate (quarterly) | Numeric |
| cons.price.idx | Consumer price index (monthly) | Numeric |
| cons.conf.idx | Consumer confidence index (monthly) | Numeric |
| euribor3m | Euribor 3-month rate | Numeric |
| nr.employed | Number of employees (quarterly) | Numeric |

#### Output Feature

| Feature | Description |
|----------|-------------|
| y | Has the client subscribed a term deposit? (binary: yes/no) |

---

## 🧠 Project Objectives

- Find the **share of clients attracted** (subscribed).  
- Calculate **mean values of numerical features** among attracted clients.  
- Determine **average call duration** for attracted clients.  
- Analyze **average age among attracted and unmarried clients**.  
- Examine **average age and call duration** for different employment types.  
- Visualize relationships for better marketing insights.

---

## 🧩 Technologies & Libraries Used

| Library | Purpose |
|----------|----------|
| Python 3 | Core programming language |
| Pandas | Data handling and manipulation |
| NumPy | Numerical computation |
| Matplotlib | Data visualization |
| Seaborn | Statistical plots |
| Jupyter Notebook | Interactive analysis environment |

---

## ⚙️ Setup Instructions

### 1️⃣ Clone the Repository

```bash
git clone https://github.com/<your-username>/EDA-in-Banking-Using-Python.git
cd EDA-in-Banking-Using-Python
```

### 2️⃣ Download the Dataset

```bash
wget https://archive.ics.uci.edu/ml/machine-learning-databases/00222/bank-additional.zip
unzip -o -q bank-additional.zip
```

**Alternate link:**

```bash
wget https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/EDA_Pandas_Banking_L1/bank-additional.zip
```

### 3️⃣ Install Required Libraries

```bash
pip install pandas numpy matplotlib seaborn
```

### 4️⃣ Run the Notebook or Script

```bash
jupyter notebook
```

---

## 🔍 Steps in Analysis

### 🧹 1. Data Loading & Inspection

- Load dataset using `pandas.read_csv()`
- Check shape, columns, datatypes
- Inspect missing values and duplicates

```python
import pandas as pd

df = pd.read_csv('bank-additional/bank-additional-full.csv', sep=';')
df.info()
df.describe()
```

### 📈 2. Descriptive Statistics

```python
df.describe()  # Numerical statistics
df.describe(include=["object"])  # Categorical statistics
```

### 🗂️ 3. Data Transformation

- Convert target variable to numeric (yes → 1, no → 0)
- Sort by columns for analysis

```python
df["y"] = df["y"].map({"no": 0, "yes": 1})
df.sort_values(by=["age", "duration"], ascending=[True, False]).head()
```

### 📊 4. Exploratory Questions

**➤ Share of attracted clients**

```python
print("Share of attracted clients =", '{:.1%}'.format(df["y"].mean()))
```

**➤ Average call duration for attracted clients**

```python
df[df["y"] == 1]["duration"].mean()
```

**➤ Average age of single and attracted clients**

```python
df[(df["y"] == 1) & (df["marital"] == "single")]["age"].mean()
```

**➤ Average age and duration by job type**

```python
df.pivot_table(["age", "duration"], ["job"], aggfunc="mean")
```

### 🎨 5. Visualizations

**📊 Histograms**

```python
df["age"].hist()
df.hist(color="k", bins=30, figsize=(15,10))
```

**📦 Boxplots**

```python
df.boxplot(column="age", by="marital")
df.boxplot(column="age", by=["marital", "housing"], figsize=(20,20))
```

**🔵 Scatter Matrix**

```python
pd.plotting.scatter_matrix(
    df[["age", "duration", "campaign"]],
    figsize=(15,15),
    diagonal="kde"
)
```

---

## 📉 Insights Gained

- The share of subscribed clients ≈ **15%**.
- **Call duration** shows strong correlation with subscription success.
- **Younger and single clients** are slightly more likely to subscribe.
- **Retired and management** professions show higher conversion rates.
- **Education level** (university or professional course) increases success likelihood.

These insights help plan targeted marketing campaigns.

---

## 📊 Example Visuals

| Visualization | Description |
|---------------|-------------|
| 📦 Boxplot | Age distribution across marital statuses |
| 📈 Histogram | Distribution of call durations |
| 🔵 Scatter Matrix | Pairwise relationships among numerical variables |
| 📑 Pivot Table | Mean age and campaign count by education |

---

## 🚀 Future Scope

- Build predictive models (Logistic Regression, Random Forest, etc.)
- Apply feature encoding and scaling
- Use correlation heatmaps & outlier detection
- Develop interactive dashboards (Streamlit / Power BI)

---

## 📚 Reference

**Moro, S., Cortez, P., & Rita, P. (2014).**  
*A Data-Driven Approach to Predict the Success of Bank Telemarketing.*  
Decision Support Systems, 62, 22–31.

📄 [Link to Dataset](https://archive.ics.uci.edu/ml/citation_policy.html)

---

## 👩‍💻 Author

**Sharvari Pataskar**  

---

## ⭐ Acknowledgments

Special thanks to:

- **UCI Machine Learning Repository**
- **IBM Cognitive Class EDA Course**

for providing open datasets and educational resources.

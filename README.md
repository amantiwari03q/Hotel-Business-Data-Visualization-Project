# 🏨 Hotel Business Data Visualization & Cancellation Analysis

> **An end-to-end exploratory data analysis project focused on hotel booking behavior, seasonality, cancellation patterns, stay duration, and booking lead time.**

![Python](https://img.shields.io/badge/Python-3.x-blue?logo=python)
![Pandas](https://img.shields.io/badge/Pandas-Data%20Analysis-150458?logo=pandas)
![NumPy](https://img.shields.io/badge/NumPy-Numerical%20Computing-013243?logo=numpy)
![Matplotlib](https://img.shields.io/badge/Matplotlib-Visualization-orange)
![Seaborn](https://img.shields.io/badge/Seaborn-Visualization-4C72B0)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?logo=jupyter)

---

## 📌 Project Overview

This project investigates hotel booking data to understand **customer booking behavior and cancellation patterns** across City Hotels and Resort Hotels.

The analysis focuses on three major business questions:

* Which hotel type receives the highest number of bookings?
* How does **length of stay** influence cancellation behavior?
* How does **booking lead time** affect cancellation rates?

The project combines **data cleaning, exploratory data analysis, statistical aggregation, and data visualization** to convert raw booking data into actionable business insights.

---

## 🎯 Business Objective

The primary objective is to identify patterns in hotel bookings and cancellations that can help hotel businesses improve:

* 📈 Revenue planning
* 🏨 Inventory management
* 👥 Staff allocation
* 💰 Pricing strategies
* 🔄 Cancellation policies
* 📅 Seasonal demand planning
* 🎯 Customer targeting

---

## 📊 Dataset

The dataset contains approximately **119K hotel booking records** covering the period **2017–2019**.

### Key Data Attributes

| Category              | Examples                    |
| --------------------- | --------------------------- |
| Hotel Information     | Hotel Type                  |
| Booking Information   | Lead Time, Market Segment   |
| Stay Information      | Weekend Nights, Week Nights |
| Customer Information  | Adults, Children, Babies    |
| Financial Information | ADR                         |
| Cancellation          | Is_Canceled                 |
| Meal                  | Meal Type                   |
| Distribution          | Agent, Company              |
| Arrival               | Month, Year, Date           |

---

## 🛠️ Tech Stack

### Programming & Analysis

* Python
* Pandas
* NumPy

### Data Visualization

* Matplotlib
* Seaborn

### Development Environment

* Jupyter Notebook

---

## 🔄 Data Preparation & Cleaning

Before performing the analysis, the dataset was examined for missing values, duplicate records, undefined values, and anomalous observations.

### Cleaning steps included:

```python
# Remove duplicate records
df = df.drop_duplicates()

# Remove negative ADR values
df = df[df['adr'] >= 0]

# Remove bookings with zero guests
df = df[
    (df['adults'] + df['children'] + df['babies']) > 0
]

# Handle missing children values
df['children'] = df['children'].fillna(0)

# Calculate total stay duration
df['total_stay'] = (
    df['stays_in_weekend_nights']
    + df['stays_in_week_nights']
)
```

### Data Quality Checks

The original dataset contained:

* **119,390 rows**
* **29 columns**
* **33,261 duplicate records**
* Missing values in selected columns
* Undefined meal values
* Negative ADR records
* Records with zero guests

After preprocessing, the dataset was reduced to approximately **85,963 valid booking records**.

---

# 📈 Exploratory Data Analysis

## 1. Hotel Booking Distribution

The analysis shows that **City Hotel** receives a larger share of bookings than Resort Hotel.

### Key Finding

* 🏙️ City Hotel — **60.98%**
* 🌴 Resort Hotel — **39.02%**

This indicates stronger overall booking demand for City Hotels within the analyzed dataset.

---

## 2. Monthly Booking Analysis

Monthly booking trends were analyzed to identify demand patterns and seasonality.

### Key Findings

* **October** recorded the highest number of bookings.
* **March** recorded the lowest number of bookings.
* Booking volumes vary significantly throughout the year.

### Business Implications

During high-demand periods, hotels can consider:

* Dynamic pricing
* Increased staffing
* Better inventory planning
* Advance room allocation

During low-demand periods:

* Promotional campaigns
* Special packages
* Discounts
* Targeted marketing

can be used to stimulate demand.

---

# 🔄 3. Cancellation Rate Analysis

Cancellation behavior was compared across hotel types.

| Hotel Type   | Cancellation Rate |
| ------------ | ----------------: |
| City Hotel   |        **30.22%** |
| Resort Hotel |        **23.49%** |

City Hotel shows a higher cancellation rate than Resort Hotel.

This makes cancellation management particularly important for City Hotel operations.

---

# 🛏️ 4. Stay Duration vs Cancellation

The relationship between **total stay duration** and cancellation behavior was investigated separately for both hotel types.

### City Hotel

Cancellation rates generally increase as the length of stay becomes longer, with particularly high cancellation percentages observed for longer stays.

For example:

* 1 night → **22.37%**
* 7 nights → **37.67%**
* 10 nights → **58.51%**
* 14 nights → **70.45%**

### Resort Hotel

The Resort Hotel shows a different pattern, with cancellation rates increasing during shorter-to-medium stay durations and then becoming more variable at longer durations.

### Possible Business Reasons

Longer bookings may have:

1. Greater uncertainty between booking date and arrival date.
2. Higher total booking value, increasing the likelihood of customers changing plans.

---

# ⏳ 5. Lead Time vs Cancellation

**Lead time** represents the number of days between the booking date and the customer's arrival date.

To analyze this relationship, bookings were divided into lead-time groups:

```python
bins = [0, 7, 30, 60, 90, 180, 365, np.inf]

labels = [
    '0-7',
    '8-30',
    '31-60',
    '61-90',
    '91-180',
    '181-365',
    '366+'
]

df['lead_time_group'] = pd.cut(
    df['lead_time'],
    bins=bins,
    labels=labels
)
```

### City Hotel

Cancellation rate increases strongly with booking lead time:

| Lead Time    | Cancellation Rate |
| ------------ | ----------------: |
| 0–7 days     |            10.54% |
| 8–30 days    |            27.96% |
| 31–60 days   |            33.09% |
| 61–90 days   |            33.88% |
| 91–180 days  |            36.73% |
| 181–365 days |            45.18% |
| 366+ days    |        **52.82%** |

### Resort Hotel

| Lead Time    | Cancellation Rate |
| ------------ | ----------------: |
| 0–7 days     |             5.95% |
| 8–30 days    |            20.83% |
| 31–60 days   |            29.20% |
| 61–90 days   |            30.38% |
| 91–180 days  |            32.13% |
| 181–365 days |            34.84% |
| 366+ days    |            21.39% |

> **Note:** The 366+ Resort Hotel group contains relatively fewer bookings, so the result should be interpreted cautiously.

---

# 💡 Key Business Insights

### Insight 1 — City Hotels dominate booking volume

City Hotels account for approximately **61% of bookings**, indicating stronger overall demand.

### Insight 2 — October is the peak booking month

October has the highest booking volume, making it an important period for revenue and capacity planning.

### Insight 3 — City Hotels have higher cancellation risk

The City Hotel cancellation rate is approximately **30.22%**, compared with **23.49%** for Resort Hotels.

### Insight 4 — Long stays can have higher cancellation risk

Longer City Hotel stays show substantially higher cancellation rates.

### Insight 5 — Far-ahead City Hotel bookings are high-risk

Cancellation rates reach approximately **45.18% for 181–365 day bookings** and **52.82% for 366+ day bookings**.

---

# 🚀 Business Recommendations

## 1. Manage Long-Lead City Hotel Bookings

For bookings made far in advance, hotels can consider:

* Advance confirmation reminders
* Deposits for high-risk bookings
* Partially non-refundable rate plans
* Flexible but higher-priced cancellation options
* Rescheduling incentives

---

## 2. Optimize Peak-Season Operations

October should receive additional attention for:

* Room inventory
* Staff planning
* Dynamic pricing
* Revenue optimization
* Marketing allocation

---

## 3. Improve Low-Season Demand

March can be targeted with:

* Promotional offers
* Weekend packages
* Seasonal discounts
* Targeted digital marketing campaigns

---

## 4. Develop Cancellation-Aware Pricing

Hotels can introduce differentiated booking options:

**Flexible Rate**
→ Higher price + flexible cancellation

**Standard Rate**
→ Moderate price + defined cancellation window

**Non-Refundable Rate**
→ Lower price + limited cancellation flexibility

---

# 📁 Project Structure

```text
Hotel-Business-Data-Visualization/
│
├── 📓 Hotel_Business_Data_Visualization.ipynb
│
├── 📊 hotel_bookings_data.csv
│
├── 📄 Hotel_Business_Data_Visualization_Report.pdf
│
├── 🎥 Project_Presentation.mp4
│
└── 📖 README.md
```

---

# 📌 Project Workflow

```text
Raw Dataset
     ↓
Data Loading
     ↓
Data Quality Assessment
     ↓
Missing Value Handling
     ↓
Duplicate Removal
     ↓
Anomaly Detection
     ↓
Feature Engineering
     ↓
Exploratory Data Analysis
     ↓
Data Visualization
     ↓
Business Insights
     ↓
Recommendations
```

---

# 📚 Skills Demonstrated

* Data Cleaning
* Exploratory Data Analysis (EDA)
* Missing Value Handling
* Duplicate Detection
* Anomaly Detection
* Feature Engineering
* GroupBy & Aggregation
* Categorical Analysis
* Time-Series / Monthly Analysis
* Data Visualization
* Business Insight Generation
* Data-Driven Recommendations

---

# 👨‍💻 Author

**Aman Tiwari**

**Data Analyst | Business Intelligence**

Focused on transforming raw data into meaningful insights and business decisions.

---

⭐ **If you found this project useful, consider giving the repository a star!**

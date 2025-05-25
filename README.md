# Bank Credit Card Launch Analysis

This repository showcases an end-to-end data analytics project focused on identifying key customer segments and validating the launch of a new credit card for a fictional bank. The dataset was sourced from [DataLelo](https://data.lelo.ai) and provided as part of a Codebasics.io mentor challenge.

---

## Datasets Used

Data was extracted from a **MySQL database** (`e_master_card`) that included the following tables:

### 1. `customers`
Contains demographic and financial attributes.

- `customer_id`: Unique ID
- `age`, `gender`, `marital_status`
- `occupation`: Profession type
- `annual_income`: Cleaned by imputing occupation-wise medians

### 2. `credit_profiles`
Contains credit behavior and creditworthiness indicators.

- `customer_id`: Foreign key
- `credit_score`, `credit_limit`
- `num_credit_cards`, `credit_utilization_ratio`

### 3. `transactions`
Captures detailed transaction data.

- `transaction_id`, `customer_id`
- `transaction_amount`, `transaction_type`, `merchant_category`, `transaction_date`

### 4. `avg_transactions_after_campaign`
Post-campaign A/B testing results, containing average daily transaction values for control and test groups.

---

## Data Cleaning

- Checked for nulls in all key datasets.
- Replaced `annual_income = 0` by computing **occupation-wise medians**.
- Standardized formatting for transaction categories and date columns.
- Removed inconsistencies in text fields (e.g., casing).

---

## Data Transformation

- Joined `customers`, `credit_profiles`, and `transactions` on `customer_id`.
- Created new features:
  - Total transactions per customer
  - Average transaction amount
  - Days since last transaction
  - Credit score segmentation
- Grouped customers into **age brackets**, **income bands**, and **credit tiers**.
- Aggregated merchant category preferences by age and income groups.

---

## Analytics Conducted

### 1. **Customer Profiling**
- Visualized demographic distributions by age, income, occupation.
- Identified financial behaviors of different age groups.
- Segmented customers into active/inactive based on recent transaction history.

### 2. **Behavioral Insights**
- Transaction frequency and preferred merchant categories were analyzed.
- Payment methods were grouped (credit card, debit card, UPI, etc.).
- Spending habits linked with credit scores and occupation.

---

## Key Finding: The Untapped 18–25 Age Group

This segment made up **~26%** of the customer base and demonstrated the following:

| Metric | Insight |
|--------|---------|
| Avg Income | < ₹50,000 |
| Credit History | Very limited |
| Credit Usage | Low credit card adoption |
| Top Spends | Electronics, Fashion & Apparel, Beauty |

➡️ Recommended as ideal for a **starter credit card** with:
- Low credit limit
- No annual fee
- Cashback rewards in their top spending categories

---

## 📐 A/B Testing: Measuring Campaign Effectiveness

### Objective:
To assess if offering the new credit card increased transaction behavior.

- **Sample size** calculated using `statsmodels` power analysis.
- Used **40 customers in control** and **40 in test** group due to budget constraints.
- Campaign ran for 2 months (09-Oct-2023 to 11-Dec-2023).
- Daily averages stored in `avg_transactions_after_campaign`.

### Hypothesis:
- **H₀**: No difference in average transaction amounts.
- **H₁**: Test group will have higher average transactions.

### Results:
- **Control Group Mean**: ₹248.94
- **Test Group Mean**: ₹370.54
- **Z-score**: 3.73 > 1.64 (critical z)
- **p-value**: 0.000096 < 0.05

**Result**: Rejected H₀. The campaign significantly increased spending.

### 95% Confidence Interval for Test Group:
`₹354.80 – ₹386.28`

---

## Recommendations

- 🎯 **Target younger segments (18–25)** with entry-level cards.
- 🛍️ Offer rewards on electronics, fashion, and personal care.
- 📲 Promote credit education and usage incentives.
- 📈 Re-run campaign with larger sample size for scaling insights.

---

## Tech Stack

- **Python**: `pandas`, `numpy`, `matplotlib`, `seaborn`, `scipy`, `statsmodels`
- **SQL**: `MySQL` used for raw data extraction
- **Jupyter Notebook**: Analysis and storytelling
- **Power Analysis**: A/B test sample size with `tt_ind_solve_power`

---

## 📁 Folder Structure
Bank-Credit-Card-Project
┣ Bank Credit Card Project.ipynb
┗ 📄 README.md

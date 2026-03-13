# CRM Analytics: RFM Segmentation & Predictive CLTV Modeling with Elo Transaction Data

## Project Overview

This project analyzes large-scale transaction-level card data from the **Elo Merchant Category Recommendation** dataset from a **CRM analytics perspective**.

Rather than approaching the dataset purely as a recommendation problem, this study reframes it as a **customer value and loyalty analysis problem**. By transforming millions of transaction records into customer-level behavioral features, the project aims to uncover actionable insights for **customer segmentation, retention strategy, churn risk evaluation, and future value prediction**.

The analysis begins with **RFM (Recency, Frequency, Monetary) segmentation** to describe past customer behavior and then transitions into **predictive CLTV modeling** using **BG/NBD** and **Gamma-Gamma** models to estimate forward-looking customer value.

---

## Project Objectives

The main goals of this project are:

- Transform transaction-level card data into customer-level insights
- Apply **RFM analysis** to measure customer loyalty and engagement
- Segment customers based on behavioral and transactional characteristics
- Analyze revenue concentration across customer groups
- Identify high-value, high-risk, and growth-opportunity segments
- Estimate **Customer Lifetime Value (CLTV)** using probabilistic models
- Compare descriptive segmentation with predictive customer valuation
- Translate analytical findings into **business-oriented CRM strategies**

---

## Dataset

This project uses the **Elo Merchant Category Recommendation** dataset from Kaggle:

**Dataset Link:**  
https://www.kaggle.com/competitions/elo-merchant-category-recommendation

### Main Tables Used

- `historical_transactions.csv`
- `new_merchant_transactions.csv`
- `train.csv`

---

## Dataset Description

The Elo dataset contains millions of card transaction records, where each row represents a single transaction linked to a customer card.

### Key Variables

| Column | Description |
|--------|-------------|
| `card_id` | Unique identifier for each customer card |
| `purchase_date` | Date and time of the transaction |
| `purchase_amount` | Normalized transaction amount |
| `authorized_flag` | Indicates whether the transaction was authorized |
| `merchant_category_id` | Merchant category identifier |
| `merchant_id` | Unique merchant identifier |
| `installments` | Number of installments |
| `month_lag` | Time difference from reference month |

### Dataset Size

- **Historical Transactions:** 29,112,361 rows
- **New Merchant Transactions:** 1,963,031 rows
- **Train Dataset:** 201,917 rows

This clearly shows that the dataset is highly **transaction-driven**, making customer-level aggregation essential before conducting CRM analysis.

---

## What I Learned from This Project

Through this project, I practiced and improved my skills in:

- transforming large-scale transaction data into customer-level features
- applying **RFM analysis** for behavioral segmentation
- interpreting customer purchasing patterns from a CRM perspective
- identifying customer lifecycle stages and churn risk signals
- analyzing revenue concentration and segment-level financial contribution
- implementing **BG/NBD** and **Gamma-Gamma** models for predictive CLTV
- combining descriptive and predictive customer analytics
- translating data findings into strategic marketing and retention recommendations

---

## Technologies & Libraries Used

- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Scikit-learn
- Lifetimes

---

## Project Workflow

The project follows two main stages:

### 1. Descriptive CRM Analytics with RFM
- Data loading and preprocessing
- Filtering authorized transactions
- Converting transaction dates
- Creating a positive monetary variable
- Aggregating transaction data to the customer level
- Calculating **Recency, Frequency, Monetary**
- Assigning RFM scores
- Creating customer segments
- Interpreting segment-level behavior and revenue structure

### 2. Predictive Customer Valuation with CLTV
- Preparing customer summary data for lifetime models
- Estimating expected future transaction frequency with **BG/NBD**
- Estimating expected average profit with **Gamma-Gamma**
- Calculating **3-month CLTV**
- Creating CLTV segments
- Comparing **RFM segments vs CLTV segments**
- Evaluating survival probability and financial sustainability

---

## Data Preprocessing

Before customer-level analysis, several preprocessing steps were applied:

- Kept only **authorized transactions**
- Converted `purchase_date` into datetime format
- Created a positive monetary variable:  
  `purchase_amount_new = purchase_amount + 1`
- Removed unnecessary columns after transformation
- Aggregated raw transaction-level data to customer level

This step was especially important because the original `purchase_amount` variable contains normalized negative values, which are not directly suitable for probabilistic lifetime models.

---

## RFM Analysis

### RFM Metrics

The following customer-level metrics were calculated:

- **Recency** → Days since the last transaction
- **Frequency** → Total number of transactions
- **Monetary** → Total spending amount

### RFM Scoring

Customers were scored into quintiles:

- Lower recency → higher score
- Higher frequency → higher score
- Higher monetary → higher score

Then, combined RF scores were mapped into customer segments.

### RFM Segments

The following segments were created:

- Champions
- Loyal Customers
- Potential Loyalists
- New Customers
- Promising
- Need Attention
- About to Sleep
- At Risk
- Cant Lose
- Hibernating

---

## Key RFM Insights

Some of the most important findings from the RFM stage were:

- **Champions** and **Loyal Customers** are the strongest revenue-generating groups.
- **Cant Lose** customers have extremely high historical value but also strong churn risk.
- **At Risk** customers represent a major retention concern.
- **Hibernating** is the largest segment by customer count, but its strategic value is relatively low.
- Revenue is highly concentrated in a limited number of top-performing segments.

### Revenue Concentration Result

The top four RFM segments:

- Champions
- Loyal Customers
- Cant Lose
- At Risk

generate nearly **80% of total revenue**.

This result highlights the importance of **value-based marketing and retention prioritization**.

---

## Business Interpretation of RFM Segments

This segmentation framework provides a strong foundation for CRM strategy:

- **Champions:** retain with VIP benefits, loyalty rewards, and premium offers
- **Loyal Customers:** grow through upsell and cross-sell strategies
- **Cant Lose:** prioritize urgent win-back campaigns
- **At Risk:** apply preventive retention strategies
- **Potential Loyalists:** nurture toward higher-value tiers
- **Hibernating:** approach with low-cost reactivation campaigns

Overall, the RFM analysis provides a clear behavioral view of customer lifecycle dynamics.

---

## CLTV Modeling

To move beyond descriptive analytics, the project transitions into **predictive Customer Lifetime Value modeling**.

### Why CLTV?

RFM explains past behavior, but it does not answer:

- Who is likely to stay active?
- Who will generate future revenue?
- Which customers justify higher retention investment?
- Which historically strong customers are actually close to churn?

To answer these questions, **BG/NBD** and **Gamma-Gamma** models were used.

---

## CLTV Modeling Framework

### Models Used

#### 1. BG/NBD (Beta-Geometric / Negative Binomial Distribution)
Used to estimate:

- expected future transaction frequency
- probability that a customer is still active

#### 2. Gamma-Gamma Model
Used to estimate:

- expected average profit per transaction

These two outputs were combined to estimate **3-month CLTV** for each customer.

---

## Key CLTV Insights

The predictive CLTV stage revealed several important patterns:

- **Segment A** customers generate the majority of total predicted lifetime value.
- **Segment D** customers have very low predicted value and high churn risk.
- Some customers with high historical frequency still show **very low future value**, proving that past activity does not always guarantee future profitability.
- CLTV adds an important **forward-looking layer** that RFM alone cannot capture.

### Revenue Concentration by CLTV Segment

- **Segment A** alone generates approximately **63.6%** of total predicted CLTV.
- **Segment B** contributes around **22.9%**
- **Segment C** contributes around **11.3%**
- **Segment D** contributes only **2.1%**

This confirms a strong **Pareto-like customer value structure**.

---

## RFM vs CLTV Combined Analysis

One of the most valuable parts of the project was combining **RFM segmentation** with **CLTV prediction**.

This comparison showed that:

- **Champions** strongly align with the highest CLTV segment
- **Loyal Customers** also show strong future financial sustainability
- **Potential Loyalists** represent real growth opportunities
- **Cant Lose** customers often look highly valuable historically, but many of them have lower survival probability and lower predicted future value

This means:

> RFM tells us what customers did in the past, while CLTV tells us what they are likely to do in the future.

That combined perspective makes the analysis much more strategic and financially meaningful.

---

## Survival Probability & Churn Risk

The BG/NBD model also provides **probability alive**, which serves as a behavioral indicator of churn risk.

### Main Insight

- High-CLTV customers also tend to have very high survival probability
- Low-CLTV customers show a much lower probability of staying active
- Churn risk is not evenly distributed across customers

This makes the project especially useful for **retention prioritization and budget allocation**.

---

## Strategic Customer Action Framework

Based on the combined RFM + CLTV insights:

| Segment | Financial Value | Survival Risk | Recommended Action |
|--------|------------------|--------------|--------------------|
| A | Very High | Very Low | Loyalty retention & premium offers |
| B | High | Low | Upsell & cross-sell campaigns |
| C | Medium | Moderate | Engagement reinforcement |
| D | Low | High | Cost-controlled reactivation |

This framework helps align marketing effort with expected financial return rather than historical behavior alone.

---

## Executive Summary

This project demonstrates how large-scale transaction-level card data can be transformed into a **customer-centric CRM analytics framework**.

First, RFM segmentation was used to identify behavioral customer groups and reveal patterns in loyalty, spending, and churn risk. Then, BG/NBD and Gamma-Gamma models were applied to estimate forward-looking CLTV, adding a financial and predictive dimension to customer evaluation.

The results show that:

- customer value is highly concentrated
- high-value segments drive most of the revenue
- some historically valuable customers are actually at strong future risk
- combining **RFM + CLTV** creates a much more strategic foundation for retention, targeting, and CRM decision-making

---

## Limitations

Although the project provides strong insights, there are some limitations:

- The CLTV model relies only on transactional history
- Demographic and external behavioral variables are not included
- BG/NBD assumes independence between purchase frequency and dropout probability
- Gamma-Gamma assumes independence between spending and transaction frequency
- Seasonality, campaign effects, and macroeconomic conditions are not explicitly modeled

Therefore, the results should be interpreted as **behavior-driven predictive estimates**, not absolute financial truth.

---

## Future Improvements

Possible next steps for improving this project include:

- adding merchant diversity and category-level features
- incorporating seasonality and campaign response signals
- testing survival-analysis or machine-learning-based CLTV alternatives
- building cohort-level CLTV monitoring
- integrating campaign ROI and response data
- creating a dashboard for dynamic customer strategy tracking

---

## 📂 Project Structure

```bash
crm-rfm-cltv-elo/
│
├── elo_crm_rfm_cltv_analysis.ipynb
├── new_customers.csv
├── cltv_prediction.csv
└── README.md

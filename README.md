# E-Commerce Customer Churn & Spending Analysis (SQL & Econometrics)

## Project Overview
Keeping customers happy and encouraging them to spend more are two of the biggest challenges in e-commerce. Using real transaction data from **Olist** (a large Brazilian online marketplace with 96,478 delivered orders across 93,358 unique customers from 2016 to 2018), this project combines **SQL** with **econometric models** in Python to answer three practical business questions:

1. **Customer Churn & Dissatisfaction:** How much do late deliveries, long shipping times, and high shipping costs increase the chances that a customer leaves a bad (1–2 star) review?
2. **Customer Spending & Payment Plans:** How do repeat purchases and paying in monthly credit card installments affect how much a customer spends overall and their chances of becoming a **Top 20%** spender?
3. **Product Category Differences:** Which product categories bring in the most revenue, and how do delivery delays and customer dissatisfaction vary across different types of products?

* **Dataset Source:** [Brazilian E-Commerce Public Dataset by Olist (Kaggle)](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce)

## Tools & Methods
* **SQL (SQLite3):** Joined 9 relational CSV tables, aggregated order logs to the customer level, calculated delivery delays, and ranked product categories.
* **Econometrics (Python / statsmodels):** Estimated Linear Probability Models (LPM) and Log-Linear OLS regressions with Huber-White robust standard errors, State and Year Fixed Effects, and a Logistic Regression (Logit) robustness check.

## Basic Statistics & Main Findings

### Basic Statistics (N = 93,350 Customers)
* **Low Repeat Retention:** Customers place an average of **1.033 orders**—only **3.0%** buy more than once.
* **Dissatisfaction & Delays:** **12.6%** leave a bad review (1–2 stars). Customers wait an average of **12.6 days** for delivery, and **8.3%** receive their order *after* the promised deadline.
* **Spending & Payments:** Average spend is **148.64 BRL** (median: **89.90 BRL**; Top 20% cutoff: **187.00 BRL**). **77.2%** pay by credit card (averaging **2.94 monthly installments**).

### What Drives Customer Dissatisfaction? (LPM & Logit)
* **Late Deliveries Cause Churn:** Holding transit days, shipping costs, and state fixed effects constant, missing the promised delivery date increases the probability of a 1–2 star review by **31.39 percentage points**. Bad reviews jump from **9.0%** on on-time orders to **52.3%** on late orders.
* **Deadlines Matter More Than Speed:** Each extra day in transit only increases dissatisfaction by **0.58 percentage points**. Customers accept longer waits to remote regions as long as the promised deadline is met.
* **Shipping Cost Penalty:** Controlling for state fixed effects, higher shipping fees relative to item price significantly increase dissatisfaction. Logit marginal effects confirm these results.

### What Drives Customer Spending? (Log-Spend OLS & Top 20% LPM)
* **Repeat Buyers Spend Double:** Returning customers spend **102.1% more** than one-time buyers and are **28.96 percentage points** more likely to be in the Top 20% of spenders.
* **Installments Boost Basket Size:** Each additional monthly credit card installment increases total spending by **14.54%** and raises the probability of being a Top 20% spender by **5.03 percentage points**.

### Product Category Differences (SQL Window Functions)
* **Quality vs. Logistics Issues:** Top-grossing goods like `health_beauty` have low dissatisfaction (**12.38%**) despite a **9.06%** delay rate. Conversely, `bed_bath_table` (**18.11%**), `furniture_decor` (**18.01%**), and `computers_accessories` (**17.02%**) have the highest dissatisfaction despite fewer shipping delays, pointing to product quality and sizing issues.

## Business Recommendations
1. **Buffer Delivery Estimates:** Add 2–3 safety days to checkout delivery estimates, as missed deadlines hurt far more than longer expected transit times.
2. **Promote Installment Thresholds:** Offer interest-free 6x–10x installment plans on carts over 180 BRL to help shoppers afford higher-priced items.
3. **Audit Home & Tech Listings:** Require stricter sizing and quality details in `bed_bath_table`, `furniture_decor`, and `computers_accessories`.

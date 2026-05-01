# Customer Purchase Behavior Analysis 🛍️

An end-to-end data analytics project analyzing customer shopping patterns, preferences, and purchase drivers to support data-driven marketing and product optimization decisions.

---

## 📋 Quick Overview

| Aspect | Details |
|--------|---------|
| **Dataset** | 3,900 customer transactions with 18 attributes |
| **Time Period** | Historical customer behavior data |
| **Key Metrics** | Revenue, purchase frequency, customer segments, product performance |
| **Technologies** | Python, SQL, Power BI, BigQuery, Pandas, NumPy |
| **Project Type** | End-to-End Analytics (ETL + Analysis + Visualization) |

---

## 🎯 Business Problem Statement

A leading retail company is looking to optimize its business strategy by understanding customer shopping behavior across different demographics, product categories, and sales channels. The key business question:

> **"How can the company leverage consumer shopping data to identify trends, improve customer engagement, and optimize marketing and product strategies?"**

### Key Business Challenges:
- ❓ Identify which factors (discounts, reviews, seasons, payment methods) drive customer purchases
- 📊 Understand customer segmentation and loyalty patterns
- 💰 Optimize revenue by identifying high-value customer segments
- 🎁 Improve product strategy based on category and seasonal performance
- 🔄 Increase repeat purchase rates and customer lifetime value

---

## 📁 Project Structure

```
customer-purchase-behavior-analysis/
│
├── README.md                          # Project documentation
├── requirements.txt                   # Python dependencies
│
├── 📂 data/
│   ├── raw/
│   │   └── customer_shopping_behavior.csv    # Raw dataset (3,900 records)
│   └── processed/
│       └── customer_behavior_cleaned.csv     # Cleaned & transformed data
│
├── 📂 notebooks/
│   └── Customer_shopping_behaviour_analysis.ipynb
│       ├── Data Loading & Exploration
│       ├── Data Cleaning & Quality Checks
│       ├── Feature Engineering
│       ├── Age Group Segmentation
│       ├── Purchase Frequency Transformation
│       └── BigQuery Integration
│
├── 📂 sql/
│   └── customer_behaviour_sql_queries.sql
│       ├── Q1: Revenue by Gender
│       ├── Q2: Discount Usage Analysis
│       ├── Q3: Top 5 Products by Review Rating
│       ├── Q4: Shipping Type Comparison
│       ├── Q5: Subscription Impact Analysis
│       ├── Q6: Discount Rate by Product
│       ├── Q7: Customer Segmentation (New/Returning/Loyal)
│       ├── Q8: Top 3 Products per Category
│       ├── Q9: Repeat Buyer Subscription Correlation
│       └── Q10: Revenue by Age Group
│
├── 📂 dashboards/
│   └── Customer_Purchase_Behavior_Dashboard.pbix
│       ├── Executive Summary KPIs
│       ├── Revenue Analytics by Category & Age Group
│       ├── Customer Segmentation Insights
│       ├── Seasonal Trends Analysis
│       ├── Discount Impact Assessment
│       └── Payment Method Preferences
│
└── 📂 reports/
    ├── Project_Report.md              # Detailed findings & recommendations
    └── Presentation_Slides.pptx       # Stakeholder presentation
```

---

## 🔍 Data Overview

### Dataset Dimensions
- **Records:** 3,900 customer transactions
- **Features:** 18 attributes covering customer demographics, purchase behavior, and transaction details

### Key Columns
| Column | Description | Type |
|--------|-------------|------|
| `customer_id` | Unique customer identifier | Integer |
| `age` | Customer age | Integer |
| `gender` | Male/Female | Categorical |
| `age_group` | Segmented age bracket (Young Adult, Adult, Middle-aged, Senior) | Categorical |
| `category` | Product category (Clothing, Accessories, Footwear, Outerwear) | Categorical |
| `item_purchased` | Specific product name | Categorical |
| `purchase_amount_usd` | Transaction amount | Float |
| `review_rating` | Product review (1-5 scale) | Float |
| `discount_applied` | Yes/No flag | Categorical |
| `subscription_status` | Subscription status | Categorical |
| `previous_purchases` | Count of prior transactions | Integer |
| `shipping_type` | Delivery method (Standard, Express, 2-Day, etc.) | Categorical |
| `frequency_of_purchases` | Purchase cadence (Weekly, Monthly, Quarterly, etc.) | Categorical |
| `purchase_frequency_days` | Numerical conversion of frequency | Integer |
| `payment_method` | PayPal, Credit Card, Debit Card, Venmo, etc. | Categorical |
| `season` | Fall, Winter, Spring, Summer | Categorical |

---

## 🛠️ Project Phases

### Phase 1: Data Preparation & Modeling (Python)

**Objective:** Clean, transform, and engineer features for analysis

#### Data Cleaning Steps:
```python
✓ Loaded 3,900 customer records
✓ Verified data completeness (no missing values in critical fields)
✓ Handled missing Review Ratings by imputing category-wise medians
✓ Standardized column names to snake_case format
✓ Validated data types and ranges
```

#### Feature Engineering:
```python
✓ Age Group Creation
  - Segmented ages into 4 quartile-based groups
  - Labels: Young Adult, Adult, Middle-aged, Senior
  
✓ Purchase Frequency Conversion
  - Mapped text-based frequencies to numerical days
  - Examples: Weekly→7, Fortnightly→14, Monthly→30, Annually→365
  
✓ Duplicate Detection
  - Identified & removed redundant 'Promo Code Used' column
  - Confirmed Discount Applied = Promo Code Used relationship
```

#### Output:
- Cleaned dataset with 17 optimized features
- Uploaded to BigQuery for scalable analysis
- Dataset ready for advanced SQL queries and visualization

---

### Phase 2: Data Analysis (SQL)

**Objective:** Extract actionable insights through structured SQL queries

#### 10 Core Business Questions Answered:

| # | Question | Key Insight |
|---|----------|------------|
| **Q1** | Revenue by Gender | Compare male vs. female spending patterns |
| **Q2** | Discount Usage | Identify price-sensitive customers who spend above average |
| **Q3** | Top 5 Products | Highest-rated products by category |
| **Q4** | Shipping Impact | Average spend difference between Standard vs. Express shipping |
| **Q5** | Subscription Value | Do subscribers spend more? Revenue impact analysis |
| **Q6** | Discount Rate by Product | Which products have highest discount penetration |
| **Q7** | Customer Segmentation | Count of New (1 purchase), Returning (2-10), Loyal (10+) customers |
| **Q8** | Category Top Performers | Top 3 products within each category by purchase count |
| **Q9** | Repeat Buyer Behavior | Subscription adoption among high-frequency buyers |
| **Q10** | Revenue by Demographics | Age-based revenue contribution and spending patterns |

#### Sample Query Insights:
```sql
-- Example: Customer Segmentation
WITH cust_seg AS (
  SELECT customer_id, previous_purchases,
    CASE
      WHEN previous_purchases = 1 THEN 'New'
      WHEN previous_purchases BETWEEN 2 AND 10 THEN 'Returning'
      ELSE 'Loyal'
    END AS customer_segment
  FROM customer_behavior.customer
)
SELECT customer_segment, COUNT(customer_id) AS no_of_customers
FROM cust_seg
GROUP BY customer_segment;
```

---

### Phase 3: Visualization & Insights (Power BI Dashboard)

**Objective:** Create interactive, stakeholder-ready dashboard

#### Dashboard Components:

**1. Executive Summary (KPIs)**
- Total Customers: 3,900
- Average Purchase Amount: $59.76
- Average Review Rating: 3.75
- Customer Subscription Rate: 27%

**2. Revenue Analytics**
- Revenue by Category: Clothing ($104K) leads, Outerwear ($19K) lowest
- Revenue by Age Group: Young Adults ($62.1K) highest spenders
- Revenue Trend by Season: Fall peaks at $60K, Summer dips to $55.8K

**3. Customer Segmentation**
- Gender Split: Male (68%) vs. Female (32%)
- Subscription Adoption: 27% subscribed, 73% non-subscribers
- Shipping Preferences: Multiple options available (Standard, Express, Free, etc.)

**4. Behavioral Insights**
- Discount Usage: 43% customers use discounts (1,677 out of 3,900)
- Product Category Filters: Accessories, Clothing, Footwear, Outerwear
- Top Payment Methods: PayPal (677), Credit Card (671), Debit Card (670)

**5. Interactive Features**
- Slicers for Gender, Category, Shipping Type
- Drill-down capability by age group and season
- Dynamic KPI cards with trend indicators

---

## 📊 Key Findings & Business Insights

### 1. **Revenue Drivers**
- **Young Adults** (18-35 years) generate highest revenue ($62.1K), indicating strong spending power in emerging markets
- **Clothing Category** dominates with $104K revenue (42% of total), suggesting it's the core business driver
- **Seasonal Variation:** Fall and Spring show 7-8% higher revenue than Summer, indicating seasonal demand patterns

### 2. **Customer Segmentation Opportunity**
- **Loyal Customers (10+ purchases):** Likely high-LTV segment, prioritize retention
- **Returning Customers (2-10 purchases):** Mid-tier segment with growth potential, target for upgrade
- **New Customers (1 purchase):** Conversion risk, focus on first-repeat incentives

### 3. **Discount Strategy Insights**
- **43% of customers** use discounts, but still contribute significant revenue
- **Top 5 discounted products** show high purchase frequency, indicating volume-driven strategy works
- **Opportunity:** Shift from discount-driven to value-based marketing for margin improvement

### 4. **Subscription Economics**
- **27% subscription rate** (1,053 customers) with $1.17B potential lifetime revenue
- **Subscribers vs. Non-subscribers:** Compare average spend and loyalty metrics
- **Growth Lever:** Increase subscription adoption through targeted campaigns to high-frequency buyers

### 5. **Shipping & Payment Preferences**
- **Express Shipping:** Higher average transaction value, indicating premium customer segment
- **PayPal dominance:** 677 transactions (17%), highest among payment methods
- **Multi-channel payment support:** Balanced usage across PayPal, Credit/Debit cards, Venmo

### 6. **Product Performance**
- **Top-rated products:** Focus marketing on high-review items (4.5+ ratings)
- **Category expansion:** Outerwear underperforms ($19K), review improvement strategy needed
- **Cross-sell opportunity:** Bundle top-performing categories (Clothing + Accessories)

---

## 🚀 Getting Started

### Prerequisites
```bash
Python 3.8+
Pandas, NumPy
Google Cloud SDK (for BigQuery)
SQL IDE (BigQuery Web UI or DBeaver)
Power BI Desktop
```

### Installation

1. **Clone the repository**
```bash
git clone https://github.com/yourusername/customer-purchase-behavior-analysis.git
cd customer-purchase-behavior-analysis
```

2. **Set up Python environment**
```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
pip install -r requirements.txt
```

3. **Configure BigQuery (Optional)**
```bash
gcloud auth application-default login
# Update project ID in notebook if using BigQuery
```

4. **Run the analysis**
```bash
# Data preparation (Jupyter)
jupyter notebook notebooks/Customer_shopping_behaviour_analysis.ipynb

# Execute SQL queries
# Use BigQuery Web UI or export queries to your SQL IDE

# Open Power BI Dashboard
# File > Open > dashboards/Customer_Purchase_Behavior_Dashboard.pbix
```

---

## 📝 Requirements

```
pandas>=1.3.0
numpy>=1.21.0
google-cloud-bigquery>=3.0.0
google-auth>=2.0.0
jupyter>=1.0.0
matplotlib>=3.4.0
seaborn>=0.11.0
```

Install with:
```bash
pip install -r requirements.txt
```

---

## 🔗 SQL Queries

All 10 business questions have been translated into optimized SQL queries:

**File:** `sql/customer_behaviour_sql_queries.sql`

### Quick Examples:

**Customer Lifetime Value by Subscription Status:**
```sql
SELECT subscription_status, COUNT(customer_id) AS total_customers,
       ROUND(AVG(purchase_amount_usd), 2) AS average_spend,
       SUM(purchase_amount_usd) AS total_revenue
FROM customer_behavior.customer
GROUP BY subscription_status
ORDER BY average_spend DESC;
```

**Top 5 Most Discounted Products:**
```sql
SELECT item_purchased, 
       ROUND(SUM(CASE WHEN LOWER(discount_applied) = 'yes' THEN 1 ELSE 0 END) 
             / COUNT(*) * 100, 2) AS discount_rate
FROM customer_behavior.customer
GROUP BY item_purchased
ORDER BY discount_rate DESC
LIMIT 5;
```

---

## 📊 Dashboard Preview

The Power BI dashboard includes:
- **6 interactive visualizations** tracking KPIs, segmentation, and trends
- **4 filter slicers** for dynamic exploration (Gender, Category, Shipping, Season)
- **Real-time drill-down** capability to analyze sub-segments
- **Conditional formatting** highlighting top/bottom performers

[<img width="1330" height="740" alt="Screenshot 2026-04-30 231729" src="https://github.com/user-attachments/assets/1f606ea4-6680-4152-8fb5-4efbb53bf12b" />]


---

## 📈 Business Recommendations

### Immediate Actions (0-30 days):
1. **Optimize Product Mix:** Increase inventory for top-performing Clothing category
2. **Enhance Customer Experience:** Target young adults (18-35) with category-specific campaigns
3. **Discount Strategy Review:** Shift 20% of discount budget to loyalty programs

### Short-term (1-3 months):
1. **Subscription Growth:** Launch tiered subscription tiers to capture mid-LTV customers
2. **Seasonal Campaigns:** Plan Fall promotions 8 weeks in advance based on historical trends
3. **Payment Integration:** Promote PayPal (highest adoption) with checkout incentives

### Long-term (3-12 months):
1. **Customer Segmentation:** Implement dynamic pricing for Loyal vs. New customer segments
2. **Category Expansion:** Develop new Outerwear products with focus on quality (review rating)
3. **Retention Programs:** Build predictive churn model using repeat purchase patterns

---

## 🎓 Learning Outcomes

This project demonstrates:
- ✅ End-to-end ETL pipeline (Extract → Transform → Load)
- ✅ Advanced Python data manipulation with Pandas
- ✅ SQL optimization for large-scale analytics
- ✅ Cloud analytics with BigQuery
- ✅ Business intelligence with Power BI
- ✅ Stakeholder communication through dashboards & reports

---

## 📧 Contact & Support

- **Author:** Ronali Sahani
- **Email:** ronalisahani24@gmail.com
- **LinkedIn:** https://www.linkedin.com/in/ronali-sahani-b491a938b
- **Project Date:** April 2026

---

## 🙏 Acknowledgments

- Dataset: 3,900 customer transactions from retail operations
- Tools: Python (Pandas/NumPy), Google BigQuery, Power BI
- Methodology: Industry-standard CRISP-DM framework


---

**Last Updated:** May 2026  
**Status:** ✅ Complete - Ready for Production Use

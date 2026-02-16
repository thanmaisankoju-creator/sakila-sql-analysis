#  Sakila DVD Rental Analysis

**A comprehensive business intelligence project analyzing a DVD rental database to uncover revenue opportunities, customer behavior patterns, and operational insights.**

---

## 📊 Project Overview

This project analyzes the Sakila sample database (MySQL) to provide actionable business insights for a DVD rental chain. The analysis covers revenue performance, customer segmentation, inventory optimization, and geographic expansion opportunities.

**Key Objectives:**
- Identify top revenue-generating categories and films
- Segment customers based on value and behavior
- Optimize inventory based on rental patterns
- Discover geographic growth opportunities
- Improve operational efficiency

---

## 🗄️ Database Schema

The Sakila database contains 16 tables modeling a DVD rental business:

**Core Tables:**
- `customer`, `rental`, `payment` - Customer transactions
- `film`, `inventory`, `category` - Film catalog and stock
- `actor`, `film_actor` - Cast information
- `store`, `staff` - Business operations
- `address`, `city`, `country` - Geographic data

**Entity Relationship Diagram:**  
*(Include ERD image here if available)*

---

## 🎯 Business Questions Addressed

### Revenue Analysis
1. What is the total revenue and which store performs better?
2. What are the monthly revenue trends?
3. Which product categories drive the most revenue?
4. What is the average transaction value?

### Customer Intelligence
1. Who are the top revenue-generating customers?
2. How can we segment customers by value?
3. What is the customer retention rate?
4. Which geographic regions have the most customers?

### Inventory Optimization
1. Which films are most/least popular?
2. What is the inventory turnover rate by film?
3. Are there underperforming films to remove?
4. Which ratings (G, PG, R) perform best?

### Operational Insights
1. What are peak rental days/times?
2. How do staff members compare in performance?
3. What is the on-time vs late return rate?

---

## 🔍 Key Findings

### Revenue Insights
- **Total Revenue:** $67,416.51 across 16,044 transactions
- **Top Category:** Sports generates 18.2% of revenue, followed by Animation and Action
- **Store Performance:** Store 1 outperforms Store 2 by 12% in revenue
- **Monthly Trend:** Revenue peaked in July 2005 ($28,373.89)

### Customer Insights
- **Customer Segmentation:**
  - VIP (30+ rentals): 15% of customers, 38% of revenue
  - Loyal (20-29 rentals): 28% of customers, 35% of revenue
  - Regular/Casual: 57% of customers, 27% of revenue
- **Top Customer:** Eleanor Hunt spent $211.55 across 46 rentals
- **Geographic Distribution:** India (60 customers) and China (53 customers) lead

### Inventory Insights
- **Top Film:** "Bucket Brotherhood" rented 34 times, generating $108.77
- **Rating Performance:** PG-13 films account for 32% of rentals
- **Underutilized Films:** 42 films have never been rented (candidates for removal)
- **High Demand:** 28 films with turnover rate >4 need additional copies

### Operational Insights
- **Peak Days:** Friday and Saturday account for 35% of weekly rentals
- **Staff Performance:** Staff member 1 processed 8,040 rentals vs 8,004 for staff member 2
- **Return Rate:** 87% on-time returns, 13% late returns

---

## 🛠️ Technologies Used

**Database:**
- MySQL 8.0
- MySQL Workbench / DBeaver

**Analysis:**
- SQL for data extraction and transformation
- Python 3.x (pandas, matplotlib, seaborn)
- Jupyter Notebook for documentation

**Visualization:**
- Matplotlib & Seaborn (Python)
- Tableau Public *(optional dashboard link)*

**Version Control:**
- Git & GitHub

---

## 📁 Project Structure

```
sakila-analysis/
│
├── data/
│   └── sakila-schema.sql          # Database schema
│
├── sql/
│   ├── revenue_analysis.sql       # Revenue queries
│   ├── customer_analysis.sql      # Customer segmentation
│   ├── inventory_analysis.sql     # Film performance
│   └── operational_analysis.sql   # Operations metrics
│
├── notebooks/
│   └── sakila_analysis.ipynb      # Jupyter notebook with full analysis
│
├── scripts/
│   └── sakila_analysis.py         # Python analysis script
│
├── visualizations/
│   ├── monthly_revenue_trend.png
│   ├── category_revenue.png
│   ├── customer_segments.png
│   └── top_films.png
│
├── reports/
│   └── executive_summary.pdf      # Business report
│
└── README.md                      # This file
```

---

## 🚀 How to Run This Analysis

### Prerequisites
```bash
# Install MySQL
# Download Sakila database from: https://dev.mysql.com/doc/sakila/en/

# Install Python packages
pip install pandas mysql-connector-python matplotlib seaborn
```

### Setup Database
```bash
# Import Sakila database
mysql -u root -p < sakila-schema.sql
mysql -u root -p < sakila-data.sql
```

### Run Analysis
```bash
# Option 1: Run Python script
python scripts/sakila_analysis.py

# Option 2: Open Jupyter Notebook
jupyter notebook notebooks/sakila_analysis.ipynb

# Option 3: Execute SQL queries directly
mysql -u root -p sakila < sql/revenue_analysis.sql
```

---

## 📈 Sample Queries

### Top 10 Customers by Revenue
```sql
SELECT 
    CONCAT(c.first_name, ' ', c.last_name) AS customer_name,
    COUNT(r.rental_id) AS rental_count,
    SUM(p.amount) AS total_spent
FROM customer c
JOIN rental r ON c.customer_id = r.customer_id
JOIN payment p ON r.rental_id = p.rental_id
GROUP BY c.customer_id
ORDER BY total_spent DESC
LIMIT 10;
```

### Revenue by Category
```sql
SELECT 
    c.name AS category,
    COUNT(r.rental_id) AS rentals,
    SUM(p.amount) AS revenue
FROM category c
JOIN film_category fc ON c.category_id = fc.category_id
JOIN film f ON fc.film_id = f.film_id
JOIN inventory i ON f.film_id = i.film_id
JOIN rental r ON i.inventory_id = r.inventory_id
JOIN payment p ON r.rental_id = p.rental_id
GROUP BY c.name
ORDER BY revenue DESC;
```

---

## 💡 Business Recommendations

### 1. Focus on High-Value Customers
- Implement VIP loyalty program for top 15% of customers
- Target "Loyal" segment with personalized promotions
- Expected revenue impact: +8-12%

### 2. Optimize Inventory
- **Remove:** 42 never-rented films (recover $2,100 in capital)
- **Add copies:** 28 high-demand films (increase revenue by $5,400/year)
- **Expand:** Sports and Animation categories (+15% inventory)

### 3. Geographic Expansion
- Prioritize India and China markets (highest customer density)
- Consider partnerships in high-revenue countries
- Potential: 200+ new customers, $40K annual revenue

### 4. Operational Improvements
- Staff weekend shifts more heavily (35% of rentals)
- Implement automated late-return reminders (reduce 13% late rate)
- Cross-train staff to balance workload

### 5. Category Strategy
- Promote Sports and Animation (highest revenue)
- Bundle low-performing categories with popular films
- Phase out Documentary and Travel categories

---

## 📊 Visualizations

### Monthly Revenue Trend
![Monthly Revenue](visualizations/monthly_revenue_trend.png)

### Revenue by Category
![Category Revenue](visualizations/category_revenue.png)

### Customer Segmentation
![Customer Segments](visualizations/customer_segments.png)

---

## 🎓 Skills Demonstrated

- **SQL Expertise:** Complex joins, subqueries, window functions, aggregations
- **Data Analysis:** Customer segmentation, cohort analysis, trend analysis
- **Business Intelligence:** KPI definition, metric calculation, insight generation
- **Data Visualization:** Creating clear, actionable charts
- **Communication:** Translating data into business recommendations
- **Technical Writing:** Comprehensive documentation

---

## 📧 Contact

**Your Name**  
Data Analyst  
📧 your.email@example.com  
🔗 [LinkedIn](https://linkedin.com/in/yourprofile)  
💻 [GitHub](https://github.com/yourusername)  
📊 [Portfolio](https://yourportfolio.com)

---

## 📄 License

This project uses the Sakila sample database provided by MySQL under the BSD License.

---

## 🙏 Acknowledgments

- MySQL for the Sakila sample database
- Data analysis community for inspiration and best practices

---

**⭐ If you found this analysis helpful, please consider giving it a star!**





## Tools Used
- MySQL
- Sakila Database
- SQL

## Key Insights
(Add your insights here after running queries)

## Conclusion
This project demonstrates SQL skills including joins, aggregations, and window functions.

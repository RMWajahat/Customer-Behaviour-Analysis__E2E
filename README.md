# Customer Shopping Behavior Analysis (Python, SQL, Power BI)

End-to-end analytics project that turns a raw customer shopping dataset into a clean analysis-ready table, answers stakeholder-style business questions in SQL, and packages insights in a Power BI dashboard and written deliverables.

## What this project demonstrates

- Data cleaning and feature engineering in Python (pandas)
- Reproducible loading of a cleaned dataset into a relational database (SQLAlchemy)
- Analytics SQL using aggregates, CTEs, and window functions
- KPI design and stakeholder-facing reporting via Power BI

## Dataset

- File: [customer_shopping_behavior.csv](Customer Shopping Behavior.csv)
- Rows: 3,900 (as loaded in the notebook)
- Output table schema (post-cleaning):
  - `customer_id`, `age`, `gender`, `item_purchased`, `category`, `purchase_amount`, `location`, `size`, `color`, `season`, `review_rating`, `subscription_status`, `shipping_type`, `discount_applied`, `previous_purchases`, `payment_method`, `frequency_of_purchases`, `age_group`, `purchase_frequency_days`

## Workflow

1. **Prepare and enrich the data (Python / Jupyter)**
   - Load the CSV, profile the data, and check nulls.
   - Impute missing `review_rating` values using the median rating within each `category`.
   - Standardize column names to `snake_case`.
   - Engineer features:
     - `age_group` via quartiles (`pd.qcut`) with labels: Young Adult / Adult / Middle-aged / Senior
     - `purchase_frequency_days` by mapping `frequency_of_purchases` to day counts
   - Validate and remove redundant fields (`promo_code_used` duplicates `discount_applied`).

2. **Load into SQL (PostgreSQL / MySQL / SQL Server)**
   - Use SQLAlchemy to write the cleaned DataFrame into a `customer` table.

3. **Answer business questions (SQL)**
   - Use [customer_behavior_sql_queries.sql](customer_behavior_sql_queries.sql) to run a set of stakeholder-driven queries.

4. **Visualize and communicate (Power BI + report + deck)**
   - Build and refresh a dashboard from the SQL table.
   - Summarize findings in a report and a slide deck.

## Business questions answered (SQL)

The SQL file includes queries to answer questions such as:

1. Total revenue by gender
2. Discounted purchases above the overall average spend
3. Top 5 products by average review rating
4. Average purchase amount by shipping type (Standard vs Express)
5. Subscriber vs non-subscriber spend (avg spend, total revenue, customer count)
6. Top 5 products by discount utilization rate
7. Customer segmentation based on `previous_purchases` (New / Returning / Loyal)
8. Top 3 most purchased products within each category (window functions)
9. Repeat buyers (previous purchases > 5): subscription propensity
10. Revenue contribution by age group

## Repository artifacts

- Notebook (Python cleaning + DB load): [Customer_Shopping_Behavior_Analysis.ipynb](Customer_Shopping_Behavior_Analysis.ipynb)
- Dataset (raw input): [customer_shopping_behavior.csv](customer_shopping_behavior.csv)
- SQL queries (analytics questions): [customer_behavior_sql_queries.sql](customer_behavior_sql_queries.sql)
- Power BI dashboard: [customer_behavior_dashboard.pbix](customer_behavior_dashboard.pbix)
- Written report: [Customer Shopping Behavior Analysis.pdf](Customer%20Shopping%20Behavior%20Analysis.pdf)
- Presentation deck: [Customer-Shopping-Behavior-Analysis.pptx](Customer-Shopping-Behavior-Analysis.pptx)
- Business context: [Business Problem  Document.pdf](Business%20Problem%20%20Document.pdf)

## How to run (reproducible)

### Option A: Run locally with Python only

1. Open the notebook: [Customer_Shopping_Behavior_Analysis.ipynb](Customer_Shopping_Behavior_Analysis.ipynb)
2. Run the Python sections for loading/cleaning/feature engineering.

### Option B: Load into a database and run SQL + Power BI

1. Create an empty database (PostgreSQL recommended).
2. In the notebook, update the connection values (host/user/password/database) and run the `to_sql(...)` cell to create/replace the `customer` table.
3. Run the queries in [customer_behavior_sql_queries.sql](customer_behavior_sql_queries.sql).
4. Open [customer_behavior_dashboard.pbix](customer_behavior_dashboard.pbix) and refresh the dataset connection.

**SQL dialect note:** the queries are written in a PostgreSQL-friendly style (e.g., `review_rating::numeric`). Minor edits may be needed for other engines.


## License

MIT. See [LICENSE](LICENSE).

## About

Muhammad Wajahat Hussain  -  Data Scientist and AI Developer.

- LinkedIn (business inquiries): https://www.linkedin.com/in/muhammad-wajahat-hussain-30091a380/

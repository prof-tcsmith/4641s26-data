# ISM4641 Course Data

Data files for ISM4641 Python for Business Analytics - Spring 2026.

## Usage

Students can access these datasets directly via raw GitHub URLs in their notebooks:

```python
import pandas as pd

# Example: Load employee data
url = "https://raw.githubusercontent.com/prof-tcsmith/4641s26-data/main/week08/employees.csv"
df = pd.read_csv(url)
```

## Available Datasets

### Week 08: Introduction to Pandas
| File | Description |
|------|-------------|
| `week08/employees.csv` | Employee data with department, salary, years, and rating |
| `week08/retail_sales.csv` | Retail sales by store and category |
| `week08/orders.csv` | Customer orders data |
| `week08/customers.csv` | Customer information |
| `week08/inventory.csv` | Product inventory data |
| `week08/jan_revenue.csv` | January product revenue |
| `week08/feb_revenue.csv` | February product revenue |
| `week08/mar_revenue.csv` | March product revenue |

### Week 09: Data Visualization with Matplotlib
| File | Description |
|------|-------------|
| `week09/monthly_sales.csv` | Monthly sales for 2024 and 2025 |
| `week09/regional_revenue.csv` | Q1 and Q2 revenue by region |
| `week09/advertising_effectiveness.csv` | Ad spend vs sales data |
| `week09/category_distribution.csv` | Revenue by product category |
| `week09/dashboard_profit.csv` | Monthly profit data |
| `week09/store_revenue.csv` | Revenue by store location |
| `week09/customer_spending.csv` | Customer spending distribution |

### Week 11: Descriptive and Inferential Statistics
| File | Description |
|------|-------------|
| `week11/salaries.csv` | Employee salaries with department outliers |
| `week11/marketing_data.csv` | Marketing metrics for correlation analysis |
| `week11/call_durations.csv` | Customer service call durations |
| `week11/region_north_sales.csv` | Sales data for North region |
| `week11/region_south_sales.csv` | Sales data for South region |
| `week11/training_scores.csv` | Before/after training scores |

### Week 12: Linear Regression
| File | Description |
|------|-------------|
| `week12/advertising_sales.csv` | Advertising spend and sales data |
| `week12/house_prices.csv` | House features and prices |
| `week12/employee_salaries.csv` | Employee experience, education, and salary |

### Week 13: Logistic Regression
| File | Description |
|------|-------------|
| `week13/customer_churn.csv` | Customer churn prediction data |
| `week13/marketing_response.csv` | Marketing campaign response data |
| `week13/loan_defaults.csv` | Loan default prediction data |

### Final Project
See [`final-project/README.md`](final-project/README.md) for the student guide, team-formation rules, and the 50-point rubric. Each of the 10 project options has its own subfolder containing a narrative (`README.md`) and the dataset students need.

| Folder | Scenario | Dataset |
|--------|----------|---------|
| `final-project/Project-01-TeleMax-Churn/` | Telecom customer churn | `telemax_customers.csv` |
| `final-project/Project-02-FirstState-Loan-Default/` | Community-bank loan default | `firststate_loans.csv` |
| `final-project/Project-03-NovaMail-Spam-Filter/` | Enterprise email spam filter | `novamail_messages.csv` |
| `final-project/Project-04-HealthPath-Diabetes-Screening/` | Primary-care diabetes screening | `healthpath_patients.csv` |
| `final-project/Project-05-SecureCard-Fraud/` | Credit-card fraud detection | `securecard_transactions.csv` |
| `final-project/Project-06-GreenLeaf-Direct-Mail/` | Grocery-chain direct-mail targeting | `greenleaf_customers.csv` |
| `final-project/Project-07-AxisCorp-Attrition/` | Consulting-firm attrition | `axiscorp_employees.csv` |
| `final-project/Project-08-PrecisionParts-QC/` | Aerospace QC flagging | `precisionparts_runs.csv` |
| `final-project/Project-09-StreamPlus-Upgrade/` | Streaming-service upgrade targeting | `streamplus_subscribers.csv` |
| `final-project/Project-10-CampusConnect-At-Risk/` | University at-risk student identification | `campusconnect_students.csv` |

## Course Information

- **Course**: ISM4641 Python for Business Analytics
- **Term**: Spring 2026
- **Instructor**: Dr. Tim Smith
- **Institution**: University of South Florida

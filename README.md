# Customer Churn Analysis: Telecom Company

Which customers leave a telecom company, why, and what should the company do about it?

I analyzed 7,032 customer records to find the patterns behind churn (customers cancelling), wrote business recommendations, and built a simple model that predicts who is likely to leave next.

Tools: Python, Pandas, Matplotlib, Seaborn, scikit-learn, Google Colab

## The business problem

Winning a new customer costs far more than keeping an existing one. About 1 in 4 customers (26.6%) in this dataset left, and they took 30.5% of the company's monthly revenue with them. The goal is to find out who is leaving and how to keep them.

## Dataset

- Source: IBM Sample Data Sets, *Telco Customer Churn*, accessed via [Kaggle](https://www.kaggle.com/datasets/blastchar/telco-customer-churn)
- Size: 7,032 customers and 21 columns (demographics, services, contract, billing, churn status)
- IBM made this dataset up for a fictional company, so it is sample data.

## Data cleaning

I checked for missing values, duplicate rows, duplicate customer IDs, wrong data types and inconsistent text, and found no issues. The 11 records with blank `TotalCharges` in the original 7,043-row file were already removed. I made the `SeniorCitizen` formatting match the other Yes/No columns.

## Key findings

| Finding | Churn rate |
|---|---|
| Overall | 26.6% |
| Month-to-month contract | 42.7% (one year: 11.3%, two year: 2.8%) |
| First 12 months as a customer | 47.7% (falls to 9.5% after 49 months) |
| Fiber optic internet | 41.9% (DSL: 19.0%) |
| Electronic check payment | 45.3% (other methods: 15% to 19%) |
| Month-to-month + fiber + electronic check | 60.4% (1,307 customers) |
| Internet customers without tech support | 41.6% (with tech support: 15.2%) |

Of the customers who left, 88.6% were on month-to-month contracts and 55.5% were in their first 12 months.

### Charts

![Overall churn](images/1_churn_overall.png)
![Churn by contract](images/2_contract.png)
![Churn by tenure](images/3_tenure.png)
![Churn by payment method](images/5_payment.png)

## Recommendations

1. Move customers off month-to-month contracts. Offer a discount or free add-on for switching to a 1-year plan. If 10% of month-to-month customers (about 388) switched and then churned at the one-year rate, roughly 122 fewer customers would leave.
2. Focus on the first year. Add onboarding check-ins at months 1 and 3 and a loyalty offer at month 6.
3. Fix the electronic check and fiber problem. Give a small bill credit for switching to automatic payment, and investigate fiber service quality and pricing.
4. Bundle tech support and online security. Offer a free trial to at-risk customers, and run an A/B test first to check whether the link is causal.

## Prediction model

I trained a Logistic Regression model on 80% of the customers and tested it on the other 20%.

| Measure | Result |
|---|---|
| ROC AUC | 0.835 |
| Recall (leavers caught) | 80% |
| Precision (flagged who really leave) | 49% |
| Accuracy | 72.6% |

Accuracy looks low because a model that always says "stays" would score 73.4% while catching nobody, so recall and ROC AUC are the better measures here. The model catches 8 of every 10 customers who leave. About half of the customers it flags would have stayed, which is acceptable because a retention offer costs far less than losing a customer.

![What drives churn](images/7_drivers.png)

## Limitations

- The dataset is fictional, so the results demonstrate the method and say little about real-world performance.
- The analysis finds relationships but cannot prove causes.
- Impact estimates are rough and assume converted customers would behave like existing one-year customers.
- The model was tested on a single train/test split. Cross-validation would be a stricter test.

## Repository contents

```
customer-churn-analysis/
├── README.md
├── churn_analysis.ipynb      # full code, charts and notes
├── data/
│   └── PROJECT.csv           # cleaned dataset
└── images/                   # charts used above
```

## How to run

1. Open `churn_analysis.ipynb` in [Google Colab](https://colab.research.google.com).
2. Upload `PROJECT.csv` to the Colab files panel.
3. Run all cells from top to bottom.

## Use of AI

I used Claude, an AI assistant from Anthropic, to help write the Python code. I chose the project, worked through each step, checked the results and wrote up the findings and recommendations myself.

## About me
I am Ketan Mehra aspiring product manager .
Linkdin:- https://www.linkedin.com/in/ketan-mehra-22b159312?utm_source=share_via&utm_content=profile&utm_medium=member_android


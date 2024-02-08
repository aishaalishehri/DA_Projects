# Churn Chasers Project

## Table Of Contents
- [Overview](#overview)
- [Results](#results)

### Overview
It was a graduation project from DA bootcamp. We was a group of 4 students and embark on a thrilling data exploration journey with HomeExchange, a global platform connecting home swappers from around the world. Our mission is to leverage data analytics to enhance customer satisfaction, reduce churn, and shape the future of HomeExchange.

### Data Source
- Google Bigquery.
  
### Tools
- Bigquery - Data Cleaning, analysis, and merging tables.
- Python - Cleaning, Transformation, correlation, and create a ML model. 
- Power BI - Creating a dashboard and a charts.
- Google slides - Create the final report

### Data cleaning and prepration
1. install all datasets and manipualte it
2. Transforming data
3. Dealing with missing values
4. Data cleaning to ensure.

### Exploarty analysis
We worked with hyoothesises: 
 - Why the churners are a huge number?and in which countries are more?
 - new registered users leave more?
 - incomplete profile (country is unknown ) indicates uninterested customers which lead to churn?
 - Users who subscribed through promotions or referrals exhibit higher loyalty?
 - Users with longer durations of activity are less likely to churn
 - Users with uncompleted exchanges tend to churn more?

### Data Analysis
- Imprtant codes:
1. Python, To get a table from Bigquery to Colab:
 ```Python
 import pandas as pd
 from google.cloud import bigquery
 from google.colab import auth
 #Will collect your credentials
 auth.authenticate_user()
 #Query Bigquery
 project_id = "churn-chasers"
 exchange = bigquery.Client(project=project_id)
 query = """
 SELECT *
 FROM `churn-chasers.exchanges.exchanges`
 """
 df_exchange= exchange.query(query).to_dataframe() 
 ```

2. Python, To get a table from Bigquery to Colab:
 ```Python
 import pandas as pd
 from google.colab import auth
 from google.cloud import bigquery
 
 auth.authenticate_user()
 
 project_id = "churn-chasers"
 dataset_id = 'exchanges'
 table_id = 'exchanges_cleaned_AA'

 df_.to_gbq(f'{dataset_id}.{table_id}',project_id=project_id, if_exists='replace')
```

- One of the exploreing code:
1. SQL, to see if the seniority let customers churn less:
  ```SQL
  SELECT
  extract(year from first_subscription_date) as year,
  #Count the total customer per year to calculate the churn rate
  count(user_id) as total_customers,
  #sum the total customer renewed per year to calculate the churn rate
  sum(renew) as total_renew,
  #The churn_rate column
  round((SAFE_DIVIDE((count(user_id)- sum(renew)),count(user_id))*100), 1) as churn_rate
  FROM `churn-chasers.exchanges.subscriptions`
  group by year
  order by year
  ```

### Results 
1. Most of the exchanges are guest points exchanges.
2. The churn rate is improving more for each year.
3. Churn rate increases from users who subscribe recently     
4. Different travel types affect the churn rate based on user continent
5. We have a classification model to predict churn with accuracy of 75%.
   This gives the company the ability to act according for those at risk of leaving by sending personalised emails, targeted
   retention campaigns for this segment of users.
   

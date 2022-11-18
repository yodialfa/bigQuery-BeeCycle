# SQL in BigQuery
![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)


Step by step access SQL BigQuery in Google Colaboratory


## Datasets

Beecycle Tables
- dim_customer
- dim_product
- fact_sales
- dim_geography
- dim_territory

## Making Project on BigQuery
- visit website console.cloud.google.com
- make sure that you have cloud account and register on bigquery
- create a project
- adding dataset (table)

## Connect BigQuery on Google Colaboratory
- Authenticate to GCP
```python
from google.colab import auth
auth.authenticate_user()
print('Authenticated')
```
after that you have to permitted your google account to access your project on bigquery.

- Specify with project_id
```python
#define project_id API
project_id = 'project-bigquery-368803'

#import bigquery library
from google.cloud import bigquery

#access bigquery
client = bigquery.Client(project=project_id)
dataset_ref = client.dataset("beecycle", project="project-bigquery-368803")

```

## Making function to show dataframe
- Define Function
```python
#function to show dataframe
import pandas as pd
def gcpdf(sql):
   query = client.query(sql)
   result = query.result()
   return result.to_dataframe()

```

- Testing
```python
#test the function with query
query = """
SELECT * 
FROM `project-bigquery-368803.beecycle.dim_customer` 
LIMIT 10
"""

df = gcpdf(query)
df

```
- Showing


|customer_id |	geography_id	| customer_name	| birthdate |	maritalstatus	| gender	| datefirstpurchase |
|--- | --- | --- | --- |--- |--- |--- |
| 11408	| 257	| Darren Gill	| 1973-05-14|	M	| M |	2018-09-06 |
| 11549	| 257	| Crystal Liang	| 1988-09-06 |	M	|F	|2017-06-23|
|11918	|2	|Kaylee Hill |	1984-03-03	|M|	F|	2017-04-15|
|11963|	2	|Antonio Patterson	|1975-06-13	|M	|M|	2017-04-24|
|11997	|2|	Kristina Kapoor|	1980-04-07	|M	|F|	2017-05-08|
|12677	|2	|Cedric Liu	|1994-11-05|	M|	M|	2017-08-07|
|12571	|2	|Jennifer Green	|2000-05-19	|M|	F	|2017-07-01|
|	12216	|258|	Gerald Rodriguez|	1982-04-02|	M|	M|	2017-09-26|
|	11110|	3|	Curtis Yang	|1982-06-06	|M|	M|	|2016-11-01|
|	12989	|3|	Carly Goel	|1989-11-13	|M	|F|	2017-10-02|

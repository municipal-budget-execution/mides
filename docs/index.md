# **MiDES: New Data and Facts from Local Procurement and Budget Execution in Brazil** 

## Overview

The dataframe shows the full process of creation and understanding about our data. We collect from several Brazilian states data provided by State Audit Courts (_TCEs_ in Portuguese) about budget execution and procurements. Initially, we show this enforcement in [working paper](https://documents.worldbank.org/en/publication/documents-reports/documentdetail/099456511072320917/idu0577a4ea10ff8504db6089400548fa91b30a3) published by the World Bank with seven states. Here, we publish updates about our dataset with more States. We provide the original source, processing codes, queries, and other analyses.

![Image](./images/MapChart_Map.png)

Currently, the budget execution dataframe contain 10 States with information about more than 3000 municipalities, approximatelly 60% of coverage.

## Acessing database

The database is hosted in [BasedosDados](https://basedosdados.org/dataset/d3874769-bcbd-4ece-a38a-157ba1021514?table=14c5d05b-9830-4710-b7ac-7e0ca1bf9d8b). For access database in BigQuery, you can follow this [steps](https://basedosdados.github.io/mais/access_data_bq/) to create a personal project and create your queries. The most simple query is

```sql
SELECT * FROM `basedosdados.world_wb_mides.empenho` LIMIT 100
```
The output is a hundred observations about commitments.
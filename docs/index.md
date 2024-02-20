# **MiDES: New Data and Facts from Local Procurement and Budget Execution in Brazil** 

## Overview

The dataframe shows the full process of creation and understanding about our data. We collect from several Brazilian states data provided by State Audit Courts (_TCEs_ in Portuguese) about budget execution and procurements. Initially, we show this enforcement in [working paper](https://documents.worldbank.org/en/publication/documents-reports/documentdetail/099456511072320917/idu0577a4ea10ff8504db6089400548fa91b30a3) published by the World Bank with seven states. Here, we publish updates about our dataset with more States. We provide the original source, processing codes, queries, and other analyses.

Our dataset on municipal procurement and budget execution currently covers ten of Brazil's twenty-seven states, highlighted in Figure 1: Ceará (CE), Distrito Federal (DF), Minas Gerais (MG), Paraíba (PB), Pernambuco (PE), Paraná (PR), Rio de Janeiro (RJ), Rio Grande do Sul (RS), Santa Catarina (SC)and São Paulo (SP). These are large states that cover a substantial share of the total number of municipalities (60%), population (67%), and GDP (76%) of the country according to 2021 data. Notably, our dataset only covers states in the South, Southeast and Northeast regions - data from the states in the North and Center-West regions are currently not available[^1].

<!-- Query Proportion
WITH sample AS (
  SELECT
    sigla_uf,
    id_municipio,
    1 AS amostra,
  FROM `basedosdados.br_bd_diretorios_brasil.municipio`
  WHERE sigla_uf in ('DF', 'CE', 'MG', 'PB', 'PE', 'PR', 'RS', 'SP', 'RJ', 'SC')
)

SELECT 
  SUM(1) AS N,
  SUM(1 * sample.amostra) AS N_munic,
  100 * SUM(1 * sample.amostra) / SUM(1) AS prop_munic,
  100 * SUM(pop.populacao * sample.amostra) / SUM(pop.populacao) AS prop_populacao,
  100 * SUM(gdp.pib * sample.amostra) / SUM(gdp.pib) AS prop_pib
FROM `basedosdados.br_bd_diretorios_brasil.municipio` AS dir
LEFT JOIN sample
  ON dir.id_municipio = sample.id_municipio
LEFT JOIN `basedosdados.br_ibge_populacao.municipio` AS pop
  ON dir.id_municipio = pop.id_municipio
LEFT JOIN `basedosdados.br_ibge_pib.municipio` AS gdp
  ON dir.id_municipio = gdp.id_municipio
WHERE pop.ano = 2021 AND gdp.ano = 2021
 -->

![Figure1](./images/MapChart_Map.png)

We provide further details on the geographical and temporal coverage of the dataset in Table 1. Starting with geographical coverage, our budget execution tables (commitment, verification, and payment) are available for all ten states. The procurement data are less comprehensive: the dataset currently includes no procurement data for SP, and the data for PB and PE include information on tenders and participants, but not on the more disaggregated level of items. In terms of temporal coverage, most of our budget execution data starts in the early- to mid-2000s, with the exception of PE (2012), PR (2013), and MG (2014), and currently runs until 2021. Once again, data on procurement is less comprehensive and, with the exception of CE (2009-2021), starts in the mid-2010s.

## Acessing database

The database is hosted in [BasedosDados](https://basedosdados.org/dataset/d3874769-bcbd-4ece-a38a-157ba1021514?table=14c5d05b-9830-4710-b7ac-7e0ca1bf9d8b). For access database in BigQuery, you can follow this [steps](https://basedosdados.github.io/mais/access_data_bq/) to create a personal project and create your queries. The most simple query is

```sql
SELECT * FROM `basedosdados.world_wb_mides.empenho` LIMIT 100
```
The output is a hundred observations about commitments.

<Footnotes>
[^1]: Municipalities that are in our sample are slightly richer and more educated than those that are not. In 2019, the average GDP per capita (literacy rate) in our sample was 26.8 thousand BRL (87.7\%), while in the municipalities that are not in our sample it was 22 thousand BRL (82.5\%). Population size, however, does not differ across the samples (37.7 thousand inhabitants in both)
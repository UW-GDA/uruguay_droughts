# Evaluating the frequency and severity of wind and meteorological droughts in Uruguay

## Member
Hernán Querbes

## Short summary
In this work, I will study the frequency and severity of meteorological and wind droughts over Uruguay for two future periods: Future 1 (2030s), covering 2025 to 2045, and Future 2 (2050s), covering 2045 to 2065. For this, I will use NASA’s NEX-GDDP-CMIP6 dataset and the SSP3-7.0 scenario for future projections.

## Some introduction background

Between October 2020 and May 2023, Uruguay experienced one of its most severe meteorological droughts, leading to significant consequences, including a decline in drinking water quality due to low reserves in the Santa Lucía River, which supplies over half of the country’s population (1). 

The Uruguayan Institute of Meteorology (INUMET) uses seven categories to monitor monthly rainfall. These categories are determined as follows: 

* First, the monthly accumulated precipitation for the reference period (1985–2014) is divided into quintiles: much higher than normal (Category 5, 5th quintile), higher than normal (Category 4, 4th quintile), normal (Category 3, 3rd quintile), less than normal (Category 2, 2nd quintile), and much lower than normal (Category 1, 1st quintile). 
* Then, Category 0 accounts for monthly accumulated precipitation lower than Category 1, while Category 6 accounts for monthly accumulated precipitation higher than Category 5 (2).

This is summarized in thee next Table:

| Precip. Category | Name                          | Range values              |
|-----------------|------------------------------|---------------------------|
| 0               | Extremely lower than normal  | Lower than Quintile 1     |
| 1               | Much lower than normal       | Quintile 1                |
| 2               | Less than normal             | Quintile 2                |
| 3               | Normal                        | Quintile 3                |
| 4               | Higher than normal           | Quintile 4                |
| 5               | Much higher than normal      | Quintile 5                |
| 6               | Extremely higher than normal | Bigger than Quintile 5    |


INUMET defines meteorological drought as three or more consecutive months with precipitation category equal or less than 2 (3). INUMET does not have a definition for wind droughts. Therefore, for the purpose of this project, I will apply an analogous definition to that of meteorological drought for wind drought.

For this prroject I chose EC-EARTH3 and TaiESM1-0 models, since previous studies concluded that they exhibit superior performance in Southeastern South America (4). Also, I selected the SSP3–7.0 scenario, which represents a future where greenhouse gas emissions would double by 2100, resulting in an estimated warming of 2.1 °C from 2041–2060 and 3.6 °C from 2081–2100 (5).

## Problem statement and questions.

My current research focuses on assessing the impact of climate change on hydroelectric production in Uruguay, specifically how meteorological and wind droughts affect it. For this reason, the questions I plan to answer in this project are:

1- Will meteorological droughts change in frequency and severity in the future?

2- Will wind droughts change in frequency and severity in the future?

## Dataset

NASA’s NEX-GDDP-CMIP6 dataset: https://www.nccs.nasa.gov/services/data-collections/land-based-products/nex-gddp-cmip6

## Tools/packages

Matplotlib https://matplotlib.org/stable/ 

Numpy https://numpy.org/doc/stable/index.html 

Xarray https://docs.xarray.dev/en/stable/ 

Rioxarray https://corteva.github.io/rioxarray/html/rioxarray.html 

Geopandas https://geopandas.org/en/stable/index.html# 

## Planned methodology/aproach

### 1- Data preprocesing: 

* Convert units for better interpretability.
* Aggregate daily data into monthly data.
* Extract Uruguay-specific data from the global dataset.
* Divide data into three periods: historical, Future 1, and Future 2

### 2 - Counting analysis:

* Determine category ranges for wind speed and precipitation.
* Assess future precipitation trends using INUMET’s definitions.

### 3 - Severety analysis:

* Measure the duration of drought episodes (in months).
* Construct severity histograms for both meteorological and wind droughts.

## Expected outcomes:

There are two expected outcomes:

1- Count of droughts (wind and meteorological) for the three time periods.

2- A severity histogram (number of consecutive drought months) for the three time periods.

## References

(1) Andreoni, M. (2023, August 10). Uruguay wasn’t supposed to run out of water. The New York Times. https://www.nytimes.com/2023/08/10/climate/uruguay-wasnt-supposed-to-run-out-of-water.html 

(2) INUMET. (n.d.). Quintiles de precipitación. https://www.inumet.gub.uy/clima/recursos-hidricos/quintiles-de-precipitacion

(3) Inumet (2024, January 17). Finalizó la sequía meteorológica 2020-2023 en todo el Uruguay. https://www.inumet.gub.uy/sala-de-prensa/noticias/finalizo-la-sequia-meteorologica-2020-2023-en-todo-el-uruguay

(4) Bazzanela, A. C., Dereczynski, C., Luiz‐Silva, W., & Regoto, P. (2024). Performance of CMIP6 models over South America. Climate Dynamics, 62, 1501-1516. https://doi.org/10.1007/s00382-023-06979-1

(5) Intergovernmental Panel on Climate Change. (2021). Summary for Policymakers. In: Climate Change 2021: The Physical Science Basis. Contribution of Working Group I to the Sixth Assessment Report of the Intergovernmental Panel on Climate Change. https://doi.org/10.1017/9781009157896.001

# Evaluating the frequency and severity of wind and meteorological droughts in Uruguay

![image](https://github.com/user-attachments/assets/a4c37e8d-1682-4fc8-9e05-60e615748b88)


## Member
Hernán Querbes

## Short summary
In this work, I will study the frequency and severity of meteorological and wind droughts over Uruguay for two future periods: Future 1 (2030s), covering 2025 to 2044, and Future 2 (2050s), covering 2045 to 2064. For this, I will use NASA’s NEX-GDDP-CMIP6 dataset and the SSP3-7.0 scenario for future projections.

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

Seaborn https://seaborn.pydata.org/

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

2- Kernel density plots (number of consecutive drought months) for the three time periods.

## Results:

### Data pre-processing:
The dataset consisted of daily values for precipitation, wind speed, and temperature. These variables were aggregated as follows:
* Precipitation: Aggregated by monthly sum.
* Wind speed and temperature: Aggregated by monthly mean.

![download](https://github.com/user-attachments/assets/ea1ea3e9-e07b-4e38-9fb7-4b8d02370c33)

This was done for all three variables across three time periods.

|Time periods     | Years range|
|-----------------|------------|
| 0               | 1985-2014  | 
| 1               | 2025-2044  | 
| 2               | 2045-2064  | 

### Counting and severity analysis:

After aggreating the dataset, clasification as mentioned in the introduction was performed. Then, monthly categories datasets were obtained.
* For precipitation and wind speed, consecutive months of category 2 or below were looked for, meaning lower precipitation/wind speed than normal.
* For temperature, consecutive months of category 4 or above were looked for, meaning higher temperature than normal.

Then the counting analysis was done in the next way:
* A square array was created, with its sides equal to the total number of months in the dataset. This array was initialized with zeros
  * Rows are the starting month of the cnsecutive count.
  * Columns are the subsequent months.
* For each starting month, meaning: (i,i) entries:
  * Precipitation and Wind Speed:
    * Each entry corresponding to a month that meets the condition (category ≤ 2) was replaced with a 1.
  * Temperature:
    * Each entry corresponding to a month that meets the condition (category ≥ 4) was replaced with a 1.
* Starting from each month, the code iterates through subsequent months:
  * If the condition is still met, the corresponding entry remains 1.
  * If the condition is not met, the counting stops for that starting month, and the loop moves to the next month.
* Finally, we obtain the number of consecutive qualifying months starting from each month by summing the entries of each row.

* Outputs:
  * Episodes vector: tracks the index of the starting month.
  * Severity vector: tracks the total number of consecutive qualifying months starting from each month.

This procedure is shown in the next figure:

<div align="center">
  <img src="https://github.com/user-attachments/assets/325d41f4-0d8c-4414-8226-c957ba6114c2">
  <br>
  <strong>Figure 1:</strong> Drought Count Diagram
  <br><br><br> 
</div>

From these outputs, Kernel Density and returning perdios plots were made:

<div align="center">
  <img src="https://github.com/user-attachments/assets/5ed63f6c-37cb-4f07-9f81-35e314d8985d">
  <br>
  <strong>Figure 2:</strong> Kernel density plot for precipitation under the SSP126 scenario.
  <br><br><br> 
</div>

<div align="center">
  <img src="https://github.com/user-attachments/assets/a0eb089e-a043-4006-b2d4-1444fe90eef2">
  <br>
  <strong>Figure 3:</strong> Returning period plot for precipitation under the SSP126 scenario.
  <br><br><br> 
</div>

<div align="center">
  <img src="https://github.com/user-attachments/assets/9fc153e0-a90e-4333-be95-6b3c902ee723">
  <br>
  <strong>Figure 4:</strong> Kernel density plot for wind speed under the SSP126 scenario.
  <br><br><br> 
</div>

<div align="center">
  <img src="https://github.com/user-attachments/assets/fb004550-ecd1-458e-addb-6ee59641f6cf">
  <br>
  <strong>Figure 5:</strong> Returning period plot for wind speed under the SSP126 scenario.
  <br><br><br> 
</div>

<div align="center">
  <img src="https://github.com/user-attachments/assets/7a35294e-8664-4c0f-8c04-471407c0d78b">
  <br>
  <strong>Figure 6:</strong> Kernel density plot for temperature under the SSP126 scenario.
  <br><br><br> 
</div>

<div align="center">
  <img src="https://github.com/user-attachments/assets/7f7abb8e-303b-4526-bb38-b26a43c56aa0">
  <br>
  <strong>Figure 7:</strong> Returning period plot for temperature under the SSP126 scenario.
  <br><br><br> 
</div>

<div align="center">
  <img src="https://github.com/user-attachments/assets/ae82b48c-0bb7-4640-809b-3e2d8fe5587b">
  <br>
  <strong>Figure 8:</strong> Kernel density plot for precipitation under the SSP370 scenario.
  <br><br><br> 
</div>

<div align="center">
  <img src="https://github.com/user-attachments/assets/475fe0cd-1774-41e7-94b8-4893841aa8a1">
  <br>
  <strong>Figure 9:</strong> Returning period plot for precipitation under the SSP370 scenario.
  <br><br><br> 
</div>

<div align="center">
  <img src="https://github.com/user-attachments/assets/6b20afa3-34c2-4d73-adba-b15a1db808c0">
  <br>
  <strong>Figure 10:</strong> Kernel density plot for wind speed under the SSP370 scenario.
  <br><br><br> 
</div>

<div align="center">
  <img src="https://github.com/user-attachments/assets/88f1b633-76be-42d6-ab9e-af5bffcea7f0">
  <br>
  <strong>Figure 11:</strong> Returning period plot for wind speed under the SSP370 scenario.
  <br><br><br> 
</div>

<div align="center">
  <img src="https://github.com/user-attachments/assets/ef3e12e2-5afe-4289-b990-7a1af6533c9b">
  <br>
  <strong>Figure 12:</strong> Kernel density plot for temperature under the SSP370 scenario.
  <br><br><br> 
</div>

<div align="center">
  <img src="https://github.com/user-attachments/assets/4296558c-c65a-478f-9c9a-df6784919dd5">
  <br>
  <strong>Figure 13:</strong> Returning period plot for temperature under the SSP370 scenario.
  <br><br><br> 
</div>

## Conclusions:


## Future directions:

* Apply this analysis to other models also recommended by Bazzanella et al. (4).  

## References

(1) Andreoni, M. (2023, August 10). Uruguay wasn’t supposed to run out of water. The New York Times. https://www.nytimes.com/2023/08/10/climate/uruguay-wasnt-supposed-to-run-out-of-water.html 

(2) INUMET. (n.d.). Quintiles de precipitación. https://www.inumet.gub.uy/clima/recursos-hidricos/quintiles-de-precipitacion

(3) Inumet (2024, January 17). Finalizó la sequía meteorológica 2020-2023 en todo el Uruguay. https://www.inumet.gub.uy/sala-de-prensa/noticias/finalizo-la-sequia-meteorologica-2020-2023-en-todo-el-uruguay

(4) Bazzanela, A. C., Dereczynski, C., Luiz‐Silva, W., & Regoto, P. (2024). Performance of CMIP6 models over South America. Climate Dynamics, 62, 1501-1516. https://doi.org/10.1007/s00382-023-06979-1

(5) Intergovernmental Panel on Climate Change. (2021). Summary for Policymakers. In: Climate Change 2021: The Physical Science Basis. Contribution of Working Group I to the Sixth Assessment Report of the Intergovernmental Panel on Climate Change. https://doi.org/10.1017/9781009157896.001

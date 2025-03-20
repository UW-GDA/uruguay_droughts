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

For this project I chose EC-EARTH3 and TaiESM1-0 models, since previous studies concluded that they exhibit superior performance in Southeastern South America (4). Also, I selected the SSP3–7.0 scenario, which represents a future where greenhouse gas emissions would double by 2100, resulting in an estimated warming of 2.1 °C from 2041–2060 and 3.6 °C from 2081–2100 (5).

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

### 1- Data preprocessing: 

* Convert units for better interpretability.
* Aggregate daily data into monthly data.
* Extract Uruguay-specific data from the global dataset.
* Divide data into three periods: historical, Future 1, and Future 2

### 2 - Counting analysis:

* Determine category ranges for wind speed and precipitation.
* Assess future precipitation trends using INUMET’s definitions.

### 3 - Severity analysis:

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
  <img src="https://github.com/user-attachments/assets/804de9f2-8c43-4bd5-ad4d-1e7d8a731a09">
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
  <img src="https://github.com/user-attachments/assets/3d3a67ae-4f86-4e06-8a9b-bd0fe8473a2b">
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
  <img src="https://github.com/user-attachments/assets/675928f2-a418-4342-ba9c-65ad36cc57fd">
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
  <img src="https://github.com/user-attachments/assets/47fa82a3-8568-44e2-997f-3a21a4586d09">
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
  <img src="https://github.com/user-attachments/assets/72f81970-fa04-4d9e-bce1-639dac758f6c">
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
  <img src="https://github.com/user-attachments/assets/4df41a48-440b-4293-94ba-988283fc7871">
  <br>
  <strong>Figure 13:</strong> Returning period plot for temperature under the SSP370 scenario.
  <br><br><br> 
</div>

## Analysis:

### Precipitation and ssp126 (Figures 2 and 3):

#### EC-Earth3 model
Analyzing Figure 2, we can see that the range of consecutive drought months during the historical period is larger than in both future periods, which have fairly similar kernel density plots. For lower values of consecutive months, Figure 3 shows comparable return periods across the three periods. However, in the historical period, we observe lower return period values for four consecutive months, along with episodes of five or more consecutive months, which are absent in the future periods. This indicates a future with fewer prolonged low-precipitation episodes compared to the historical period.

#### TaiESM1 model
The kernel density plots for this model show similar distributions for the historical and future 1 periods, compared to future 2, which appears more dispersed in terms of the number of consecutive months. The return periods are similar up to four consecutive months, after which the differences become more pronounced. Future 2 exhibits the highest number of consecutive months, followed by the historical period and then future 1, suggesting that in the far future, extreme events may last longer than those observed during the historical period.

### Wind speed and ssp126 (Figures 4 and 5):

#### EC-Earth3 model

The kernel density distribution for the historical and Future 1 periods appears almost identical, while the Future 2 kernel plot shows a broader range of consecutive months. Regarding the return periods, the historical period seems to fall between Future 1 and Future 2. In Future 1, wind speed extremes occur for fewer consecutive months at higher return periods, and this pattern worsens in Future 2, with longer drought periods observed at lower return periods.

#### TaiESM1 model

For the TaiESM1 model, we notice a reduction in the range of consecutive months over time (Historical > Future 1 > Future 2). Despite this, we observe similar return periods up to four consecutive months. Beyond that, Future 2 shows longer return periods than Future 1, and Future 1 shows longer return periods than the historical period.

### Temperature and ssp126 (Figures 6 and 7):

#### EC-Earth3 model

For the EC-Earth3 model, the kernel density plots show very similar shapes. This similarity is also reflected in the return period plot, with a substantial difference only in the return period for six consecutive months. While the historical period shows a 15-year return period, the future periods show values of 3 and 5 years, indicating a higher frequency of extreme temperature events.

#### TaiESM1 model

In contrast to the previous model, this one shows a similar density distribution for the historical period, but the future periods differ, being more concentrated at lower consecutive month values. However, we observe higher return periods for up to three consecutive months compared to the historical period, indicating fewer episodes and less severe extreme temperature events the opposite conclusion of the previous model.

### Precipitation and ssp370 (Figures 8 and 9):

#### EC-Earth3 model

Here, we observe a temporal trend where the historical period shows higher consecutive month values compared to Future 1, followed by Future 2, with values becoming more concentrated at lower levels over time. In the return period plot, we observe a similar pattern to the SSP126 scenario, where the future periods have longer return periods for the same number of consecutive months compared to the historical period.

#### TaiESM1 model

In contrast, the TaiESM1 model provides conclusions similar to those for the SSP126 scenario, where the historical period shows fewer consecutive months and longer return periods, presenting conclusions that are almost the opposite of those from the EC-Earth3 model.

### Wind speed and ssp370 (Figures 10 and 11):

#### EC-Earth3 model

Here, we see that the historical and Future 1 periods have similar kernel density plots, while Future 2 concentrates on lower values of consecutive months. Despite this, Future 2 has the longest return periods, followed by Future 1 and then the historical period. This leads us to the conclusion that, in the future, we will experience less severe and less frequent wind drought events.

#### TaiESM1 model

In the kernel density plots, we see how Future 2 appears to be midway between the historical period and Future 1, with Future 1 being more concentrated on lower consecutive month values. Despite this, as with the previous model, the historical period shows smaller return period values compared to the future scenarios.

### Temperature and ssp370 (Figures 12 and 13):

#### EC-Earth3 model

Here, we see identical future distributions that are more dispersed in consecutive month values than the historical period, which is slightly more concentrated on lower values. However, the return period plots are almost identical up to five consecutive months, after which the historical period shows the highest return period values, indicating a future with more extreme temperature events.

#### TaiESM1 model

We see Future 2 as being midway between Future 1 and the historical period, with the latter being more dispersed at higher values of consecutive months. This behavior is also reflected in the return period plots, where Future 1 shows the smallest consecutive month values and the highest return periods, while the historical period shows the largest consecutive month values and the lowest return periods. This indicates a future where, initially, such episodes will become less common and severe, but later, they will increase in both frequency and severity.

## Conclusions:

### Scenarios comparison:

### Models comparison:

## Future directions:

* Apply this analysis to other models also recommended by Bazzanella et al. (4).
* Look for spatial trends.  

## References

(1) Andreoni, M. (2023, August 10). Uruguay wasn’t supposed to run out of water. The New York Times. https://www.nytimes.com/2023/08/10/climate/uruguay-wasnt-supposed-to-run-out-of-water.html 

(2) INUMET. (n.d.). Quintiles de precipitación. https://www.inumet.gub.uy/clima/recursos-hidricos/quintiles-de-precipitacion

(3) Inumet (2024, January 17). Finalizó la sequía meteorológica 2020-2023 en todo el Uruguay. https://www.inumet.gub.uy/sala-de-prensa/noticias/finalizo-la-sequia-meteorologica-2020-2023-en-todo-el-uruguay

(4) Bazzanela, A. C., Dereczynski, C., Luiz‐Silva, W., & Regoto, P. (2024). Performance of CMIP6 models over South America. Climate Dynamics, 62, 1501-1516. https://doi.org/10.1007/s00382-023-06979-1

(5) Intergovernmental Panel on Climate Change. (2021). Summary for Policymakers. In: Climate Change 2021: The Physical Science Basis. Contribution of Working Group I to the Sixth Assessment Report of the Intergovernmental Panel on Climate Change. https://doi.org/10.1017/9781009157896.001

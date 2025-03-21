# Evaluating the frequency and severity of wind and meteorological droughts in Uruguay

![image](https://github.com/user-attachments/assets/a4c37e8d-1682-4fc8-9e05-60e615748b88)


## Member
Hernán Querbes

## Short summary
In this work, I will study the frequency and severity of meteorological and wind droughts, as well as extreme temperature episodes, over Uruguay for two future periods: Future 1 (2030s), covering 2025 to 2044, and Future 2 (2050s), covering 2045 to 2064. For this, I will use NASA’s NEX-GDDP-CMIP6 dataset and the SSP1-2.6 and SSP3-7.0 scenarios for future projections.

## Introduction/background

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


INUMET defines a meteorological drought as three or more consecutive months with a precipitation category equal to or less than 2 (3). I will adopt an analogous definition for wind droughts and extreme temperature events. However, in the case of extreme temperature events, I will identify sequences of months with a category equal to or greater than 4, as I want to look for high temperature episodes.

For this project I chose EC-EARTH3 and TaiESM1-0 models, since previous studies concluded that they exhibit superior performance in Southeastern South America (4). Also, I selected two scenarios for future projections:
* SSP1–2.6: 1.8 °C predicts an estimated warming by the end of the century
* SSP3–7.0: 3.8 °C predicts an estimated warming by the end of the century
  
## Problem statement and questions

My current research focuses on assessing the impact of climate change on hydroelectric production in Uruguay, specifically how meteorological and wind droughts affect it. For this reason, the questions I plan to answer in this project are:

1- Will meteorological/wind droughts change in frequency and severity in the future?

2- How will the frequency and severity of extreme temperature events change in the future?

## Dataset

NASA’s NEX-GDDP-CMIP6 dataset: https://www.nccs.nasa.gov/services/data-collections/land-based-products/nex-gddp-cmip6
* Data Resolution:
  * Latitude and Longitude resolution: 0.25 degrees (25 km)
  * Temporal Resolution: daily
  * Variables used:
    * Precipitation (pr)
    * Wind speed (sfcWind)
    * Temperature (tas)

## Tools/packages

Matplotlib https://matplotlib.org/stable/ 

Numpy https://numpy.org/doc/stable/index.html 

Xarray https://docs.xarray.dev/en/stable/ 

Rioxarray https://corteva.github.io/rioxarray/html/rioxarray.html 

Geopandas https://geopandas.org/en/stable/index.html# 

Seaborn https://seaborn.pydata.org/

## Repository structure

* Filtered_data: Folder where the downloaded data is stored.
* Data: Notebook used to download data.
* Functions: Notebook used to perform the analysis.
* gddp-cmip6-thredds-fileserver: CSV file containing URLs for accessing the climate data (used by the Data notebook).
* ury_adm_2020_shp: File containing Uruguay's shape geometry.

## Planned methodology/aproach

### 1- Data preprocessing 

* Clip Uruguay geometry to the dataset.
* Aggregate daily data into monthly data (Precipitation: sum. Wind speed and temperature: mean)
* Divide data into three periods: historical, Future 1, and Future 2

### 2 - Categorization analysis

* Categorize each monthly value for the three variables and three periods using the INUMET method.
  
### 3 - Severity analysis

* Measure the duration of drought episodes (in months).

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

The methodology is synthetized in the next figure:

<div align="center">
  <img src="https://github.com/user-attachments/assets/13d1c4dd-d981-4624-9476-1db3bf8d84a2">
  <br>
  <strong>Figure 1:</strong> Methodology ilustration.
  <br><br><br> 
</div>

### 4 - Plots

* Construct Kernel density plots and returning period plots for the three variables and periods of time.
  
## Expected outcomes

There are two expected outcomes:

1- Kernel density plots (number of consecutive drought months) for the three time periods.

2- Returning period plots (number of consecutive drought months) for the three time periods.

## Results

### Data pre-processing
The dataset consisted of daily values for precipitation, wind speed, and temperature. These variables were aggregated as follows:
* Precipitation: Aggregated by monthly sum.
* Wind speed and temperature: Aggregated by monthly mean.

![download](https://github.com/user-attachments/assets/ea1ea3e9-e07b-4e38-9fb7-4b8d02370c33)

This was done for all three variables across three time periods.

Then the analysis was performed, resulting in the next plots:

<div align="center">
  <img src="https://github.com/user-attachments/assets/df5a7c83-32f8-4cac-b700-9deef49d782f">
  <br>
  <strong>Figure 2:</strong> Kernel density plot for precipitation under the SSP126 scenario.
  <br><br><br> 
</div>

<div align="center">
  <img src="https://github.com/user-attachments/assets/68466421-b9eb-44fd-bf3b-6a4ab524369d">
  <br>
  <strong>Figure 3:</strong> Returning period plot for precipitation under the SSP126 scenario.
  <br><br><br> 
</div>

<div align="center">
  <img src="https://github.com/user-attachments/assets/9361b6fa-7155-4f35-bca4-17962e0213ed">
  <br>
  <strong>Figure 4:</strong> Kernel density plot for wind speed under the SSP126 scenario.
  <br><br><br> 
</div>

<div align="center">
  <img src="https://github.com/user-attachments/assets/39c19105-a2d2-4375-9cb7-c7f2b2cb2111">
  <br>
  <strong>Figure 5:</strong> Returning period plot for wind speed under the SSP126 scenario.
  <br><br><br> 
</div>

<div align="center">
  <img src="https://github.com/user-attachments/assets/4ade72a4-5871-4d56-a94d-2542572bb722">
  <br>
  <strong>Figure 6:</strong> Kernel density plot for temperature under the SSP126 scenario.
  <br><br><br> 
</div>

<div align="center">
  <img src="https://github.com/user-attachments/assets/e8525dff-4352-4755-b0e1-5ed1adc576ec">
  <br>
  <strong>Figure 7:</strong> Returning period plot for temperature under the SSP126 scenario.
  <br><br><br> 
</div>

<div align="center">
  <img src="https://github.com/user-attachments/assets/9cdf894d-1179-4e0e-9671-09c682a5df24">
  <br>
  <strong>Figure 8:</strong> Kernel density plot for precipitation under the SSP370 scenario.
  <br><br><br> 
</div>

<div align="center">
  <img src="https://github.com/user-attachments/assets/7d19b8a7-cff5-4e46-a5e7-d4e9c20f1d7f">
  <br>
  <strong>Figure 9:</strong> Returning period plot for precipitation under the SSP370 scenario.
  <br><br><br> 
</div>

<div align="center">
  <img src="https://github.com/user-attachments/assets/17b7353a-336f-4590-8783-f054193a35c2">
  <br>
  <strong>Figure 10:</strong> Kernel density plot for wind speed under the SSP370 scenario.
  <br><br><br> 
</div>

<div align="center">
  <img src="https://github.com/user-attachments/assets/ce241ef1-4a19-43e0-9e09-af0b79fc8018">
  <br>
  <strong>Figure 11:</strong> Returning period plot for wind speed under the SSP370 scenario.
  <br><br><br> 
</div>

<div align="center">
  <img src="https://github.com/user-attachments/assets/0e7c27af-ef91-47d1-be22-279f76ac2459">
  <br>
  <strong>Figure 12:</strong> Kernel density plot for temperature under the SSP370 scenario.
  <br><br><br> 
</div>

<div align="center">
  <img src="https://github.com/user-attachments/assets/cc154015-1b23-41f7-8fed-fba2166dd5ee">
  <br>
  <strong>Figure 13:</strong> Returning period plot for temperature under the SSP370 scenario.
  <br><br><br> 
</div>

## Analysis

### Precipitation and ssp126 (Figures 2 and 3)

#### EC-Earth3 model
Analyzing Figure 2, we can see that the range of consecutive drought months during the historical period is larger than in both future periods, which have fairly similar kernel density plots. For lower values of consecutive months, Figure 3 shows comparable return periods across the three periods. However, in the historical period, we observe lower return period values for four consecutive months, along with episodes of five or more consecutive months, which are absent in the future periods. This indicates a future with fewer prolonged low-precipitation episodes compared to the historical period.

#### TaiESM1 model
The kernel density plots for this model show similar distributions for the historical and future 1 periods, compared to future 2, which appears more dispersed in terms of the number of consecutive months. The return periods are similar up to four consecutive months, after which the differences become more pronounced. Future 2 exhibits the highest number of consecutive months, followed by the historical period and then future 1, suggesting that in the far future, extreme events may last longer than those observed during the historical period.

### Wind speed and ssp126 (Figures 4 and 5)

#### EC-Earth3 model

The kernel density distribution for the historical and Future 1 periods appears almost identical, while the Future 2 kernel plot shows a broader range of consecutive months. Regarding the return periods, the historical period seems to fall between Future 1 and Future 2. In Future 1, wind speed extremes occur for fewer consecutive months at higher return periods, and this pattern worsens in Future 2, with longer drought periods observed at lower return periods.

#### TaiESM1 model

For the TaiESM1 model, we notice a reduction in the range of consecutive months over time (Historical > Future 1 > Future 2). Despite this, we observe similar return periods up to four consecutive months. Beyond that, Future 2 shows longer return periods than Future 1, and Future 1 shows longer return periods than the historical period.

### Temperature and ssp126 (Figures 6 and 7)

#### EC-Earth3 model

For the EC-Earth3 model, the kernel density plots show very similar shapes. This similarity is also reflected in the return period plot, with a substantial difference only in the return period for six consecutive months. While the historical period shows a 15-year return period, the future periods show values of 3 and 5 years, indicating a higher frequency of extreme temperature events.

#### TaiESM1 model

In contrast to the previous model, this one shows a similar density distribution for the historical period, but the future periods differ, being more concentrated at lower consecutive month values. However, we observe higher return periods for up to three consecutive months compared to the historical period, indicating fewer episodes and less severe extreme temperature events the opposite conclusion of the previous model.

### Precipitation and ssp370 (Figures 8 and 9)

#### EC-Earth3 model

Here, we observe a temporal trend where the historical period shows higher consecutive month values compared to Future 1, followed by Future 2, with values becoming more concentrated at lower levels over time. In the return period plot, we observe a similar pattern to the SSP126 scenario, where the future periods have longer return periods for the same number of consecutive months compared to the historical period.

#### TaiESM1 model

In contrast, the TaiESM1 model provides conclusions similar to those for the SSP126 scenario, where the historical period shows fewer consecutive months and longer return periods, presenting conclusions that are almost the opposite of those from the EC-Earth3 model.

### Wind speed and ssp370 (Figures 10 and 11)

#### EC-Earth3 model

Here, we see that the historical and Future 1 periods have similar kernel density plots, while Future 2 concentrates on lower values of consecutive months. Despite this, Future 2 has the longest return periods, followed by Future 1 and then the historical period. This leads us to the conclusion that, in the future, we will experience less severe and less frequent wind drought events.

#### TaiESM1 model

In the kernel density plots, we see how Future 2 appears to be midway between the historical period and Future 1, with Future 1 being more concentrated on lower consecutive month values. Despite this, as with the previous model, the historical period shows smaller return period values compared to the future scenarios.

### Temperature and ssp370 (Figures 12 and 13)

#### EC-Earth3 model

Here, we see identical future distributions that are more dispersed in consecutive month values than the historical period, which is slightly more concentrated on lower values. However, the return period plots are almost identical up to five consecutive months, after which the historical period shows the highest return period values, indicating a future with more extreme temperature events.

#### TaiESM1 model

We see Future 2 as being midway between Future 1 and the historical period, with the latter being more dispersed at higher values of consecutive months. This behavior is also reflected in the return period plots, where Future 1 shows the smallest consecutive month values and the highest return periods, while the historical period shows the largest consecutive month values and the lowest return periods. This indicates a future where, initially, such episodes will become less common and severe, but later, they will increase in both frequency and severity.

### Scenarios and models comparison

#### Precipitation

For each model, we observe similar density distributions and return period values across the different future scenarios. While the EC-Earth3 model suggests a future with less severe and less frequent drought episodes, the TaiESM1 model predicts slightly more frequent episodes in the future. No clear conclusion can be drawn from the comparison of these two models.

#### Wind speed

For the EC-Earth3 model, we observe that the behavior of Future 2 is more dependent on the scenario. In an optimistic future (SSP126), it exhibits fewer wind drought episodes than in the past, while in a less optimistic future (SSP370), it shows more frequent extreme events. On the other hand, the TaiESM1 model predicts a future with fewer episodes under both scenarios, suggesting a general trend toward fewer wind drought episodes in the future.

#### Temperature

The plots appear similar for both future scenarios. The most noticeable differences are between the models. While the EC-Earth3 model exhibits very similar behavior across the three periods (except for the six consecutive months episode, which shows considerable differences in the return period), the TaiESM1 model predicts similar futures for the SSP126 scenario, where events are less frequent than in the past. A similar pattern occurs in the SSP370 scenario, although here the short-term future appears worse than the long-term future.  No clear conclusion can be drawn from the comparison of these two models.

## Conclusions

* Drought Events:
  * EC-Earth3: Fewer drought episodes for precipitation (more wetter future). More frequent wind drought in optimistic conditions (SSP126) but less frequent and severe events in pessimistic conditions (SSP370)
  * TaiESM1: Consistently predicts fewer and less severe drought episodes across both scenarios.
* Extreme Temperature Events:
  * EC-Earth3: Projected increase in frequency and severity of extreme temperature events.
  * TaiESM1: Initially less frequent episodes, but worsening conditions over scenarios.

## Future directions

* Apply this analysis to other models also recommended by Bazzanella et al. (4).
* Look for spatial trends.  

## References

(1) Andreoni, M. (2023, August 10). Uruguay wasn’t supposed to run out of water. The New York Times. https://www.nytimes.com/2023/08/10/climate/uruguay-wasnt-supposed-to-run-out-of-water.html 

(2) INUMET. (n.d.). Quintiles de precipitación. https://www.inumet.gub.uy/clima/recursos-hidricos/quintiles-de-precipitacion

(3) Inumet (2024, January 17). Finalizó la sequía meteorológica 2020-2023 en todo el Uruguay. https://www.inumet.gub.uy/sala-de-prensa/noticias/finalizo-la-sequia-meteorologica-2020-2023-en-todo-el-uruguay

(4) Bazzanela, A. C., Dereczynski, C., Luiz‐Silva, W., & Regoto, P. (2024). Performance of CMIP6 models over South America. Climate Dynamics, 62, 1501-1516. https://doi.org/10.1007/s00382-023-06979-1

(5) Intergovernmental Panel on Climate Change. (2021). Summary for Policymakers. In: Climate Change 2021: The Physical Science Basis. Contribution of Working Group I to the Sixth Assessment Report of the Intergovernmental Panel on Climate Change. https://doi.org/10.1017/9781009157896.001

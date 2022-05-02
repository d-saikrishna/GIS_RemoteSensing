# Delhi breathes during COVID-19?

## Abstract

On the evening of March 24 2020, the Indian government announced a national lockdown in its fight against COVID-19. A similar lockdown was announced during the second wave of COVID-19 in 2021, during the months of April-June. These lockdowns came as an exogenous shock to human mobility and economic activities. As per the Google Mobility data, mobility fell up to 80% during the lockdown periods. There was an associated fall in industrial activity, businesses etc., as well. This led to a 27% reduction in NO2 pollution and a 50% reduction in aerosol values during the first lockdown. Other environmental variables like temperature, vegetation cover, water quality also negatively correlate with mobility and economic activity during both the lockdown periods. This evidence can guide urban policies on mobility, pollution and heat wave management.

## Study Area and Data sources:

The city of Delhi is chosen as the study area for this research. 

![Administrative boundary of the Union Territory of Delhi](Delhi%20breathes%20during%20COVID-19%203f901418ae164568b88540490f90f98e/Untitled.png)

Administrative boundary of the Union Territory of Delhi

[Delhi is the most polluted capital city in the world](https://www.business-standard.com/article/current-affairs/new-delhi-world-s-most-polluted-capital-city-for-2nd-consecutive-year-122032200328_1.html#:~:text=Photo%3A%20ANI-,New%20Delhi%20has%20been%20ranked%20the%20world's%20most%20polluted%20capital,2021%2C%2012%20were%20in%20India.) and is also registering [record summer temperatures and heat waves.](https://www.indiatoday.in/cities/delhi/story/india-witnesses-hottest-march-in-122-yrs-heatwave-to-continue-in-delhi-1933173-2022-04-04) Various mobility reduction programs were taken up by the Delhi government (Odd-Even, Ek Trip Kam) to combat air pollution, especially during winters. However, multiple research projects have not been able to find a statistically significant impact of these mobility reduction programs on air pollution. Given that [two-wheelers are a dominant source of air pollution](https://www.nature.com/articles/ncomms4749), exempting them from the Odd-Even policy was suggested as one of the reasons behind this. However, the mobility reduction during the lockdowns impacted two wheeler mobility as well. In this light, it gives me another opportunity to re-investigate the effect of reduction in mobility on air pollution.

I also hypothesize that the reduction in pollution would have led to reduced temperatures due to the reduction in urban heat island effect. This relation is studied in this research. Other environmental variables like precipitation, vegetation, open waters are also studied. A brief description of these variables is given in the table below:

| Variable (Units) | Source | Resolution | Description |
| --- | --- | --- | --- |
| NO2_column_number_density (mol/m^2) | European Union/ESA/Copernicus | Spatial: 1113.2 meters
Temporal: Daily | Total vertical column of NO2 (ratio of the slant column density of NO2 and the total air mass factor). |
| tmmx (degrees Celsius) | TERRACLIMATE | Spatial: 4638.3 meters
Temporal: Monthly | Monthly mean maximum temperature (with a scale factor 0.1) |
| Precipitation (mm/day) | IMERG | Spatial: 0.2*0.2 degree^2
Temporal: Daily | Height of the equivalent liquid water in a square meter per time interval. |
| absorbing_aerosol_index (unitless) | European Union/ESA/Copernicus | Spatial: 1113.2 meters
Temporal: Daily | When the AAI is positive, it indicates the presence of UV-absorbing aerosols like dust and smoke. |
| Aerosol Optical Depth - Blue band. | MODIS | Spatial: 1000m
Temporal: Daily | Blue band (0.47 μm) aerosol optical depth over land |
| NDVI (unitless -1 to 1) | Copernicus/S2 | Spatial: 10 meters
Temporal: ~2 per week | Normalized difference of bands B8 (NIR) and B4 (Red) of Copernicus S2. Higher the NDVI, greener the pixel. |
| NDTI (unitless -1 to 1) | Copernicus/S2 | Spatial: 10 meters
Temporal: ~2 per week | Normalized difference of bands B3 (Green) and B4 (Red) of Copernicus S2. Higher the NDTI, higher the turbidity of water. I captured this index for open water features in Delhi obtained by using MNDWI as mask. |
| avg_rad (nanoWatts/cm2/sr) | NOAA/VIIRS | Spatial: 463.83  meters
Temporal: Monthly | Average DNB radiance values. |
| retail_and_recreation_percent_change_from_baseline (%) | Google Community Mobility Report | Spatial: disrict and state levels
Temporal: Daily - available from 2020. | Retail mobility change from the baseline value. Baseline value is the median day of the week during the 5 week period of Jan3rd-Feb6th 2020.

While there are many categories of mobility (workplace, retail etc); they followed almost a similar trend during lockdowns. Considering only retail mobility.  |

All variables are considered between the years 2017-2021. These variables are also standardized for the purposes of regression analysis using percentage change from baseline value. The baseline considered here is the mean value during Jan3rd-Feb6th of 2021.

The code for data collection can be found here - [Link](https://github.com/d-saikrishna/GIS_RemoteSensing/blob/master/Covid_Env/Data%20Collection%20and%20Pre-Processing.ipynb)

The code for regression analysis can be found here - [Link](https://github.com/d-saikrishna/GIS_RemoteSensing/blob/master/Covid_Env/Correlations.ipynb)

The code for causal estimation can be found here - [Link](https://github.com/d-saikrishna/GIS_RemoteSensing/blob/master/Covid_Env/Causality.ipynb)

## Mobility and Economic impact of COVID-19 on Delhi

Lockdowns in India were at phases of various stringency. The 2020 lockdown was a national lockdown that existed from 24th March to 31st May. In 2021, lockdowns were more regional. In Delhi, lockdown 2 was in force from 19th April to 7th June. The associated changes in retail mobility during these periods can be seen in the figure below. 

![Google Community Mobility Report - Delhi](Delhi%20breathes%20during%20COVID-19%203f901418ae164568b88540490f90f98e/Untitled%201.png)

Google Community Mobility Report - Delhi

There were associated changes in the economy of Delhi as well. The [2021 Economic Survey](http://delhiplanning.nic.in/sites/default/files/2.%20State%20Economy.pdf) of the Delhi government reported a 5.6% dip in Delhi’s economy in 2020-21 and a 20,000 INR reduction in per capita income. However, a more granular official data for economy is not available. It is well accepted in the research community that [night lights data is a good proxy for economic performance, especially for urban areas](https://www.sciencedirect.com/science/article/pii/S235293852100183X?via%3Dihub). I thus first test this hypothesis by exploring the relationship between night lights and mobility.

![Night light levels in 2020 April compared to 2019 April - Fall observed both in mean and peak values.](Delhi%20breathes%20during%20COVID-19%203f901418ae164568b88540490f90f98e/Untitled%202.png)

Night light levels in 2020 April compared to 2019 April - Fall observed both in mean and peak values.

I further regressed the night lights level with retail mobility change to observe that a one percent reduction in mobility caused an 0.03 (nanoWatts/cm2/sr) reduction in night light level. On the days of severe lockdown, when mobility fell by more than 80%, this corresponds to a fall of 1.6 (nanoWatts/cm2/sr) in night lights level. I assume a high sensitivity of night lights level with respect to mobility and economic activity.

![Both month and year fixed effects are considered.](Delhi%20breathes%20during%20COVID-19%203f901418ae164568b88540490f90f98e/Untitled%203.png)

Both month and year fixed effects are considered.

With this evidence, I proceed to find the impact of COVID-19 on environmental variables on three levels. Firstly, I do a high-level analysis on the environmental variables exploring how they got impacted in 2020 and 2021 compared to pre-COVID19 years. Secondly, I regress environmental variables with both mobility and night lights levels to get a more granular insight on relationship between environment and mobility, economy. Finally, to understand the causality dynamics, I use time series forecasting to predict the environmental variables for 2020 Lockdown period using the pre-COVID19 data. Then I use this forecast as the control group and compare it with the actual data as the treatment group. 

### 1 . High-level analysis

I first compare the yearly means of all environmental variables to get preliminary evidence of the effect of COVID19. Since the reductions in mobility and economy persisted for greater part of the year, I hypothesize that the effect would be captured in yearly means. The results are in the figure below.

![Untitled](Delhi%20breathes%20during%20COVID-19%203f901418ae164568b88540490f90f98e/Untitled%204.png)

A few observations from the above figure:

1. There is visually considerable improvement in NDVI, aerosol levels and NO2 levels validating my hypothesis. Other variables have to be statistically tested.
2. There is an element of trend in a few variables (NO2 pollution, night lights). To delineate the trend effect from our analysis, de-trending has been done.

I test above observations by regressing the percent change of environmental variables with dummy variables representing Lockdown-1 and Lockdown-2 periods. The results are shown in the figure below:

![All regressions considered both month and year fixed effects to remove seasonality and trend effects.](Delhi%20breathes%20during%20COVID-19%203f901418ae164568b88540490f90f98e/Untitled%205.png)

All regressions considered both month and year fixed effects to remove seasonality and trend effects.

During the first lockdown, I observe that maximum temperature reduced by 4%, NO2 pollution reduced by 14%, night lights level reduce by 2%. Water turbidity, represented by NDTI, also reduced by 10% while vegetation cover (NDVI) increased by 10%. The pattern remains similar during the second lockdown as well for most variables. I explain these observations through following mechanisms:

- **NO2 Pollution:** I hypothesize a direct causal relationship between lockdown and reduction in NO2 levels. The primary sources of NO2 are vehicular emissions, industries — most of them saw reduced activity during Lockdown1. The activity was slightly higher during Lockdown2, but still less than baseline. These reductions would have *caused* reduction in NO2 pollution.

![May 2019 - Mean NO2](Delhi%20breathes%20during%20COVID-19%203f901418ae164568b88540490f90f98e/Untitled%206.png)

May 2019 - Mean NO2

![May 2020 - Mean NO2](Delhi%20breathes%20during%20COVID-19%203f901418ae164568b88540490f90f98e/Untitled%207.png)

May 2020 - Mean NO2

![May 2021 - Mean NO2](Delhi%20breathes%20during%20COVID-19%203f901418ae164568b88540490f90f98e/Untitled%208.png)

May 2021 - Mean NO2

- **NDTI:** NDTI represents turbidity of water. I hypothesize that reduced economic activity also reduced water pollution and thus reduced NDTI levels during lockdowns.
- **NDVI:** It is far-fetched to assume that lockdowns immediately increased tree cover in the city. But the lockdown would have curbed de-forestation activities in the forest belts of Delhi. Moreover, [the increase in NDVI could be because of increased crop area.](https://link.springer.com/article/10.1007/s12524-020-01213-5) [Delhi has agricultural lands](https://ruralindiaonline.org/en/articles/they-say-there-are-no-farmers-in-delhi/). Delayed harvesting of Rabi crop and increased cropping of Zaid crop (as labor was out of work) could have contributed to it. Another research found a similar [increase of NDVI in Jaipur](https://www.researchgate.net/publication/351286542_COVID-19_lockdown_effect_on_land_surface_temperature_and_normalized_difference_vegetation_index_Subhanil_Guha_Himanshu_Govil_COVID-19_lockdown_effect_on_land_surface_temperature_and_normalized_differe).
- **Maximum temperature:** I hypothesize the reduction in maximum temperature using the urban heat island theory. According to which, cities experience more temperature due to the presence of green house gases in atmosphere. Though NO2 is not a greenhouse gas, it plays a prominent role in creation of tropospheric ozone, which is a greenhouse gas. Moreover, I assume that just like NO2 levels reduced during lockdowns, greenhouse gases like CO2, CO, SO2 would also have reduced. This, along with increased vegetation, could have contributed to reduction in maximum temperature.

With reduction in mobility, it was expected that aerosols in air would reduce (lesser particulate matter). However, the results for aerosols are not statistically significant. I further explore this behavior in the next section.

### 2. Statistical relationship between environmental variables and mobility/economy

In this section, I regress the percent change in the environmental variables with the percentage change in retail mobility and night lights level from their respective baseline values. The environmental variables are de-seasonalized and de-trended by differencing them with their values an year ago. I interpolate for the missing values during the month for variables that are not at daily frequency. The results from the regression analyses are present in the figures below.

![Untitled](Delhi%20breathes%20during%20COVID-19%203f901418ae164568b88540490f90f98e/Untitled%209.png)

![Untitled](Delhi%20breathes%20during%20COVID-19%203f901418ae164568b88540490f90f98e/Untitled%2010.png)

![Untitled](Delhi%20breathes%20during%20COVID-19%203f901418ae164568b88540490f90f98e/Untitled%2011.png)

![Untitled](Delhi%20breathes%20during%20COVID-19%203f901418ae164568b88540490f90f98e/Untitled%2012.png)

![Untitled](Delhi%20breathes%20during%20COVID-19%203f901418ae164568b88540490f90f98e/Untitled%2013.png)

![Untitled](Delhi%20breathes%20during%20COVID-19%203f901418ae164568b88540490f90f98e/Untitled%2014.png)

From the results, I observe that if mobility reduces by 10%:

1. NO2 pollution would reduce by ~5%
2. Maximum temperature would reduce by ~1%
3. Vegetation cover (NDVI) would increase by ~1%
4. Water turbidity (NDTI) would reduce by ~1%
5. Precipitation did not show a direct effect. But upon using a lag of two months it showed a 7% increase. However, I recognize this is a far-fetched assumption.
6. Aerosol Index continues to show a in-significant statistic.

The patterns with respect to night lights are similar, except for aerosols. Increase in night lights level  by 1% shows a reduction in aerosol level by 1%. I suspect that this counter intuitive assumption is because the presence of aerosols in air affects the measurement of night lights values.

All the analysis so far only observes correlation between the variables of interest. To further test my hypothesis that COVID-19 induced mobility and economic changes caused improvements in environment, I should conduct an experiment. However, given the global nature of COVID-19, there is no control group available for a city like Delhi. Hence, in the next section, I build a control group using time series forecasting and compare that with observed data, to establish causal relationships.

### 3. Causality

To build a counter-factual control group, I use the data of environmental variables available between 2017-2019 to forecast them for the first 5 months of 2020. In the figure below, the green dashed line represents the last training data value in 2019. The period between the green dashed line and the first red dashed line represents the pre-COVID period of 2020. This period allows us to test our forecast. The period between the two red dashed lines represent the first lock-down. Fbprophet model was used for time series forecasting. 

![Untitled](Delhi%20breathes%20during%20COVID-19%203f901418ae164568b88540490f90f98e/Untitled%2015.png)

I observe a distinct variation during the lockdown period, between the control and treatment group for the variables temperature, NO2 and aerosol levels. Finally, I perform a differences-in-differences test to establish the causality. *envar* is the environmental variable of interest. $\beta_3$ is the main co-efficient that measures the causality. *treatment* refers to the treated group, i.e., the observed data. *after* refers to the period of treatment i.e., the first lockdown period.

$envar = \beta_0 + \beta_1*treatment +\beta_2*after +\beta_3*(treatment*after)$ 

![Regression results of differences in differences - environmental variables in their respective units](Delhi%20breathes%20during%20COVID-19%203f901418ae164568b88540490f90f98e/Untitled%2016.png)

Regression results of differences in differences - environmental variables in their respective units

With these results in hand, I make the following final observations:

1. The reduction in temperature saw a strong correlation with lockdown, but it’s observed that  this correlation is not a causation.
2. Causal explanations can be provided to pollution variables. NO2 pollution reduced by 27%  and Aerosol depth reduced by 50% compared to the counter-factual group. As it was researched that a [1% reduction in AOD reduces PM2.5 by 0.5%](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3237057/), this would have led to about 25% reduction in PM2.5 in Delhi. 

## Further research:

The causal explanation of temperature is still a matter of interest as per the Urban Heat Island theory. However, there is an alternative hypothesis as per some research work. According to which, the [reduced aerosol concentration in atmosphere led to increased solar irradiance](https://iopscience.iop.org/article/10.1088/1748-9326/ac109c) and thus increased temperature. I suspect that the reduction in heat island effect possibly balanced out this increased solar irradiance. This relationship between temperature and aerosols could be further researched using a panel data of multiple geographies.

It was also suggested that due to increase in solar irradiance, low pressure developed on Indian mainland that eventually led to the strengthening of Indian monsoons. Delhi doesn’t fall in the main monsoon geography of India and I suspect that I haven’t seen any significant relationship with precipitation for this reason. This hypothesis can be further tested in another geography that is more dependent on South-West monsoons.

Causal explanations are made only during the first lockdown because the data until 2019 could be used for building a counter factual during the first lockdown period. There were model inaccuracies to forecast for the period of second lockdown and thus a counter-factual group couldn’t be built. In further research, a stronger forecasting model would help in giving a casual explanation about second lockdown as well.

Finally, this research work assumed linear relationship between variables. Given the complexity of environmental systems, non-linearity can exist between the variables of our interest. In further research, non-linear dynamics between variables should also be considered.

## Conclusion

In this research, I study the impact of COVID-19 lockdowns on environmental variables. I give causal explanation for the impact of first lockdown on pollution variables (NO2, aerosol levels). 27% NO2 pollution and 50% Aerosol levels reduced due to the first lockdown. For other variables, I study their correlation with the mobility and economic activity, proxied by night lights level. I observed that temperature reduces by 1%, vegetation and water quality improves by 1% when there is a 10% reduction in mobility. This evidence can guide the city government’s policies on urban mobility, pollution and heat wave management.

All references are hyperlinked.

---

If the pollution cannot be seen, it can be heard. Look out for the silence near 30th second.

[Y- Axis: NO2 levels in mol/m^2](Delhi%20breathes%20during%20COVID-19%203f901418ae164568b88540490f90f98e/No2_Sonification.mp4)

Y- Axis: NO2 levels in mol/m^2
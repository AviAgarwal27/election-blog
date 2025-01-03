---
title: 'Post #7: State Level Predictions'
author: Avi Agarwal
date: '2024-10-21'
slug: super-ensembling-simulations
categories: []
tags: []
---






















































































































# Introduction

# National Two Party Vote Share

Given the limited role of the national popular vote in determining the outcome of U.S. elections, I have decided to retain the model I presented in Week 5, despite its acknowledged flaws, which I addressed in last week’s post. I am unlikely to update this prediction further and will instead focus on my state-level model.

<table style="border-collapse:collapse; border:none;">
<caption style="font-weight: bold; text-align:left;">2024 Democrat Two Party Vote Share via Linear Regression</caption>
<tr>
<th style="border-top: double; text-align:center; font-style:italic; font-weight:normal; padding:0.2cm; border-bottom:1px solid black; text-align:left; ">Prediction</th>
<th style="border-top: double; text-align:center; font-style:italic; font-weight:normal; padding:0.2cm; border-bottom:1px solid black; ">Lower.Bound</th>
<th style="border-top: double; text-align:center; font-style:italic; font-weight:normal; padding:0.2cm; border-bottom:1px solid black; ">Upper.Bound</th>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; border-bottom: double; ">53.31%</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; border-bottom: double; ">46.57%</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; border-bottom: double; ">60.05%</td>
</tr>
</table>



# Linear Model

This week, I made significant quality improvements to my linear model, which has evolved since Week 5. First, I updated the polling data to reflect the most recent results. Instead of using an average polling score across all weeks, I replaced it with an average from the most recent polling week.

The first major improvement was the addition of lagged vote shares from the two previous election cycles as a covariate in my model. Historical data tends to be a strong predictor of future outcomes, and I observed a reduction in in-sample MSE after incorporating this variable. The second key update involved changing the national-level economic variable. Over the past two weeks, I used Quarter 2 growth in real disposable income, even though my earlier analysis (in Week 2) indicated that Quarter 2 unemployment was a better indicator. After testing which model resulted in a lower in-sample MSE, I reverted to using unemployment growth.

Previously, my model only used data from elections up to 2016, excluding 2020 due to the economic outliers caused by the pandemic. However, I trained the model in this iteration using data only up to 2012 so I could use the 2016 election to evaluate out-of-sample MSE. I will explain the necessity of out-of-sample MSE later.  The exclusion of a solid Republican electoral college victory from the training set may have biased this model toward the Democrats compared to last week’s version.

The most significant change, however, lies in the methodology for predicting the two-party vote share of a state. Previously, I relied solely on data filtered to the Democratic party, which resulted in unconstrained predictions. If I built the same model for Republicans, the combined predicted vote shares could exceed 100%. Moreover, in extreme cases, a state could hypothetically surpass 100% vote share for one party, though this was unlikely in swing states. To address this, I duplicated the model for Republicans, predicted their vote shares, and then rescaled the predicted Democratic and Republican shares to sum to 100%, providing a more accurate margin.




```
## [1] "In-sample MSE for Optimized LM Model: 1.77876259651781"
```

```
## [1] "Out-sample MSE for Optimized LM Model: 3.66463924611509"
```


The immediate improvement is clear: the in-sample MSE dropped from 5.55 last week to less than 1.8 this week. The model performed well when predicting the 2016 election with an out-of-sample MSE of 3.67. These reductions in MSE suggest that this model is more robust than last week’s, though the exclusion of 2016 could also contribute to the improvements.
<table style="border-collapse:collapse; border:none;">
<caption style="font-weight: bold; text-align:left;">Summary of Democrat Vote Share Model</caption>
<tr>
<td style=" text-align:center; border-bottom:1px solid; font-style:italic; font-weight:normal;nodv  text-align:left; ">Predictors</td>
<td style=" text-align:center; border-bottom:1px solid; font-style:italic; font-weight:normal;nodv  ">Estimates</td>
<td style=" text-align:center; border-bottom:1px solid; font-style:italic; font-weight:normal;nodv  ">std. Error</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">polling trend 7 3</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">0.25</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">0.10</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">polling trend 12 8</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">&#45;0.10</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">0.14</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">D pv2p lag1</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">0.46</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">0.12</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">D pv2p lag2</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">&#45;0.20</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">0.07</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">current week</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">0.24</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">0.08</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">incumbent party</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">&#45;1.08</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">1.07</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">dpi inflation adjusted</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">&#45;0.23</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">0.26</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">unemployment growth<br>quarterly</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">0.37</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">0.11</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">stateArizona</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">25.29</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">3.98</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">stateGeorgia</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">25.04</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">3.97</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">stateMichigan</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">28.68</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">4.66</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">stateNevada</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">27.04</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">4.37</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">stateNorth Carolina</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">24.75</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">4.16</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">stateWisconsin</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">28.87</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">4.73</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">statePennsylvania</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">28.40</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">4.65</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; padding-top:0.1cm; padding-bottom:0.1cm; border-top:1px solid;">Observations</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; padding-top:0.1cm; padding-bottom:0.1cm; text-align:left; border-top:1px solid;" colspan="2">46</td>
</tr>

</table>


<table style="border-collapse:collapse; border:none;">
<caption style="font-weight: bold; text-align:left;">LM Predictions</caption>
<tr>
<th style="border-top: double; text-align:center; font-style:italic; font-weight:normal; padding:0.2cm; border-bottom:1px solid black; text-align:left; ">State</th>
<th style="border-top: double; text-align:center; font-style:italic; font-weight:normal; padding:0.2cm; border-bottom:1px solid black; ">Dem.Vote</th>
<th style="border-top: double; text-align:center; font-style:italic; font-weight:normal; padding:0.2cm; border-bottom:1px solid black; ">Rep.Vote</th>
<th style="border-top: double; text-align:center; font-style:italic; font-weight:normal; padding:0.2cm; border-bottom:1px solid black; ">Dem.Margin</th>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">Arizona</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">49.71%</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">50.29%</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">-0.59%</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">Georgia</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">50.26%</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">49.74%</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">0.52%</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">Michigan</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">53.73%</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">46.27%</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">7.47%</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">Nevada</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">52.19%</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">47.81%</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">4.37%</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">North Carolina</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">49.44%</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">50.56%</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">-1.13%</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">Pennsylvania</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">53.06%</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">46.94%</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">6.11%</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; border-bottom: double; ">Wisconsin</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; border-bottom: double; ">53%</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; border-bottom: double; ">47%</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; border-bottom: double; ">6.01%</td>
</tr>
</table>

For the 2024 predictions, this model flips Georgia from Trump to Harris by a margin of 0.5 points, whereas last week’s model predicted a narrow Trump win. Interestingly, for the other swing states where the expected winner remained the same—Nevada, Wisconsin, Michigan, and Pennsylvania for Harris, and Arizona and North Carolina for Trump—the margin of victory increased for both parties compared to last week. I am uncertain which specific model adjustment caused this, though I believe the addition of lagged vote share as a covariate played a role.


# Ensemble Model

While I believe my linear model is strong, I thought I could enhance its accuracy and reduce overfitting by creating an ensemble model that combines multiple models. As a result, I developed an ensemble model using three distinct models. The first model focuses solely on fundamentals, excluding polling altogether. It is similar to the linear model but without polling-based covariates, using Q2 real disposable income growth as the sole economic indicator. The second model relies entirely on polling, using the two trend variables and the average polling from the most recent week (currently week 3). The third model is identical to the second one.

Using the 2016 election results, I applied constrained optimization to determine the weights for each model. I observed that for Democrats, the third model tended to yield disproportionately higher predictions, leading to it being weighted more heavily. Similarly, the first model had a higher weight for Republicans.

After developing the ensemble model, I calculated the in-sample MSE using the training data and the out-of-sample MSE using the 2016 data. As expected from a supervised learning model, the in-sample MSE was higher than that of the linear model, while the out-of-sample MSE was lower.



```
## [1] "In-sample MSE for Ensemble Model (Democrat): 6.71465280630496"
```

```
## [1] "In-sample MSE for Ensemble Model (Republican): 4.89529595168979"
```


```
## [1] "Out-sample MSE for Ensemble Model (Democrat): 2.1882978374969"
```

```
## [1] "Out-sample MSE for Ensemble Model (Republican: 3.22497868787428"
```

<table style="border-collapse:collapse; border:none;">
<caption style="font-weight: bold; text-align:left;">Ensemble Predictions</caption>
<tr>
<th style="border-top: double; text-align:center; font-style:italic; font-weight:normal; padding:0.2cm; border-bottom:1px solid black; text-align:left; ">State</th>
<th style="border-top: double; text-align:center; font-style:italic; font-weight:normal; padding:0.2cm; border-bottom:1px solid black; ">Dem.Vote</th>
<th style="border-top: double; text-align:center; font-style:italic; font-weight:normal; padding:0.2cm; border-bottom:1px solid black; ">Rep..Vote</th>
<th style="border-top: double; text-align:center; font-style:italic; font-weight:normal; padding:0.2cm; border-bottom:1px solid black; ">Dem.Margin</th>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">Arizona</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">46.54%</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">53.46%</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">-6.91%</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">Georgia</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">47.15%</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">52.85%</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">-5.7%</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">Michigan</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">50.32%</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">49.68%</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">0.64%</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">Nevada</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">49.89%</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">50.11%</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">-0.22%</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">North Carolina</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">46.06%</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">53.94%</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">-7.88%</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">Pennsylvania</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">50.7%</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">49.3%</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">1.41%</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; border-bottom: double; ">Wisconsin</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; border-bottom: double; ">50.65%</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; border-bottom: double; ">49.35%</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; border-bottom: double; ">1.3%</td>
</tr>
</table>

For the 2024 predictions in swing states, the model assigns Pennsylvania, Wisconsin, and Michigan to Harris, while Trump is projected to win Arizona, Nevada, Georgia, and North Carolina. This would result in Vice President Harris winning the electoral college with 270 votes to Trump’s 268.

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-59-1.png" width="672" />


Overall, I’m pleased with the improvements the ensemble model brings to my predictions, and I plan to continue using it in the future. Additionally, I hope to integrate a regularization method for polling and further improve the model with simulations to estimate likelihood of either candidate winning or losing. Thanks!

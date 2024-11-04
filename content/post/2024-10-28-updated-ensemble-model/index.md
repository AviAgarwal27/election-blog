---
title: Updated Ensemble Model
author: Avi Agarwal
date: '2024-10-28'
slug: updated-ensemble-model
categories: []
tags: []
---






















































```
## [1] "Arizona"
## [1] 47.49625
## [1] 50.15683
## [1] 2.660585
## [1] "Georgia"
## [1] 47.42172
## [1] 50.11933
## [1] 2.697607
## [1] "Michigan"
## [1] 52.6748
## [1] 51.41356
## [1] 1.261239
## [1] "Nevada"
## [1] 54.51226
## [1] 51.22312
## [1] 3.289144
## [1] "North Carolina"
## [1] 48.77503
## [1] 49.31582
## [1] 0.5407834
## [1] "Pennsylvania"
## [1] 53.37993
## [1] 50.58921
## [1] 2.790725
## [1] "Wisconsin"
## [1] 53.16148
## [1] 50.31906
## [1] 2.842421
```




































# Introoduction
This week, most of the work focused on updating last week’s ensemble model to create weights for individual states. The adjustments were more challenging than expected, taking additional time and limiting other updates.

# National Two-Party Vote Share

This model remains the same as in previous weeks, predicting that VP Harris will win by 3.31 percentage points.
Linear State Model


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

The primary adjustment here was adding updated polling data and removing the lagged vote share from two elections ago. I felt this change was necessary since many of the states in question (Georgia, Arizona, North Carolina) were not considered swing states in 2016, and significant demographic shifts have since altered the electorate, making the 2016 vote share an unreliable predictor for 2024. Beyond these changes, the model maintains last week’s approach, regressing over polling, fundamentals, and economic factors.

The model still predicts a win for Harris in Michigan, Nevada, Wisconsin, and Pennsylvania, though with narrower margins than last week, likely due to a tighter polling spread. This week, however, the model flips Georgia back to Trump by a razor-thin margin of 0.14 percentage points, and overall, there’s a slight shift in predicted vote shares toward Trump across all states.
Ensemble Model



<table style="width: 50%;">
<caption style="font-weight: bold; text-align: center;">LM Model Predicted Vote Share</caption>
<tr>
<th style="border-top: double; text-align:center; font-style:italic; font-weight:normal; padding:0.2cm; border-bottom:1px solid black; text-align:left; ">state</th>
<th style="border-top: double; text-align:center; font-style:italic; font-weight:normal; padding:0.2cm; border-bottom:1px solid black; ">adj_dem_vote</th>
<th style="border-top: double; text-align:center; font-style:italic; font-weight:normal; padding:0.2cm; border-bottom:1px solid black; ">adj_rep_vote</th>
<th style="border-top: double; text-align:center; font-style:italic; font-weight:normal; padding:0.2cm; border-bottom:1px solid black; ">margin</th>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">Arizona</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">49.29</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">50.71</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">-1.42</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">Georgia</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">50.24</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">49.76</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">0.48</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">Michigan</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">51.87</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">48.13</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">3.75</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">Nevada</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">51.85</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">48.15</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">3.70</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">North Carolina</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">49.25</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">50.75</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">-1.50</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">Pennsylvania</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">52.05</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">47.95</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">4.09</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; border-bottom: double; ">Wisconsin</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; border-bottom: double; ">52.07</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; border-bottom: double; ">47.93</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; border-bottom: double; ">4.13</td>
</tr>
</table>
# Ensemble Model

Last week’s model had a significant flaw: it used the same weights across all states instead of creating state-specific weights. I addressed this by creating a function to apply individualized weights for each state. Additionally, I realized that excluding an intercept since week four might have reduced prediction accuracy. To resolve this, I’ve reintroduced an intercept using Florida as the baseline.

The model was trained on elections up to 2016, with weights fitted to 2016 data. This week, I also added 2019 projections of economic factors to 2020 data to enhance prediction accuracy, though I kept 2020 data isolated to calculate a true out-of-sample MSE for testing accuracy.

These adjustments substantially improved the in-sample MSE, with most states now below 1. However, I suspect this improvement is due to overfitting to 2016 data rather than genuine model strength, given the high out-of-sample MSE. While states like Georgia and North Carolina appear accurate, this may be due to random chance rather than predictive accuracy.






The main issue with this model is likely due to restrictive weight constraints. Currently, the model applies a Beta between 0 and 1, preventing negative weights. This constraint may be overly limiting, as two of the regression models are often minimized to nearly zero, relying mainly on a single model. Optimizing these constraints and weights should improve predictive accuracy.

At present, the ensemble model predicts a win for Harris only in Nevada. Nearly all states have shifted towards Trump, with margins between 1.5 and 2.5 points, except North Carolina, which shows a more substantial lead for Trump at -7.06 points.


<table style="width: 50%;">
<caption style="font-weight: bold; text-align: center;">Ensemble Model Predicted Vote Share</caption>
<tr>
<th style="border-top: double; text-align:center; font-style:italic; font-weight:normal; padding:0.2cm; border-bottom:1px solid black; text-align:left; ">state</th>
<th style="border-top: double; text-align:center; font-style:italic; font-weight:normal; padding:0.2cm; border-bottom:1px solid black; ">adj_dem_vote</th>
<th style="border-top: double; text-align:center; font-style:italic; font-weight:normal; padding:0.2cm; border-bottom:1px solid black; ">adj_rep_vote</th>
<th style="border-top: double; text-align:center; font-style:italic; font-weight:normal; padding:0.2cm; border-bottom:1px solid black; ">margin</th>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">Arizona</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">47.06</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">52.94</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">-5.88</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">Georgia</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">45.64</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">54.36</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">-8.71</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">Michigan</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">51.43</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">48.57</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">2.85</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">Nevada</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">49.92</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">50.08</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">-0.16</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">North Carolina</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">46.99</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">53.01</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">-6.01</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">Pennsylvania</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">49.22</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">50.78</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">-1.55</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; border-bottom: double; ">Wisconsin</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; border-bottom: double; ">51.02</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; border-bottom: double; ">48.98</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; border-bottom: double; ">2.04</td>
</tr>
</table>

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-40-1.png" width="672" />


---
title: Updated Ensemble Model
author: Avi Agarwal
date: '2024-10-28'
slug: updated-ensemble-model
categories: []
tags: []
---














































































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
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">48.78</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">51.22</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">-2.43</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">Georgia</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">49.93</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">50.07</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">-0.14</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">Michigan</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">51.66</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">48.34</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">3.32</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">Nevada</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">51.69</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">48.31</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">3.38</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">North Carolina</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">49.03</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">50.97</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">-1.95</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">Pennsylvania</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">51.67</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">48.33</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">3.33</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; border-bottom: double; ">Wisconsin</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; border-bottom: double; ">51.76</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; border-bottom: double; ">48.24</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; border-bottom: double; ">3.51</td>
</tr>
</table>
# Ensemble Model

Last week’s model had a significant flaw: it used the same weights across all states instead of creating state-specific weights. I addressed this by creating a function to apply individualized weights for each state. Additionally, I realized that excluding an intercept since week four might have reduced prediction accuracy. To resolve this, I’ve reintroduced an intercept using Florida as the baseline.

The model was trained on elections up to 2016, with weights fitted to 2016 data. This week, I also added 2019 projections of economic factors to 2020 data to enhance prediction accuracy, though I kept 2020 data isolated to calculate a true out-of-sample MSE for testing accuracy.

These adjustments substantially improved the in-sample MSE, with most states now below 1. However, I suspect this improvement is due to overfitting to 2016 data rather than genuine model strength, given the high out-of-sample MSE. While states like Georgia and North Carolina appear accurate, this may be due to random chance rather than predictive accuracy.


<table style="width: 60%;">
<caption style="font-weight: bold; text-align: center;">In-Sample MSE for Democratic Predictions by Swing State (2016 Data)</caption>
<tr>
<th style="border-top: double; text-align:center; font-style:italic; font-weight:normal; padding:0.2cm; border-bottom:1px solid black; text-align:left; ">state</th>
<th style="border-top: double; text-align:center; font-style:italic; font-weight:normal; padding:0.2cm; border-bottom:1px solid black; ">mse_dem</th>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">Arizona</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">1.6159</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">Georgia</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">0.0000</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">Michigan</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">0.1371</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">Nevada</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">0.0000</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">North Carolina</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">0.0000</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">Pennsylvania</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">0.5241</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; border-bottom: double; ">Wisconsin</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; border-bottom: double; ">0.6886</td>
</tr>
</table>

<table style="width: 60%;">
<caption style="font-weight: bold; text-align: center;">Out-of-Sample MSE for Democratic Predictions by Swing State (2020 Data)</caption>
<tr>
<th style="border-top: double; text-align:center; font-style:italic; font-weight:normal; padding:0.2cm; border-bottom:1px solid black; text-align:left; ">state</th>
<th style="border-top: double; text-align:center; font-style:italic; font-weight:normal; padding:0.2cm; border-bottom:1px solid black; ">mse_dem</th>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">Arizona</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">2.6367</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">Georgia</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">0.3509</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">Michigan</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">9.5468</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">Nevada</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">14.6477</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">North Carolina</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">0.0149</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">Pennsylvania</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">35.6564</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; border-bottom: double; ">Wisconsin</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; border-bottom: double; ">12.7381</td>
</tr>
</table>

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
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">49.21</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">50.79</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">-1.58</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">Georgia</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">49.41</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">50.59</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">-1.17</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">Michigan</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">48.96</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">51.04</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">-2.08</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">Nevada</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">51.22</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">48.78</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">2.43</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">North Carolina</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">46.47</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">53.53</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">-7.06</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">Pennsylvania</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">49.35</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">50.65</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">-1.30</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; border-bottom: double; ">Wisconsin</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; border-bottom: double; ">48.90</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; border-bottom: double; ">51.10</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; border-bottom: double; ">-2.21</td>
</tr>
</table>

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-40-1.png" width="672" />


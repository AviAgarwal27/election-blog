---
title: 'Post #5: State Level Predictions'
author: Avi Agarwal
date: '2024-10-07'
slug: post-5-state-level-predictions
categories: []
tags: []
---





















```r
in_sample_rf_predictions <- predict(rf_fit, data = train_data)$predictions

in_sample_mse <- mean((rf_model_data_r$pv2p - in_sample_rf_predictions)^2)

in_sample_fit_df <- data.frame(
  year = rf_model_data_r$year,
  Actual = sprintf("%.2f%%", rf_model_data_r$pv2p),
  Predicted = sprintf("%.2f%%", in_sample_rf_predictions)
)

nat_rf_in_sample_error <- tab_df(in_sample_fit_df, 
       title = paste("In-sample Fit of Democrat National Two Party Vote Share via Random Forest\n(In-sample MSE:", sprintf("%.4f", in_sample_mse), ")"),
       show.rownames = FALSE)


rf_nat_pred <- tab_df(pred_model_rf_df, 
       title = "2024 Democrat NationalTwo Party Vote Share via Random Forest Model",
       show.rownames = FALSE)
```

















# Introduction

This week’s post builds on last week’s and introduces the structure followed in each post leading up to the election. I will develop two models to predict the national two-party popular vote and forecast the Electoral College outcome. These models will be updated with new data, such as recent polls, and enhanced with additional variables and prediction methods to fine-tune our projections.

# National Two-Party Vote Predictions

I decided to shift away from using a weighted polling average and instead focus on a simple average of polls from weeks 5 to 8. The main reason for this change is that the weighted polling average, constructed by regressing historical data on each week, resulted in an artificially high R-squared of around 0.95 when recent poll data was added. This high correlation occurred because the weighted polling average was based on the same outcome factor being regressed again, leading to a model that seemed highly accurate but was likely overfitting to past data. Such overfitting makes it a poor predictor of future election outcomes. By switching to an average of polls from weeks 5 to 8, I aim to use a more straightforward and unbiased metric, which should offer better predictive power without inflating the model’s performance through recursive correlation. I will later explain why I chose this specific period.

As a result, this week's linear regression model, which is otherwise identical to last week’s, has a lower adjusted R-squared. However, I believe this model is a better predictor for future outcomes. The share it predicts for Harris has increased to 53% which is more compared to last week, likely due to recent polling trends in her favor over Trump. I am unsure why Q2 RDPI growth is no longer statistically significant in this model. My main theory is that polls closer to the election are more strongly correlated with the actual two-party vote share, which may reduce the overall impact of Q2 RDPI growth in the model.

<table style="border-collapse:collapse; border:none;">
<caption style="font-weight: bold; text-align:left;">Linear Regression Model for Democrat Two Party Vote Share
(In-sample MSE: 4.9637 )</caption>
<tr>
<th style="border-top: double; text-align:center; font-style:normal; font-weight:bold; padding:0.2cm;  text-align:left; ">&nbsp;</th>
<th colspan="4" style="border-top: double; text-align:center; font-style:normal; font-weight:bold; padding:0.2cm; ">Democrat National Two Party Vote Share</th>
</tr>
<tr>
<td style=" text-align:center; border-bottom:1px solid; font-style:italic; font-weight:normal;  text-align:left; ">Predictors</td>
<td style=" text-align:center; border-bottom:1px solid; font-style:italic; font-weight:normal;  ">Estimates</td>
<td style=" text-align:center; border-bottom:1px solid; font-style:italic; font-weight:normal;  ">std. Error</td>
<td style=" text-align:center; border-bottom:1px solid; font-style:italic; font-weight:normal;  ">CI</td>
<td style=" text-align:center; border-bottom:1px solid; font-style:italic; font-weight:normal;  ">p</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">(Intercept)</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">20.36</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">5.09</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">8.85&nbsp;&ndash;&nbsp;31.87</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  "><strong>0.003</strong></td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">weighted_avg_poll</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">0.60</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">0.11</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">0.34&nbsp;&ndash;&nbsp;0.86</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  "><strong>&lt;0.001</strong></td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">RDPI_growth_quarterly</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">0.35</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">0.27</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">&#45;0.27&nbsp;&ndash;&nbsp;0.97</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">0.237</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">incumbent_party</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">3.56</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">1.66</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">&#45;0.19&nbsp;&ndash;&nbsp;7.30</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">0.060</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; padding-top:0.1cm; padding-bottom:0.1cm; border-top:1px solid;">Observations</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; padding-top:0.1cm; padding-bottom:0.1cm; text-align:left; border-top:1px solid;" colspan="4">13</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; padding-top:0.1cm; padding-bottom:0.1cm;">R<sup>2</sup> / R<sup>2</sup> adjusted</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; padding-top:0.1cm; padding-bottom:0.1cm; text-align:left;" colspan="4">0.788 / 0.718</td>
</tr>

</table>

<table style="border-collapse:collapse; border:none;">
<caption style="font-weight: bold; text-align:left;">2024 Democrat Two Party Vote Share via Linear Regression</caption>
<tr>
<th style="border-top: double; text-align:center; font-style:italic; font-weight:normal; padding:0.2cm; border-bottom:1px solid black; text-align:left; ">Prediction</th>
<th style="border-top: double; text-align:center; font-style:italic; font-weight:normal; padding:0.2cm; border-bottom:1px solid black; ">Lower.Bound</th>
<th style="border-top: double; text-align:center; font-style:italic; font-weight:normal; padding:0.2cm; border-bottom:1px solid black; ">Upper.Bound</th>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; border-bottom: double; ">53.30%</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; border-bottom: double; ">46.56%</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; border-bottom: double; ">60.04%</td>
</tr>
</table>

For comparison, I also created a random forest model using the same covariates and time period but through a different methodology. The in-sample fit of the random forest model produced an MSE of around 7%, which is higher than the linear regression’s MSE of around 5%.

The random forest model also predicts a popular vote victory for Harris, but by a much smaller margin. In fact, her predicted lead of 1.63% in the popular vote suggests that losing the Electoral College could be a real possibility. To fully assess the outcome of this election, we must look more closely at individual states.


<table style="border-collapse:collapse; border:none;">
<caption style="font-weight: bold; text-align:left;">In-sample Fit of Democrat National Two Party Vote Share via Random Forest
(In-sample MSE: 7.0798 )</caption>
<tr>
<th style="border-top: double; text-align:center; font-style:italic; font-weight:normal; padding:0.2cm; border-bottom:1px solid black; text-align:left; ">year</th>
<th style="border-top: double; text-align:center; font-style:italic; font-weight:normal; padding:0.2cm; border-bottom:1px solid black; ">Actual</th>
<th style="border-top: double; text-align:center; font-style:italic; font-weight:normal; padding:0.2cm; border-bottom:1px solid black; ">Predicted</th>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">1968</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">49.60%</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">47.63%</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">1972</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">38.21%</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">43.61%</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">1976</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">51.14%</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">50.76%</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">1980</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">44.84%</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">47.47%</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">1984</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">40.88%</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">44.91%</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">1988</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">46.17%</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">47.26%</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">1992</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">53.62%</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">50.76%</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">1996</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">54.80%</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">51.98%</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">2000</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">50.26%</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">49.90%</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">2004</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">48.73%</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">47.52%</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">2008</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">53.77%</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">49.79%</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">2012</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">51.92%</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">51.63%</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; border-bottom: double; ">2016</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; border-bottom: double; ">51.16%</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; border-bottom: double; ">50.19%</td>
</tr>
</table>

<table style="border-collapse:collapse; border:none;">
<caption style="font-weight: bold; text-align:left;">2024 Democrat NationalTwo Party Vote Share via Random Forest Model</caption>
<tr>
<th style="border-top: double; text-align:center; font-style:italic; font-weight:normal; padding:0.2cm; border-bottom:1px solid black; text-align:left; ">year</th>
<th style="border-top: double; text-align:center; font-style:italic; font-weight:normal; padding:0.2cm; border-bottom:1px solid black; ">Prediction</th>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; border-bottom: double; ">2024</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; border-bottom: double; ">51.63%</td>
</tr>
</table>

# State Level Predictions

I would like to begin by discussing the states I will be covering in my predictions. As we discovered in week 1, there are only seven states that could realistically be won by either party in this election based on historical trends. This is further supported by the fact that these seven states are currently listed as toss-ups by both the Cook Political Report and Sabato’s Crystal Ball. As a result, it is impractical to predict the outcome in any other state, where the winner is almost certain. This means we are starting with Harris holding 226 electoral votes and Trump with 219 votes. The remaining 95 electoral votes are in play across Arizona, Georgia, Nevada, Pennsylvania, Wisconsin, and Michigan.

To predict the outcomes in these swing states, I built a linear regression model using polling averages, Q2 RDPI growth, the incumbent party, and state-level differentiation. The decision to focus on polling averages from weeks 8 to 5 in the national model comes from the fact that this was the smallest, most recent time frame in which every state had available polls for all elections measured from 1968 to 2016. Another choice I made was to use national RDPI growth instead of state-level data. While state-specific economic indicators could offer additional granularity, many voters tend to view the economy in national terms. Even if their state is doing well, hearing about broader economic struggles in the media may influence their perception of the national economy negatively. For this reason, I decided to stick with national Q2 RDPI growth in the model.


<table style="border-collapse:collapse; border:none;">
<caption style="font-weight: bold; text-align:left;">Linear Regresion Model for Swing States</caption>
<tr>
<th style="border-top: double; text-align:center; font-style:normal; font-weight:bold; padding:0.2cm;  text-align:left; ">&nbsp;</th>
<th colspan="4" style="border-top: double; text-align:center; font-style:normal; font-weight:bold; padding:0.2cm; ">Democrat Two Party Vote Share</th>
</tr>
<tr>
<td style=" text-align:center; border-bottom:1px solid; font-style:italic; font-weight:normal;  text-align:left; ">Predictors</td>
<td style=" text-align:center; border-bottom:1px solid; font-style:italic; font-weight:normal;  ">Estimates</td>
<td style=" text-align:center; border-bottom:1px solid; font-style:italic; font-weight:normal;  ">std. Error</td>
<td style=" text-align:center; border-bottom:1px solid; font-style:italic; font-weight:normal;  ">CI</td>
<td style=" text-align:center; border-bottom:1px solid; font-style:italic; font-weight:normal;  ">p</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">(Intercept)</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">27.19</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">3.61</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">19.94&nbsp;&ndash;&nbsp;34.43</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  "><strong>&lt;0.001</strong></td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">avg_poll_8_5</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">0.43</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">0.10</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">0.23&nbsp;&ndash;&nbsp;0.62</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  "><strong>&lt;0.001</strong></td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">stateGeorgia</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">&#45;0.79</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">2.05</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">&#45;4.89&nbsp;&ndash;&nbsp;3.31</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">0.700</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">stateMichigan</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">4.13</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">1.94</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">0.24&nbsp;&ndash;&nbsp;8.03</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  "><strong>0.038</strong></td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">stateNevada</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">0.18</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">2.06</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">&#45;3.95&nbsp;&ndash;&nbsp;4.32</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">0.929</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">stateNorth Carolina</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">&#45;2.23</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">1.92</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">&#45;6.08&nbsp;&ndash;&nbsp;1.61</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">0.250</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">statePennsylvania</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">3.94</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">2.05</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">&#45;0.17&nbsp;&ndash;&nbsp;8.05</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">0.060</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">stateWisconsin</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">3.37</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">2.00</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">&#45;0.64&nbsp;&ndash;&nbsp;7.39</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">0.098</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">RDPI_growth_quarterly</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">0.32</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">0.24</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">&#45;0.15&nbsp;&ndash;&nbsp;0.80</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">0.175</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">incumbent_party</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">2.30</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">1.36</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">&#45;0.42&nbsp;&ndash;&nbsp;5.02</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">0.096</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; padding-top:0.1cm; padding-bottom:0.1cm; border-top:1px solid;">Observations</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; padding-top:0.1cm; padding-bottom:0.1cm; text-align:left; border-top:1px solid;" colspan="4">65</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; padding-top:0.1cm; padding-bottom:0.1cm;">R<sup>2</sup> / R<sup>2</sup> adjusted</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; padding-top:0.1cm; padding-bottom:0.1cm; text-align:left;" colspan="4">0.561 / 0.489</td>
</tr>

</table>


This model saw Harris winning Michigan, Nevada, Wisconsin, and Pennsylvania which would push her over 270 and result in her wining the presidency. The adjusted R-squared was less that 0.5 suggesting this model does not account for much of the variance in state electionS.

<table style="border-collapse:collapse; border:none;">
<caption style="font-weight: bold; text-align:left;">2024 Democrat Two Party Vote Share via Linear Model in Swing States</caption>
<tr>
<th style="border-top: double; text-align:center; font-style:italic; font-weight:normal; padding:0.2cm; border-bottom:1px solid black; text-align:left; ">state</th>
<th style="border-top: double; text-align:center; font-style:italic; font-weight:normal; padding:0.2cm; border-bottom:1px solid black; ">year</th>
<th style="border-top: double; text-align:center; font-style:italic; font-weight:normal; padding:0.2cm; border-bottom:1px solid black; ">Prediction</th>
<th style="border-top: double; text-align:center; font-style:italic; font-weight:normal; padding:0.2cm; border-bottom:1px solid black; ">Lower.Bound</th>
<th style="border-top: double; text-align:center; font-style:italic; font-weight:normal; padding:0.2cm; border-bottom:1px solid black; ">Upper.Bound</th>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">Arizona</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">2024</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">49.82%</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">40.89%</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">58.75%</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">Georgia</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">2024</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">49.18%</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">40.26%</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">58.09%</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">Michigan</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">2024</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">54.49%</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">45.77%</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">63.21%</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">Nevada</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">2024</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">50.20%</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">41.37%</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">59.04%</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">North Carolina</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">2024</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">47.80%</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">39.07%</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">56.54%</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">Pennsylvania</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">2024</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">54.21%</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">45.47%</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">62.95%</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; border-bottom: double; ">Wisconsin</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; border-bottom: double; ">2024</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; border-bottom: double; ">53.96%</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; border-bottom: double; ">45.23%</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; border-bottom: double; ">62.69%</td>
</tr>
</table>

Similar to national two party vote, I also created a random forest model that predicted the state level outcomes. This model resulted the same state level prediction except for Arizona which flipped back to Harris by a extremely thin margin. 


<table style="border-collapse:collapse; border:none;">
<caption style="font-weight: bold; text-align:left;">2024 Democrat Two Party Vote Share via Random Forest Model in Swing States</caption>
<tr>
<th style="border-top: double; text-align:center; font-style:italic; font-weight:normal; padding:0.2cm; border-bottom:1px solid black; text-align:left; ">state</th>
<th style="border-top: double; text-align:center; font-style:italic; font-weight:normal; padding:0.2cm; border-bottom:1px solid black; ">year</th>
<th style="border-top: double; text-align:center; font-style:italic; font-weight:normal; padding:0.2cm; border-bottom:1px solid black; ">Prediction</th>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">Arizona</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">2024</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">50.001%</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">Georgia</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">2024</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">49.822%</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">Michigan</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">2024</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">52.429%</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">Nevada</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">2024</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">51.497%</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">North Carolina</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">2024</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">49.798%</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">Pennsylvania</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">2024</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">52.190%</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; border-bottom: double; ">Wisconsin</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; border-bottom: double; ">2024</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; border-bottom: double; ">52.410%</td>
</tr>
</table>

# Conclusion

Overall, all of my models predict a Harris victory in the Electoral College and national two party popular vote though by slim margins. I look forward to refining these models further as we get close to election day.

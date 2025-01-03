---
title: 'Post #2: Modeling Using the Economy'
author: Avi Agarwal
date: '2024-09-16'
slug: post-2-modeling-using-the-economy
categories: []
tags: []
---










# Introduction

The economy is often cited as a core 'fundamental' in predicting election outcomes. A strong economy typically suggests that the incumbent party is likely to win and vice versa. In some elections, like in 1980, where rampant inflation—significantly rising gas prices—dominated, it was clear that incumbent Jimmy Carter would lose due to the weak economy. However, in other elections, such as 2012 or 2016, it was less clear whether the economy was strong enough to predict an incumbent party victory.

Voters' interactions with the economy can influence their votes in various ways. Some may be 'pocketbook voters,' supporting incumbents when they are personally better off. Others may focus on macroeconomic issues, such as GDP growth or unemployment rates, that may not directly affect them but could still influence their vote through sociotropic considerations.

It is also unclear which economic timeframe is most important in shaping voters' decisions. Does the economy’s performance right before the election matter most? Or does the entire term or just the year leading up to the election have a greater impact on vote share?

To explore some of these questions, I created six models that examine economic factors relative to incumbent two-party vote share. The first two models measure the percent change in real disposable personal income (RDPI), one of the most common metrics for predicting elections. The first model looks at the increase from the end of Quarter 1 to the end of Quarter 2 in an election year. Typically, data from Quarter 2 to Quarter 3 would be preferred. Still, because I aim to use this data to predict the 2024 election outcome, I am using Quarter 2 as the latest available data to match current 2024 figures. The second RDPI model looks at percent growth over the course of a year, from the end of Q2 one year before the election to the end of Q2 in the election year. For example, the first point in the dataset measures growth from Q2 1959 to Q2 1960.

In addition to RDPI, I developed two models each for quarterly and annual percent growth in unemployment and the S&P 500. These factors offer a scale of how much voters care about personal wealth versus macroeconomic health. RDPI is theoretically the most personally relevant, the S&P 500 falls somewhere in between, and unemployment most represents sociotropic concerns.

Before diving into the models, I want to clarify that I used the same years for each dataset, starting from 1960—the first election with complete data. I also excluded 2020 from all models due to the massive Q2 economic decline caused by the COVID-19 pandemic, which is an anomaly that wouldn’t be expected in a non-pandemic election year. While these limitations certainly affect the results, I believe they provide the most representative picture of an average presidential election.


# Real Disposable Personal Income Growth

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-6-1.png" width="672" />

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-7-1.png" width="672" />


Both the annual and quarterly RDPI growth models show a similar trend, with a slightly positive slope, indicating a direct relationship between RDPI growth and election outcomes. A cursory glance suggests that the annual model has a larger coefficient, which is confirmed by the data below (1.49 vs. 0.7). Interestingly, the annual model also has a significantly lower p-value and a higher R-squared value (0.374 vs. 0.22 for the quarterly model). These figures suggest that the annual model is a better predictor than the quarterly model, as it explains more of the variance in the election outcome. However, with an R-squared of 0.374, it is clear that neither model accounts for enough of the election dynamics to serve as a strong standalone predictor.


<table style="border-collapse:collapse; border:none;">
<caption style="font-weight: bold; text-align:left;">Regression Table for Quarterly RDPI Growth (1960-2016)</caption>
<tr>
<th style="border-top: double; text-align:center; font-style:normal; font-weight:bold; padding:0.2cm;  text-align:left; ">&nbsp;</th>
<th colspan="4" style="border-top: double; text-align:center; font-style:normal; font-weight:bold; padding:0.2cm; ">Incumbent
 National Popular Two Party Vote Share (%)</th>
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
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">49.21</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">1.95</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">45.00&nbsp;&ndash;&nbsp;53.42</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  "><strong>&lt;0.001</strong></td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">Quarterly RDPI Growth (%)</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">0.70</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">0.37</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">&#45;0.09&nbsp;&ndash;&nbsp;1.49</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">0.078</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; padding-top:0.1cm; padding-bottom:0.1cm; border-top:1px solid;">Observations</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; padding-top:0.1cm; padding-bottom:0.1cm; text-align:left; border-top:1px solid;" colspan="4">15</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; padding-top:0.1cm; padding-bottom:0.1cm;">R<sup>2</sup> / R<sup>2</sup> adjusted</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; padding-top:0.1cm; padding-bottom:0.1cm; text-align:left;" colspan="4">0.220 / 0.160</td>
</tr>

</table>

<table style="border-collapse:collapse; border:none;">
<caption style="font-weight: bold; text-align:left;">Regression Table for Annual RDPI Growth (1960-2016)</caption>
<tr>
<th style="border-top: double; text-align:center; font-style:normal; font-weight:bold; padding:0.2cm;  text-align:left; ">&nbsp;</th>
<th colspan="4" style="border-top: double; text-align:center; font-style:normal; font-weight:bold; padding:0.2cm; ">Incumbent
 National Popular Two Party Vote Share (%)</th>
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
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">46.48</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">2.30</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">41.50&nbsp;&ndash;&nbsp;51.45</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  "><strong>&lt;0.001</strong></td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">Annual RDPI Growth (%)</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">1.49</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">0.53</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">0.33&nbsp;&ndash;&nbsp;2.64</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  "><strong>0.015</strong></td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; padding-top:0.1cm; padding-bottom:0.1cm; border-top:1px solid;">Observations</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; padding-top:0.1cm; padding-bottom:0.1cm; text-align:left; border-top:1px solid;" colspan="4">15</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; padding-top:0.1cm; padding-bottom:0.1cm;">R<sup>2</sup> / R<sup>2</sup> adjusted</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; padding-top:0.1cm; padding-bottom:0.1cm; text-align:left;" colspan="4">0.374 / 0.325</td>
</tr>

</table>










# S&P 500 Growth
<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-10-1.png" width="672" />
<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-11-1.png" width="672" />

These graphs were quite unexpected for me. I initially thought the S&P 500 would be a strong indicator of how most Americans perceive the economy, given that it is reported daily by nearly every news source and many Americans have a significant personal stake in its performance, especially through retirement savings tied to the S&P 500. However, the nearly flat lines in both graphs and the large standard errors indicate that the S&P 500 is a poor predictor of election outcomes.

Looking at the tables, the quarterly growth shows a slight inverse relationship of -0.82, which doesn't make much sense, though this result can largely be disregarded due to the high p-value and the low R-squared of 0.053. The annual model shows almost no relationship between two-party vote share and annual S&P 500 growth, with similarly large p-values and inconsequential R-squared values.

Overall, while the S&P 500 may have value in models that aggregate multiple economic variables, it is clear that it performs poorly as a standalone predictor of election outcomes.


<table style="border-collapse:collapse; border:none;">
<caption style="font-weight: bold; text-align:left;">Regression Table for Quarterly S&P 500 Growth (1960-2016)</caption>
<tr>
<th style="border-top: double; text-align:center; font-style:normal; font-weight:bold; padding:0.2cm;  text-align:left; ">&nbsp;</th>
<th colspan="4" style="border-top: double; text-align:center; font-style:normal; font-weight:bold; padding:0.2cm; ">Incumbent
 National Popular Two Party Vote Share (%)</th>
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
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">52.60</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">1.50</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">49.37&nbsp;&ndash;&nbsp;55.84</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  "><strong>&lt;0.001</strong></td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">Quarterly S&P 500 Growth (%)</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">&#45;0.82</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">0.96</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">&#45;2.88&nbsp;&ndash;&nbsp;1.25</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">0.408</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; padding-top:0.1cm; padding-bottom:0.1cm; border-top:1px solid;">Observations</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; padding-top:0.1cm; padding-bottom:0.1cm; text-align:left; border-top:1px solid;" colspan="4">15</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; padding-top:0.1cm; padding-bottom:0.1cm;">R<sup>2</sup> / R<sup>2</sup> adjusted</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; padding-top:0.1cm; padding-bottom:0.1cm; text-align:left;" colspan="4">0.053 / -0.020</td>
</tr>

</table>
<table style="border-collapse:collapse; border:none;">
<caption style="font-weight: bold; text-align:left;">Regression Table for Annual S&P 500 Growth (1960-2016)</caption>
<tr>
<th style="border-top: double; text-align:center; font-style:normal; font-weight:bold; padding:0.2cm;  text-align:left; ">&nbsp;</th>
<th colspan="4" style="border-top: double; text-align:center; font-style:normal; font-weight:bold; padding:0.2cm; ">Incumbent
 National Popular Two Party Vote Share (%)</th>
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
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">51.79</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">1.60</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">48.34&nbsp;&ndash;&nbsp;55.24</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  "><strong>&lt;0.001</strong></td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">Annual S&P 500 Growth (%)</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">0.05</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">0.14</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">&#45;0.25&nbsp;&ndash;&nbsp;0.36</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">0.707</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; padding-top:0.1cm; padding-bottom:0.1cm; border-top:1px solid;">Observations</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; padding-top:0.1cm; padding-bottom:0.1cm; text-align:left; border-top:1px solid;" colspan="4">15</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; padding-top:0.1cm; padding-bottom:0.1cm;">R<sup>2</sup> / R<sup>2</sup> adjusted</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; padding-top:0.1cm; padding-bottom:0.1cm; text-align:left;" colspan="4">0.011 / -0.065</td>
</tr>

</table>

# Unemployment Growth

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-14-1.png" width="672" />
<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-15-1.png" width="672" />

Unemployment growth also proved surprising, though for the opposite reason. I chose to focus on unemployment rather than GDP as a test of macroeconomic conditions, since unemployment is typically more frequently reported in the news than GDP, as evidenced by its relevance in Tuesday’s debate. Many Americans who vote based on sociotropic conditions may be more influenced by unemployment than GDP.

Both graphs show a strong inverse relationship between unemployment growth and two-party vote share. Looking at the tables, we see that a one percent reduction in unemployment is associated with a 0.6 increase in two-party vote share for the incumbent party. The annual model displayed a smaller coefficient of -0.23. Both models were statistically significant at the 0.05 level according to their p-values, and they had fairly strong R-squared values: 0.405 for the quarterly model and 0.38 for the annual model. Quarterly unemployment growth had the highest R-squared value of all six models analyzed.

<table style="border-collapse:collapse; border:none;">
<caption style="font-weight: bold; text-align:left;">Regression Table for Quarterly Unemployment Growth (1960-2016)</caption>
<tr>
<th style="border-top: double; text-align:center; font-style:normal; font-weight:bold; padding:0.2cm;  text-align:left; ">&nbsp;</th>
<th colspan="4" style="border-top: double; text-align:center; font-style:normal; font-weight:bold; padding:0.2cm; ">Incumbent
 National Popular Two Party Vote Share (%)</th>
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
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">52.13</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">1.08</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">49.78&nbsp;&ndash;&nbsp;54.47</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  "><strong>&lt;0.001</strong></td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">Quarterly Unemployment Growth (%)</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">&#45;0.60</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">0.20</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">&#45;1.03&nbsp;&ndash;&nbsp;-0.16</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  "><strong>0.011</strong></td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; padding-top:0.1cm; padding-bottom:0.1cm; border-top:1px solid;">Observations</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; padding-top:0.1cm; padding-bottom:0.1cm; text-align:left; border-top:1px solid;" colspan="4">15</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; padding-top:0.1cm; padding-bottom:0.1cm;">R<sup>2</sup> / R<sup>2</sup> adjusted</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; padding-top:0.1cm; padding-bottom:0.1cm; text-align:left;" colspan="4">0.405 / 0.359</td>
</tr>

</table>
<table style="border-collapse:collapse; border:none;">
<caption style="font-weight: bold; text-align:left;">Regression Table for Annual Unemployment Growth (1960-2016)</caption>
<tr>
<th style="border-top: double; text-align:center; font-style:normal; font-weight:bold; padding:0.2cm;  text-align:left; ">&nbsp;</th>
<th colspan="4" style="border-top: double; text-align:center; font-style:normal; font-weight:bold; padding:0.2cm; ">Incumbent
 National Popular Two Party Vote Share (%)</th>
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
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">51.29</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">1.14</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">48.83&nbsp;&ndash;&nbsp;53.76</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  "><strong>&lt;0.001</strong></td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">Annual Unemployment Growth (%)</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">&#45;0.23</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">0.08</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">&#45;0.41&nbsp;&ndash;&nbsp;-0.05</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  "><strong>0.014</strong></td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; padding-top:0.1cm; padding-bottom:0.1cm; border-top:1px solid;">Observations</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; padding-top:0.1cm; padding-bottom:0.1cm; text-align:left; border-top:1px solid;" colspan="4">15</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; padding-top:0.1cm; padding-bottom:0.1cm;">R<sup>2</sup> / R<sup>2</sup> adjusted</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; padding-top:0.1cm; padding-bottom:0.1cm; text-align:left;" colspan="4">0.380 / 0.332</td>
</tr>

</table>


# Predictions and Concluding Thoughts

Given its poor in-sample model fit, I decided not to use the S&P 500 as a predictor for the election. All the economic predictors suggest a Donald Trump popular vote victory, but at a 95% confidence interval, an extremely wide range of outcomes is possible.


Table: <span id="tab:unnamed-chunk-18"></span>Table 1: **Predicted 2024 Incumbent
 National Popular Two Party Vote Share based on RDPI Growth**

|Independent Variable  | Predicted Two Party Vote Share| Lower Bound (95% CI)| Upper Bound (95% CI)|
|:---------------------|------------------------------:|--------------------:|--------------------:|
|Quarterly RDPI Growth |                          49.91|                38.90|                60.91|
|Annual RDPI Growth    |                          47.88|                37.73|                58.03|


Table: <span id="tab:unnamed-chunk-19"></span>Table 2: **Predicted 2024 Incumbent
 National Popular Two Party Vote Share based on Unemployment Growth**

|Independent Variable          | Predicted Two Party Vote Share| Lower Bound (95% CI)| Upper Bound (95% CI)|
|:-----------------------------|------------------------------:|--------------------:|--------------------:|
|Quarterly Unemployment Growth |                          48.97|                39.33|                58.61|
|Annual Unemployment Growth    |                          48.45|                38.49|                58.42|


Overall, I believe the best approach to using economic predictors is to aggregate multiple variables, such as RDPI growth and unemployment growth, and weigh them accordingly as part of a larger model that also incorporates polling and other fundamentals. It’s clear that no single economic factor is sufficient to predict an election, nor is there a strong preference between factors that affect personal wealth versus macroeconomic conditions. The highest R-squared any of the models achieved as 0.4, meaning around 60% of the variance in elections could not be accounted for. Of course, multicollinearity would be a significant issue in any model using multiple economic factors, so adjustments to account for it would be necessary.






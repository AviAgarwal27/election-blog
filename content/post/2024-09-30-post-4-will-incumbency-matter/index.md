---
title: 'Post #4: Will Incumbency Matter?'
author: Avi Agarwal
date: '2024-09-30'
slug: post-4-will-incumbency-matter
categories: []
tags: []
---



































# Introduction

Typically, the question of incumbency in an election is straightforward: either one of the candidates is the sitting president, or they aren’t. Of course, in 2024, no question is that simple.

In this week’s post, I’ll address a few key questions: how to factor Kamala Harris’ status as an incumbent in predictions, whether incumbency has a significant effect on forecasts, and how my models compare to Abramowitz’s Time for Change model, which emphasizes incumbency.


# Who are the incumbents?

In a contest between Biden and Trump, the issue of incumbency would be clear. Even though Trump is a former president, both candidates have similar levels of notoriety, with Biden closely tied to the current administration. However, with Harris as the nominee, some might argue that Trump’s status as a former president grants him an advantage similar to that of an incumbent. I disagree for a few reasons.

First, despite his decisive primary win, Trump faced notable challengers, including Florida Governor Ron DeSantis. While his victory demonstrates his grip on the Republican base, it also meant he had to spend time contesting with party rivals rather than focusing on the general election. Second, Trump lacks access to federal grant spending and control over the executive branch—one of the strongest advantages of incumbency. Lastly, voter fatigue, often a downside of incumbency, also applies to Trump, given his dominance in American politics over the past decade. I believe Trump’s notoriety will be reflected in his polling averages, eliminating the need for additional variables to account for his unique circumstances.

A similar question arises with Harris: should she be considered an incumbent due to her last-minute nomination and close ties to the administration? I argue no, for several reasons. One of the most significant advantages of incumbency is bypassing the primary process. While Harris didn’t face challengers, she also missed out on the extra six months of campaigning that normally comes with being the automatic nominee. She was only confirmed as the nominee about two weeks before the convention. Additionally, while Harris is a prominent part of the administration, she doesn’t control federal grant spending. Many of the Biden administration’s priorities, such as infrastructure and manufacturing, are more closely associated with Biden himself, who often touts his blue-collar background—something Harris rarely campaigns on. Finally, she lacked the public recognition typically enjoyed by incumbents before being named the nominee, making her more akin to an up-and-coming challenger than an incumbent.
Thus, for the purposes of my models, I will consider Harris an incumbent-party nominee.


# Model One: Excluding Incumbency

To test the broader effect of the incumbent party on election outcomes, I built two models that predict the Democratic two-party vote share based on basic fundamentals: one includes incumbency, and the other excludes it. The models use two fundamental factors. The first is a weighted poll average from weeks 12 to 7 leading up to the election wich only includes data comparing Harris to Trump. To create the weight, I averaged the polls for each week and regressed them against the two-party vote share. Then, I used the coefficients from the model to create a weighted average. The second factor is quarter 2 real disposable personal income (RDPI) growth, identified as the best economic covariate in blog post #2. I chose to use only one economic variable to avoid issues of multicollinearity. The model uses data from 1968 to 2016 and excludes 2020, as the unique economic factors of the COVID pandemic make it an outlier. It's important to note that this model will improve as the election nears, with more recent polling data and quarter 3 RDPI growth.


<table style="border-collapse:collapse; border:none;">
<caption style="font-weight: bold; text-align:left;">Excluding Incumbent Regression Results</caption>
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
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">22.06</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">4.64</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">11.71&nbsp;&ndash;&nbsp;32.41</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  "><strong>0.001</strong></td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">weighted_avg_poll</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">0.60</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">0.10</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">0.38&nbsp;&ndash;&nbsp;0.83</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  "><strong>&lt;0.001</strong></td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">RDPI_growth_quarterly</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">0.24</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">0.24</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">&#45;0.30&nbsp;&ndash;&nbsp;0.78</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">0.340</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; padding-top:0.1cm; padding-bottom:0.1cm; border-top:1px solid;">Observations</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; padding-top:0.1cm; padding-bottom:0.1cm; text-align:left; border-top:1px solid;" colspan="4">13</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; padding-top:0.1cm; padding-bottom:0.1cm;">R<sup>2</sup> / R<sup>2</sup> adjusted</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; padding-top:0.1cm; padding-bottom:0.1cm; text-align:left;" colspan="4">0.777 / 0.732</td>
</tr>

</table>

The model results, shown above, have an adjusted R-squared of 0.732, which is decently high. However, since the RDPI increase is statistically insignificant at a test statistic of 0.05, most of the prediction is driven by the weighted poll average. This model predicts Harris winning about 51% of the two-party vote, with a wide 75% confidence interval.

<table style="border-collapse:collapse; border:none;">
<caption style="font-weight: bold; text-align:left;">2024 Democrat Two Party Vote Share via Model Excluding Incumbent Party</caption>
<tr>
<th style="border-top: double; text-align:center; font-style:italic; font-weight:normal; padding:0.2cm; border-bottom:1px solid black; text-align:left; ">Prediction</th>
<th style="border-top: double; text-align:center; font-style:italic; font-weight:normal; padding:0.2cm; border-bottom:1px solid black; ">Lower.Bound</th>
<th style="border-top: double; text-align:center; font-style:italic; font-weight:normal; padding:0.2cm; border-bottom:1px solid black; ">Upper.Bound</th>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; border-bottom: double; ">50.96%</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; border-bottom: double; ">44.70%</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; border-bottom: double; ">57.22%</td>
</tr>
</table>

# Model Two: Including Incumbency

Using the same fundamentals but adding a binary incumbent party variable (1 if the candidate is from the same party as the sitting president) immediately improves the overall model. The adjusted R-squared increases by more than 0.1, totaling 0.836, meaning this model accounts for 83.6% of the variance in elections. Additionally, all covariates are statistically significant at a test statistic of 0.05.


<table style="border-collapse:collapse; border:none;">
<caption style="font-weight: bold; text-align:left;">Including Incumbent Regression Results</caption>
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
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">20.02</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">3.71</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">11.63&nbsp;&ndash;&nbsp;28.40</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  "><strong>&lt;0.001</strong></td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">weighted_avg_poll</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">0.59</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">0.08</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">0.41&nbsp;&ndash;&nbsp;0.77</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  "><strong>&lt;0.001</strong></td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">RDPI_growth_quarterly</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">0.49</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">0.21</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">0.01&nbsp;&ndash;&nbsp;0.96</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  "><strong>0.045</strong></td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">incumbent_party</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">3.42</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">1.26</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">0.57&nbsp;&ndash;&nbsp;6.28</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  "><strong>0.024</strong></td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; padding-top:0.1cm; padding-bottom:0.1cm; border-top:1px solid;">Observations</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; padding-top:0.1cm; padding-bottom:0.1cm; text-align:left; border-top:1px solid;" colspan="4">13</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; padding-top:0.1cm; padding-bottom:0.1cm;">R<sup>2</sup> / R<sup>2</sup> adjusted</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; padding-top:0.1cm; padding-bottom:0.1cm; text-align:left;" colspan="4">0.877 / 0.836</td>
</tr>

</table>

This model shows an increase in Democratic vote share by about 1% and a slightly narrower confidence interval, with overall predictions still favoring Harris winning the two-party vote share.


<table style="border-collapse:collapse; border:none;">
<caption style="font-weight: bold; text-align:left;">2024 Democrat Two Party Vote Share via Model Including Incumbent Party</caption>
<tr>
<th style="border-top: double; text-align:center; font-style:italic; font-weight:normal; padding:0.2cm; border-bottom:1px solid black; text-align:left; ">Prediction</th>
<th style="border-top: double; text-align:center; font-style:italic; font-weight:normal; padding:0.2cm; border-bottom:1px solid black; ">Lower.Bound</th>
<th style="border-top: double; text-align:center; font-style:italic; font-weight:normal; padding:0.2cm; border-bottom:1px solid black; ">Upper.Bound</th>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; border-bottom: double; ">52.10%</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; border-bottom: double; ">47.04%</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; border-bottom: double; ">57.17%</td>
</tr>
</table>

# Time For Change Model

To compare this model to a prominent one, I created a representative model using Abramowitz's Time for Change model. I also excluded 2020, as Abramowitz used a different model for that election.

<table style="border-collapse:collapse; border:none;">
<caption style="font-weight: bold; text-align:left;">Time For Change Regression Results</caption>
<tr>
<th style="border-top: double; text-align:center; font-style:normal; font-weight:bold; padding:0.2cm;  text-align:left; ">&nbsp;</th>
<th colspan="4" style="border-top: double; text-align:center; font-style:normal; font-weight:bold; padding:0.2cm; ">Incumbent Party Two Party Vote Share</th>
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
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">49.34</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">1.95</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">44.92&nbsp;&ndash;&nbsp;53.75</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  "><strong>&lt;0.001</strong></td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">juneapp</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">0.17</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">0.06</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">0.02&nbsp;&ndash;&nbsp;0.31</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  "><strong>0.030</strong></td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">GDP_growth_quarterly</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">0.33</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">0.27</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">&#45;0.28&nbsp;&ndash;&nbsp;0.93</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">0.251</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">incumbent</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">1.65</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">1.79</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">&#45;2.39&nbsp;&ndash;&nbsp;5.70</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">0.379</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; padding-top:0.1cm; padding-bottom:0.1cm; border-top:1px solid;">Observations</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; padding-top:0.1cm; padding-bottom:0.1cm; text-align:left; border-top:1px solid;" colspan="4">13</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; padding-top:0.1cm; padding-bottom:0.1cm;">R<sup>2</sup> / R<sup>2</sup> adjusted</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; padding-top:0.1cm; padding-bottom:0.1cm; text-align:left;" colspan="4">0.734 / 0.646</td>
</tr>

</table>

As shown above, my model performs slightly better in terms of adjusted R-squared and covariate statistical significance. Additionally, his model predicts a Trump victory in the two-party vote share, likely due to its reliance on the June approval rating, which was historically low for Joe Biden, harming the incumbent party—in this case, the Democrats.

<table style="border-collapse:collapse; border:none;">
<caption style="font-weight: bold; text-align:left;">2024 Democrat Two Party Vote Share via Time for Change Model</caption>
<tr>
<th style="border-top: double; text-align:center; font-style:italic; font-weight:normal; padding:0.2cm; border-bottom:1px solid black; text-align:left; ">Prediction</th>
<th style="border-top: double; text-align:center; font-style:italic; font-weight:normal; padding:0.2cm; border-bottom:1px solid black; ">Lower.Bound</th>
<th style="border-top: double; text-align:center; font-style:italic; font-weight:normal; padding:0.2cm; border-bottom:1px solid black; ">Upper.Bound</th>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; border-bottom: double; ">46.67%</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; border-bottom: double; ">39.12%</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; border-bottom: double; ">54.23%</td>
</tr>
</table>

# Conclusion

Overall, it’s clear that incumbency is important to include in this election, even though defining who qualifies as an incumbent is far from straightforward.

In the coming weeks, I will modify the second model to create state-level predictions for the seven swing states and build a prediction for the Electoral College, which I will update weekly. Thanks for reading!


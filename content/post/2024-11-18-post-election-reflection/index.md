---
title: Post-Election Reflection
author: Avi Agarwal
date: '2024-11-18'
slug: post-election-reflection
categories: []
tags: []
---

<script src="{{< blogdown/postref >}}index_files/kePrint/kePrint.js"></script>
<link href="{{< blogdown/postref >}}index_files/lightable/lightable.css" rel="stylesheet" />
<script src="{{< blogdown/postref >}}index_files/kePrint/kePrint.js"></script>
<link href="{{< blogdown/postref >}}index_files/lightable/lightable.css" rel="stylesheet" />
<script src="{{< blogdown/postref >}}index_files/kePrint/kePrint.js"></script>
<link href="{{< blogdown/postref >}}index_files/lightable/lightable.css" rel="stylesheet" />
<script src="{{< blogdown/postref >}}index_files/kePrint/kePrint.js"></script>
<link href="{{< blogdown/postref >}}index_files/lightable/lightable.css" rel="stylesheet" />
<script src="{{< blogdown/postref >}}index_files/htmlwidgets/htmlwidgets.js"></script>
<script src="{{< blogdown/postref >}}index_files/plotly-binding/plotly.js"></script>
<script src="{{< blogdown/postref >}}index_files/typedarray/typedarray.min.js"></script>
<script src="{{< blogdown/postref >}}index_files/jquery/jquery.min.js"></script>
<link href="{{< blogdown/postref >}}index_files/crosstalk/css/crosstalk.min.css" rel="stylesheet" />
<script src="{{< blogdown/postref >}}index_files/crosstalk/js/crosstalk.min.js"></script>
<link href="{{< blogdown/postref >}}index_files/plotly-htmlwidgets-css/plotly-htmlwidgets.css" rel="stylesheet" />
<script src="{{< blogdown/postref >}}index_files/plotly-main/plotly-latest.min.js"></script>
<script src="{{< blogdown/postref >}}index_files/kePrint/kePrint.js"></script>
<link href="{{< blogdown/postref >}}index_files/lightable/lightable.css" rel="stylesheet" />
<script src="{{< blogdown/postref >}}index_files/kePrint/kePrint.js"></script>
<link href="{{< blogdown/postref >}}index_files/lightable/lightable.css" rel="stylesheet" />
<script src="{{< blogdown/postref >}}index_files/kePrint/kePrint.js"></script>

<link href="{{< blogdown/postref >}}index_files/lightable/lightable.css" rel="stylesheet" />

# Recap of Model

My model used an enabling method combining three OLS regressions, which is displayed below. The first model focused on fundamentals, the second on polling, and the third used a combined approach. The exact meaning of each covariate can be found in my final election prediction post

**Model 1:**  
$$
`\begin{aligned}
D\_pv2p = & \, \alpha + \beta_1(\text{state}) + \beta_2(\text{D\_pv2p\_lag1}) + \beta_3(\text{D\_pv2p\_lag2}) \\
& + \beta_4(\text{updated\_rdpi} \times \text{incumbent\_party}) + \beta_5(\text{dpi\_inflation\_adjusted} \times \text{incumbent\_party}) + \epsilon
\end{aligned}`
  $$
**Model 2:**  
$$
`\begin{aligned}
D\_pv2p = & \, \alpha + \beta_1(\text{state}) + \beta_2(\text{polling\_trend\_5\_1}) + \beta_3(\text{polling\_trend\_10\_6}) \\
& + \beta_4(\text{current\_week}) + \beta_5(\text{support\_DEM\_1}) + \beta_6(\text{support\_DEM\_2}) + \beta_7(\text{support\_DEM\_3}) + \epsilon
\end{aligned}`
  $$
**Model 3:**  
$$
`\begin{aligned}
D\_pv2p = & \, \alpha + \beta_1(\text{state}) + \beta_2(\text{D\_pv2p\_lag1}) + \beta_3(\text{D\_pv2p\_lag2}) + \beta_4(\text{support\_DEM\_1}) \\
& + \beta_5(\text{polling\_trend\_5\_1}) + \beta_6(\text{polling\_trend\_10\_6}) + \beta_7(\text{dpi\_inflation\_adjusted} \times \text{incumbent\_party}) \\
& + \beta_8(\text{unemployment\_growth\_quarterly} \times \text{incumbent\_party}) + \beta_9(\text{updated\_rdpi} \times \text{incumbent\_party}) + \epsilon
\end{aligned}`
  $$

To generate the weights displayed below, I used a Leave-Out-Out scheme that predicted the outcome of each election via each model in the data set (1980 to 2020), excluding that year’s election in the training dataset. Then, I used constrained optimization to create weights.

<table class="table table-striped table-hover table-condensed table-responsive" style="width: auto !important; margin-left: auto; margin-right: auto;">
<caption>
<span id="tab:unnamed-chunk-2"></span>Table 1: Model Weights by State
</caption>
<thead>
<tr>
<th style="text-align:left;">
State
</th>
<th style="text-align:right;">
Model 1
</th>
<th style="text-align:right;">
Model 2
</th>
<th style="text-align:right;">
Model 3
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;width: 8em; text-align: center;">
Arizona
</td>
<td style="text-align:right;width: 6em; text-align: center;">
0.028
</td>
<td style="text-align:right;width: 6em; text-align: center;">
0.972
</td>
<td style="text-align:right;width: 6em; text-align: center;">
0.000
</td>
</tr>
<tr>
<td style="text-align:left;width: 8em; text-align: center;">
Georgia
</td>
<td style="text-align:right;width: 6em; text-align: center;">
0.130
</td>
<td style="text-align:right;width: 6em; text-align: center;">
0.838
</td>
<td style="text-align:right;width: 6em; text-align: center;">
0.031
</td>
</tr>
<tr>
<td style="text-align:left;width: 8em; text-align: center;">
Michigan
</td>
<td style="text-align:right;width: 6em; text-align: center;">
0.129
</td>
<td style="text-align:right;width: 6em; text-align: center;">
0.610
</td>
<td style="text-align:right;width: 6em; text-align: center;">
0.260
</td>
</tr>
<tr>
<td style="text-align:left;width: 8em; text-align: center;">
Nevada
</td>
<td style="text-align:right;width: 6em; text-align: center;">
0.128
</td>
<td style="text-align:right;width: 6em; text-align: center;">
0.730
</td>
<td style="text-align:right;width: 6em; text-align: center;">
0.143
</td>
</tr>
<tr>
<td style="text-align:left;width: 8em; text-align: center;">
North Carolina
</td>
<td style="text-align:right;width: 6em; text-align: center;">
0.395
</td>
<td style="text-align:right;width: 6em; text-align: center;">
0.570
</td>
<td style="text-align:right;width: 6em; text-align: center;">
0.034
</td>
</tr>
<tr>
<td style="text-align:left;width: 8em; text-align: center;">
Pennsylvania
</td>
<td style="text-align:right;width: 6em; text-align: center;">
0.031
</td>
<td style="text-align:right;width: 6em; text-align: center;">
0.958
</td>
<td style="text-align:right;width: 6em; text-align: center;">
0.010
</td>
</tr>
<tr>
<td style="text-align:left;width: 8em; text-align: center;">
Wisconsin
</td>
<td style="text-align:right;width: 6em; text-align: center;">
0.154
</td>
<td style="text-align:right;width: 6em; text-align: center;">
0.642
</td>
<td style="text-align:right;width: 6em; text-align: center;">
0.204
</td>
</tr>
</tbody>
</table>

Using data from the 2024 election resulted in the following prediction in the table below compared to the estimated actual results of the seven swing states. This prediction forecasted a Harris Victory, with the VP winning Wisconsin, Nevada, Michigan, and Pennsylvania and Trump winning Arizona, Georgia, and North Carolina.

<table class="table table-striped table-hover table-condensed" style="width: auto !important; margin-left: auto; margin-right: auto;">
<caption>
<span id="tab:unnamed-chunk-5"></span>Table 2: 2024 Presidential Election Results by State
</caption>
<thead>
<tr>
<th style="text-align:left;">
State
</th>
<th style="text-align:right;">
Real Democratic Vote Share (%)
</th>
<th style="text-align:right;">
Predicted Democratic Vote Share (%)
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">
Arizona
</td>
<td style="text-align:right;">
47.153
</td>
<td style="text-align:right;">
47.69
</td>
</tr>
<tr>
<td style="text-align:left;">
Georgia
</td>
<td style="text-align:right;">
48.878
</td>
<td style="text-align:right;">
49.23
</td>
</tr>
<tr>
<td style="text-align:left;">
Michigan
</td>
<td style="text-align:right;">
49.302
</td>
<td style="text-align:right;">
51.41
</td>
</tr>
<tr>
<td style="text-align:left;">
Nevada
</td>
<td style="text-align:right;">
48.378
</td>
<td style="text-align:right;">
51.68
</td>
</tr>
<tr>
<td style="text-align:left;">
North Carolina
</td>
<td style="text-align:right;">
48.299
</td>
<td style="text-align:right;">
49.24
</td>
</tr>
<tr>
<td style="text-align:left;">
Pennsylvania
</td>
<td style="text-align:right;">
48.982
</td>
<td style="text-align:right;">
50.30
</td>
</tr>
<tr>
<td style="text-align:left;">
Wisconsin
</td>
<td style="text-align:right;">
49.532
</td>
<td style="text-align:right;">
50.68
</td>
</tr>
</tbody>
</table>

I simulated the outcomes of the seven swing states 1000 times to account for polling error, in which Harris won 58.9% of the time.

<table class="table table-striped table-hover table-condensed table-responsive" style="width: auto !important; margin-left: auto; margin-right: auto;">
<caption>
<span id="tab:unnamed-chunk-6"></span>Table 3: Simulation Results: Harris and Trump Victory Counts
</caption>
<thead>
<tr>
<th style="text-align:right;">
Harris Victory Wins
</th>
<th style="text-align:right;">
Trump Victory Wins
</th>
<th style="text-align:left;">
Harris Victory %
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:right;width: 5em; text-align: center;">
589
</td>
<td style="text-align:right;width: 5em; text-align: center;">
411
</td>
<td style="text-align:left;width: 5em; text-align: center;">
58.9%
</td>
</tr>
</tbody>
</table>

# Measuring Model Error

Obviously, my model was very incorrect, estimating only 3/7 swing states correctly and predicting the wrong person as the next President. However, to quantify the error, I calculated the bias, MSE, RMSE, and MAE based on the estimated 2024 election results.

It is very apparent that my model was biased against Donald Trump, overestimating Democratic vote share in every single swing state – including the states I had predicted Trump to win. However, the magnitude of the bias is far from consistent, being less than 0.5 in Arizona and more significant than 3.3 in Nevada. As a side note, the bias, RMSE, and MAE have the same magnitude since only one observation per metric exists. The average RMSE was 1.148, meaning my prediction was, on average, overestimating Democratic vote share by 1.148 points in each swing state – not a massive amount, but enough to flip the election’s outcome entirely

<table class="table table-striped table-hover table-condensed" style="width: auto !important; margin-left: auto; margin-right: auto;">
<caption>
<span id="tab:unnamed-chunk-7"></span>Table 4: State-Level MSE Table
</caption>
<thead>
<tr>
<th style="text-align:left;">
State
</th>
<th style="text-align:right;">
Bias
</th>
<th style="text-align:right;">
MSE
</th>
<th style="text-align:right;">
RMSE
</th>
<th style="text-align:right;">
MAE
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">
Arizona
</td>
<td style="text-align:right;">
-0.537
</td>
<td style="text-align:right;">
0.289
</td>
<td style="text-align:right;">
0.537
</td>
<td style="text-align:right;">
0.537
</td>
</tr>
<tr>
<td style="text-align:left;">
Georgia
</td>
<td style="text-align:right;">
-0.352
</td>
<td style="text-align:right;">
0.124
</td>
<td style="text-align:right;">
0.352
</td>
<td style="text-align:right;">
0.352
</td>
</tr>
<tr>
<td style="text-align:left;">
Michigan
</td>
<td style="text-align:right;">
-2.108
</td>
<td style="text-align:right;">
4.446
</td>
<td style="text-align:right;">
2.108
</td>
<td style="text-align:right;">
2.108
</td>
</tr>
<tr>
<td style="text-align:left;">
Nevada
</td>
<td style="text-align:right;">
-3.302
</td>
<td style="text-align:right;">
10.901
</td>
<td style="text-align:right;">
3.302
</td>
<td style="text-align:right;">
3.302
</td>
</tr>
<tr>
<td style="text-align:left;">
North Carolina
</td>
<td style="text-align:right;">
-0.941
</td>
<td style="text-align:right;">
0.886
</td>
<td style="text-align:right;">
0.941
</td>
<td style="text-align:right;">
0.941
</td>
</tr>
<tr>
<td style="text-align:left;">
Pennsylvania
</td>
<td style="text-align:right;">
-1.318
</td>
<td style="text-align:right;">
1.736
</td>
<td style="text-align:right;">
1.318
</td>
<td style="text-align:right;">
1.318
</td>
</tr>
<tr>
<td style="text-align:left;">
Wisconsin
</td>
<td style="text-align:right;">
-1.148
</td>
<td style="text-align:right;">
1.319
</td>
<td style="text-align:right;">
1.148
</td>
<td style="text-align:right;">
1.148
</td>
</tr>
<tr>
<td style="text-align:left;">
Average
</td>
<td style="text-align:right;">
-1.387
</td>
<td style="text-align:right;">
2.814
</td>
<td style="text-align:right;">
1.387
</td>
<td style="text-align:right;">
1.387
</td>
</tr>
<tr>
<td style="text-align:left;">
Median
</td>
<td style="text-align:right;">
-1.148
</td>
<td style="text-align:right;">
1.319
</td>
<td style="text-align:right;">
1.148
</td>
<td style="text-align:right;">
1.148
</td>
</tr>
</tbody>
</table>

The map below shows how much I overestimated the Democratic vote share in each state, with a darker shade of red equating to a higher overestimation. In states where I predicted Trump to win, there is only a slight bias compared to states where I expected Kamala to win, where the bias is much greater.

<div class="plotly html-widget html-fill-item" id="htmlwidget-1" style="width:672px;height:480px;"></div>
<script type="application/json" data-for="htmlwidget-1">{"x":{"visdat":{"61804222f94":["function () ","plotlyVisDat"]},"cur_data":"61804222f94","attrs":{"61804222f94":{"locations":{},"locationmode":"USA-states","z":{},"text":{},"hoverinfo":"text","colorscale":[["0","darkred"],["0.5","white"],["1","darkblue"]],"zmin":-4,"zmid":0,"zmax":4,"colorbar":{"title":"Model Bias <br />(Red = Overestimated <br />Dem. Vote %)","y":0.5,"yanchor":"middle"},"alpha_stroke":1,"sizes":[10,100],"spans":[1,20],"type":"choropleth"}},"layout":{"margin":{"b":40,"l":60,"t":25,"r":10},"title":{"text":"Swing State Model Bias","y":0.94999999999999996,"x":0.5,"xanchor":"center","yanchor":"top"},"geo":{"scope":"usa","projection":{"type":"albers usa"},"showlakes":false,"showcountries":false,"showcoastlines":false,"coastlinecolor":"rgba(255,255,255,1)","showframe":false},"scene":{"zaxis":{"title":"Bias"}},"hovermode":"closest","showlegend":false,"legend":{"yanchor":"top","y":0.5}},"source":"A","config":{"modeBarButtonsToAdd":["hoverclosest","hovercompare"],"showSendToCloud":false},"data":[{"colorbar":{"title":"Model Bias <br />(Red = Overestimated <br />Dem. Vote %)","ticklen":2,"y":0.5,"yanchor":"middle","len":0.5,"lenmode":"fraction"},"colorscale":[["0","darkred"],["0.5","white"],["1","darkblue"]],"showscale":true,"locations":["AZ","GA","MI","NV","NC","PA","WI"],"locationmode":"USA-states","z":[-0.53747346355770276,-0.35155030253291386,-2.1084448240057725,-3.3017124462760208,-0.94110553222387239,-1.3176535411938204,-1.148442057732332],"text":["State: Arizona <br>Bias: -0.54 %","State: Georgia <br>Bias: -0.35 %","State: Michigan <br>Bias: -2.11 %","State: Nevada <br>Bias: -3.3 %","State: North Carolina <br>Bias: -0.94 %","State: Pennsylvania <br>Bias: -1.32 %","State: Wisconsin <br>Bias: -1.15 %"],"hoverinfo":["text","text","text","text","text","text","text"],"zmin":-4,"zmid":0,"zmax":4,"type":"choropleth","marker":{"line":{"color":"rgba(31,119,180,1)"}},"frame":null}],"highlight":{"on":"plotly_click","persistent":false,"dynamic":false,"selectize":false,"opacityDim":0.20000000000000001,"selected":{"opacity":1},"debounce":0},"shinyEvents":["plotly_hover","plotly_click","plotly_selected","plotly_relayout","plotly_brushed","plotly_brushing","plotly_clickannotation","plotly_doubleclick","plotly_deselect","plotly_afterplot","plotly_sunburstclick"],"base_url":"https://plot.ly"},"evals":[],"jsHooks":[]}</script>

To further quantify my prediction error, I tried to create a confusion matrix; however, only two types of forecasts were available: true positives and false positives. As a result, only two metrics can be generated: accuracy and sensitivity, which were around 0.43.

<table class="table table-striped table-hover" style="width: auto !important; margin-left: auto; margin-right: auto;">
<caption>
<span id="tab:unnamed-chunk-9"></span>Table 5: Confusion Matrix Metrics
</caption>
<thead>
<tr>
<th style="text-align:left;">
Metric
</th>
<th style="text-align:right;">
Value
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">
Accuracy
</td>
<td style="text-align:right;">
0.429
</td>
</tr>
<tr>
<td style="text-align:left;">
Sensitivity (Recall)
</td>
<td style="text-align:right;">
0.429
</td>
</tr>
<tr>
<td style="text-align:left;">
Specificity
</td>
<td style="text-align:right;">
NA
</td>
</tr>
<tr>
<td style="text-align:left;">
Precision
</td>
<td style="text-align:right;">
NA
</td>
</tr>
<tr>
<td style="text-align:left;">
F1 Score
</td>
<td style="text-align:right;">
NA
</td>
</tr>
</tbody>
</table>

I also calculated the Brier score of my simulation prediction, which was 0.347.

<table class="table table-striped table-hover" style="width: auto !important; margin-left: auto; margin-right: auto;">
<thead>
<tr>
<th style="text-align:left;">
Metric
</th>
<th style="text-align:right;">
Value
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">
Brier Score
</td>
<td style="text-align:right;">
0.347
</td>
</tr>
</tbody>
</table>

# A Fixed Model

Before exploring the hypotheses explaining why my model was incorrect, I wanted to know if I could adjust the covariates to generate a completely accurate prediction model for the 2024 election.

The adjusted three OLS models listed below, ensembled in the same method as before, correctly predicted that Trump would sweep the swing state. The central adjustment was deleting the measures of Harris’ polling in favor of just using the polling margin (Harris Polling minus Trump Polling), which was measured by current week and polling trend covariates.

**Model 1:**  
$$
`\begin{aligned}
D\_pv2p = & \, \alpha + \beta_1(\text{state}) + \beta_2(\text{D\_pv2p\_lag1}) + \beta_3(\text{D\_pv2p\_lag2}) \\
& + \beta_4(\text{updated\_rdpi} \times \text{incumbent\_party}) + \beta_5(\text{unemployment\_growth\_quarterly} \times \text{incumbent\_party}) \\
& + \beta_6(\text{dpi\_inflation\_adjusted} \times \text{incumbent\_party}) + \epsilon
\end{aligned}`
$$

**Model 2:**  
$$
`\begin{aligned}
D\_pv2p = & \, \alpha + \beta_1(\text{state}) + \beta_2(\text{polling\_trend\_5\_1}) + \beta_3(\text{polling\_trend\_10\_6}) \\
& + \beta_4(\text{current\_week}) + \epsilon
\end{aligned}`
$$

**Model 3:**  
$$
`\begin{aligned}
D\_pv2p = & \, \alpha + \beta_1(\text{state}) + \beta_2(\text{D\_pv2p\_lag1}) + \beta_3(\text{D\_pv2p\_lag2}) + \beta_4(\text{current\_week}) \\
& + \beta_5(\text{polling\_trend\_5\_1}) + \beta_6(\text{polling\_trend\_10\_6}) + \beta_7(\text{dpi\_inflation\_adjusted} \times \text{incumbent\_party}) \\
& + \beta_8(\text{unemployment\_growth\_quarterly} \times \text{incumbent\_party}) + \beta_9(\text{updated\_rdpi} \times \text{incumbent\_party}) + \epsilon
\end{aligned}`
$$
This model, whose bias is depicted below, not only correctly predicted the election’s outcome but also had a much lower average RMSE at a remarkable 0.858. Furthermore, unlike my model, it overestimated Trump’s vote share in some states like Georgia, North Carolina, and Wisconsin – though not by much.

<table class="table table-striped table-hover table-condensed" style="width: auto !important; margin-left: auto; margin-right: auto;">
<caption>
<span id="tab:unnamed-chunk-11"></span>Table 6: Updated Model
</caption>
<thead>
<tr>
<th style="text-align:left;">
State
</th>
<th style="text-align:right;">
Bias
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;">
Arizona
</td>
<td style="text-align:right;">
-0.032
</td>
</tr>
<tr>
<td style="text-align:left;">
Georgia
</td>
<td style="text-align:right;">
1.112
</td>
</tr>
<tr>
<td style="text-align:left;">
Michigan
</td>
<td style="text-align:right;">
-0.308
</td>
</tr>
<tr>
<td style="text-align:left;">
Nevada
</td>
<td style="text-align:right;">
-1.579
</td>
</tr>
<tr>
<td style="text-align:left;">
North Carolina
</td>
<td style="text-align:right;">
1.116
</td>
</tr>
<tr>
<td style="text-align:left;">
Pennsylvania
</td>
<td style="text-align:right;">
-0.033
</td>
</tr>
<tr>
<td style="text-align:left;">
Wisconsin
</td>
<td style="text-align:right;">
0.289
</td>
</tr>
<tr>
<td style="text-align:left;">
Average RMSE
</td>
<td style="text-align:right;">
0.858
</td>
</tr>
</tbody>
</table>

# Why My Model Was Wrong

## Hypothesis \#1: Polling

One reason that stands out is the insight gained from the model I created above. I used measures of poll margin and raw Democratic candidate polling because I believed they captured different aspects of an election. Poll margin indicates how one candidate compares to their competitor, showing the gap between them. On the other hand, raw poll support reflects the general electorate’s enthusiasm for a candidate, acting as a pseudo-measure of turnout. For instance, a race polling at 49-48 is expected to have a significantly higher turnout than a race averaging 43-42. Although the poll margins are identical in both cases, higher enthusiasm could lead to different outcomes in state-specific models.

However, this intuition proved incorrect. I now hypothesize that an increasing trend in overall polarization has caused total polling percentages to more frequently sum to 100. This is because fewer voters remain undecided before election day compared to previous years, resulting in raw polling data having an inflationary effect on the projected Democratic vote share versus actual results.

To measure this, one would need access to unadjusted polling data and analyze the percentage of undecided voters at similar time points across multiple elections. If that percentage has decreased over time, it will support this hypothesis.

However, I do want to note that I do not think the polling error was too significant in favor of Democrats and that one would always incorrectly predict a Harris victory. If you use the polling margin and exclude raw polling support, which is the best predictor of polls in elections, the polling reveals a result that is not too far from reality.

## Hypothesis \#2: The Economy

Another potential explanation for my model’s bias toward the Democrats was an incorrect assessment of the economy’s impact on the election. This election presented a highly unusual economic scenario that rendered typical economic measures insufficient. The non-incumbent candidate was a former President under whom the economy thrived, with most Americans experiencing improved financial conditions from the start of his term until the COVID-19 pandemic. As a result, voters evaluating the incumbent party’s economic performance did not assess Joe Biden’s term in isolation. Instead, they compared it directly to Trump’s first term, which featured record GDP and S&P growth, as well as low unemployment. This comparison created a fundamental challenge for the Democrats. With Trump on the ticket, many Americans recalled the economic boom under his administration, leading to a less favorable view of the Biden administration. However, the growth during Trump’s tenure was unsustainable and unlikely to be maintained, even if the pandemic had not triggered a recession. Thus, the Democrats faced an unfair comparison to an idealized memory of Trump’s economic success that was difficult, if not impossible, to match.

To test this hypothesis, one would want to conduct mass surveys and see how much of people’s perception of the economy is colored by comparisons to Trump’s term. Additionally, one could build models that use comparisons in growth from one term to the last term of the opposing party and see if that improved accuracy for this election.

A further factor lies in how economic indicators are measured. Typically, there is minimal difference between economic conditions in the year before an election and the election year itself, so many analysts, myself included, use the most recent data as economic predictors. However, I did not adequately account for the impact of historically high inflation in 2023, which drove up prices to such an extent that it cast a negative shadow on the economy long after inflation was controlled. Unlike unemployment, which can decrease, prices remain elevated after a spike. Thus, even when inflation was managed and real disposable personal income growth was strong in 2024, the high inflation of 2023 continued to negatively affect Americans’ perceptions of the economy on election day. This is why incorporating state-level DPI economic covariates from the year preceding the election improved the model’s accuracy.

To test this, it is prudent to include additional covariates that capture long-term economic data over the full presidential term or from the period following the midterm elections. Incorporating more measures of consumer confidence and sentiment about the economy, rather than relying solely on objective economic indicators, would be beneficial, as public perception can often differ significantly from fiscal realities.

## Hypothesis \#3: Nevada

To be honest, I am confident that the theories discussed above account for most of the errors in my model. However, I must address the biggest miss in my predictions: Nevada. My model predicted a substantial likelihood of Nevada remaining blue, with only 14 out of 1,000 scenarios showing a Republican win. While most swing states had biases of less than 2 points, Nevada’s was significantly higher at 3.3. Even the adjusted model I created above still overestimated the Democratic vote share by 1.5 points, so my model is clearly consistently missing Nevada. So, why was Nevada so much more inaccurate than the others?

First, polling errors must be considered. Most polls showed Nevada as the only state where Harris had more than a 1-point lead, which proved incorrect. However, I believe the unique inaccuracy in Nevada’s prediction stems from the reliance on lagged vote share. Nevada and North Carolina were the only states that voted for the same party in 2016 and 2020. Unlike North Carolina, Nevada favored the Democrats. Clinton and Biden won the state by over 2 points, making 2024’s result a notable departure from this trend.

Additionally, the Nevada model weighted fundamentals heavily, around 0.15, which caused the high-lagged vote share from 2020 and 2016 to inflate the predicted outcome. However, those past vote shares did not accurately reflect recent demographic shifts within the state. Finally, Nevada’s significant Hispanic population, which saw record shifts toward Trump, further disrupted my prediction.

To test this hypothesis, I could create a model for Nevada excluding lagged vote share and see if it is more representative of the state. This would confirm whether lagged vote share is not a good covariate in some states due to demographic shifts between elections.

# What I Would Change

If I could go back and try again, I would start with the model I developed earlier that showed greater predictive accuracy for the election. I would then allow each state model to use different covariates instead of applying the same ones uniformly, as certain predictors might perform better in specific states. Lastly, I would refine my measurement of economic fundamentals by emphasizing long-term data and consumer sentiment. These combined adjustments would likely result in a more accurate prediction for the 2024 election.

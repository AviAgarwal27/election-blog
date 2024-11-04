---
title: Final Prediction
author: Avi Agarwal
date: '2024-11-04'
slug: final-prediction
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

\#Model 1

$$
\text{Democratic Vote Share (D_pv2p)} = \beta_0 + \beta_1 \text{ State } + \beta_2 \text{ Democratic Vote Share Lag 1 (D_pv2p_lag1)} + \beta_3 \text{ Democratic Vote Share Lag 2 (D_pv2p_lag2)} + \beta_4 \text{ Updated RDPI} \times \text{ Incumbent Party} + \beta_5 \text{ DPI Inflation Adjusted} \times \text{ Incumbent Party} + \epsilon
$$

# Model 2

$$
\text{Democratic Vote Share (D_pv2p)} = \beta_0 + \beta_1 \text{ State } + \beta_2 \text{ Polling Trend (Weeks 5-1) (polling_trend_5_1)} + \beta_3 \text{ Polling Trend (Weeks 10-6) (polling\_trend_10_6)} + \beta_4 \text{ Current Week Margin (current_week)} + \beta_5 \text{ Democratic Support (support_DEM_1)} + \epsilon
$$
\# Model 3
$$
\text{Democratic Vote Share (D_pv2p)} = \beta_0 + \beta_1 \text{ State } + \beta_2 \text{ Democratic Vote Share Lag 1 (D_pv2p_lag1)} + \beta_3 \text{ Democratic Vote Share Lag 2 (D_pv2p_lag2)} + \beta_4 \text{ Democratic Support (support_DEM_1)} + \beta_5 \text{ Polling Trend (Weeks 5-1) (polling_trend_5_1)} + \beta_6 \text{ Polling Trend (Weeks 10-6) (polling_trend_10_6)} + \beta_7 \text{ DPI Inflation Adjusted} \times \text{ Incumbent Party} + \beta_8 \text{ Unemployment Growth Quarterly} \times \text{ Incumbent Party} + \beta_9 \text{ Updated RDPI} \times \text{ Incumbent Party} + \epsilon
$$
\# Weights

<table class="table table-striped table-hover table-condensed table-responsive" style="width: auto !important; margin-left: auto; margin-right: auto;">
<caption>
<span id="tab:unnamed-chunk-20"></span>Table 1: Model Weights by State
</caption>
<thead>
<tr>
<th style="text-align:left;">
State
</th>
<th style="text-align:right;">
Weight.Model.1
</th>
<th style="text-align:right;">
Weight.Model.2
</th>
<th style="text-align:right;">
Weight.Model.3
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;width: 8em; text-align: center;">
Arizona
</td>
<td style="text-align:right;width: 6em; text-align: center;">
0.0000
</td>
<td style="text-align:right;width: 6em; text-align: center;">
1.0000
</td>
<td style="text-align:right;width: 6em; text-align: center;">
0.0000
</td>
</tr>
<tr>
<td style="text-align:left;width: 8em; text-align: center;">
Georgia
</td>
<td style="text-align:right;width: 6em; text-align: center;">
0.0878
</td>
<td style="text-align:right;width: 6em; text-align: center;">
0.9122
</td>
<td style="text-align:right;width: 6em; text-align: center;">
0.0000
</td>
</tr>
<tr>
<td style="text-align:left;width: 8em; text-align: center;">
Michigan
</td>
<td style="text-align:right;width: 6em; text-align: center;">
0.2227
</td>
<td style="text-align:right;width: 6em; text-align: center;">
0.4650
</td>
<td style="text-align:right;width: 6em; text-align: center;">
0.3123
</td>
</tr>
<tr>
<td style="text-align:left;width: 8em; text-align: center;">
Nevada
</td>
<td style="text-align:right;width: 6em; text-align: center;">
0.3240
</td>
<td style="text-align:right;width: 6em; text-align: center;">
0.6032
</td>
<td style="text-align:right;width: 6em; text-align: center;">
0.0727
</td>
</tr>
<tr>
<td style="text-align:left;width: 8em; text-align: center;">
North Carolina
</td>
<td style="text-align:right;width: 6em; text-align: center;">
0.4250
</td>
<td style="text-align:right;width: 6em; text-align: center;">
0.5750
</td>
<td style="text-align:right;width: 6em; text-align: center;">
0.0000
</td>
</tr>
<tr>
<td style="text-align:left;width: 8em; text-align: center;">
Pennsylvania
</td>
<td style="text-align:right;width: 6em; text-align: center;">
0.0922
</td>
<td style="text-align:right;width: 6em; text-align: center;">
0.9078
</td>
<td style="text-align:right;width: 6em; text-align: center;">
0.0000
</td>
</tr>
<tr>
<td style="text-align:left;width: 8em; text-align: center;">
Wisconsin
</td>
<td style="text-align:right;width: 6em; text-align: center;">
0.2659
</td>
<td style="text-align:right;width: 6em; text-align: center;">
0.3742
</td>
<td style="text-align:right;width: 6em; text-align: center;">
0.3599
</td>
</tr>
</tbody>
</table>

# RMSE (In-sample & Out-of-sample)

<table class="table table-striped table-hover table-condensed table-responsive" style="width: auto !important; margin-left: auto; margin-right: auto;">
<caption>
<span id="tab:unnamed-chunk-21"></span>Table 2: In-Sample RMSE for 2020 by State
</caption>
<thead>
<tr>
<th style="text-align:left;">
</th>
<th style="text-align:left;">
State
</th>
<th style="text-align:right;">
RMSE.2020
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;width: 8em; text-align: center;">
Arizona
</td>
<td style="text-align:left;width: 6em; text-align: center;">
Arizona
</td>
<td style="text-align:right;">
0.5894
</td>
</tr>
<tr>
<td style="text-align:left;width: 8em; text-align: center;">
Georgia
</td>
<td style="text-align:left;width: 6em; text-align: center;">
Georgia
</td>
<td style="text-align:right;">
0.1473
</td>
</tr>
<tr>
<td style="text-align:left;width: 8em; text-align: center;">
Michigan
</td>
<td style="text-align:left;width: 6em; text-align: center;">
Michigan
</td>
<td style="text-align:right;">
0.7499
</td>
</tr>
<tr>
<td style="text-align:left;width: 8em; text-align: center;">
Nevada
</td>
<td style="text-align:left;width: 6em; text-align: center;">
Nevada
</td>
<td style="text-align:right;">
0.6348
</td>
</tr>
<tr>
<td style="text-align:left;width: 8em; text-align: center;">
North Carolina
</td>
<td style="text-align:left;width: 6em; text-align: center;">
North Carolina
</td>
<td style="text-align:right;">
0.7515
</td>
</tr>
<tr>
<td style="text-align:left;width: 8em; text-align: center;">
Pennsylvania
</td>
<td style="text-align:left;width: 6em; text-align: center;">
Pennsylvania
</td>
<td style="text-align:right;">
1.5191
</td>
</tr>
<tr>
<td style="text-align:left;width: 8em; text-align: center;">
Wisconsin
</td>
<td style="text-align:left;width: 6em; text-align: center;">
Wisconsin
</td>
<td style="text-align:right;">
1.2928
</td>
</tr>
</tbody>
</table>
<table class="table table-striped table-hover table-condensed table-responsive" style="width: auto !important; margin-left: auto; margin-right: auto;">
<caption>
<span id="tab:unnamed-chunk-22"></span>Table 3: Out-of-Sample RMSE for 2020 by State
</caption>
<thead>
<tr>
<th style="text-align:left;">
</th>
<th style="text-align:left;">
State
</th>
<th style="text-align:right;">
RMSE.2020
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;width: 8em; text-align: center;">
Arizona
</td>
<td style="text-align:left;width: 6em; text-align: center;">
Arizona
</td>
<td style="text-align:right;">
0.2358
</td>
</tr>
<tr>
<td style="text-align:left;width: 8em; text-align: center;">
Georgia
</td>
<td style="text-align:left;width: 6em; text-align: center;">
Georgia
</td>
<td style="text-align:right;">
0.1407
</td>
</tr>
<tr>
<td style="text-align:left;width: 8em; text-align: center;">
Michigan
</td>
<td style="text-align:left;width: 6em; text-align: center;">
Michigan
</td>
<td style="text-align:right;">
0.1871
</td>
</tr>
<tr>
<td style="text-align:left;width: 8em; text-align: center;">
Nevada
</td>
<td style="text-align:left;width: 6em; text-align: center;">
Nevada
</td>
<td style="text-align:right;">
0.1007
</td>
</tr>
<tr>
<td style="text-align:left;width: 8em; text-align: center;">
North Carolina
</td>
<td style="text-align:left;width: 6em; text-align: center;">
North Carolina
</td>
<td style="text-align:right;">
1.6074
</td>
</tr>
<tr>
<td style="text-align:left;width: 8em; text-align: center;">
Pennsylvania
</td>
<td style="text-align:left;width: 6em; text-align: center;">
Pennsylvania
</td>
<td style="text-align:right;">
1.9071
</td>
</tr>
<tr>
<td style="text-align:left;width: 8em; text-align: center;">
Wisconsin
</td>
<td style="text-align:left;width: 6em; text-align: center;">
Wisconsin
</td>
<td style="text-align:right;">
0.1821
</td>
</tr>
</tbody>
</table>

# Ensemble Model Predictions

<table class="table table-striped table-hover table-condensed table-responsive" style="width: auto !important; margin-left: auto; margin-right: auto;">
<caption>
<span id="tab:unnamed-chunk-23"></span>Table 4: Ensemble Model Predicted Vote Share
</caption>
<thead>
<tr>
<th style="text-align:left;">
State
</th>
<th style="text-align:left;">
Margin
</th>
</tr>
</thead>
<tbody>
<tr>
<td style="text-align:left;width: 8em; text-align: center;">
Arizona
</td>
<td style="text-align:left;width: 8em; text-align: center;">
-7.02%
</td>
</tr>
<tr>
<td style="text-align:left;width: 8em; text-align: center;">
Georgia
</td>
<td style="text-align:left;width: 8em; text-align: center;">
-2.52%
</td>
</tr>
<tr>
<td style="text-align:left;width: 8em; text-align: center;">
Michigan
</td>
<td style="text-align:left;width: 8em; text-align: center;">
2.79%
</td>
</tr>
<tr>
<td style="text-align:left;width: 8em; text-align: center;">
Nevada
</td>
<td style="text-align:left;width: 8em; text-align: center;">
3.41%
</td>
</tr>
<tr>
<td style="text-align:left;width: 8em; text-align: center;">
North Carolina
</td>
<td style="text-align:left;width: 8em; text-align: center;">
-1.72%
</td>
</tr>
<tr>
<td style="text-align:left;width: 8em; text-align: center;">
Pennsylvania
</td>
<td style="text-align:left;width: 8em; text-align: center;">
0.03%
</td>
</tr>
<tr>
<td style="text-align:left;width: 8em; text-align: center;">
Wisconsin
</td>
<td style="text-align:left;width: 8em; text-align: center;">
1.83%
</td>
</tr>
</tbody>
</table>
<div class="plotly html-widget html-fill-item" id="htmlwidget-1" style="width:672px;height:480px;"></div>
<script type="application/json" data-for="htmlwidget-1">{"x":{"visdat":{"4a9c1756281":["function () ","plotlyVisDat"]},"cur_data":"4a9c1756281","attrs":{"4a9c1756281":{"locations":{},"locationmode":"USA-states","z":{},"text":{},"hoverinfo":"text","colorscale":[["0","darkred"],["0.5","white"],["1","blue"]],"zmin":-7.5,"zmid":0,"zmax":7.5,"colorbar":{"title":"Dem. Voting Margin (%)"},"alpha_stroke":1,"sizes":[10,100],"spans":[1,20],"type":"choropleth"}},"layout":{"margin":{"b":40,"l":60,"t":25,"r":10},"title":{"text":"2024 Swing State Voting Margins","y":0.94999999999999996,"x":0.5,"xanchor":"center","yanchor":"top"},"geo":{"scope":"usa","projection":{"type":"albers usa"},"showlakes":true,"lakecolor":"rgba(173,216,230,1)","showcountries":false,"showcoastlines":false,"coastlinecolor":"rgba(255,255,255,1)","showframe":false},"scene":{"zaxis":{"title":"Margin"}},"hovermode":"closest","showlegend":false,"legend":{"yanchor":"top","y":0.5}},"source":"A","config":{"modeBarButtonsToAdd":["hoverclosest","hovercompare"],"showSendToCloud":false},"data":[{"colorbar":{"title":"Dem. Voting Margin (%)","ticklen":2,"len":0.5,"lenmode":"fraction","y":1,"yanchor":"top"},"colorscale":[["0","darkred"],["0.5","white"],["1","blue"]],"showscale":true,"locations":["AZ","GA","MI","NV","NC","PA","WI"],"locationmode":"USA-states","z":[-7.024446302939694,-2.5184827592694461,2.7934920971141111,3.4112621178387883,-1.7217337269380835,0.026786108144975174,1.8304330600754923],"text":["State: Arizona <br>Margin: -7.02 %","State: Georgia <br>Margin: -2.52 %","State: Michigan <br>Margin: 2.79 %","State: Nevada <br>Margin: 3.41 %","State: North Carolina <br>Margin: -1.72 %","State: Pennsylvania <br>Margin: 0.03 %","State: Wisconsin <br>Margin: 1.83 %"],"hoverinfo":["text","text","text","text","text","text","text"],"zmin":-7.5,"zmid":0,"zmax":7.5,"type":"choropleth","marker":{"line":{"color":"rgba(31,119,180,1)"}},"frame":null}],"highlight":{"on":"plotly_click","persistent":false,"dynamic":false,"selectize":false,"opacityDim":0.20000000000000001,"selected":{"opacity":1},"debounce":0},"shinyEvents":["plotly_hover","plotly_click","plotly_selected","plotly_relayout","plotly_brushed","plotly_brushing","plotly_clickannotation","plotly_doubleclick","plotly_deselect","plotly_afterplot","plotly_sunburstclick"],"base_url":"https://plot.ly"},"evals":[],"jsHooks":[]}</script>

# Simulations

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-34-1.png" width="672" />

<table class="table table-striped table-hover table-condensed table-responsive" style="width: auto !important; margin-left: auto; margin-right: auto;">
<caption>
<span id="tab:unnamed-chunk-28"></span>Table 5: Simulation Results: Harris and Trump Victory Counts
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
492
</td>
<td style="text-align:right;width: 5em; text-align: center;">
508
</td>
<td style="text-align:left;width: 5em; text-align: center;">
49.2%
</td>
</tr>
</tbody>
</table>

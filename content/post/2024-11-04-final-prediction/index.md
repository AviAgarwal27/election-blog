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

# Model Equations

1.  Model 1:
    $$
    D\_pv2p = \alpha + \beta_1(\text{state}) + \beta_2(\text{D\_pv2p\_lag1}) + \beta_3(\text{D\_pv2p\_lag2}) + \beta_4(\text{updated\_rdpi} \times \text{incumbent\_party}) + \beta_5(\text{dpi\_inflation\_adjusted} \times \text{incumbent\_party}) + \epsilon
    $$

2.  Model 2:
    $$
    D\_pv2p = \alpha + \beta_1(\text{state}) + \beta_2(\text{polling\_trend\_5\_1}) + \beta_3(\text{polling\_trend\_10\_6}) + \beta_4(\text{current\_week}) + \beta_5(\text{support\_DEM\_1}) + \beta_6(\text{support\_DEM\_2}) + \beta_7(\text{support\_DEM\_3}) + \epsilon
    $$

3.  Model 3:
    $$
    D\_pv2p = \alpha + \beta_1(\text{state}) + \beta_2(\text{D\_pv2p\_lag1}) + \beta_3(\text{D\_pv2p\_lag2}) + \beta_4(\text{support\_DEM\_1}) + \beta_5(\text{polling\_trend\_5\_1}) + \beta_6(\text{polling\_trend\_10\_6}) + \beta_7(\text{dpi\_inflation\_adjusted} \times \text{incumbent\_party}) + \beta_8(\text{unemployment\_growth\_quarterly} \times \text{incumbent\_party}) + \beta_9(\text{updated\_rdpi} \times \text{incumbent\_party}) + \epsilon
    $$

# Weights

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
0.0281
</td>
<td style="text-align:right;width: 6em; text-align: center;">
0.9719
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
0.1304
</td>
<td style="text-align:right;width: 6em; text-align: center;">
0.8381
</td>
<td style="text-align:right;width: 6em; text-align: center;">
0.0315
</td>
</tr>
<tr>
<td style="text-align:left;width: 8em; text-align: center;">
Michigan
</td>
<td style="text-align:right;width: 6em; text-align: center;">
0.1293
</td>
<td style="text-align:right;width: 6em; text-align: center;">
0.6102
</td>
<td style="text-align:right;width: 6em; text-align: center;">
0.2604
</td>
</tr>
<tr>
<td style="text-align:left;width: 8em; text-align: center;">
Nevada
</td>
<td style="text-align:right;width: 6em; text-align: center;">
0.1276
</td>
<td style="text-align:right;width: 6em; text-align: center;">
0.7298
</td>
<td style="text-align:right;width: 6em; text-align: center;">
0.1426
</td>
</tr>
<tr>
<td style="text-align:left;width: 8em; text-align: center;">
North Carolina
</td>
<td style="text-align:right;width: 6em; text-align: center;">
0.3955
</td>
<td style="text-align:right;width: 6em; text-align: center;">
0.5703
</td>
<td style="text-align:right;width: 6em; text-align: center;">
0.0342
</td>
</tr>
<tr>
<td style="text-align:left;width: 8em; text-align: center;">
Pennsylvania
</td>
<td style="text-align:right;width: 6em; text-align: center;">
0.0312
</td>
<td style="text-align:right;width: 6em; text-align: center;">
0.9585
</td>
<td style="text-align:right;width: 6em; text-align: center;">
0.0104
</td>
</tr>
<tr>
<td style="text-align:left;width: 8em; text-align: center;">
Wisconsin
</td>
<td style="text-align:right;width: 6em; text-align: center;">
0.1537
</td>
<td style="text-align:right;width: 6em; text-align: center;">
0.6419
</td>
<td style="text-align:right;width: 6em; text-align: center;">
0.2043
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
<td style="text-align:right;width: 6em; text-align: center;">
0.6719
</td>
</tr>
<tr>
<td style="text-align:left;width: 8em; text-align: center;">
Georgia
</td>
<td style="text-align:right;width: 6em; text-align: center;">
0.0435
</td>
</tr>
<tr>
<td style="text-align:left;width: 8em; text-align: center;">
Michigan
</td>
<td style="text-align:right;width: 6em; text-align: center;">
1.5867
</td>
</tr>
<tr>
<td style="text-align:left;width: 8em; text-align: center;">
Nevada
</td>
<td style="text-align:right;width: 6em; text-align: center;">
1.5505
</td>
</tr>
<tr>
<td style="text-align:left;width: 8em; text-align: center;">
North Carolina
</td>
<td style="text-align:right;width: 6em; text-align: center;">
0.5768
</td>
</tr>
<tr>
<td style="text-align:left;width: 8em; text-align: center;">
Pennsylvania
</td>
<td style="text-align:right;width: 6em; text-align: center;">
1.7680
</td>
</tr>
<tr>
<td style="text-align:left;width: 8em; text-align: center;">
Wisconsin
</td>
<td style="text-align:right;width: 6em; text-align: center;">
2.0518
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
<td style="text-align:right;width: 6em; text-align: center;">
0.3713
</td>
</tr>
<tr>
<td style="text-align:left;width: 8em; text-align: center;">
Georgia
</td>
<td style="text-align:right;width: 6em; text-align: center;">
0.2846
</td>
</tr>
<tr>
<td style="text-align:left;width: 8em; text-align: center;">
Michigan
</td>
<td style="text-align:right;width: 6em; text-align: center;">
1.1598
</td>
</tr>
<tr>
<td style="text-align:left;width: 8em; text-align: center;">
Nevada
</td>
<td style="text-align:right;width: 6em; text-align: center;">
1.2268
</td>
</tr>
<tr>
<td style="text-align:left;width: 8em; text-align: center;">
North Carolina
</td>
<td style="text-align:right;width: 6em; text-align: center;">
1.5875
</td>
</tr>
<tr>
<td style="text-align:left;width: 8em; text-align: center;">
Pennsylvania
</td>
<td style="text-align:right;width: 6em; text-align: center;">
2.4631
</td>
</tr>
<tr>
<td style="text-align:left;width: 8em; text-align: center;">
Wisconsin
</td>
<td style="text-align:right;width: 6em; text-align: center;">
1.9281
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
-4.41%
</td>
</tr>
<tr>
<td style="text-align:left;width: 8em; text-align: center;">
Georgia
</td>
<td style="text-align:left;width: 8em; text-align: center;">
-1.53%
</td>
</tr>
<tr>
<td style="text-align:left;width: 8em; text-align: center;">
Michigan
</td>
<td style="text-align:left;width: 8em; text-align: center;">
2.82%
</td>
</tr>
<tr>
<td style="text-align:left;width: 8em; text-align: center;">
Nevada
</td>
<td style="text-align:left;width: 8em; text-align: center;">
3.37%
</td>
</tr>
<tr>
<td style="text-align:left;width: 8em; text-align: center;">
North Carolina
</td>
<td style="text-align:left;width: 8em; text-align: center;">
-1.51%
</td>
</tr>
<tr>
<td style="text-align:left;width: 8em; text-align: center;">
Pennsylvania
</td>
<td style="text-align:left;width: 8em; text-align: center;">
0.61%
</td>
</tr>
<tr>
<td style="text-align:left;width: 8em; text-align: center;">
Wisconsin
</td>
<td style="text-align:left;width: 8em; text-align: center;">
1.38%
</td>
</tr>
</tbody>
</table>
<div class="plotly html-widget html-fill-item" id="htmlwidget-1" style="width:672px;height:480px;"></div>
<script type="application/json" data-for="htmlwidget-1">{"x":{"visdat":{"16c85d2a4ae3":["function () ","plotlyVisDat"]},"cur_data":"16c85d2a4ae3","attrs":{"16c85d2a4ae3":{"locations":{},"locationmode":"USA-states","z":{},"text":{},"hoverinfo":"text","colorscale":[["0","darkred"],["0.5","white"],["1","blue"]],"zmin":-10,"zmid":0,"zmax":10,"colorbar":{"title":"Dem. Voting Margin (%)","y":0.5,"yanchor":"middle"},"alpha_stroke":1,"sizes":[10,100],"spans":[1,20],"type":"choropleth"}},"layout":{"margin":{"b":40,"l":60,"t":25,"r":10},"title":{"text":"2024 Swing State Voting Margins","y":0.94999999999999996,"x":0.5,"xanchor":"center","yanchor":"top"},"geo":{"scope":"usa","projection":{"type":"albers usa"},"showlakes":false,"showcountries":false,"showcoastlines":false,"coastlinecolor":"rgba(255,255,255,1)","showframe":false},"scene":{"zaxis":{"title":"Margin"}},"hovermode":"closest","showlegend":false,"legend":{"yanchor":"top","y":0.5}},"source":"A","config":{"modeBarButtonsToAdd":["hoverclosest","hovercompare"],"showSendToCloud":false},"data":[{"colorbar":{"title":"Dem. Voting Margin (%)","ticklen":2,"y":0.5,"yanchor":"middle","len":0.5,"lenmode":"fraction"},"colorscale":[["0","darkred"],["0.5","white"],["1","blue"]],"showscale":true,"locations":["AZ","GA","MI","NV","NC","PA","WI"],"locationmode":"USA-states","z":[-4.4121567351972715,-1.5341034414037864,2.8235235667392828,3.3705583134253061,-1.5069849367033186,0.60727480942513523,1.3756902964105535],"text":["State: Arizona <br>Margin: -4.41 %","State: Georgia <br>Margin: -1.53 %","State: Michigan <br>Margin: 2.82 %","State: Nevada <br>Margin: 3.37 %","State: North Carolina <br>Margin: -1.51 %","State: Pennsylvania <br>Margin: 0.61 %","State: Wisconsin <br>Margin: 1.38 %"],"hoverinfo":["text","text","text","text","text","text","text"],"zmin":-10,"zmid":0,"zmax":10,"type":"choropleth","marker":{"line":{"color":"rgba(31,119,180,1)"}},"frame":null}],"highlight":{"on":"plotly_click","persistent":false,"dynamic":false,"selectize":false,"opacityDim":0.20000000000000001,"selected":{"opacity":1},"debounce":0},"shinyEvents":["plotly_hover","plotly_click","plotly_selected","plotly_relayout","plotly_brushed","plotly_brushing","plotly_clickannotation","plotly_doubleclick","plotly_deselect","plotly_afterplot","plotly_sunburstclick"],"base_url":"https://plot.ly"},"evals":[],"jsHooks":[]}</script>

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

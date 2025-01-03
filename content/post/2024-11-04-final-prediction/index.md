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

# Introduction

This model aims to predict the outcome of the Electoral College, thereby determining the next President of the United States. Consequently, I chose not to predict the national vote share, as it is not irrelevant to the outcome of the election.

As an aside, I strongly believe the Electoral College should be abolished. If you’re interested in exploring an innovative proposal on this topic, please read [this article I wrote for the Harvard Political Review](https://www.google.com/url?q=https://theharvardpoliticalreview.com/abolishing-the-electoral-college-might-not-be-as-hard-as-you-think/&sa=D&source=docs&ust=1730744938415047&usg=AOvVaw0DxVlAlSrc9iDKDJnC6FvV).

This model is based on the assumption that only the following states are truly competitive: Arizona, Georgia, Michigan, Nevada, North Carolina, Pennsylvania, and Wisconsin. I identified these states as battlegrounds in my [Week \#1 Post](https://www.google.com/url?q=https://aviagarwal27.github.io/election-blog/post/2024/09/09/post-1/&sa=D&source=docs&ust=1730744938419669&usg=AOvVaw396BBePF9Prpw5Quf-SVqp), an assessment shared by other experts such as the [Cook Political Report](https://www.google.com/url?q=https://www.cookpolitical.com/ratings/presidential-race-ratings&sa=D&source=docs&ust=1730744938420324&usg=AOvVaw3bqDvDo0UMv4WgnsBToQEc). Therefore, this model will focus exclusively on predicting the two-party vote share in these seven states, assuming an initial distribution of electoral votes where Harris holds 226 and Trump holds 219.

Given the volume of polls that only display these states as toss-ups, I am confident in this assumption. However, [a recent poll by Selzer & Co.](https://www.google.com/url?q=https://www.economist.com/united-states/2024/11/03/a-much-watched-poll-from-iowa-points-to-a-harris-landslide&sa=D&source=docs&ust=1730744938416006&usg=AOvVaw02ROEOOtCjGOG9ISwsKd7_)—a highly respected pollster—found Harris leading by 3 points in Iowa, a state Trump won by 8 points in 2020. If accurate, this poll could challenge the model’s assumptions and potentially signal a landslide Harris electoral college victory, exceeding the model’s maximum of 319 electoral votes.

# Model Equations

For this model, I wanted to balance the effects of fundamentals and polling based on historical election outcomes to increase the predictive accuracy of my model. Given this, I chose to use a super-learning model ensembling method predicting the expected vote share with three distinct Ordinary Least Square (OLS) models and then combining them using empirically generated weights.

Initially, I had created one set of weights I had used for all the swing states, but I soon realized that having individual weights for each state would lead to lower RMSE. As a result, I chose to loop the swing states and create separate models using Florida as an intercept. Since I created three individual models for each state or 21 models in total, I chose not to include the summaries of the coefficients.

I used data from the 1980 - 2020 elections to train the models, the largest range where all data was available.

**Model 1:**

$$
`\begin{aligned}
D\_pv2p = & \, \alpha + \beta_1(\text{state}) + \beta_2(\text{D\_pv2p\_lag1}) + \beta_3(\text{D\_pv2p\_lag2}) \\
& + \beta_4(\text{updated\_rdpi} \times \text{incumbent\_party}) + \beta_5(\text{dpi\_inflation\_adjusted} \times \text{incumbent\_party}) + \epsilon
\end{aligned}`
  $$

The first model uses only fundamental predictors, including lagged Democratic two-party vote shares from 2016 and 2020 and two measures of Real Disposable Personal Income (RDPI).

The first RDPI measure, “updated RDPI,” is the most recent national RDPI data available, covering June 1 to September 1 of the election year (between Q2 and Q3). This data is sourced from [the Federal Reserve Bank of St. Louis](https://www.google.com/url?q=https://fred.stlouisfed.org/&sa=D&source=docs&ust=1730744938416565&usg=AOvVaw25h3mQydPwVYzl7WAQtJHK). To avoid the economic impact of the COVID-19 pandemic on 2020 data, I used the [Congressional Budget Office](https://www.google.com/url?q=https://www.cbo.gov/data/budget-economic-data&sa=D&source=docs&ust=1730744938417175&usg=AOvVaw2FKA59eQxjB1eMN60eNEcj)’s 2020 RDPI growth projections rather than actual values.

The second RDPI measure, “DPI inflation-adjusted,” uses state-level disposable income data from the [Bureau of Economic Analysis](https://www.google.com/url?q=https://www.bea.gov/data&sa=D&source=docs&ust=1730744938417709&usg=AOvVaw0qAVTfeqQsGNBAii-wnssN), adjusted for inflation with World Bank data. Since quarterly state-level DPI is unavailable for 2024, I used data from the year preceding the election.

Both economic variables are modeled as interaction effects, with a binary variable indicating the incumbent party. Including both state and national predictors helps capture voter perceptions of national economic conditions and personal financial situations.

**Model 2:**

$$
`\begin{aligned}
D\_pv2p = & \, \alpha + \beta_1(\text{state}) + \beta_2(\text{polling\_trend\_5\_1}) + \beta_3(\text{polling\_trend\_10\_6}) \\
& + \beta_4(\text{current\_week}) + \beta_5(\text{support\_DEM\_1}) + \beta_6(\text{support\_DEM\_2}) + \beta_7(\text{support\_DEM\_3}) + \epsilon
\end{aligned}`
  $$

The second model relies solely on various polling-based covariates, all sourced from [FiveThirtyEight](https://www.google.com/url?q=https://projects.fivethirtyeight.com/polls/&sa=D&source=docs&ust=1730744938418979&usg=AOvVaw3PPYvini-EY-MVTfSMOHoj) with their poll weighting applied. The data is state-level and grouped by the weeks remaining before the election.

The first three polling variables—Polling Trend 5-1, Polling Trend 6-10, and Current Week—are measured in poll margin (Democratic candidate polling minus Republican candidate polling). Polling Trend 5-1 captures the change in margin from five weeks to one week before the election, indicating whether a candidate is gaining or losing ground close to Election Day. Polling Trend 6-10 reflects changes from six to ten weeks out, while Current Week is the margin from one week before the election.

The last three variables—Support Dem. 1, Support Dem. 2, and Support Dem. 3—represent the average Democratic candidate polling one, two, and three weeks before the election, respectively. I chose to include these covariates to capture additional shifts in Democratic candidate support as the election approaches.

**Model 3:**

$$
`\begin{aligned}
D\_pv2p = & \, \alpha + \beta_1(\text{state}) + \beta_2(\text{D\_pv2p\_lag1}) + \beta_3(\text{D\_pv2p\_lag2}) + \beta_4(\text{support\_DEM\_1}) \\
& + \beta_5(\text{polling\_trend\_5\_1}) + \beta_6(\text{polling\_trend\_10\_6}) + \beta_7(\text{dpi\_inflation\_adjusted} \times \text{incumbent\_party}) \\
& + \beta_8(\text{unemployment\_growth\_quarterly} \times \text{incumbent\_party}) + \beta_9(\text{updated\_rdpi} \times \text{incumbent\_party}) + \epsilon
\end{aligned}`
  $$

The third model combines Models 1 and 2 covariates with the addition of national-level Q2 unemployment growth from the Fed. in St. Louis, which is included as an interaction effect with the incumbent party. Including this factor reduced the RMSE, which led me to incorporate it in this combined model.

# Weights

To generate weights without excluding election cycles and reduce overfitting concerns from training on a single election, I used a Leave-One-Out scheme where I trained all three models, excluding one election cycle at a time, and then predicted the results for the excluded election.

After repeating this process for each election in the dataset, I performed a constrained optimization with a Beta between 0 and 1 using the three predicted values (each from one of the above models) and the actual vote share to generate the individual state weights. Table 1 below displays the resulting weights for each state.

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

The second model, which relies solely on polling data, consistently receives the highest weight. In states like Arizona and Pennsylvania, its weight comprises nearly the entire model, while in Michigan and Nevada, it is slightly above 0.5.

The fundamental model is weighted just above 0.1 in four swing states, reaching nearly 0.4 in North Carolina and dips to a low in Pennsylvania and Arizona. Model 3, the combined model, shows the greatest variance, with weights close to zero in some states and over 0.2 in others. Overall, the weights clearly vary significantly depending on the state.

# RMSE (In-sample & Out-of-sample)

To test the predictive accuracy of this model, I calculated both in-sample and out-of-sample root mean square error (RMSE) based on the 2020 election. For the in-sample RMSE, I included 2020 data in the training set while using the same weights derived from all prior elections. For the out-of-sample RMSE, I excluded the 2020 data from the training set, but still applied the same weights. Although this means the out-of-sample RMSE reflects weights partially trained on 2020 data, removing this data would be challenging given the method I used for generating the weights, and the impact of any single election on weight determination is minimal.

The in-sample RMSE results, in Table 2, were encouraging, ranging from a low of 0.04 in Georgia to a high of 2.05 in Wisconsin, indicating that the maximum prediction error was within 2 percentage points—enough to potentially swing a state. Most of the error came from overestimating the Democratic vote share.

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
<th style="text-align:right;">
Predicted.Vote.Share
</th>
<th style="text-align:right;">
True.Vote.Share
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
<td style="text-align:right;width: 8em; text-align: center;">
49.4850
</td>
<td style="text-align:right;width: 8em; text-align: center;">
50.1568
</td>
</tr>
<tr>
<td style="text-align:left;width: 8em; text-align: center;">
Georgia
</td>
<td style="text-align:right;width: 6em; text-align: center;">
0.0435
</td>
<td style="text-align:right;width: 8em; text-align: center;">
50.1629
</td>
<td style="text-align:right;width: 8em; text-align: center;">
50.1193
</td>
</tr>
<tr>
<td style="text-align:left;width: 8em; text-align: center;">
Michigan
</td>
<td style="text-align:right;width: 6em; text-align: center;">
1.5867
</td>
<td style="text-align:right;width: 8em; text-align: center;">
53.0003
</td>
<td style="text-align:right;width: 8em; text-align: center;">
51.4136
</td>
</tr>
<tr>
<td style="text-align:left;width: 8em; text-align: center;">
Nevada
</td>
<td style="text-align:right;width: 6em; text-align: center;">
1.5505
</td>
<td style="text-align:right;width: 8em; text-align: center;">
52.7736
</td>
<td style="text-align:right;width: 8em; text-align: center;">
51.2231
</td>
</tr>
<tr>
<td style="text-align:left;width: 8em; text-align: center;">
North Carolina
</td>
<td style="text-align:right;width: 6em; text-align: center;">
0.5768
</td>
<td style="text-align:right;width: 8em; text-align: center;">
48.7390
</td>
<td style="text-align:right;width: 8em; text-align: center;">
49.3158
</td>
</tr>
<tr>
<td style="text-align:left;width: 8em; text-align: center;">
Pennsylvania
</td>
<td style="text-align:right;width: 6em; text-align: center;">
1.7680
</td>
<td style="text-align:right;width: 8em; text-align: center;">
52.3572
</td>
<td style="text-align:right;width: 8em; text-align: center;">
50.5892
</td>
</tr>
<tr>
<td style="text-align:left;width: 8em; text-align: center;">
Wisconsin
</td>
<td style="text-align:right;width: 6em; text-align: center;">
2.0518
</td>
<td style="text-align:right;width: 8em; text-align: center;">
52.3709
</td>
<td style="text-align:right;width: 8em; text-align: center;">
50.3191
</td>
</tr>
</tbody>
</table>

The out-of-sample RMSE results, while expectedly higher, remained strong. The highest RMSE was in Pennsylvania at 2.46, due to a significant overestimation of the Democratic vote share. This is likely due to the model’s reliance on polling data for Pennsylvania, as shown in Table 1, where polling errors led to an overestimate.

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
<th style="text-align:right;">
Predicted.Vote.Share
</th>
<th style="text-align:right;">
True.Vote.Share
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
<td style="text-align:right;width: 8em; text-align: center;">
49.7855
</td>
<td style="text-align:right;width: 8em; text-align: center;">
50.1568
</td>
</tr>
<tr>
<td style="text-align:left;width: 8em; text-align: center;">
Georgia
</td>
<td style="text-align:right;width: 6em; text-align: center;">
0.2846
</td>
<td style="text-align:right;width: 8em; text-align: center;">
49.8347
</td>
<td style="text-align:right;width: 8em; text-align: center;">
50.1193
</td>
</tr>
<tr>
<td style="text-align:left;width: 8em; text-align: center;">
Michigan
</td>
<td style="text-align:right;width: 6em; text-align: center;">
1.1598
</td>
<td style="text-align:right;width: 8em; text-align: center;">
52.5734
</td>
<td style="text-align:right;width: 8em; text-align: center;">
51.4136
</td>
</tr>
<tr>
<td style="text-align:left;width: 8em; text-align: center;">
Nevada
</td>
<td style="text-align:right;width: 6em; text-align: center;">
1.2268
</td>
<td style="text-align:right;width: 8em; text-align: center;">
52.4499
</td>
<td style="text-align:right;width: 8em; text-align: center;">
51.2231
</td>
</tr>
<tr>
<td style="text-align:left;width: 8em; text-align: center;">
North Carolina
</td>
<td style="text-align:right;width: 6em; text-align: center;">
1.5875
</td>
<td style="text-align:right;width: 8em; text-align: center;">
47.7283
</td>
<td style="text-align:right;width: 8em; text-align: center;">
49.3158
</td>
</tr>
<tr>
<td style="text-align:left;width: 8em; text-align: center;">
Pennsylvania
</td>
<td style="text-align:right;width: 6em; text-align: center;">
2.4631
</td>
<td style="text-align:right;width: 8em; text-align: center;">
53.0523
</td>
<td style="text-align:right;width: 8em; text-align: center;">
50.5892
</td>
</tr>
<tr>
<td style="text-align:left;width: 8em; text-align: center;">
Wisconsin
</td>
<td style="text-align:right;width: 6em; text-align: center;">
1.9281
</td>
<td style="text-align:right;width: 8em; text-align: center;">
52.2472
</td>
<td style="text-align:right;width: 8em; text-align: center;">
50.3191
</td>
</tr>
</tbody>
</table>

# Ensemble Model Predictions

Now, with the preamble complete, we can finally reach the main event: Who will win the 2024 Presidential Election?

Using data from 2024, my model predicts that Harris will narrowly win in Pennsylvania and Wisconsin, with more substantial leads in Michigan and Nevada—enough to reach 270 electoral votes and become **America’s 47th President**. She is projected to lose Arizona by a large margin, with close losses in both North Carolina and Georgia, finishing with 276 electoral votes to Trump’s 262.

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

You can view the margins in Table 4 above or by hovering over the states in the interactive map below .

<div class="plotly html-widget html-fill-item" id="htmlwidget-1" style="width:672px;height:480px;"></div>
<script type="application/json" data-for="htmlwidget-1">{"x":{"visdat":{"5ff847ef5996":["function () ","plotlyVisDat"]},"cur_data":"5ff847ef5996","attrs":{"5ff847ef5996":{"locations":{},"locationmode":"USA-states","z":{},"text":{},"hoverinfo":"text","colorscale":[["0","darkred"],["0.5","white"],["1","blue"]],"zmin":-10,"zmid":0,"zmax":10,"colorbar":{"title":"Dem. Voting Margin (%)","y":0.5,"yanchor":"middle"},"alpha_stroke":1,"sizes":[10,100],"spans":[1,20],"type":"choropleth"}},"layout":{"margin":{"b":40,"l":60,"t":25,"r":10},"title":{"text":"2024 Swing State Voting Margins","y":0.94999999999999996,"x":0.5,"xanchor":"center","yanchor":"top"},"geo":{"scope":"usa","projection":{"type":"albers usa"},"showlakes":false,"showcountries":false,"showcoastlines":false,"coastlinecolor":"rgba(255,255,255,1)","showframe":false},"scene":{"zaxis":{"title":"Margin"}},"hovermode":"closest","showlegend":false,"legend":{"yanchor":"top","y":0.5}},"source":"A","config":{"modeBarButtonsToAdd":["hoverclosest","hovercompare"],"showSendToCloud":false},"data":[{"colorbar":{"title":"Dem. Voting Margin (%)","ticklen":2,"y":0.5,"yanchor":"middle","len":0.5,"lenmode":"fraction"},"colorscale":[["0","darkred"],["0.5","white"],["1","blue"]],"showscale":true,"locations":["AZ","GA","MI","NV","NC","PA","WI"],"locationmode":"USA-states","z":[-4.4121567351972715,-1.5341034414037864,2.8235235667392828,3.3705583134253061,-1.5069849367033186,0.60727480942513523,1.3756902964105535],"text":["State: Arizona <br>Margin: -4.41 %","State: Georgia <br>Margin: -1.53 %","State: Michigan <br>Margin: 2.82 %","State: Nevada <br>Margin: 3.37 %","State: North Carolina <br>Margin: -1.51 %","State: Pennsylvania <br>Margin: 0.61 %","State: Wisconsin <br>Margin: 1.38 %"],"hoverinfo":["text","text","text","text","text","text","text"],"zmin":-10,"zmid":0,"zmax":10,"type":"choropleth","marker":{"line":{"color":"rgba(31,119,180,1)"}},"frame":null}],"highlight":{"on":"plotly_click","persistent":false,"dynamic":false,"selectize":false,"opacityDim":0.20000000000000001,"selected":{"opacity":1},"debounce":0},"shinyEvents":["plotly_hover","plotly_click","plotly_selected","plotly_relayout","plotly_brushed","plotly_brushing","plotly_clickannotation","plotly_doubleclick","plotly_deselect","plotly_afterplot","plotly_sunburstclick"],"base_url":"https://plot.ly"},"evals":[],"jsHooks":[]}</script>

# Simulations

However, even if my model were 100% accurate, these predictions would only hold if polling error were zero. As we saw in 2016 and 2020, polling errors can be significant, sometimes even reversing expectations entirely, as in 2016.

To account for this, I ran 1,000 simulations of all polling-based covariates, using a normal distribution centered around the mean with a standard deviation of 3. I then predicted Harris’s total electoral vote share in all 1,000 simulations to estimate her likelihood of winning the election.

The plot below represents the distribution of these simulations, with each dot representing five simulations. Harris victories are shown in blue, while losses are shown in red. As you can see, the majority of simulations predict a Harris victory, with the most common outcome being Harris achieving 276 electoral votes, the scenario predicted above. As expected, the most common loss scenario is when Harris earns only 257 electoral votes, primarily from losing Pennsylvania.

Table 5 below shows that, out of the 1,000 simulations, Harris wins in 589 and loses in 411.

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

# Conclusion & Acknowledgements

Overall, my model suggests that Harris has a **slightly higher chance of winning the election**, but ultimately, the race is still a toss-up and far too close to call.

In closing, I would like to acknowledge the exceptional faculty and course staff of Gov 1347: Election Analytics, without whose teaching and guidance this project would not have been possible: Professor Ryan Enos, Teaching Fellow Matthew Dardet, and Course Assistants Ethan Jasney and Yusuf Mian.

Thank you for reading, and I hope you enjoyed this analysis! If you have any questions or feedback, please feel free to reach out to me at *aviagarwal@college.harvard.edu*.

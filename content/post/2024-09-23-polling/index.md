---
title: 'Post #3: Polling'
author: Avi Agarwal
date: '2024-09-23'
slug: post-3-polling
categories: []
tags: []
---





































# Introduction

For many, polling is considered the foundation of electoral predictions. However, its predictive power may be significantly less reliable than expected. In this week’s post, I explore this by creating a few predictive models for national and state races using only polling data, and I analyze the results.

Despite polling’s prominence, the circumstances surrounding this election make data particularly limited. Since President Biden exited the race in mid-July, there are only eight weeks of polling data available that directly compares the current two candidates. This data spans from 15 weeks before the election to 7 weeks prior, which presents some challenges.

When it comes to incorporating polling into a regression model, there are a few different approaches to consider. The simplest, though likely the least accurate, is to average all available data for a candidate over a specific period. To make things more complex, one could treat each week as a separate variable in a regression and then apply a regularization method to exclude certain weeks by minimizing the mean-squared error. While this method might be preferable for predicting national vote share, it presents challenges at the state level. State-level races require weekly polling in each state, and that kind of data simply doesn't exist. As a result, I had to rely on the simpler method of averaging polling support over a period for my models. Another potential approach is to manually weight each week's polling data, with more weight given to polls conducted closer to the election. However, determining the correct weights would require extensive analysis to avoid arbitrary decisions.

# National Model

As mentioned earlier, this model uses OLS to measure the relationship between the average polling support for each party’s candidate (from 1968 to 2020) and the eventual two-party vote share in that election. The polling data spans from 15 weeks before the election to 7 weeks prior.

I created separate models for each party due to how polling data is structured. Each poll essentially asks whether a voter supports a particular candidate, but a lack of support for one candidate does not necessarily indicate support for the opposing party. It simply means the voter isn't committed to the candidate in question. Therefore, it's not accurate to only focus on polling responses about one party’s candidate when predicting the election outcome.


Table: <span id="tab:unnamed-chunk-5"></span>Table 1: National Polling Model Coefficients, P-Values, and R-Squared for Republicans and Democrats

|   Party    | Polling Coefficient |  P-Value  | R-Squared |
|:----------:|:-------------------:|:---------:|:---------:|
| Republican |      0.6699376      | 0.0001198 | 0.7218553 |
|  Democrat  |      0.5008233      | 0.0059140 | 0.4814119 |

As shown in the table above, both models are statistically significant based on their p-values at the 0.05 level. However, the R-squared value and the coefficient for the Republican polling vote share model are much higher than those for the Democratic model. Typically, this indicates that higher national polling in this period for Republicans is more strongly associated with a higher eventual two-party vote share in the election. This finding aligns with recent elections, where polls have tended to overestimate how well Democratic candidates would perform compared to their actual results. 



Table: <span id="tab:unnamed-chunk-6"></span>Table 2: 2024 National Predicted 2-Party Vote Share

|   Party    | Predicted 2PV (2024) | Lower 95% Interval | Upper 95% Interval |
|:----------:|:--------------------:|:------------------:|:------------------:|
| Republican |       50.88708       |      44.78523      |      56.98894      |
|  Democrat  |       50.23635       |      41.87147      |      58.60124      |

Interestingly, both models predict a vote share greater than 50% for their respective parties, which is, of course, impossible since the total must sum to 100. This is likely due to the election and polling being extremely close. As I mentioned earlier, polls only measure whether a candidate is supported, without accounting for voters who are uncommitted or plan to vote for a third party. Typically, polling support of around 47-48% correlates to an eventual vote share of around 51-52%, as 5-10% of voters often remain undecided or support third-party candidates. In this case, it seems that, according to the 2024 polls, more voters are committed to one of the two main party candidates than usual. This could explain why the models predict that both candidates receiving more than 50% of the vote, an anomaly that reflects the tight race and polarized electorate. 

Lastly, while both candidates receive more than 50% of the vote, the predicted vote share for the Republican candidate is 0.6 percentage points higher than for the Democratic candidate. This might seem surprising, given that most polls favor Harris in a contest against Trump. However, when you account for the coefficient showing Republican candidates tend to outperform their poll standings, the results make more sense. Historically, Democrats have underperformed their poll averages from weeks 15 to 7, while Republicans have exceeded theirs. As a result, despite Harris leading in the polls, Trump is still predicted to gain more of the vote share.

# State Models

While predicting the National Two-Party Vote Share is interesting, that particular metric doesn't determine the winner of the election. Instead, the outcome will likely hinge on the winners of the seven key swing states I identified in my first post:

- North Carolina
- Georgia
- Arizona
- Nevada
- Pennsylvania
- Michigan
- Wisconsin

To assess whether polls could help predict the outcome of these states in the 2024 election, I replicated the methodology above, but individually for each state. However, the amount of historical polling data available for each state is much more limited. For some states, like Nevada, no data was available for an entire election, or results were determined by a single poll. As a result, many of the models were not statistically significant, as shown in the tables below.



Table: <span id="tab:unnamed-chunk-11"></span>Table 3: State Polling Model Coefficients, P-Values, and R-Squared for Democratic Candidates

|     State      | Polling Coefficient |  P-Value  | R-Squared |
|:--------------:|:-------------------:|:---------:|:---------:|
|    Arizona     |      0.0675212      | 0.7864333 | 0.0111972 |
|    Georgia     |     -0.0422767      | 0.8792238 | 0.0041723 |
|    Michigan    |      0.2908922      | 0.1325988 | 0.2114132 |
| North Carolina |      0.8065565      | 0.0005226 | 0.7158211 |
|  Pennsylvania  |     -0.1412926      | 0.3147346 | 0.1670427 |
|     Nevada     |      0.6011793      | 0.2791756 | 0.1908194 |
|   Wisconsin    |      0.2237993      | 0.0650050 | 0.3635602 |


Table: <span id="tab:unnamed-chunk-12"></span>Table 4: State Polling Model Coefficients, P-Values, and R-Squared for Republican Candidates

|     State      | Polling Coefficient |  P-Value  | R-Squared |
|:--------------:|:-------------------:|:---------:|:---------:|
|    Arizona     |      0.3977551      | 0.0241515 | 0.5397860 |
|    Georgia     |      0.4160517      | 0.0247965 | 0.5959767 |
|    Michigan    |      0.1785548      | 0.4191225 | 0.0662982 |
| North Carolina |      0.5414656      | 0.0009602 | 0.6803417 |
|  Pennsylvania  |      0.2938137      | 0.1202547 | 0.3532072 |
|     Nevada     |      0.2291605      | 0.7357058 | 0.0204175 |
|   Wisconsin    |      0.0970018      | 0.6602218 | 0.0253794 |

For the Democratic models, only two states passed the statistical significance test at the 0.1 level: Wisconsin and North Carolina. Both had numerous polls for every election in the dataset, which explains why a predictive model could be developed. For the Republican models, only three state models are passed the same test and are worth considering: North Carolina, Arizona, and Georgia.


Table: <span id="tab:unnamed-chunk-16"></span>Table 5: 2024 Democratic Predicted 2-Party Vote Share

|     State      | Predicted 2PV (Democratic) | Lower 95% Interval | Upper 95% Interval |
|:--------------:|:--------------------------:|:------------------:|:------------------:|
| North Carolina |          48.87390          |      40.67340      |      57.07439      |
|   Wisconsin    |          52.28988          |      46.16889      |      58.41087      |


Table: <span id="tab:unnamed-chunk-15"></span>Table 6: 2024 Republican Predicted 2-Party Vote Share

|     State      | Predicted 2PV (Republican) | Lower 95% Interval | Upper 95% Interval |
|:--------------:|:--------------------------:|:------------------:|:------------------:|
|    Arizona     |          53.59233          |      47.18375      |      60.00090      |
|    Georgia     |          52.51831          |      47.06603      |      57.97059      |
| North Carolina |          54.15122          |      45.64429      |      62.65815      |

Given these results, I chose to create predictive models only for those that were statistically significant. Both models predict a Republican victory in North Carolina. Additionally, the Republican model forecasts wins in Arizona and Georgia, while the Democratic model predicts a Democratic win in Wisconsin.

# Concluding Thoughts

Overall, while state polling provides valuable granularity, the limited amount of data makes predicting outcomes much harder compared to national statistics.

As for polling in general, I believe the same conclusion applies as we discussed last week regarding economic factors: while polling can be a decent standalone predictor, especially as data gets closer to election day, it is most accurate when combined with other factors.

---
title: 'Week #6: Improving Electoral College Model'
author: 'Avi '
date: '2024-10-14'
slug: week-6-improving-model-spending
categories: []
tags: []
---













































```r
swing_map_data <- as.data.frame(elec_college_results_dems)


swing_states_data_dems <- data.frame(
  state = swing_state_data_test$state,
  margin = swing_map_data$fit)
```



```r
swing_state_data_dems <- swing_states_data_dems %>%
  mutate(state = tolower(state))

us_states <- map_data("state")

swing_map_data <- us_states %>%
  left_join(swing_state_data_dems, by = c("region" = "state"))


map <- ggplot(data = swing_map_data, aes(x = long, y = lat, group = group, fill = margin)) +
  geom_polygon(color = "white") +
  scale_fill_gradient2(low = "darkred", mid = "white", high = "darkblue", midpoint = 50, 
                       name = "Dem. Voting Margin (%)") +
  theme_minimal() +
  coord_fixed(1.3) +
  labs(title = "2024 Swing State Voting Margins",
       subtitle = "Shaded by predicted Democratic (blue) or Republican (red) vote margins") +
  theme(
    axis.line = element_blank(),        # Remove axis lines
    axis.text = element_blank(),        # Remove axis text
    axis.ticks = element_blank(),       # Remove axis ticks
    axis.title = element_blank(),       # Remove axis titles
    panel.grid = element_blank()        # Remove grid lines
  )
```


# Introduction

As surprising as it might seem, we are less than 22 days away from the 2024 Election Day. As a result, this week, I focused solely on refining my electoral college prediction mode rather than adding any new predictors or techniques. This allowed me to make several substantial improvements to my model that will increase predictive potential. 

# Polling

I have adjusted how I incorporate polling into my models each week and have finally settled on a preferred method. Due to the last-minute candidate switch, one recurring challenge is the limited number of weeks with polling data for this election. This makes it difficult to eliminate any weeks of polling data through regularization methods like elastic net. Furthermore, modeling state-level predictors requires more historical data to apply the method to all the swing states. However, simply using an average removes the influence of polling trends on a candidate’s performance over time. While a weighted average could be helpful, it involves assigning arbitrary weights, which can lead to overfitting issues, like in week 4. As a result, I decided to use three distinct polling-based covariates in my model.

The first covariate is an average of all the weeks of polling between Harris and Trump, providing a baseline of predicted support for each candidate. The other two are trend indicators that measure changes in support over time. One measures the difference in support between 15 weeks and 9 weeks remaining, while the second measures from 8 weeks to 4 weeks remaining. This approach allows me to utilize the limited polling data while giving more weight to recent polls and accounting for trends that may influence vote share over time. Lastly, to maintain a complete dataset for each week, if no polling data was available for a specific week, I carried over the data from the nearest available poll to simulate the presence of data. I preferred this method over using historical data for imputation, as polling averages can vary significantly between elections due to factors like strong third-party candidates and name recognition.

# Economic Fundamentals

I believe both national and state-level economic factors are essential for determining state-level predictions. I only used national economic factors in my previous models, but I corrected that for this week. Unfortunately, robust state-level economic indicators are not widely available. No historical quarterly RDPI growth data is available at the state level, so I had to use the Bureau of Economic Analysis measure of annual personal income growth instead. Since no yearly data is available for 2024, I used the overall increase from the previous election year. For example, for 2020, I used the increase in 2019, and so on.

This data was not adjusted for inflation, so I attempted to find each state's Consumer Price Index increase by year. However, that data was also unavailable, so I used a national measure from the World Bank instead. While this means the estimates are not entirely accurate, inflation rates rarely vary drastically by state, so I was comfortable using it. Since I was using data from the preceding year, I also included the national Q2 RDPI increase, which refers to a separate period, meaning multicollinearity should not be an issue.

# Performance of Adjusted Models

In addition to the new covariates, I retained the incumbent party variable, reflecting how economic fundamentals should influence the candidate's performance. I slightly adjusted the regression format by excluding an intercept term, focusing solely on the direct effects of the swing state covariates without a reference category. As a result, the R-squared is exceptionally high, making it an unreliable measure of the model's predictive quality.

Instead, I calculated the in-sample MSE, 0.0554, or 5.54 percentage points. While still somewhat high, it is reasonable compared to other state-level models. It represents a significant improvement from last week’s model, which had an in-sample MSE of about 10.5 percentage points.

<table style="border-collapse:collapse; border:none;">
<caption style="font-weight: bold; text-align:left;">Linear Regression Model for Democrat Two-Party Vote Share
(In-sample MSE: 5.5428 )</caption>
<tr>
<th style="border-top: double; text-align:center; font-style:normal; font-weight:bold; padding:0.2cm;  text-align:left; ">&nbsp;</th>
<th colspan="4" style="border-top: double; text-align:center; font-style:normal; font-weight:bold; padding:0.2cm; ">Democrat Two-Party Vote Share</th>
</tr>
<tr>
<td style=" text-align:center; border-bottom:1px solid; font-style:italic; font-weight:normal;  text-align:left; ">Predictors</td>
<td style=" text-align:center; border-bottom:1px solid; font-style:italic; font-weight:normal;  ">Estimates</td>
<td style=" text-align:center; border-bottom:1px solid; font-style:italic; font-weight:normal;  ">std. Error</td>
<td style=" text-align:center; border-bottom:1px solid; font-style:italic; font-weight:normal;  ">CI</td>
<td style=" text-align:center; border-bottom:1px solid; font-style:italic; font-weight:normal;  ">p</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">Polling Trend (Weeks 8-4)</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">0.90</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">0.15</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">0.60&nbsp;&ndash;&nbsp;1.19</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  "><strong>&lt;0.001</strong></td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">Polling Trend (Weeks 12-8)</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">0.23</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">0.17</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">&#45;0.11&nbsp;&ndash;&nbsp;0.58</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">0.182</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">Average Polling</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">0.45</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">0.11</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">0.22&nbsp;&ndash;&nbsp;0.67</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  "><strong>&lt;0.001</strong></td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">Incumbent Party</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">&#45;0.07</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">0.89</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">&#45;1.87&nbsp;&ndash;&nbsp;1.73</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">0.936</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">DPI Inflation Adjusted</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">&#45;0.10</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">0.25</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">&#45;0.60&nbsp;&ndash;&nbsp;0.40</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">0.694</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">RDPI Growth Quarterly</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">&#45;0.03</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">0.03</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">&#45;0.09&nbsp;&ndash;&nbsp;0.04</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">0.457</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">Arizona</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">28.41</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">4.35</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">19.67&nbsp;&ndash;&nbsp;37.16</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  "><strong>&lt;0.001</strong></td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">Georgia</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">28.87</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">4.48</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">19.86&nbsp;&ndash;&nbsp;37.88</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  "><strong>&lt;0.001</strong></td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">Michigan</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">31.02</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">4.97</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">21.03&nbsp;&ndash;&nbsp;41.01</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  "><strong>&lt;0.001</strong></td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">Nevada</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">30.42</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">4.72</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">20.92&nbsp;&ndash;&nbsp;39.91</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  "><strong>&lt;0.001</strong></td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">North Carolina</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">27.21</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">4.73</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">17.70&nbsp;&ndash;&nbsp;36.73</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  "><strong>&lt;0.001</strong></td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">Wisconsin</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">31.79</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">5.10</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">21.52&nbsp;&ndash;&nbsp;42.05</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  "><strong>&lt;0.001</strong></td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">Pennsylvania</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">31.36</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">5.01</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">21.29&nbsp;&ndash;&nbsp;41.43</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  "><strong>&lt;0.001</strong></td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; padding-top:0.1cm; padding-bottom:0.1cm; border-top:1px solid;">Observations</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; padding-top:0.1cm; padding-bottom:0.1cm; text-align:left; border-top:1px solid;" colspan="4">60</td>
</tr>

</table>


Using this model for predictions, Harris is forecasted to win Michigan, Wisconsin, Pennsylvania, and Nevada, while Trump is predicted to win North Carolina, Arizona, and, narrowly, Georgia. This would result in a final electoral vote tally of 276 for Harris and 262 for Trump, leading to a narrow Harris victory.

<table style="border-collapse:collapse; border:none;">
<caption style="font-weight: bold; text-align:left;">2024 Democrat Two-Party Vote Share Predictions in Swing States</caption>
<tr>
<th style="border-top: double; text-align:center; font-style:italic; font-weight:normal; padding:0.2cm; border-bottom:1px solid black; text-align:left; ">state</th>
<th style="border-top: double; text-align:center; font-style:italic; font-weight:normal; padding:0.2cm; border-bottom:1px solid black; ">Prediction</th>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">Arizona</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">48.92% ± 3.14%</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">Georgia</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">49.61% ± 3.07%</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">Michigan</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">52.34% ± 2.99%</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">Nevada</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">51.65% ± 3.07%</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">North Carolina</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">47.84% ± 2.97%</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">Pennsylvania</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">52.61% ± 2.98%</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; border-bottom: double; ">Wisconsin</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; border-bottom: double; ">52.98% ± 2.94%</td>
</tr>
</table>

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-26-1.png" width="672" />

# Future Improvements

While this model shows significant improvement from last week, I plan to test several changes in the coming weeks to enhance its accuracy. I intend to experiment with an elastic net model using imputed data to see if that offers a better method for incorporating polling data. I will also explore modeling various economic fundamentals to create a more nuanced measure of economic effects in this election.

While campaign fundraising is a useful indicator of public support, strong data for 2024 are not yet available, making it difficult to make meaningful predictions in this area. However, I may also attempt to incorporate it into the model next week.






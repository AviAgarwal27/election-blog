---
title: 'Post #5: State Level Predictions'
author: Avi Agarwal
date: '2024-10-07'
slug: post-5-state-level-predictions
categories: []
tags: []
---
























```r
swing_states <- c("Arizona", "Georgia", "Michigan", "Nevada", "North Carolina", "Pennsylvania", "Wisconsin")
swing_state_polls <- read_csv("state_polls_1968-2024.csv") |>
  filter(state %in% swing_states & weeks_left < 15 & weeks_left >= 5 & party == "DEM") |>
  group_by(year, state) |>
  summarize(avg_poll_14_9 = mean(poll_support[weeks_left <= 14 & weeks_left >= 9]),
    avg_poll_8_5 = mean(poll_support[weeks_left < 9 & weeks_left >= 5]))
```

```
## Rows: 205100 Columns: 9
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr  (3): state, party, candidate
## dbl  (4): year, weeks_left, days_left, poll_support
## lgl  (1): before_convention
## date (1): poll_date
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
## `summarise()` has grouped output by 'year'. You can override using the `.groups` argument.
```













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
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">39.32</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">0.84</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">37.42&nbsp;&ndash;&nbsp;41.22</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  "><strong>&lt;0.001</strong></td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">weighted_avg_poll</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">0.20</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">0.01</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">0.17&nbsp;&ndash;&nbsp;0.23</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  "><strong>&lt;0.001</strong></td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">RDPI_growth_quarterly</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">0.18</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">0.12</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">&#45;0.08&nbsp;&ndash;&nbsp;0.44</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">0.149</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">incumbent_party</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">1.02</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">0.72</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">&#45;0.61&nbsp;&ndash;&nbsp;2.66</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">0.192</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; padding-top:0.1cm; padding-bottom:0.1cm; border-top:1px solid;">Observations</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; padding-top:0.1cm; padding-bottom:0.1cm; text-align:left; border-top:1px solid;" colspan="4">13</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; padding-top:0.1cm; padding-bottom:0.1cm;">R<sup>2</sup> / R<sup>2</sup> adjusted</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; padding-top:0.1cm; padding-bottom:0.1cm; text-align:left;" colspan="4">0.963 / 0.950</td>
</tr>

</table>

<table style="border-collapse:collapse; border:none;">
<caption style="font-weight: bold; text-align:left;">2024 Democrat Two Party Vote Share via Model Including Incumbent Party</caption>
<tr>
<th style="border-top: double; text-align:center; font-style:italic; font-weight:normal; padding:0.2cm; border-bottom:1px solid black; text-align:left; ">Prediction</th>
<th style="border-top: double; text-align:center; font-style:italic; font-weight:normal; padding:0.2cm; border-bottom:1px solid black; ">Lower.Bound</th>
<th style="border-top: double; text-align:center; font-style:italic; font-weight:normal; padding:0.2cm; border-bottom:1px solid black; ">Upper.Bound</th>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; border-bottom: double; ">52.96%</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; border-bottom: double; ">50.15%</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; border-bottom: double; ">55.77%</td>
</tr>
</table>

<table style="border-collapse:collapse; border:none;">
<caption style="font-weight: bold; text-align:left;">2024 Democrat Two Party Vote Share via Random Forest Model</caption>
<tr>
<th style="border-top: double; text-align:center; font-style:italic; font-weight:normal; padding:0.2cm; border-bottom:1px solid black; text-align:left; ">year</th>
<th style="border-top: double; text-align:center; font-style:italic; font-weight:normal; padding:0.2cm; border-bottom:1px solid black; ">Prediction</th>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; border-bottom: double; ">2024</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; border-bottom: double; ">51.78%</td>
</tr>
</table>


```
## 
## Call:
## lm(formula = pv2p ~ avg_poll_8_5 + state + RDPI_growth_quarterly + 
##     incumbent_party, data = swing_model_data_r)
## 
## Coefficients:
##           (Intercept)           avg_poll_8_5           stateGeorgia  
##               27.1854                 0.4272                -0.7936  
##         stateMichigan            stateNevada    stateNorth Carolina  
##                4.1338                 0.1846                -2.2326  
##     statePennsylvania         stateWisconsin  RDPI_growth_quarterly  
##                3.9401                 3.3733                 0.3248  
##       incumbent_party  
##                2.2992
```

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


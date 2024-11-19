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

``` r
library(tidyverse)
```

    ## ── Attaching core tidyverse packages ──────────────────────── tidyverse 2.0.0 ──
    ## ✔ dplyr     1.1.4     ✔ readr     2.1.5
    ## ✔ forcats   1.0.0     ✔ stringr   1.5.1
    ## ✔ ggplot2   3.4.4     ✔ tibble    3.2.1
    ## ✔ lubridate 1.9.3     ✔ tidyr     1.3.0
    ## ✔ purrr     1.0.2     
    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()
    ## ℹ Use the conflicted package (<http://conflicted.r-lib.org/>) to force all conflicts to become errors

``` r
library(knitr)
library(plotly)
```

    ## Warning: package 'plotly' was built under R version 4.3.3

    ## 
    ## Attaching package: 'plotly'
    ## 
    ## The following object is masked from 'package:ggplot2':
    ## 
    ##     last_plot
    ## 
    ## The following object is masked from 'package:stats':
    ## 
    ##     filter
    ## 
    ## The following object is masked from 'package:graphics':
    ## 
    ##     layout

``` r
library(maps)
```

    ## 
    ## Attaching package: 'maps'
    ## 
    ## The following object is masked from 'package:purrr':
    ## 
    ##     map

``` r
library(car)
```

    ## Warning: package 'car' was built under R version 4.3.3

    ## Loading required package: carData

    ## Warning: package 'carData' was built under R version 4.3.3

    ## 
    ## Attaching package: 'car'
    ## 
    ## The following object is masked from 'package:dplyr':
    ## 
    ##     recode
    ## 
    ## The following object is masked from 'package:purrr':
    ## 
    ##     some

``` r
library(CVXR)
```

    ## Warning: package 'CVXR' was built under R version 4.3.3

    ## 
    ## Attaching package: 'CVXR'
    ## 
    ## The following object is masked from 'package:dplyr':
    ## 
    ##     id
    ## 
    ## The following object is masked from 'package:purrr':
    ## 
    ##     is_vector
    ## 
    ## The following object is masked from 'package:stats':
    ## 
    ##     power

``` r
library(stringr)
library(knitr)
library(kableExtra)
```

    ## Warning: package 'kableExtra' was built under R version 4.3.3

    ## 
    ## Attaching package: 'kableExtra'
    ## 
    ## The following object is masked from 'package:dplyr':
    ## 
    ##     group_rows

``` r
library(caret)
```

    ## Warning: package 'caret' was built under R version 4.3.3

    ## Loading required package: lattice
    ## 
    ## Attaching package: 'caret'
    ## 
    ## The following object is masked from 'package:purrr':
    ## 
    ##     lift

``` r
library(yardstick)
```

    ## Warning: package 'yardstick' was built under R version 4.3.3

    ## 
    ## Attaching package: 'yardstick'
    ## 
    ## The following objects are masked from 'package:caret':
    ## 
    ##     precision, recall, sensitivity, specificity
    ## 
    ## The following object is masked from 'package:readr':
    ## 
    ##     spec

``` r
set.seed(02138)
```

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

``` r
weights_df <- read_csv("weights_df.csv") |>
  kable("html", 
        col.names = c("State", "Model 1", "Model 2", "Model 3"),
        caption = "Model Weights by State", digits = 3) %>%
  kable_styling(full_width = FALSE, bootstrap_options = c("striped", "hover", "condensed", "responsive")) %>%
  column_spec(1, width = "8em", extra_css = "text-align: center;") %>%
  column_spec(2:4, width = "6em", extra_css = "text-align: center;")
```

    ## Rows: 7 Columns: 4
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (1): State
    ## dbl (3): Weight.Model.1, Weight.Model.2, Weight.Model.3
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
weights_df
```

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

``` r
swing_states <- c("Arizona", "Georgia", "Michigan", "Nevada", "North Carolina", "Pennsylvania", "Wisconsin")

avi_preds <- read_csv("avi_2024_preds - Sheet1.csv")
```

    ## Rows: 7 Columns: 2
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (1): state
    ## dbl (1): Dv2p
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
state_vote_2024 <- read_csv("state_votes_pres_2024.csv") |>
  filter(row_number() != 1) |>
  select(c("Geographic Name", "Total Vote", "Kamala D. Harris", "Donald J. Trump")) |>
  mutate(
    state = `Geographic Name`,
    `Total Vote` = as.numeric(`Total Vote`),
    `Kamala D. Harris` = as.numeric(`Kamala D. Harris`),
    `Donald J. Trump` = as.numeric(`Donald J. Trump`)
  ) |>
  filter(state %in% swing_states) |>
  mutate(Dv2p_real = `Kamala D. Harris` / (`Kamala D. Harris` + `Donald J. Trump`)*100)
```

    ## New names:
    ## Rows: 52 Columns: 42
    ## ── Column specification
    ## ──────────────────────────────────────────────────────── Delimiter: "," chr
    ## (42): FIPS, Geographic Name, Geographic Subtype, Total Vote, Kamala D. H...
    ## ℹ Use `spec()` to retrieve the full column specification for this data. ℹ
    ## Specify the column types or set `show_col_types = FALSE` to quiet this message.
    ## • `0` -> `0...31`
    ## • `0` -> `0...32`
    ## • `0` -> `0...33`
    ## • `0` -> `0...34`
    ## • `0` -> `0...35`
    ## • `0` -> `0...36`
    ## • `0` -> `0...37`
    ## • `0` -> `0...38`
    ## • `0` -> `0...39`
    ## • `0` -> `0...40`
    ## • `0` -> `0...41`
    ## • `0` -> `0...42`

``` r
state_vote_2024 <- state_vote_2024 |>
  left_join(avi_preds, by = "state")
```

``` r
state_vote_2024_table <- state_vote_2024 |>
  select(c("state", "Dv2p_real", "Dv2p" )) |>
  mutate(across(where(is.numeric), round, digits = 3)) |>
  kable(
    caption = "2024 Presidential Election Results by State",
    col.names = c("State", "Real Democratic Vote Share (%)", "Predicted Democratic Vote Share (%)"),
    format = "html"
  ) |>
  kable_styling(
    full_width = FALSE,
    bootstrap_options = c("striped", "hover", "condensed")
  )
```

    ## Warning: There was 1 warning in `mutate()`.
    ## ℹ In argument: `across(where(is.numeric), round, digits = 3)`.
    ## Caused by warning:
    ## ! The `...` argument of `across()` is deprecated as of dplyr 1.1.0.
    ## Supply arguments directly to `.fns` through an anonymous function instead.
    ## 
    ##   # Previously
    ##   across(a:b, mean, na.rm = TRUE)
    ## 
    ##   # Now
    ##   across(a:b, \(x) mean(x, na.rm = TRUE))

``` r
state_vote_2024_table  
```

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

``` r
win_counts <- read_csv("win_counts.csv")
```

    ## Rows: 1 Columns: 3
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (1): Harris Victory %
    ## dbl (2): Harris Victory Wins, Trump Victory Wins
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
sim_table <- win_counts %>%
  kable("html", caption = "Simulation Results: Harris and Trump Victory Counts") %>%
  kable_styling(full_width = FALSE, bootstrap_options = c("striped", "hover", "condensed", "responsive"), position = "center") %>%
  column_spec(1, width = "5em", extra_css = "text-align: center;") %>%
  column_spec(2, width = "5em", extra_css = "text-align: center;") %>%
  column_spec(3, width = "5em", extra_css = "text-align: center;")

sim_table
```

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

``` r
MSE <- state_vote_2024 |>
  mutate(
    error_squared = (Dv2p_real - Dv2p)^2,
    abs_error = abs(Dv2p_real - Dv2p)
  ) |>
  group_by(state) |>
  summarise(
    Bias = mean(Dv2p_real - Dv2p),
    MSE = mean(error_squared),
    RMSE = sqrt(MSE),
    MAE = mean(abs_error)
  )

average_row <- state_vote_2024 |>
  summarise(
    state = "Average",
    Bias = mean(Dv2p_real - Dv2p),
    MSE = mean((Dv2p_real - Dv2p)^2),
    RMSE = mean(sqrt(MSE)),
    MAE = mean(abs(Dv2p_real - Dv2p))
  )


MSE <- bind_rows(MSE, average_row) |>
  rename("State" = state)

MSE_table <- MSE |>
  mutate(across(where(is.numeric), round, digits = 3)) |>
  kable(
    caption = "State-Level MSE Table",
    col.names = c("State", "Bias", "MSE", "RMSE", "MAE"),
    format = "html"
  ) |>
  kable_styling(
    full_width = FALSE,
    bootstrap_options = c("striped", "hover", "condensed")
  )

MSE_table
```

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
1.678
</td>
<td style="text-align:right;">
1.387
</td>
</tr>
</tbody>
</table>

``` r
map_data <- MSE |>
  mutate(state = tolower(State)) 

us_states <- map_data("state")


swing_map_data <- us_states %>%
  filter(region %in% map_data$state) %>%
  left_join(map_data, by = c("region" = "state"))

swing_map_data <- swing_map_data %>%
  distinct(region, .keep_all = TRUE) %>%
  mutate(state = tools::toTitleCase(region)) %>%
  mutate(state_code = state.abb[match(state, state.name)]) |>
  mutate(region = tools::toTitleCase(region))

map_plot <- plot_ly(
  data = swing_map_data,
  type = "choropleth",
  locations = ~state_code,
  locationmode = "USA-states",
  z = ~Bias,
  text = ~paste("State:", region, "<br>Bias:", round(Bias, 2), "%"),
  hoverinfo = "text",
  colorscale = list(c(0, "darkblue"), c(0.5, "white"), c(1, "darkred")),
  zmin = -4,   
  zmid = 0,     
  zmax = 4,    
  colorbar = list(
    title = "Model Bias \n(Blue = Overestimated \nDem. Vote %)",
    y = 0.5,           
    yanchor = "middle" 
  )
) %>%
  layout(
    title = list(
      text = "Swing State Model Bias",
      y = 0.95,
      x = 0.5,
      xanchor = "center",
      yanchor = "top"
    ),
    geo = list(
      scope = "usa",
      projection = list(type = "albers usa"),
      showlakes = FALSE,
      showcountries = FALSE,
      showcoastlines = FALSE,
      coastlinecolor = toRGB("white"),
      showframe = FALSE
    )
  )
map_plot
```

<div class="plotly html-widget html-fill-item" id="htmlwidget-1" style="width:672px;height:480px;"></div>
<script type="application/json" data-for="htmlwidget-1">{"x":{"visdat":{"868c35f4512e":["function () ","plotlyVisDat"]},"cur_data":"868c35f4512e","attrs":{"868c35f4512e":{"locations":{},"locationmode":"USA-states","z":{},"text":{},"hoverinfo":"text","colorscale":[["0","darkblue"],["0.5","white"],["1","darkred"]],"zmin":-4,"zmid":0,"zmax":4,"colorbar":{"title":"Model Bias <br />(Blue = Overestimated <br />Dem. Vote %)","y":0.5,"yanchor":"middle"},"alpha_stroke":1,"sizes":[10,100],"spans":[1,20],"type":"choropleth"}},"layout":{"margin":{"b":40,"l":60,"t":25,"r":10},"title":{"text":"Swing State Model Bias","y":0.94999999999999996,"x":0.5,"xanchor":"center","yanchor":"top"},"geo":{"scope":"usa","projection":{"type":"albers usa"},"showlakes":false,"showcountries":false,"showcoastlines":false,"coastlinecolor":"rgba(255,255,255,1)","showframe":false},"scene":{"zaxis":{"title":"Bias"}},"hovermode":"closest","showlegend":false,"legend":{"yanchor":"top","y":0.5}},"source":"A","config":{"modeBarButtonsToAdd":["hoverclosest","hovercompare"],"showSendToCloud":false},"data":[{"colorbar":{"title":"Model Bias <br />(Blue = Overestimated <br />Dem. Vote %)","ticklen":2,"y":0.5,"yanchor":"middle","len":0.5,"lenmode":"fraction"},"colorscale":[["0","darkblue"],["0.5","white"],["1","darkred"]],"showscale":true,"locations":["AZ","GA","MI","NV","NC","PA","WI"],"locationmode":"USA-states","z":[-0.53747346355770276,-0.35155030253291386,-2.1084448240057725,-3.3017124462760208,-0.94110553222387239,-1.3176535411938204,-1.148442057732332],"text":["State: Arizona <br>Bias: -0.54 %","State: Georgia <br>Bias: -0.35 %","State: Michigan <br>Bias: -2.11 %","State: Nevada <br>Bias: -3.3 %","State: North Carolina <br>Bias: -0.94 %","State: Pennsylvania <br>Bias: -1.32 %","State: Wisconsin <br>Bias: -1.15 %"],"hoverinfo":["text","text","text","text","text","text","text"],"zmin":-4,"zmid":0,"zmax":4,"type":"choropleth","marker":{"line":{"color":"rgba(31,119,180,1)"}},"frame":null}],"highlight":{"on":"plotly_click","persistent":false,"dynamic":false,"selectize":false,"opacityDim":0.20000000000000001,"selected":{"opacity":1},"debounce":0},"shinyEvents":["plotly_hover","plotly_click","plotly_selected","plotly_relayout","plotly_brushed","plotly_brushing","plotly_clickannotation","plotly_doubleclick","plotly_deselect","plotly_afterplot","plotly_sunburstclick"],"base_url":"https://plot.ly"},"evals":[],"jsHooks":[]}</script>

``` r
state_vote_2024 <- state_vote_2024 |>
  mutate(
    actual = ifelse(Dv2p_real >= 50, 1, 0),
    predicted = ifelse(Dv2p >= 50, 1, 0),
    predicted_prob = Dv2p / 100
  )

actual_factor <- factor(state_vote_2024$actual, levels = c(0, 1))
predicted_factor <- factor(state_vote_2024$predicted, levels = c(0, 1))

confusion_matrix <- confusionMatrix(predicted_factor, actual_factor)

# Extract relevant metrics from the confusion matrix
metrics <- data.frame(
  Metric = c("Accuracy", "Sensitivity (Recall)", "Specificity", "Precision", "F1 Score"),
  Value = c(
    round(confusion_matrix$overall['Accuracy'], 3),
    round(confusion_matrix$byClass['Sensitivity'], 3),
    round(confusion_matrix$byClass['Specificity'], 3),
    round(confusion_matrix$byClass['Pos Pred Value'], 3),
    round(2 * (confusion_matrix$byClass['Pos Pred Value'] * confusion_matrix$byClass['Sensitivity']) /
          (confusion_matrix$byClass['Pos Pred Value'] + confusion_matrix$byClass['Sensitivity']), 3)
  )
)

# Display the table using kable
kable(metrics, caption = "Confusion Matrix Metrics", format = "html") %>%
  kable_styling(full_width = FALSE, bootstrap_options = c("striped", "hover"))
```

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

``` r
pred_chance <- win_counts |> 
  mutate(pred_chance = `Harris Victory Wins`/ 1000) |>
  select("pred_chance")
brier_score <- mean((pred_chance$pred_chance - 0)^2) |>
  round(3)

print(brier_score)
```

    ## [1] 0.347

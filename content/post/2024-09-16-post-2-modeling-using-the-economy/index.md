---
title: 'Post #2: Modeling Using the Economy'
author: Avi Agarwal
date: '2024-09-16'
slug: post-2-modeling-using-the-economy
categories: []
tags: []
---


```r
library(ggplot2)
library(maps)
library(tidyverse)
```

```
## ── Attaching core tidyverse packages ──────────────────────── tidyverse 2.0.0 ──
## ✔ dplyr     1.1.4     ✔ readr     2.1.5
## ✔ forcats   1.0.0     ✔ stringr   1.5.1
## ✔ lubridate 1.9.3     ✔ tibble    3.2.1
## ✔ purrr     1.0.2     ✔ tidyr     1.3.0
## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
## ✖ dplyr::filter() masks stats::filter()
## ✖ dplyr::lag()    masks stats::lag()
## ✖ purrr::map()    masks maps::map()
## ℹ Use the conflicted package (<http://conflicted.r-lib.org/>) to force all conflicts to become errors
```

```r
#library(patchwork)
library(stargazer)
```

```
## 
## Please cite as: 
## 
##  Hlavac, Marek (2022). stargazer: Well-Formatted Regression and Summary Statistics Tables.
##  R package version 5.2.3. https://CRAN.R-project.org/package=stargazer
```

```r
library(sjPlot)
```

```
## Warning: package 'sjPlot' was built under R version 4.3.3
```

```
## Learn more about sjPlot with 'browseVignettes("sjPlot")'.
```


```r
d_popvote <- read_csv("popvote_1948-2020.csv")
```

```
## Rows: 38 Columns: 9
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr (2): party, candidate
## dbl (3): year, pv, pv2p
## lgl (4): winner, incumbent, incumbent_party, prev_admin
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```r
d_fred <- read_csv("fred_econ.csv")
```

```
## Rows: 387 Columns: 14
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## dbl (14): year, quarter, GDP, GDP_growth_quarterly, RDPI, RDPI_growth_quarte...
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```r
d_fred_adjusted <- d_fred |>
  filter(year > 1958) |>
  mutate(unemployment_growth_quarterly = (unemployment - lag(unemployment, 1)) / lag(unemployment, 1) * 100) |>
  filter(quarter == 2) |>
  mutate(RDPI_growth_annually = (RDPI - lag(RDPI, 1)) / lag(RDPI, 1) * 100) |> #learned about lag from LLM/ChatGPT
  mutate(sp500_growth_quarterly = ((sp500_adj_close - sp500_open)) / sp500_open * 100) |>
  mutate(sp500_growth_anually = (sp500_adj_close - lag(sp500_adj_close, 1)) / lag(sp500_adj_close, 1) * 100) |> 
  mutate(unemployment_growth_anually = (unemployment - lag(unemployment, 1)) / lag(unemployment, 1) * 100) |>
  filter(year >= 1960 & year != 2020) |> #exclude 2020 since it such an outlier
  select(year, RDPI_growth_quarterly, RDPI_growth_annually, sp500_growth_quarterly, sp500_growth_anually, unemployment_growth_quarterly, unemployment_growth_anually)


# Filter and merge data. 
d_inc_econ <- d_popvote |> 
  filter(incumbent_party == TRUE & year >= 1960 & year != 2020) |> 
  select(year, pv2p, winner) |> 
  left_join(d_fred_adjusted, by = "year")
```


```r
plot_unemp_quarterly <- ggplot(d_inc_econ, aes(x = unemployment_growth_quarterly, y = pv2p, label = year)) + 
  geom_point() +
  geom_text(hjust = 1.2, size = 3) + 
  geom_smooth(method = "lm", formula = y ~ x) +
  geom_hline(yintercept = 50, lty = 2) + 
  geom_vline(xintercept = 0, lty = 2) + 
  labs(x = "Q2 Unemployment Growth (%)", 
       y = "National Popular Two Party Vote Share (%)",
       caption = "The years in the graph are from 1960 to 2016.") + 
  theme_bw() + 
  theme(plot.title = element_text(size = 14, hjust = 0.5),
        axis.title = element_text(size = 12))
#used LLM to replicate graphs
plot_unemp_annually <- ggplot(d_inc_econ, aes(x = unemployment_growth_anually, y = pv2p, label = year)) + 
  geom_point() +
  geom_text(hjust = 1.2, size = 3) + 
  geom_smooth(method = "lm", formula = y ~ x) +
  geom_hline(yintercept = 50, lty = 2) + 
  geom_vline(xintercept = 0, lty = 2) + 
  labs(x = "Annual Unemployment Growth (%)", 
       y = "National Popular Two Party Vote Share (%)",
       caption = "The years in the graph are from 1960 to 2016.") + 
  theme_bw() + 
  theme(plot.title = element_text(size = 14, hjust = 0.5),
        axis.title = element_text(size = 12))

plot_rdpi_quarterly <- ggplot(d_inc_econ, aes(x = RDPI_growth_quarterly, y = pv2p, label = year)) + 
  geom_point() +
  geom_text(hjust = 1.2, size = 3) + 
  geom_smooth(method = "lm", formula = y ~ x) +
  geom_hline(yintercept = 50, lty = 2) + 
  geom_vline(xintercept = 0, lty = 2) + 
  labs(x = "Q2 RDPI Growth (%)", 
       y = "National Popular Two Party Vote Share (%)",
       caption = "The years in the graph are from 1960 to 2016.") + 
  theme_bw() + 
  theme(plot.title = element_text(size = 14, hjust = 0.5),
        axis.title = element_text(size = 12))

plot_rdpi_annually <- ggplot(d_inc_econ, aes(x = RDPI_growth_annually, y = pv2p, label = year)) + 
  geom_point() +
  geom_text(hjust = 1.2, size = 3) + 
  geom_smooth(method = "lm", formula = y ~ x) +
  geom_hline(yintercept = 50, lty = 2) + 
  geom_vline(xintercept = 0, lty = 2) + 
  labs(x = "Annual RDPI Growth (%)", 
       y = "National Popular Two Party Vote Share (%)",
       caption = "The years in the graph are from 1960 to 2016.") + 
  theme_bw() + 
  theme(plot.title = element_text(size = 14, hjust = 0.5),
        axis.title = element_text(size = 12))

plot_sp500_quarterly <- ggplot(d_inc_econ, aes(x = sp500_growth_quarterly, y = pv2p, label = year)) + 
  geom_point() +
  geom_text(hjust = 1.2, size = 3) + 
  geom_smooth(method = "lm", formula = y ~ x) +
  geom_hline(yintercept = 50, lty = 2) + 
  geom_vline(xintercept = 0, lty = 2) + 
  labs(x = "Q2 S&P 500 Growth (%)", 
       y = "National Popular Two Party Vote Share (%)",
       caption = "The years in the graph are from 1960 to 2016.") + 
  theme_bw() + 
  theme(plot.title = element_text(size = 14, hjust = 0.5),
        axis.title = element_text(size = 12))


plot_sp500_annually <- ggplot(d_inc_econ, aes(x = sp500_growth_anually, y = pv2p, label = year)) + 
  geom_point() +
  geom_text(hjust = 1.2, size = 3) + 
  geom_smooth(method = "lm", formula = y ~ x) +
  geom_hline(yintercept = 50, lty = 2) + 
  geom_vline(xintercept = 0, lty = 2) + 
  labs(x = "Annual S&P 500 Growth (%)", 
       y = "National Popular Two Party Vote Share (%)",
       caption = "The years in the graph are from 1960 to 2016.") + 
  theme_bw() + 
  theme(plot.title = element_text(size = 14, hjust = 0.5),
        axis.title = element_text(size = 12))
```


```r
model_unemp_quarterly <- lm(pv2p ~ unemployment_growth_quarterly, data = d_inc_econ)

model_unemp_annually <- lm(pv2p ~ unemployment_growth_anually, data = d_inc_econ)

model_rdpi_quarterly <- lm(pv2p ~ RDPI_growth_quarterly, data = d_inc_econ)

model_rdpi_annually <- lm(pv2p ~ RDPI_growth_annually, data = d_inc_econ)

model_sp500_quarterly <- lm(pv2p ~ sp500_growth_quarterly, data = d_inc_econ)

model_sp500_annually <- lm(pv2p ~ sp500_growth_anually, data = d_inc_econ)
```

#Real Disposable Personal Income Growth


```r
plot_rdpi_quarterly
```

```
## Warning: The following aesthetics were dropped during statistical transformation: label
## ℹ This can happen when ggplot fails to infer the correct grouping structure in
##   the data.
## ℹ Did you forget to specify a `group` aesthetic or to convert a numerical
##   variable into a factor?
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-5-1.png" width="672" />


```r
tab_model(model_rdpi_quarterly, show.se = TRUE, 
          title = "Regression Table for Quarterly RDPI Growth (1960-2016)", 
          dv.labels = "National Popular Two Party Vote Share (%)",
          pred.labels = c("(Intercept)", "Quarterly RDPI Growth (%)"))
```

<table style="border-collapse:collapse; border:none;">
<caption style="font-weight: bold; text-align:left;">Regression Table for Quarterly RDPI Growth (1960-2016)</caption>
<tr>
<th style="border-top: double; text-align:center; font-style:normal; font-weight:bold; padding:0.2cm;  text-align:left; ">&nbsp;</th>
<th colspan="4" style="border-top: double; text-align:center; font-style:normal; font-weight:bold; padding:0.2cm; ">National Popular Two Party Vote Share (%)</th>
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



```r
plot_rdpi_annually
```

```
## Warning: The following aesthetics were dropped during statistical transformation: label
## ℹ This can happen when ggplot fails to infer the correct grouping structure in
##   the data.
## ℹ Did you forget to specify a `group` aesthetic or to convert a numerical
##   variable into a factor?
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-7-1.png" width="672" />


```r
tab_model(model_rdpi_annually, show.se = TRUE, 
          title = "Regression Table for Annual RDPI Growth (1960-2016)", 
          dv.labels = "National Popular Two Party Vote Share (%)",
          pred.labels = c("(Intercept)", "Annual RDPI Growth (%)"))
```

<table style="border-collapse:collapse; border:none;">
<caption style="font-weight: bold; text-align:left;">Regression Table for Annual RDPI Growth (1960-2016)</caption>
<tr>
<th style="border-top: double; text-align:center; font-style:normal; font-weight:bold; padding:0.2cm;  text-align:left; ">&nbsp;</th>
<th colspan="4" style="border-top: double; text-align:center; font-style:normal; font-weight:bold; padding:0.2cm; ">National Popular Two Party Vote Share (%)</th>
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

#S&P 500 Growth


```r
plot_sp500_quarterly
```

```
## Warning: The following aesthetics were dropped during statistical transformation: label
## ℹ This can happen when ggplot fails to infer the correct grouping structure in
##   the data.
## ℹ Did you forget to specify a `group` aesthetic or to convert a numerical
##   variable into a factor?
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-9-1.png" width="672" />


```r
tab_model(model_sp500_quarterly, show.se = TRUE, 
          title = "Regression Table for Quarterly S&P 500 Growth (1960-2016)", 
          dv.labels = "National Popular Two Party Vote Share (%)",
          pred.labels = c("(Intercept)", "Quarterly S&P 500 Growth (%)"))
```

<table style="border-collapse:collapse; border:none;">
<caption style="font-weight: bold; text-align:left;">Regression Table for Quarterly S&P 500 Growth (1960-2016)</caption>
<tr>
<th style="border-top: double; text-align:center; font-style:normal; font-weight:bold; padding:0.2cm;  text-align:left; ">&nbsp;</th>
<th colspan="4" style="border-top: double; text-align:center; font-style:normal; font-weight:bold; padding:0.2cm; ">National Popular Two Party Vote Share (%)</th>
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



```r
plot_sp500_annually
```

```
## Warning: The following aesthetics were dropped during statistical transformation: label
## ℹ This can happen when ggplot fails to infer the correct grouping structure in
##   the data.
## ℹ Did you forget to specify a `group` aesthetic or to convert a numerical
##   variable into a factor?
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-11-1.png" width="672" />


```r
tab_model(model_sp500_annually, show.se = TRUE, 
          title = "Regression Table for Annual S&P 500 Growth (1960-2016)", 
          dv.labels = "National Popular Two Party Vote Share (%)",
          pred.labels = c("(Intercept)", "Annual S&P 500 Growth (%)"))
```

<table style="border-collapse:collapse; border:none;">
<caption style="font-weight: bold; text-align:left;">Regression Table for Annual S&P 500 Growth (1960-2016)</caption>
<tr>
<th style="border-top: double; text-align:center; font-style:normal; font-weight:bold; padding:0.2cm;  text-align:left; ">&nbsp;</th>
<th colspan="4" style="border-top: double; text-align:center; font-style:normal; font-weight:bold; padding:0.2cm; ">National Popular Two Party Vote Share (%)</th>
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

#Unemployment Growth


```r
plot_unemp_quarterly
```

```
## Warning: The following aesthetics were dropped during statistical transformation: label
## ℹ This can happen when ggplot fails to infer the correct grouping structure in
##   the data.
## ℹ Did you forget to specify a `group` aesthetic or to convert a numerical
##   variable into a factor?
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-13-1.png" width="672" />


```r
tab_model(model_unemp_quarterly, show.se = TRUE, 
          title = "Regression Table for Quarterly Unemployment Growth (1960-2016)", 
          dv.labels = "National Popular Two Party Vote Share (%)",
          pred.labels = c("(Intercept)", "Quarterly Unemployment Growth (%)"))
```

<table style="border-collapse:collapse; border:none;">
<caption style="font-weight: bold; text-align:left;">Regression Table for Quarterly Unemployment Growth (1960-2016)</caption>
<tr>
<th style="border-top: double; text-align:center; font-style:normal; font-weight:bold; padding:0.2cm;  text-align:left; ">&nbsp;</th>
<th colspan="4" style="border-top: double; text-align:center; font-style:normal; font-weight:bold; padding:0.2cm; ">National Popular Two Party Vote Share (%)</th>
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



```r
plot_unemp_annually
```

```
## Warning: The following aesthetics were dropped during statistical transformation: label
## ℹ This can happen when ggplot fails to infer the correct grouping structure in
##   the data.
## ℹ Did you forget to specify a `group` aesthetic or to convert a numerical
##   variable into a factor?
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-15-1.png" width="672" />


```r
tab_model(model_unemp_annually, show.se = TRUE, 
          title = "Regression Table for Annual Unemployment Growth (1960-2016)", 
          dv.labels = "National Popular Two Party Vote Share (%)",
          pred.labels = c("(Intercept)", "Annual Unemployment Growth (%)"))
```

<table style="border-collapse:collapse; border:none;">
<caption style="font-weight: bold; text-align:left;">Regression Table for Annual Unemployment Growth (1960-2016)</caption>
<tr>
<th style="border-top: double; text-align:center; font-style:normal; font-weight:bold; padding:0.2cm;  text-align:left; ">&nbsp;</th>
<th colspan="4" style="border-top: double; text-align:center; font-style:normal; font-weight:bold; padding:0.2cm; ">National Popular Two Party Vote Share (%)</th>
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



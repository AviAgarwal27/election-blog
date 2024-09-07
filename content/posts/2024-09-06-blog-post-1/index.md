---
title: Blog Post 1
author: Avi Agarwal
date: '2024-09-09'
slug: blog-post-1
categories: []
tags: []
---

This is the first of a series of blog posts in which I will be analyzing and prediciting the 2024 Presidential Election. 


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
states_map <- map_data("state")
d_pvstate_wide <- read_csv("clean_wide_state_2pv_1948_2020.csv")
```

```
## Rows: 959 Columns: 14
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## chr  (1): state
## dbl (13): year, D_pv, R_pv, D_pv2p, R_pv2p, D_pv_lag1, R_pv_lag1, D_pv2p_lag...
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```


```r
d_pvstate_wide_pred_2024 <- d_pvstate_wide |>
  filter(year == 2020) |> 
  group_by(state) |>
  summarize(D_vote2024 = 0.75*D_pv2p + 0.25*D_pv2p_lag1) |>
  mutate(region = tolower(state), winner = if_else(D_vote2024 > 50, "D", "R"))
```



```r
d_pvstate_wide_pred_2024 |>
  left_join(states_map, by = "region") |>
  ggplot(mapping = aes(x = long, y = lat, group = group, fill = winner)) + geom_polygon() + theme_void() + scale_fill_manual(values = c("blue", "red")) 
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-4-1.png" width="672" />
```


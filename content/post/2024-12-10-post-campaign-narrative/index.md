---
title: Post-Campaign Narrative
author: Avi Agarwal
date: '2024-12-10'
slug: post-campaign-narrative
categories: []
tags: []
---
<script src="{{< blogdown/postref >}}index_files/kePrint/kePrint.js"></script>
<link href="{{< blogdown/postref >}}index_files/lightable/lightable.css" rel="stylesheet" />

```r
library(dplyr)
```

```
## 
## Attaching package: 'dplyr'
```

```
## The following objects are masked from 'package:stats':
## 
##     filter, lag
```

```
## The following objects are masked from 'package:base':
## 
##     intersect, setdiff, setequal, union
```

```r
library(tidytext)
```

```
## Warning: package 'tidytext' was built under R version 4.3.3
```

```r
library(ggplot2)
```

```
## Warning: package 'ggplot2' was built under R version 4.3.3
```

```r
library(knitr)
library(kableExtra)
```

```
## Warning: package 'kableExtra' was built under R version 4.3.3
```

```
## 
## Attaching package: 'kableExtra'
```

```
## The following object is masked from 'package:dplyr':
## 
##     group_rows
```

```r
library(stopwords)
```

```
## Warning: package 'stopwords' was built under R version 4.3.3
```

```r
library(tidyverse)
```

```
## ── Attaching core tidyverse packages ──────────────────────── tidyverse 2.0.0 ──
## ✔ forcats   1.0.0     ✔ stringr   1.5.1
## ✔ lubridate 1.9.3     ✔ tibble    3.2.1
## ✔ purrr     1.0.2     ✔ tidyr     1.3.0
## ✔ readr     2.1.5
```

```
## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
## ✖ dplyr::filter()          masks stats::filter()
## ✖ kableExtra::group_rows() masks dplyr::group_rows()
## ✖ dplyr::lag()             masks stats::lag()
## ℹ Use the conflicted package (<http://conflicted.r-lib.org/>) to force all conflicts to become errors
```



```r
categories <- list(
  #used ai to help generate this
  Economy = c(
    "economy", "jobs", "employment", "trade", "market", "budget", "tax", 
    "spending", "inflation", "growth", "investment", "industry", "financial", 
    "business", "revenue", "profits", "income", "poverty", "deficit", 
    "wages", "regulation", "commerce", "productivity", "fiscal", "monetary", 
    "debt", "surplus", "credit", "loans", "exports", "imports", "capital", 
    "enterprises", "subsidies", "tariffs", "economic", "stocks", "bonds", 
    "banking", "insurance", "costs", "prices", "markets", "profits", 
    "commodities", "wealth", "gross", "domestic", "product"
  ),
  Domestic_Policy = c(
    "healthcare", "education", "immigration", "infrastructure", "housing", 
    "crime", "police", "justice", "schools", "teachers", "students", 
    "citizenship", "border", "roads", "transportation", "energy", "environment", 
    "climate", "clean", "water", "electricity", "family", "welfare", 
    "childcare", "labor", "workers", "unions", "safety", "pensions", "benefits", 
    "medicaid", "medicare", "security", "employment", "poverty", "urban", 
    "rural", "public", "health", "infrastructure", "renewable", "recycling", 
    "carbon", "emissions", "forests", "wildlife", "discrimination", "diversity", 
    "equality", "justice", "laws", "legislation", "marriage", "civil", "rights", 
    "affordable", "housing", "crime", "violence", "addiction", "mental", "health"
  ),
  Foreign_Policy = c(
    "foreign", "defense", "war", "allies", "diplomacy", "nuclear", 
    "security", "military", "troops", "peace", "terrorism", "global", 
    "treaty", "international", "relations", "sanctions", "conflict", 
    "weapons", "strategy", "border", "aid", "humanitarian", "refugees", 
    "geopolitics", "espionage", "intelligence", "alliances", "cooperation", 
    "trade", "sanctions", "blockades", "proliferation", "arms", "embassies", 
    "ambassadors", "UN", "NATO", "treaties", "diplomatic", "sovereignty", 
    "negotiations", "peacekeeping", "hostilities", "intervention", "coalition"
  ),
  Character = c(
    "dishonesty", "corruption", "incompetence", "arrogance", "greed", "selfishness", 
    "cowardice", "hypocrisy", "deception", "unethical", "irresponsibility", 
    "failure", "indecisive", "untrustworthy", "lazy", "ignorance", 
    "prejudice", "unreliable", "manipulative", "biased", "unaccountable", 
    "apathetic", "opportunistic", "exploitative", "immoral", "manipulation", 
    "abuse", "cruelty", "dishonor", "vindictive", "corrupt", "reckless", 
    "shortsighted", "intolerant", "narrowminded", "greedy", "tyrannical", 
    "unethical", "exploit", "deceitful", "spiteful", "bigoted", "self-centered", 
    "authoritarian", "irresponsible", "hypocritical", "abusive"
  )
)
```


```r
harris <- readLines("New folder (4)/Harris-10-31.txt")
```

```
## Warning in readLines("New folder (4)/Harris-10-31.txt"): incomplete final line
## found on 'New folder (4)/Harris-10-31.txt'
```

```r
gallego <- readLines("New folder (4)/Gallego-10-31.txt")
```

```
## Warning in readLines("New folder (4)/Gallego-10-31.txt"): incomplete final line
## found on 'New folder (4)/Gallego-10-31.txt'
```

```r
lake <- readLines("New folder (4)/Lake-10-24.txt")
```

```
## Warning in readLines("New folder (4)/Lake-10-24.txt"): incomplete final line
## found on 'New folder (4)/Lake-10-24.txt'
```

```r
trump <- readLines("New folder (4)/Trump-10-24.txt")
```

```
## Warning in readLines("New folder (4)/Trump-10-24.txt"): incomplete final line
## found on 'New folder (4)/Trump-10-24.txt'
```

```r
harris_text <- paste(harris, collapse = " ")
gallego_text <- paste(gallego, collapse = " ")
lake_text <- paste(lake, collapse = " ")
trump_text <- paste(trump, collapse = " ")

speeches <- data.frame(
  speaker = c("Harris", "Gallego", "Lake", "Trump"),
  text = c(harris_text, gallego_text, lake_text, trump_text),
  stringsAsFactors = FALSE
)
```


```r
tokenized_speeches <- speeches %>%
  unnest_tokens(word, text) %>%                   
  filter(nchar(word) >= 3) %>%                
  mutate(word = tolower(word)) %>%             
  filter(!word %in% stopwords("en"))           
```


```r
categorize_word <- function(word, categories) {
  for (category in names(categories)) {
    if (word %in% categories[[category]]) {
      return(category)
    }
  }
  return("Other") 
}

categorized_words <- tokenized_speeches %>%
  mutate(category = sapply(word, categorize_word, categories = categories))
```


```r
summary_by_category <- categorized_words %>%
  group_by(speaker, category) %>%
  summarise(word_count = n(), .groups = "drop") %>%
  arrange(speaker, desc(word_count))
```


```r
categorized_filtered <- categorized_words %>%
  filter(category != "Other")

proportions_by_category <- categorized_filtered %>%
  group_by(speaker, category) %>%
  summarise(word_count = n(), .groups = "drop") %>%
  group_by(speaker) %>%
  mutate(proportion = word_count / sum(word_count)) %>%
  arrange(speaker, desc(proportion))
```


```r
ggplot(proportions_by_category, aes(x = speaker, y = proportion, fill = category)) +
  geom_bar(stat = "identity", position = "stack") +
  scale_y_continuous(labels = scales::percent_format()) + 
  theme_minimal() +
  labs(
    title = "Proportion of Words by Category ",
    x = "Speaker",
    y = "Proportion of Words",
    fill = "Category"
  ) +
  theme(
    axis.text.x = element_text(angle = 45, hjust = 1),  
    legend.title = element_text(size = 12),             
    legend.text = element_text(size = 10)              
  )
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-8-1.png" width="672" />


```r
pivoted_table <- proportions_by_category %>%
  select(speaker, category, proportion) %>%  
  pivot_wider(
    names_from = category, 
    values_from = proportion,  
    values_fill = 0  
  )

kable(
  pivoted_table, 
  format = "html", 
  col.names = c("Speaker", "Economy", "Domestic Policy", "Foreign Policy", "Character"), 
  caption = "Proportion of Words by Speaker and Category (Excluding 'Other')",
  digits = 3  
) %>%
  kable_styling(bootstrap_options = c("striped", "hover", "condensed"), full_width = FALSE) %>%
  column_spec(1, bold = TRUE)
```

<table class="table table-striped table-hover table-condensed" style="width: auto !important; margin-left: auto; margin-right: auto;">
<caption><span id="tab:unnamed-chunk-9"></span>Table 1: Proportion of Words by Speaker and Category (Excluding 'Other')</caption>
 <thead>
  <tr>
   <th style="text-align:left;"> Speaker </th>
   <th style="text-align:right;"> Economy </th>
   <th style="text-align:right;"> Domestic Policy </th>
   <th style="text-align:right;"> Foreign Policy </th>
   <th style="text-align:right;"> Character </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;font-weight: bold;"> Gallego </td>
   <td style="text-align:right;"> 1.000 </td>
   <td style="text-align:right;"> 0.000 </td>
   <td style="text-align:right;"> 0.000 </td>
   <td style="text-align:right;"> 0.000 </td>
  </tr>
  <tr>
   <td style="text-align:left;font-weight: bold;"> Harris </td>
   <td style="text-align:right;"> 0.621 </td>
   <td style="text-align:right;"> 0.276 </td>
   <td style="text-align:right;"> 0.069 </td>
   <td style="text-align:right;"> 0.034 </td>
  </tr>
  <tr>
   <td style="text-align:left;font-weight: bold;"> Lake </td>
   <td style="text-align:right;"> 1.000 </td>
   <td style="text-align:right;"> 0.000 </td>
   <td style="text-align:right;"> 0.000 </td>
   <td style="text-align:right;"> 0.000 </td>
  </tr>
  <tr>
   <td style="text-align:left;font-weight: bold;"> Trump </td>
   <td style="text-align:right;"> 0.621 </td>
   <td style="text-align:right;"> 0.242 </td>
   <td style="text-align:right;"> 0.126 </td>
   <td style="text-align:right;"> 0.011 </td>
  </tr>
</tbody>
</table>


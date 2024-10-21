---
title: 'Post #7: State Level Predictions'
author: Avi Agarwal
date: '2024-10-21'
slug: super-ensembling-simulations
categories: []
tags: []
---






















































































































# Introduction

# National Two Party Vote Share

<table style="border-collapse:collapse; border:none;">
<caption style="font-weight: bold; text-align:left;">2024 Democrat Two Party Vote Share via Linear Regression</caption>
<tr>
<th style="border-top: double; text-align:center; font-style:italic; font-weight:normal; padding:0.2cm; border-bottom:1px solid black; text-align:left; ">Prediction</th>
<th style="border-top: double; text-align:center; font-style:italic; font-weight:normal; padding:0.2cm; border-bottom:1px solid black; ">Lower.Bound</th>
<th style="border-top: double; text-align:center; font-style:italic; font-weight:normal; padding:0.2cm; border-bottom:1px solid black; ">Upper.Bound</th>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; border-bottom: double; ">53.31%</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; border-bottom: double; ">46.57%</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; border-bottom: double; ">60.05%</td>
</tr>
</table>


# Linear Model


```
## [1] "In-sample MSE for Optimized LM Model: 1.77876259651781"
```

```
## [1] "Out-sample MSE for Optimized LM Model: 3.66463924611509"
```

<table style="border-collapse:collapse; border:none;">
<caption style="font-weight: bold; text-align:left;">Summary of Democrat Vote Share Model</caption>
<tr>
<td style=" text-align:center; border-bottom:1px solid; font-style:italic; font-weight:normal;nodv  text-align:left; ">Predictors</td>
<td style=" text-align:center; border-bottom:1px solid; font-style:italic; font-weight:normal;nodv  ">Estimates</td>
<td style=" text-align:center; border-bottom:1px solid; font-style:italic; font-weight:normal;nodv  ">std. Error</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">polling trend 7 3</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">0.25</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">0.10</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">polling trend 12 8</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">&#45;0.10</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">0.14</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">D pv2p lag1</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">0.46</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">0.12</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">D pv2p lag2</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">&#45;0.20</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">0.07</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">current week</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">0.24</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">0.08</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">incumbent party</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">&#45;1.08</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">1.07</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">dpi inflation adjusted</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">&#45;0.23</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">0.26</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">unemployment growth<br>quarterly</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">0.37</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">0.11</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">stateArizona</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">25.29</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">3.98</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">stateGeorgia</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">25.04</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">3.97</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">stateMichigan</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">28.68</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">4.66</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">stateNevada</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">27.04</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">4.37</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">stateNorth Carolina</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">24.75</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">4.16</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">stateWisconsin</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">28.87</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">4.73</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">statePennsylvania</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">28.40</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center;  ">4.65</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; padding-top:0.1cm; padding-bottom:0.1cm; border-top:1px solid;">Observations</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; padding-top:0.1cm; padding-bottom:0.1cm; text-align:left; border-top:1px solid;" colspan="2">46</td>
</tr>

</table>


<table style="border-collapse:collapse; border:none;">
<caption style="font-weight: bold; text-align:left;">LM Predictions</caption>
<tr>
<th style="border-top: double; text-align:center; font-style:italic; font-weight:normal; padding:0.2cm; border-bottom:1px solid black; text-align:left; ">State</th>
<th style="border-top: double; text-align:center; font-style:italic; font-weight:normal; padding:0.2cm; border-bottom:1px solid black; ">Dem.Vote</th>
<th style="border-top: double; text-align:center; font-style:italic; font-weight:normal; padding:0.2cm; border-bottom:1px solid black; ">Rep.Vote</th>
<th style="border-top: double; text-align:center; font-style:italic; font-weight:normal; padding:0.2cm; border-bottom:1px solid black; ">Dem.Margin</th>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">Arizona</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">49.71%</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">50.29%</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">-0.59%</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">Georgia</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">50.26%</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">49.74%</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">0.52%</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">Michigan</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">53.73%</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">46.27%</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">7.47%</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">Nevada</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">52.19%</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">47.81%</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">4.37%</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">North Carolina</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">49.44%</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">50.56%</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">-1.13%</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">Pennsylvania</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">53.06%</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">46.94%</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">6.11%</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; border-bottom: double; ">Wisconsin</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; border-bottom: double; ">53%</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; border-bottom: double; ">47%</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; border-bottom: double; ">6.01%</td>
</tr>
</table>


# Ensemble Model


```
## [1] "In-sample MSE for Ensemble Model (Democrat): 7.77770935294101"
```

```
## [1] "In-sample MSE for Ensemble Model (Republican): 4.80193656647045"
```


```
## [1] "Out-sample MSE for Ensemble Model (Democrat): 2.24877477301082"
```

```
## [1] "Out-sample MSE for Ensemble Model (Republican: 3.5026609257715"
```

<table style="border-collapse:collapse; border:none;">
<caption style="font-weight: bold; text-align:left;">Ensemble Predictions</caption>
<tr>
<th style="border-top: double; text-align:center; font-style:italic; font-weight:normal; padding:0.2cm; border-bottom:1px solid black; text-align:left; ">State</th>
<th style="border-top: double; text-align:center; font-style:italic; font-weight:normal; padding:0.2cm; border-bottom:1px solid black; ">Dem.Vote</th>
<th style="border-top: double; text-align:center; font-style:italic; font-weight:normal; padding:0.2cm; border-bottom:1px solid black; ">Rep..Vote</th>
<th style="border-top: double; text-align:center; font-style:italic; font-weight:normal; padding:0.2cm; border-bottom:1px solid black; ">Dem.Margin</th>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">Arizona</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">47.19%</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">52.81%</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">-5.62%</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">Georgia</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">47.62%</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">52.38%</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">-4.76%</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">Michigan</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">50.95%</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">49.05%</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">1.89%</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">Nevada</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">50.15%</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">49.85%</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">0.3%</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">North Carolina</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">46.66%</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">53.34%</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">-6.69%</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">Pennsylvania</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">51.15%</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">48.85%</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">2.29%</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; border-bottom: double; ">Wisconsin</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; border-bottom: double; ">51.07%</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; border-bottom: double; ">48.93%</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; border-bottom: double; ">2.14%</td>
</tr>
</table>


<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-59-1.png" width="672" />


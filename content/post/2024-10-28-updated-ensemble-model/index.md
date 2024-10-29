---
title: Updated Ensemble Model
author: Avi Agarwal
date: '2024-10-28'
slug: updated-ensemble-model
categories: []
tags: []
---







































```
##            [,1]
## [1,] 0.45206657
## [2,] 0.54984103
## [3,] 0.02857024
##           [,1]
## [1,] 0.7357583
## [2,] 0.1781891
## [3,] 0.1462848
##               [,1]
## [1,] -1.008197e-19
## [2,]  9.708179e-01
## [3,] -7.521749e-20
##           [,1]
## [1,] 0.1141483
## [2,] 0.3340155
## [3,] 0.5794384
##           [,1]
## [1,] 0.2115558
## [2,] 0.4861141
## [3,] 0.3223469
##               [,1]
## [1,] -9.931070e-20
## [2,]  4.545288e-02
## [3,]  1.000000e+00
##               [,1]
## [1,] -1.198229e-19
## [2,]  9.693694e-01
## [3,] -1.169093e-21
```


```
## [1] "Arizona"
## [1] 49.38116
## [1] 49.38116
## [1] "Georgia"
## [1] 47.33883
## [1] 47.33883
## [1] "Michigan"
## [1] 50.25262
## [1] 49.88233
## [1] "Nevada"
## [1] 51.29371
## [1] 51.29371
## [1] "North Carolina"
## [1] 48.09625
## [1] 48.09625
## [1] "Pennsylvania"
## [1] 50.34844
## [1] 49.62446
## [1] "Wisconsin"
## [1] 50.42181
## [1] 49.59201
```


```
## [1] "Arizona"
## [1] 48.53305
## [1] 48.30525
## [1] "Georgia"
## [1] 49.527
## [1] 50.11933
## [1] "Michigan"
## [1] 54.50334
## [1] 51.41356
## [1] "Nevada"
## [1] 55.05035
## [1] 51.22312
## [1] "North Carolina"
## [1] 49.19369
## [1] 49.31582
## [1] "Pennsylvania"
## [1] 56.5605
## [1] 50.58921
## [1] "Wisconsin"
## [1] 53.88811
## [1] 50.31906
```






```
## [1] 50.5873
## [1] 51.84354
## [1] 54.19823
## [1] 50.41905
## [1] 56.09717
## [1] 53.12924
## [1] 54.39335
```





























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

<table style="width: 50%;">
<caption style="font-weight: bold; text-align: center;">LM Model Predicted Vote Share</caption>
<tr>
<th style="border-top: double; text-align:center; font-style:italic; font-weight:normal; padding:0.2cm; border-bottom:1px solid black; text-align:left; ">state</th>
<th style="border-top: double; text-align:center; font-style:italic; font-weight:normal; padding:0.2cm; border-bottom:1px solid black; ">adj_dem_vote</th>
<th style="border-top: double; text-align:center; font-style:italic; font-weight:normal; padding:0.2cm; border-bottom:1px solid black; ">adj_rep_vote</th>
<th style="border-top: double; text-align:center; font-style:italic; font-weight:normal; padding:0.2cm; border-bottom:1px solid black; ">margin</th>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">Arizona</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">48.78</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">51.22</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">-2.43</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">Georgia</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">49.93</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">50.07</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">-0.14</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">Michigan</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">51.66</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">48.34</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">3.32</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">Nevada</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">51.69</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">48.31</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">3.38</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">North Carolina</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">49.03</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">50.97</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">-1.95</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">Pennsylvania</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">51.67</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">48.33</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">3.33</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; border-bottom: double; ">Wisconsin</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; border-bottom: double; ">51.76</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; border-bottom: double; ">48.24</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; border-bottom: double; ">3.51</td>
</tr>
</table>

<table style="width: 60%;">
<caption style="font-weight: bold; text-align: center;">In-Sample MSE for Democratic Predictions by Swing State (2020 Data)</caption>
<tr>
<th style="border-top: double; text-align:center; font-style:italic; font-weight:normal; padding:0.2cm; border-bottom:1px solid black; text-align:left; ">state</th>
<th style="border-top: double; text-align:center; font-style:italic; font-weight:normal; padding:0.2cm; border-bottom:1px solid black; ">mse_dem</th>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">Arizona</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">1.6159</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">Georgia</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">0.0000</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">Michigan</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">0.1371</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">Nevada</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">0.0000</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">North Carolina</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">0.0000</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">Pennsylvania</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">0.5241</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; border-bottom: double; ">Wisconsin</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; border-bottom: double; ">0.6886</td>
</tr>
</table>

<table style="width: 60%;">
<caption style="font-weight: bold; text-align: center;">In-Sample MSE for Democratic Predictions by Swing State (2020 Data)</caption>
<tr>
<th style="border-top: double; text-align:center; font-style:italic; font-weight:normal; padding:0.2cm; border-bottom:1px solid black; text-align:left; ">state</th>
<th style="border-top: double; text-align:center; font-style:italic; font-weight:normal; padding:0.2cm; border-bottom:1px solid black; ">mse_dem</th>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">Arizona</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">2.6367</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">Georgia</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">0.3509</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">Michigan</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">9.5468</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">Nevada</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">14.6477</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">North Carolina</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">0.0149</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">Pennsylvania</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">35.6564</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; border-bottom: double; ">Wisconsin</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; border-bottom: double; ">12.7381</td>
</tr>
</table>

<table style="width: 50%;">
<caption style="font-weight: bold; text-align: center;">Ensemble Model Predicted Vote Share</caption>
<tr>
<th style="border-top: double; text-align:center; font-style:italic; font-weight:normal; padding:0.2cm; border-bottom:1px solid black; text-align:left; ">state</th>
<th style="border-top: double; text-align:center; font-style:italic; font-weight:normal; padding:0.2cm; border-bottom:1px solid black; ">adj_dem_vote</th>
<th style="border-top: double; text-align:center; font-style:italic; font-weight:normal; padding:0.2cm; border-bottom:1px solid black; ">adj_rep_vote</th>
<th style="border-top: double; text-align:center; font-style:italic; font-weight:normal; padding:0.2cm; border-bottom:1px solid black; ">margin</th>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">Arizona</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">49.21</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">50.79</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">-1.58</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">Georgia</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">49.41</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">50.59</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">-1.17</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">Michigan</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">48.96</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">51.04</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">-2.08</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">Nevada</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">51.22</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">48.78</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">2.43</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">North Carolina</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">46.47</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">53.53</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">-7.06</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; ">Pennsylvania</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">49.35</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">50.65</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; ">-1.30</td>
</tr>
<tr>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:left; border-bottom: double; ">Wisconsin</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; border-bottom: double; ">48.90</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; border-bottom: double; ">51.10</td>
<td style=" padding:0.2cm; text-align:left; vertical-align:top; text-align:center; border-bottom: double; ">-2.21</td>
</tr>
</table>

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-40-1.png" width="672" />


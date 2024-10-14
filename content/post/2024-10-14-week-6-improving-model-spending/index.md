---
title: 'Week #6: Improving Electoral College Model'
author: 'Avi '
date: '2024-10-14'
slug: week-6-improving-model-spending
categories: []
tags: []
---













































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


```
## function (database = "world", regions = ".", exact = FALSE, boundary = TRUE, 
##     interior = TRUE, projection = "", parameters = NULL, orientation = NULL, 
##     fill = FALSE, col = 1, plot = TRUE, add = FALSE, namesonly = FALSE, 
##     xlim = NULL, ylim = NULL, wrap = FALSE, resolution = if (plot) 1 else 0, 
##     type = "l", bg = par("bg"), mar = c(4.1, 4.1, par("mar")[3], 
##         0.1), myborder = 0.01, namefield = "name", lforce = "n", 
##     ...) 
## {
##     if (resolution > 0 && !plot) 
##         stop("must have plot=TRUE if resolution is given")
##     if (!fill && !boundary && !interior) 
##         stop("one of boundary and interior must be TRUE")
##     doproj <- !missing(projection) || !missing(parameters) || 
##         !missing(orientation)
##     if (doproj && !requireNamespace("mapproj", quietly = TRUE)) {
##         stop("Please install the package 'mapproj' for projections.")
##     }
##     coordtype <- maptype(database)
##     if (coordtype == "unknown") 
##         stop("missing database or unknown coordinate type")
##     if (doproj && coordtype != "spherical") 
##         stop(paste(database, "database is not spherical; projections not allowed"))
##     if (length(wrap) >= 2 && !doproj && wrap[2] - wrap[1] != 
##         360) 
##         stop("The specified longitudes for wrapping are inconsistent, they should be 360 apart.")
##     if (is.character(database)) 
##         as.polygon = fill
##     else as.polygon <- TRUE
##     xlim_tmp <- if (length(wrap) >= 2) 
##         NULL
##     else xlim
##     coord <- map.poly(database, regions, exact, xlim_tmp, ylim, 
##         boundary, interior, fill, as.polygon, namefield = namefield)
##     if (is.na(coord$x[1])) 
##         stop("first coordinate is NA. Bad map data?")
##     if (length(wrap) >= 2) {
##         antarctica <- if (length(wrap) == 2) 
##             -89.9
##         else wrap[3]
##         coord <- map.wrap.poly(coord, xlim = wrap[1:2], poly = fill, 
##             antarctica = antarctica)
##     }
##     if (lforce == "e") {
##         coord <- map.clip.poly(coord, xlim, ylim, poly = fill)
##     }
##     if (plot) {
##         .map.range(coord$range)
##     }
##     if (doproj) {
##         nam <- coord$names
##         coord <- mapproj::mapproject(coord, projection = projection, 
##             parameters = parameters, orientation = orientation)
##         coord$projection = projection
##         coord$parameters = parameters
##         coord$orientation = orientation
##         coord$names <- nam
##         if (!is.null(xlim) && !is.null(ylim) && lforce %in% c("s", 
##             "l")) {
##             prange <- mapproj::mapproject(x = rep(xlim, 2), y = rep(ylim, 
##                 each = 2))
##             if (lforce == "s") {
##                 xlim <- c(max(prange$x[c(1, 3)]), min(prange$x[c(2, 
##                   4)]))
##                 ylim <- c(max(prange$y[c(1, 2)]), min(prange$y[c(3, 
##                   4)]))
##             }
##             else {
##                 xlim <- c(min(prange$x[c(1, 3)]), max(prange$x[c(2, 
##                   4)]))
##                 ylim <- c(min(prange$y[c(1, 2)]), max(prange$y[c(3, 
##                   4)]))
##             }
##         }
##         if (plot && coord$error) 
##             if (all(is.na(coord$x))) 
##                 stop("projection failed for all data")
##             else warning("projection failed for some data")
##     }
##     if (length(wrap) == 1 && wrap) 
##         coord <- map.wrap(coord)
##     if (plot) {
##         if (!add) {
##             opar = par(bg = bg)
##             if (!par("new")) 
##                 plot.new()
##             if (is.null(xlim) || (doproj && !(lforce %in% c("s", 
##                 "l")))) 
##                 xrange <- range(coord$x, na.rm = TRUE)
##             else xrange <- xlim
##             if (is.null(ylim) || (doproj && !(lforce %in% c("s", 
##                 "l")))) 
##                 yrange <- range(coord$y, na.rm = TRUE)
##             else yrange <- ylim
##             if (coordtype != "spherical" || doproj) {
##                 aspect <- c(1, 1)
##             }
##             else aspect <- c(cos((mean(yrange) * pi)/180), 1)
##             d <- c(diff(xrange), diff(yrange)) * (1 + 2 * myborder) * 
##                 aspect
##             if (coordtype != "spherical" || doproj) {
##                 plot.window(xrange, yrange, asp = 1/aspect[1])
##             }
##             else {
##                 par(mar = mar)
##                 p <- par("fin") - as.vector(matrix(c(0, 1, 1, 
##                   0, 0, 1, 1, 0), nrow = 2) %*% par("mai"))
##                 par(pin = p)
##                 p <- par("pin")
##                 p <- d * min(p/d)
##                 par(pin = p)
##                 d <- d * myborder + ((p/min(p/d) - d)/2)/aspect
##                 usr <- c(xrange, yrange) + rep(c(-1, 1), 2) * 
##                   rep(d, c(2, 2))
##                 par(usr = usr)
##             }
##             on.exit(par(opar))
##         }
##         if (type != "n") {
##             if (!as.polygon && resolution != 0) {
##                 pin <- par("pin")
##                 usr <- par("usr")
##                 resolution <- resolution * min(diff(usr)[-2]/pin/100)
##                 coord[c("x", "y")] <- mapthin(coord, resolution)
##             }
##             if (fill) 
##                 polygon(coord, col = col, ...)
##             else lines(coord, col = col, type = type, ...)
##         }
##     }
##     class(coord) = "map"
##     value <- if (namesonly) 
##         coord$names
##     else coord
##     if (plot) 
##         invisible(value)
##     else value
## }
## <bytecode: 0x0000013edd205b18>
## <environment: namespace:maps>
```


# Future Improvements

While this model shows significant improvement from last week, I plan to test several changes in the coming weeks to enhance its accuracy. I intend to experiment with an elastic net model using imputed data to see if that offers a better method for incorporating polling data. I will also explore modeling various economic fundamentals to create a more nuanced measure of economic effects in this election.

While campaign fundraising is a useful indicator of public support, strong data for 2024 are not yet available, making it difficult to make meaningful predictions in this area. However, I may also attempt to incorporate it into the model next week.






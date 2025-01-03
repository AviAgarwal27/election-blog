---
title: 'Post #1: Defining the Swing States'
author: Avi Agarwal
date: '2024-09-09'
slug: post-1
categories: []
tags: []
---



























## Introduction

This is the first of a series of blog posts in which I will analyze and predict the 2024 Presidential Election. In my first post, I will analyze historical data from past presidential elections to determine how competitive presidential elections are, what states can be seen as reliable for either party, while what states are considered swing states.

## What states are competitive?

To begin, I will examine the vote margins for each state in the Democratic and Republican parties' presidential elections from 2000 to 2020. A brief overview shows that even the most partisan states had relatively close margins. Excluding D.C., every state was within 30 percentage points, and most were within 15 points. However, under the U.S. Electoral College system, whether state margins are 80-20 or 52-48, if they consistently vote for the same party, the margin does not affect the overall election outcome. The only states that genuinely impact the result are those with razor-thin margins capable of switching sides, and these states tend to be nearly white on the electoral map below.


<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-10-1.png" width="960" />

Certain swing states in 2000 and subsequent elections have trended towards one party, removing them from contention. Ohio and Iowa now lean Republican, while New Mexico, Oregon, and Minnesota lean Democratic. Texas appears to be inching toward swing state status but remains solidly Republican. Virginia presents an interesting case, having shifted from reliably red to reliably blue during this period.

Pennsylvania, Wisconsin, Nevada, and Michigan have consistently been swing states throughout this period, including the most recent election. Conversely, Arizona, Georgia, and North Carolina have shifted from being reliably Republican to competitive. Florida is difficult to gauge; while its vote margins suggest swing state status, recent election results resemble those of more consistently red states like Iowa or Texas. Therefore, we'll reserve judgment until further analysis of more recent maps.

## Swing Map #1: 2016 vs. 2020

This map examines the change in vote margins in each state between 2016 and 2020. As expected, most of the map is blue since a Republican won in 2016 but lost in 2020. However, a few noteworthy trends emerge. First, while much of the country shifted towards the Democrats, Florida moved further towards the Republicans. In my opinion, this shift is significant enough to remove Florida's status as a swing state. Florida moved towards a Republican candidate even as Republicans underperformed nationwide.

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-11-1.png" width="864" />

Another interesting point is that New York and California, two Democratic strongholds, also trended Republican. These two states represent major electoral college strongholds for the Democrats. Many argue that recent trends make it unlikely for Democrats to lose the popular vote but still win the Electoral College. While this is mainly true, if these states continue to trend Republican, it could become possible in future elections.

## Swing Map #2: 2012 vs. 2020

While the map comparing vote margins from 2016 to 2020 is interesting, there isn’t much detailed analysis to draw from it, as most of the country swung in favor of the party shift. A more fascinating comparison comes from looking at the 2012 and 2020 presidential elections, where Democratic candidates won both times. However, it’s important to note that the 2012 election was a more decisive victory for the Democrats. Obama won 126 more electoral votes than Romney, while Biden only won 74 more than Trump.

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-12-1.png" width="864" />

This map supports earlier analysis. Arizona and Georgia stand out as they have become far more competitive for the Democratic Party, evolving into swing states. Conversely, Ohio, Iowa, and Florida have trended more Republican and are no longer considered swing states. Many traditional swing states in the Midwest and Nevada trended Republican, though this is expected, given that Obama won more significantly than Biden.

Utah has become significantly more Democratic-leaning, though it remains far from becoming a swing state. Texas has also shifted noticeably toward the Democrats during this period, signaling its potential move toward swing state status. Interestingly, some reliably red states like Kansas and Idaho have trended more Democratic, while others, like North Dakota and West Virginia, have become significantly more Republican. I don't have a strong theory for why some traditionally Republican states shifted in opposite directions beyond basic immigration patterns.

## Concluding Thoughts

Overall, it seems safe to conclude that U.S. elections remain highly competitive, even in states reliably aligned with a particular party. Based on historical data, I’ve identified the likely swing states for the upcoming election:
  - Arizona
  - Nevada
  - Georgia
  - Wisconsin
  - Michigan
  - Pennsylvania
  - North Carolina

Of course, more recent polling may suggest a different set of states, and I look forward to refining this list and eventually predicting the winner in each as I update my model. Thanks for reading!


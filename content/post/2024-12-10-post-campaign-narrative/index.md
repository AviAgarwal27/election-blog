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














# Background on Arizona

Arizona [is](https://www.britannica.com/place/Arizona-state) a southwestern state with most of its population concentrated in two cities. Phoenix, the capital and largest city, is centrally located and surrounded by numerous suburbs. Tucson, a much smaller city, lies to the south but is still far from the Mexican border. Both cities are in an arid desert climate dominated by the Sonoran Desert, home to the iconic saguaro cactus. The northern part of the state features coniferous forests, although only a small portion of the population resides there.

White people make up the plurality of Arizona voters, but the state also has a significant Latinx population, as noted in the [2020 census](https://data.census.gov/profile/Arizona?g=040XX00US04#race-and-ethnicity). Additionally, Arizona is home to many Indigenous peoples, with the largest reservations by land area in the United States.

Due to its proximity to the border, immigration is a [key](https://www.arizonafuture.org/the-arizona-we-want/arizona-voters-agenda/results/#anchorEnvironment) issue for Arizona voters. Other uniquely significant concerns include education, as Arizona has one of the worst public education systems in the country and water access, given the decades-long drought affecting the state. While the economy is also a significant concern, Arizonans' perspectives may differ from national views due to inflation rates in the state being [much higher](https://grandcanyontimes.com/stories/665259888-arizona-experiences-higher-inflation-rate-than-national-average-as-of-september-2024) than the national average in recent years.

Arizona’s shift into a swing state is a relatively [recent development](https://ballotpedia.org/Arizona). Until the 2016 election, Arizona was considered a reliably Republican state in both state and federal elections. However, changing demographics and the state’s rapid population growth began to loosen the Republican Party’s hold, turning Arizona increasingly purple. The first significant signs of this shift emerged in the 2018 midterm elections. Moderate Republican Senator Jeff Flake chose not to seek reelection, [citing](https://www.azcentral.com/story/news/politics/arizona/2017/10/24/why-senator-jeff-flake-says-he-wont-run-drops-out-race-trump-gop-politics/795497001/) his diverging views with the Republican Party. In the wake of a nationwide wave of Democratic victories, Kyrsten Sinema, a former State Representative, won Flake’s Senate seat, paving the way for Democrats to contest statewide races in the Grand Canyon State.

This trend continued in 2020 when Democrats achieved a series of statewide victories. Joe Biden became the first Democratic presidential candidate to win Arizona’s electoral votes since Bill Clinton in 1996. The special election for the late Senator John McCain’s seat also resulted in a Democratic win, with former astronaut Mark Kelly defeating his Republican opponent. The momentum carried into 2022, when Democrats won the governorship, Kelly secured a full six-year Senate term, and other key statewide offices, such as Secretary of State, also flipped to Democratic control.

In 2024, several crucial races were on the ballot beyond the presidential contest. These included a high-profile Senate race between Republican news anchor and Trump ally Kari Lake and Democratic Representative Ruben Gallego, vying for Kyrsten Sinema’s seat. Additionally, a ballot measure aimed at enshrining access to abortion was up for a vote. There were also [two competitive House races](https://www.cookpolitical.com/ratings/house-race-ratings), AZ-01 and AZ-06, both held by incumbent Republicans.

# Forecasts vs. Reality

## My Prediction

Arizona was one of the seven swing states I predicted, and one of only three where I correctly forecasted a Trump victory. While I still overestimated Harris’ support, my prediction was off by only around 0.5 percentage points—quite close to the actual result. I had anticipated Trump to win Arizona by the widest margin compared to the other swing states, which also proved to be true. Despite the shortcomings of my predictions in the Midwest, Arizona stood out as a success.

It’s worth noting how I derived my prediction for Arizona. The weights for my Arizona model were unique, with polling-based variables accounting for 97% of the prediction, fundamentals contributing just 3%, and the combined model receiving no weight at all. This is likely because lagged vote share, which heavily influences both the fundamentals and combined models, is a poor predictor for Arizona. The state’s significant demographic shifts and its recent emergence as a swing state render polling the most reliable measure for forecasting Arizona’s outcomes in my model. Thus, while my model correctly anticipated that polls are the best predictor for Arizona, the accuracy of the polls can be attributed to my predictions alignment with reality.

## Expert Predictions

Many expert predictions also correctly forecasted the result in Arizona. [Sabato’s Crystal Ball](https://centerforpolitics.org/crystalball/2024-president/) categorized Arizona as “Leans R,” while mainstream prediction platforms like [FiveThirtyEight](https://projects.fivethirtyeight.com/2024-election-forecast/), [The Economist](https://www.economist.com/interactive/us-2024-election/prediction-model/president), and The [Silver Bulletin](https://www.natesilver.net/p/nate-silver-2024-president-election-polls-model) all projected Trump as more likely to win the state.

Like my prediction, these forecasts were likely influenced by polling data leading up to election day, which generally showed Trump [ahead](https://www.realclearpolling.com/polls/president/general/2024/arizona/trump-vs-harris) by 1–2 points—a relatively comfortable margin compared to other swing states, where polls indicated less than a one-point difference.

# Evaluation of the Campaigns

From the beginning of her campaign in late July to election day, Harris [visited](https://www.azcentral.com/story/news/politics/elections/2024/10/07/trump-harris-visits-arizona-campaign/75483822007/) Arizona four times, matched by Trump with the same number of visits. However, Harris held a [spending edge](https://www.opensecrets.org/states/AZ/presidential/2024), allocating $17 million compared to Trump’s $12 million.

While these statistics are noteworthy, they provide little insight into the messaging strategies of each campaign, and even less about their effectiveness. To address this gap, I conducted a brief study using text analysis of speeches given by both presidential candidates. I focused on Arizona due to its unique dynamic: like three other swing states, Arizona elected a Democratic senator despite Trump winning the state’s electoral votes. This is particularly intriguing because Kari Lake, the Republican candidate, closely aligned herself with Trump’s brand, while Ruben Gallego, the Democrat, positioned himself as a moderate—similar to Harris during her campaign.

To explore why these results diverged so significantly, I analyzed equivalent campaign events where both the presidential and senatorial candidates spoke, searching for noticeable differences in messaging.

For this analysis, I selected two comparable campaign events. For the Democrats, I used Harris’s [October 31 rally](https://www.youtube.com/watch?v=81bu2cqav6o), her final visit to Arizona, where she delivered a 24-minute speech following a 6.5-minute introduction by Gallego. For the Republicans, I examined the [October 24 rally](https://www.youtube.com/watch?v=9BdBvztQCdU&t=5s) where [Lake introduced](https://www.youtube.com/watch?v=eL4LhTnWiWk) Trump with a similarly timed 6.5-minute speech, followed by Trump’s iconic “weave,”lasting over 50 minutes. The primary distinction between the two events was that Trump made one additional visit to Arizona, but that event was not suitable for this analysis as it was a conversational interview with Tucker Carlson rather than a campaign rally.

To analyze these speeches, I first downloaded the auto-generated transcripts from YouTube recordings of each speech. After processing the transcripts, I categorized every word into one of five groups: “economy,” “foreign policy,” “domestic policy,” “character,” and “other.”

* The "economy" category included words like “inflation” or “jobs.”
* "Foreign policy" encompassed country names and defense-related terms.
* "Domestic policy" focused on issues like “immigration,” “healthcare,” and “climate change.”
* "Character" included negative attributes assigned to political rivals.
* "Other" comprised words that didn’t fit into any of the above categories and were excluded from the analysis.

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-8-1.png" width="672" />
The graph above charts the proportion of total speech content falling into each category. Focusing first on the presidential candidates, their distributions of words across the categories were strikingly similar. While Harris spoke slightly more about negative character traits and slightly less about foreign policy, the overall similarity between the two speeches was surprising.

Similarly, Lake and Gallego’s speeches exhibited an almost identical distribution, though distinct from their presidential counterparts. Given the brevity of their speeches—each lasting under ten minutes—it is difficult to compare them directly to the much longer presidential addresses. However, it is noteworthy that neither candidate mentioned the word “economy” during their combined 15 minutes of speaking time. Instead, both exclusively focused on issues related to domestic policy.

<table class="table table-striped table-hover table-condensed" style="width: auto !important; margin-left: auto; margin-right: auto;">
<caption><span id="tab:unnamed-chunk-9"></span>Table 1: Proportion of Words by Topic Area</caption>
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
# Deviations from the Forecasted Outcome

While the analysis above has several flaws, such as limitations in YouTube’s transcription algorithm or potentially insufficiently comprehensive dictionaries, it raises an interesting theory about why the results turned out as they did. According to [Professor Vavreck’s theories on campaign types](https://academic.oup.com/poq/article-abstract/74/3/585/1913810), Trump should have been running a clarifying campaign that highlighted flaws in the economy, while Harris should have focused more on a singular divergent issue. The basic analysis suggests that Harris ended up speaking about economic issues just as much as Trump.


Although one could argue that the text analysis also indicates Trump didn’t emphasize economic issues enough, his resounding victory in the swing state leads me to believe his campaign strategy was effective. Conversely, Harris may have strayed off course—though proving the counterfactual is impossible. On the other hand, a lack of focus on the economy may have contributed to Lake’s downfall in the Senate race, as she completely neglected the topic in her brief speech, while Gallego rightly avoided it. The contrasting focus on the economy in the Senate race versus the presidential race might have played a role in why these contests ended up favoring different parties.

Overall, most forecasts correctly predicted the winner in Arizona, likely due to the relatively low polling error compared to other swing states. Trump was projected to win by a margin of over 1 point, which aligned with the final result. Arizona seemed to play a smaller role in this election compared to 2020, given its consistent lean toward Trump—a fact both campaigns likely recognized, as they devoted more time to the “Blue Wall” states than to Arizona. While Arizona’s significance in the 2028 election remains uncertain, it is clear that its [shifting demographics](https://www.prb.org/resources/latinos-whites-and-the-shifting-demography-of-arizona/) and evolving political landscape will continue to make it a fascinating state to watch.


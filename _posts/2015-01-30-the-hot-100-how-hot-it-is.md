---
title: "Exploring the Hot 100: How Hot Can it Be?"
excerpt: "This post explores explonatory data analysis of the top 100 songs for the year 2000"
header:
  overlay_image: hot100_5.jpg
  overlay_filter: 0.4
  caption: ""
  cta_label: " "
categories:
  - data science
tags:
  - EDA
  - analysis
  - billboard
  - time series
  - bubble charts
author: "Marina Drus"
date: "1 October 2016"
---

{% include base_path %}

### Introduction

The Billboard charts are the United States music industry standard popularity ranking issued weekly by Billboard magazine.  The Billboard charts rank songs relative to each other. The ranking is based on radio plays and sales (both physical and digital) data monitored by Nielsen Music, which electronically monitors radio stations in more than 140 markets across the United States. 

The goal of this project was to perform an explanatory data analysis using the billboard data of 2000. The billboard data is interesting in terms of its unique structure and introduces some minor challenges for data cleaning. To analyze the 2000 chart, the data structure was reshaped using pd.melt() function. Specifically, multiple columns indicating a number of weeks in chart and peak position were transformed into only 2 columns. For the details, please see [the python code](https://github.com/dmarinav/My_Projects/blob/master/Billboard100.ipynb).


### Explanatory Data Analysis 

During the year of 2000, 317 songs entered and existed the billboard chart. As indicated by the wordcloud graph below, the most prominent words in the song titles were “love”, “wanna”, “baby”, “girl”, “God”, “friend”, “heart”, “need” and so on. Unsurprisingly (or maybe surprisingly) it was all about love, and love was definitely in the air. That is, most of the songs’ titles contained the magic word LOVE.


![Count of Songs by Genre]({{ site.url }}{{ site.baseurl }}/images/pic1_1.png) 


I tried to find benchmark categories that can help me group and relate my data in order to extract the maximum amount of information. Finding the benchmark categories is extremely important for detecting a trend in data. For this reason, most of the data was grouped and explored by genre. Out of 317 songs, there were 137 rock songs, 74 country songs, 58 rap songs, 23 R&B songs, 9 pop songs, 9 Latin songs, 1 reggae song, 1 jazz song, and 1 gospel song. That makes sense as rock was the most popular genre in the U.S. in 2000. 


![Wordcloud of Tracks' Names]({{ site.url }}{{ site.baseurl }}/images/pic1_2.png) 


The average track length also varied by genre. While length of most tracks ranged from 200 seconds to 280 seconds long; jazz, gospel, electronic, and reggae had the highest average tack length. It is hard to say, however, whether it is a general trend since the chart contains only a few songs of these specific genres. 


![Track Length]({{ site.url }}{{ site.baseurl }}/images/pic1_3.png)


A typical boxplot displays information of a statistical data set in regards to its shape, variability, and median (middle of the data range). Below is a boxplot of peak position by genre. Note this plot is composed of an average peak position for each song—that is why you won’t see the top whiskers reaching the very peak position. A typical peak position was the highest for rock and jazz followed by Latin and pop. However, only rock songs had the highest variability among its peak positions. They had the highest and the lowest average peak position. In other words, rock songs in the year of 2000 either rocked or sucked (sorry, I could not help but rhyme here). 


![Boxplot of Peak Position]({{ site.url }}{{ site.baseurl }}/images/pic1_4.png)


The next logical step was to show a relationship between peak position and a number of days it takes each song to reach the peak position. The bubble chart below explores this relationship by genre and track length. In the chart, track length is proportional to the bubble area. It takes around 120 days for most songs to reach their peak positions. Rock songs take the highest average peak positions in the chart, followed by rap and Latin music. 

In general, as noted above, rock songs’ average peak positions had the highest variability. Country, jazz, pop, electronica, gospel, R&B, and reggae songs rarely reached the highest peak positions or stayed at the highest peak positions for a long time. It is obvious from the chart that the track length did not affect neither the number of days it takes to reach peak positions nor the peak position itself. While most songs reached their peak positions within 120-200 days, there were several exceptions. Those songs were Amazed by Lonestar (273 days), Kryptonite by 3 Doors Down (217 days), Sexual by Amber (210 days), and Higher by Creed (316 days).


![Bubble Chart]({{ site.url }}{{ site.baseurl }}/images/pic1_5.png)


The time series plot below indicates that rock and country followed by rap genre stayed in the billboard chart longer than other genres. They also take to peak later than other genres. Pop and Latin music reaches their peak positions sooner but also exists the chart sooner than rock, country, and rap. It is hard to make definite conclusion about reggae, R&B, jazz, and gospel as the number of songs reflecting these genres which entered the chart in 2000 is limited. 


![Time Series]({{ site.url }}{{ site.baseurl }}/images/pic1_6.png)


Finally, I looked at the number of days to reach peak position by month entered the chart. There has been an obvious trend that partially makes sense. Songs that entered the chart in December, March, and February reached their peak position sooner than songs that entered at other months. December is a holiday month so people are in the holiday mood to listen the music. There is a Grammy Award in February, so February has a plausible explanation as well. However, it is not that obvious what is so special about March. If you have an idea, send me an email. I would love to know. 


![Month Entered the Chart]({{ site.url }}{{ site.baseurl }}/images/pic1_6.png)


### Conclusion












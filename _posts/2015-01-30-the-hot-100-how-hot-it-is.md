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
  - histogram
  - charts
author: "Marina Drus"
date: "1 October 2016"
---

{% include base_path %}

Introduction
-------

The Billboard charts are the United States music industry standard popularity ranking issued weekly by Billboard magazine.  The Billboard charts rank songs relative to each other. The ranking is based on radio plays and sales (both physical and digital) data monitored by Nielsen Music, which electronically monitors radio stations in more than 140 markets across the United States. The goal of this project was to perform an explanatory data analysis using the billboard data of 2000. The billboard data is interesting in terms of its unique structure and introduces some minor challenges for data cleaning. To analyze the 2000 chart, the data structure was reshaped using pd.melt() function. Specifically, multiple columns indicating a number of weeks in chart and peak position were transformed into only 2 columns. For the details, please see [the python code](https://github.com/dmarinav/My_Projects/blob/master/Billboard100.ipynb).
-------

Explanatory Data Analysis 

During the year of 2000, 317 songs entered and existed the billboard chart. As indicated by the wordcloud graph below, the most prominent words in the song titles were “love”, “wanna”, “baby”, “girl”, “God”, “friend”, “heart”, “need” and so on. Unsurprisingly (or maybe surprisingly) it was all about love, and love was definitely in the air. That is, most of the songs’ titles contained the magic word LOVE.

![Count of Songs by Genre]({{ site.url }}{{ site.baseurl }}/images/pic1_1.png) 

I tried to find benchmark categories that can help me group and relate my data in order to extract the maximum amount of information. Finding the benchmark categories is extremely important for detecting a trend in data. For this reason, most of the data was grouped and explored by genre. Out of 317 songs, there were 103 rock songs, 74 country songs, 58 rap songs, 34 rock’n’roll songs, 23 R&B songs, 9 pop songs, 9 Latin songs, 1 reggae song, 1jazz song, and 1 gospel song. 

![Wordcloud of Tracks' Names]({{ site.url }}{{ site.baseurl }}/images/pic1_2.png) 

The average track length also varied by genre. While length of most tracks ranged from 200 seconds to 280 seconds long; jazz, gospel, electronic, and reggae had the highest average tack length. It is hard to say, however, whether it is a general trend since the chart contains only a few songs of these specific genres.

![Track Length]({{ site.url }}{{ site.baseurl }}/images/pic1_3.png)

A typical boxplot displays information of a statistical data set in regards to its shape, variability, and median (middle of the data range). Below is a boxplot of peak position by genre. Note this plot is composed of an average peak position for each song—that is why you won’t see the top whiskers reaching the very peak position. A typical peak position was the highest for rock’n’roll followed by jazz, Latin, and rock. However, rock songs had the highest variability among its peak positions. They had the highest and the lowest average peak position. In other words, rock songs in the year of 2000 either rocked or sucked (sorry, I could not help but rhyme here).

![Boxplot of Peak Position]({{ site.url }}{{ site.baseurl }}/images/pic1_4.png)







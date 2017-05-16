---
title: "Predicting Match at First Sight"
excerpt: "The post predicts love at first sight for speed dating participants at Columbia University"

header:
  overlay_image: speed2.jpg
  overlay_filter: 0.4
  caption: " "
  cta_label: "Next Post"
  cta_url: "https://dmarinav.github.io/data%20science/the-hot-100-how-hot-it-is/"
categories:
  - data science
tags:
  - classification algorithms
  - binary classification 
  - Kuggle competition
  - SMOT
  - feature selection
author: "Marina Drus"
date: "15 November 2017"
---

{% include base_path %}

### Introduction

For this project, I selected data from the [Kaggle Speed Dating Experiment]( https://www.kaggle.com/annavictoria/speed-dating-experiment).  Feeling a nostalgia for social psychology, I thought this data was a perfect representative of social science research. It was compiled by Columbia Business School professors Ray Fisman and Sheena Iyengar.The data “was gathered from participants in experimental speed dating events from 2002-2004. During the events, the attendees would have a four minute "first date" with every other participant of the opposite sex. At the end of their four minutes, participants were asked if they would like to see their date again. They were also asked to rate their date on six attributes: Attractiveness, Sincerity, Intelligence, Fun, Ambition, and Shared Interests.”

In addition, the dataset included data collected at different points in time. In addition, demographics, dating habits, self-perception across key attributes, beliefs on what others find valuable in a mate, and lifestyle information were collected. See the [Speed Dating Data Key document] for details (click on View Raw to see the key).

The features were assessed at Time 1 (before and right after participating in the event), Time 2 (the day after participating in the event), and Time 3 (3-4 weeks after participating in the event). I only used data from Time 1 since it was relevant to my model, and I wanted to predict the probability of leaving the event with a match. My project has 4 parts: 1) Data Cleaning, 2) EDA, 3) Feature selection, and 4) Model selection.

My hypothesis was to find out what influences love at first sight and whether participants would leave speed dating event with a match. Because of gender differences in partner selection (Fisman, Raymond, et al., 2006), my decision was to build two models: model for males and model for females with dependent variable "match.” The first model predicted a probability of finding a match for females while the second model predicted a probability of finding a match for females. 


#### Explanatory Data Analysis


The goal of the explanatory data analysis (EDA) was to investigate demographic data and highlight gender differences in mate selection.


[![Histogram]({{ site.url }}{{ site.baseurl }}/images/pic6_1.png)]({{ site.url }}{{ site.baseurl }}/images/pic6_1.png)


As we can see from the histogram, most female were in the age group of 18-25, and most males were in the age goup of 25-40. However, there was one male of 43 y.o. and one female of 55 y.o.

As shown below, most participants were European Americans, followed by Asian Americans, Hispanic Americans, others, and African Americans, respectively. There were approximately the same amount males and females in each race group.


[![Count of Race]({{ site.url }}{{ site.baseurl }}/images/pic6_2.png)]({{ site.url }}{{ site.baseurl }}/images/pic6_2.png)


Furthermore, there were some gender differences in fun activities.  Males were more interested in sports, TV sports, and gaming while females preferred yoga, watching TV, theater, shopping, dining concerts, and art. Both genders liked reading, music, movies, hiking, exercise, and clubbing. 
 

[![Diff in Fun Activities]({{ site.url }}{{ site.baseurl }}/images/pic6_3.png)]({{ site.url }}{{ site.baseurl }}/images/pic6_3.png)


In spite of the gender differences, both genders equally value funny, intelligent, sincere partners who share their interests. However, as shown below, males are more likely to value attractive females, while females are more likely to value ambitious males. 


[![Diff in Fun Activities]({{ site.url }}{{ site.baseurl }}/images/pic6_4.png)]({{ site.url }}{{ site.baseurl }}/images/pic6_4.png)


This EDA showed that there are gender differences in fun activities and mate selection. Thus, it is crucial to build two different models predicting speed dating match: 1) model for males, 2) model for females. Different features predicting match for males vs. females can affect predictive accuracy of models.


#### Feature Selection

Feature selection methods are important to create accurate predictive models. They help to choose features that will provide the best possible model fit with less data. The feature extraction process here was divided onto two parts. For feature extraction, I used four different learning methods: 1). Random Forest Classifier, 2). Adaptive Boosting Classifier, 3). Gradient Boosting Classifier, 4). Decision Tree Classifier. 

In Part I (preliminary feature extraction process), I investigated separate effects of continuous and categorical features on dependent variable. Some of the categorical features consisted of over 100 categories,  there were around 60 continuous features in the dataset at Time1. Because categorical features with many categories tend to mask the effect of other variable on dependent variable, to avoid the masking effect, I preliminary ran two feature selection models: 1) a model with the continuous features, and 2) a model with categorical features. After I selected most important continuous features and most important categorical features, I implemented Part II of my feature selection process. See the python code and output [here].

In Part II (final feature extraction process), I combined most important continuous and categorical features that was extracted in Part 1, and ran another feature selection model using the selected features. The features from the final feature extraction process for my final model were selected in the way to produce the highest accuracy score across various machine learning algorithms covered in the next section, Model Selection.

To select features, I used social science theories and feature selection methods in machine learning. Fist, in order for a participant to find a match, the participant should like his/her speed dating partner. The data did not contain the evaluation of the qualities of a given speed dating partner by the participant, however, it included participant’s decision about his/her speed dating (whether the participant would like to see he/her again). Thus, I used decision of the participant in my model (dec) to evaluate whether the participant likes his/her speed dating partner. The data also contained an evaluation of the participant’s qualities by the speed dating partner, demographics of the participant and his/her speed dating partner, and preferences in mate selection and fun activities by participant and his/her speed dating partner. 

I also included some variables that might not seem to affect match of the participant at first glance, however, these variables could affect participant’s mood and thus his decision. I deemed it was important to control for these features and, thus, included them in my preliminary feature selection. These variables are: 1) station number where partners met (position) since this can affect their mood and thus their decision, 2) condition (condtn) since some participants had limited choice (one is more likely to be happy with his/her choice when it is limited), 3) wave or date (wave) when the event took place, 4) a number of people met in wave (round) because again, according to social science research, the more people we meet with, the less likely we to make a choice or even a correct choice. That is why online dating rarely works.  I excluded unique partner’s id (pid) from the models. It did predict finding a match because some variable some individuals are more socially popular and more attractive, and hence, they get more attention at dating events. However, I refrained from using it in my model as it would be hard to apply to a different set of participants. Their unique id’s would affect the models differently. 


[![Feature Selection Females]({{ site.url }}{{ site.baseurl }}/images/pic6_5.png)]({{ site.url }}{{ site.baseurl }}/images/pic6_5.png)




























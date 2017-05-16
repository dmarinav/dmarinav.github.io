---
title: "Predicting Love at First Sight"
excerpt: "The post predicts finiding a match for speed dating participants at Columbia University"

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


### Explanatory Data Analysis


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


### Feature Selection

Feature selection methods are important to create accurate predictive models. They help to choose features that will provide the best possible model fit with less data. The feature extraction process here was divided onto two parts. For feature extraction, I used four different learning methods: 1). Random Forest Classifier, 2). Adaptive Boosting Classifier, 3). Gradient Boosting Classifier, 4). Decision Tree Classifier. 

In Part I (preliminary feature extraction process), I investigated separate effects of continuous and categorical features on dependent variable. Some of the categorical features consisted of over 100 categories,  there were around 60 continuous features in the dataset at Time1. Because categorical features with many categories tend to mask the effect of other variable on dependent variable, to avoid the masking effect, I preliminary ran two feature selection models: 1) a model with the continuous features, and 2) a model with categorical features. After I selected most important continuous features and most important categorical features, I implemented Part II of my feature selection process. See the python code and output [here].

In Part II (final feature extraction process), I combined most important continuous and categorical features that was extracted in Part 1, and ran another feature selection model using the selected features. The features from the final feature extraction process for my final model were selected in the way to produce the highest accuracy score across various machine learning algorithms covered in the next section, Model Selection.

To select features, I used social science theories and feature selection methods in machine learning. Fist, in order for a participant to find a match, the participant should like his/her speed dating partner. The data did not contain the evaluation of the qualities of a given speed dating partner by the participant, however, it included participant’s decision about his/her speed dating (whether the participant would like to see he/her again). Thus, I used decision of the participant in my model (dec) to evaluate whether the participant likes his/her speed dating partner. The data also contained an evaluation of the participant’s qualities by the speed dating partner, demographics of the participant and his/her speed dating partner, and preferences in mate selection and fun activities by participant and his/her speed dating partner. 

I also included some variables that might not seem to affect match of the participant at first glance, however, these variables could affect participant’s mood and thus his/her decision. I deemed it was important to control for these features and, thus, included them in my preliminary feature selection. These variables are: 1) station number where partners met (position) since this can affect their mood and thus their decision, 2) condition (condtn) since some participants had limited choice (one is more likely to be happy with his/her choice when it is limited), 3) wave or date (wave) when the event took place, 4) a number of people met in wave (round) because again, the more people one meets the less likely he/she finds a match. I know it sounds counterintuitive, but according to [social science research](https://en.wikipedia.org/wiki/Overchoice) that the more people we are dating at a time, the less likely we to make a choice or make a correct choice and find a partner. That is why [online dating rarely works]( https://www.psychologytoday.com/blog/love-digitally/201504/7-research-based-reasons-internet-dating-doesnt-work). Thus, a number of people met in a wave can a significant predictor of whether one can find a match or not.


 I excluded unique partner’s id (pid) from the models. It did predict finding a match because some variable some individuals are more socially popular and more attractive, and hence they get more attention at dating events. However, I refrained from using it in my model as it would be hard to apply to a different set of participants. Their unique id’s would affect the models differently. 


[![Feature Selection Males]({{ site.url }}{{ site.baseurl }}/images/pic6_6.png)]({{ site.url }}{{ site.baseurl }}/images/pic6_6.png)


As seen above, first and foremost, it is important for a participant-male to like his partner to find a match as her decision (dec) is the first feature to predicts a match. It is kind of obvious, I would say. Next, it is very important for his speed dating partner (female in this case) to find him attractive (att_o), to like him overall (like_o), to think he likes her too (prob_o), to share the same interests with him (share_o), thinking he is a fun person (fun_o), sincere (sin_o), and ambitious (amb_o). Age of partner (age_o) is also important for males to find their match, and it is also important if his speed dating partner has met him before (met_o). 

It is also essential what qualities in general your female partner finds important in males. Thus, males are more likely to meet their match if their female dating partner values intelligent (pf_o_int) first and attraction (pf_o_att) second,  and after that she values whether he shares her interests (pf_o_sha),  how fun he is (pf_o_fun), how sincere he is (pf_o_sin), and how ambitious he is (pf_o_amb), consequentially. So, dear Males, you are more likely to find a love at first sight at a Columbia University speed dating event if your female speed dating partner value intelligence first and beauty second. 

Now, what should males think in order to find a match. According to the graph above, in order to find a match, he has to think that his partner is more likely to value how fun he is (fun1_1) and whether he share common interests (sha1_1) with her, and whether he values fun in his potential partner (fun2_1).  Obviously, this kind of thinking works, possibly because the males who think this way so are more likely to appear fun and interesting to their potential mate and hence to get a potential mate

Finally, how many people a participant-male met in wave (round) and whether he is a frequent dater (date) also plays a large role in finding a match. As I explained above, the more people there are in the wave the less likely one to meet his match. That is exactly what I found in the data (not sown here). Also, frequent male-daters are more likely to get themselves a match. I know it is not fair but frequent dater are more experienced and hence more appealing.

I excluded the station number (position), whether his appearance important (att1_1), and  importance of racial background (imprace)  from the final model as they did not really add to the accuracy score. 


[![Feature Selection Females]({{ site.url }}{{ site.baseurl }}/images/pic6_5.png)]({{ site.url }}{{ site.baseurl }}/images/pic6_5.png)


It is slightly different for females, but not by much. Unsurprisingly, it is equally important for a female-participant to like her match (dec). In addition, in order for females to meet their match, it is very important for her speed dating partner to find her attractive (att_o), share common interests (share_o), like her overall (like_o), thinking she likes him too (prob_o), and only after that it is important for him whether she is fun (fun_o) and ambitious (amb_o). Interestingly, sincerity (sin_o) is not even on the picture here. Ladies, keep your sincerity to yourself if you would like to find a love at first sight!

While age of partner (age_o) is equally important for females as for males to find their match, it is also important how young this female is (age). Based on research and life in general, this result is not surprising at all. 

Just like in case with male feature selection model, here it is also essential what qualities in general speed dating male partner finds important in their potential dating partner. Thus, females are more likely to meet their match if their male dating partner values female beauty first (pf_o_att) – even more than he values your beauty (att_o). I guess the males who value female beauty know their way with women. Then female-participants are more likely to find a match if he values whether she shares his interests (pf_o_sha),  how fun she is (pf_o_fun), how sincere she is (pf_o_sin), how intelligent she is (pf_o_int), and only after that how ambitious she is (pf_o_amb). Interestingly, even though males value sincerity in their potential mate, they do not want to see it in short-term mating interactions. I assume sincerity works for males as a long-term mating strategy.






















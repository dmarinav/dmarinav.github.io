---
title: "Predicting Love at First Sight - Part 1"
excerpt: "The post goes over EDA and feature selection to predict a match for speed dating participants at Columbia University"

header:
  overlay_image: speed2.jpg
  overlay_filter: 0.4
  caption: " "
  cta_label: "Part 2"
  cta_url: "https://dmarinav.github.io/data%20science/speed-dating-part2/"
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

For this project, I selected data from the [Kaggle Speed Dating Experiment]( https://www.kaggle.com/annavictoria/speed-dating-experiment).  Feeling nostalgia for social psychology, I thought this data was a perfect representative of social science research. It was compiled by Columbia Business School professors Ray Fisman and Sheena Iyengar. The data “was gathered from participants in experimental speed dating events from 2002-2004. During the events, the attendees would have a four minute "first date" with every other participant of the opposite sex. At the end of their four minutes, participants were asked if they would like to see their date again. They were also asked to rate their date on six attributes: Attractiveness, Sincerity, Intelligence, Fun, Ambition, and Shared Interests.”

In addition, demographics, dating habits, self-perception across key attributes, beliefs on what others find valuable in a mate, and lifestyle information were collected at different points in time.  See the [Speed Dating Data Key document]( https://github.com/dmarinav/My_Projects/blob/master/SPEED%20DATING/Speed%20Dating%20Data%20Key.doc) for details (click on View Raw to see the key).

The features were assessed at Time 1 (before and right after participating in the event), Time 2 (the day after participating in the event), and Time 3 (3-4 weeks after participating in the event). I only used data from Time 1 since only this data was relevant to my model and wanted to predict the probability of leaving the event with a match for both males and females. The project had 4 parts: 1) Data Cleaning, 2) EDA, 3) Feature selection, and 4) Model selection.

My hypothesis was to find out what attitudes towards mating influences love at first sight as well as a probability of finding love at first sight at Columbia speed dating events with. Because of gender differences in partner selection (Fisman, Raymond, et al., 2006), my decision was to build two models: a model for males and a model for females with dependent variable "match.” Thus, the first model predicted a probability of finding match for males while the second model predicted a probability of finding match for females.


### Explanatory Data Analysis

The goal of the explanatory data analysis (EDA) was to investigate demographic data and highlight gender differences in mate selection.


[![Histogram]({{ site.url }}{{ site.baseurl }}/images/pic6_1.png)]({{ site.url }}{{ site.baseurl }}/images/pic6_1.png)


As we can see from the histogram, most females and males were in the age group of 20-35 with several minor exceptions. There were also a couple of outliers, a male of 43 y.o. and a female of 55 y.o. 


[![Count of Race]({{ site.url }}{{ site.baseurl }}/images/pic6_2.png)]({{ site.url }}{{ site.baseurl }}/images/pic6_2.png)


Most participants were European Americans, followed by Asian Americans, Hispanic Americans, others, and African Americans, respectively. There were approximately the same amount of males and females in each race group.

Furthermore, as seen below, there were some gender differences in fun activities.  Males were more interested in sports, TV sports, and gaming while females preferred yoga, watching TV, theater, shopping, dining concerts, and art. Both genders liked reading, music, movies, hiking, exercise, and clubbing. 
 

[![Diff in Fun Activities]({{ site.url }}{{ site.baseurl }}/images/pic6_3.png)]({{ site.url }}{{ site.baseurl }}/images/pic6_3.png)


In spite of the gender differences, both genders equally valued funny, intelligent, sincere partners who share their interests. However, as shown below, males were more likely to value attractive females, while females were more likely to value ambitious males. 


[![Diff in Fun Activities]({{ site.url }}{{ site.baseurl }}/images/pic6_4.png)]({{ site.url }}{{ site.baseurl }}/images/pic6_4.png)


The EDA indicates that there were gender differences in fun activities and mate selection, confirming my suspicion that it is crucial to build two different models predicting speed dating match: 1) a model for males, 2) a model for females. Different features predicting match for males vs. females can affect predictive accuracy of a model.


### Feature Selection

Feature extraction methods are important to create accurate predictive models. They help to choose features that will provide the best possible model fit with less data. The feature extraction process here was divided onto two parts. 

In the first part of feature extraction process (preliminary feature extraction), I investigated separate effects of continuous and categorical features on dependent variable. Some of the categorical features consisted of over 100 categories, and there were around 60 continuous features in the dataset at Time 1. Because categorical features with many categories tend to mask the effect of continuous variables, to avoid the masking effect, I preliminary ran two feature selection models for males and females: 1) a model with continuous features, and 2) a model with categorical features. After I selected most important continuous features and most important categorical features, I implemented the second part of the feature extraction process. See the python code and output [here]( https://github.com/dmarinav/My_Projects/blob/master/SPEED%20DATING/FEATURE%20EXTRACTION_MALE%20MODEL_PART3b.ipynb) for males and [here]( https://github.com/dmarinav/My_Projects/blob/master/SPEED%20DATING/FEATURE%20EXTRACTION_FEMALE%20MODEL_PART3a.ipynb) for females.

In the second part (final feature extraction process), I combined most important continuous and categorical features that was extracted in the first part, and ran another feature selection model for males and females using the selected features. The features from the final feature extraction process for my final model were selected in the way to produce the highest accuracy score across four machine learning classifiers: 1). Random Forest, 2). Adaptive Boosting, 3). Gradient Boosting, and 4). Decision Tree.

In addition to the feature selection algorithms, I used social science theories to select final features. For example, in order for a participant to find a match, the participant first and foremost should like his/her speed dating partner. Because the data did not contain the evaluation of the qualities of a given speed dating partner by the participant, instead, I used the participant’s decision in my model (dec) to evaluate whether the participant likes his/her speed dating partner. In addition, the data also contained the evaluation of the participant’s qualities by his/her speed dating partner, demographics of the participant and his/her speed dating partner, and preferences in mate selection and fun activities by participant and his/her speed dating partner. 

I included in the models some variables that, at first glance, might not seem to affect whether a participant finds a match. However, these variables could affect the participant’s psychological processes, and thus his/her decision. I deemed it was important to control for these features and included them in my preliminary feature selection. Those variables were: 1) station number where partners met (position) since this can affect their mood and thus their decision, 2) condition (condtn) since some participants had limited choice (one is more likely to be happy with his/her choice when it is limited), 3) wave or date (wave) when the event took place, 4) a number of people met in wave (round) because having met more people increases chances of finding the one. 

I excluded unique partner’s id (pid) from the models, even though it predicted finding a match, since some individuals are more socially popular and more attractive, and hence they get more attention at dating events. However, I refrained from using it in my model as it would be hard to apply to a different set of participants. Their unique id’s would affect the models differently. 


[![Feature Selection Males]({{ site.url }}{{ site.baseurl }}/images/pic6_6.png)]({{ site.url }}{{ site.baseurl }}/images/pic6_6.png)


As seen above, first and foremost, it is important for male participant to like his partner to find a match as his decision (dec) is very important in predicting a match. It is kind of obvious, I would say. Next, it is very important for his speed dating partner (female) to find him attractive (att_o), to like him overall (like_o), to think he likes her too (prob_o), to share the same interests with him (share_o), and to think he is a fun person (fun_o). Interestingly, after running a logistic regression with predictors in the output (see it [here]( https://github.com/dmarinav/My_Projects/blob/master/SPEED%20DATING/MALE%20MODEL_LOGISTIC_REG_OUTPUT.ipynb)), finding your male dating partner as sincere (sin_o) and ambitious (amb_o) negatively predicted finding a match. It seemed like sincerity and ambition did not help males to find love at first sight. 

Age of partner (age_o) is also important for males to find their match as well as it is important if his speed dating partner has met him before (met_o), indicating that males tend to warm up faster to females they know. 

It is also essential what qualities in general female speed dating partner finds important in males. That is right! How female thinks in general about what qualities she finds important in men influenced whether male participant would match with her or not.  Consequentially, males are more likely to click with their match if their female dating partner values intelligent (pf_o_int) and attraction (pf_o_att) first of all, and then she values whether he shares her interests (pf_o_sha),  how fun he is (pf_o_fun), how sincere he is (pf_o_sin), and how ambitious he is (pf_o_amb), respectively. Sincerity and ambitions negatively predicted finding a match, indicating that being sincere and ambitious for males does not pay off during speed dating events, even though in general females do report a desire for their potential partner to be sincere and ambitious. 

What should males look for in females in order to find a match? He has to look for a potential partner who is fun (fun1_1) and who does NOT share common interests (sha1_1) with him (Surprise!). Interestingly, sha1_1 negatively predicted finding a match, indicating that the less males deem shared interests important in a potential partner the more likely they were to find a match at Columbia speed dating events. Another interesting observation is that the less males participants think that being a fun person is important for the opposite sex (fun2_1) the more likely they are to find a match. It is an interesting observation because females' speed dating partners would report sharing common interests and having fun with those males even though the males did not think these qualities are important to have.  

Finally, how many people male participant meet in a wave (round) and whether he is a frequent dater (date) also plays a large role in finding a match. The more people there are in the wave the more likely one to meet his match. Frequent male-daters are more likely to get themselves a match. I know it is not fair but I suppose frequent dater are more experienced and hence more appealing.


[![Feature Selection Females]({{ site.url }}{{ site.baseurl }}/images/pic6_5.png)]({{ site.url }}{{ site.baseurl }}/images/pic6_5.png)


[Feature importance for the female model]( http://localhost:8888/notebooks/Documents/GA%20Data%20Science/projects/projects-capstone/capstone_last_version/FEATURE%20EXTRACTION_FEMALE%20MODEL_PART3a.ipynb) is slightly different. Just like for male participant, it is equally important for female participant to like her match (dec). In addition, in order for female participant to meet her match, it is very important for her speed dating partner to find her attractive (att_o), share common interests with her (share_o), like her overall (like_o), think she likes him too (prob_o), and only after that it is important for him whether she is fun (fun_o) and not very ambitious (amb_o). Being ambitious negatively predicted finding a match for females at Columbia speed dating events, while sincerity (sin_o) was not even on the picture. 

While age of partner (age_o) is equally important for females as for males to find their match (as reported by participants), only female age (age) negatively predicted finding a match. Basically, it means that females of older age had much harder time finding love at first sight. 

Just like in case with males, it is also essential for females what qualities in general their speed dating male partner finds important in their potential partner. Consequentially, females are more likely to meet their match if their date values female beauty most of the all (pf_o_att) – even more than he values his speed dating partner’s beauty (att_o). I assume males who value female beauty in general know their way with women. Furthermore, female participants are more likely to click with male-dating partner, if he appreciates sharing interests with his potential date  (pf_o_sha),  how fun she is (pf_o_fun), how sincere she is (pf_o_sin), how intelligent she is (pf_o_int), and only after that how ambitious she is (pf_o_amb). Interestingly, even though males value sincerity in their potential mates, just like females they do not want to see it in short-term mating interactions. I assume sincerity works for males and females as a long-term mating strategy or both genders report that it is important for them, while in reality it is not. 

Replicating findings with males, a number of people in a wave (round) also positively predicted finding a match for females. Those females who thought that opposite sex is less likely to look for shared interests (shar2_1) in their match were more likely to leave speed dating with a match, and those who thought that opposite sex is likely to look for intelligence (intel2_1) in their partner were more likely to find a match. Females who looked for intelligence (intel1_1) in their partner were also more likely to find a match. Finally, major(field_cd) played a huge role in whether females would get selected for further dating. Most popular majors among males were Film and Social Work compared to Biology/Chemistry/Physics. 

I excluded other features from the male and female models as they did not really add any additional value to the accuracy scores of classifiers.

To be continued in [Part 2]( https://dmarinav.github.io/data%20science/speed-d)

{% capture notice-2 %}
#### REFERENCES

* Fisman, R., Iyengar, S. S., Kamenica, E., & Simonson, I. (2006). Gender differences in mate selection: Evidence from a speed dating experiment. The Quarterly Journal of Economics, 121(2), 673-697.

<div class="notice">
  {{ notice-2 | markdownify }}
</div>



























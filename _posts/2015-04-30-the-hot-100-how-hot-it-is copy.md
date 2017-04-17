---
title: "Predicting Survival on the Titanic"
excerpt: "This post completes a predictive analysis of who were likely to survive on the Titanic"
header:
  overlay_image: titanic5.jpg
  overlay_filter: 0.4
  caption: ""
  cta_label: " "
categories:
  - data science
tags:
  - Titanic
  - Kuggle competition
  - imputation
  - binary classification 
  - nested cross-validation
author: "Marina Drus"
date: "15 October 2016"
---

{% include base_path %}

### Introduction

RMS Titanic was a British passenger ship that sank on April 15, 1912 on his way to New York. It perhaps was the most infamous shipwreck in the world history. The Titanic sank after colluding with an iceberg killing 1502 out of 2224 people, including passengers and crew. The Titanic data set obtained from [Kaggle](https://www.kaggle.com/c/titanic/data)contains data for only 891 passengers of the Titanic who either survived or died during the disaster. This is a basic Kaggle data set that can be approach with a challenge and creativity. The data set contains the information about age, sex, passengers class, family on-board, ticket number, ticket price, where passengers boarded the ship, and cabins location. 

### Analysis Overview and Strategy

To approach the problem of determining who survived or died in the Titanic accident, I broke the analysis into several parts, including an initial exploratory analysis. In the initial explanatory stage, I wanted to detect any possible interactions for defining my statistical model. When variables (features) interact the effect of one independent variable can depend on the level of the other independent variable.

For example, intuitively it makes sense to assume that more females survived on the Titanic than males. However, it also makes sense to assume that more females of 1st class vs. females of 3rd class survived. That is, if females of 1st class were more like to survive than females of 3rd class, there is a possible interaction. Another possible interaction is between age and class and so on. Thus, my first goal was to explore all the possible interactions. 

My second goal was to address missing data for the variable Age. About a 20% of the total number of observations for Age are missing values, which could leave me with only 712 data points and decrease predictive accuracy of the final model. This problem could be addressed by using an advanced imputation method. 

Since the data set contain more data on people who perished vs. survived, my third goal was to combat the imbalanced classes using a synthetic minority over-sampling technique. Finally, nested cross-validation was applied to measure and evaluate the predictive performance of the model.

### Explanatory Data Analysis 

The correlational matrix below explores the relationship between variables. Although, correlational matrix is not specifically informative to explore relationship between categorical and continuous features, some minor trends can be detected.  As seen below, the relationship between features varies from small to moderate. No all independent variables have significant relationships with the binary outcome Survive, but as I mentioned earlier correlational matrix is a perfect informative of significant relationship between categorical and continuous features. 


![Correlational Matrix]({{ site.url }}{{ site.baseurl }}/images/pic3_1.png) 


A set of histogram of continuous features below indicates that normal distribution of Age was slightly skewed towards elder people. The number of younger people (age of 0 to 20) in the data set (not necessary on the board of the ship) exceeded the number of elder people (age of 50 and up). More passengers traveled alone and had neither children, nor parents, nor other family members accompanied them. Most passengers (approximately 70%) paid for their fare 50 pounds or less.


![Histograms]({{ site.url }}{{ site.baseurl }}/images/pic3_2.png) 


A fist possible interaction between Age and Sex is explored below. It looks like age played a significant role in survival of young boys. Age did not seem to play any role in survival of females -- females across all ages were more likely to survive on the Titanic.


![Age and Sex Interaction]({{ site.url }}{{ site.baseurl }}/images/pic3_3.png) 


Second possible interaction was explored between Age and Class. As seen below, the passengers of 1st class vs. 2nd and 3rd classes were more likely to survive on the Titanic. However, passengers of younger age were more likely to survive regardless of their class. 


![Age and Class Interaction]({{ site.url }}{{ site.baseurl }}/images/pic3_4.png) 


The next swarmplot looks into interactive relationship between fare and a port of embarkation. In general passengers who embarked in Queenstown were less likely to survive. Also, it seems that proportionally-wise, passengers who embarked in Cherbourg were more likely to survive. The richest passengers on the ship, who paid the highest fare (over $500) and who embarked in Cherbourg, survived as well. As we will see further, it did not matter whether they were males or females. 


![Fare and Embarked]({{ site.url }}{{ site.baseurl }}/images/pic3_5.png)


As seen below, although the three richest passengers on the Titanic survived regardless of their gender, cost of the ticket played a significant role in whether females survived or not. More females who paid high fare vs. low fare survived. That was not the case for males. Males were less likely to survive regardless of the fare they paid. Well, it definitely, did not pay off to be a male on the Titanic unless it was a super rich male. 

 
![Fare and Sex]({{ site.url }}{{ site.baseurl }}/images/pic3_6.png)


The swarmplot below explores interaction between gender and class. It replicates the findings from the Fare by Sex interaction, but it is another alternative interaction to explore. Females of 1st and 2nd class were more likely to survive, but that was not a case for males. Males were less likely to survive regardless of their class. 


![Fare and Sex]({{ site.url }}{{ site.baseurl }}/images/pic3_7.png)

 

### Conclusion















---
title: "Predicting Love at First Sight - Part 2"
excerpt: "The post predicts finding a match for speed dating participants at Columbia University"

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
date: "30 November 2017"
---

{% include base_path %}


### SMOT and Model Selection 


In Part 1 I went over EDA and feature selection. Please visit [Part 1](https://dmarinav.github.io/data%20science/speed-dating/) for the review as many interesting findings were discovered there. This part is about synthetic minority oversampling techniques (SMOT) and model selection. Synthetic minority oversampling techniques is a very useful strategy to combat imbalance classes. More people usually find no match at speed dating events than do, and of course I made sure my data has imbalanced classes before implementing these techniques. From my experience, SMOT is extremely valuable in increasing model’s accuracy. Almost all the times, I used SMOTs I would drastically increase my accuracy score.  

In this project, I implemented several SMOT techniques and choose the one that would give me the best accuracy across nine classifiers: 1) Decision Tree, 2) Logistic Regression, 3) Bagging DT, 4) Random Forest, 5) Extra Trees, 6) Ada Boost, 7) Gradient Boosting, 8) Bernoulli NB, and 9) Support Vector Machine. 

Below is an illustration of various synthetic minority oversampling techniques for the male model (in blue) and female model (in purple). I will not go into description of each technique, but as you can see from the graphs, they create additional data for the imbalanced class Match, but they use different approach. My favorite technique is Random Oversampling. Random Oversampling uses a bootstrapping method that works by randomly oversampling the minority class. Usually, I find this one giving me the best accuracy scores. 


[![SMOT Males]({{ site.url }}{{ site.baseurl }}/images/pic6_8.png)]({{ site.url }}{{ site.baseurl }}/images/pic6_8.png)


[![SMOT Females]({{ site.url }}{{ site.baseurl }}/images/pic6_7.png)]({{ site.url }}{{ site.baseurl }}/images/pic6_7.png)


Indeed, in the tables of scores below, you can see that Random Oversampling does produces highest accuracy scores across multiple classifiers.

| Male Model Classifiers | ORIGINAL    | SMOT SVM      |ADASYN        |SMOT REG     |SMOT BORDER 1|RANDOM OVERS |
|:----------------------:|:-----------:|:-------------:|:-------------:-------------:-------------:------------ :
|Decision Tree           |0.832 ± 0.03 | 0.893 ± 0.022 |0.893 ± 0.018 |0.885 ± 0.024|0.881 ± 0.025|0.886 ± 0.029|                |
|Logistic Regr           |0.893 ± 0.022|
|Bagging DT              |0.893 ± 0.018|
|Random Forest           |0.885 ± 0.024|
|Extra Trees             |0.881 ± 0.025|
|Ada Boost               |0.886 ± 0.029|
|Gradient Boosting       |0.896 ± 0.02 |
|Bernoulli NB            |0.882 ± 0.021|
|Support Vector          |0.894 ± 0.018| 






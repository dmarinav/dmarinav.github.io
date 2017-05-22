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

Below is an illustration of various synthetic minority oversampling techniques for the male model (in blue) and female model (in purple). As you can see from the graphs, they create additional data for the imbalanced class Match, but they use different approaches. 

#### MALE MODEL
[![SMOT Males]({{ site.url }}{{ site.baseurl }}/images/pic6_8.png)]({{ site.url }}{{ site.baseurl }}/images/pic6_8.png)

#### FEMALE MODEL
[![SMOT Females]({{ site.url }}{{ site.baseurl }}/images/pic6_7.png)]({{ site.url }}{{ site.baseurl }}/images/pic6_7.png)


My favorite technique is Random Oversampling. I will not go into detailed description of each technique, but generally SMOTs oversample by creating “synthetic” examples rather by over-sampling with replacement. On the other hand, Random Oversampling works by randomly over-sampling with replacement. Previous research (Chawla, et al., 2002; Ling & Li, 1998; Japkowicz, 2000) noted Random Oversampling doesn’t significantly improve minority class recognition. That is, however, not my experience with this technique. As you will see below, not only Random Oversampling significantly improve minority class recognition, it does a much better job with some classifiers (e.g., Bagging DT, Random Forest, and Extra Trees) than other SMOT techniques. 

Indeed, in the tables of accuracy scores of the training set below, you can see that Random Oversampling does produces highest accuracy scores across Bagging DT, Random Forest, and Extra Trees classifiers. 

#### MALE MODEL

|Classifiers             | ORIGINAL    | SMOT SVM    |ADASYN       |SMOT REG     |SMOT BOR1    |RANDOM OVER  |
|:----------------------:|:-----------:|:-----------:|:------------:-------------:-------------:------------ :
|Decision Tree           |0.832 ± 0.030|0.904 ± 0.013|0.901 ± 0.018|0.899 ± 0.016|0.897 ± 0.016|0.891 ± 0.019|
|Logistic Regr           |0.893 ± 0.022|0.895 ± 0.011|0.875 ± 0.017|0.891 ± 0.018|0.891 ± 0.015|0.880 ± 0.012|
|Bagging DT              |0.893 ± 0.018|0.928 ± 0.013|0.931 ± 0.020|0.931 ± 0.016|0.936 ± 0.017|0.948 ± 0.016|
|Random Forest           |0.885 ± 0.024|0.936 ± 0.010|0.936 ± 0.011|0.937 ± 0.011|0.936 ± 0.014|0.952 ± 0.018|
|Extra Trees             |0.881 ± 0.025|0.940 ± 0.011|0.943 ± 0.010|0.947 ± 0.007|0.945 ± 0.015|0.968 ± 0.010|
|Ada Boost               |0.886 ± 0.029|0.930 ± 0.012|0.921 ± 0.016|0.926 ± 0.014|0.926 ± 0.018|0.895 ± 0.016|
|Gradient Boosting       |0.896 ± 0.020|0.938 ± 0.015|0.931 ± 0.015|0.939 ± 0.014|0.944 ± 0.016|0.916 ± 0.012|
|Bernoulli NB            |0.882 ± 0.021|0.888 ± 0.014|0.847 ± 0.027|0.864 ± 0.016|0.863 ± 0.018|0.845 ± 0.020|
|Support Vector          |0.894 ± 0.018|0.895 ± 0.010|0.873 ± 0.015|0.891 ± 0.020|0.887 ± 0.014|0.878 ± 0.014|


#### FEMALE MODEL

|Classifiers             | ORIGINAL    | SMOT SVM    |ADASYN       |SMOT REG     |SMOT BOR1    |RANDOM OVER  |
|:----------------------:|:-----------:|:-----------:|:------------:-------------:-------------:------------ :
|Decision Tree           |0.886 ± 0.029|0.935 ± 0.009|0.930 ± 0.014|0.927 ± 0.017|0.930 ± 0.009|0.922 ± 0.016|
|Logistic Regr           |0.917 ± 0.020|0.933 ± 0.011|0.922 ± 0.009|0.933 ± 0.014|0.934 ± 0.015|0.925 ± 0.011|
|Bagging DT              |0.921 ± 0.018|0.946 ± 0.010|0.949 ± 0.013|0.946 ± 0.015|0.952 ± 0.010|0.959 ± 0.009|
|Random Forest           |0.905 ± 0.011|0.950 ± 0.006|0.961 ± 0.006|0.957 ± 0.010|0.955 ± 0.011|0.965 ± 0.009|
|Extra Trees             |0.907 ± 0.011|0.959 ± 0.008|0.962 ± 0.010|0.960 ± 0.008|0.960 ± 0.006|0.969 ± 0.009|
|Ada Boost               |0.919 ± 0.013|0.945 ± 0.012|0.943 ± 0.007|0.948 ± 0.010|0.949 ± 0.008|0.933 ± 0.010|
|Gradient Boosting       |0.928 ± 0.014|0.952 ± 0.009|0.948 ± 0.010|0.955 ± 0.012|0.956 ± 0.009|0.943 ± 0.010|
|Bernoulli NB            |0.911 ± 0.013|0.901 ± 0.014|0.896 ± 0.017|0.894 ± 0.019|0.898 ± 0.019|0.883 ± 0.013|
|Support Vector          |0.921 ± 0.022|0.933 ± 0.012|0.922 ± 0.009|0.929 ± 0.015|0.931 ± 0.014|0.922 ± 0.013|


I chose the Extra Tree classifier with random over-sampling because it gave me the highest score on my training sets. After tuning the models, I received cross validation scores of 0.967 and 0.969 for the male and female models, respectively. The best accuracy scores for the male model were 100%, 97.34%, and 100% for training, test, and complete sets, respectively. The confusion matrices for both models introduced below.

#### MALE MODEL
[![SMOT Females]({{ site.url }}{{ site.baseurl }}/images/pic6_10.png)]({{ site.url }}{{ site.baseurl }}/images/pic6_10.png)

#### FEMALE MODEL
[![SMOT Females]({{ site.url }}{{ site.baseurl }}/images/pic6_9.png)]({{ site.url }}{{ site.baseurl }}/images/pic6_9.png)


As seen on confusion matrices, random over-sampling produced perfect confusion matrix and significantly improved minority class recognition. Moreover, it helped to yield perfect AUC scores for both models.


[![SMOT Females]({{ site.url }}{{ site.baseurl }}/images/pic6_12.png)]({{ site.url }}{{ site.baseurl }}/images/pic6_12.png)


[![SMOT Females]({{ site.url }}{{ site.baseurl }}/images/pic6_11.png)]({{ site.url }}{{ site.baseurl }}/images/pic6_11.png)


### Conclusion

In this project, I implemented feature selection techniques, synthetic minority oversampling techniques, modeling techniques, and model tuning to achieve very high accuracy scores and confusion matrices with 100% of precision, recall, and f-1 score. This project demonstrated that all the above-mentioned techniques can boost prediction accuracy scores by almost 10 points, indicating that model accuracy should be attributed to mastery of data analysis and data science and not to data quality.

Furthermore, I build two models, for each gender, that predict finding love at first sight. The findings indicate that there are gender differences in everyday activities as well as in mating and relating.  Males were more interested in sports, TV sports, and gaming while females preferred yoga, watching TV, theater, shopping, dining concerts, and art. Males preferred attractive females while females preferred ambitious men. Feature selection process showed that love at first sight can be pretty superficial and not necessarily guarantee a long-lasting relationship. For example, ambitions negatively predicted finding a match for both genders while sincerity negatively predicated finding a match for males and was trivial predictor in matching with a speed dating partners for females. That is, both males and females do not consider sincerity an important factor in finding love at first sight even though in an imaginary world both genders want sincerity in relationship (as they reported them as important qualities in a potential mate). Older females had a much harder time finding a match – for them age negatively predicted love at first sight, and those females who major in Film and Social Work were more likely to find a match compared with those who major in Biology/Chemistry/Physics. Is anyone now surprised that there is a shortage of females in STEM?

These are just some highlights and, of course, love at first sight is not completely superficial. Both genders would choose a partner who they perceived sharing interests with them, and those who valued intelligence in their partners were more likely to find a match. However, these findings cannot be applicable to general population.  Columbia students and students in general do not behave like general population. To make these findings applicable to general population, data should be collected from multiple speed dating events, from various states, from all age groups, and from people with various economic background. 


{% capture notice-2 %}
#### REFERENCES

* Batista, G. E., Prati, R. C., & Monard, M. C. (2004). A study of the behavior of several methods for balancing machine learning training data. ACM Sigkdd Explorations Newsletter, 6(1), 20-29.

* Chawla, Nitesh V., et al. "SMOTE: synthetic minority over-sampling technique." Journal of artificial intelligence research 16 (2002): 321-357.Chawla, N. V., Bowyer, K. W., Hall, L. O., & Kegelmeyer, W. P. (2002). SMOTE: synthetic minority over-sampling technique. Journal of artificial intelligence research, 16, 321-357.

* Japkowicz, N. (2000). The Class Imbalance Problem: Significance and Strategies. In Proceedings of the 2000 International Conference on Artificial Intelligence (IC-AI’2000): Special Track on Inductive Learning Las Vegas, Nevada.

* Ling, C., & Li, C. (1998). Data Mining for Direct Marketing Problems and Solutions. In
Proceedings of the Fourth International Conference on Knowledge Discovery and Data Mining (KDD-98) New York, NY. AAAI Press.

* Nguyen, H. M., Cooper, E. W., & Kamei, K. (2011). Borderline over-sampling for imbalanced data classification. International Journal of Knowledge Engineering and Soft Data Paradigms, 3(1), 4-21.
{% endcapture %}

<div class="notice">
  {{ notice-2 | markdownify }}
</div>
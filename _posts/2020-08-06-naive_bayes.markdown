---
layout: post
title:      "Naive Bayes"
date:       2020-08-06 17:58:08 +0000
permalink:  naive_bayes
---


Naïve Bayes, to me, is one of the most intuitive machine learning algorithms.  Naïve Bayes is a two-class or multi-class classification algorithm.  It uses conditional probability to estimates the probability that a given data point will fall into a certain class.  In this post, I will walk you through an example that I used while learning this algorithm.

I first imported the necessary libraries used for data exploration and scientific computing, Pandas and NumPy.  These are the only two libraries I used, I did not used scikit-learn, a popular machine learning library that has most machine learning models already built in. In supervised machine learning, the data used has a target variable and depending on the model, several variables used as predictors.


import NumPy as np
import Pandas as pd

After importing these libraries, I then created a data frame with a target column (what we are trying to predict) and feature columns (used for learning and as predictors).  I related the example to wildlife and the reason I started learning data science.  I want to take what I learn and go back to Africa and use different machine learning models and algorithms to predict poaching patterns so it can be used to reduce or hopefully to end poaching.  The variable I used for the target was Species:

X['Species'] = ['lion', 'lion', 'rhino', 'rhino', 'rhino', 'lion', 'rhino', 'lion']

I included 8 observations, so this is a very small dataset.  I used three different variables for my predictors, Weight, Height, and Tooth or Horn size:


X['Weight'] = [330,250,2500, 1150,2000,500,1750,425]
X['Height'] = [60,50,90,100,115,55,110,80]
X['Tooth or Horn size'] = [2.2,3,12,10,11,2.6,10,3.5]

I created the data frame by setting X equal to pd.DataFrame:


Species	Weight	Height	Tooth or Horn size
0	lion	330	60	2.2
1	lion	250	50	3.0
2	rhino	2500	90	12.0
3	rhino	1150	100	10.0
4	rhino	2000	115	11.0
5	lion	500	55	2.6
6	rhino	1750	110	10.0
7	lion	425	80	3.5



I created another data frame with three observation of weight, height, and tooth or horn size but I did not add a target variable.  This data is going to be used to test our model:


   Weight Height Tooth or Horn size
0   450       56                            2.9



To use the Naïve Bayes formula, I first had to do some calculation.  I had to find the probability of seeing each species in the dataset given no data.  This was simple since there was an even number of lions and rhinos, so the probability for each was 5%:

n_lion = X['Species'][X['Species'] == 'lion'].count()



n_rhino = X['Species'][X['Species'] == 'rhino'].count()


total_species = X['Species'].count()


Prob_lion = n_lion/total_species


Prob_rhino = n_rhino/total_species



Next I needed to find the mean and variance of the data for both species so I could find the likelihood.  Likelihood is the probability of observing data given certain parameters(conditions).

# Means for lions
lion_height_mean = Species_means['Height'][Species_var.index == 'lion'].values[0]
lion_weight_mean = Species_means['Weight'][Species_var.index == 'lion'].values[0]
lion_tooth_mean = Species_means['Tooth or Horn size'][Species_var.index == 'lion'].values[0]

#Variance for Lions
lion_height_var = Species_var['Height'][Species_var.index == 'lion'].values[0]
lion_weight_var = Species_var['Weight'][Species_var.index == 'lion'].values[0]
lion_tooth_var = Species_var['Tooth or Horn size'][Species_var.index == 'lion'].values[0]

#Means for Rhino
rhino_height_mean = Species_means['Height'][Species_var.index == 'rhino'].values[0]
rhino_weight_mean = Species_means['Weight'][Species_var.index == 'rhino'].values[0]
rhino_horn_mean = Species_means['Tooth or Horn size'][Species_var.index == 'rhino'].values[0]

#Variance for Rhino
rhino_height_var = Species_var['Height'][Species_var.index == 'rhino'].values[0]
rhino_weight_var = Species_var['Weight'][Species_var.index == 'rhino'].values[0]
rhino_horn_var = Species_var['Tooth or Horn size'][Species_var.index == 'rhino'].values[0]

With this information I could calculate the probability likelihood by creating a function and using the formula:

def p_y_given_x(x, mean_y, variance_y):
    
    
    p = 1/(np.sqrt(2*np.pi*variance_y)) * np.exp((-(x-mean_y) ** 2)/(2*variance_y))
    
    
    
    return p

With all of this I could plug in the data from my observation data frame into my new function and find the probability of each animal that the data represents:

Prob_lion * \
p_y_given_x(observation['Height'][0], lion_height_mean, lion_height_var) * \
p_y_given_x(observation['Weight'][0], lion_weight_mean, lion_weight_var) * \
p_y_given_x(observation['Tooth or Horn size'][0], lion_tooth_mean, lion_tooth_var)
2.8964845209040603e-05
In [53]:



Prob_rhino * \
p_y_given_x(observation['Height'][0], rhino_height_mean, rhino_height_var) * \
p_y_given_x(observation['Weight'][0], rhino_weight_mean, rhino_weight_var) * \
p_y_given_x(observation['Tooth or Horn size'][0], rhino_horn_mean, rhino_horn_var)
5.621641543861427e-26


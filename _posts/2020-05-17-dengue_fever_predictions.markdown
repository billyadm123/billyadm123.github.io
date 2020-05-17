---
layout: post
title:      "**Dengue Fever Predictions**"
date:       2020-05-17 19:12:16 +0000
permalink:  dengue_fever_predictions
---



For a self-project I did for Flatiron school, I decided to use what I had learned about machine learning to see if I could predict cases of dengue fever.  I came up with two problem statements for this project: 1. Predict what causes Dengue fever. 2. Seperate the data between each city.  The data I used for this project I found on https://www.drivendata.org/.

Dengue fever is a mosquito-borne virus and is spread by female mosquitos.  Some may not even know that they have been infected by the virus while others suffer from severe flu-like symptoms and even death.  Those who show symptoms usually don't start seeing them until three to fourteen days after infection and it takes two to seven days to recover form dengue.  It is spread by several species of female mosquitos. Early detection will lower the fatality rate of dengue fever.  For more information, you can visit: https://www.who.int/news-room/fact-sheets/detail/dengue-and-severe-dengue.

The data I used for this project contained different weather measurements for two cities, San Juan, Puerto Rico and Iquitos, Peru. To start my project, I first plotted both cities using Arcgis API:
```
gis = GIS()
map = gis.map('San Juan',10, mode='3D')
map
```

After plotting both cities, I did some critcal thinking on the environment for each and how each could be different.  Since San Juan is on the ocean and Iquitos is sorrounded by jungle, I came to the conclusion that Iquitos would be more humid, muggy, and moist than San Juan. Iquitos also seemed to be more remote which might be the cause for the lack of data and it might limit the healthcare system resources.  I plotted the cases for each city over time using a dot plot:
```
plt.figure(figsize=(11,9))
plt.plot(sj['total_cases'], '.b', label="San Juan", color='b')
plt.plot(iq['total_cases'], '.b', label="Iquitos", color='g')
plt.legend()
```

From this plot I could see that San Juan had a lot more data than Iquitos so I decided to drop all Iquitos data for now. There was a periodic trend for both cities in the number of cases and even though there was less data for Iquitos, the cases were more condensed.  I think it could be because of the environment or San Juan was able to handle cases better.

I used pca - principle component analysis to help me find variables that best explained the data. PCA centers each data point to the orgin of a graph by subtracting the mean of each data point form the mean of the dataset.  The new points are plotted and a line of best fit is drawn through those data points.  The residuals from the line to the data points are used to select features or the data points are projected on to the line and the distances from those projected data point to the orgin are used.  After this analysis I found that 10 features were able to explain 99 percent of the data.
1. weekofyear	
2. ndvi_ne	
3. ndvi_nw	
4. ndvi_se	
5. ndvi_sw	
6. precipitation_amt_mm	
7. reanalysis_air_temp_k	
8. reanalysis_avg_temp_k	
9. reanalysis_dew_point_temp_k	
10. reanalysis_max_air_temp_k
Ndvi is the normalized differencevegatation index.

For my first problem statement I used simple linear regression and a random forest regressor.  For my linear regression model, I got a score of 99.7% and for my random forest, I got 99.4% accuracy in predicting dengue fever.  I believe that when you have enough domain knowledge on a subject, a simple polynomial regression model can be pretty accurate.

For my second problem statement, trying to seperate the data between both cities, I used three seperate classification models.  The first model I used for this problem was logistic regression.  I used the two cities as my target variables and all the same features as the regression problem. I balanced the classes so each city had an equal chance of being chose.  I was able to get a TPR - true positive rate of 93% for San Juan and a TPR of 82% for Iquitos.  The other two models I used were a k nearest neighbor model and a support vector machine. The knn model got 93% for SanJuan and only 75% for Iquitos and the support vector classifier did even worse.

For better modeling and decisions you would need more data on the healthcare system for each city, poverty and sanitation data, and if any control measures are currently being used.



# Phase 3 Project

## Step 1: Business Understanding

The purpose of this section is to understand what the business problem and the stakeholders that will be understanding the work that I am performing. The stakeholder of my project is the Austrialian government. In 2020, wildfires raged across the country of Australia, in order to prevent a catastrophe like this from happening again, they have contacted me to generate a machine learning classification model to help predict whether or not it will rain the next day after a certain set of conditions. The primary purpose of this algorithm is predictive, meaning we will use certain attributes to predict whether it will rain or not the next day. The work performed here should help the Australian government prepare necessary measures in real-time to work towards combating future wild-fires. 

## Step 2: Data Understanding

The columns in the data are below:

> **MinTemp:** The minimum temperature in degrees celsius

>**MaxTemp:** The maximum temperature in degrees celsius

>**Rainfall:** The amount of rainfall recorded for the day in mm

>**Evaporation:** The so-called Class A pan evaporation (mm) in the 24 hours to 9am

>**Sunshine:** The number of hours of bright sunshine in the day.

>**WindGustDir:** The direction of the strongest wind gust in the 24 hours to midnight

>**WindGustSpeed:** The speed (km/h) of the strongest wind gust in the 24 hours to midnight

>**WindDir9am:** Direction of the wind at 9am

>**WindDir3pm:** Direction of the wind at 3pm

>**WindSpeed9am:** Wind speed (km/hr) averaged over 10 minutes prior to 9am

>**WindSpeed3pm:** Wind speed (km/hr) averaged over 10 minutes prior to 3pm

>**Humidity9am:** Humidity (percent) at 9am

>**Humidity3pm:** Humidity (percent) at 3pm

>**Pressure9am:** Atmospheric pressure (hpa) reduced to mean sea level at 9am

>**Pressure3pm:** Atmospheric pressure (hpa) reduced to mean sea level at 3pm

>**Cloud9am:** Fraction of sky obscured by cloud at 9am. This is measured in "oktas", which are a unit of eigths. It records how many eigths of the sky are obscured by cloud. A 0 measure indicates completely clear sky whilst an 8 indicates that it is completely overcast.

>**Cloud3pm:** Fraction of sky obscured by cloud (in "oktas": eighths) at 3pm. See Cload9am for a description of the values

>**Temp9am:** Temperature (degrees C) at 9am

>**Temp3pm:** Temperature (degrees C) at 3pm

>**RainToday:** Boolean: 1 if precipitation (mm) in the 24 hours to 9am exceeds 1mm, otherwise 0

>**RainTomorrow:** The amount of next day rain in mm. Used to create response variable RainTomorrow. A kind of measure of the "risk".

After looking at the histograms of the columns, most seem to be normally distributed, except for cloud data.

![Image1]

## Step 3: Data Preparation

Before modeling, I create dummy variables for the categorical columns. I remove some of the columns to avoid the dummy trap. I then complete the train-test split, and get to work on imputing nulls. I imputed nulls based on relationships and findings from the data. For Cloud Data, I use rain data and humidity to generate relationships. For sunshine data, I use rain data and the mean. The rest I imputed using the mean, as they seemed normally distributed. Lastly, I normalize the data.

## Step 4: Modeling

I ran different models using different parameters using Logistic Regression, kNN and Decision Trees. To select the best parameters, I used GridSearchCV. See the confusion matrices for the best models below.

### Logistic Regression

Baseline Model:
![Image2](https://raw.githubusercontent.com/justingrisanti/dsc-phase-3-project/main/Visualizations/LogRegBase.png)

Best GridSearch Model:
![Image6](https://raw.githubusercontent.com/justingrisanti/dsc-phase-3-project/main/Visualizations/LogRegBest.png)

### k-Nearest Neighbors 

![Image3](https://raw.githubusercontent.com/justingrisanti/dsc-phase-3-project/main/Visualizations/KNN.png)

### Decision Trees

![Image4](https://raw.githubusercontent.com/justingrisanti/dsc-phase-3-project/main/Visualizations/DT.png)

## Step 5: Regression Results

The logistic regression baseline model was our best model, with an accuracy score of 85%, with the least amount of Type 1 and Type 2 error. The results are generated below: 

Training Data Results:

              precision    recall  f1-score   support

         0.0       0.87      0.95      0.91     85187
         1.0       0.72      0.49      0.59     23908

    accuracy                           0.85    109095
   macro avg       0.79      0.72      0.75    109095
weighted avg       0.84      0.85      0.84    109095


Test Data Results:

              precision    recall  f1-score   support

         0.0       0.89      0.91      0.90     28396
         1.0       0.65      0.60      0.62      7969

    accuracy                           0.84     36365
   macro avg       0.77      0.75      0.76     36365
weighted avg       0.84      0.84      0.84     36365


Our AUC is .85

![Image5](https://raw.githubusercontent.com/justingrisanti/dsc-phase-3-project/main/Visualizations/AUC.png)

## Next Steps

As our precision and recall scores are a little low, it might be beneficial to test using different models in the future, like random forests. We could also obtain more data from different periods to see how our model applies to other years.


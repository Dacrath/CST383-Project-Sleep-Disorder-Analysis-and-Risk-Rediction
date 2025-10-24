# CST383-Project-Sleep-Disorder-Analysis-and-Risk-Rediction
Members
Steven Jackson
Andrew Kopf
Jeremy Norvell
Dominick Racela


## Project Idea
The sleep health dataset located on Kaggle at this link will be analyzed for risk factors which influence insomnia or sleep apnea. By analyzing the data for correlative features and cleansing of any potential outliers or spurious data, key risk factors can be identified which may help people adjust their habits to achieve better sleep. In addition, risk factors that are immutable (such as age) can be listed to assist people in developing healthier sleep habits as their bodies age.

In addition, since both apnea and insomnia are considered to be independent conditions, they will be used as separate target variables into a predictive modeling. This will allow exploration of multiple model types across separate predictive variables when generating an overall risk score for each condition.

Lastly, any interaction between variables which show a strong influence in either model can be analyzed as well as developing separate analysis between each condition to see how their predictors may be similar and how they may differ.

## Choice of Dataset
This dataset about sleep health and how it relates to lifestyle has information about an individual's sleep patterns, lifestyle habits, and health indicators. The goal of this dataset is to see how variations in sleep such as duration, quality, or consistency relates to daily performance metrics such as productivity and well-being. It contains basic columns like gender and age to characterize the individual. Columns such as sleep duration, quality of sleep, and stress levels are included to determine the individual's sleep patterns. Additional features include physical activity levels, caffeine consumption, and mood, which help researchers understand broader lifestyle influences. Overall, the dataset offers opportunities for exploring correlations between healthy sleep habits, stress management, and improved productivity outcomes.

## Data Dictionary
The dataset as provided on Kaggle provides a high-level data dictionary describing each of the variables. It has been copied below for reference. Each of these features will be discussed in later sections of this document to clarify their role in the project.

Person ID – Unique identifier for each individual
Gender – Male/Female
Age – Age of the individual
Occupation – Job category of the individual
Sleep Duration (hours) – Average sleep duration per day
Quality of Sleep (scale 1–10) – Self-reported sleep quality
Physical Activity Level (minutes/day) – Daily physical activity duration
Stress Level (scale 1–10) – Self-reported stress level
BMI Category – Body Mass Index classification (Normal/Overweight/Obese, etc.)
Blood Pressure (mmHg) – Systolic/Diastolic blood pressure
Heart Rate (bpm) – Resting heart rate
Daily Steps – Number of steps taken per day
Sleep Disorder – Sleep-related disorder (None, Insomnia, Sleep Apnea)
Data Import

## Observations and Preprocessing
While the original dataset has ten potential features to include in a model, four of these are of type "object" and will limit the number of machine learning algorithims that can be applied. In order to improve the data for analysis and model building, several features have been engineeered from the existing data. Processing details are listed below:

## Features
"Blood Pressure" displays a character string of XXX/YY, where XXX and YY represent systolic and diastolic blood pressure. These will be split into separate data elements to serve as potential features.
"BMI Category" provides four categories: "Normal", "Normal Weight", "Overweight", and "Obese". These have been split into binary features using one-hot encoding. Further exploration may be needed to determine the difference between "Normal", and "Normal Weight"
"Occupation" contains a series of values that will be binned into high, medium, and low quantiles which are represented by ascending integers (e.g. 0,1, and 2). These bins represent the correlation to each respective predictive variable.
"Gender" is an object showing "male" and "female" values. This will be split into binary features using one-hot encoding to identify male observations.
Target Variables
"Sleep Disorder" gives displays three values: NaN (no sleep disorder reported), "Insomnia", and "Sleep Apnea". These have been split into individual binary variables using one hot encoding. These variables will ultimately become the target variable for any emerging model.

## Exploration and Visualization
To better understand relationships within our data, our next step is to generate basic visualizations using both default and engineered variables.
These will help identify patterns and correlations that could improve model accuracy.

Histograms can show distributions for key numeric variables:

Age
Sleep Duration
Stress Level
Quality of Sleep
Systolic and Diastolic Blood Pressure
Scatterplots can show potential correlations between variables:

Stress Level vs. Sleep Duration
Sleep Duration vs. Quality of Sleep
Age vs. Systolic Blood Pressure
Heart Rate vs. Stress Level

Majority of the participants in the 25–60 years age group with an average sleep duration between 6–8 hours and sleep quality scores of 6–8 which indicates generally adequate rest. Their stress levels are moderate to high with blood pressure readings that fall within normal limits. The data represents a relatively healthy adult group with moderate variation in sleep and lifestyle factors.

## Initial Predictions
Logistic regression allows us to predict the probability of a person may develop sleep apnea as they age. A person at age 40 has 0.126 probability of developing sleep apnea versus a person at age 50 that has a probability of 0.3519.

## Predicting Insomnia
While the above logistic regression model gives us a quick overview of how a model can be used to see if a prediction is possible, it does not take advantage of machine learning for optimization.

Grid Search Approach
The code uses machine learning in what is effectively a grid search methodology. This iterates through multiple hyperparameters and input predictors in order to find an optimum model for the prediction of the insomnia variable. A decision tree is used for this portion of the model in order to build experience and show the visual explainability of this type of model.

In order to avoid overfitting, hyperparameters for the minimum samples per leaf (min_samples_leaf) and the maximum tree depth (max_depth) were both chosen at 5 and 3, respectively. These were selected after some experimentation with building trees and seem to give a balance between optimization and overfitting. A quick internet search shows that these are commonly accepted values to reduce overfitting.

In addition, the code allows hyperparameters to be applied in a deliberately chosen order. This is intentional should the model developer want to prioritize explainability over performance. For example, using 'best' settings for split will often be more easily interpreted than 'random'. The latter of these may produce counterintuitve results.

## Predicting Apnea
This uses the k-Nearest Neighbors (kNN) machine learning model to predict if a person has sleep apnea. It defines the sleep apnea column as the target variable and selects health and lifestyle features such as age, sleep duration, and gender as predictors. It then removes missing data and gives the dataset a training and testing split of 70/30 respectively. The model is trained and tested 12 times with different k-values and weighting methods (uniform and distance). The results shows how each model performed and helps identify which k and weighting method gives the highest prediction accuracy.

Confusion Matrix
This confusion matrix displays that the model correctly predicted that 84 samples had no sleep apnea and that 21 samples had sleep apnea. A small sample of people were incorrectly identified as indicated by the top right and bottom left squares on the confusion matrix. Overall, the confusion matrix is able to display the model's high accuracy as evidenced by its high amount of true positives and true negatives.

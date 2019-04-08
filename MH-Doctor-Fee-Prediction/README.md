# Predict A Doctor's Consultation Fee Hackathon
* Competition link: https://www.machinehack.com/course/predict-a-doctors-consultation-fees-hackathon/
* Dataset link: Same as above

## Problem Statement
We have all been in situation where we go to a doctor in emergency and find that the consultation fees are too high. As a data scientist we all should do better. What if you have data that records important details about a doctor and you get to build a model to predict the doctor’s consulting fee.? This is the hackathon that lets you do that.

<img src="https://www.machinehack.com/wp-content/uploads/2019/02/practo-inside-banner-.jpg" width="400px" height="200px"/>

## Features
* Qualification: Qualification and degrees held by the doctor
* Experience: Experience of the doctor in number of years
* Rating: Rating given by patients
* Profile: Type of the doctor
* Miscellaeous_Info: Extra information about the doctor
* Fees: Fees charged by the doctor :point_left: This is the target variable
* Place: Area and the city where the doctor is located.

## Objective
Based on values of above features, predict the consultation fee of a doctor.

## Evaluaton Metric
Score = 1 - Root-Mean-Squared-Log-Error (RMSLE)

## Solution Approach
1. The first step was extensive EDA of all the features. The dataset is not too messy, but not very clean either. There are significant number of values missing for `Rating`, `Place` and `Miscellaneous_Info`.
2. All features expect `Fees` are text-based, so normalization is required.
3. Following are few of the steps performed for clean-up and data munging.
- Extracted numerical values from `Experience`
- Split `Qualification` into `Qualification_1` and `Qualification_2`, and normalized the text.
- Created feature as `Qualification_Total`, to capture total number of degrees.
- Split `Place` into `City` and `Town`, along with text normalization.
- Imputed missing `Rating` rows with mean of rating values.
3. Many of the features are categorical. As a next step, created One-Hot-Encoding of the categorical features, thus resulting into many columns.
4. Built models (and tested on train data splitted into train and CV set) 
- Tried with basic regression algorithms - Linear Regression, SVM, KNN, Decision Trees, Decision Forests and so on. Based on the result, it was clear that the data is highly non-linear.
- Tree based algorithms were giving relatively good result, and ensemble models were performing even better.
- Tried Bagging, Gradient Boosting and XG Boosting - XGBoost performed well.
- Performed extensive hyperparameter tuning to reduce overfit on XGBoost model. Reached a score of ~0.68 on train set and ~0.42 on local CV set.
- :point_right: This solution scored 0.74829539 on [final LB](https://www.machinehack.com/course/predict-a-doctors-consultation-fees-hackathon/leaderboard), while the score for 1st place was 0.76162342.
5. Possible further improvements:
- Consider log of Fees instead of given values.
- Consider `Miscellaeous_Info` and extract meaningful info out of it.
- Drop `Rating` feature.

## Instruction to run this code
- Requirements: Python 3, Numpy, Matplotlib, Scikit-Learn, XGBoost
- Download the dataset from link provided above
- Modify the `input_data_dir` variable and point to your local directory where data the downloaded data is stored

## Contact
:love_letter: For any feedback or questions or just to say "Hi", drop me a line anytime at supratimh@gmail.com.

Thank you for reading :heart:

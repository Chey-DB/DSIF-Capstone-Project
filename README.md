# Predictive Modelling on Lending Club's Loan Application Dataset
-----------------------

## Project Overview
Lending Club is seeking the expertise of a data science consultant to perform comprehensive data cleaning, exploratory data analysis (EDA), and predictive modeling on their loan application dataset. The project will also explore the potential for deploying a real-time scoring application. The primary objective is to prepare the dataset for accurate analysis and modeling, understand the key variables influencing loan approval, and recommend a predictive model for classifying loan applications.

## Dataset Description
The dataset consists of loan application records stored in a CSV file.
The dataset contains various attributes such as applicant information, loan details, financial metrics, and application status.
A data dictionary is also provided.
The dataset can be found on Kaggle by clicking this [link](https://www.kaggle.com/datasets/ethon0426/lending-club-20072020q1).

## Objectives
1. Data Preparation and Data Cleaning
2. Exploratory Data Analysis
3. Modelling

## Deliverables
1. Insights and Recommendations based on EDA
2. Predictive Model
3. Real-Time Scoring App (dependent on outcome of predictive model)
4. Report

## Key Metrics and Acceptance Criteria
- Accuracy
- Precision
- Recall
- ROC-AUC
- The model should achieve an Acuuracy and ROC-AUC score above 80%
---------------------------------------------------------
## Executive Summary

- We started out with 100,000 samples and 143 features.
- We conducted univariate, bivariate and multivariate analysis on these features to gain insights into the data.
- We were limited in our domain knowledge due to lack of an SME. As a result, assumptions had to be made and certain decisions which may have impacted the quality of the dataset had to be taken. For example, features with more than 50% missing values were dropped as we had no way of gaining a better understanding of what this means and whether it was by design or not.
- For numerical features, either the mode or median were used to impute missing values where applicable.
- Out of the 143 original features, 37 were chosen, which includes 3 features that were engineered by combining features together. (This does not include the target).
- These features were selected by dropping one feature out of feature pairs with very high correlation (above 0.9 or below -0.9), dropping features with more than 50% missing values (as mentioned above), dropping features that are determined post-loan issuance or after acquiring a "Charged Off" status (this was done to meet the business requirements i.e a model that can predict loan defaults with the intention of using it accept or reject loan applications, other reasons for dropping columns include (but are not limited to) irrelevancy, redundancy, low variability (constant).
- There was quite a big imbalance between the target variable classes. 51258:12431 = 4.12:1 = 80.5% Fully Paid, 19.5% Charged Off.
- SMOTE was used to handle this imbalance.
- Models used were: LogisticRegression, DecisionTreeClassifier, RandomForestClassifier, CatboostClassifier and Feed Forward Neural Networks.
- SHAP was used for interpretability and through RFE we gained an understanding of the most important features.
- CatboostClassifier produced the best results - Accuracy:0.81, Precision:0.58, Recall:0.05, F1-Score:0.09, ROC-AUC:0.71 rounded to 2 decimal places.
- Our best model did not meet the evaluation metrics required for this model to be productionised.

## Conclusion
The best model does not meet the needs and criteria of the business with regards to the evaluation results. Despite attempts to make up for the class imbalance, the models were not able to distinguish between the two classes with a heavy bias towards "Fully Paid". From my understanding of the business, this could cost the Lending Club a lot of money as false negatives i.e predicting that the person will not default on the loan when in actual fact they will costs the business more than predicting that they will default on the loan when in actual fact they won't. For this reason, the model cannot be used by the business as intended.

## Insights
1. Over 20% of the data had more than 50% of the values missing.
2. About 90% of people who were "Charged Off" did not have a hardship plan.
3. People with one of more public records of bankruptcies are more likely to be "Charged Off" on their loan.
4. The original data contains a lot of redundant features.
5. The original data contains a lot of features that are post-loan issuance but have a status of "Current".
6. The higher the grade/sub-grade the more likely a customer is to default on their loan.
7. Debt-to-income ratio was the most important feature in determining whether someone would default on a loan or not.

 ## Recommended Actions (Next steps) - based on key insights above
 1. I'm not sure what the reason for the missing values is but that data could prove valuable in building a robust and accurate model. If the missing values are a result of customers not filling out certain parts of forms, then those fields should be made mandatory or a default value should be placed there that best describes the meaning of a blank field. This will lead to beter data quality, which can lead to better model accuracy, which means better decision making and money savings through determining whether someone will be "Charged Off" or not.
2. More effort should go into setting up a hardship plan for people who either have a significant dip in their fico_score or fall into the late category to prevent customers from getting to the "Charged Off" stage.
3. Interest rates should be closely tied to the number of bankruptcies so that even if a customers loan is "Charged Off", we can still break even or people with one or more bankruptcies should need to provide some form of collateral or have a guarantor to minimise the risk.
4. Proper implementation of ETL/ELT pipelines including data validation, data redundacy check etc. should be carried out to improve the quality of the data. The better the quality of the data, the better the model can learn.
5. As it stands the current best model cannot be used to predict loan defaults without the business incurring a massive loss. However, the post-loan issuance data/features can be used to build a model for early detection/signals of defaults so that the necessary actions can be taken to help prevent the loan from defaulting such as initiating a hardship plan or providing customers with financial advice to help them stay on track with monthly installments.
6. Interest rates should be highly determined by grade/sub-grade since number of defaults goes up linearly with grade/sub-grade.
7. Customers with high debt-to-income ratio should be checked thoroughly, looking and public records of bankruptcies or high credit stress can help with making more informed decisions on whether to accept a loan application or not.

# Predicting-customer-churn-competition

A solution of the [credit card customers competition](https://www.kaggle.com/sakshigoyal7/credit-card-customers).

The goal of this project is to predict the customers who want to cancel a credit card program, such that actions can be taken to prevent the event from happening.

The top priority is to identify customers who are getting churned. Even if we predict non-churning customers as churned, it won’t harm our business. But predicting churning customers as non-churning will do. So recall (True positives/(True positives + False negatives) must be high.

The dataset is strongly un-balanced: only 16% of customers churned.

The notebook is organized as follow:

+ In Section 1, the dataset is explored, checking if null values are present.

+ In Section 2, feature engineering is performed as follow:
    + The categorical target feature (the Attrition_Flag) is converted to numerical.
    + Other categorical features are one-hot encoded.
    + The dataset is divided into train and test, using stratified sampling.
    + The outliers in the training dataset are identified.
    + A data preprocessing pipeline is built, removing the outliers identified in the previous step and standardizing each feature.
    + Highly correlated features are removed, identifing highly correleted feature pairs
    + Highly multicollinear features are removed, estimating the variance inflation factor
	

+ In Section 3, XGBoost is used as a model for predicting churned/not churned customers. Model hyperparameters are searched as follow:
    + An objective function is defined. The objective function computes the average value of the cross-validation score on the training dataset, using the negative log loss as a scoring metric
    + Being the dataset strongly imbalanced, the minority class is oversampled using SMOTE and the majority class randomly undersampled. This process is repeated on each train set of the cross validation fold.
	+ The maximum value of the objective function is searched using the Bayesian framework Optuna [https://optuna.org/]
    + On the test dataset, the recall value is 0.9490

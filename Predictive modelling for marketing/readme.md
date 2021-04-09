# Predictive modelling for marketing

The main goal of this project is to develop machine learning model to predict customer acceptance of promotional campaign. The dataset is composed by several features of socio-demographic, purchasing and promotional nature. In the notebook you can find end-to-end development process, where I'm going through data exploration & cleansing (outlier identification), enrichment (creation of new features), feature selection and last but not the least predictive modelling.

## Data

I'm using customer data of a certain retail chain, which sells different products (electronics, games, etc.) via online platform and physical stores. You can find data [here](https://github.com/VasylTsykolanov/Data_Science_Portfolio/blob/main/Predictive%20modelling%20for%20marketing/Store_Campaign.xlsx). The dataset contains the following features about customers:


* Custid: unique identification number
* Year_Birth: year of birth
* Education: educational level
* Marital_Status: marital status
* Income: yearly income
* Kidhome: how many kids at home
* Teenhome: how many teens at home
* Dt_Customer: first purchasing date
* Recency: how many days since the last purchase
* MntMiniatures: spending on products of type miniatures
* MntPainting_Material: spending on products of type painting material
* MntCard_Games: spending on products of type card games
* MntMagazines: spending on products of type magazines
* MntScenario: spending on products of type scenario/decorations
* MntBrandA_Material: spending on products of type Brand A Material
* NumDealsPurchases: number of promotional deals while purchasing products
* NumWebPurchases: number of web purchases
* NumCatalogPurchases: numer of purchases from catalogue
* NumStorePurchases: nnumber of purchases from store
* NumWebVisitsMonth: number of web visits per month
* AcceptedCmp1: if accepted 1st promotional campaign
* AcceptedCmp2: if accepted 2nd promotional campaign
* AcceptedCmp3: if accepted 3rd promotional campaign
* AcceptedCmp4: if accepted 4th promotional campaign
* AcceptedCmp5: if accepted 5th promotional campaign
* Complain: if had any complain
* Z_CostContact: cost of contacting
* Z_Revenue: revenue if accepting campaign
* DepVar: Target variable - if accepted promotional campaign or not

## Data cleansing & Outlier detection

Missing values were treated by using imputation technique. We are using imputation in order to 1) Not to lose relevant observations and 2) Not to change original data distribution. Therefore, I used median imputation for interval data and mode imputation for categorical data.

Outliers were identified and removed based on two-step approach: 1) Identify features with very uncommon observations via [interquartile range method (IQR)](https://online.stat.psu.edu/stat200/lesson/3/3.2) method, which was scripted in _detect_outliers_ function and 2) For each feature with uncommon observations we create scatterplots to visualize the data and decide on outliers. Based on this method 82 outliers were identified and removed from dataset.

Here you can visualize the process:

![outlier detection](https://github.com/VasylTsykolanov/Data_Science_Portfolio/blob/main/Predictive%20modelling%20for%20marketing/images/Outlier%20detection.PNG)

## Correlated features detection

Correlated features were removed to increase simplicity (with less variable as possible but still highly accurate) of machine learning model. Two-fold approach was taken to detect correlated features:

1) Detect correlated features - [Spearman correlation matrix] (https://en.wikipedia.org/wiki/Spearman%27s_rank_correlation_coefficient) to detect numerical correlated features and [Chi-Square test of independence] (https://en.wikipedia.org/wiki/Chi-squared_test) to detect categorical correlated features. The logic was embedded into function _detect_correlation_.
2) Assess feature importance, when predicting target variable and remove correlated features, which does not have a very high importance when predicting target variable.

Ex: Feature A is correlated with Feature B. However, Feature A is more important to predict target variable. Therefore, feature B is removed.

Here you can see Spearman correlation matrix:

![correlated_features](https://github.com/VasylTsykolanov/Data_Science_Portfolio/blob/main/Predictive%20modelling%20for%20marketing/images/corr.png)

## Feature selection and machine learning model training

Feature selection was done for the purposes of dimensionality reduction. It was used [Extra Trees](https://medium.com/@namanbhandari/extratreesclassifier-8e7fc0502c7) algorithm, which is ensemble learning method fundamentally based on decision trees. 


Here you can see the top15 of features and its respective importance while predicting target variable (if customer accepted promotional campaign):
For example, Recency is very important when predicting target variable. We can interpret it as customer activity pattern (if he/she made any purchase recently) is a very good predictor of promotional campaign acceptance.

<img src="https://github.com/VasylTsykolanov/Data_Science_Portfolio/blob/main/Predictive%20modelling%20for%20marketing/images/feature_selection.PNG" width="500">

## Train Gradient Boosting model

Finally, [Gradient Bossting](https://docs.paperspace.com/machine-learning/wiki/gradient-boosting) model was trained. It is a popular supervised machine learning technique for regression and classification problems that aggregates an ensemble of weak individual models to obtain a more accurate final model.

Here you can see the training process from high-level perspective:

![Gradient](https://github.com/VasylTsykolanov/Data_Science_Portfolio/blob/main/Predictive%20modelling%20for%20marketing/images/akira-ai-gradient-boosting-ml-technique.png)

In order to train ML model, hyperparameter tunning was used, where the goal is to find the best possible combinations of parameters for ML algorithm, which would maximize the accuracy of our model. In this case, learning rate (learning_rate), the number of boosting stages to perform (n_estimators) and  number of terminal nodes (max_depth).

It was possible to achieve the model accuracy of _94.7%_.

## Future work

The next step for this project would be to make the machine learning model available via API as a service. This service will not only include ML model but also functionalities of detecting & removing outliers, detection of correlated features detection and feature selection, which I developed during this project.












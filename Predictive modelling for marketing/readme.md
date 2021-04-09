# Predictive modelling for marketing

The main goal of this project is to develop machine learning model to predict customer acceptence of promotional campaign. The data set is composed by several features of socio-demographic, firmographic and promotional nature. In the notebook you can find end-to-end development process, where I'm going through data exploration & cleansing (outlier identification), enrichemnt (creation of new features), feature selection and last but not the least predictive modelling.

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
* NumDealsPurchases: number of promotional deals while pruchasing products
* NumWebPurchases: number of web purchases
* NumCatalogPurchases: numer of purchases from catalog
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

## Outlier detection

Outliers were identified and removed based on two-step approach: 1) Identify features with very uncommon observations via [interquartile range method (IQR)](https://online.stat.psu.edu/stat200/lesson/3/3.2) method, which was scripted in _detect_outliers_ function and 2) For each feature with uncommon observations we create scatterplots to visualize the data and decide on outliers. Based on this method 82 outliers were identified and removed from dataset.

![outlier detection](https://github.com/VasylTsykolanov/Data_Science_Portfolio/blob/main/Predictive%20modelling%20for%20marketing/images/Outlier%20detection.PNG)

## Correlated features detection

Correlated features were removed to incirease simplicity (with less variable as possible but still highly accurate) of machine learning model. Two-fold apporach was taken to detect correlated features:

1) Detect correlated features - [Spearman correlation matrix] (https://en.wikipedia.org/wiki/Spearman%27s_rank_correlation_coefficient) to detect numerical correlated features and [Chi-Square test of independence] (https://en.wikipedia.org/wiki/Chi-squared_test) to detect categorical correlated features. The logic was embedded into function _detect_correlation_.
2) Assess feature importance, when predicting target variable and remove correlated features, which does not have a very high importance when predicting target variable.

Ex: Feature A is correlated with Feature B. However, Feature A is more important to predict target variable. Therefore, feature B is removed.

![correlated_features](https://github.com/VasylTsykolanov/Data_Science_Portfolio/blob/main/Predictive%20modelling%20for%20marketing/images/corr.png)

## Feature selection

Feature selection was done for the purposes of dimensionality reduction. For feature selection we used [ExtraTreesClassifier](https://medium.com/@namanbhandari/extratreesclassifier-8e7fc0502c7) , which is ensemble learning method fundamentally based on decision trees.













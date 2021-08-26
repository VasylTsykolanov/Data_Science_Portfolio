# Electronic Products and Pricing Data

The main goal of this project is to identify retail industry trends in pricing strategy and develop solution for price positioning. The dataset is a list of over 15.000 electronic products with pricing information. In the first notebook (price_recommend_data_explore.ipynb) you can find data explanatory analysis, where I'm going through data explore, cleansing (outlier identification) and enrichment (creation of new features). Also, I'm trying to understand how different product characteristics affect the pricing. (e.g. What role does a product’s category play in its listing price?). In the second notebook (price_recommend_solution.ipynb) I'm accessing the development of pricing solution based on the dataset, which was cleaned and enriched in previous step.


# Data

I'm using data from [Kaggle](https://www.kaggle.com/datafiniti/electronic-products-prices) with pricing info about products and its characteristics (brand, category, merchant, name, source, etc.) 
You can find full metadata by this [link](https://developer.datafiniti.co/docs/product-data-schema).

* **price_recommend_data_explore.ipynb** contains data exploration and transformation code
* **price_recommend_solution.ipynb** contains machine learning code


## Data challenges

Several features were transformed in order to ensure data quality and consistency. Some of the examples are price and weight of product, which were presented in different units in the dataset. 
Products were measured in pounds, kilograms, ounces, etc. In order to execute EDA properly and apply ML algorithms, product weight was converted into pounds.

<image src = "https://github.com/VasylTsykolanov/Data_Science_Portfolio/blob/main/Price%20positioning%20of%20electronic%20products/images/weight.png" width = "250">
  
Same logic was applied to product price, since it was measured in different currencies (USD, CAD, EUR, etc.).
Another data issue was missing values. Imputation was used in order to 1) Avoid losing relevant observations and 2) Avoid changing original data distribution. Therefore, we used median imputation according to the product category (e.g. missing values in product weight of specific television are imputed with median value of category “TV”).
Outliers were identified and removed by using interquartile range method (IQR). Further, each feature with uncommon observations was analyzed. Box plot example of price feature with some outliers:

<image src = "https://github.com/VasylTsykolanov/Data_Science_Portfolio/blob/main/Price%20positioning%20of%20electronic%20products/images/boxplot.png" width="450">

## Price analysis

As we can see, the distribution of feature price is mostly got skewed to right side. This is because of varying density in that price range.
  
<image src = "https://github.com/VasylTsykolanov/Data_Science_Portfolio/blob/main/Price%20positioning%20of%20electronic%20products/images/price_dist.png" width = "800">
  
As a next step, I analyzed how price distribution changes depending on brand. As we can, average price of Intel products is higher compared to HP. Therefore, we can assume that brand might be important predictor while explaining product price.
  
<image src = "https://github.com/VasylTsykolanov/Data_Science_Portfolio/blob/main/Price%20positioning%20of%20electronic%20products/images/price_dist_brand.png" width = "800">

Same conclusions were derived when looking into product category. For this analysis two product categories were selected – Camaras and Accessories (e.g. portable power banks, chargers, adapters, etc.). As expected, the average price of product is influenced by the product category. Average price of accessories is lower compared to cameras.
 
<image src = "https://github.com/VasylTsykolanov/Data_Science_Portfolio/blob/main/Price%20positioning%20of%20electronic%20products/images/price_dist_product_cat.png" width = "800">

Another interesting insight was generated when looking into the relationship between product weight and price. When analyzing scatterplot, we can see that there is a slight correlation between two features, which can also be expected. On average, heavier products tend to cost more (e.g. TV is heavier than portable charger).
  
<image src = "https://github.com/VasylTsykolanov/Data_Science_Portfolio/blob/main/Price%20positioning%20of%20electronic%20products/images/price_dist_prod_weight.png" width = "500">
  
 ## Feature selection and final solution
  
Feature selection was done in order to understand the importance of each factor when explaining product price. Random Forest and Gradient Boosting were used with [random search] (https://scikit-learn.org/stable/modules/generated/sklearn.model_selection.RandomizedSearchCV.html) of parameters (Random search is a method in which random combinations of hyperparameters are selected and used to train a model. The best random hyperparameter combinations are used.)
Here you can see the importance of all features while predicting price. For example, product weight is the most important predictor of product price. Also, it’s important to consider number of days since the product was added into data base (n_days_since_added). Other important predictors are product manufacturer (manufacturerNumber), brand (brand_x) and categories (category_0, category_1, category_2, category_3, category_4, etc.). These categories are keywords used to identify product. Example of product: category_0 (Home Improvement), category_1 (Heating, Cooling, & Air Quality), category_2 (Heaters), category_3 (Propane Heaters), etc.

<image src = "https://github.com/VasylTsykolanov/Data_Science_Portfolio/blob/main/Price%20positioning%20of%20electronic%20products/images/feature_imp.png" width = "800">
  
## Future work

Before running ML algorithms, I built baseline model. The reason for baseline model is to compare it with ML model, which uses advanced algorithms. It needs to be simple to set up and has a reasonable chance of providing decent results. In our case baseline model is simply the average price of product categories. Example:

<image src = "https://github.com/VasylTsykolanov/Data_Science_Portfolio/blob/main/Price%20positioning%20of%20electronic%20products/images/baseline_model.png" width = "800">
  
With baseline model I was able to obtain Mean Absolute Error (sum of absolute differences between predicted price and actual price) of 104.
However, when using Gradient Boosting, the Mean Absolute Error was 92, which is only slightly better than very simplistic approach of averaging the price of categories and use it as a recommended price.
Therefore, in order to improve quality of ML solution, we would need to improve data quality as well. Dataset has a lot data issues (skewness, strange values, errors, etc.). If these issues are solved, ML model could gain significant performance. Also, another suggestion could be to include demand data from POS systems, which I didn’t have when developing final solution.

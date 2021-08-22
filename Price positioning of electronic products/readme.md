# Electronic-Products-and-Pricing-Data

The main goal of this project is to identify retail industry trends in pricing strategy and develop solution for price positioning. The dataset is a list of over 15.000 electronic products with pricing information. In the first notebook (price_recommend_data_explore.ipynb) you can find data explanatory analysis, where I'm going through data explore, cleansing (outlier identification) and enrichment (creation of new features). Also, I'm trying to understand how different product characteristics affect the pricing. (e.g. What role does a product’s category play in its listing price?). In the second notebook (price_recommend_solution.ipynb) I'm accessing the development of pricing solution based on the dataset, which was cleaned and enriched in previous step.


# Data

I'm using data from [Kaggle](https://www.kaggle.com/datafiniti/electronic-products-prices) with pricing info about products and its characteristics (brand, category, merchant, name, source, etc.) 
You can find full metadata by this [link](https://developer.datafiniti.co/docs/product-data-schema).

* **price_recommend_data_explore.ipynb** contains data exploration and transformation code
* **price_recommend_solution.ipynb** contains machine learning code


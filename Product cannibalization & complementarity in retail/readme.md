
# Product cannibalization & complementarity in retail - under construction

For retail companies it is of great importance to understand how their customers take purchase decisions. Complementarity of products is well-known classical case of applying data science in retail industry. However, it is of special interest to also measure customer propensity to switch from one product to another (product cannibalization) in situations when one product goes on promotion or lacks availability. This information have several benefits, namely 1) It can be used to improve demand forecasting accuracy, 2) To better understand products and CUSTOMER decisions, which will lead into 3) Increase of customer satisfaction. In the notebook I show how to calculate product cannibalization effect by using Apriori algorithm. Also, you will find how we can cluster products WITHOUT USING ANY master data.

## Data

I'm using OnlineRetail dataset. This is a transnational data set which contains all the transactions occurring between 01/12/2010 and 09/12/2011 for a UK-based and registered non-store online retail. The company mainly sells unique all-occasion gifts. Many customers of the company are wholesalers.


You can find data [here](https://github.com/VasylTsykolanov/Data_Science_Portfolio/blob/main/Product%20cannibalization%20%26%20complementarity%20in%20retail/OnlineRetail.zip). The dataset contains the following features:

* InvoiceNo: Invoice number. Nominal, a 6-digit integral number uniquely assigned to each transaction. If this code starts with letter 'c', it indicates a cancellation.
* StockCode: Product (item) code. Nominal, a 5-digit integral number uniquely assigned to each distinct product.
* Description: Product (item) name. Nominal.
* Quantity: The quantities of each product (item) per transaction. Numeric.
* InvoiceDate: Invice Date and time. Numeric, the day and time when each transaction was generated.
* UnitPrice: Unit price. Numeric, Product price per unit in sterling.
* CustomerID: Customer number. Nominal, a 5-digit integral number uniquely assigned to each customer.
* Country: Country name. Nominal, the name of the country where each customer resides.

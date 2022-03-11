
# Predict Fake or True news

The main goal of this project is to develop machine learning model able to determine if an article is fake news or not. The dataset is composed by several features of text nature. In the notebook you can find ent-to-end development process. In the notebook I go through data exploration, cleaning, visualization and modelling. In the data modelling section (Create ML models based on text field) I use 2 apporaches: 1) Use 3 specific ML-Based algorithms to train text classifier and 2) Build simple model with only one feature. By using the 2nd method, I was able to 99% of accuracy.

# Data

I'm using data from Kaggle, which can be found [here](https://www.kaggle.com/clmentbisaillon/fake-and-real-news-dataset). The data set contains the following features:

* Title: the title of the article
* text: the text of the article
* subject: The subkect of the article (Middle-east, politics, government, etc.)
* date: The date at which the article was posted

# SneakerMove 1.0 - What's Your Move?

## Problem Statement

The sneaker culture blew up mostly in part to basketball and hip-hop and is still a massively rapid growing culture. Many sneakerheads collect sneakers with some people collecting sneakers of different time periods, models, and colorways. Highly sought-after or limited quantity sneakers have marked-up resale prices. Sneakers can go as high as thousands of dollars with many people more than willing to pay those prices. StockX is a platform for buying and selling authentic sneakers where buyers make bids for the sneakers they want and sellers set asking prices for the sneakers they’re willing to sell. 

I want to create a suggesting function in which the user selects a sneaker that is registered in our database, and returns prediction of the resale price of the sneaker over the course of time while providing the user with suggested actions on whether to sell the sneaker, hold off on the sneaker, or buy the sneaker.
- Class 0: Sell the sneaker because it is at an estimated high price
- Class 1: Hold off on the sneaker because the price is a relative mean to historic sales
- Class 2: Buy the sneaker because it is at an estimated low price

## Workflow
1. Data Collection
- To accomplish this, I will investigate the resale prices over time by retrieving historic sales data on StockX using their api, preprocessing the data, and running LSTM models on the time series as well as multiclass classification logistic regression on suggesting the course of action to the user. The dataset coming from [StockX]('https://stockx.com/retro-jordans') will consist of 992 Jordan sneaker, all of the historic sales data including their respective unique product id, sales timestamp, and resale price totalling to 1.3 million rows of sales. The historic sales data includes all sales up until Jan 27, 2019.

2. Exploratory Data Analysis
- The data was relatively clean in json format. Dates were cleaned of timestamps, duplicates shoes were removed. The 1.3 million rows of historic sales data was reduced to ~130,000 when all the sales were aggregated to weekly average sale prices. Sale price was plotted against shoe size to observe any particular trends. The higher of sale price of shoe sizes were between 8 and 13. Shoe size was plotted against number of sales. The higher of amount of sales of shoe sizes were between 8 and 13.

3. Modeling
- Persistence Forecast Baseline Model
    - rmse = 15.456
- LSTM Model
    - rmse = 14.163
    - performed slightly better than baseline model
- Multiclass Classification Logistic Regression Model
    - accuracy score: between 50% and 97%
    - very wide range, not accurate at all
    
## Model Takeaways
The LSTM Model can be further investigated through applying different preprocessing methods as well as the parameters of the model. I noticed that sneakers with longer historic data tend to work better with the model as the model learns the trends whereas for sneakers with shorter historic data, the predictions tend to more or less converge to the mean. Although the rmse of the LSTM model is low, there needs to be further investigation to explore the possibilities of various number of nodes, neurons, sliding window sizes, epochs, and different approaches to preprocessing input data.

For the multiclass classification logistic regression model, the confidence is between 50% to 97% which is a huge difference and proves the model is not very accurate and needs work. More investment into the EDA and how I input the data can be further investigated. Different approaches to process the input data as well as the modeling parameters must be explored to improve the model.

## Conclusions
Use the LSTM model as the production model because it performed very well and can be further tuned with more preprocessing steps and hyper parameters. The Multiclass Classification Logistic Regression Model did not perform very well and needs work. Therefore the model should not be used yet. Further preprocessing steps as well as how the model works with the data should considered and various methods should be applied to check for accuracy metrics. Next steps would be to consider using another outside source to serve as a signal to not help forecast the time series but also verify key trends in how the data acting with the models in order to best choose how to preprocess the data inputing to both the LSTM model and the multiclass classification logistic regression model. The possible outside source would be to scrape popular social media platforms such as Twitter or popular forums such as Reddit for various ways in measuring counts and frequencies of sneaker name mention, post or comment.
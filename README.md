# Project : Forecasting Future Restaurants Customer Visits.     
Author:  Anna Pavlova

## Problem Statement:
Making predictions of future events is a difficult task for multiple reasons. This project explores data science techniques to forecast future daily customer visits in in restaurants across Japan. Everybody knows restaurant business is tough and risky. Predicting future visitors would alleviate some risk by helping restaurants make informed decisions, plan ingredient purchasing and staff scheduling requirements. Many factors may affect the outcome, including location, local competition and even weather. It is difficult for restaurants to predict how they will do; however historical data may help and foresee either an imminent decline or sudden success.  

### Data Description Summary:
Analysis presented here takes advantage of Kaggle dataset, provided by AirRegi/Restaurant board website, that tracks restaurant reservations and cash register systems at restaurants across Japan. The main dataset includes number of customer visits spanning a time period of January 2016 through May 2017 at 82 unique (anonymized) restaurants. The main challenge is to predict future visitors based on the limited information available in main dataset, composed of restaurant ID, date and number of visitors. Fortunately, additional related databases are available and include geo-spatial locations (latitude, longitude), cuisine genre, restaurant area names, calendar holidays. 

### Data Exploration:
Various aspects of the data were explored with an aim to find relationships between number of visitors at given restaurant and factors like: time, geographical location (latitude, longitude), cuisine genre, type of restaurant as well as statistical summaries of visitors at a given restaurant on given day of the week. The number of daily visitors seems to have a strong weekly cycle in all restaurants. However, individual restaurant’s daily visitor cycles differ drastically, which indicates many other factors may impact number of visitors at each place. Further exploratory data analysis showed that factors such as geographical location (latitude, longitude), cuisine genre and type of restaurant, all have a significant effect on daily visits and weekly visits on a restaurant-specific basis. 

### Approach:
The most intuitive approach to number of visitors’ pattern prediction was to use time series analysis techniques such as ARIMA or FB Prophet, were predictions would be made on correlation patterns of data points alone. Next, the problem was translated into regression-based prediction techniques with incorporation of engineered features such as decomposed time attributes, geo-spatial latitude and longitude, cuisine genre, type of restaurants and statistical summaries of visitors at specific restaurants on specific weekdays. The statistical summaries included specific restaurant week-day specific visitors minimum, maximum, mean, median for each specific restaurant. 

### Analytical Process and Production Models:
A baseline scores of Root Mean Square Error (RMSE) was established first as a mean number of visitors per weekday for all restaurants and second as a mean number of visitors per weekday per each restaurant individually. The aim of the further analysis was to obtain a better RMSE score by modeling the predictions with various techniques.
First, ARIMA time series analysis was performed. The time series data for one of the stores was used as an example. The autocorrelation and partial autocorrelation of time points in the data was examined and strong weekly correlation between data point was detected.  Data was checked for stationarity and appropriate degree of differencing of the data was determined using Dickey-Fuller test to make it stationary and appropriate for ARIMA analysis.  Auto_arima model from ‘pmdarima’ python package was used to further optimize and find optimal parameters of p (autoregressive term) and q (moving average order) for daily as well as Seasonal parts of auto_arima. Visual inspection of the result revealed poor fit of weekly/daily trend, however with a good overall yearly trend of the time series. RMSE metric was found to be higher than the baseline score even with optimal parameters. 

Next, Prophet (developed and provided by Facebook) package was used, which deals with seasonality and missing data among other aspects of time series data in a more automated statistical manner. This model resulted in a much better visual fit of time series yearly, weekly and daily patterns, however RMSE metric was still higher than the baseline score. 

Finally, the problem was reformulated for a multiple feature regression analysis. Here advantage was taken of several relational data based in the dataset. The customer visit database was merged with databases containing information on geo-spatial latitude and longitude, cuisine genre, type of restaurant, which were used as features in the regression analysis. In addition, statistical summaries of week-day specific visitors minimum, maximum, mean, median for each specific restaurant, which values were also used as features in the regression analysis. Visit date parameter (originally in year-month-day format) was decomposed into four different features of year, month, day of the year and weekday and all four parameters were used as separate features in the regression analysis. This merged database with engineered features and containing all of the restaurants in the system was used in the regression analysis using Random Forest model. Resulting forecast resulted in visitor predictions for each restaurant with a record-low RMSE value, drastically lower than the baseline score. 

## Conclusions:
Prediction of daily visitors at different restaurants in Japan depends on many different parameters, including date, location, cuisine genre, restaurant type. This type of data is easily accessible through combination of data mining and datasets collected through AirRegi/Restaurant board website. Accurate forecasting of future restaurant visitors was achieved via data science modeling process and may be used to significantly relieve the pressure of planning daily operations in tough restaurant business. 

## Limitations and Next Steps:

It is custom to treat restaurant visitor forecasting problems as time series problems that are intuitively treated with modeling techniques such as ARIMA and Prophet.  However, some of the very important potential factors affecting restaurants visitations cannot be accounted for by ARIMA analysis. Here a time series problem was turned into a regression problem, where multiple engineered features can be used to make accurate visitor forecasting. In next steps several more features could be explored. First advantage can be taken from geo-spatial data, for example determining spatial proximity of each restaurant from busiest areas. Second, data about the weather in different areas of the country could be used and additional features could be engineered from this data to be used in the proposed regression model. 

### Data Dictionary:
|Feature|Description|
|---|---|
|**air_visit_data.csv**|The file contains historical visit data for the air restaurants| 
|**date_info.csv_**|The file gives basic information about the calendar dates and date combination| 
|**air_store_info.csv**|The file contains information about select restaurants| 
|**air_reserve.csv**|The file contains reservations made in the system| 

### Data Sources:

We used Kaggle Dataset 'Recruit Restaurant Visitor Forecasting'.
Source: 
[Kaggle](https://www.kaggle.com/c/recruit-restaurant-visitor-forecasting/data) 
                  
# Anna Pavlova GA-DSI-7 Capstone-Project
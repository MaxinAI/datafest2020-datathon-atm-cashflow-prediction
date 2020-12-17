# ATM cashflow prediction

# LSTM Model
## EDA
Time series data had positive trends with different magnitude per year/month/day. But the target variable had different time series properties across different ATM, hence decided to use LSTM network which is able to predict on different targets which differ by some features. 

## Model
We applied LSTM model with the features that were available. Time series values of ATM total withdrawal (scaled) and ID of ATM. We used 7 day window for LSTM.  2017-2018 is for training set and 2019 for test set.  
The MAE score on train set was 0.0700 and test set was 0.0850. 

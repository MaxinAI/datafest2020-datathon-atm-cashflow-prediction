# ATM cashflow prediction

# ARIMA Model
will be added soon

# LSTM Model
## EDA
Time series data had positive trends with different magnitude per year/month/day. But the target variable had different time series properties across different ATM, hence decided to use LSTM network which is able to predict on different targets which differ by some features. 

## Model
We applied LSTM model with the features that were available. Time series values of ATM total withdrawal (scaled) and ID of ATM. We used 7 day window for LSTM.  2017-2018 is for training set and 2019 for test set.  
The MAE score on train set was 0.0700 and test set was 0.0850. 


# Some Insights
- Some ATM's didn't have all records. Missing records mean that they didn't work for given days. We assume that they stopped working in given days. In case they end before 2019-12-31 we could remove them from consideration, because they may never function in 2020.
- Some ATM's does have 0.0 values for several consecutive days, which means that they didn't have money for these days or stopped working temporarily (continued after fixing or filling money in). I think that prediction of such problems isn't easy since they are unexpected events. The option is to fill these values with model predictions (do some augmentation with independent time series models).
- Clusterization of different ATM's can be done by analyzing their cashflow time series data, calculate correlation between them and do some custom clusterization to find ATMs that have similar cashflow patterns. 
- Looking at the time series data, we can find some spikes in times series which can be used as Holiday like features. But as I found spikes in global trend not always generalize to each ATM. Holiday dates and maybe previous and next week are very informative because sometimes people buy things before holiday and sometimes on holiday week.
- Change the count of total ATMs in time could be informative also, because increase of ATM's would actually decrease the cashflow in neareset ATMs. Neighborhood could be calculated by Map coordinates, etc.
- We would recommend to use non-symmetric evaluation metrics. If prediction is higher than actual it means that there are some extra money in ATM which is ok but prediction is lower than actual it means that no money will be left and it's a problem for customers. I would put less weight for positive difference between predicted and actual and more weight on negative ones.

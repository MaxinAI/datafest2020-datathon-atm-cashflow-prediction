# ATM cashflow prediction

## ARIMA Model

At the very last moment we decided to use ARIMA(1,1,1) as the training other models took lots of time. By observing model statistics we conclude that the model is valid. However, it's not complex enough to extract all the information from the noise term. Hence, we have left some useful information in the error which have could been harnessed for more accurate forecasting.

## LSTM Model

## EDA

Time series data had positive trends with different magnitude per year/month/day. But the target variable had different time series properties across different ATM, hence decided to use LSTM network which is able to predict on different targets which differ by some features. 

## Model

We applied LSTM model with the features that were available. Time series values of ATM total withdrawal (scaled) and ID of ATM. We used 7 day window for LSTM.  2017-2018 is for training set and 2019 for test set.  
The MAE score on train set was 0.0700 and test set was 0.0850. 

## Some Insights

- Some ATM's didn't have all records. Missing records mean that they didn't work for given days. We assume that they stopped working in given days. In case they end before 2019-12-31 we could remove them from consideration, because they may never function in 2020.
- Some ATM's does have 0.0 values for several consecutive days, which means that they didn't have money for these days or stopped working temporarily (continued after fixing or filling money in). I think that prediction of such problems isn't easy since they are unexpected events. The option is to fill these values with model predictions (do some augmentation with independent time series models).
- One possible reason why some ATMs did not have 0.0 values could be that those ATMs were inside some building and this building was close. Hence, the team who was responsible to put money in ATM could not do that.
- Clusterization of different ATM's can be done by analyzing their cashflow time series data, calculate correlation between them and do some custom clusterization to find ATMs that have similar cashflow patterns. 
- Looking at the time series data, we can find some spikes in times series which can be used as Holiday like features. But as I found spikes in global trend not always generalize to each ATM. Holiday dates and maybe previous and next week are very informative because sometimes people buy things before holiday and sometimes on holiday week.
- One of the helpful insight is that the ATMs close to country borders and airports can exhibit different behavior compared to other ATM. Generally, the demand for cash in such places are higher and does not follow clear trend.
- It's also noteworthy what is the effect of payroll to ATM cashflow. Generally, at the last friday of the month or 25th of each month there are wages of different people. This may increase the demand for a cash and hence have high withdrawal.
- Change the count of total ATMs in time could be informative also, because increase of ATM's would actually decrease the cashflow in neareset ATMs. Neighborhood could be calculated by Map coordinates, etc.

## Recommendations

- We would recommend to use non-symmetric evaluation metrics. If prediction is higher than actually it means that there are some extra money in ATM which is ok but prediction is lower than actual it means that no money will be left and it's a problem for customers. I would put less weight for positive difference between predicted and actual and more weight on negative ones.
- Data augmentation would also be very helpful for forecasting. Possible features could be geospatial data. For example the distance between ATM and service center which is responsible to put money in that ATM. The distance between ATM's. Proximity of the ATM to the border or airport or shopping mall.
- The incorporation of the COVID-19 effect can be done by re-fitting the model, changing the parameters or even taking completely new model which will be able to capture the trend changing time series behavior.

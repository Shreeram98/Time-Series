					               Time Series


Whether you are a scientist who is analysing the tsunami/earthquake data and trying to predict the next one to occur or you are a business analyst trying to find the time when customers are more likely to buy certain products ,understanding time series is essential to making a better data informed decisions.
 
This introduction to Time series will be helpful in understanding the components that make up a series like trend,seasonality and noise.
It will also delve upon how to remove some unwanted characteristics and why we would want to remove them.

Time Series:

Time series is a sequence of data points in chronological sequence,often gathered in regular intervals of time.Time series analysis can be applied to any variable that changes over time.

Components of Time Series Data:

Any time series data includes trend,seasonality,noise(randomness),curve.It is also important to know that not all time series data consists of all the components.Let us take an example of audio file.This audio file does not have seasonality component in it.Whereas some fields like online shopping data contains seasonality component(if it is festival time , sales goes up).

Level: It describes the mean of the series

Noise:It is unavoidable,all the time series data consists of noise and it is left to the reader to know how to get rid of that noise.

Seasonality: It is the regular and predictable fluctuations occurring in the data.It is important to know that seasonality is domain specific,for example during the weekends there may be more number of movie tickets sold when compared to weekdays.

Trend: Trend gives us the first impact on the data.If the curve is going up our general understanding says that there is a rise in the number of tickets sold(in our movie ticket example).

Cycles: Cycles are not related to calendar.This includes audio files that contains cycles which do not make sense in relating them to the months,weeks or days of a calendar.

It is hard to see seasonality and other components in the data, we use a technique called "decomposition" to identify the various parts of our series.

There are two types of Time Series:

1.Multiplicative Time Series
2.Additive Time Series

When the fluctuations in the time series increase over time and dependent of the level of the series,then we call it as Multiplicative Time Series

		Multiplicative Model= t*s*n (trend * seasonality * noise)

When the fluctuations stay constant over time, we call it as Additive Time Series.

		    Additive Model= t+s+n (trend + seasonality + noise)

Additive Models should be constant and are independent of the level over time.

It is important to know whether your data is Additive or Multiplicative in order to decompose the data.

What is decomposition?
Decomposition is the deconstruction of series data into various components "if they exist".
The main aim of decomposing the series is to look at the components individually without these components being influenced by other component like seasonality,trend,noise.
For example, if we want to look at the trend of the stock market,we would like to remove the noise produced due to randomness.
It is difficult to find out the trend in the presence of seasonality and noise.

Moving Averages:

We have alreaday seen the ways to remove the noise from the data by decomposing.Sometimes we would like to just reduce the noise and make the curve smoother inorder to better forecast the future.

A moving average model leverages the average of the data points that exist in a specific overlapping subsection of the series.
Moving Average is taken on the first subset of data and then it is moved forward by dropping the initial point.It can give us information about current trends and also reduce the noise in the data.It is a common step done before forecasting.It is used to find the short term trends.

We will cover one of the simple moving average models called Auto Regressive Integrated Moving Average(ARIMA).

I would like to take a slight detour to make you understand what a Simple Moving Average is.

Simple Moving Average(SMA):

SMA is calculated by taking the moving average as mentioned above,adds together the data points and then takes the average over the subset of data.It can help in identifying the direction of the trend(rise or fall).

There is also Exponential Moving Average(EMA) which unlike SMA uses all the data points by assigning weights without dropping them.The recent most point will have more weight and it reduces as the data point gets older.

Cumulative Moving Average(CMA):

In cumulative moving average we calculate the mean of the data stream upto the current data point.This gets updated as new data points enter the stream.

The difference between SMA and CMA is that since CMA is applied to a data stream the average is updated as each new data point enters whereas SMA is applied on static data.

Auto Regressive Integrated Moving Average(ARIMA):

ARIMA is a univariate linear function that is used to predict the future values based on the past data.Since ARIMA relies on its own past data points , a longer series is most likely to get more accurate results.

Before starting ARIMA we must make sure that the data is stationary, which means the mean,variance and other measures of central tendency must remain same over the time.In order to make the data stationary we need to remove the trend,seasonality,cycles,etc.,
The "differencing" method is used to fit the model by subtracting the current value from the previous values including the lag.
Lag is the difference between values of same period.

For example if we have data that has monthly seasonality,we would take each current data point and subtract it from the previous data point of same month from previous year.This is called as Differencing which is used to make data stationary by removing seasonality.

'p' - represents the number of lag observations included in the model (AR)
'd' - represents the number of differences (I)
'q' - is the forecast error coefficient/size of the moving average window (MA)

These together make up ARIMA.Each of these components are explicitly specified in the model as a parameter. A standard notation is used of ARIMA(p,d,q) where the parameters are substituted with integer values to quickly indicate the specific ARIMA model being used.

If we want to select the parameters manually, we can do so by estimating with AutoCorrelation(ACF) and Partial Correlation Functions(PCF)

A value of 0 can be used for a parameter, which indicates to not use that element of the model.

The "statsmodels" library provides the capability to fit an ARIMA model.

			from statsmodels.tsa.arima_model import ARIMA
			model = ARIMA(data, order=(5,1,0))
			model_fit = model.fit(disp=0)
			print(model_fit.summary())

You can find AIC and BIC values which describe the fitness of model to the data.

Anomaly Detection:

It is used to find abnormal behaviour of the data points in a series.The anomaly can be of short term or long term.
For example,the presence of any unusual point in the credit card transaction of a person indicates that the transaction is fraudulent.It can also be used to find the abnormalities in the rate of the heart beats.

One type of supervised machine learning method to detect anomaly is to use Support Vector Machine model.SVM,as most of the supervised algorithms do need training data with data points labelled as abnormal to classify unseen data.SVM's rely on a hyperplane to separate the binary classes.

The labelled data set should contain both the cases of fraud and normal transactions.As mentioned above SVM relies on a hyperplane that divides the data into fraud/not fraud and the SVM model focuses on the data points that are close to the hyperplane(optimize,rather than checking all transactions).


I hope this blog helped you in understanding the basic terminology and some methods used in Time Series analysis.Thank You!

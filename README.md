# Forecasting-Recent-College-Grad-Unemployment-with-SARIMA

In this notebook, I used a Seasonal Auto-Regressive Integrated Moving Average (SARIMA) model to forecast recent college graduate unemployment.

## Data can be found here: https://fred.stlouisfed.org/series/CGBD2024
I utilized the FRED API to retrieve the time series data and employed decomposition to identify a seasonal trend within the data. 


## SARIMA Model/Rolling Forecast Origin Evaluation
The SARIMA model is a continuation of the ARIMA Model. The SARIMA uses two sets of parameters(non-seasonal components as well as seasonal components). The AR(p) part involves using past values to predict the future. The AR term can often be found with cut-offs in the Partial Autocorrelation Function(PACF) plot. The MA part is used to predict future values based on previous shock terms. The Autocorrelation Function(ACF) can help determine the AR term for both q and Q.

<img width="1400" height="650" alt="Image" src="https://github.com/user-attachments/assets/6ab0ecb3-0c09-43ae-a138-10ff823d6cbc" />

The specific model we used was a SARIMA(1,0,1)(0,1,0,12). It uses a non-seasonal autoregressive and moving average component, a seasonal differencing term, as well as a 12-month seasonal component. To test the model's performance, we used a rolling forecast average. Instead of just predicting on the whole test set, we predicted the very next data point, added the true test value to the model, and expanded the model to test until the end of the test set. The mean squared error was 0.98, which is very low, indicating the model performs very well. 
After this, to end the project, I forecasted rates until the end of the year.


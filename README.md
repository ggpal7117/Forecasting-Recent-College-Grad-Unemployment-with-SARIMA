# Forecasting-Recent-College-Grad-Unemployment-with-SARIMA

In this notebook, I used a Seasonal Auto-Regressive Integrated Moving Average (SARIMA) model to forecast recent college graduate unemployment.

## Data can be found here: https://fred.stlouisfed.org/series/CGBD2024
I utilized the FRED API to retrieve the time series data and employed decomposition to identify a seasonal trend within the data. 


## SARIMA Model/Rolling Forecast Origin Evaluation
The SARIMA model is a continuation of the ARIMA Model. The SARIMA uses two sets of parameters(non-seasonal components as well as seasonal components). The AR(p) part involves using past values to predict the future. The AR term can often be found with cut-offs in the Partial Autocorrelation Function(PACF) plot. The MA part is used to predict future values based on previous shock terms. The Autocorrelation Function(ACF) can help determine the AR term for both q and Q.

<img width="1400" height="650" alt="Image" src="https://github.com/user-attachments/assets/6ab0ecb3-0c09-43ae-a138-10ff823d6cbc" />

The specific model we used was a SARIMA(1,0,1)(0,1,0,12): 
$$
\text{model} = \text{SARIMAX}\big(\text{history}, \, \text{order} = (1, 0, 1), \, \text{seasonal\_order} = (0, 1, 0, 12)\big).\text{fit}(\text{disp} = \text{False})
$$


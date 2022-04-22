# Seminar project 

**MARKOV-SWITCHING ARMA MODELS**
The introduction of Markov switching model by Hamilton (1989) is one of the most popular nonlinear time series models in the literature, which appears to properly fit data which changes patterns in different time interval. This model involves multiple structures that can characterize the time series behaviours in different regimes. By allowing switching between regimes, this model is suitable to capture more complex dynamic patterns.

Data is the daily SP500 price for Brazilian stock market, from 3rd June 2002 to 28th November 2017. The return is calculated by the different of log prices. Data is characterized by the autoregressive conditional heteroscedasticity of high frequent data.  


**RESULT INTERPRETATION **

1.

Regime 1 displays with negative mean return with very high variance -> bear state

Regime 2 with positive mean of return and smallest volatility       -> bull state

Regime 3 with zero mean return and average variance.                -> normal state

2. 

Confirming the presence of positive feedback trader when there is negative mutual relationship between variance and autocorrelation coefficients

3.

Markov switching is preferred to Linear Autoregressive model when it comes to heteroskedastic and clustering time series estimation, also General-Switching Model show more improvement comparing to parameter switching models and it is best fitted when consider three-state model (based on AIC) 

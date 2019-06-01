
library(MASS)
setwd("~/Desktop/Seminar paper - Nguyen Phuong Uyen, Le")
#Importing data, the SP500 daily prices of stocks in Brazil marke
price = read.table("SP500.csv", header = TRUE,sep = ";", skipNul = TRUE, fill = TRUE)
#calculating return from SP500 price
return = 100*diff(log(price$SP500))
date = as.Date(price$Date[-1], "%d.%m.%y")
re = data.frame(date,return)

#ploting distribution of return
h = hist(return, breaks = 60, density = 10, main = "Return distribution", axes = TRUE, col = "cadetblue")
xfit<-seq(min(return),max(return)) 
yfit<-dnorm(xfit,mean=mean(return),sd=sd(return)) 
yfit <- yfit*diff(h$mids[1:2])*length(return) 
lines(xfit, yfit, lwd=1)
plot(date, return, type = "b", xlab = "Time", ylab = "Return", col = "blue" )

#plot autocorrelation in return series
acf(re$return, lag.max = 12, type = "correlation", plot = TRUE, na.action = na.fail, demean = TRUE)
#autocorrelation lag dies out quickly, showing a strong autocorreation in lag 1, indicating that return series is stationary.

#ADF test for unit root in time series
install.packages("tseries")
library("tseries")
adf.test(re$return, alternative = "explosive", k = 2 ) 
#since p-value is insignificant, thus we cannot reject the stationary null hypothesis

# AR estimation for return series up to 2 lag
AR= lm(re$return[3: length(re$return)] ~ re$return[3: length(re$return) -1] + re$return[3: length(re$return) -2])
summary(AR)

#Serial correlation test on residual of return
Box.test(resid(AR), lag =12, type = c("Box-Pierce", "Ljung-Box"), fitdf = 1)
# p-value<0.01: strongly reject null hypothesis of no serial correlation
Box.test(resid(AR)^2, lag =12, type = c("Box-Pierce", "Ljung-Box"), fitdf = 1)
#p-value<<0.01: strongly confirm the ARCH effect in residual of return

#MARKOV estimation
install.packages("MSwM")
library("MSwM")
#Objectives: comparing perfornments of four alternative empirical models and AR model

#General-Switching model with 2 regimes
GSM2=msmFit(AR, k = 2, sw = c(T,T,T,T))
#Mean-switching model
MSM=msmFit(AR, k = 2, sw = c(T,F,F,F))
#Autocorrelation-switching model
ASM=msmFit(AR, k = 2, sw = c(F,T,T,F))
#Volatility-switching model
VSM=msmFit(AR, k = 2, sw = c(F,F,F,T))
#General-Switching model with 3 regimes
GSM3=msmFit(AR, k = 3, sw = c(T,T,T,T))
data.frame(AIC(AR), AIC(MSM), AIC(ASM), AIC(VSM), AIC(GSM2), AIC(GSM3))

# As GSM3 have the lowest AIC value, thus it is the best fitted model for time series
summary(GSM3)
# Plotting probability of being in each regime 
plotProb(GSM3, which = 1) 


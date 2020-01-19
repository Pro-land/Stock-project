# Stock-project
A repository for analysing stock data 
import pandas as pd
import numpy as np
from scipy.stats import norm
df = pd.read_excel("D:\Programming\FB-_1_.xlsx")

df['Date'] = pd.to_datetime(df['Date'])

import matplotlib.pyplot as plt

pd.plotting.register_matplotlib_converters()

df['Daily Lag'] = df['Close'].shift(1)

df['Daily Returns'] = (df['Daily Lag']/df['Close']) -1
mean = df['Daily Returns'].mean()
std = df['Daily Returns'].std()
if mean < 0:
    print('mean =', mean, 'it is generally not recommended to buy and sell on the same day')
else:
    print('mean =', mean, 'it is generally recommended to buy and sell on the same day')
print('Std deviation =',std)
kurtosis = df['Daily Returns'].kurtosis()
print('kurtosis:', kurtosis)

print(df['Daily Returns'].hist())

df['Daily Returns'].hist(bins=20)

#pandas hist() method = A histogram is an accurate representation of the distribution of numerical data. It is an estimate of the probability distribution of a continuous variable and was first introduced by Karl Pearson.[1] It differs from a bar graph, in the sense that a bar graph relates two variables, but a histogram relates only one. 

#plt.axvline adds vertical lines in data coordinates.
plt.axvline(mean,color='red',linestyle='dashed',linewidth=2)
#to plot the std line we plot both the positive and negative values
plt.axvline(std,color='g',linestyle='dashed',linewidth=2)
plt.axvline(-std,color='g',linestyle='dashed',linewidth=2)
plt.show()

plt.figure(figsize=(20,8))
plt.plot('Date','Close',data=df)
plt.xlabel('Date')
plt.ylabel('Close Price')
plt.xticks(rotation=45)
plt.grid(True)
plt.legend("Facebook stock")
plt.title("Facebook stock prices in the last 3 months")
plt.show()

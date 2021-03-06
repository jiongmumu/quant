---
description: 数学返回结果，不知道有什么参考价值- -
---

# Statistic Functions

## TSF - Time Series Forecast

[The Time Series Forecast \(TSF\) ](https://library.tradingtechnologies.com/trade/chrt-ti-time-series-forecast.html)is a linear regression calculation that plots each bar's current regression value using the least square fit method. This indicator is sometimes referred to as a moving linear regression similar to a moving average. For example, the TSF value that covers 10 days will have the same value as a 10-day Time Series Forecast. This differs slightly from the Linear Regression indicator in that the Linear Regression indicator does not add the slope to the ending value of the regression line. 

![](../.gitbook/assets/image%20%2810%29.png)

 

```python

def draw_candle_stick_TSF(prices):
    candle = go.Candlestick(x=prices.index,
                           open=prices['open'],
                           high=prices['high'],
                           low=prices['low'],
                           close=prices['close'])

    talib_result = talib.TSF(prices['close'],  timeperiod=5)

    fig = tools.make_subplots(rows=1, cols=1)

    talib_result_line = go.Scatter(x=prices.index,y=talib_result, line = dict(color = ('rgb(255,0,0)')),name='talib_result')
    fig.append_trace(candle, 1, 1)
    fig.append_trace(talib_result_line, 1, 1)

    pyoff.plot(fig) 
```

{% embed url="https://mrjbq7.github.io/ta-lib/func\_groups/statistic\_functions.html" %}

## CORREL - Pearson's Correlation Coefficient \(r\)

```python
#和上面绘图函数几乎相同，除了这里有两个图以外
def draw_candle_stick_CORREL(prices):
    candle = go.Candlestick(x=prices.index,
                           open=prices['open'],
                           high=prices['high'],
                           low=prices['low'],
                           close=prices['close'])

    talib_result = talib.CORREL(prices['high'], prices['low'], timeperiod=5)
    fig = tools.make_subplots(rows=2, cols=1, shared_xaxes=True,subplot_titles=(str(stock),'2CRWOS'))
    
    talib_result_line = go.Scatter(x=prices.index,y=talib_result, line = dict(color = ('rgb(255,0,0)')),name='talib_result')
    fig.append_trace(candle, 1, 1)
    fig.append_trace(talib_result_line, 2, 1)

    pyoff.plot(fig)  # 离线方式绘图
```


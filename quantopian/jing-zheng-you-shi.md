---
description: 从四个指标分析竞争优势
---

# 竞争优势



```python
# First, we need to import Fundamentals in any notebook that uses them
from quantopian.pipeline import Pipeline
from quantopian.research import run_pipeline
from quantopian.pipeline.data import Fundamentals
from quantopian.pipeline.experimental import QTradableStocksUS

# Import the StaticAsset filter since we already know the specific stocks we want data for
from quantopian.pipeline.filters import StaticAssets
```

```python
# We're going to need a date string for some of our queries. Let's grab one.
import datetime

today = datetime.datetime.now().strftime('%Y-%m-%d')
today
```

```text
'2019-01-07'
```

```python
#Fundamentals.net_income_cash_flow_statement?
Pipeline?
```

```python
# Create pipeline filters on the market cap and p/e ratio
big_market_cap = Fundamentals.market_cap.latest > 1e9
big_pe = Fundamentals.pe_ratio.latest > 5 
small_pe = Fundamentals.pe_ratio.latest < 30

# Combine those pipeline filters with the QTradableStocksUS, a liquid trading universe
# https://www.quantopian.com/posts/working-on-our-best-universe-yet-qtradablestocksus
universe = QTradableStocksUS() & big_market_cap & big_pe & small_pe

# Define which stocks you want to get data for
my_stocks = StaticAssets(symbols([
                        'AAPL',
                        'IBM',
                        'AMZN',
                        'NFLX',
                        'GOOG'])
                        )

# Create the pipeline
pipe = pipe = Pipeline(
    columns = {
        'pe_ratio' : Fundamentals.pe_ratio.latest,
        'market_cap' : Fundamentals.market_cap.latest,
        #'net_income_from_continuing_operations' : Fundamentals.net_income_from_continuing_operations.latest,
        'cash_flow_from_continuing_financing_activities' : Fundamentals.cash_flow_from_continuing_financing_activities.latest,
        #'net_income_growth' : Fundamentals.net_income_growth.latest,
        'capital_expenditure' : Fundamentals.capital_expenditure.latest,
        'operating_revenue' : Fundamentals.operating_revenue.latest,
        'revenue_growth' : Fundamentals.revenue_growth.latest,
        'normalized_net_profit_margin' : Fundamentals.normalized_net_profit_margin.latest,
        'roe' : Fundamentals.roe.latest,
        'roa' : Fundamentals.roa.latest,
    },
    screen = my_stocks
)

# Run the pipeline
# P97 find earnings managerment companies.
fundamental_data = run_pipeline(pipe, start_date = today, end_date = today)
```

```python
fundamental_data.sort_values('cash_flow_from_continuing_financing_activities')
```

|  |  | capital\_expenditure | cash\_flow\_from\_continuing\_financing\_activities | market\_cap | normalized\_net\_profit\_margin | operating\_revenue | pe\_ratio | revenue\_growth | roa | roe |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 2019-01-07 00:00:00+00:00 | Equity\(3766 \[IBM\]\) | -9.550000e+08 | -4.370000e+08 | 1.066197e+11 | 0.142530 | 1.875500e+10 | 18.741214 | -0.020780 | 0.022117 | 0.140664 |
| Equity\(23709 \[NFLX\]\) | -3.933300e+07 | 2.923700e+07 | 1.297658e+11 | 0.098868 | 3.999374e+09 | 106.275000 | 0.339887 | 0.017503 | 0.084752 |  |
| Equity\(24 \[AAPL\]\) | -3.041000e+09 | -2.258000e+10 | 7.035527e+11 | 0.224563 | 6.290000e+10 | 12.448363 | 0.196295 | 0.039515 | 0.127197 |  |
| Equity\(46631 \[GOOG\]\) | -5.300000e+09 | -3.478000e+09 | 7.471879e+11 | 0.237351 | 2.895400e+10 | 40.176735 | 0.214893 | 0.042443 | 0.055400 |  |
| Equity\(16841 \[AMZN\]\) | -3.352000e+09 | -2.369000e+09 | 7.703163e+11 | 0.052453 | 5.657600e+10 | 88.207727 | 0.293343 | 0.020756 | 0.077793 |  |

```python
my_stocks = StaticAssets(symbols([
                        'HRB',#布洛克税务公司
                        'KHC',#卡夫亨氏
                        'KO',#可口可乐
                        'DIS',#迪士尼
                        'ADBE',#Adbobe
                        'MTCH',#okcupid等
                        'AMZN',
                        'JD',
                        'NTES',#网易
                        'BABA',#阿里巴巴
                        'INTC',#英特尔
                        'TCEHY',#腾讯控股
                        'AAPL'])
                        )
```



|  |  | capital\_expenditure | market\_cap | normalized\_net\_profit\_margin | operating\_revenue | pe\_ratio | revenue\_growth | roa | roe |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 2019-01-07 00:00:00+00:00 | Equity\(3660 \[HRB\]\) | -5.436500e+07 | 5.232738e+09 | -1.147507 | 1.488710e+08 | 9.224638 | 0.056917 | -0.072866 | -2.194070 |
| Equity\(49229 \[KHC\]\) | -1.560000e+08 | 5.425265e+10 | 0.098777 | 6.378000e+09 | 5.265089 | 0.015605 | 0.005215 | 0.009614 |  |
| Equity\(21669 \[NTES\]\) | NaN | 3.017277e+10 | 0.092885 | NaN | 27.704323 | 0.350824 | 0.020546 | 0.036702 |  |
| Equity\(2190 \[DIS\]\) | -1.201000e+09 | 1.631732e+11 | 0.125344 | 1.430700e+10 | 13.111244 | 0.119571 | 0.023527 | 0.048956 |  |
| Equity\(46979 \[JD\]\) | NaN | 3.177254e+10 | 0.028799 | NaN | 159.446821 | 0.251020 | 0.013886 | 0.049106 |  |
| Equity\(47740 \[BABA\]\) | NaN | 3.594272e+11 | 0.236447 | NaN | 41.744770 | 0.544719 | 0.024710 | 0.049182 |  |
| Equity\(114 \[ADBE\]\) | -6.355800e+07 | 1.104109e+11 | 0.298177 | 2.291076e+09 | 46.733471 | 0.244424 | 0.043607 | 0.075855 |  |
| Equity\(16841 \[AMZN\]\) | -3.352000e+09 | 7.703163e+11 | 0.052453 | 5.657600e+10 | 88.207727 | 0.293343 | 0.020756 | 0.077793 |  |
| Equity\(3951 \[INTC\]\) | -3.851000e+09 | 2.155121e+11 | 0.334013 | 1.916300e+10 | 14.664596 | 0.186637 | 0.050336 | 0.090412 |  |
| Equity\(4283 \[KO\]\) | -3.050000e+08 | 2.024824e+11 | 0.288781 | 8.245000e+09 | 65.164384 | -0.091760 | 0.021307 | 0.102769 |  |
| Equity\(24 \[AAPL\]\) | -3.041000e+09 | 7.035527e+11 | 0.224563 | 6.290000e+10 | 12.448363 | 0.196295 | 0.039515 | 0.127197 |  |
| Equity\(49608 \[MTCH\]\) | -6.495000e+06 | 1.197161e+10 | 0.294040 | 4.439430e+08 | 35.875000 | 0.292719 | 0.057326 | 0.216641 |  |


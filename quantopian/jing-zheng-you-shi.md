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

```


# 行业选股

```python
import os
from jqdatasdk import *

auth(os.environ['JOINT_QUANT_USERNAME'],os.environ['JOINT_QUANT_PWD'])

#行业概念数据
#https://www.joinquant.com/data/dict/plateData
# 获取概念板块成分股
concept_stocks = get_concept_stocks('GN030', date=None)

q = query(indicator.code, indicator.operating_profit,
          indicator.roe, indicator.roa, indicator.net_profit_margin,
          indicator.ocf_to_operating_profit, indicator.inc_total_revenue_year_on_year
            ).filter(indicator.code.in_(concept_stocks))

df = get_fundamentals(q, date='2019-01-07')

#apply 用法
def get_name(code):
    return get_security_info(code).display_name

df['display_name'] = df['code'].apply(get_name)
```

```python
df[df.operating_profit >0].sort_values('roe', ascending=False).head(10)
```

|  | code | operating\_profit | roe | roa | net\_profit\_margin | ocf\_to\_operating\_profit | inc\_total\_revenue\_year\_on\_year | display\_name |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 40 | 300638.XSHE | 3.461682e+07 | 8.92 | 3.80 | 10.89 | 88.64 | 140.92 | 广和通 |
| 37 | 300371.XSHE | 2.563974e+07 | 4.94 | 4.50 | 35.30 | 42.59 | 6.86 | 汇中股份 |
| 44 | 600271.XSHG | 6.575431e+08 | 4.71 | 3.54 | 9.19 | 24.12 | 8.23 | 航天信息 |
| 4 | 002049.XSHE | 5.807765e+07 | 4.52 | 3.04 | 25.68 | -36.43 | 29.71 | 紫光国微 |
| 34 | 300349.XSHE | 1.076189e+08 | 4.26 | 3.27 | 27.71 | 112.29 | 38.39 | 金卡智能 |
| 39 | 300590.XSHE | 2.933722e+07 | 4.20 | 3.61 | 28.90 | 161.68 | 67.19 | 移为通信 |
| 5 | 002139.XSHE | 1.004980e+08 | 4.11 | 2.33 | 8.80 | 119.91 | 30.17 | 拓邦股份 |
| 46 | 600690.XSHG | 1.391408e+09 | 3.78 | 1.21 | 4.13 | 408.28 | 11.50 | 青岛海尔 |
| 9 | 002402.XSHE | 6.594799e+07 | 3.57 | 1.77 | 8.49 | 115.54 | 33.50 | 和而泰 |
| 27 | 300114.XSHE | 5.391186e+07 | 2.83 | 2.32 | 15.48 | 76.59 | 1.05 | 中航电测 |

```python

```


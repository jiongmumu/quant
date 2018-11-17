# 获取各种因子数据的研究

```python
import pandas as pd
import datetime
from jqfactor import get_factor_values
from jqlib.alpha191 import *
from jqlib.technical_analysis import *

now = datetime.datetime.now().strftime("%Y-%m-%d %H:%M:%S")

stocks = get_index_stocks('000009.XSHG')

# previous 5 days factor
start_date = (datetime.datetime.now() - datetime.timedelta(50)).strftime("%Y-%m-%d %H:%M:%S")

# 获取中证100的所有成分股的2015年的天数据, 返回一个[pandas.Panel]
panel =  get_price(security= stocks , 
                   fields=['open', 'close','volume', 'money'], 
                   start_date=start_date,
                   #count = 100,
                   end_date=now, 
                   frequency='1d') #evey day 8 records ?
#df_open = panel['open']  # 获取开盘价的[pandas.DataFrame],  行索引是[datetime.datetime]对象, 列索引是指数代号
#df_volume = panel['volume']  # 获取交易量的[pandas.DataFrame]
#panel['open-close'] =  panel['open'] - panel['close']
#panel['close']
# panel['close'].head(1)['000423.XSHE'][0]
# df_open['000001.XSHE'] # 获取平安银行的2015年每天的开盘价数据
# panel['close'].mean()['000423.XSHE']
# panel['close'].describe()
# panel['close'].min()['000423.XSHE']

yesterday = (datetime.datetime.now() - datetime.timedelta(1)).strftime("%Y-%m-%d")

factor_data = get_factor_values(securities=stocks,
                                factors=['operating_profit_per_share','AR','VOL5','sharpe_ratio_20',
                                         'net_profit_growth_rate','BR','operating_revenue_growth_rate',
                                         'eps_ttm','net_asset_per_share'],
                                start_date=start_date, 
                                end_date=now)

#获取最近一天的因子，返回的是Series
alpha_001 = alpha_002(stocks)

#获取各种技术分析指标，https://www.joinquant.net/data/dict/technicalanalysis
mtm = MTM(stocks, check_date=now, timeperiod = 8)
mfi = MFI(stocks, check_date=now, timeperiod = 21)


#获取换手率,turnover_ratio 等
q_fundamental = query(valuation.turnover_ratio, valuation.market_cap,
                      valuation.pe_ratio,valuation.pb_ratio,
                      indicator.eps).filter(valuation.code.in_(stocks))
panel_fundamental = get_fundamentals_continuously(q_fundamental, end_date=now, count=5)

result = pd.DataFrame()
panel_fundamental_keys = panel_fundamental.mean()['turnover_ratio'].keys()
for stock in stocks:
    if stock not in panel_fundamental_keys:
        continue
    result[stock] = pd.Series(
        { #'ratio':ratio, 
         'latest_price': panel['close'].tail(1)[stock][0],
         #'max_price': panel['close'].max()[stock],
         'min_price': panel['close'].min()[stock],
         'latest_vs_min': panel['close'].tail(1)[stock][0]/panel['close'].min()[stock],
         #'current_ratio':latest_price/panel['close'].min()[stock],
         'volume':panel['volume'].mean()[stock],
         'mtm':mtm[stock],
         'MFI':mfi[stock],
         #'money':panel['money'].mean()[stock],
         'operating_profit_per_share':factor_data['operating_profit_per_share'].mean()[stock],
         'net_asset_per_share':factor_data['net_asset_per_share'].mean()[stock],
         #'sharpe_ratio_20':factor_data['sharpe_ratio_20'].mean()[stock],
         'net_profit_growth_rate':factor_data['net_profit_growth_rate'].mean()[stock],
         'eps_ttm':factor_data['eps_ttm'].mean()[stock],
         #'AR':factor_data['AR'].mean()[stock],
         #'VOL5':factor_data['VOL5'].mean()[stock],
         'operating_revenue_growth_rate':factor_data['operating_revenue_growth_rate'].mean()[stock],
         #'BR':factor_data['BR'].mean()[stock],
         #'alpha_001':alpha_001[stock],
         #'turnover_ratio':panel_fundamental.major_xs('2018-11-12')['turnover_ratio'][stock],
         'turnover_ratio':panel_fundamental.mean()['turnover_ratio'][stock],
         'pe_ratio':panel_fundamental.mean()['pe_ratio'][stock],
         'pb_ratio':panel_fundamental.mean()['pb_ratio'][stock],
         'a_name':get_security_info(stock).display_name
        })


t=result.transpose()
df = t[(t.operating_profit_per_share > 0.15) & (t.volume > 100000)].sort_values('latest_vs_min', ascending=[True])
#df = t[(t.ratio > 0.15) & (t.volume > 100000)].sort_values('current_ratio')
create_download_link(df)
```


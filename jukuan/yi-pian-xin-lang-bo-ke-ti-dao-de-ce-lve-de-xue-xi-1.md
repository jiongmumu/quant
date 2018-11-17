# 成长股内在价值投资

由于我比较感兴趣的是短线，所以这个价值投资我如果每天运行，对我意义不大。

```text
def Value_stock(context):
    current_date = context.current_dt.date()
    time1 = current_date - timedelta(days = 365)
    time2 = current_date - 2*timedelta(days = 365)
    time3 = current_date - 3*timedelta(days = 365)
    ## 获取近几年的EPS，并用近三年的历史增长率代表预期收益增长率
    df = get_fundamentals(query(
        income.code,
        income.day,
        income.operating_revenue,
        income.basic_eps
    ),date = current_date)
    t = list(df['code'])
    df1 = get_fundamentals(query(
        income.basic_eps
    ).filter(
        income.code.in_(t)
    ),date = time1)
    df2 = get_fundamentals(query(
        income.basic_eps
    ).filter(
        income.code.in_(t)
    ),date = time2)
    df3 = get_fundamentals(query(
        income.basic_eps
    ).filter(
        income.code.in_(t)
    ),date = time3)
    dnf = pd.concat([df,df1,df2,df3],axis = 1).dropna()
    tt = list(dnf['code'])
    dnf.columns = ['code','R','Value','basic_eps','basic_eps1','basic_eps2','basic_eps3']
    # 计算预期收益增长率
    dnf['R'] = ((dnf['basic_eps']/dnf['basic_eps1']-1) \
        +(dnf['basic_eps1']/dnf['basic_eps2']-1) \
        +(dnf['basic_eps2']/dnf['basic_eps3']-1))/3
    # 计算成长股内在价值Value
    dnf['Value'] = dnf['basic_eps']*(8.5 + 2*dnf['R'])
    V = dict(zip(dnf['code'],dnf['Value']))
    ## 获取Value/Price 在1到1.2之间的股票
    h = history(1, '1d', 'price', security_list=tt, df=False)
    Buy_stock = {}
    for stock in tt:
        if 1< V[stock]/h[stock][0] <1.2:
            Buy_stock[stock] = V[stock]/h[stock][0]
    log.info(current_date)
    log.info(Buy_stock)
    return Buy_stock
```


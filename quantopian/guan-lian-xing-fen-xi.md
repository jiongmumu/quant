# 关联性分析

```text
# Useful Functions
def find_most_correlated(data):
    n = data.shape[1]
    keys = data.keys()
    pair = []
    max_value = 0
    for i in range(n):
        for j in range(i+1, n):
            S1 = data[keys[i]]
            S2 = data[keys[j]]
            result = np.corrcoef(S1, S2)[0,1]
            if result > max_value:
                pair = (keys[i], keys[j])
                max_value = result
    return pair, max_value

```

```text
symbol_list = ['MOMO', 'NIO', 'FB', 'JD', 'BABA']
data = get_pricing(symbol_list, fields=['price']
                               , start_date='2018-01-01', end_date='2019-04-13')['price']
data.columns = symbol_list

find_most_correlated(data)
data.plot()
```

{% embed url="https://www.quantopian.com/lectures/linear-correlation-analysis" %}




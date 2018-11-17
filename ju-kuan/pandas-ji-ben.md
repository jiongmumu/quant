# pandas基本

## series和dataframe的用法

```text
stocks = get_index_stocks('000009.XSHG')
hist = history(20, security_list = stocks, field='close')
#hist是DataFrame,通过iloc用索引获取series,at获取
hist.iloc[-1].at['000300.XSHG'][0]
```


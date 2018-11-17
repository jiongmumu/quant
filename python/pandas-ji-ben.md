# pandas基本

## [去除重复的列](https://stackoverflow.com/questions/14984119/python-pandas-remove-duplicate-columns)

```python
hist = hist.loc[:,~hist.columns.duplicated()]
```

## 排序

```text
#按照某列值排序
df.sort_values('open', ascending=[False])

#按照列排序,只是按照列名排序
df.sort_index(axis=1)
```

## series和dataframe的用法

```text
stocks = get_index_stocks('000009.XSHG')
hist = history(20, security_list = stocks, field='close')
#hist是DataFrame,通过iloc用索引获取series,at获取
hist.iloc[-1].at['000300.XSHG'][0]
```


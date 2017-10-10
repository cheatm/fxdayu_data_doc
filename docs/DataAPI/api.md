# API

在python中使用DataAPI读取数据。设置好配置文件后，可以在python脚本中导入DataAPI。

```python
from fxdayu_data import DataAPI
```

## candle

- 读取K线数据。

```python
DataAPI.candle(symbols, freq, fields=None, start=None, end=None, length=None, adjust=None)
```

**参数：**

|参数名|必选|类型|说明|
|:----|:---|:----- |-----   |
|symbols|是|String, Iterable|要读取的品种名或返回元素为品种名的可迭代对象(list, tuple)|
|freq|是|String|要读取数据的时间周期|
|fields|否|String, Iterable|要读取的字段:(open, high, low, close, volume)|
|start|否|String, Datetime|开始时间，String类型格式为: "YYYY-mm-dd"或"YYYY-mm-dd HH:MM:SS"|
|end|否|String, Datetime|开始时间，String类型格式为: "YYYY-mm-dd"或"YYYY-mm-dd HH:MM:SS"|
|length|否|int|要读取的时间长度|
|adjust|否|String|数据复权类型，"before"为前复权，"after"为后复权|

## factor

- 读取因子数据

```python
DataAPI.factor(symbols, fields=None, start=None, end=None, length=None)
```

**参数：**

|参数名|必选|类型|说明|
|:----|:---|:----- |-----   |
|symbols|是|String, Iterable|要读取的品种名或返回元素为品种名的可迭代对象(list, tuple)|
|fields|否|String, Iterable|要读取的字段|
|start|否|String, Datetime|开始时间，String类型格式为: "YYYY-mm-dd"或"YYYY-mm-dd HH:MM:SS"|
|end|否|String, Datetime|开始时间，String类型格式为: "YYYY-mm-dd"或"YYYY-mm-dd HH:MM:SS"|
|length|否|int|要读取的时间长度|


## info

读取其他信息

- codes:
读取股票池数据

```python
DataAPI.info.codes(name)
```

|参数名|必选|类型|说明|
|:----|:---|:----- |-----   |
|name|是|String|指定股票分类的名字|
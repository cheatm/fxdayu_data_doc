# 配置文件

DataAPI通过配置文件来连接上层方法与底层数据源。一般地，配置文件是一个满足了以下条件的python脚本：

- 声明了全局变量**candle**，其指向的对象的类继承自
```python
fxdayu_data.data_api.basic.candle.BasicCandle
```

- 声明了全局变量**factor**，其指向的对象的类继承自
```python
fxdayu_data.data_api.basic.factor.BasicFactor
```

- 声明了全局变量**info**，其指向的对象的类继承自
```python
fxdayu_data.data_api.basic.info.BasicInfo
```

## 配置文件模板

为了简化配置文件编写，DataAPI提供了配置文件模板，对于已知的数据源，可以直接导出模板再在模板上做相应修改以匹配数据源。可通过以下命令导出配置文件模板。

```
DataAPI export [OPTIONS] [PATH]
```

>
    PATH: 要导出文件的路径，如果缺省则导出为当前目录的config.py文件。
    OPTIONS:
        -t, --type: 指定导出的配置文件相关的数据源，目前支持以mongo或bundle作为数据源。缺省默认为mongo。
        -n, --name: 将该配置文件以指定的名字添加进DataAPI，缺省则不添加。

目前提供了mongodb模板和bundle模板。


- **mongodb模板**

```python
# encoding:utf-8
from pymongo import MongoClient
from fxdayu_data.data_api import mongo

# client用于与mongodb连接，MongoClient是由mongodb官方提供的python连接mongodb客户端。
client = MongoClient()

# candle指向DataAPI内部实现的从mongodb读取指定数据的对象。
# 其中复权数据来自db: adjust, 小时数据来自db: Stock_H, 日线数据来自db: Stock_D。
candle = mongo.candle(client, "adjust", H="Stock_H", D="Stock_D")

# factor指向DataAPI内部实现的从mongodb读取指定数据的对象，数据来自db: factor。
factor = mongo.factor(client, "factor")

# info指向DataAPI内部实现的从mongodb读取指定数据的对象，数据来自db: info。
info = mongo.info(client, "info")
```

可通过以下命令导出：
```
DataAPI export -t mongo
```

- **bundle模板**

```python
# encoding:utf-8
from fxdayu_data.data_api import bundle
import os

# 获取主目录，主目录为FILE(配置文件路径)所在的目录。
home = os.path.split(FILE)[0]

# candle指向DataAPI内部实现的从bundle读取指定数据的对象。
candle = bundle.candle(
    # 复权数据来自主目录下名为ex_cum_factor.bcolz的bundle数据。
    os.path.join(home, "ex_cum_factor.bcolz"),
    # 日线数据来自主目录下名为Stock_D.bcolz的bundle数据。
    D=os.path.join(home, "Stock_D.bcolz"),
    # 小时数据来自主目录下名为Stock_H1.bcolz的bundle数据。
    H=os.path.join(home, "Stock_H1.bcolz")
)

# factor指向DataAPI内部实现的从bundle读取指定数据的对象，因子数据来自主目录下名为factors.bcolz的bundle数据。
factor = bundle.factor(os.path.join(home, "factors.bcolz"))

# info指向DataAPI内部实现的读取指定数据的对象，数据来自主目录下名为info的数据集。
info = bundle.info(os.path.join(home, "info"))
```

可通过以下命令导出：
```
DataAPI export -t bundle
```





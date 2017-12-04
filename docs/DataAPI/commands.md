# DataAPI 命令行工具

DataAPI命令行工具用于在terminal(cmd)中通过配置文件对数据源进行配置和测试，一下所有命令均需在terminal(cmd)中输入执行。

## add

add命令向DataAPI中添加一个配置文件, 使用方法：

```
DataAPI add [OPTIONS] PATH
```

>
    PATH：要添加的配置文件的绝对路径。
    OPTIONS：
        -n, --name : 配置文件在DataAPI中的名字，如果缺省，则将添加的配置文件设为默认配置。

- **使用案例**

向DataAPI中添加绝对路径为 D:/config.py 的配置文件，并命名为config1。

```
DataAPI add -n config1 D:/config.py
```

## use

use命令将一个已经添加到DataAPI中的配置文件设为默认配置。在python中导入DataAPI时会以默认配置作为配置文件连接数据源。

```
DataAPI use NAME
```

>
    NAME：要使用的配置文件名字(在add时使用[-n, --name] 指定的名字)

- **使用案例**

将上面添加的config1设为默认配置。
```
DataAPI use config1
```

## delete

delete删除一个DataAPI中的配置文件。

```
DataAPI delete NAME
```

>
    NAME：要删除的配置文件名字(在add时使用[-n, --name] 指定的名字)

**注意：** 不要删除名字为main的配置文件。

- **使用案例**
删除刚刚添加的config1文件。
```
DataAPI delete config1
```

## show

显示已添加的目录。

```
DataAPI show
```

## export
export命令用于导出配置文件模板，目前支持导出以mongodb或bundle数据做为数据源的模板。

```
DataAPI export [OPTIONS] [PATH]
```

>
    PATH: 要导出文件的路径，如果缺省则导出为当前目录的config.py文件。
    OPTIONS:
        -t, --type: 指定导出的配置文件相关的数据源，目前支持以mongo或bundle作为数据源。缺省默认为mongo。
        -n, --name: 将该配置文件以指定的名字添加进DataAPI，缺省则不添加。

- **使用案例**

- 在当前目录导出模板，指定名字为bundle加入DataAPI，使用bundle作为数据源。
```
DataAPI export -n bundle -t bundle
```

- 将mongo模板导出到D:/MongoConfig.py, 不添加到DataAPI。
```
DataAPI export -t bundle D:/MongoConfig.py
```


## update
update命令用于更新数据，目前支持从2015年开始的沪深300的日线，分红和因子数据。

```
DataAPI update [TARGET]
```

>
    TARGET: 更新后数据存放的目录。


# requests模块介绍

> requests文档<https://requests.readthedocs.io/projects/cn/zh_CN/latest> 

## 一. requests模块的作用

- 发送http请求，获取响应数据

## 二. requests模块的使用

requests模块是一个第三方模块，需要在你的python(虚拟)环境中额外安装

```shell
pip install requests
```

## 三. requests模块简单的get请求

> 1.  需求：通过requests向百度首页发送请求，获取该页面的源码
> 1.  运行下面的代码，观察打印输出的结果

```python
# coding: utf8
""" 
@File: part_001.py
@Author: Alice(From Chengdu.China)
@HomePage: https://github.com/AliceEngineerPro
@CreatedTime: 2022/10/17 2:25
"""

import os, sys

"""初识requests模块和简单的response对象"""

# 导入requests模块
import requests 

# 目标url
url = 'https://www.baidu.com' 
# 向目标url发送get请求
response = requests.get(url)
# 打印响应内容
print(response.text)
```


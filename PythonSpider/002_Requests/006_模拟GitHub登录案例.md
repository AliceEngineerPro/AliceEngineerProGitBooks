# 案例: 模拟GitHub登录

参考代码:

```python
# coding: utf8
""" 
@File: part_006.py
@Author: Alice(From Chengdu.China)
@HomePage: https://github.com/AliceEngineerPro
@CreatedTime: 2022/10/19 22:44
"""

import os, sys

"""模拟github登录返回个人主页"""

import requests
import re

def get_github_profile() -> None:
    """
    请求github
    :return: 
    """
    # 请求头
    headers = {
        'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/109.0.0.0 Safari/537.36',
    }
    # 实例化session
    session = requests.session()
    # 代理
    proxy = {
        'http': 'http://127.0.0.1:56789',
        'https': 'http://127.0.0.1:56789'
    }
    # 访问登陆页获取登陆请求所需参数
    response = session.get('https://github.com/login', headers=headers, proxies=proxy)
    authenticity_token = re.search('name="authenticity_token" value="(.*?)" />', response.text).group(1)  # 使用正则获取登陆请求所需参数

    # 构造登陆请求参数字典
    data = {
        'commit': 'Sign in',  # 固定值
        'utf8': '✓',  # 固定值
        'authenticity_token': authenticity_token,  # 该参数在登陆页的响应内容中
        'login': input('输入github用户名：'),
        'password': input('输入github账号：')
    }

    # 发送登陆请求（无需关注本次请求的响应）
    session.post('https://github.com/session', headers=headers, data=data, proxies=proxy)

    # 打印需要登陆后才能访问的页面
    response = session.get(f'https://github.com/{data.get("login")}', headers=headers, proxies=proxy)
    print(response.text)
    
if __name__ == '__main__':
    get_github_profile()
```


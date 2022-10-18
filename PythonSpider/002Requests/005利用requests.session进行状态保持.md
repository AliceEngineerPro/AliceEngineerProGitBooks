# 利用requests.session进行状态保持

>   requests模块中的Session类能够自动处理发送请求获取响应过程中产生的cookie,进而达到状态保持的目的。

## 一. requests.session的作用以及应用场景

-   requests.session的作用

    自动处理cookie,即下一次请求会带上前一次的cookie

-   requests.session的应用场景

    自动处理连续的多次请求过程中产生的cookie

## 二. requests.session使用方法

>   session实例在请求了一个网站后,对方服务器设置在本地的cookie会保存在session中,下一次再使用session请求对方服务器的时候,会带上前一次的cookie

-   session对象发送get或post请求的参数,与requests模块发送请求的参数完全一致


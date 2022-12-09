# selenium的其它使用方法

## 一. selenium标签页的切换

> 当selenium控制浏览器打开多个标签页时，控制浏览器在不同的标签页中进行切换
>
> 需要以下两步：
>
> 1. 获取所有标签页的窗口`句柄`[^1]
> 2. 利用窗口句柄字切换到句柄指向的标签页

参考代码示例:

```python
import time
from selenium import webdriver

driver = webdriver.Chrome()
driver.get("https://www.baidu.com/")

time.sleep(1)
driver.find_element_by_id('kw').send_keys('python')
time.sleep(1)
driver.find_element_by_id('su').click()
time.sleep(1)

# 通过执行js来新开一个标签页
js = 'window.open("https://www.sogou.com");'
driver.execute_script(js)
time.sleep(1)

# 1. 获取当前所有的窗口
windows = driver.window_handles

time.sleep(2)
# 2. 根据窗口索引进行切换
driver.switch_to.window(windows[0])
time.sleep(2)
driver.switch_to.window(windows[1])

time.sleep(6)
driver.quit()
```

[^1]: 指向标签页对象的标识

## 二. switch_to切换frame标签

> iframe是html中常用的一种技术，即一个页面中嵌套了另一个网页，selenium默认是访问不了frame中的内容的，对应的解决思路是`driver.switch_to.frame(frame_element)`。接下来我们通过qq邮箱模拟登陆来学习这个知识点
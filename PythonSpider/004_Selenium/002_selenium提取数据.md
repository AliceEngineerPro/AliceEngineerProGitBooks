# selenium提取数据

## 一. driver对象的常用属性和方法

> 在使用selenium过程中，实例化driver对象后，driver对象有一些常用的属性和方法

1. `driver.page_source` 当前标签页浏览器渲染之后的网页源代码
2. `driver.current_url` 当前标签页的url
3. `driver.close()` 关闭当前标签页，如果只有一个标签页则关闭整个浏览器
4. `driver.quit()` 关闭浏览器
5. `driver.forward()` 页面前进
6. `driver.back()` 页面后退
7. `driver.save_screenshot(img_name)` 页面截图

示例代码:

```python
# coding: utf8
""" 
@File: part_004.py
@Author: Alice(From Chengdu.China)
@HomePage: https://github.com/AliceEngineerPro
@CreatedTime: 2022/12/9 6:33
"""

from selenium import webdriver
from selenium.webdriver.common.by import By
import time

url = 'https://baidu.com/'
driver_path = r'./driver/firefox_107_0_1_x86_64/win/geckodriver.exe'
webdriver.FirefoxOptions().binary_location = r'C:\Program Files\Mozilla Firefox\firefox.exe'
driver = webdriver.Firefox(executable_path=driver_path)
driver.get(url=url)
print(driver.page_source)
driver.find_element(by=By.ID, value='kw').send_keys('python')
driver.find_element(by=By.ID, value='su').click()
time.sleep(3)
driver.save_screenshot(filename='./python_百度搜索.png')
print(driver.current_url)
driver.get(url='https://douban.com/')
driver.save_screenshot(filename='./豆瓣主页.png')
driver.back()
driver.forward()
time.sleep(3)
driver.quit()

```

## 二. driver对象定位标签元素获取标签对象的方法

> 在selenium中可以通过多种方式来定位标签，返回标签元素对象

1. 导入`By`模块

   ```python
   from selenium.webdriver.common.by import By
   ```

2. 调用`find_element`/`find_elements`方法

   - 参数`by`: 
     1. `By.ID`: 返回一个元素
     2. `By.XPATH`: 返回一个包含元素的列表
     3. `By.LINK_TEXT`: 根据连接文本获取元素列表
     4. `By.PARTIAL_LINK_TEXT`: 根据链接包含的文本获取元素列表
     5. `By.NAME`: 根据标签的name属性值返回包含标签对象元素的列表
     6. `By.TAG_NAME`: 根据标签名获取元素列表
     7. `By.CLASS_NAME`: 根据类名获取元素列表
     8. `By.CSS_SELECTOR`: 根据css选择器来获取元素列表
   - 参数`value`: 对应值

`find_element`和`find_elements`的区别：

1. 如果匹配有多个结果, `find_element`返回匹配到的第一个标签对象, `find_elements`返回列表
2. 如果匹配没有结果, `find_element`抛出异常, `find_elements`返回空列表

`By.LINK_TEXT`和`By.PARTIAL_LINK_TEXT`的区别: `LINK_TEXT`返回全部文本, `PARTIAL_LINK_TEXT`返回包含某个文本

## 三. 标签对象提取文本内容和属性值

> find_element仅仅能够获取元素，不能够直接获取其中的数据，如果需要获取数据需要使用以下方法

对定位到的标签对象进行点击操作: `.click()`

对定位到的标签对象输入数据: `.send_keys(data)`

通过定位获取的标签对象的`text`属性，获取文本内容: `.text`

通过定位获取的标签对象的`get_attribute`函数，传入属性名，来获取属性的值: `.get_attribute("属性名")`

示例代码:

```python
# coding: utf8
""" 
@File: part_005.py
@Author: Alice(From Chengdu.China)
@HomePage: https://github.com/AliceEngineerPro
@CreatedTime: 2022/12/9 7:08
"""

from selenium import webdriver
from selenium.webdriver.common.by import By
import time

url = 'https://movie.douban.com/explore'
driver_path = r'./driver/firefox_107_0_1_x86_64/win/geckodriver.exe'
webdriver.FirefoxOptions().binary_location = r'C:\Program Files\Mozilla Firefox\firefox.exe'
driver = webdriver.Firefox(executable_path=driver_path)
driver.get(url=url)
time.sleep(3)
ul = driver.find_elements(by=By.CLASS_NAME, value='explore-list')
for data in ul:
    for i in data.find_elements(by=By.TAG_NAME, value='a'):
        print(i.get_attribute('href'))
    for i in data.find_elements(by=By.CLASS_NAME, value='drc-subject-info-title-text'):
        print(i.text)
driver.quit()
```


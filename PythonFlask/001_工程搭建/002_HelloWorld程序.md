# Flask的HelloWorld程序

## 一. Flask程序编写

- 创建helloworld.py文件

```python
# 导入Flask类
from flask import Flask

#Flask类接收一个参数__name__
app = Flask(__name__)

# 装饰器的作用是将路由映射到视图函数index
@app.route('/')
def index():
    return 'Hello World'

# Flask应用程序实例的run方法启动WEB服务器
if __name__ == '__main__':
    app.run()
```

## 二. 启动运行

```shell
python helloworld.py
```
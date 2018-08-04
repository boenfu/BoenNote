创建一个Python项目 就一定要给他创建一个虚拟环境

（就像 npm 项目 都需要一个package.json）

pip install pipenv

pipenv install / uninstall

pipenv shell

虚拟环境中 就用 pipenv 安装了 （就像npm）

exit 退出虚拟环境

常用指令

pipenv graph 看版本依赖关系

 pipenv --venv 安装目录



```python
from flask import Flask

app = Flask(__name__)

@app.route('/hello')
def hello():
    return 'Hello Boen'

if __name__ == '__main__':
    app.run()

// 最简单的一个应用
// @app.route('/hello') hello后面不带 / 的话
// 用户地址栏输入 /hello/ 是无法访问的
// 如果 @app.route('/hello/') 就可以兼容带斜杠和不带斜杠
// 但其实 在这个条件下 用户输入 /hello 是做的重定向 重定向到 /hello/ 
// flask 这样做 是符合单一url原则

// app.run(debug=True) 开启调试模式 能热更新
// 除了使用装饰器注册路由 还可以用
// app.add_url_rule('/hello', view_func=hello)
// app.run() 里面还能添加 host 指定ip,port 指定端口

// 要导入配置文件 用 app.config.from_object('配置文件名') 如 app.config
// 然后通过 app.config['参数名'] 就能访问配置了
// 配置参数都用大写 另外DEBUG参数在flask里默认有 是false

// if __name__ == '__main__':
//  的意思是作为入口文件的时候再执行后面的   
```



注解中的url 里 需要参数的话可以用<>

如 ‘/hello/\<a\>’  a就会作为参数传进注解绑定的函数

如果是用问号传递参数的话

需要 从flask导入 request

然后在路由方法里用 request.args['a']取

request.args.to_dict() 变成字典



requests 库

r = requests.get(url)

r.json 将请求返回的内容转为json

r.status_code 请求的状态码



路由方法返回的结果用元祖放三个参数

内容, 状态码, 响应头

内容要用 json.dumps变成序列

flask提供了简便的一个方法

jsonify(内容) 就可以达到上面效果





像java写后台一样

controller 放一个里面不太好 最好按功能分文件放

在flask 里 叫蓝图 通常只创建一个app 然后为他添加多个蓝图 每个蓝图都有一系列接口

但是 flask 里的蓝图 范围更大一点

通常比如 为web提供的可以放在一个蓝图

专门提供api的可以建一个api蓝图

管理内容资源的 cms 建一个蓝图

而在一个蓝图下再根据功能分模块放



注册一个蓝图

```python
from flask import Blueprint
# 创建蓝图
xxx = Blueprint('web', __name__)
# 第一个参数是蓝图名称
# 第二个参数是蓝图的模块 __name__指的当前的

# app 里注册蓝图
# app.register_blueprint(web)
```



一个比较好的做法就是

app 或 蓝图的初始化 都放在文件夹下的 init py里





表单验证

pipenv install wtforms

![](file:///D:\BoenMD\Python\Flask\f1.png)

![](file:///D:\BoenMD\Python\Flask\f2.png)

想拿到错误的原因 在form.errors

自定义提示 就在 validators 里加一个 message

想去掉空格的干扰 加一个 DataRequired()



想从其他地方拿到app实例 可以用

from flask import current_app





从模型生成数据库表

sqlalchemy

flask改进了它 弄了个 Flask_SQLAlchemy

pipenv install flask-sqlalchemy

![](file:///D:\BoenMD\Python\Flask\f3.png)



要和 flask 关联起来 

![](file:///D:\BoenMD\Python\Flask\f4.png)

然后在app的init文件里 导入 这里的db

调用

db.init_app(app) 初始化

然后 调用 db.create_all() 来创建





连接数据库

在flask配置文件里 

添加 SQlALCHEMY_DATABASE_URI = 'mysql+cymysql://root:123456@localhost:3366/fisher'

 'mysql+cymysql' 分别是 数据库名 和 数据库驱动
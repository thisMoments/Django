### Django基础知识

- Django的模式简称MVT(model view template)模式，本质上和MVC(model view control)没什么区别。
  
      Model（模型）表示应用程序核心（比如数据库记录列表）
      View（视图）显示数据（数据库记录）
      Controller（控制器）处理输入（写入数据库记录）
      Template(模板) 把页面展示给用户
      

![mvt简单图解](https://img-blog.csdn.net/2018050310585556?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzQxNzY3OTMw/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

- 安装虚拟环境(命令提示符)  pip install virtualenv

      安装env环境  virtualenv --no-site-packages testenv
      进入虚拟环境  source bin/activate
      pip freeze
      pip install mymysql
      退出虚拟环境  deactivate

- 安装Django  pip install django==1.11

- 创建一个Django项目 django-admin startproject helloworld

- 启动Django项目 python manage.py runserver ip:端口号(如果不填写，默认端口号为8000)
  
  （这时候在浏览器新建窗口，输入服务器ip地址及端口号，页面显示it worked即表示启动项目成功）
  
- 创建app python manage.py startapp appname
  
      admin.py - 管理后台注册模型
      settings.py 配置信息位置，注册qpp的时候需要用到，一般不推荐这样使用
      apps.py - 模块
        from app.apps import AppConfig
        AppConfig.name
      models.py - 写模型的地方，与数据库操作相关，存入或读取数据时用到这个
      views.py - 写处理业务逻辑的地方
      urls.py - 网址入口，关联到对应的views.py中的一个函数（或者generic类），访问网址就对应一个函数
        Django url() 可以接收四个参数，分别是两个必选参数：regex、view 和两个可选参数：kwargs、name
          regex: 正则表达式，与之匹配的 URL 会执行对应的第二个参数 view
          view: 用于执行与正则表达式匹配的 URL 请求
          kwargs: 视图使用的字典类型的参数
          name: 用来反向获取 URL

- 迁移数据库 

      python manage.py makemigrations
      python manage.py migrate
     
- 保持数据 xxx.save()
     

- 创建超级用户 python manage.py createsuperuser

      admin(用户)
      xxx@xx.com(邮箱，可以随意填写)
      admin1234(密码)

      python manage.py makemigrations(重启项目)
      
- ORM对象关系映射,翻译机（objects relational mapping）

#### models模型字段

      CharField(): 字符串
      BooleanField： 布尔类型
      DateField: 年月日/日期
          auto_now_add: 第一次创建这条数据的时候赋值
          auto_now: 每次修改的时候赋值
      DateTimeField: 年月日/时分秒
          auto_now_add / auto_now
          
- AutoField: 自动增长

- DecimalField(): 长度

      max_length总长度（位数），decimal_places小数点后长度（位数）
      
- TextField: 存文本信息

      IntegerField: 整数
      FloatField: 浮点数
  
- FileField: 文件上传字段

      ImageField(): 上传图片
      upload_to="" 指定上传图片的路径
    
#### 模型参数

- default: 默认

      null: 设置是否为空，针对数据库中该字段是否可以为空
      blank: 设置是否为空，针对表单提交该字段是否可以为空
      primary key: 主键
      unique: 唯一
  
#### 过滤
  
- 修改字段名 alter tale table_name change

- objects对象 通过模型.objects来实现数据的CRUD操作

      相当于SQL中的select
      获取所有 select * from xxxx
      模型.bojects.all()
  
- 获取信息 filter(过滤条件) get(过滤条件)

      区别：get返回一个满足条件的对象，没有满足条件的则直接报DoesNotExit的异常，
            如果查询结果有多个数据的话，就报MulitiObjectsReturned
        filter() 返回满足条件的结果
        first() 返回第一条数据
        last() 返回最后一条数据
        count() 求和
        gt / gte: 大于 / 大于等于
        lt / lte: 小于 / 小于等于
        
- F() / Q() 
  from django.db.models import F, Q
  
#### 关联

- 1:1 OneToOneField  主键和外键是一对一的关系，在关联表中，只能关联一个主表的id

      拓展表找主表： 拓展信息对象.关联字段
      主表找拓展表的信息： 主表对象.关联表的model_name
  
  1:N
  
  M:N
  
- on_delete

      默认cascade，主表删除，从表也删除
      set_null, 主表删除，从表关联字段设为空
      protect， 不让删除
      set_default, 主表删除，从表关联字段设置为默认值
      
- 静态资源记载（两种方法）

      1, static/images/xxx.png
      2, {% load static %}
      
         {% static 'images/xxx.png' %}
         
 - for
 
       {% for i in stu %}
       {% empty %}
       {% endfor %}
       
 - if
      
       {% if xxx %}
       {% endif %}
       
- ifequal

      {% ifequal xxx 1 %}
      {% else %}
      {% endifequal %}
      
- forloop

      forloop.counter
      计数从0开始：{{ forloop.counter0 }} 
      计数从1开始：{{ forloop.counter }}
      计数从最后开始，到1停：{{ forloop.revcounter }} 
      计数从最后开始，到0停：{{ forloop.revcounter0 }} 
      
- 过滤器 （|） 在变量显示前修改

      date 年: y 两年 Y 四年
           月: m
           日: d
           时: h 12小时制 H 24小时制
           分: m
           秒: s
           
- 注释 {# #}
 
       {% comment %}
       {% endcomment %}
       
- 大小写 uper lower

- {% url'namespace:name' value %}

      工程中url定义namespace
      模块appurl中定义name
      
- 请求

      post 提交数据隐藏了
      get  提交数据在url上
      put  更新全部数据
      patch 更新局部数据
      delete 删除
      
- form

      <input type='text'>
      <input type='date'>
      <input type='files'>

#### Request 对象

- 每个 view 函数的第一个参数是一个 HttpRequest 对象

  HttpRequest对象包含当前请求URL的一些信息：
  
      path 请求页面的全路径,不包括域名
      method 请求中使用的HTTP方法的字符串表示，全大写表示
      GET 包含所有HTTP GET参数的类字典对象
      POST 包含所有HTTP POST参数的类字典对象
      REQUEST POST和GET属性的集合体，但是有特殊性，先查找POST属性，然后再查找GET属性
      COOKIES 包含所有cookies的标准Python字典对象，Keys和values都是字符串
      FILES  包含所有上传文件的类字典对象。FILES中的每个Key都是<input type="file" name="" />标签中name属性的值. FILES中的每个value 同时也是一个标准Python字典对象，包含下面三个Keys:
          filename: 上传文件名,用Python字符串表示
          content-type: 上传文件的Content type
          content: 上传文件的原始内容
      META 包含所有可用HTTP头部信息的字典
      user 是一个django.contrib.auth.models.User 对象，代表当前登录的用户

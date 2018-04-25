### Django基础知识

- Django的模式简称MVT(model view template)模式，本质上和MVC(model view control)没什么区别。
  
      Model（模型）表示应用程序核心（比如数据库记录列表）
      View（视图）显示数据（数据库记录）
      Controller（控制器）处理输入（写入数据库记录）

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
  
      admin.py - 管理后台祖册模型
      settings.py 配置信息位置，注册qpp的时候需要用到，一般不推荐这样使用
      apps.py - 模块
        from app.apps import AppConfig
        AppConfig.name
      models.py - 写模型的地方
      views.py - 写处理业务逻辑的地方

- 迁移数据库 

      python manage.py makemigrations
      python manage.py migrate
     
- 保持数据 xxx.save()
     

- 创建超级用户 python manage.py createsuperuser

      admin(用户)
      xxx@xx.com(邮箱)
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

- 获取所有 select * from xxxx

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


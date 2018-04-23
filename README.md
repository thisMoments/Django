# Django
- Django的模式简称MVT(model view template)模式，本质上和MVC(model view control)没什么区别。
    
    Model（模型）表示应用程序核心（比如数据库记录列表）。
    
    View（视图）显示数据（数据库记录）。
    
    Controller（控制器）处理输入（写入数据库记录）。

- 安装虚拟环境(命令提示符)  pip install virtualenv

- 安装env环境  virtualenv --no-site-packages testenv

- 进入虚拟环境  source bin/activate

     pip freeze
     
     pip install mymysql
     
  退出虚拟环境  deactivate

- 安装Django  pip install django==1.11

- 创建一个Django项目 django-admin startproject helloworld

- 启动Django项目 python manage.py runserver ip:端口号
  
  （这时候在浏览器新建窗口，打开服务器地址，页面显示it worked即表示启动项目成功）
  
- 创建app python manage.py startapp appname
  
  admin.py - 管理后台祖册模型
  
  apps.py - settings.py里面注册qpp的时候需要用到，一般不推荐这样使用
  
    from app.apps import AppConfig
    
    AppConfig.name
    
  models.py - 写模型的地方
  
  views.py - 写处理业务逻辑的地方

- 迁移数据库 python manage.py makemigrations

     python manage.py migrate

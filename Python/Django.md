
* 官方文档：[Online-1.11](https://docs.djangoproject.com/en/1.11/) | [Offline-1.11](E:\Baidu Netdisk\Ebook&Document\Python\django-docs-1.11-en\index.html)

* 网络文档：

* 视频教程：

* 纸质书：

* 电子书：

* 源码学习：Django

* 项目开发：OPMS,ElephantIsland




Django是python的web开发框架，遵循MVC的设计模式，但在Django中通常称为MTV(model-template-views)。MVC(model-view-controller)

model是数据持久层，主要存放实体映射、实体关系以及实体的一些方法。

template是表示层，主要是用来显示数据，Django的视图引擎可以将其渲染成HTML并显示。

views是业务逻辑层，在Django中充当着链接model与template的桥梁，处理模型并向template提交数据，同时也接受template的请求和参数，完成相应的逻辑后提交模型修改。代码逻辑处理的主要地点，项目中大部分代码均在这里编写。

[TOC]

### Setting up Your Environment

#### 安装Django

#### 查看Django版本
> $ python -m django --version

#### Creating a project

From the command line, cd into a directory where you’d like to store your code, then run the following command:

```shell

$ django-admin startproject mysite

$ tree mysite
mysite/
├── mysite
│   ├── __init__.py
│   ├── settings.py
│   ├── urls.py
│   └── wsgi.py
└── manage.py

```
These files are:

* 外部mysite/目录只是你项目的一个容器，目录的名字与Django无关，你可以修改为任何你喜欢的名字。

* manage.py: 一个让你用各种方式与Django项目进行交互的命令行工具。你可以了解更多细节通过[django-admin and manage.py]()。

* 内部mysite/目录是你的项目的实际Python包。它的名字是你需要导入其中任何内容的Python包名称。 (e.g. mysite.urls)

* mysite/__init__.py: 告诉Python将这个目录当作一个Python包的空文件，如果你是一个Python初学者可以阅读Python的官方文档关于[more about packages]()。

* mysite/settings.py: 此Django项目的配置文件. [Django settings]()会告诉你所有有关配置的工作原理。

* mysite/urls.py: 该Django项目的URL声明; 您的Django网站活动的“目录”。你可以阅读更多有关URLs的内容在[URL dispatcher]()。

* mysite/wsgi.py: 为你的项目提供服务的WSGI兼容的Web服务器的入门点。有关详细信息，请参阅[How to deploy with WSGI]()。


**注意**
Project names only have numbers, letters and underscores.如'-'是不允许的

```
#django-admin startproject Franky-Blog
CommandError: 'Franky-Blog' is not a valid project name. Please make sure the name is a valid identifier.
#

```

#### The development server
> $ python manage.py runserver

通过浏览器访问http://127.0.0.1:8000/

改变服务端口
> $ python manage.py runserver 8080

更改服务器IP，将其与端口一起传递。如，要监听所有可用的公共IP（如果您正在运行Vagrant或想要在网络上的其他计算机上炫耀您的工作），可以使用：
> $ python manage.py runserver 0:8000

0是0.0.0.0的简写

开发服务器根据需要自动重新加载每个请求的Python代码。修改代码不需要重新启动服务器以使代码更改生效。 但是，一些操作（如添加文件）不会触发重新启动，因此在这些情况下必须重新启动服务器。

**注意**

不要在任何类似于生产环境的任何地方使用这个服务器。它只适用于开发(我们正在制作Web框架，而不是Web服务器)。


#### 项目和应用程序有什么区别？ 
一个应用程序是一个可以执行某些操作Web应用程序，例如Weblog系统。一个项目是特定网站配置和应用程序的集合。项目可以包含多个应用程序。一个应用程序可以在多个项目中。

#### Creating a app

确保在manage.py的同级目录下输入：python manage.py startapp app_name

```shell
$ python manage.py startapp polls
```

```python
polls/
    __init__.py
    admin.py
    apps.py
    migrations/
        __init__.py
    models.py
    tests.py
    views.py
```

#### view

The url() function is passed four arguments, two required: regex and view, and two optional: kwargs, and name. 

#### Configuring the Database

If you’re using MySQL, you’ll need a DB API driver like mysqlclient. 

> pip install mysqlclient

```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'djangotest',
        'USER': 'root',
        'PASSWORD': 'aaron123',
        'HOST': 'localhost',
        'PORT': '3306',
        'TIME_ZONE': 'Asia/Shanghai',
    }
}
```
```python
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'blog',
    'blog2',
    'contacts',
    'news',
    'polls',
]
```

#### Creating a Model

#### The development server

If you want to change the server’s IP, pass it along with the port. For example, to listen on all available public IPs (which is useful if you are running Vagrant or want to show off your work on other computers on the network), use:

> $ python3 manage.py runserver 0:8000

0 is a shortcut for 0.0.0.0. 

Now that the server’s running, visit http://XXX.XXX.XXX.XXX:8000/ with your Web browser. You’ll see a “Welcome to Django” page, in pleasant, light-blue pastel. It worked!

**注意**

首先会报如下错误：

```
DisallowedHost at /
Invalid HTTP_HOST header: 'XXX.XXX.XXX.XXX:8000'. You may need to add u'XXX.XXX.XXX.XXX' to ALLOWED_HOSTS.
```

In your settings.py, there is a list called ALLOWED_HOSTS. You need to add the IP address you see in the error to that list:

ALLOWED_HOSTS = ['XX.XX.XX.XX']


#### Design your model

Django的理念是，你的网站应由员工或客户端编辑，也可能只是你自己编辑，而不需要创建后端接口来管理内容。

创建Django应用程序的一个典型工作流程是创建模型并尽可能快地让管理站点运行起来，因此你的员工（或客户端）可以开始填充数据。 然后，开发数据呈现给公众的方式。

#### App管理

在Django中需要创建多个app，这时可以把所有的app放到同个文件夹，比较清楚，看起来也比较规范。这就需要创建一个文件夹（文件名不建议取apps），将应用放入这个目录中，会自动生成__init__.py文件(包目录)。

此时，编辑器的语法不能再检测到在应用中import到的包，如果用的是pycharm，则可以将这个目录使用右键->mark directory as->sources root 这样编辑器便会识别，不再报错。

这个时候基本可以在pycharm中正常使用，但是如果部署在实际环境中就不能正常运行，需要在setting.py文件中加入

```
import sys
sys.path.insert(0,os.path.join(BASE_DIR,'文件夹名')) 
# 设置默认搜索路径（0表示优先级，会优先检索这个目录）

```

#### Exception

```
django.db.migrations.exceptions.InconsistentMigrationHistory: Migration admin.0001_initial is applied before its dependency users.0001_initial on database 'default'.
```
I take it you ran './manage.py migrate' first, and then created your custom user model? Unfortunately this isn't supported - creating a custom user model has to be the very first thing you do on a project, before the rest of the database tables are built. (This is a Django limitation - see the warning at https://docs.djangoproject.com/en/1.10/topics/auth/customizing/#substituting-a-custom-user-model .) 

If starting from a fresh database is an option, then deleting/recreating the database and re-running './manage.py migrate' should work. 



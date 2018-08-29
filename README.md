# django-blog

环境：cmd(windows NT)  
工具：Python (V 3.6.4)  

## 工作目录  
```cmd
C:\Users\Herrera>mkdir djangoopt
C:\Users\Herrera>cd djangoopt
C:\Users\Herrera\djangoopt>dir #查看文件夹内容
```

## Install  

### 安装 python3 ，pip  
官网下载软件包：python-3.6.4-amd64.exe  
双击安装：期间会有勾选PIP 安装的选项，顺带安装pip工具  
```cmd
C:\Users\Herrera>python -V
Python 3.6.4

C:\Users\Herrera>pip -V
pip 9.0.1 from c:\users\herrera\appdata\local\programs\python\python36\lib\site-packages (python 3.6)

```
### 安装 Django  
我们用 `django==1.10.6 `来安装指定的 `Django` 版本以保证和教程中的一致。  
```cmd
C:\WINDOWS\system32>pip install django==1.10.6
You are using pip version 9.0.1, however version 9.0.2 is available.
You should consider upgrading via the 'python -m pip install --upgrade pip' command.

C:\Users\Herrera>pip install django==1.10.6
Collecting django==1.10.6
  Downloading Django-1.10.6-py2.py3-none-any.whl (6.8MB)
    100% |████████████████████████████████| 6.8MB 121kB/s
Installing collected packages: django
Successfully installed django-1.10.6
You are using pip version 9.0.1, however version 9.0.2 is available.
You should consider upgrading via the 'python -m pip install --upgrade pip' command.
```
如果直接 `pip install django` 的话有可能安装最新的 `Django` 发行版本，而不是 `Django 1.10.6`。  

测试：  

```python
C:\Users\Herrera>python
Python 3.6.4 (v3.6.4:d48eceb, Dec 19 2017, 06:54:40) [MSC v.1900 64 bit (AMD64)] on win32
Type "help", "copyright", "credits" or "license" for more information.
>>> import django
>>> print(django.get_version())
1.10.6
```

查看pip安装记录：  
```cmd
C:\Users\Herrera>pip list
DEPRECATION: The default format will switch to columns in the future. You can use --format=(legacy|columns) (or define a format=(legacy|columns) in your pip.conf under the [list] section) to disable this warning.
Django (1.10.6)
pip (9.0.1)
setuptools (28.8.0)
wheel (0.30.0)
You are using pip version 9.0.1, however version 9.0.2 is available.
You should consider upgrading via the 'python -m pip install --upgrade pip' command.
```

## 创建`Django`工程  

在我们的工作目录 djangoopt 下创建:   
```cmd
C:\Users\Herrera\djangoopt>django-admin startproject djblog
C:\Users\Herrera\djangoopt>tree . /F
文件夹 PATH 列表
卷序列号为 B035-7893
C:\USERS\HERRERA\DJANGOOPT
│  build.django.blog.md
│
└─djblog
    │  manage.py
    │
    └─djblog
            settings.py
            urls.py
            wsgi.py
            __init__.py
```
这就是我们的博客后台文件：  
最顶层的 djblog\ 目录是我们刚刚指定的工程目录。djblog\ 目录下面有一个 manage.py 文件，manage 是管理的意思，顾名思义 manage.py 就是 Django 为我们生成的管理这个项目的 Python 脚本文件，以后用到时会再次介绍。与 manage.py 同级的还有一个 djblog\ 的目录，这里面存放了一些 Django 的配置文件，例如 settings.py、urls.py 等等，以后用到时会详细介绍。
  
manage.py  
``` python3
#!/usr/bin/env python
import os
import sys

if __name__ == "__main__":
    os.environ.setdefault("DJANGO_SETTINGS_MODULE", "djblog.settings")
    try:
        from django.core.management import execute_from_command_line
    except ImportError:
        # The above import may fail for some other reason. Ensure that the
        # issue is really that Django is missing to avoid masking other
        # exceptions on Python 2.
        try:
            import django
        except ImportError:
            raise ImportError(
                "Couldn't import Django. Are you sure it's installed and "
                "available on your PYTHONPATH environment variable? Did you "
                "forget to activate a virtual environment?"
            )
        raise
    execute_from_command_line(sys.argv)
```

## 开启服务  

```
C:\Users\Herrera\djangoopt\djblog>python manage.py runserver
Performing system checks...

System check identified no issues (0 silenced).

You have 13 unapplied migration(s). Your project may not work properly until you apply the migrations for app(s): admin, auth, contenttypes, sessions.
Run 'python manage.py migrate' to apply them.
March 17, 2018 - 14:22:42
Django version 1.10.6, using settings 'djblog.settings'
Starting development server at http://127.0.0.1:8000/
Quit the server with CTRL-BREAK.
[17/Mar/2018 14:23:25] "GET / HTTP/1.1" 200 1767
[17/Mar/2018 14:25:03] "GET / HTTP/1.1" 200 1767
```
说明服务已开启  
登陆`http://127.0.0.1:8000/` 查看：  
![ceshi]({filename}/hello.png)

命令栏工具下按 Ctrl + c 可以退出开发服务器（按一次没用的话连续多按几次）。重新开启则再次运行 python manage.py runserver 。  

---  
## 一些配置  
C:\Users\Herrera\djangoopt\djblog\djblog\setting.py  
```python
# 把英文改为中文
#LANGUAGE_CODE = 'en-us'
LANGUAGE_CODE = 'zh-hans'

# 把国际时区改为中国时区
#TIME_ZONE = 'UTC'
TIME_ZONE = 'Asia/Shanghai'
```
再次开启服务：  
![ceshi1]({filename}/hello1.png)  


## 创建 blog app  

``` cmd
C:\Users\Herrera\djangoopt\djblog>python manage.py startapp blog

C:\Users\Herrera\djangoopt\djblog>tree /F blog
文件夹 PATH 列表
卷序列号为 B035-7893
C:\USERS\HERRERA\DJANGOOPT\DJBLOG\BLOG
│  admin.py
│  apps.py
│  models.py
│  tests.py
│  views.py
│  __init__.py
│
└─migrations
        __init__.py
```

这个应用的文件夹结构 Django 已经为我们建立好了，但它还只是包含各种文件的一个文件夹而已，Django 目前还不知道这是一个应用。我们得告诉 Django 这是我们建立的应用，专业一点说就是在 Django 的配置文件中注册这个应用。  

  
C:\Users\Herrera\djangoopt\djblog\djblog\setting.py  
```python# Application definition

INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
	'blog',#注册blog应用
]
```


## migration  
```
C:\Users\Herrera\djangoopt\djblog>python manage.py makemigrations
Migrations for 'blog':
  blog\migrations\0001_initial.py:
    - Create model Category
    - Create model Post
    - Create model Tag
    - Add field tags to post
```
C:\Users\Herrera\djangoopt\djblog\blog\migrations 下面会多出：`0001_initial.py` 这个文件是 Django 用来记录我们对模型做了哪些修改的文件。  

go on
```
C:\Users\Herrera\djangoopt\djblog>python manage.py migrate
Operations to perform:
  Apply all migrations: admin, auth, blog, contenttypes, sessions
Running migrations:
  Applying contenttypes.0001_initial... OK
  Applying auth.0001_initial... OK
  Applying admin.0001_initial... OK
  Applying admin.0002_logentry_remove_auto_add... OK
  Applying contenttypes.0002_remove_content_type_name... OK
  Applying auth.0002_alter_permission_name_max_length... OK
  Applying auth.0003_alter_user_email_max_length... OK
  Applying auth.0004_alter_user_username_opts... OK
  Applying auth.0005_alter_user_last_login_null... OK
  Applying auth.0006_require_contenttypes_0002... OK
  Applying auth.0007_alter_validators_add_error_messages... OK
  Applying auth.0008_alter_user_username_max_length... OK
  Applying blog.0001_initial... OK
  Applying sessions.0001_initial... OK
```

不过此时还只是告诉了 Django 我们做了哪些改变，为了让 Django 真正地为我们创建数据库表，接下来又执行了 python manage.py migrate 命令。  
Django 通过检测应用中 migrations\ 目录下的文件，得知我们对数据库做了哪些操作，然后它把这些操作翻译成数据库操作语言，从而把这些操作作用于真正的数据库。  

```
C:\Users\Herrera\djangoopt\djblog>python manage.py sqlmigrate blog 0001
BEGIN;
--
-- Create model Category
--
CREATE TABLE "blog_category" ("id" integer NOT NULL PRIMARY KEY AUTOINCREMENT, "name" varchar(100) NOT NULL);
--
-- Create model Post
--
CREATE TABLE "blog_post" ("id" integer NOT NULL PRIMARY KEY AUTOINCREMENT, "title" varchar(70) NOT NULL, "body" text NOT NULL, "created_time" datetime NOT NULL, "modified_time" datetime NOT NULL, "excerpt" varchar(200) NOT NULL, "author_id" integer NOT NULL REFERENCES "auth_user" ("id"), "category_id" integer NOT NULL REFERENCES "blog_category" ("id"));
--
-- Create model Tag
--
CREATE TABLE "blog_tag" ("id" integer NOT NULL PRIMARY KEY AUTOINCREMENT, "name" varchar(100) NOT NULL);
--
-- Add field tags to post
--
CREATE TABLE "blog_post_tags" ("id" integer NOT NULL PRIMARY KEY AUTOINCREMENT, "post_id" integer NOT NULL REFERENCES "blog_post" ("id"), "tag_id" integer NOT NULL REFERENCES "blog_tag" ("id"));
CREATE INDEX "blog_post_4f331e2f" ON "blog_post" ("author_id");
CREATE INDEX "blog_post_b583a629" ON "blog_post" ("category_id");
CREATE UNIQUE INDEX "blog_post_tags_post_id_4925ec37_uniq" ON "blog_post_tags" ("post_id", "tag_id");
CREATE INDEX "blog_post_tags_f3aa1999" ON "blog_post_tags" ("post_id");
CREATE INDEX "blog_post_tags_76f094bc" ON "blog_post_tags" ("tag_id");
COMMIT;

```
你将看到输出了经 Django 翻译后的数据库表创建语句，这有助于你理解 Django ORM 的工作机制。  

### 选择数据库版本
我们没有安装任何的数据库软件，Django 就帮我们迁移了数据库。这是因为我们使用了 Python 内置的 SQLite3 数据库。  
SQLite3 是一个十分轻巧的数据库，它仅有一个文件。  
你可以看一到项目根目录下多出了一个 db.sqlite3 的文件，这就是 SQLite3 数据库文件，Django 博客的数据都会保存在这个数据库文件里。  
Django 在 settings.py 里为我们做了一些默认的数据库配置：  

blogproject/settings.py  
```
## 其它配置选项...
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.sqlite3',
        'NAME': os.path.join(BASE_DIR, 'db.sqlite3'),
    }
}
## 其它配置选项...
```
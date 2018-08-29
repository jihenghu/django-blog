title: 创建 Admin 后台管理员账户  
author: jiheng hu  
tags: django,python  
category : Python  
slug: django-blog-admin  
date: 2018-05-25  
modified: 2018-05-25  

[TOC]
## 创建 Admin 后台管理员账户  
运行 python manage.py createsuperuser 命令新建一个：  
```cmd
C:\Users\Herrera\djangoopt\djblog>python manage.py createsuperuser
Username (leave blank to use 'herrera'): jihenghu
Email address: hjh18305@gmail.com
Password:
Password (again):
Superuser created successfully.
```

[jihenghu hjh1831743701h]

## 在 Admin 后台注册模型  
这样 Django Admin 才能知道它们的存在，注册非常简单，只需要在 blog\admin.py 中加入下面的代码：  

```python
#blog/admin.py

from django.contrib import admin
from .models import Post, Category, Tag

admin.site.register(Post)
admin.site.register(Category)
admin.site.register(Tag)
```

python manage.py runserver启动服务，访问：localhost:8000/admin/ 即可进入后台。  

在 admin post 列表页面，我们只看到了文章的标题  
但是我们希望它显示更加详细的信息，这需要我们来定制 Admin 了，在 admin.py 添加如下代码：  
blog/admin.py  
```python
from django.contrib import admin
from .models import Post, Category, Tag

class PostAdmin(admin.ModelAdmin):
    list_display = ['title', 'created_time', 'modified_time', 'category', 'author']

# 把新增的 PostAdmin 也注册进来
admin.site.register(Post, PostAdmin)
admin.site.register(Category)
admin.site.register(Tag)
```
刷新 Admin Post 列表页面，可以看到显示的效果好多了。  

title: 创建django应用前端模板  
author: jiheng hu  
tags: django,python  
category : Python  
slug: django-blog-template  
date: 2018-05-28  
modified: 2018-05-28  

## 使用模板系统  
在 blog\urls.py 中写入这些代码：  
blog/urls.py  

``` python
from django.conf.urls import url

from . import views

urlpatterns = [
    url(r'^$', views.index, name='index'),
]
```

在我们的项目根目录（即 `manage.py` 文件所在目录）下建立一个名为 `templates `的文件夹，用来存放我们的模板。    
然后在 `templates\ `目录下建立一个名为` blog `的文件夹，用来存放和 `blog `应用相关的模板。  
我们在 `templates\blog `目录下建立一个名为 `index.html `的文件，此时你的目录结构应该是这样的：  

```cmd
blogproject\
    manage.py
    blogproject\
        __init__.py
        settings.py
        ...
    blog\
        __init__.py
        models.py
        ,,,
    templates\
        blog\
            index.html
```

在` templates\blog\index.html` 文件里写入下面的代码：  
```HTML
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>{{ title }}</title>
</head>
<body>
<h1>{{ welcome }}</h1>
</body>
</html>
```
这是一个标准的 HTML 文档，只是里面有两个比较奇怪的地方：`{{ title }}`，`{{ welcome }} `。  
这是 Django 规定的语法。用 `{{ }}` 包起来的变量叫做模板变量。  
Django 在渲染这个模板的时候会根据我们传递给模板的变量替换掉这些变量，最终在模板中显示的将会是我们传递的值。  


在 `settings.py `找到` TEMPLATES `选项，它的内容是这样的：  
blogproject/settings.py
```python
TEMPLATES = [
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        'DIRS': [],
        'APP_DIRS': True,
        'OPTIONS': {
            'context_processors': [
                'django.template.context_processors.debug',
                'django.template.context_processors.request',
                'django.contrib.auth.context_processors.auth',
                'django.contrib.messages.context_processors.messages',
            ],
        },
    },
]
``` 
其中 DIRS 就是设置模板的路径，在 `[]` 中写入 `os.path.join(BASE_DIR, 'templates')`，即像下面这样：  

blogproject/settings.py  
```python
TEMPLATES = [
    {
        ...
        'DIRS': [os.path.join(BASE_DIR, 'templates')],
        ...
    },
]
```  
`BASE_DIR` 是 `settings.py` 在配置开头前面定义的变量，记录的是工程根目录 `blogproject\ `的值（注意是最外层的` blogproject\` 目录）。
在这个目录下有模板文件所在的目录 `templates\`，于是利用`os.path.join` 把这两个路径连起来，构成完整的模板路径，`Django` 就知道去这个路径下面找我们的模板了。


视图函数可以改一下了：  
blog/views.py  
```python
from django.http import HttpResponse
from django.shortcuts import render

def index(request):
    return render(request, 'blog/index.html', context={
                      'title': '我的博客首页', 
                      'welcome': '欢迎访问我的博客首页'
                  })
```

```cmd python manage.py runserver```   重启服务并查看效果。  

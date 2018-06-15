＞ [Home](../index.md)    ＞＞ [first step](1805-django-first-step.md) ＞＞ [second step](1805-django-second-step.md)  

＞＞[4th step](1805-django-4th-step.md)  


#  1806-django-third-step

##  Overview
- Django site で、templateを使った画面生成を、記述する。


##  Code share


## Environment
- windows / powershell。（Ubuntuで操作の場合は、読み替えてください）

- package environment

```powershell
PS G:\> python
Python 3.6.5 (v3.6.5:f59c0932b4, Mar 28 2018, 16:07:46) [MSC v.1900 32 bit (Intel)] on win32
Type "help", "copyright", "credits" or "license" for more information.
>>> exit()
PS G:\> python --version
Python 3.6.5
PS G:\> virtualenv --version
16.0.0
PS G:\> whereis virtualenvwrapper
G:\Users\sakai\AppData\Local\Programs\Python\Python36-32\Scripts\virtualenvwrapper.bat
PS G:\> dir Env: | Out-String -Stream | sls 'WORKON|PROJECT'

PROJECT_HOME                   G:\workplace\py
WORKON_HOME                    G:\env\py


PS G:\> workon

Pass a name to activate one of the following virtualenvs:
==============================================================================
djfirst
djsecond
sandbox

```

##  Procedure List

### １．virtualenv環境 - pip install

- mkprojectにより、project環境を構築。（virtualenvwrapperを使ってます。condaの場合は、読み替えてください）

```powershell
PS G:\workspace\py> mkproject djthird
PS G:\workspace\py> workon

Pass a name to activate one of the following virtualenvs:
==============================================================================
batch
bplate
djfirst
djfirst2
mq
mservice
rest
sandbox
djthird

PS G:\workspace\py>

```

- $Env:PROJECT_HOME\djthirdフォルダに移動。
- 以下を実行して、activate 

```powershell
PS G:\> $p = 'djthird'
PS G:\> cd $Env:WORKON_HOME\$p
PS G:\env\py\djthird> .\Scripts\activate
(djthird) PS G:\env\py\djthird> cd $Env:PROJECT_HOME\$p
(djthird) PS G:\workplace\py\djthird>

```

- requirements packages

```powershell
(djthird) PS G:\workplace\py\djthird> pip install django
Collecting django
  Using cached https://files.pythonhosted.org/packages/56/0e/afdacb47503b805f3ed213fe732bff05254c8befaa034bbada580be8a0ac/Django-2.0.6-py3-none-any.whl
Collecting pytz (from django)
  Using cached https://files.pythonhosted.org/packages/dc/83/15f7833b70d3e067ca91467ca245bae0f6fe56ddc7451aa0dc5606b120f2/pytz-2018.4-py2.py3-none-any.whl
Installing collected packages: pytz, django
Successfully installed django-2.0.6 pytz-2018.4
(djthird) PS G:\workplace\py\djthird> pip freeze
Django==2.0.6
pytz==2018.4
(djthird) PS G:\workplace\py\djthird> django-admin --version
2.0.6
```


### ２．Create site
- virtualenvwrapperのmkprojectで作成したproject folderが、 django-admin で生成するフォルダと かぶるので、削除する。
- 以下、Site (project)を作成する。

```powershell
(djthird) PS G:\workplace\py\djthird> cd ..
(djthird) PS G:\workplace\py> rmdir djthird
(djthird) PS G:\workplace\py> django-admin startproject djthird
(djthird) PS G:\workplace\py> ls


    Directory: G:\workplace\py


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
d-----         6/2/2018   8:18 AM                djfirst
d-----         6/2/2018  12:01 PM                djsecond
d-----        6/15/2018   9:07 PM                djthird
d-----        6/10/2018   4:29 PM                sandbox


(djthird) PS G:\workplace\py> cd .\djthird\
(djthird) PS G:\workplace\py\djthird> ls


    Directory: G:\workplace\py\djthird


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
d-----        6/15/2018   9:07 PM                djthird
-a----        6/15/2018   9:07 PM            554 manage.py
```


- siteを、python manage.py runserverで起動する。
  access : http://127.0.0.1:8000/

```powershell
(djthird) PS G:\workplace\py\djthird> python manage.py runserver
Performing system checks...

System check identified no issues (0 silenced).

You have 14 unapplied migration(s). Your project may not work properly until you apply the migrations for app(s): admin, auth, contenttypes, sessions.
Run 'python manage.py migrate' to apply them.
June 15, 2018 - 21:08:22
Django version 2.0.6, using settings 'djthird.settings'
Starting development server at http://127.0.0.1:8000/
Quit the server with CTRL-BREAK.
```


- siteを、python manage.py runserver 0.0.0.0:8000 で起動する。
  access : http://192.168.1.189:8000/ ※固定IPで他のPCからアクセスする場合
- 以下の対応を、/djthird/settings.pyに記述する。

- /djthird/settings.py

```python
ALLOWED_HOSTS = ['192.168.1.189', '127.0.0.1']
```


### ３．Create App
- 簡単なtemplateを使ったWelcome Home を表示させる。

```powershell
(djthird) PS G:\workplace\py\djthird> python manage.py startapp hello
```

### ３．１　Web Siteの設定変更

- 簡単なテンプレートを使ったhello world


- /djthird/settings.py

```python
# Application definition

INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'hello',   ##＜＜
]

TEMPLATES = [
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        'DIRS': [os.path.join(BASE_DIR, 'templates'),], ##＜＝
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

![django third template folder](https://i.imgur.com/uDpraRp.png)

- /djthird/urls.py

```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('hello/', include('hello.urls')),
    path('admin/', admin.site.urls),
]

```


### ３．２　Web Appの設定変更

- hello/views.py

```python
from django.http.response import HttpResponse
from django.shortcuts import render


def hello(request):
    return render(request,'hello.html')

```

- hello/urls.py

```python
from django.urls import path

from . import views

urlpatterns = [
    path('', views.hello, name='hello'),
]

```

### ３．３ Web Appのtemplate

- templates/hello.html

```html
<!DOCTYPE html>
<html>
 <head lang="ja">
    <meta charset="UTF-8">
    <title></title>
 </head>
 <body>
  <p>welcome Django Template page</p>
 </body>
</html>

```

- http://127.0.0.1:8000/hello/
![django third](https://i.imgur.com/5YzzzUC.png)


## ４．ページをを追加する

### ４．１　Webサイトの設定変更

- djthird/urls.py
 
 特になし


### ４．２　Webアプリの設定変更

- djthird/views.py

```python
from django.http.response import HttpResponse
from django.shortcuts import render

from datetime import datetime

def hello(request):
    return render(request,'hello.html')

def index(request):
    d_now = datetime.now()
    Datetime = {
        'timestamp': d_now.strftime("%Y/%m/%d %H:%M:%S") ,
    }
    return render(request, 'index.html', Datetime)
```

- hello/urls.py

```python
from django.urls import path
from django.conf.urls import url ## FIXME url/pathの違い

from . import views

urlpatterns = [
    path('', views.hello, name='hello'),  ## /hello
    url(r'^index$', views.index, name='index'), ## /hello/index
]

```


### ４．３ Web Appのtemplate

- template/index.html

```html
<!DOCTYPE html>
<html>
 <head lang="ja">
    <meta charset="UTF-8">
    <title></title>
 </head>
 <body>
  <p>Hello template index</p>

    <p>{{timestamp}} です</p>

 </body>
</html>
```

- http://127.0.0.1:8000/hello/
![django third](https://i.imgur.com/5YzzzUC.png)

- http://127.0.0.1:8000/hello/index
![django-third-hello-index](https://i.imgur.com/UuNNE29.png)


- http://127.0.0.1:8000
![django-third-not-found](https://i.imgur.com/PpsYy27.png)

## ** SUMMARY
- 以下を実施した。
  * -- django install
  * -- Site 作成
  * -- Web app 作成
  * -- Web appのページの追加

// --- end of file
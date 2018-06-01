＞ [Home](../index.md)

# 1805-django-first-step

## Overview
- Djangoのインストールと、hello worldを表示するまでを、記述する。


## Environment
- Windows 10 1709
- powershell 5.1.16299.431
- python 3.6.5
- pip 10.0.1
- virtualenv 16.0.0
- virtualenvwrapper-win
- git 2.16.2.windows.1

- 以下、このArticleでinstallation
-- django 2.0.5

## 1. 環境確認

- poowershellで環境を確認


``` powershell
PS G:\env\py> git --version
git version 2.16.2.windows.1
PS G:\env\py> python --version
Python 3.6.5
PS G:\env\py> pip --version
pip 10.0.1 from c:\users\niddev\appdata\local\programs\python\python36-32\lib\site-packages\pip (python 3.6)
PS G:\env\py> virtualenv --version
16.0.0
PS G:\env\py> dir Env: | out-string -stream | sls "WORKON|PROJECT"

PROJECT_HOME                   G:\workspace\py
WORKON_HOME                    G:\env\py

PS G:\env\py> workon

Pass a name to activate one of the following virtualenvs:
==============================================================================

```


## 2. virtualenv構築

- mkprojectで、virtual環境を構築

``` powershell
PS G:\env\py> mkproject djfirst
Using base prefix 'c:\\users\\<username>\\appdata\\local\\programs\\python\\python36-32'
New python executable in G:\env\py\djfirst\Scripts\python.exe
Installing setuptools, pip, wheel...done.

    "G:\workspace\py\djfirst" is now the project directory for
    virtualenv "G:\env\py\djfirst"

    "G:\workspace\py\djfirst" added to
    G:\env\py\djfirst\Lib\site-packages\virtualenv_path_extensions.pth
PS G:\env\py> workon

Pass a name to activate one of the following virtualenvs:
==============================================================================
djfirst
```


## 3. pip install django

### 3.1 django installation

- djangoのインストール

``` powershell
PS > cd $Env:WORKON_HOME
PS G:\env\py> .\djfirst\Scripts\activate
(djfirst) PS G:\env\py> pip install django
Collecting django
  Using cached https://files.pythonhosted.org/packages/23/91/2245462e57798e9251de87c88b2b8f996d10ddcb68206a8a020561ef7bd3/Django-2.0.5-py3-none-any.whl
Collecting pytz (from django)
  Using cached https://files.pythonhosted.org/packages/dc/83/15f7833b70d3e067ca91467ca245bae0f6fe56ddc7451aa0dc5606b120f2/pytz-2018.4-py2.py3-none-any.whl
Installing collected packages: pytz, django
Successfully installed django-2.0.5 pytz-2018.4

(djfirst) PS G:\env\py> pip list
Package    Version
---------- -------
Django     2.0.5
pip        10.0.1
pytz       2018.4
setuptools 39.2.0
wheel      0.31.1

(djfirst) PS G:\env\py> lssitepackages

dir /b "G:\env\py\djfirst\Lib\site-packages"
==============================================================================
django
Django-2.0.5.dist-info
easy_install.py
pip
pip-10.0.1.dist-info
pkg_resources
pytz
pytz-2018.4.dist-info
setuptools
setuptools-39.2.0.dist-info
virtualenv_path_extensions.pth
wheel
wheel-0.31.1.dist-info
__pycache__

G:\env\py\djfirst\Lib\site-packages\easy-install.pth
==============================================================================
指定されたファイルが見つかりません。

G:\env\py\djfirst\Lib\site-packages\virtualenv_path_extensions.pth
==============================================================================
G:\workspace\py\djfirst


(djfirst) PS G:\env\py> dir $Env:WORKON_HOME\djfirst\Scripts

    Directory: G:\env\py\djfirst\Scripts

Mode                LastWriteTime         Length Name
----                -------------         ------ ----
d-----         6/1/2018   6:46 AM                __pycache__
-a----         6/1/2018   6:44 AM           2169 activate
-a----         6/1/2018   6:44 AM            948 activate.bat
-a----         6/1/2018   6:44 AM           8325 activate.ps1
-a----         6/1/2018   6:44 AM           1137 activate_this.py
-a----         6/1/2018   6:44 AM            599 deactivate.bat
-a----         6/1/2018   6:46 AM          93080 django-admin.exe
-a----         6/1/2018   6:46 AM            146 django-admin.py
-a----         6/1/2018   6:44 AM          93047 easy_install-3.6.exe
-a----         6/1/2018   6:44 AM          93047 easy_install.exe
-a----         6/1/2018   6:44 AM          93029 pip.exe
-a----         6/1/2018   6:44 AM          93029 pip3.6.exe
-a----         6/1/2018   6:44 AM          93029 pip3.exe
-a----         6/1/2018   6:44 AM          97944 python.exe
-a----         6/1/2018   6:44 AM          58520 python3.dll
-a----         6/1/2018   6:44 AM        3303064 python36.dll
-a----         6/1/2018   6:44 AM          96408 pythonw.exe
-a----         6/1/2018   6:44 AM          93026 wheel.exe
```

### 3.2 django-admin

- django-admin : django web application frameworkのadminツール
  + djangoでは、サイト、アプリのひな型をコマンドで指示して自動作成したり、modelに即したRDBを自動で生成したりする機能がある提供されている。

``` powershell
(djfirst) PS G:\workspace> whereis django-admin
G:\env\py\djfirst\Scripts\django-admin.exe
(djfirst) PS G:\> django-admin --version
2.0.5
```
-- django-admin command

|comand|description|note|
|------|------|------|
|startproject|project　(site)　を作成||
|startapp|web appを作成||
|runserver|siteを起動する||
|createsuperuser|管理ユーザを作成する||
|makemigrations|マイグレーションファイルの作成||
|migrate|データベースにマイグレーションを適用する||

- reference
-- Django 管理コマンド manage.py まとめ
-- https://qiita.com/okoppe8/items/7e3de8a4dd40b48debea


## 4. Site作成

### 4.1 django-admin startproject：サイトの作成

- djangoサイト（Web Application Server)を、http://127.0.0.1:8000/で立ち上げる
  + mkprojectで作成したプロジェクトフォルダが、django-adminのcommandで生成するフォルダとかぶるので、削除する。
  + その後、```django-admin startproject djfirst```で、Site（プロジェクト）を生成する。

``` powershell
(djfirst) PS > cd $Env:PROJECT_HOME
(djfirst) PS G:\workplace\py> rmdir .\djfirst\
(djfirst) PS G:\workplace\py> django-admin startproject djfirst
(djfirst) PS G:\workplace\py> ls -recurse

    Directory: G:\workplace\py

Mode                LastWriteTime         Length Name
----                -------------         ------ ----
d-----         6/1/2018   6:56 AM                djfirst

    Directory: G:\workplace\py\djfirst

Mode                LastWriteTime         Length Name
----                -------------         ------ ----
d-----         6/1/2018   6:56 AM                djfirst
-a----         6/1/2018   6:56 AM            554 manage.py

    Directory: G:\workplace\py\djfirst\djfirst

Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----         6/1/2018   6:56 AM           3211 settings.py
-a----         6/1/2018   6:56 AM            770 urls.py
-a----         6/1/2018   6:56 AM            407 wsgi.py
-a----         6/1/2018   6:56 AM              0 __init__.py
```


### 4.2 python manage.py runserver：サイトの立ち上げ

``` powershell
(djfirst) PS G:\workplace\py> cd .\djfirst\
(djfirst) PS G:\workplace\py\djfirst> python manage.py runserver
Performing system checks...

System check identified no issues (0 silenced).

You have 14 unapplied migration(s). Your project may not work properly until you apply the migrations for app(s): admin, auth, contenttypes, sessions.
Run 'python manage.py migrate' to apply them.
June 01, 2018 - 06:59:51
Django version 2.0.5, using settings 'djfirst.settings'
Starting development server at http://127.0.0.1:8000/
Quit the server with CTRL-BREAK.

```

### 4.3 SiteへAccess
- access http://127.0.0.1:8000/

![Django first installation success screen](https://i.imgur.com/KDJJhA9.png)


- 生成されたファイル

|py|description|note|
|------|------|------|
|manage.py|manageツール||
|db.sqlite3|RDBファイル(SQLite3)||
|djfirst|Package directory||
|jdfirst/settings.py|Web Siteの設定ファイル||
|jdfirst/urls.py|Pathの設定ファイル (url dispatcher) ||
|jdfirst/wsgi.py|Web ServerとApplication Serverの接続設定<br>(WSGI互換Webサーバーとのエントリーポイント)|※変更なし|
|jdfirst/\_\_init__.py|このディレクトリがpythonパッケージであることを示す空ファイル|※変更なし|


### 4.4 git repository commit

- gitの初期設定


``` powershell
(djfirst) PS G:\workspace\py\djfirst> git config --global user.name "User Name"
(djfirst) PS G:\workspace\py\djfirst> git config --global user.email "User Mail address"
(djfirst) PS G:\workspace\py\djfirst> git config --list
core.symlinks=false
core.autocrlf=true
color.diff=auto
 :
user.name=<user name>
user.email=<user mail address>
 :
core.symlinks=false
core.ignorecase=true
```


- gitのfirst commit


``` powershell
(djfirst2) PS G:\workspace\py\djfirst> notepad README.md
(djfirst2) PS G:\workspace\py\djfirst> notepad .gitignore
(djfirst2) PS G:\workspace\py\djfirst> ls

    ディレクトリ: G:\workspace\py\djfirst

Mode                LastWriteTime         Length Name
----                -------------         ------ ----
d-----       2018/05/28     12:22                djfirst
-a----       2018/05/28     11:35             13 .gitignore
-a----       2018/05/28     12:22              0 db.sqlite3
-a----       2018/05/28     12:18            555 manage.py
-a----       2018/05/28     11:32            144 README.md

(djfirst) PS G:\workspace\py\djfirst> git init
Initialized empty Git repository in G:/workspace/py/djfirst/.git/
(djfirst) PS G:\workspace\py\djfirst> git add .
(djfirst) PS G:\workspace\py\djfirst> git commit -m "first commit"
[master (root-commit) 57465b3] first commit
 8 files changed, 180 insertions(+)
 create mode 100644 .gitignore
 create mode 100644 README.md
 create mode 100644 db.sqlite3
 create mode 100644 djfirst/__init__.py
 create mode 100644 djfirst/settings.py
 create mode 100644 djfirst/urls.py
 create mode 100644 djfirst/wsgi.py
 create mode 100644 manage.py
```



## 5. Hello world web app作成
- reference
  - Djangoメモ(3) : Hello Worldを表示するアプリを作成 
    * https://wonderwall.hatenablog.com/entry/2018/03/05/070000

### 5.1 python manage.py startapp hello : Web Applicationの作成

``` powershell
(djfirst) PS G:\workspace\py\djfirst> python manage.py startapp hello
(djfirst) PS G:\workspace\py\djfirst> ls

    ディレクトリ: G:\workspace\py\djfirst

Mode                LastWriteTime         Length Name
----                -------------         ------ ----
d-----       2018/05/28     12:22                djfirst
d-----       2018/05/28     12:56                hello
-a----       2018/05/28     12:35             18 .gitignore
-a----       2018/05/28     12:22              0 db.sqlite3
-a----       2018/05/28     12:18            555 manage.py
-a----       2018/05/28     11:32            144 README.md

(djfirst2) PS G:\workspace\py\djfirst> ls .\hello\

    ディレクトリ: G:\workspace\py\djfirst\hello

Mode                LastWriteTime         Length Name
----                -------------         ------ ----
d-----       2018/05/28     12:56                migrations
-a----       2018/05/28     12:56             66 admin.py
-a----       2018/05/28     12:56             90 apps.py
-a----       2018/05/28     12:56             60 models.py
-a----       2018/05/28     12:56             63 tests.py
-a----       2018/05/28     12:56             66 views.py
-a----       2018/05/28     12:56              0 __init__.py
```

- 生成されたファイル

|py|description|note|
|------|------|------|
|hello|Web App directory||
|hello/models.py|modelsファイル||
|hello/views.py|viewsファイル<br>(pathに対する動作を定義) ||
|hello/urls.py|Routing setting |追加で作成|
|hello/tests.py|unittest用||
|hello/apps.py||※変更なし|
|hello/admin.py||※変更なし|
|hello/\_\_init__.py|このディレクトリがpythonパッケージである<br>ことを示す空ファイル|※変更なし|

### 5.2 hello/views.pyを編集

- hello/views.py

``` python:views.py
from django.http import HttpResponse

def hello(request):
    return HttpResponse('Hello Django!')
```

### 5.3 djfirst/urls.pyを編集

``` python:urls.py
urlpatterns = [
    path('', views.hello, name='hello'),
    path('admin/', admin.site.urls),
]
```

### 5.4 Web Applicationの起動
- web siteを起動


``` powershell
(djfirst) PS G:\workspace\py\djfirst2> python manage.py runserver
```


### 5.5 Web ApplicationへのAccess
- http://127.0.0.1:8000/

![Django Hello ](https://i.imgur.com/V3R8alb.png)

### 5.4 git commit
- git commit

``` powershell
(djfirst) PS G:\workspace\py\djfirst2> git add .
(djfirst) PS G:\workspace\py\djfirst2> git commit -m "add hello world apps."
[master dfe436c] add hello world apps.
 9 files changed, 27 insertions(+), 1 deletion(-)
 create mode 100644 hello/__init__.py
 create mode 100644 hello/admin.py
 create mode 100644 hello/apps.py
 create mode 100644 hello/migrations/__init__.py
 create mode 100644 hello/models.py
 create mode 100644 hello/tests.py
 create mode 100644 hello/urls.py
 create mode 100644 hello/views.py
```

## 6. まとめ

- 以下を実施した。
  - djangoをインストール
  - Web Site作成
  - Web Applicationを作成（簡易なHello Django!と表示）


// --- end of markdown

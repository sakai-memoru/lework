＞ [Home](../index.md)    ＞＞ [first step](1805-django-first-step.md)

# 1805-django-second-step

## Overview
- Templateを使って、hello worldを表示するまでを、記述する。
- Django管理画面を操作してみる。

## Code
https://github.com/sakai-memoru/djsecond

## Environment
- Windows 10 1709
- powershell 5.1.16299.431
- python 3.6.5
- pip 10.0.1
- virtualenv 16.0.0
- virtualenvwrapper-win
- git 2.16.2.windows.1
- django 2.0.5

## 1. 環境確認

- powershellで環境を確認


``` powershell
PS G:\env\py> git --version
git version 2.16.2.windows.1
PS G:\env\py> python --version
Python 3.6.5
PS G:\env\py> pip --version
pip 10.0.1 from c:\users\niddev\appdata\local\programs\python\python36-32\lib\site-packages\pip (python 3.6)

PS G:\env\py> pip --version
PS G:\env\py> pip list
Package               Version
--------------------- -------
pip                   10.0.1
setuptools            39.0.1
virtualenv            16.0.0
virtualenvwrapper-win 1.2.5

PS G:\env\py> virtualenv --version
16.0.0


PS G:\env\py> dir Env: | out-string -stream | sls "WORKON|PROJECT"

PROJECT_HOME                   G:\workspace\py
WORKON_HOME                    G:\env\py

PS G:\env\py> workon

Pass a name to activate one of the following virtualenvs:
==============================================================================
djfirst

```


## 2. make virtualenv, install django, start a site

- make virtualenv with mkproject

``` powershell
PS G:\env\py> mkproject djsecond
Using base prefix 'g:\\users\\sakai\\appdata\\local\\programs\\python\\python36-32'
New python executable in G:\env\py\djsecond\Scripts\python.exe
Installing setuptools, pip, wheel...done.

    "G:\workplace\py\djsecond" is now the project directory for
    virtualenv "G:\env\py\djsecond"

    "G:\workplace\py\djsecond" added to
    G:\env\py\djsecond\Lib\site-packages\virtualenv_path_extensions.pth
PS G:\env\py> workon

Pass a name to activate one of the following virtualenvs:
==============================================================================
djfirst
djsecond

PS G:\env\py> cd $Env:WORKON_HOME
PS G:\env\py> .\djsecond\Scripts\activate
(djsecond) PS G:\env\py> pip install django
Collecting django
  Downloading https://files.pythonhosted.org/packages/56/0e/afdacb47503b805f3ed213fe732bff05254c8befaa034bbada580be8a0ac/Django-2.0.6-py3-none-any.whl (7.1MB)
    100% |████████████████████████████████| 7.1MB 5.4MB/s
Collecting pytz (from django)
  Using cached https://files.pythonhosted.org/packages/dc/83/15f7833b70d3e067ca91467ca245bae0f6fe56ddc7451aa0dc5606b120f2/pytz-2018.4-py2.py3-none-any.whl
Installing collected packages: pytz, django
Successfully installed django-2.0.6 pytz-2018.4
(djsecond) PS G:\env\py> django-admin --version
2.0.6

(djsecond) PS G:\env\py> cd $Env:PROJECT_HOME
(djsecond) PS G:\workplace\py> rmdir djsecond
(djsecond) PS G:\workplace\py> ls


    Directory: G:\workplace\py


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
d-----         6/2/2018   8:18 AM                djfirst


(djsecond) PS G:\workplace\py> django-admin djsecond
No Django settings specified.
Unknown command: 'djsecond'
Type 'django-admin help' for usage.
(djsecond) PS G:\workplace\py> django-admin startproject djsecond
(djsecond) PS G:\workplace\py> ls

    Directory: G:\workplace\py

Mode                LastWriteTime         Length Name
----                -------------         ------ ----
d-----         6/2/2018   8:18 AM                djfirst
d-----         6/2/2018   9:16 AM                djsecond

(djsecond) PS G:\workplace\py> cd .\djsecond\
(djsecond) PS G:\workplace\py\djsecond>
```

## 3. start app

- Start a web application.

``` powershell

(djsecond) PS G:\workplace\py\djsecond> django-admin startapp hello2

(djsecond) PS G:\workplace\py\djsecond> sakura README.md
(djsecond) PS G:\workplace\py\djsecond> sakura .gitignore


(djsecond) PS G:\workplace\py\djsecond> ls

    Directory: G:\workplace\py\djsecond

Mode                LastWriteTime         Length Name
----                -------------         ------ ----
d-----         6/2/2018   9:17 AM                djsecond
d-----         6/2/2018   9:22 AM                hello2
-a----         6/2/2018   9:17 AM              0 db.sqlite3
-a----         6/2/2018   9:16 AM            555 manage.py

(djsecond) PS G:\workplace\py\djsecond> explorer .
```

![Django second application''s folder](https://i.imgur.com/0C9CbUr.png)


- initial commit

```
(djsecond) PS G:\workplace\py\djsecond> git init
Initialized empty Git repository in G:/workplace/py/djsecond/.git/

(djsecond) PS G:\workplace\py\djsecond> git status
On branch master

Initial commit

Untracked files:
  (use "git add <file>..." to include in what will be committed)

        .gitignore
        README.md
        db.sqlite3
        djsecond/
        hello2/
        manage.py

nothing added to commit but untracked files present (use "git add" to track)
(djsecond) PS G:\workplace\py\djsecond> git add .
(djsecond) PS G:\workplace\py\djsecond> git commit -m 'first commit'
[master (root-commit) 6e9595b] first commit
 15 files changed, 265 insertions(+)
 create mode 100644 .gitignore
 create mode 100644 README.md
 create mode 100644 db.sqlite3
 create mode 100644 djsecond/__init__.py
 create mode 100644 djsecond/settings.py
 create mode 100644 djsecond/urls.py
 create mode 100644 djsecond/wsgi.py
 create mode 100644 hello2/__init__.py
 create mode 100644 hello2/admin.py
 create mode 100644 hello2/apps.py
 create mode 100644 hello2/migrations/__init__.py
 create mode 100644 hello2/models.py
 create mode 100644 hello2/tests.py
 create mode 100644 hello2/views.py
 create mode 100644 manage.py
(djsecond) PS G:\workplace\py\djsecond>

```

## 4. create superuser
- Migrate database and create superuser.

  - reference
    - Django 管理画面の利用 
      - http://python.keicode.com/django/admin-site-enabling.php 

``` powershell
(djsecond) PS G:\workplace\py\djsecond> python manage.py migrate
Operations to perform:
  Apply all migrations: admin, auth, contenttypes, sessions
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
  Applying auth.0009_alter_user_last_name_max_length... OK
  Applying sessions.0001_initial... OK

(djsecond) PS G:\workplace\py\djsecond> python manage.py createsuperuser
Username (leave blank to use 'sakai'): admin
Email address: sakai.memoru@gmail.com
Password:
Password (again):
Superuser created successfully.
(djsecond) PS G:\workplace\py\djsecond>
```

- access http://127.0.0.1:8000/admin/
  - When managing databse related to models, we can use this admin tool.

![django admin login](https://i.imgur.com/g6xD3PW.png)

![django admin top](https://i.imgur.com/KEbMtsU.png)

![django admin users](https://i.imgur.com/T5GRk7z.png)

## 5. Web Application with templates

``` powershell
(djsecond) PS G:\workplace\py\djsecond> mkdir template

```

[gimmick:gist](19a6f60a50919cf879becbd6c3ef5d81)

## 6. Summery

- On the article we have done below:
  - Login on Django Admin site.
  - Displate html with django template.


// --- end of markdown

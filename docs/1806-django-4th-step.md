＞ [Home](../index.md)    ＞＞ [first step](1805-django-first-step.md) ＞＞ [second step](1805-django-second-step.md)  ＞＞[Third step](1806-django-third-step.md)  

# * 1806-django-4th-step

## Overview
- Django site で、DBとORMを使った画面生成を、記述する。


## Code share


## Diagrams
![django MVT ](https://i.imgur.com/vCofEWY.png)

|module|role|note|
|------|----|----|
|site/wsgi.py|WSGI|Web ServerとApplication Serverを取り持つ|
|site/settings.py|site setting|siteの定義ファイル|
|site/urls.py|urlpatterns(dispatch)|Web Appへ振り分ける|
|apps/urls.py|router|Web Apps内のWeb Pageへ振り分ける|
|apps/views.py|control|requestに対するactionを定義|
|apps/models.py|data model|Data Model(ORMでDatabaseと自動で連携)|
|template/xxx.pug or html|template view|template engineと連携したResponse View(page)生成|
|db.sqlite3|database|DBファイル(default)|


## Reference
- Django models
  -  https://docs.djangoproject.com/en/2.0/topics/db/models/
- Django モデル層
  -  https://qiita.com/sandream/items/494887598bacfc2b244c
- 【Django入門】Djangoアプリの設計哲学！MTVモデルをmodelsを通して学ぼう！
  -  https://www.sejuku.net/blog/27387


## Environment
- windows / powershell。（Ubuntuでの操作の場合は、読み替えてください）

- package environment

```powershell
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
djthird
sandbox

```

## ** Procedure List

### １．virtualenv環境 - pip install

- mkprojectにより、project環境を構築。（virtualenvwrapperを使ってます。condaの場合は、読み替えてください）

```powershell
PS G:\workspace\py> mkproject djfourth
PS G:\workspace\py> workon

Pass a name to activate one of the following virtualenvs:
==============================================================================
djfirst
djfourth
djsecond
djthird
sandbox
PS G:\workspace\py>

```

- $Env:PROJECT_HOME\djfourthフォルダに移動。
- 以下を実行して、activate 

```powershell
PS G:\workplace\py> $p = 'djfourth'
PS G:\workplace\py> cd $Env:WORKON_HOME\$p
PS G:\env\py\djfourth> .\Scripts\activate
(djfourth) PS G:\env\py\djfourth> cd $Env:PROJECT_HOME\$p
(djfourth) PS G:\workplace\py\djfourth>

```

- requirements packages

```powershell
(djfourth) PS G:\workplace\py\djfourth> pip install django
Collecting django
  Using cached https://files.pythonhosted.org/packages/56/0e/afdacb47503b805f3ed213fe732bff05254c8befaa034bbada580be8a0ac/Django-2.0.6-py3-none-any.whl
Collecting pytz (from django)
  Using cached https://files.pythonhosted.org/packages/dc/83/15f7833b70d3e067ca91467ca245bae0f6fe56ddc7451aa0dc5606b120f2/pytz-2018.4-py2.py3-none-any.whl
Installing collected packages: pytz, django
Successfully installed django-2.0.6 pytz-2018.4
(djfourth) PS G:\workplace\py\djfourth> pip freeze
Django==2.0.6
pytz==2018.4
(djfourth) PS G:\workplace\py\djfourth> django-admin --version
2.0.6
```


### ２．Create site
- virtualenvwrapperのmkprojectで作成したproject folderが、 django-admin で生成するフォルダと かぶるので、削除する。
- 以下、Site (project)を作成する。

```powershell
(djfourth) PS G:\workplace\py> django-admin startproject djfourth
(djfourth) PS G:\workplace\py> ls


    Directory: G:\workplace\py


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
d-----        6/15/2018  11:15 PM                djfirst
d-----        6/15/2018  11:17 PM                djfourth
d-----         6/2/2018  12:01 PM                djsecond
d-----        6/15/2018  11:02 PM                djthird
d-----        6/10/2018   4:29 PM                sandbox

(djfourth) PS G:\workplace\py> cd .\djfourth\
(djfourth) PS G:\workplace\py\djfourth> ls


    Directory: G:\workplace\py\djfourth


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
d-----        6/15/2018  11:17 PM                djfourth
-a----        6/15/2018  11:17 PM            555 manage.py
```


- siteを、python manage.py runserverで起動する。
  access : http://127.0.0.1:8000/

```powershell
(djfourth) PS G:\workplace\py\djfourth> python manage.py runserver
```


### ３．Create App
- 簡単なテーブルをを使ったアプリを作成する。

{code}
```powershell
(djfourth) PS G:\workplace\py\djfourth> python manage.py startapp postcodes
(djfourth) PS G:\workplace\py\djfourth> ls


    Directory: G:\workplace\py\djfourth


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
d-----        6/15/2018  11:23 PM                djfourth
d-----        6/15/2018  11:28 PM                postcodes
-a----        6/15/2018  11:23 PM              0 db.sqlite3
-a----        6/15/2018  11:17 PM            555 manage.py
```
{/code}

#### ３．１　Web Siteの設定変更

- 簡単なテンプレートを使ったindex page


- /djfourth/settings.py
```powershell
(djfourth) PS G:\workplace\py\djfourth> sakura .\djfourth\settings.py
```

```python
# Application definition

INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'postcodes',   ##＜＜
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


- /djfourth/urls.py
```powershell
(djfourth) PS G:\workplace\py\djfourth> sakura .\djfourth\urls.py
```

```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('', include('postcodes.urls')),
    path('postcodes/', include('postcodes.urls')),
    path('admin/', admin.site.urls),
]

```


#### ３．２　Web Appの設定変更

- postcodes/views.py
```powershell
(djfourth) PS G:\workplace\py\djfourth> sakura .\postcodes\views.py
```

```python
from django.http.response import HttpResponse
from django.shortcuts import render


def hello(request):
    return render(request,'index.html')

```

- postcodes/urls.py
```powershell
(djfourth) PS G:\workplace\py\djfourth> sakura .\postcodes\urls.py
```

```python
from django.urls import path

from . import views

urlpatterns = [
    path('', views.index, name='index'),
]

```

#### ３．３ Web Appのtemplate

- templates/index.html

```html
<!DOCTYPE html>
<html>
 <head lang="ja">
    <meta charset="UTF-8">
    <title>djfourth</title>
 </head>
 <body>
  <h1>Post Code Home</h1>

    <p>時刻は、{{timestamp}}です。</p>

 </body>
</html>

```


- http://127.0.0.1:8000/postcodes/
```
python manage.py runserver
```

![Imgur](https://i.imgur.com/wvpJ90Q.png)


### ４．データベースを生成する

#### ４．０　管理ユーザ生成 (createsuperuser)

```
(djfourth) PS G:\workplace\py\djfourth> python manage.py createsuperuser
Username (leave blank to use 'sakai'): admin
Email address: sakai.xxxxx@gmail.com
Password:
Password (again):
```

#### ４．１　初期データベース生成（maigrate）
- 管理系のデータベース生成
```powershell
(djfourth) PS G:\workplace\py\djfourth> python manage.py migrate
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
```

- 以下のDefault Web Application用？
  - jango.contrib.admin - 管理（admin）サイト。
  - django.contrib.auth - 認証システム
  - django.contrib.contenttypes - コンテンツタイプフレームワーク
  - django.contrib.sessions - セッションフレームワーク
- なお、[INSTALLED_APPS]には、以下もdefaultで設定がある。
  - django.contrib.messages - メッセージフレームワーク
  - django.contrib.staticfiles - 静的ファイルの管理フレームワーク

```
# Application definition

INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'postcodes',   ## ＜＜
]
```

- Django administration aps
  - http://127.0.0.1:8000/admin/ 

#### ４．２　DB確認
- SQLite3を、dbshellで確認。
- SQLite3を、インストールが必要
   -  https://www.sqlite.org/download.html
```
(djfourth) PS G:\workplace\py\djfourth> python manage.py dbshell
SQLite version 3.24.0 2018-06-04 19:24:41
Enter ".help" for usage hints.
sqlite>
```

or
```
(djfourth) PS G:\workplace\py\djfourth> sqlite3 .\db.sqlite3
SQLite version 3.24.0 2018-06-04 19:24:41
Enter ".help" for usage hints.
```

```
sqlite> .schema
CREATE TABLE IF NOT EXISTS "django_migrations" ("id" integer NOT NULL PRIMARY KEY AUTOINCREMENT, "app" varchar(255) NOT NULL, "name" varchar(255) NOT NULL, "applied" datetime NOT NULL);
CREATE TABLE sqlite_sequence(name,seq);
CREATE TABLE IF NOT EXISTS "auth_group" ("id" integer NOT NULL PRIMARY KEY AUTOINCREMENT, "name" varchar(80) NOT NULL UNIQUE);
CREATE TABLE IF NOT EXISTS "auth_group_permissions" ("id" integer NOT NULL PRIMARY KEY AUTOINCREMENT, "group_id" integer NOT NULL REFERENCES "auth_group" ("id") DEFERRABLE INITIALLY DEFERRED, "permission_id" integer NOT NULL REFERENCES "auth_permission" ("id") DEFERRABLE INITIALLY DEFERRED);
CREATE TABLE IF NOT EXISTS "auth_user_groups" ("id" integer NOT NULL PRIMARY KEY AUTOINCREMENT, "user_id" integer NOT NULL REFERENCES "auth_user" ("id") DEFERRABLE INITIALLY DEFERRED, "group_id" integer NOT NULL REFERENCES "auth_group" ("id") DEFERRABLE INITIALLY DEFERRED);
CREATE TABLE IF NOT EXISTS "auth_user_user_permissions" ("id" integer NOT NULL PRIMARY KEY AUTOINCREMENT, "user_id" integer NOT NULL REFERENCES "auth_user" ("id") DEFERRABLE INITIALLY DEFERRED, "permission_id" integer NOT NULL REFERENCES "auth_permission" ("id") DEFERRABLE INITIALLY DEFERRED);
CREATE UNIQUE INDEX auth_group_permissions_group_id_permission_id_0cd325b0_uniq ON "auth_group_permissions" ("group_id", "permission_id");
CREATE INDEX "auth_group_permissions_group_id_b120cbf9" ON "auth_group_permissions" ("group_id");
CREATE INDEX "auth_group_permissions_permission_id_84c5c92e" ON "auth_group_permissions" ("permission_id");
CREATE UNIQUE INDEX auth_user_groups_user_id_group_id_94350c0c_uniq ON "auth_user_groups" ("user_id", "group_id");
CREATE INDEX "auth_user_groups_user_id_6a12ed8b" ON "auth_user_groups" ("user_id");
CREATE INDEX "auth_user_groups_group_id_97559544" ON "auth_user_groups" ("group_id");
CREATE UNIQUE INDEX auth_user_user_permissions_user_id_permission_id_14a6b632_uniq ON "auth_user_user_permissions" ("user_id", "permission_id");
CREATE INDEX "auth_user_user_permissions_user_id_a95ead1b" ON "auth_user_user_permissions" ("user_id");
CREATE INDEX "auth_user_user_permissions_permission_id_1fbb5f2c" ON "auth_user_user_permissions" ("permission_id");
CREATE TABLE IF NOT EXISTS "django_admin_log" ("id" integer NOT NULL PRIMARY KEY AUTOINCREMENT, "object_id" text NULL, "object_repr" varchar(200) NOT NULL, "action_flag" smallint unsigned NOT NULL, "change_message" text NOT NULL, "content_type_id" integer NULL REFERENCES "django_content_type" ("id") DEFERRABLE INITIALLY DEFERRED, "user_id" integer NOT NULL REFERENCES "auth_user" ("id") DEFERRABLE INITIALLY DEFERRED, "action_time" datetime NOT NULL);
CREATE INDEX "django_admin_log_content_type_id_c4bce8eb" ON "django_admin_log" ("content_type_id");
CREATE INDEX "django_admin_log_user_id_c564eba6" ON "django_admin_log" ("user_id");
CREATE TABLE IF NOT EXISTS "django_content_type" ("id" integer NOT NULL PRIMARY KEY AUTOINCREMENT, "app_label" varchar(100) NOT NULL, "model" varchar(100) NOT NULL);
CREATE UNIQUE INDEX django_content_type_app_label_model_76bd3d3b_uniq ON "django_content_type" ("app_label", "model");
CREATE TABLE IF NOT EXISTS "auth_permission" ("id" integer NOT NULL PRIMARY KEY AUTOINCREMENT, "content_type_id" integer NOT NULL REFERENCES "django_content_type" ("id") DEFERRABLE INITIALLY DEFERRED, "codename" varchar(100) NOT NULL, "name" varchar(255) NOT NULL);
CREATE UNIQUE INDEX auth_permission_content_type_id_codename_01ab375a_uniq ON "auth_permission" ("content_type_id", "codename");
CREATE INDEX "auth_permission_content_type_id_2f476e4b" ON "auth_permission" ("content_type_id");
CREATE TABLE IF NOT EXISTS "auth_user" ("id" integer NOT NULL PRIMARY KEY AUTOINCREMENT, "password" varchar(128) NOT NULL, "last_login" datetime NULL, "is_superuser" bool NOT NULL, "username" varchar(150) NOT NULL UNIQUE, "first_name" varchar(30) NOT NULL, "email" varchar(254) NOT NULL, "is_staff" bool NOT NULL, "is_active" bool NOT NULL, "date_joined" datetime NOT NULL, "last_name" varchar(150) NOT NULL);
CREATE TABLE IF NOT EXISTS "django_session" ("session_key" varchar(40) NOT NULL PRIMARY KEY, "session_data" text NOT NULL, "expire_date" datetime NOT NULL);
CREATE INDEX "django_session_expire_date_a5c62663" ON "django_session" ("expire_date");
```


#### ４．３ モデルを生成
- reference
  - https://docs.djangoproject.com/ja/2.0/intro/tutorial02/

-　郵便番号表テーブルを作る

- postcodes/models.py
```powershell
(djfourth) PS G:\workplace\py\djfourth> sakura .\postcodes\models.py
```
```python
from django.db import models

class PostCode(models.Model):
    #id = AutoField()
    jisx0401 = CharField( max_length='5')
    post_code5 = CharField( max_length='3')
    post_code = CharField( max_length='7', unique=True)
    prefecture_kana = CharField( max_length='30')
    city_kana = CharField( max_length='30')
    town_kana = CharField( max_length='30')
    prefecture = CharField( max_length='30')
    city = CharField( max_length='30')
    town = CharField( max_length='2000')
    flag_1 = CharField( max_length='1', null=True)
    flag_2 = CharField( max_length='1', null=True)
    flag_3 = CharField( max_length='1', null=True)
    flag_4 = CharField( max_length='1', null=True)
    flag_5 = CharField( max_length='1', null=True)
    reason_for_update = CharField( max_length='1', null=True)
```

- djfourth/settings.py
```powershell
(djfourth) PS G:\workplace\py\djfourth> sakura .\postcodes\models.py
```
```python
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'postcodes',   ## ＜＜
]
```

- table migration
```powershell
(djfourth) PS G:\workplace\py\djfourth> sakura .\postcodes\models.py
```

```python
from django.db import models

class PostCode(models.Model):
    # id = # models.AutoField()
    jisx0401 = models.CharField( max_length= 5)
    post_code5 = models.CharField( max_length= 3)
    post_code = models.CharField( max_length= 7, unique=True)
    prefecture_kana = models.CharField( max_length= 30)
    city_kana = models.CharField( max_length= 30)
    town_kana = models.CharField( max_length= 30)
    prefecture = models.CharField( max_length= 30)
    city = models.CharField( max_length= 30)
    town = models.CharField( max_length= 2000)
    flag_1 = models.CharField( max_length= 1, null=True)
    flag_2 = models.CharField( max_length= 1, null=True)
    flag_3 = models.CharField( max_length= 1, null=True)
    flag_4 = models.CharField( max_length= 1, null=True)
    flag_5 = models.CharField( max_length= 1, null=True)
    reason_for_update = models.CharField( max_length= 1, null=True)

```

```powershell
(djfourth) PS G:\workplace\py\djfourth> python manage.py makemigrations postcodes
Migrations for 'postcodes':
  postcodes\migrations\0001_initial.py
    - Create model PostCode
```

```powershell
(djfourth) PS G:\workplace\py\djfourth> python manage.py sqlmigrate postcodes 0001
BEGIN;
--
-- Create model PostCode
--
CREATE TABLE "postcodes_postcode" ("id" integer NOT NULL PRIMARY KEY AUTOINCREMENT, "jisx0401" varchar(5) NOT NULL, "post_code5" varchar(3) NOT NULL, "post_code" varchar(7) NOT NULL UNIQUE, "prefecture_kana" varchar(30) NOT NULL, "city_kana" varchar(30) NOT NULL, "town_kana" varchar(30) NOT NULL, "prefecture" varchar(30) NOT NULL, "city" varchar(30) NOT NULL, "town" varchar(2000) NOT NULL, "flag_1" varchar(1) NULL, "flag_2" varchar(1) NULL, "flag_3" varchar(1) NULL, "flag_4" varchar(1) NULL, "flag_5" varchar(1) NULL, "reason_for_update" varchar(1) NULL);
COMMIT;
```

```powershell
(djfourth) PS G:\workplace\py\djfourth> python manage.py migrate
Operations to perform:
  Apply all migrations: admin, auth, contenttypes, postcodes, sessions
Running migrations:
  Applying postcodes.0001_initial... OK
```

```powershell
(djfourth) PS G:\workplace\py\djfourth> python manage.py shell
:
時間がなくパス
:
```



## ** SUMMARY
- 以下を実施した。
  * -- django install
  * -- Site 作成
  * -- Web app 作成
  * -- DB Modelの追加

// --- end of file

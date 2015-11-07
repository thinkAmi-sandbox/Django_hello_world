# Django_hello_world

以下の内容で作成した、Hello World的なDjangoアプリです。

　  
## 環境

- Windows10
- Python 3.4.3
- Django 1.8.6

　  
## 作成手順
### Django用のディレクトリ作成
```
path\to\root>mkdir Django_hello_world
path\to\root>cd Django_hello_world
```

　  
### Python3.4.3のvirtualenvを作成
```
path\to\root\Django_hello_world>virtualenv env -p c:\python34\python.exe
Already using interpreter c:\python34\python.exe
Using base prefix 'c:\\python34'
New python executable in env\Scripts\python.exe
Installing setuptools, pip, wheel...done.
```

　  
### virtualenvのActivate
```
path\to\root\Django_hello_world>env\Scripts\activate
```

　  
### virtualenvへDjangoをインストール
```
(env) path\to\root\Django_hello_world>pip install django
...
Successfully installed django-1.8.6
```

　  
### `my_project`プロジェクトの作成
```
(env) path\to\root\Django_hello_world>python env\Scripts\django-admin.py startproject my_project
```

　  
### `my_app`アプリの作成
(env) path\to\root\Django_hello_world>cd my_project
(env) path\to\root\Django_hello_world\my_project>python manage.py startapp my_app

　  
### INSTALLED_APPSに`my_app`アプリを追加
###### my_project\my_project\settings.py
```python
...
INSTALLED_APPS = (
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'my_app',    # add
)
...
```

　  
### Modelの作成
###### my_project\my_app\models.py
```python
from django.db import models

class MyModel(models.Model):
	name = models.CharField('my_name', max_length=255)
```

　  
### マイグレーション
```
(env) path\to\root\Django_hello_world\my_project>python manage.py makemigrations my_app
Migrations for 'my_app':
  0001_initial.py:
    - Create model MyModel

(env) path\to\root\Django_hello_world\my_project>python manage.py migrate
...
  Applying sessions.0001_initial... OK
```

　  
### 管理者ページ用設定
#### 管理者ページの対象に、MyModelを追加 
###### my_project\my_app\admin.py

```python
from django.contrib import admin
from my_app.models import MyModel

admin.site.register(MyModel)
```

　  
#### 管理者ユーザ作成
ユーザ名・パスワードとも、`admin`で作成

```
(env) path\to\root\Django_hello_world\my_project>python manage.py createsuperuser
Username (leave blank to use 'user_name'): admin
Email address: admin@example.com
Password:
Password (again):
Superuser created successfully.
```

　  
## 動作確認

```
(env) path\to\root\Django_hello_world\my_project>python manage.py runserver
```

にてDjangoを起動後、

- http://127.0.0.1:8000 にアクセスし、`It worked!`が表示されること
- http://127.0.0.1:8000/admin/ にアクセスし、My_Modelの編集ができること

を確認

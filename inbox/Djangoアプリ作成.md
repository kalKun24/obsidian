## 1. appの作成
``` shell
python3 manage.py startapp {app-name}
```

## 2. urlsへの追加
``` python
from django.contrib import admin

from django.urls import path, include

  

urlpatterns = [

    path('admin/', admin.site.urls),

    path('', include(challenge.urls)) #challengeクラスへのアクセス

]
```

## 3. プロジェクトにアプリを認識させる
``` python
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',

    'challenge.apps.ChallengeConfig', #challngeをプロジェクトに認識させる。

]
```

# Django와 관련된 것들 정리





### python 설치는 했는데 ( cmd / shell ) 등에서 python 명령어가 들지 않을 때

- `python --version`을 아무리 쳐도 Python이라고만 떴다.
- path 설정 오류다.
  - 고급 시스템 설정 > 환경변수 > **시스템변수**에서 **path**선택 > python의 올바른 설치 경로를 등록해준다.
  - `C:\Users\OWNER\AppData\Local\Programs\Python\Python39` : 나는 Local이 아닌 Roaming의 하위 폴더에 있는 경로로 잘못 설정해주어서 오류가 생겼다.
  - `C:\Users\OWNER\AppData\Local\Programs\Python\Python39\Scripts` : pip과 같은 명령어를 사용하기 위해서는 이것도 등록해줘야 한다고 한다.





### Django를 설치하는 순서

- `$ python -m pip install --upgrade pip` : Django를 설치하는 데 필요한 pip을 최신 버전으로 업그레이드 한다. 사실, Django를 먼저 설치했을 때, pip의 업데이트가 필요하면 `Warning`으로 업데이트 하라고 명령어까지 친절하게 알려준다.
- `$ python -m pip install Django` : Django 설치





### 프로젝트 만들기

- 프레임워크다 보니 프로젝트를 생성할 때, 여러개의 옵션이나 설정들이 자동으로 결정되므로, 프로젝트를 진행할 폴더에 진입하여 프로젝트를 생성해야 한다.

- `$ django-admin startproject hello` : 생각해보니 저 django라는 명령어가 shell에서 듣지를 않아서 `cmd`에서 했던 것 같다. 다시 확인해봐야겠다ㅠㅠ

  - hello 프로젝트 안에 hello라는 동일한 이름의 폴더가 생긴다. 이 안에 설정파일이 많다

  - manage.py가 중요한 역할을 한다.

  - ```
    hello
        ├── hello
        |       __init__.py
        |       asgi.py
        |       settings.py
        |       urls.py
        |       wsgi.py
        ├── manage.py
    ```





### 프로젝트 안에 애플리케이션 만들기

- `$ python manage.py startapp hello_app` : hello_app이라는 애플리케이션을 생성

- ```
  hello (project)
      ├── **hello**
      |       __init__.py
      |       asgi.py
      |       settings.py
      |       urls.py
      |       wsgi.py
      ├── **hello_app**
      |			├── **migrations**
      |			|          __init__.py
      |       __init__.py
      |       admin.py
      |       apps.py
      |       models.py
      |       tests.py
      |       views.py
      |       urls.py (이건 내가 추가한 파일)
      ├── manage.py
  ```

- `hello/settings.py` 파일에서 INSTALLED_APPS에 새롭게 만든 앱을 추가합니다.

- ```
  INSTALLED_APPS = [
      'django.contrib.admin',
      'django.contrib.auth',
      'django.contrib.contenttypes',
      'django.contrib.sessions',
      'django.contrib.messages',
      'django.contrib.staticfiles',
      'hello_app',
  ]
  ```





### 웹서버 실행

- `$ python manage.py runserver` : 서버가 실행 됨
- `Ctrl` + `C` : 서버 실행 종료





### 기억할 소스코드

1. `hello/urls.py`

   ```python
   # app별로 urls.py를 만들어서 각 앱에서 요청이 들어오면 어디로 이어줄지 path를 정해줬다.
   # 그런데 app이 여러개라면 여기서 설정한다
   from django.contrib import admin
   from django.urls import include, path
   
   # hello라고 요청이 들어오면, hello_app 패키지에 urls모듈이 실행되도록 해라
   urlpatterns = [
       path('hello/', include('hello_app.urls')),
       path('admin/', admin.site.urls),
   ]
   ```

2. `hello_app/urls.py`

   ```python
   from django.urls import path
   
   from . import views
   
   # hello_app에서 요청이 들어왔을때
   # path에 아무것도 안들어왔다면, views의 index를 줘라
   urlpatterns = [
       path('', views.index, name='index'),
   ]
   ```

3. `hello_app/models.py` : entity 역할
4. `hello_app/views.py` : controller 역할
5. `app`을 생성할 때마다 `hello/settings.py`의 `INSTALLED_APPS`에 새롭게 만든 앱을 추가
6. `hello_app` 하위에 `/templates/~.html` 이렇게 만들어서 view 역할을 하게 하자
7. `urls.py` : request 들어오는 요청 url별로 views.py의 함수 mapping 추가





### 순서

1. `localhost:8000/hello`라고 요청이 들어오면, `hello/urls.py`에서 mapping 한다. hello라고 요청이 들어오면, hello_app 패키지에 urls 모듈이 실행되도록 한다.

   ```python
   # app별로 urls.py를 만들어서 각 앱에서 요청이 들어오면 어디로 이어줄지 path를 정해줬다.
   # 그런데 app이 여러개라면 여기서 설정한다
   from django.contrib import admin
   from django.urls import include, path
   
   # hello라고 요청이 들어오면, hello_app 패키지에 urls모듈이 실행되도록 해라
   urlpatterns = [
       path('hello/', include('hello_app.urls')),
       path('admin/', admin.site.urls),
   ]
   ```

2. `hello_app/urls.py`에서 더 이상의 `path`가 들어오지 않았다면, `hello_app/views.py`의 `index`를 호출한다.

   ```python
   from django.urls import path
   
   from . import views
   
   # hello_app에서 요청이 들어왔을때
   # path에 아무것도 안들어왔다면, views의 index를 줘라
   urlpatterns = [
       path('', views.index, name='index'),
   ]
   ```

3. `hello_app/views.py`의 `index`에서 해당 내용을 브라우저에 `response`한다.

   ```python
   from django.shortcuts import render
   
   # Create your views here.
   # controller 역할
   
   from django.http import HttpResponse
   
   def index(request):
       return HttpResponse("Hello, world. You're at the Hello Django App index.")
   ```

   
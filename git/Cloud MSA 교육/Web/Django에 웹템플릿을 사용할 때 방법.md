# Django에 웹템플릿을 적용할 때

##### 참고사이트

1. https://rednooby.tistory.com/105

2. https://tunghs.github.io/2019/09/07/2019-09-07-Apply-Django-Bootstrap/

3. https://www.inflearn.com/questions/32484

   `{%load statifciles%}`는 Django 3.0부터는 사용하지 않는다. `{%load static%}`를 이용하면 된다.



##### 순서

1. `django-admin startproject Diary`
2. `cd Diary`
3. `python manage.py startapp diary_app`
4. 프로젝트 `settings.py`에서 `INSTALLED_APPS`에 `diary_app`을 등록
5. 프로젝트 `urls.py`와 애플리케이션 `urls.py`는 별개다. 애플리케이션 폴더에 `urls.py`를 생성해준다.
   - 프로젝트 `urls.py`에서는 브라우저에서 요청이 들어오면 어디 애플리케이션으로 향할지 설정해준다.
   - 애플리케이션 `urls.py`에서는 요청에따라 어떠한 서비스를 실행할지 연결해준다.
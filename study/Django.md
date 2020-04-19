# Django

#### MVT패턴





#### 장고 설치

```
pip install django
```





#### 프로젝트 생성

##### 프로젝트 생성

```
$ django-admin startproject 프로젝트이름
```

##### app 생성

```
$ ./menage.py startapp app이름
```

##### 

#### 프로젝트에 생성된 파일

##### settings.py

:프로젝트 관련 설정 파일

- DEBUG
  - True: 개발할때
  - False: 배포할때는
- INSTALLED_APPS
  - 서드파일 어플리케이션 사용
  - 
- MIDDELWQRE_CLASSES
- TEMPLATES
  - template와 관련된 설정
- DATABASE
- STATIC_URL 

```

```





##### manage.py

- 프로젝트 관리 명령어 모음
- 생성, 인증 관련
- 주요 명령어
  - startapp: 앱생성
  - runserver: 서버실행  ex)./manage.py runserver 0.0.0.0:8080
  - createsuperuser: 관리자 생성
  - makemigrations app이름: app에 변화가 있는지 확인
  - migrate : 모델 변경 사항 디비에 저장
  - shell
  - collectstatic: static 파일 한곳에 모음



##### models.py

```python
from django.db import models

class Article(models.Model)
	name = ;
```





##### urls.py

외부에서 접근할 url관리

```python
urlpatterns = [
    url(r'^write/',write, name ='wirte') //주소, 함수,이름 
]
```



##### view.py

```python
from django.shortcuts import render
from community.forms import *

def write(request):
    if request.method == 'POST':
        form = Form(request.POST)
        if form.is_valid():
            form.save()	// 폼을 그대로 db에 저장, 변수랑 sql작성할 필요 없음
    else:
    	form = Form()
    return render(request,'write.html',{'form':form}) //렌더해서 wirte.html로 보냄
```



###### template/write.html

```html
<body>
    <form>
        {{form.as_p}} //p태그로 폼 만듦
        {%csrf_token%} //에러 안나게 하려면 이거 추가
        <button>
    </form>
</body>
```


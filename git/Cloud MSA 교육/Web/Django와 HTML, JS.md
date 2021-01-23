# Django와 HTML, JS



#### 질문

```html
<div class="row">
   {% for story in stories %}
      <div class="col-4 col-6-medium col-12-small">
         <a href="#story" class="image fit" onclick="myFunction({{story.id}}, '{{story.story_date}}', '{{story.story_keyword}}', '{{story.story_title}}', '{{story.story_content}}');"><img src="/static/images/pic01.jpg" alt=""></a>
      </div>
   {% endfor %}
</div>
```

선생님, 제가 위와 같은 코드를 가지고 있습니다.
그런데 story.story_content에서 내용물에 작은따옴표를 가지고 있는 문자열이 있으면 문제가 생깁니다.
그래서
var tmp = story.story_content
tmp.replace("'", "\'")
이런것처럼 story.story_content를 특정 변수에 할당하고, 그 변수를 replace("'", "\'")를 사용해서 내용물을 바꿔준 후, 파라미터에 해당 변수(tmp)를 넣고 싶습니다.
그런데 어떻게 해야 할지 모르겠습니다ㅠㅠ 



#### 해결

```html
<div class="row">
   {% for story in stories %}
      <div class="col-4 col-6-medium col-12-small">
      <script>
         var tmp = "{{story.story_content|safe}}";
         tmp = tmp.replace("'", "\'");
      </script>
         <a href="#story" class="image fit" onclick="myFunction({{story.id}}, '{{story.story_date}}', '{{story.story_keyword}}', '{{story.story_title}}', tmp);"><img src="/static/images/pic01.jpg" alt=""></a>
      </div>
   {% endfor %}
</div>
```

저거 그냥 script에서 처리하고, 아래처럼 처리해줬는데 된다
미쳤다 카타르시스



#### <%%> 사용

```html
<%@ page language="java" contentType="text/html; charset=UTF-8" pageEncoding="UTF-8"%>
```

예전에 기억하던 <%%> 이 문법은 jsp 페이지에서 java를 사용할 때 쓰던것이다.
페이지 가장 상단에 아래와 같은 코드를 붙여 사용했다.
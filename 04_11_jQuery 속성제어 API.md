### DOM
## jQuery 속성제어 API
- Element의 API 기능을 jQuery에서는 어떻게 구사하는지 알아보자


## 속성제어
- jQuery 객체 메소드
  - setAttribute, getAttribute == attr
  - removeAttribute == removeAttr
```
<a id="target" href="http://opentutorials.org">opentutorials</a>

<script src="//code.jquery.com/jquery-1.11.0.min.js"></script>
<script>
  var t = $('#target');
  console.log(t.attr('href'));  // http://opentutorials.org
  
  // title 속성의 값을 설정
  t.attr('title', 'opentutorials.org'); 

  // title 속성을 제거 
  t.removeAttr('title');
</script>
```
> $('#target')는 jQuery객체를 리턴하므로, '$'로 감싸지않고 바로 jQuery함수 사용이 가능

> var ex = $('~'); 에서 a는 jQuery객체를 리턴(유사배열)한다. 리턴한 객체의 요소 즉, ex[0] 와 같은 것들이 DOM 객체가 된다.


## attribute 와 property
- DOM과 마찬가지로 jQuery도 속성과 프로퍼티를 구분함
- 속성방식 : attr \/ 프로퍼티 방식 : prop
```
현재 문서의 URL이 http://localhost/jQuery_attribute_api/demo2.html 일때

<a id="t1" href="./demo.html">opentutorials</a>

<script src="//code.jquery.com/jquery-1.11.0.min.js"></script>
<script>
  var t1 = $('#t1');
  console.log(t1.attr('href')); // ./demo.html 
  console.log(t1.prop('href')); // http://localhost/jQuery_attribute_api/demo.html 
</script>
```

```
<input id="t2" type="checkbox" checked="checked" />

<script src="//code.jquery.com/jquery-1.11.0.min.js"></script>
<script>
  var t2 = $('#t2');
  console.log(t2.attr('checked'));  // checked
  console.log(t2.prop('checked'));  // true
</script>
```

- jQuery를 이용하면 프로퍼티의 이름으로 html 속성의 이름과 다른 이름을 사용해도 올바른 것으로 교정해줌
- 이러한 점이 라이브러리를 사용하는 의의
```
<div id="t1">opentutorials</div>
<div id="t2">opentutorials</div>

<script src="//code.jquery.com/jquery-1.11.0.min.js"></script>
<script>
  $('#t1').prop('className', 'important');  // 프로퍼티 이름
  $('#t2').prop('class', 'current');  // HTML 속성 이름
</script>
```
> 둘다 실행가능

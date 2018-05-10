### DOM
## jQuery
- jQuery는 DOM을 내부에 감추고 보다 __쉽게__ 웹페이지를 조작할 수 있도록 돕는 도구
  - HTMLElement(DOM)은 브라우저에 원래 있는 기능이고 jquery는 이 기능을 이용해 좀 더 쉽게 브라우저를 제어할 방법을 제공
- javascript의 라이브러리
  - 라이브러리 : 자주 사용하는 로직을 효율적으로 재사용할 수 있도록 고안된 소프트웨어


## jQuery의 사용
- jQuery를 사용하기 위해서는 jQuery를 HTML로 로드해야 함
```
<script src="http://code.jquery.com/jquery-3.3.1.min.js"></script>
```
> 다운받아 사용하는 방법과 위와같이 스크립트 태그를 이용하는 방법 두가지가 있다.
```
<script>
  jQuery(document).ready(function($){
    $('body').prepend('<h1>Hello world</h1>');
  });
</script>
```
> 인자의 h1태그가 body태그 아래에 추가됨
- `prepend() : $('선택')한 태그 바로 아래에 인자의 태그를 추가시킴`
- jQuery(document).ready(function($){}); == $(document).ready(function(){});

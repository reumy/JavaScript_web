### 이벤트
## jQuery 이벤트
-  직접 이벤트 프로그래밍을 하는 것보다 jQuery를 이용하면 더욱 편리함
```
<input type="button" id="pure" value="pure" />
<input type="button" id="jquery" value="jQuery" />

<script src="//code.jquery.com/jquery-1.11.0.min.js"></script>
```
- 순수하게 구현
```
var target = document.getElementById('pure');

if(target.addEventListener){
  target.addEventListener('click', function(event){
    alert('pure');
  });
} else {
  target.attachEvent('onclick', function(event){
    alert('pure');
  });
}
```
> addEventListener의 유무에 따른 기능테스트(ie 하위버전)가 들어가면서 코드가 길어짐

- jQuery 사용
```
$('#jquery').on('click', function(event){
  alert('jQuery');
});
```
> 코드 분량에 큰차이가 있고 jQuery는 크로스브라우징을 알아서 처리해준다.<br/>즉, 순수하게 구현한 코드는 ie 오래된 버전에서 지원X \/ jQuery를 이용한 코드는 ie 버전에서 지원O

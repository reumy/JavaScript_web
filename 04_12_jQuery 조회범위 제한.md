### DOM
## jQuery 조회 범위 제한
- Element 객체에서 getElementsBy* 메소드를 이용해 조회범위를 그 객체의 하위엘리먼트로 제한했던 기능을 jQuery 알아보자.


## selector context
- jQuery에서의 제한된 범위를 말함
- 조회할 때 조회 범위를 제한하는것이 가장 간편한 방법
```
<ul>
  <li class="marked">html</li>
  <li>css</li>
  <li id="active">JavaScript
    <ul>
      <li>JavaScript Core</li>
      <li class="marked">DOM</li>
      <li class="marked">BOM</li>
    </ul>
  </li>
</ul>

<script src="//code.jquery.com/jquery-1.11.0.min.js"></script>
<script>
  $( ".marked", "#active").css( "background-color", "red" );
  $( "#active .marked").css( "background-color", "red" );
</script>
```
- 결과
```
<li class="marked" style="background-color: red;">DOM</li>
<li class="marked" style="background-color: red;">BOM</li>
```
> 두 코드의 실행결과는 같다.

```
$( "효과를 주고자하는 element", "selector context")
```
> 여기에서 selector context는 첫번째인자에 해당되는 셀렉터를 제어하려고하는 엘리먼트의 선택자가 됨


## .find()
- 인자로 전달된 선택자에 해당되는 엘리먼트들만 찾음
- find가 적용된 해당 객체의 하위 객체에서만 불러옴
- 체인을 끊지 않고 작업의 대상을 변경하고 싶을 때 사용
  - 단, find를 너무 복잡하게 사용하면 코드를 유지보수하기 어려움
```
$( "#active").find('.marked').css( "background-color", "red" );
```
> 위 예제와 같은 결과
```
$('#active').css('color','blue').find('.marked').css( "background-color", "red" );
```
> 체인
- 결과
```
<li id="active" style="color: blue;">JavaScript
  <ul>
    <li>JavaScript Core</li>
    <li class="marked" style="background-color: red;">DOM</li>
    <li class="marked" style="background-color: red;">BOM</li>
  </ul>
</li>
```
> active 하위 엘리먼트들도 전부 글씨가 파란색이 됨<br/>이유는 css의 color속성은 상속이 되기때문에 하위 엘리먼트도 적용됨

- 더 많은 예제는 [.find()](https://api.jquery.com/find/) 참고

### 이벤트 - jQuery 이벤트
## [on](http://api.jquery.com/on/) API
- on은 jQuery에서 가장 중요하고 자유도가 높은 이벤트 API
- `.on(events [, selector ] [, data ], handler(eventObject))`
  - event : 등록하고자 하는 이벤트 타입을 지정한다. (예: "click")
  - selector : 이벤트가 설치된 엘리먼트의 하위 엘리먼트를 이벤트 대상으로 필터링함
  - data : 이벤트가 실행될 때 핸들러로 전달될 데이터를 설정함
  - handler : 이벤트 핸들러 함수
  - [ ~ ] : 생략가능


## selector
- selector 파라미터는 이벤트 대상을 필터링함
```
<ul>
  <li><a href="#">HTML</a></li>
  <li><a href="#">CSS</a></li>
  <li><a href="#">JavaScript</a></li>
</ul>

<script src="//code.jquery.com/jquery-1.11.0.min.js"></script>
<script>
  $('ul').on('click','a, li', function(event){
    console.log(this.tagName);
  })
</script>
```
- 결과
```
A
LI
```
>  ul 엘리먼트의 하위 엘리먼트 중에  a, li 엘리먼트들에 대해서만 이벤트가 발생한다.<br/>주의 할 것은 ul 엘리먼트는 이벤트가 발생하지 않는다는 점이다.<br/>이것은 jQuery에서 이벤트 버블링을 구현하는 방법이기도 하다.

> 여기에서 this는 이벤트를 필터링하고있는 a, li를 가르킴

### late binding
- 존재하지 않는 엘리먼트에도 이벤트를 등록할 수 있음
```
<body>
  <script src="//code.jquery.com/jquery-1.11.0.min.js"></script>
  <script>
    $('ul').on('click','a, li', function(event){
      console.log(this.tagName);
    })
  </script>

  <ul>
    <li><a href="#">HTML</a></li>
    <li><a href="#">CSS</a></li>
    <li><a href="#">JavaScript</a></li>
  </ul>
</body>
```
> 실행X<br/>script가 ul보다 먼저 위치해서 ul 엘리먼트가 존재하지않을 때 이벤트 설치를 시도하고 있기 때문

```
$('body').on('click','a, li', function(event){
  console.log(this.tagName);
})
```
> 실행O<br/>body는 script보다 위에 위치하기 때문에 일단 설치가 가능하다.<br/>그래서 body태그 하위에 현재는 존재하지 않고 나중에 나올 엘리먼트에게도 이벤트를 추후로 장착할 수 있다.


## 다중 바인딩
- 하나의 엘리먼트에 여러개의 이벤트 타입을 동시에 등록하는 방법
```
<input type="text" id="target" />
<p id="status"></p>
```
```
$('#target').on('focus blur', function(e){
  $('#status').html(e.type);
})
```
> 한번에 여러개의 이벤트 타입을 선택해 동일한 이벤트 핸들러를 연결

```
var handler = function(e){
  $('#status').html(e.type);
}

$('#target').on(
  {
  'focus' : handler, 
  'blur' : handler
  }
)
```
> 이벤트에 따라 각각 다른 핸들러를 실행하고 싶을때
```
var handler = function(e){
  $('#status').html(e.type);
}
$('#target').on('focus', handler).on('blur', handler);
```
> 체인링을 이용한 동일 코드

(결과 [실행](http://output.jsbin.com/tatuf/1/))


## 이벤트 제거
- 이벤트를 제거할 때는 off를 사용
```
<input type="text" id="target"></textarea>
<input id="remove"  type="button" value="remove" />
<p id="status"></p>

<script src="//code.jquery.com/jquery-1.11.0.min.js"></script>
<script>
  var handler = function(e){
    $('#status').text(e.type+Math.random());  // (1)
  };

  $('#target').on('focus blur', handler);
  $('#target').on('focus', function(e){
    alert(1);
  });
</script>
```
> (1)은 단순히 실행유무를 눈으로 판단하기위한 코드

- focus 이벤트 모두제거
```
$('#remove').on('click' , function(e){
  $('#target').off('focus');
});
```
> handler기능과 alert기능이 모두 삭제됨

- focus 이벤트 중에 handler 기능을 가진 이벤트만 제거
```
$('#target').off('focus', handler);
```
> handler기능은 제거되고 alert기능은 정상동작함

- 모두 제거
```
$('#target').off('focus blur', handler);
```
> 이벤트타입이 focus와 blur인 이벤트 모두 제거됨

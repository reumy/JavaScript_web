### 이벤트 등록방법
## addEventListener()
- 이벤트를 등록하는 가장 권장되는 방식
- 여러개의 이벤트 핸들러를 등록할 수 있음
- addEventListener(event type, event handler)

```
<input type="button" id="target" value="button" />

<script>
  var t = document.getElementById('target');
  t.addEventListener('click', function(event){
    alert('Hello world, '+event.target.value);
  });
</script>
```
- attachEvent : ie8 이하에서 사용
```
var t = document.getElementById('target');
if(t.addEventListener){
  t.addEventListener('click', function(event){
    alert('Hello world, '+event.target.value);
  }); 
} else if(t.attachEvent){
  t.attachEvent('onclick', function(event){
    alert('Hello world, '+event.target.value);
  })
}
```
> addEventListener이 안될경우 attachEvent를 사용한다.<br/>attachEvent일때는 click을 onclick처럼 on_접미사를 붙여서 사용해야함

- 하나의 이벤트 대상에 복수의 동일 이벤트 타입 리스너를 등록
```
<input type="button" id="target" value="button" />

<script>
  var t = document.getElementById('target');
  t.addEventListener('click', function(event){
    alert(1);
  });
  t.addEventListener('click', function(event){
    alert(2);
  });
</script>
```
> 알림창이 1, 2 순차적으로 두 번 실행된다.<br/>동일한 이벤트에 프로퍼티 리스너방식이라면 단 하나의 이벤트핸들러만을 설치할 수 있기때문에 마지막 이벤트만 실행된다.

- 이벤트 객체를 이용하면 복수의 엘리먼트에 하나의 리스너를 등록해서 재사용할 수 있음
```
<input type="button" id="target1" value="button1" />
<input type="button" id="target2" value="button2" />

<script>
  var t1 = document.getElementById('target1');
  var t2 = document.getElementById('target2');

  function btn_listener(event){
    switch(event.target.id){
      case 'target1':
        alert(1);
        break;
      case 'target2':
        alert(2);
        break;
    }
  }

  t1.addEventListener('click', btn_listener);
  t2.addEventListener('click', btn_listener);
</script>
```
> 클릭한 이벤트 객체의 id가 target1 이면 1을 띄운 알림창을 실행 후 종료<br/>id가 target2 이면 2를 띄운 알림창을 실행 후 종료

- `switch : if문과 비슷한 함수`
- `event.target.id : 어디에서 호출되었는지 그리고 그 id를 알아냄`<br/>하나의 함수에서 동작할 때는 어디에서 발생한 것인지 확인해야 함

- 위 예제 t1.addEventListener('click', btn_listener) 에서 두번째 인자에 괄호가 빠진 이유
> function btn_listener(event){} == var btn_listener = function(event){}로 btn_listener 는 함수객체 자체를 의미한다.<br/>즉, addEventListener는 두번째 인자로 함수객체를 받아야 하는데 btn_listener()를 지정하면 btn_listener라는 함수의 실행결과를 인자로 넘기는 셈이므로 btn_listener를 인자로 지정해야 함수객체를 그대로 넘기게 된다.

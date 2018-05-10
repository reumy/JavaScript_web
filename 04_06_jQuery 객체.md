### DOM
## jQuery 객체
- jQuery 함수의 리턴값
- jQuery 함수를 이용해 선택한 엘리먼트들에 대해 처리할 작업을 프로퍼티로 가지고 있는 객체
```
<ul>
  <li>HTML</li>
  <li>CSS</li>
  <li>JavaScript</li>
</ul>

<script>
  var li = $('li');
</script>
```
- 결과
```
[<li>HTML</li>, <li>CSS</li>, <li>JavaScript</li>]
```
> $('li')는 jQuery 함수(function)이고, 반환되는 li는 jQuery 객체(Object)이다.


## 암시적 반복
- jQuery 객체의 가장 중요한 특성
- DOM과 다르게 jQuery 객체의 메소드를 실행하면 선택된 엘리먼트 전체에 대해서 동시에 작업이 처리됨<br/>즉, 반복문을 사용하지 않고도 반복이 된 결과를 가져옴
- 암시적 반복은 값을 설정할 때만 동작
```
<ul>
  <li>HTML</li>
  <li>CSS</li>
  <li>JavaScript</li>
</ul>

<script>
  var li = $('li');
  li.css('text-decoration', 'underline');  // (1)
  li.css('text-decoration');  // underline (2)
</script>
```
> (1) 내부적으로 li 태그를 순회하면서 모든 li에 underline 속성을 지정함(암시적 반복 - 값을 설정할 때만 동작)<br/>(2) text-decoration이 적용된 첫번째 태그만 가져옴<br/>  즉, 첫번째 li에 underline이 있는경우 underline으로 조회(값을 가져올 때는 선택된 엘리먼트 중 첫번째에있는 값만을 반환)

### jQuery 문법상 인자의 갯수
- 인자가 2개 : (효과, 값) 효과에 값을 준다. 설정
- 인자가 1개 : 효과의 값을 가져온다. 가져오기<br/>값을 가져올때는 선택된 엘리먼트 중 첫번째에대한 값만을 반환


## 체이닝(chainig)
- 선택된 엘리먼트에 대해서 연속적으로 작업을 처리할 수 있는 방법
```
li.css('text-decoration', 'underline').css('color','blue');
```
> .css().css()


## 엘리먼트 정보조회
- jQuery 객체에는 조회된 엘리먼트가 담겨있음
- jQuery 객체는 유사배열 형태로 조회된 엘리먼트를 가지고 있어서 배열처럼 사용해 엘리먼트를 가져올 수 있음
  - 즉, $('')[index]로 특정 위치의 요소를 가져올 수 있지만, 이렇게 가져온 객체는 jQuery객체가 아니기 때문에 eq()메소드를 사용함
```
<ul>
  <li>html</li>
  <li>css</li>
  <li>JavaScript</li>
</ul>

<script src="http://code.jquery.com/jquery-3.3.1.min.js"></script>
<script>
  console.log($('li').length);  // 3
  console.log($('li')[0]);  // <li>html</li>
  
  var li = $('li');
  for(var i=0; i<li.length; i++){
    console.log(li[i]);  // [<li>html</li>, <li>css</li>, <li>JavaScript</li>]
  }
</script>
```
- 주의할 것은 li[i]의 값은 해당 엘리먼트에 대한 jQuery 객체가 아니라 DOM 객체라는 것이다.
```
for(var i=0; i<li.length; i++){
  console.log(li[i].constructor);
}
```
- 결과
```
function HTMLLIElement(){[native code]}
function HTMLLIElement(){[native code]}
function HTMLLIElement(){[native code]}
```
> 각각의 객체는 HTMLLIElement 즉, DOM객체이므로 jQuery 객체가 아니다.<br/>따라서 jQuery의 기능을 이용해서 이 객체를 제어하려면 jQuery 함수를 이용해야 한다.
```
for(var i=0; i<li.length; i++){
  li[i].css('color', 'red');  // 실행X
  $(li[i]).css('color', 'red');  // 실행O
}
```
> li[i]인 DOM 객체를 jQuery 함수로 감싸서 $(li[i]) jQuery객체를 만들면 jQeury로 제어가 가능하다.

- jQuery 객체로 바꾸기
  - jQuery 함수의 인자로 전달 : $( li[i] )
```
var li = $('li');

for(var i=0; i<li.length; i++){
  console.log(li[i].constructor);
}
```
- 결과
```
function HTMLLIElement(){[native code]}
function HTMLLIElement(){[native code]}
function HTMLLIElement(){[native code]}
```
> DOM 객체 리턴
```
$('li')
```
- 결과
```
[li, li, li]
```
> jQuery 객체 리턴

- 해석<br/>jQuery를 담은 변수는 jQeury가 아닌 DOM이다. 그러나 jQuery Object가 유사배열을 가지고 있을 경우 그 유사배열의 한 객체가 DOM Object인 것이다.<br/>즉, var li = $('li'); 일때, li는 jQuery object이고 li[0], li[1], li[2] ...는 DOM object 인 것이다.<br/>그래서 li[1]에 jQuery 함수(.css , .attr 과 같은 함수)를 쓰고 싶으면 $()로 감싸주어야 jQuery 함수를 사용가능한 것이다.<br/>그러나 li자체를 사용할때는 jQuery객체이므로 '$'로 감싸줄 필요없이 바로 사용가능하다. `ex) li.attr();`


## .map()
- 조회된 결과 열람
- .map(function(index, elem){})
  - index : element의 index 전달
  - elem : DOM 객체 전달
- map은 jQuery 객체의 엘리먼트를 하나씩 순회하면서 첫번째 인자로 전달된 함수가 호출 됨
```
<ul>
  <li>html</li>
  <li>css</li>
  <li>JavaScript</li>
</ul>

<script src="http://code.jquery.com/jquery-3.3.1.min.js"></script>
<script>
  var li = $('li');
  li.map(function(index, elem){
    console.log(index, elem);
    $(elem).css('color', 'red');
  });
</script>
```
- 결과
```
0 <li>html</li>
1 <li>css</li>
2 <li>JavaScript</li>

그리고, 모든 li에 red가 적용됨
```
> 0,1,2 : element(index) \/ li : DOM Object(elem)<br/>DOM 객체를 jQuery($) 형식으로 감싸서 사용함

- [참고](https://api.jquery.com/map/)


## jQuery 객체 API
- 제어할 대상을 선택한 후에는 대상에 대한 연산을 해야함
- .css와 .attr은 jQuery 객체가 가지고있는 메소드인데, jQuery는 그 외에도 많은 API를 제공하고 있음
- [jQuery API](https://api.jquery.com/)
- 모든 API를 익힐수는 없고, 중요하고 반복적을 사용되는 API를 보면서 사용법을 익혀야함

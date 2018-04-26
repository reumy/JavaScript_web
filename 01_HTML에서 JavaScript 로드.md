### HTML에서 JavaScript 로드
## inline
- 태그에 직접 자바스크립트를 기술하는 방식
  - 장점 : 태그에 연관된 스크립트가 분명하게 드러남
  - 단점 : 정보(html)와 제어(js)가 섞여 있기 때문에 정보로서의 가치가 떨어짐<br/>유지보수의 어려움
```
<input type="button" onclick="alert('Hello world')" value="Hello world" />
```


## script
- <script></script> 태그 안에 자바스크립트 코드를 삽입하는 방식
  - 장점 : html 태그와 js 코드를 분리할 수 있음
- <script type="text/javascript">의 type은 HTML5 부터 생략가능
```
<input type="button" id="hw" value="Hello world" />

<script type="text/javascript">
  var hw = document.getElementById('hw');
  hw.addEventListener('click', function(){
    alert('Hello world');
  })
</script>
```


## 외부파일로 분리
- js를 별도의 파일로 분리하는 방식
  - 장점 : 보다 엄격하게 정보(html)와 제어(js)를 분리할 수 있음<br/>하나의 js 파일로 여러 웹페이지에서 로드함으로 재활용성을 높임<br/>클라이언트와 서버간의 속도향상과 HTML의 용량 경량화
```
<input type="button" id="hw" value="Hello world" />

<script type="text/javascript" src="script01.js"></script>
```
- script01.js
```
var hw = document.getElementById('hw');
hw.addEventListener('click', function(){
  alert('Hello world');
})
```


## script 파일의 위치
- script를 head 태그에 위치시킬 수도 있음
  - 단점 : 오류의 위험
```
<!DOCTYPE html>
<html>
<head>
  <script src="script01.js"></script>
</head>
<body>
  <input type="button" id="hw" value="Hello world" />
</body>
</html>
```
> html 보다 js를 먼저 읽어서 id=hw를 인식못하기 때문에 오류가 남 js코드에 window.onload를 이용해 오류해결
- script01.js
```
window.onload = function(){
  var hw = document.getElementById('hw');
  hw.addEventListener('click', function(){
    alert('Hello world');
  })
}
```
> `window.onload = function(){} : 웹브라우저의 모든 구성요소에 대한 로드가 끝났을 때 브라우저에 의해서 호출되는 함수`
- TIP : 이러한 이유와 속도향상의 이유로 script 파일은 head 태그 보다 __body태그가 끝나는 하단에 위치__시키는 것이 더 좋다. 

### DOM
## Node 관계 API
- Node 객체는 Node 간의 관계 정보를 담고 있는 일련의 API를 가지고 있음

  - Node.childNodes : 자식노드들을 유사배열에 담아서 리턴
  - Node.firstChild : 첫번째 자식노드
  - Node.lastChild : 마지막 자식노드
  - Node.nextSibling : 다음 형제 노드
  - Node.previousSibling : 이전 형제 노드
  - Node.parentNode : 부모 객체 반환
  
```
<body id="start">
  <ul>
    <li><a href="./532">html</a></li> 
    <li><a href="./533">css</a></li>
    <li><a href="./534">JavaScript</a>
      <ul>
        <li><a href="./535">JavaScript Core</a></li>
        <li><a href="./536">DOM</a></li>
        <li><a href="./537">BOM</a></li>
      </ul>
    </li>
  </ul>

  <script>
    var s = document.getElementById('start');
    console.log(s.firstChild);  // #text

    var ul = s.firstChild.nextSibling
    console.log(ul);  // ul
    console.log(ul.nextSibling);  // #text
    console.log(ul.nextSibling.nextSibling);  // script
    console.log(ul.childNodes);  //text, li, text, li, text, li, text
    console.log(ul.childNodes[1]);  // li(html)
    console.log(ul.parentNode);  // body
  </script>
</body>
```
> 줄바꿈과 같은 공백도 text라는 노드로 인식함
```
for(var i = 0; i<start.childNodes.length;i++){
  start.childNodes[i].style.color = 'red';
};
```
> 중간에 공백의 text Node 때문에 오류

- 해결
```
for(var i = 0; i<start.childNodes.length;i++){
  if(start.childNodes[i].style)
  start.childNodes[i].style.color = 'red';
};
```
> 스타일이 가능한지를 확인 후 적용

- 빈 text노드 거르는 프로퍼티
```
firstElementChild
lastElementChild
nextElementSibling
previousElementSibling
...
```

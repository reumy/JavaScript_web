### DOM
## 노드 추가 API
- [appendChild(child)](https://developer.mozilla.org/en-US/docs/Web/API/Node/appendChild) : 노드의 마지막 자식으로 주어진 엘리먼트 추가
- [insertBefore(newElement, referenceElement)](https://developer.mozilla.org/en-US/docs/Web/API/Node/insertBefore) : referenceElement로 전달한 위치 앞에 엘리먼트 추가

### 노드 생성 API
- 노드를 추가하기 위해서는 추가할 엘리먼트를 생성해야 하는데 이것은 document 객체의 기능이다.
- [document.createElement(tagname)](https://developer.mozilla.org/ko/docs/DOM/document.createElement) : 엘리먼트 노드 추가
- [document.createTextNode(data)](https://developer.mozilla.org/ko/docs/Web/API/Document/createTextNode) : 텍스트 노드 추가

```
<ul id="target">
  <li>HTML</li>
  <li>CSS</li>
</ul>
```
- ul태그 아래에 태그추가
```
<input type="button" onclick="callAppendChild();" value="appendChild()" />
```
```
function callAppendChild(){
  var target = document.getElementById('target');
  var li = document.createElement('li');  // (1)
  var text = document.createTextNode('JavaScript');  // (2)
  li.appendChild(text);  // (3)
  target.appendChild(li);  // (4)
}
```
- 결과
```
<ul id="target">
  <li>HTML</li>
  <li>CSS</li>
  <li>JavaScript</li>
</ul>
```
> (1) 변수 li에 li 태그객체를 생성함. 내용은 비어있음<br/>어떤 특정 태그가 생성하는 것이 아닌 문서(document)가 생성하므로 document.createElement()인 것<br/>(2) 변수 text에 JavaScript2 텍스트(내용)를 생성<br/>(3) 인자의 내용이 생성된 li 태그 안쪽에 들어감<br/>(4) id가 target인 ul 태그의 마지막에 추가됨

- 맨 앞이나, 태그 사이에 넣고싶을 때는 insert 를 사용
```
<input type="button" onclick="callInsertBefore();" value="insertBefore()" />
```
```
  function callInsertBefore(){
    var target = document.getElementById('target');
    var li = document.createElement('li');
    var text = document.createTextNode('jQuery');
    li.appendChild(text);
    target.insertBefore(li, target.firstChild);
  }
```
- 결과
```
<ul id="target">
  <li>jQuery</li>
  <li>HTML</li>
  <li>CSS</li>
  <li>JavaScript</li>
</ul>
```
> 변수 li를 맨 앞으로 위치시킴<br/>즉, 두번째인자인 target.firstChild (=#text) 앞에 첫번째인자인 li 를 위치시킴


## 노드 제거
- [removeChild(child)](https://developer.mozilla.org/en-US/docs/Web/API/Node/removeChild) : 삭제대상의 부모 노드객체를 호출해 실행해야함
```
<ul>
  <li>HTML</li>
  <li>CSS</li>
  <li id="target">JavaScript</li>
</ul>

<input type="button" onclick="callRemoveChild();" value="removeChild()" />

<script>
  function callRemoveChild(){
    var target = document.getElementById('target');
    target.parentNode.removeChild(target);
  }
</script>
```
- 결과
```
<ul>
  <li>HTML</li>
  <li>CSS</li>
</ul>
```
> 어떤 태그를 삭제하기 위해서는 그 태그의 부모 엘리먼트를 알아야 함

- 삭제해야하는 대상과 그 부모까지 알아야하는 설계상의 문제점이 `DOM이 비판받는 이유`이다. 


## 노드 교체
- [replaceChild(newChild, oldChild)](https://developer.mozilla.org/en-US/docs/Web/API/Node.replaceChild)
```
<ul>
  <li>HTML</li>
  <li>CSS</li>
  <li id="target">JavaScript</li>
</ul>

<input type="button" onclick="callReplaceChild();" value="replaceChild()" />

<script>
  function callReplaceChild(){
    var a = document.createElement('a');  // (1)
    a.setAttribute('href', 'http://opentutorials.org/module/904/6701');  // (2)
    a.appendChild(document.createTextNode('Web browser JavaScript'));  // (3)
 
    var target = document.getElementById('target');
    target.replaceChild(a,target.firstChild);  // (4)
  }
</script>
```
- 결과
```
<ul>
  <li>HTML</li>
  <li>CSS</li>
  <li id="target">
    <a href="http://opentutorials.org/module/904/6701">Web browser JavaScript</a>
  </li>
</ul>
```
> (1) 엘리먼트를 생성<br/>(2) 속성부여<br/>(3) 내용추가<br/>(4) a객체를 target의 firstChild에 변경

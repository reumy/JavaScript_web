### DOM
## HTMLElement
- 조회한 객체들을 대상으로 구체적인 작업을 처리
- 작업을 처리하기위해 획득한 객체가 무엇인지 알아야 적절한 메소드나 프로퍼티를 사용할 수 있음


## 단수와 복수
```
<ul>
  <li>HTML</li>
  <li>CSS</li>
  <li id="active">JavaScript</li>
</ul>

<script>
  var li = document.getElementById('active');
  console.log(li.constructor.name);
  
  var lis = document.getElementsByTagName('li');
  console.log(lis.constructor.name);
</script>
```
- 결과
```
HTMLLIElement 
HTMLCollection
```
> 즉, 실행결과가 '하나'인 경우 HTMLLIELement, '복수'인 경우 HTMLCollection(유사배열)을 리턴

- `constructor : 객체의 Element 종류 조회`

## HTMLElement
- 실행결과가 하나인 엘리먼트
```
<a id="anchor" href="http://opentutorials.org">opentutorials</a>
<ul>
  <li>HTML</li>
  <li>CSS</li>
  <li id="list">JavaScript</li>
</ul>
<input type="button" id="button" value="button" />

<script>
  var target = document.getElementById('list');
  console.log(target.constructor.name);
 
  var target = document.getElementById('anchor');
  console.log(target.constructor.name);
 
  var target = document.getElementById('button');
  console.log(target.constructor.name);
</script>
```
- 결과
```
HTML__LI__Element
HTML__Anchor__Element
HTML__Input__Element
```
> 엘리먼트의 종류에 따라서 리턴되는 객체가 조금씩 다름

- 즉, 엘리먼트 객체에 따라서 프로퍼티가 다르다. 하지만 모든 엘리먼트들은 HTMLElement를 상속 받고 있다.

- DOM의 스펙
  - [HTMLElement](https://www.w3.org/TR/2003/REC-DOM-Level-2-HTML-20030109/html.html#ID-74680021)
  - [HTMLAnchroElement](https://www.w3.org/TR/DOM-Level-2-HTML/html.html#ID-48250443)
  - [HTMLInputElement](https://www.w3.org/TR/DOM-Level-2-HTML/html.html#ID-6043025)

- HTMLElement
```
interface HTMLLIElement : __HTMLElement__ {
  attribute DOMString       type;
  attribute long            value;
};
```
- HTMLAnchroElement
```
interface HTMLAnchorElement : __HTMLElement__ {
    attribute DOMString       accessKey;
    attribute DOMString       charset;
    attribute DOMString       coords;
    attribute DOMString       href;
    attribute DOMString       hreflang;
    attribute DOMString       name;
    attribute DOMString       rel;
    attribute DOMString       rev;
    attribute DOMString       shape;
    attribute long            tabIndex;
    attribute DOMString       target;
    attribute DOMString       type;
  void               blur();
  void               focus();
};
```
> 공통적인 태그(HTMLElement)의 성격을 가졌지만 각각의 기능이 세세하게 다르기 때문에 객체가 다르다.


## DOM Tree
- 모든 엘리먼트는 HTMLElement의 자식이다.<br/>따라서 HTMLElement의 프로퍼티를 똑같이 가지고 있다.<br/>동시에 엘리먼트의 성격에 따라서 자신만의 프로퍼티를 가지고 있는데 이것은 엘리먼트의 성격에 따라서 달라진다.<br/>HTMLElement는 Element의 자식이고 Element는 Node의 자식이고 Node는 Object의 자식이다.<br/>이러한 관계를 DOM Tree라고 한다.


![DOM Tree](images/jsw02.png)

[그림출처](https://web.stanford.edu/class/cs98si/slides/the-document-object-model.html)

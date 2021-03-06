### DOM
## HTMLElement
- 브라우저에 원래 있는 기능
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
> 객체의 이름을 조회함

- HTML\*ELement : 조회한 객체가 '하나'인 경우 ( \* : 각 엘리먼트에 해당되는 객체)<br/>HTMLCollection : '복수'인 경우 유사배열을 리턴
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
HTML'LI'Element
HTML'Anchor'Element
HTML'Input'Element
```
> 각 해당되는 태그를 추상화한 객체의 이름

- 엘리먼트의 종류(태그명)에 따라서 리턴되는 객체가 조금씩 다르다.<br/>그 말은 엘리먼트 객체에 따라서 프로퍼티(기능)가 다르다는 뜻<br/>하지만 모든 엘리먼트들은 공통적으로 HTMLElement를 상속 받고 있다.<br/>즉, 공통적인 프로퍼티를 가지고 있다. 하지만 동시에 태그의 성격과 쓰임에 따라 기능이 다르다.

- DOM의 스펙
  - [HTMLElement](https://www.w3.org/TR/2003/REC-DOM-Level-2-HTML-20030109/html.html#ID-74680021)
  - [HTMLAnchorElement](https://www.w3.org/TR/DOM-Level-2-HTML/html.html#ID-48250443)
  - [HTMLInputElement](https://www.w3.org/TR/DOM-Level-2-HTML/html.html#ID-6043025)

- HTMLElement
```
interface HTMLLIElement : HTMLElement {
  attribute DOMString       type;
  attribute long            value;
};
```
- HTMLAnchorElement
```
interface HTMLAnchorElement : HTMLElement {
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
- HTMLLIElement, HTMLAnchorElement, HTMLInputElement는 HTMLElement를 부모로 가지고있음<br/>즉, 공통적인 태그(HTMLElement)의 성격을 가졌지만 각각의 기능이 세세하게 다르기 때문에 각각 부가적인 기능을 가짐


## DOM Tree
- 모든 엘리먼트는 HTMLElement의 자식이다.<br/>따라서 HTMLElement의 프로퍼티를 똑같이 가지고 있다.<br/>동시에 엘리먼트의 성격에 따라서 자신만의 프로퍼티를 가지고 있는데 이것은 엘리먼트의 성격에 따라서 달라진다.<br/>HTMLElement는 Element의 자식이고 Element는 Node의 자식이고 Node는 Object의 자식이다.<br/>이러한 관계를 DOM Tree라고 한다.


![DOM Tree](images/jsw02.png)

[그림출처](https://web.stanford.edu/class/cs98si/slides/the-document-object-model.html)

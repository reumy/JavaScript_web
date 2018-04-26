## BOM
- 웹브라우저를 제어하기 위해 브라우저가 제공해주는 객체들을 의미
- 전역객체인 Window의 프로퍼티와 메소드들을 통해서 제어할 수 있으므로 BOM은 Window 객체의 프로퍼티와 메소드의 사용과 같다고 할 수 있음
- 자바스크립트를통해 새창을 열기, 해당URL을 파악, 웹브라우저의 제품명, 모델명(크롬, 사파리 등)을 알아낼 수 있다.


## Window 전역객체
- 창, 프레임
- Window 객체는 모든 객체가 소속된 객체로 전역객체이다.
- Window 객체는 식별자 window를 통해서 얻을 수 있으며 생략이 가능
```
alert('Hello world');
 
window.alert('Hello world');
```
> 경고창
```
var a = 1;
 
alert(a);
alert(window.a);
```
> 전역변수 a에 접근
```
var a = {id:1};
 
alert(a.id);
alert(window.a.id);
```
> 객체를 만든다는 것은 결국, window 객체의 프로퍼티를 만드는 것과 같음
 
- 결국 '전역변수'와 '함수'는 window 객체의 프로퍼티와 메소드라는 것이고 모든 객체는 window의 자식이라는 것이다. 이 특성을 ECMAScript에서는 Global 객체라고 한다. 웹브라우저 자바스크립트에서 Window 객체는 ECMAScript의 전역객체이면서 동시에 웹브라우저의 창이나 프레임을 제어하는 역할을 한다.

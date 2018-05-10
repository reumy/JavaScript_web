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
- 전역변수를 만든다는것은 window 객체의 프로퍼티, 메소드를 만드는것과 같다.
```
var a = {id:1};
 
alert(a.id);
alert(window.a.id);
```
> 객체를 만든다는 것은 결국, window 객체의 프로퍼티를 만드는 것과 같음
 
- 결국 '전역변수'와 '함수'는 window 객체의 프로퍼티와 메소드라는 것이고 모든 객체는 window의 자식이라는 것이다. 이 특성을 ECMAScript에서는 Global 객체라고 한다. 웹브라우저 자바스크립트에서 Window 객체는 ECMAScript의 전역객체이면서 동시에 웹브라우저의 창이나 프레임을 제어하는 역할을 한다.

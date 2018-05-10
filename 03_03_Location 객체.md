### BOM
## Location 객체
- 윈도우의 문서의 주소(URL)을 알아내거나 변경할 수 있고, 문서의 위치와 관련해서 다양한 정보를 얻을 수 있음


### 현재 윈도우 URL 알아내기
- 현재 윈도우의 문서가 위치하는 URL을 알아내는 방법
```
console.log(location.toString(), location.href);  // url 출력
```
> location.toString(), location.href 모두 같은값을 리턴하지만, location.href 를 사용하는 것이 더 일반적

```
console.log(location)
```
> 객체가 가진 프로퍼티(location)를 분석해서 보여줌 (객체정보)
```
alert(location)  // url을 출력함
```
> alert은 인자로 입력한 입력값이 문자열이어야 하기때문에 결과를 문자화시켜서 보여줌


### URL Parsing
- URL의 구간 정보 알아내기
- location 객체는 URL을 의미에 따라서 별도의 프로퍼티로 제공하고 있음

ex) http://opentutorials.org:80/module/1?id=1#bookmark
```
console.log(location.protocol);  // http:
```
> 프로토콜 (http, https, file 등)

> `HTTP : 웹서버와 웹브라우저가 서로 통신하기위한 통신규약`

```
console.log(location.host);  // opentutorials.org
```
> 서비스를 식별하는 주소
```
console.log(location.port);  // :80
```
> 포트번호 (= 서버 소프트웨어 식별)<br/>기본포트(80, 8080)일땐 생략됨(undefined)
```
console.log(location.pathname);  // module/1
```
> 웹서버의 구체적인, 특정한 정보 (하위 디렉토리)
```
console.log(location.search);  // ?id=1
```
> 사이트 즉, 애플리케이션에게 전달한 값 (?~)
```
console.log(location.hash);  // #bookmark
```
> 문서에 정의해둔 특정구간 위치 식별자

- 위와 같은 location에 대한 부분들을 분석해서 뿌리기
```
console.log(location)
```


## URL 변경하기
- 현재 문서를 http://egoing.net으로 이동
```
location.href = 'http://egoing.net';

location = 'http://egoing.net';
```
- 현재 문서를 리로드
```
location.href = location.href

location.reload();
```

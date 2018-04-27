## Location 객체
- 윈도우의 문서의 주소(URL)을 알아내거나 변경할 수 있고, 문서의 위치와 관련해서 다양한 정보를 얻을 수 있음


### 현재 윈도우 URL 알아내기
- 현재 윈도우의 문서가 위치하는 URL을 알아내는 방법
```
console.log(location.toString(), location.href);
```
> location.toString(), location.href 모두 같은값을 리턴하지만, location.href 를 사용하는 것이 더 일반적

### URL Parsing
- URL의 구간 정보 알아내기
- location 객체는 URL을 의미에 따라서 별도의 프로퍼티로 제공하고 있음

ex) http://opentutorials.org:80/module/1?id=1#bookmark
```
console.log(location.protocol);  // http:
```
> 프로토콜 (http, https, file 등)
```
console.log(location.host);  // opentutorials.org
```
> 식별하는 주소
```
console.log(location.port);  // :80
```
> 포트번호 (= 서버 소프트웨어 식별)<br/>기본포트(80, 8080)일땐 undefined
```
console.log(location.pathname);  // module/1
```
> 웹서버의 구체적인, 특정한 정보
```
console.log(location.search);  // ?id=1
```
> 사이트 즉, 애플리케이션에게 전달한 값
```
console.log(location.hash);  // #bookmark
```
> 특정구간 식별자
- console.log(location)을 실행하면 위와 같은 location에 대한 부분들을 분석해서 뿌려줌


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

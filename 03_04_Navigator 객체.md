### BOM
## Navigator 객체
- 브라우저의 정보(제품명, 버젼 등)를 제공하는 객체
- 브라우저 특성에 맞는 코딩을 할 수 있도록 제공함
```
console.log(navigator);

console.dir(navigator);
```
> Navigator의 모든 프로퍼티 열람


### 크로스브라우징(cross browsing)
- Netscape와 IE브라우저 두 회사의 경쟁으로 무질서하게 기능이 추가되어 각기 다른 브라우저에 다른 코드를 작성해야하는 불편함이 생겼다.<br/>W3C(ECMA) 국제표준화기구가 `웹표준`을 세워 질서를 바로았으나 세밀한 부분은 아직 남아있다.<br/>이러한 현상을 크로스브라우징이라 부르고 각기 다른 브라우저의 호환성을 확인하기 위해 Navigator객체를 사용한다.
- IE, FireFox, Chrome, Safari, Opera 


## 주요 프로퍼티

### appName
- 웹브라우저의 이름
  - IE은 Microsoft Internet Explorer 로 표시 (현재는 IE, Edge도 Nescape로 표시)
  - 파이어폭스, 크롬 등은 Nescape 로 표시
```
console.dir(navigator.appName);
```

### appVersion
- 브라우저의 버전
```
console.dir(navigator.appVersion);
```

### userAgent
- 브라우저가 서버측으로 전송하는 User Agent HTTP 헤더의 내용
- appVersion과 비슷
```
console.dir(navigator.userAgent);
```

### platform
- 브라우저가 동작하고 있는 운영체제에 대한 정보
```
console.dir(navigator.platform);
```

### 기능 테스트
- 작성한 코드가 브라우저에서 동작될때 사용할 기능이 동작되는지 테스트 하는 방법을 알아보는 것
- Navigator 객체는 브라우저 호환성을 위해서 주로 사용하지만 모든 브라우저에 대응하는 것은 쉬운 일이 아니므로 기능 테스트를 사용하는 것이 더 선호됨
- 예를들어 Object.keys (key 값을 배열로 리턴하는 Object의 메소드)는 ECMAScript5 (최신 JavaScript)에 추가되었기 때문에 오래된 자바스크립트와는 호환되지 않기때문에 `브라우저에 따라 다르게 동작하는 처리가 필요`하다. 그럴때 아래의 코드처럼 호환성을 맞출 수 있다.
```
if (!Object.keys) {
  Object.keys = (function () {
    'use strict';
    var hasOwnProperty = Object.prototype.hasOwnProperty,
        hasDontEnumBug = !({toString: null}).propertyIsEnumerable('toString'),
        dontEnums = [
          'toString',
          'toLocaleString',
          'valueOf',
          'hasOwnProperty',
          'isPrototypeOf',
          'propertyIsEnumerable',
          'constructor'
        ],
        dontEnumsLength = dontEnums.length;
 
    return function (obj) {
      if (typeof obj !== 'object' && (typeof obj !== 'function' || obj === null)) {
        throw new TypeError('Object.keys called on non-object');
      }
 
      var result = [], prop, i;
 
      for (prop in obj) {
        if (hasOwnProperty.call(obj, prop)) {
          result.push(prop);
        }
      }
 
      if (hasDontEnumBug) {
        for (i = 0; i < dontEnumsLength; i++) {
          if (hasOwnProperty.call(obj, dontEnums[i])) {
            result.push(dontEnums[i]);
          }
        }
      }
      return result;
    };
  }());
}
```
> 만약 Object.keys이 없다면 위의 코드를 실행해 같은 기능을 구현시켜라 (코드분석은 나중에)

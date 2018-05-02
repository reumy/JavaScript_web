## 등록방법
- 이벤트 프로그래밍을 하기 위해서는 이벤트의 대상에 이벤트 핸들러를 등록해줘야 한다.


## inline
- 이벤트를 이벤트 대상의 태그 속성으로 지정하는 것
- 인라인 방식은 태그에 이벤트가 포함되어 이벤트의 소재를 파악하는 것이 편리하지만 정보(HTML)와 제어(JavaScript)가 혼재된 형태라서 바람직한 방법이 아니다.

```
<input type="button" onclick="alert('Hello world');" value="button" />
```
- 이벤트가 발생한 대상을 필요로하는 경우 this를 통해서 참조할 수 있음
```
<input type="button" id="target" onclick="alert('Hello world, '+document.getElementById('target').value);" value="button" />
```
> 자기 자신을 참조하는 불편한 방법<br/>여러개 복사했을때 동작X<br/>id값이 겹치고 getElementById는 하나의 값을 retrun하기 때문이다.

```
<input type="button" onclick="alert('Hello world, '+this.value);" value="button" />
```
> this를 통해서 간편하게 참조<br/>여러개 복사했을때 동작O<br/>

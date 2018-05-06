## jQuery Ajax
- jQuery이용해서 Ajax를 사용하게 되면 크로스브라우징의 문제를 jQuery가 알아서 해결해줌
- 그 외에도 많은 편리한 기능들을 제공
- [jQuery의 Ajax관련 API](http://api.jquery.com/category/ajax/)


## [$.ajax](http://api.jquery.com/jQuery.ajax/)
- 가장 중요한 API
```
jQuery.ajax([settings])
```
> setting는 Ajax 통신을 위한 옵션을 담고 있는 객체가 들어감

### 주요옵션
```
$.ajax({
  url: 'http://opentutorials.org/example/jquery/example.jquery.ajax.php',
  dataType: 'json',
  type: 'POST',
  data: {
    'msg': $('#msg').val()
  },
  success: function(result) {
    if (result['result'] == true) {
      $('#result').html(result['msg']);
    }
  }
});
```
- data : 서버에 전송할 데이터 (key, value)
- dataType : 서버거 리턴하는 데이터 타입 (xml, json, script, html)<br/>값으로 올 데이터 형식을 지정하지 않으면 jQuery가 알아서 판단
- success : 성공했을 때 호출될 콜백(이벤트 핸들러)을 지정<br/>Function(PlainObject data, String textStatus, jqXHR jqXHR)
- type : 서버로 전송하는 데이터 방식 (GET, POST)


### Ajax의 모든 예제를 jQuery화 하기
- time.php
```
<?php
$d1 = new DateTime;
$d1->setTimezone(new DateTimezone("asia/seoul"));
echo $d1->format('H:i:s');
?>
```
- demo1.html
```
<p>time : <span id="time"></span></p>
<input type="button" id="execute" value="execute" />

<script src="//code.jquery.com/jquery-1.11.0.min.js"></script>
<script>
  $('#execute').click(function(){
    $.ajax({
      url:'./time.php',
      success:function(data){
        $('#time').append(data);
      }
    })
  })
</script>
```
> XMLHttpRequest에 비해서 코드가 훨씬 간결해짐


## POST
- time2.php
```
<?php
$d1 = new DateTime;
$d1->setTimezone(new DateTimezone($_POST['timezone']));
echo $d1->format($_POST['format']);
?>
```

- demo2.html
```
<p>time : <span id="time"></span></p>
<form>
  <select name="timezone">
    <option value="Asia/Seoul">asia/seoul</option>
    <option value="America/New_York">America/New_York</option>
  </select>
  <select name="format">
    <option value="Y-m-d H:i:s">Y-m-d H:i:s</option>
    <option value="Y-m-d">Y-m-d</option>
  </select>
</form>
<input type="button" id="execute" value="execute" />

<script src="//code.jquery.com/jquery-1.11.0.min.js"></script>
<script>
  $('#execute').click(function(){
    $.ajax({
      url:'./time2.php',
      type:'post',
      data:$('form').serialize(),
      success:function(data){
        $('#time').text(data);
      }
    })
  })
</script>
```
> data:$('form').serialize()는 form 태그의 정보를 '값의이름=값의내용&값'의 형식으로 바꿔서 서버로 전송한다.<br/>즉, 서버로 전송하는 데이터의 형식을 지키는 코드인 data += ~ 단계가 생략됨<br/>단, serialize 작업시에는 form 태그 안에 있는 태그들은 반드시 name 속성을 가지고 있어야 함


## JSON 처리
- $.ajax를 이용해서 JSON을 처리하는 방법


- time3.php
```
<?php
$timezones = ["Asia/Seoul", "America/New_York"];
echo json_encode($timezones);
?>
```

- demo3.html
```
<p id="timezones"></p>
<input type="button" id="execute" value="execute" />

<script src="//code.jquery.com/jquery-1.11.0.min.js"></script>
<script>
  $('#execute').click(function(){
    $.ajax({
      url:'./time3.php',
      dataType:'json',
      success:function(data){
        var str = '';
        for(var name in data){
          str += '<li>'+data[name]+'</li>';
        }
        $('#timezones').html('<ul>'+str+'</ul>');
      }
    })
  })
</script>
```
> dataType:'json'은 서버에서 리턴한 값을 json 형식으로 갖고있음을 명시해줌

##### JQuery(JavaScript를 편리하게 쓰기위한 라이브러리, 똑같이 <script>태그 안에다 작성한다.)

<script> 태그로 둘러싼 스크립트 언어다. 

jQuery 라이브러리를 가져오는 <script>태그를 먼저 써주고 그 밑에 코드를 작성하는 <Script>태그를 쓰자(그래야 둘다 인식한다.)

ex)

<head>
<script src="/resources/plugins/jQuery/jQuery-2.1.4.min.js"></script> // 라이브러리를 가져오는 태그를 먼저 입력 후
<script>
	var bno=10;
	
	$.getJSON("/replies/all/"+bno, function(data) {
		console.log(data.length);
	});
</script>								// 코드를 작성하는 태그 입력

일반적으로 <head> 태그 안에다 작성하고 <body> 태그에다 작성해도 무관하다.

위치

1. 내부 : <head>섹션 또는 <body>섹션에다 작성

2. 외부 : 일반적으로 <head>섹션에 작성하고 외부 파일의 스크립트를 사용할 수 있다.
	  ex) <script src="myscript.js"></script>

3. 인라인 : HTML 태그 내부에 이벤트 속성으로 삽입한다.
	    ex) onclick속성 : <button type="button" onclick="alert('반갑습니다.')">버튼을 누르세요!</button>


-----

##### 값 가져오는 방법

클래스 : $(".해당class");

아이디 : $("#해당id");

이름 : $('[name="해당name"]');

역할(role) : $("form[role='해당role']");

-----

##### 자주 쓰이는 메서드

###### $("#해당id").val();

 : 해당 id에 입력된 값(input 태그의 값)을 가져온다.

ex)

var replyer = $("#newReplyWriter").val();


-----

###### $("#해당id").val(data);

 : 아이디가 해당id인 요소의 값을 data로 정한다.

-----

###### $("#testId").html() 

: 해당 id를 가지는 태그의 자식태그의 값을 가져온다(태그 포함, 자식태그 없이 해당 태그의 값만 있으면 그 값만 가져온다.)

ex) <div class="test">haha</div>

console.log($(".test").html); // output : haha

<div>
   <button>test button</button>
</div>

console.log($(".test").html); // output : <button>test button</button>



$("#testId").html(html data) : 해당 id를 가지는 태그의 내용을 인자의 값으로 바꾼다.


$("#testId").text() : 해당 id를 가지는 태그의 값을 가져온다(태그 제외하고 태그 내의 값만) 

-----

.val()과 .text()의 차이 : val()은 사용자가 입력한 input태그의 값을 가져오고, text()는 이미 지정되어 있는 text의 값을 가져온다.


-----

$(class or id or name).on(event, selector, data);

event : 활성화 되는 이벤트(ex) "click")

select : 실행 할 태그

data : 이벤트가 실행 될 때 전달되는 data(function(data)) 를 통해 data를 사용한 실행 내용을 만들 수도 있다.




-----


$(class or id or name).attr(tag's name)

해당 태그의 값을 가져온다.


-----

##### JQuery를 사용해 view에서 JSON객체를 받는 방법(getJSON() 메소드 사용)

$.getJSON("/replies/all/" + bno, function(data) {

	console.log(data.length);	

});

view이름이 test라면 path를 /test로 접근했을 때 /replies/all/해당bno로 접근해서 데이터를 가져온다는 의미다.

-----

##### Ajax 전송 형식 

: jquery의 비동기 전송방식 중 한개($.ajax(), $.get(), $.post() 총 3가지가 있다.)

headers에서 content-Type(context-Type으로 헷갈렸었다. 주의하자)

ex)

$.ajax({
type : 'post',
url : '/replies',
headers : {
	"Content-Type" : "application/json"
	"X-HTTP-Method-Override" : "POST"
},
dataType : 'text',
data : JSON.stringify({
	bno : bno,
	replyer : replyer,
	replyText : replytext
}),
success : function(result) {
	if(result == 'SUCCESS') {
		alert("등록되었습니다.")
	}
}
   }); // ajax end
});


data에서 JSON형식으로 보낼 때는 {VO객체의 필드 : 보낼 값}으로 해야 된다.

-----


##### ajax 구성요소

type : 전송방식

url : 입력한 url로 data를 전송

headers : 아직 잘 모르겠다.

dataType : 전송할 데이터의 타입

data : 전송하고자 하는 데이터

success : 성공했을 때 실행할 내용

processData

- 데이터를 일반적인 query string으로 변환할 것인지를 결정

- 기본값 : 'application / x-www-form-urlencoded'

- 다른 형식의 데이터를 보내기 위해 자동 변환하고 싶지 않은 경우 false를 지정하면 된다.

contentType

- 기본값 : 'application / x-wwwform-urlencoded'

- 파일의 경우 multipart/form-data 방식으로 전송하기 위해 false로 지정해야 한다.




-----

##### Ajax가 무반응 일때

<sciprt>태그를 <body>태그 안에서

view관련 태그를 모두 작성하고 아래에다 써준다.

-----

api : https://api.jquery.com/jquery.getjson/

$.getJSON(URL, function(data) {

			$(data.list).each(function() {
				str += "<li data-rno='"+this.rno+"' class='replyLi'>"
				+ this.rno+":"+this.replyText+
				"<button>MOD</button></li>";
			});
			
			$("#replies").html(str);

});

data : uri에 접근 했을 때 Controller에서 mapping되는 메서드의 return 값을 얻을 수 있다.

data.list : 예제에서 Controller에서 mapping되는 메서드의 리턴 값이 map인데 key값으로 list가 있어서 바로 접근해 반복문을 돌리는 것이다.



-----

$.getJSON(URL, function(data)
$.each(data, fucntion(key,value))

와 같은 jQuery의 첫 번째 인자에서 반환하는 데이터를 function의 인자로 넣을 수 있다.
(따로 인자를 넣어줘야 하는 것이 아니라 첫 번째 인자에서 function의 인자로 알아서 인식한다.)


-----

$(document).ready(function(){
   
   executed statement

});


프로젝트를 실행함과 동시에 실행되는 부분

Java Script의

window.onload = function(){

   executed statement

}

와 동일한 기능을 하지만 window.onload보다 document가 먼저 실행된다.(1.document > 2.window.onload)



-----

ex) 

that.parent("div").remove();


: that 이 <small> 태그였을 경우 <small>태그 바깥쪽(부모)에서 가장 가까이 있는 <div>태그를 지우는 기능을 한다.


-----

##### jQuery를 사용하는 <script>는 <body> 최하단에 작성하자(<head>에다 작성하면 인식하지 못하는 경우가 있다.)

-----
$(".class b") : 해당 class명을 가지는 태그 내부의 b 태그(id 또는 class) 


$(".uploadedList li").each(function(index) {
			arr.push($(this)("data-src"))
		});

의 경우 class명이 uploadedList인 태그 안에 선언되어 있는 li태그에 대해 적용하는 함수다.

-----




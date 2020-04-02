##### <script> 태그로 둘러싼 스크립트 언어다. 

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

---

##### 일반적으로 <head> 태그 안에다 작성하고 <body> 태그에다 작성해도 무관하다.

위치

1. 내부 : <head>섹션 또는 <body>섹션에다 작성

2. 외부 : 일반적으로 <head>섹션에 작성하고 외부 파일의 스크립트를 사용할 수 있다.
	  ex) <script src="myscript.js"></script>

3. 인라인 : HTML 태그 내부에 이벤트 속성으로 삽입한다.
	    ex) onclick속성 :    <button type="button" onclick="alert('반갑습니다.')">버튼을 누르세요!</button>


##### JSP파일 관련 오류는 웹 브라우저의 F12를 눌러 Console에서 확인하자(STS의 콘솔창에서는 view파일에서 발생한 오류를 확인할 수 없다.)

##### console

###### console.log

	var a = 1;
	var b = "hello";
	var c = true;

	console.log(a); // 하나만 로그
	
	console.log(a,b,c); // 여러 개 동시에 로그
	
	console.log("idx : ", idx) // 텍스트와 변수 동시 출력
	
	console.log("idx : ", idx, ", val : ", val); // 여러 텍스트/변수 동시 출력
	
	console.log("${a}는 숫자, ${b}는 문자열"); // 변수와 텍스트 동시 출력(안되는데?)
	
* 주의 사항

객체의 필드 값을 출력하고 싶을 땐 ${인스턴스.필드} 로 검색해야 한다.

예시의 경우처럼 선언한 변수 또는 메소드의 인자의 경우는 바로 변수 명을 입력해야된다.

객체의 변경사항이 실시간으로 반영된다.


###### console.dir

객체를 로깅할 경우 필드 값을 정리해서 출력한다.

객체는 dir, 나머지는 log로 로깅하면 편리하다.

ex)

	console.dir("${alist}");
	
alist는 ArrayList 인스턴스다.

###### console.count

몇번이나 카운트되었는지 확인하고 싶을 때 사용한다.

	console.count('카운터1'); // 카운터1: 1
	console.count('카운터1'); // 카운터1: 2
	console.count('카운터2'); // 카운터2: 1
	console.count('카운터2'); // 카운터2: 2
	console.count('카운터1'); // 카운터1: 3

###### console.time, console.timeEnd

코드의 수행시간을 확인할 때 사용한다.

	console.time('타이머');
	for (var i = 0; i < 1000000; i++) z = 5;
	console.timeEnd('타이머'); // 타이머: 6.76611328125ms


##### JQuery(JavaScript를 편리하게 쓰기위한 라이브러리, 똑같이 <script>태그 안에다 작성한다.)

###### 값 가져오는 방법

클래스 : $(".해당class");

아이디 : $("#해당id");

이름 : $('[name="해당name"]');

역할(role) : $("form[role='해당role']");

###### JQuery를 사용해 view에서 JSON객체를 받는 방법(getJSON(uri,function(data)) 메소드 사용)

$.getJSON("/replies/all/" + bno, function(data) {

	console.log(data.length);	

});

view이름이 test라면 path를 /test로 접근했을 때 /replies/all/해당bno로 접근해서 데이터를 가져온다는 의미다.


##### document.

write(text) : text를 웹페이지에 띄운다.

getElementById(id) : id가 id인 요소를 가져온다.


-----

alert(text) : text를 메세지로 하는 경고창을 화면에 출력

confirm(text) : text를 메세지로 하는 창을 출력 확인 / 취소를 누를 수 있고 true / false를 반환한다.

-----

prompt(text, defaultText) : dialbox를 띄운다. 사용자가 입력한 텍스트를 반환한다.

text : 입력칸 위에 안내 메세지

defautText(선택) : 입력칸에 초기 메세지 출력

-----

요소(Elements) : 

HTML에서 시작 태그와 종료태그로 이루어진 모든 명령어들을 의미합니다.

태그(Tag) : 

요소(Elements)의 일부로 시작 태그와 종료 태그 두 종류가 있습니다.

속성(Attributes) : 

요소의 시작 태그 안에서 사용되는 것으로 좀 더 구체화된 명령어 체계를 의미합니다.

section : http://webdir.tistory.com/310

------

for/in loop

for(변수 in 객체) {} : 변수에 객체의 모든 속성이 하나씩 대입되면서 반복한다.


------

self.location = "path";

: 해당 path로 redirection 한다.

------


##### JSTL

<C:ooo> 태그를 사용하는 라이브러리

ex) 

<c:forEach></c:forEach> : <c:forEach items="${list}" var="boardVO"> 또는 <c:forEach begin="startNum" end="endNum"></c:forEach>


<c:if></c:if> : <c:if test="조건문"> true일경우 실행 </c:if>

<c:out></c:out> : <c:out value="출력할 값(3항 연산자 사용가능)"></c:out>

-----

메서드 선언

var methodName = function(params) {

	// executed statement

}

메서드를 재사용하기 위해서는 위와 같이 선언해야 한다.


-----

modal : 사용자의 입력을 독점하는 UI(팝업창)

modality : modal의 특성


-----


DOM(Document Object Model) : Java Script를 사용한 작업이 이루어지는 장소. Java Script로 하는 작업 = DOM API

ex)

// view code

<div id="container"></div>

// Java Script code

<script>
  var container = document.getElementById("container");
  container.innerHTML = "New Content!";
</script>


// 브라우저의 개발 툴

<div id="container">New Content!</div>  // 이게 DOM

보통 view파일의 코드와는 다르다.



-----

parent.메소드명

: 현재 페이지로 오기 바로 전 페이지(jsp파일)에 정의되어 있는 메소드를 호출한다.


-----

<script> 태그의 적절한 위치


단순 java script : <body> 최하단

jQuery : <head>

CSS : <head>

이유도 찾아서 확인하자


-----
js 파일 생성 방법(java script의 소스만 담겨져 있는 파일)

new > Java Script Source File 생성


-----

js 또는 css파일이 웹 브라우저에서 바로바로 적용되지 않을 때

<script>의 입력하는 경로의 마지막에 "?ver=1"을 추가해준다.(숫자는 아무거나 해도 상관 없다.)

브라우저가 기존 캐쉬에 있는 파일과 다른 파일로 인식해서 수정한 내용이 바로 적용된다.

ex)

<script type="text/javascript" src="/resources/js/upload.js?ver=1"></script>

그래도 안될 경우

\workspace\.metadata\.plugins\org.eclipse.wst.server.core\tmp1\work\Catalina\localhost\ROOT\org\apache\jsp\WEB_002dINF\views

views 폴더안에 있는 관련 파일을 모두 삭제한다.

-----

$(document).ready(function{

// 이 안에 작성하는 내용은 처음 페이지로 이동했을 때만 실행되고

click 같은 이벤트가 발생했을 때 실행되는 내용은 적용되지 않는다.

});

근데 될 때도 있네..?(안될 때는 뭐가 문제지...)

-----

event.preventDefault();

: 해당 이벤트(ex) 클릭)를 했을 때 default로 설정되어 있는 실행 내용이 실행되지 않도록 해준다.

ex) 이미지 클릭 : 페이지를 이동하여 해당 이미지를 확대해서 보여준다.

-----
##### <script> 태그로 둘러싼 스크립트 언어다. 

<script type="text/javascript">

</script>

type을 명시하지 않아도 HTML5에서는 default가 javascript이기 때문에 무방하지만

표준은 명시해주는 것이 맞다.

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

##### var

모든 자로형 / 자료구조는 var 타입으로 정의된다.

typeof(변수명) 을 통해 세부타입을 확인할 수 있다.

ex)

	var name = "yoo";
	
	console.log(typeof(name)); // "String" 을 리턴한다.
	
	console.log(name.length); // name의 길이인 3을 리턴한다.
	


	
###### 배열

	var array = new array();
	var array = [];
	
	array[0] = "haha";
	array[1] = "hoho";
	
	var array = new array("haha", "hoho"); 
	
	var date = "2020-05-04";
	
	var array = date.split("-");
	
	var array = ["2020", "05", "04"];
	
##### 반복문

###### for

	for(var index = 0; index < 5; index++){
		console.log(index); // 0 1 2 3 4 의 순서로 출력된다.
	}
	

###### for-in

	for(var arrayIndex in array){
		console.log(array[arrayIndex]);
	}
	
배열의 크기만큼 알아서 반복문이 실행된다.

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


ex)

		function updateComment(commentIndex) {

			$.ajax({

				url : "./editComment",
				type : "POST",
				data : {
					commentIndex : commentIndex,
					comment : $("#updatedComment").val() // 이 부분
				},
				success : function(data) {

					if (data == "1") {
						alert("수정이 완료되었습니다.");
						getCommentList();
					}
				}
			});
		}
		
태그의 id 속성이 updatedComment인 태그의 값을 가져온다.


###### 주의사항



###### JQuery를 사용해 view에서 JSON객체를 받는 방법(getJSON(uri,function(data)) 메소드 사용)

$.getJSON("/replies/all/" + bno, function(data) {

	console.log(data.length);	

});

view이름이 test라면 path를 /test로 접근했을 때 /replies/all/해당bno로 접근해서 데이터를 가져온다는 의미다.


##### document



document.write(text) : text를 웹페이지에 띄운다.

document.getElementById(id) : id가 id인 요소(객체)를 가져온다.(String, list 처럼 다양한 자료형/자료구조가 리턴될 수 있다.)

document.form태그의id.submit() : 해당 id를 가지는 form태그를 전송한다.(버튼 없이 이렇게 메소드로 가능하다.)

document.ready : 안에 있는 소스는 페이지 이동과 동시에 실행된다.

	document.ready(
			function(){
				
				// 실행할 소스
			
			});



---

##### 자주 쓰이는 메소드들

location.href = "../review_edit/" + ${bean.reviewIndex} : 해당 URL로 이동시켜준다.(그냥 변수에 초기화 하는 것 같은데 메소드 처럼 작동한다.)

alert(text) : text를 메세지로 하는 경고창을 화면에 출력

confirm(text) : text를 메세지로 하는 창을 출력. 확인 / 취소를 누를 수 있고 true / false를 반환한다.

prompt(text, defaultText) : dialbox를 띄운다. 사용자가 입력한 텍스트를 반환한다.

text : 입력칸 위에 안내 메세지

defautText(선택) : 입력칸에 초기 메세지 출력

---

##### 페이지 최초 이동시 자동으로 functions을 실행하도록 하는 방법

			$(function() {

				getCommentList(1); // 실행할 메소드를 명시하면 된다.

			});

---

##### HTML 구성요소

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


##### DOM(Document Object Model) : Java Script를 사용한 작업이 이루어지는 장소. Java Script로 하는 작업 = DOM API

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

##### parent.메소드명

: 현재 페이지로 오기 바로 전 페이지(jsp파일)에 정의되어 있는 메소드를 호출한다.


-----

##### <script> 태그의 적절한 위치


단순 java script : <body> 최하단

jQuery : <head>

CSS : <head>

이유도 찾아서 확인하자


-----
##### js 파일 생성 방법(java script의 소스만 담겨져 있는 파일)

new > Java Script Source File 생성


-----

##### js 또는 css파일이 웹 브라우저에서 바로바로 적용되지 않을 때

<script>의 입력하는 경로의 마지막에 "?ver=1"을 추가해준다.(숫자는 아무거나 해도 상관 없다.)

브라우저가 기존 캐쉬에 있는 파일과 다른 파일로 인식해서 수정한 내용이 바로 적용된다.

ex)

<script type="text/javascript" src="/resources/js/upload.js?ver=1"></script>

그래도 안될 경우

\workspace\.metadata\.plugins\org.eclipse.wst.server.core\tmp1\work\Catalina\localhost\ROOT\org\apache\jsp\WEB_002dINF\views

views 폴더안에 있는 관련 파일을 모두 삭제한다.

-----

##### $(document).ready(function{

// 이 안에 작성하는 내용은 처음 페이지로 이동했을 때만 실행되고

click 같은 이벤트가 발생했을 때 실행되는 내용은 적용되지 않는다.

});

근데 될 때도 있네..?(안될 때는 뭐가 문제지...)

-----

##### event.preventDefault();

: 해당 이벤트(ex) 클릭)를 했을 때 default로 설정되어 있는 실행 내용이 실행되지 않도록 해준다.

ex) 이미지 클릭 : 페이지를 이동하여 해당 이미지를 확대해서 보여준다.

-----

##### form태그에서 submit 하기 전에 전송되는 데이터를 체크하고 싶을 때


	<script>
	
		function checkMainImage(){
		
		var mainImage = document.getElementById("mainImage").value;
		var subImages = document.getElementById("subImages").value;
		
		if(mainImage.length == 0 && subImages.length > 0) {
			alert("메인 이미지를 첨부해주세요.");
			return false;
		} else
			document.imageUpload.submit();
		
	}
	
	</script>

	<form method="POST" enctype="multipart/form-data" name="imageUpload">
		
		<div>
			<input  type="file" name="mainImage" id="mainImage" />
		</div>		
		<div>
			<input type="file" name="subImages" id="subImages" multiple="multiple" />
		</div>
		
		<button type="button" class="btn btn-default" onclick="checkMainImage()">완료</button>
	</form>
	
	

<button>의 type을 button으로 해준 다음 script에서 input의 값을 확인하고 submit을 실행하도록 한다.

type이 submit일 경우 버튼을 누르면 script에서 submit을 실행하지 않아도 강제로 form의 데이터가 전송된다.

---

##### <script> 태그 안에서 el, jquery 사용

<script> 태그 안에서도


	data : { clientID : "${bean.clientID}"},

와 같이 el표현으로 값을 가져올 수 있다.(controller에서 model.addAttribute("name", value)된 값을 사용하는 것이다.)

같은 문서 내에서 태그안에 작성하는 것이니까 당연히 되는 것이라고 생각하면 된다.(JQuery를 사용한 값도 가져올 수 있다.)

---

##### function 파라미터의 타입

			html += "<div><table class='table'><h6><strong>"
					+ data[i].clientID
					+ "</strong>&emsp;<a href='#' onClick='changeToTextArea("
					+ data[i].commentIndex
					+ ",\""
					+ data[i].comment // <- 이부분
					+ "\")'>수정</a>&emsp;<a href='#' onClick='deleteComment("
					+ data[i].commentIndex
					+ ")'>삭제</a></h6>";
					
					
data[i].comment가 숫자일 경우 int가 되고 문자일 경우 String이 된다.

하지만 두 경우 다 문자로 받아야 changeToTextArea메소드에서 파라미터로 사용할 수 있기 때문에

타입을 통일시키기 위해서 양 옆에 ""로 씌워준다.

"" 안에 ""를 작성하는 것이기 때문에 오류가 발생한다. 

이를 해결하는 방법으로 "를 문자로 인식하기 위해서 \(이스케이프문자)를 "앞에 입력해줘야 된다.

---

##### 따옴표 사용(태그의 속성)

	pagingHTML += "<c:if test="+pageMaker.prev+">"; // 오류난다.(못 읽는다.)

	pagingHTML += "<c:if test=true>"; // 이건 오류난다.(문법 오류)
	
뭐가 문젠지 확인하자.

---

##### 다른 URL로 이동하는 방법

	window.location = "URL";
	
	window.location.href = "URL";
	
	window.location.assign("URL");
	
	window.location.replace("URL");
	
	self.location = "URL";
	
	top.location = "URL";


window.location은 단순히 location만 사용해도 된다. 위 코드 중 첫 내게는 아래와 같이 사용이 가능하다.

	location = "URL";
	
	location.href = "URL";
	
	location.assign("URL");
	
	location.replace("URL");
	
참고사이트 : https://jamesdreaming.tistory.com/43
	
---

##### 현재 페이지 새로고침

	location.reload(true);

	location.href = location.href;

	history.go(0);

##### javascript: 기능

			<a class="btn btn-default" href="javascript:history.back();"
			role="button">뒤로</a>

javascript:history.back() : 이전페이지로 갈 수 있다.

javascript:history.forward() : 이후 페이지로 갈 수 있다.

javascript:history.go(page) : 원하는 만큼의 페이지로 이동할 수 있다.

page

양수 : 앞으로(forward를 원하는 만큼)

음수 : 뒤로(back을 원하는 만큼)

0 : 현재페이지 새로고침

---

##### 객체 생성

JavaScript는 class가 없다. 하지만 객체를 생성할 때 프로토타입으로 만들어서 class처럼 사용할 수는 있다.

이전에 공부한 방법으로는 new 키워드를 사용해 객체를 여러개 만들어 낼 수 없다.

사용자 정의 객체 선언

   function Point(xpos, ypos) {
	
	this.x = xpos;
	this.y = ypos;
	this.getDistance = function(){
	   return Math.sqrt(this.x* this.x + this.y * this.y);
	}

   }


객체 생성

   var p1 = new Point(10,20);
   var p2 = new Point(10,30); 


객체의 변수 접근

   p1.getDistance();
   p2.xpos = 50;
                                                                                                                                                                    
생성된 객체에 새로운 속성/메소드 추가


p1.turbo = 5;
p1.showModel = function(){
	alert("모델은" + this.model + "입니다.");
   }                                             

생성자를 변경할 필요없이 해당 객체만 추가해줄 수 있다.

물론 공통적으로 추가하고 싶으면 생성자를 수정하면 된다.

                                                                                 
---

##### 프로토타입

위의 예시에서 getDistance는 모든 객체에서 동일하게 작동하기 때문에 객체별로 따로 메모리 공간을 차지할 필요가 없다.

   function Point(xpos, ypos) {
	
	this.x = xpos;
	this.y = ypos;
	this.prototype.getDistance = function(){
	   return Math.sqrt(this.x* this.x + this.y * this.y);
	}

   }

prototype을 명시해주면 생성된 객체에서 getDistance를 공유한다.(java의 static 메소드가 된다.)

---

##### call by value / call by reference

javaScript에서 기본형/객체 타입을 파라미터로 넘겼을 경우 call by value가 된다.(java와는 다르다.)

하지만 배열을 파라미터로 넘기면 call by reference가 된다.(왠지는 모르겠다. 같은 객체인데..)


---

##### DOM(Document Object Model)

- HTML(JSP)문서의 구조를 트리로 표현한 것

- 이미 만들어져 있는 document 객체를 통해 HTML 요소들을 값을 확인, 조작할 수 있다.

- 한 페이지의 root node가 document고 그 밑으로 태그를 생성할 때마다 document객체의 key값이 추가된다고 생각하면 된다.

<div id="main">이것이 div 요소(element)입니다.</div>

element는 태그 안에 있는 자식태그까지 모두 포함된다.

var x = document.getElementById("main"); // id가 main인 element를 찾아서 반환(태그 그 자체를 반환한다고 생각하면 됨)

var x = document.getElementById("main").innerHTML; // id가 main인 element의 내용(내부에 작성되어 있는 태그 코드)을 출력

---

##### 입력 양식 찾기

<form> // document.forms[0]

	<input type="text" value=""> // document.form[0].elements[0]
	<input type="text" value=""> // document.form[0].elements[1]
	<input type="submit">
</form>


마찬가지로 form이 여러개라면 작성된 순서대로 인덱스를 부여받는다.

<form name="myForm"> // document.myForm
	<input type="text" id="target1" name="text1" value=""> // document.myForm.text1
	<input type="text" id="target2" name="text2" value=""> // document.myForm.text2
	<input type="submit">
</form>

name속성이 정의되어 있는 경우 인덱스 대신 name속성명으로 접근 가능하다.

---

##### element의 검색 / 변경

검색 : 메소드만 호출

변경 : 메소드 호출 = 변경할 값;

element의 내용(자식태그) 검색

document.getElementById("main").innerHTML; // id 값을 String으로 입력해야 한다.

element의 내용 변경

document.getElementById("main").innerHTML = "<div>hahahoho<div>";


element의 속성 값 검색

document.getElementById("main").속성명(ex)value,src,class,id 등)

element의 속성 변경

document.getElementById("main").속성명 = 새로운 속성 값

---

##### BOM(Browser Object Model)

DOM의 부모 개념

DOM은 웹사이트의 한 페이지

BOM은 페이지 간의 관계까지 포함

windows객체로 BOM의 메소드를 사용할 수 있다.

---

##### 정규표현식(다른 언어에서도 공통적으로 사용되니까 잘 알아두자)

- 문자열의 검색/치환을 위해 사용되는 수식

element.value.match(정규표현식) 의 형식으로 사용된다.

구성 : 메타문자(+수량한정자)

메타문자

^ : 문자열의 시작
$ : 문자열의 끝
. : 한 개의 문자와 일치
\d : 한개의 숫자와 일치
\w : 한 개의 문자나 숫자와 일치
\s : 공백, 탭, 줄 바꿈, 캐리지 리턴 문자와 일치
[] : 문자 종류, 문자 범위

/ : 하나의 정규 표현식을 묶는 단위, 한 문자열에 여러 표현을 사용해서 정규표현식을 만들 수 있다.

ex)

/abc/ : 정확히 "abc"와 일치

/./ : 한 자리의 문자

/\d\d\d/ : 3자리의 숫자

/[a-z]/ : a 부터 z 까지의 소문자 알파벳 한 글자


수량한정자 : 메타문제 '뒤'에 올 수 있다.

* : 0회이상 반복
+ : 1회 이상 반복
? : 0회 또는 1회
{m} : m회 이상
{m,n} : m회 이상 n회 이하
(ab) : 그룹화(정확히 이 표현식과 일치)


ex)	

		<form>
			<input type="text" id="user" />
			<input type="button" onclick="checkId(document.getElementById('user'))" value="확인" />	
		</form>
	
		function checkId(id) {
	
		   var exp1 = "[a-z0-9]+"; // 문자열 내에 포함되어 있으면 true가 나온다. ("ㅋㅋㅋasdas123ㅇㅇㅇ" 도 true를 반환한다.)
		   var exp2 = "^[a-z0-9]+$"; // 처음과 끝(String 내의 모든 문자)을 지정했기 때문에 숫자와 알파벳 소문자의 조합으로만 가능하다.
		   var exp = "^[a-z0-9]+"; // 해당 정규식으로 시작만 하면 된다.("dfajmk123ㅋㅋㅋ"는 true를 반환한다.)
		   var exp = "[a-z0-9]+$"; // 해당 정규식으로 끝나기만 하면 된다.("ㅋㅋㅋdfnakj123"는 true를 반환한다.)
	   
			}
	
	
		}

---

validate 플러그인에 정규표현식으로 vaildating하는 것 추가하기

addMethod 실행

        jQuery.validator.addMethod(
        		"regex",
        		function(value, element, regexp) {
        			console.log("value : ", value); // validating 할 문자열
        			console.log("element : ", element); // vaildating할 태그(ex)<input type="text" class="form-control"
								name="id" id="id" placeholder="아이디를 입력해주세요"
								style="width: 493px; height: 34px;" />)
        			console.log("regexp : ", regexp); // 정규표현식
       			if(regexp.constructor != RegExp)
        				regexp = new RegExp(regexp);
        			else if(regexp.global)
        				regexp.lastIndex = 0;
        			
        			return this.optional(element) || regexp.test(value); // test는 RegExp 객체에 있는 메소드

			// this는 validate 객체

        		}
        )


플러그인에 적용하기

        id:{required:true,
            minlength:4,
            remote: {
                    url:"/checkIDDup",
                    type:"POST",
                    data: {
                    	id : function() {
                           return $("#id").val();
                        }
                    }
              },
              regex : "^[0-9a-z]+$" // 이 부분, regex는 addMethod의 첫 번째 인자
        }

---

##### $(document).ready(function(){}) 과 $(function(){}); 은 실행되는 내용이 같다.

---

##### addEventListener

- event가 일어나는지 계속 듣고(listen) 있다가 event가 발생하면 메소드를 실행한다.


이벤트 종류

click : 클릭
change : value의 변동
focus : 포커스(커서)를 얻었을 때(<-> blur)
keydown : 키보드를 눌렀을 때
keyup : 눌렀던 키보드 버튼을 뗏을 때
load : 로드가 완료되었을 때
mousedown : 마우스를 클릭했을 때
mouseup : 마우스에서 손을 뗐을 때 (mousedown+up : click과 같다.)
mouseout : 마우스가 특정 객체 밖으로 나갔을 때
mouseover : 마우스가 특정 객체 위로 올려졌을 때
mousemove : 마우스가 움직였을 때

option 태그 등에서 선택을 했을 때는 change로 이벤트를 확인하면 된다.(select의 value가 change됐으니까, 내가 본 자료에서는 이벤트명이 select라고 되어있었는데 아니다.)


###### element.addEventListener

- 지정한 element에 대해서 event가 일어났을 때 메소드를 실행한다.

ex)

   document.getElementById("email").addEventListener("click", function(){// 실행내용}) // email을 id속성으로 가지는 element에서 click 이벤트가 일어났을 때 메소드를 실행한다.



###### document.addEventListener

- 페이지 내에 있는 모든 element에서 특정 event가 일어났을 때 메소드를 실행한다.

ex)

   document.addEventListener("change", function(){// 실행내용}); // 페이지 내에 있는 어떤 태그에서 change이벤트가 발생해도 메소드가 실행된다.


###### window.addEventListener

- 브라우저에서 특정 event가 일어났을 때 메소드를 실행한다.

ex)

   window.addEventListener("load", function(){ // 실행내용}); // 페이지가 로드되면 메소드가 실행된다.

   window.addEventListener("click", function(){ // 실행내용}); // 브라우저 내의 어떤 곳을 클릭하더라고 메소드가 실행된다.(빈 곳을 클릭해도 실행된다.)
   
---
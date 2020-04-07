#### 경로

절대경로

/ : 루트 디렉토리


상대경로

./ 또는 경로 미입력 : 현재 디렉토리

../ : 부모 디렉토리


* front 관련 파일들의 root 경로는 webapp이다.

ex)

/resources/~~


/WEB-INF/views/~~

---


#### JSTL : JSP의 출력문법을 대체하는 언어

jsp파일에 작성하고 태그로 작성하지만 서버에서 실행되는 언어다.

아주 이기적인 언어이기 때문에 JSTL문법으로 이루어진 태그'만' 확인한다.

ex)

		<c:forEach begin="+pageMaker.startPage+" end="+pageMaker.endPage+" var='idx'>

만 쏙 빼내서 인식하기 때문에(맨앞의 pagingHTML += "  맨 뒤의 "; 은 무시한다.)

begin 속성을 +pageMaker.startPage+

end 속성을 +pageMaker.endPage+

로 봤기 때문에 이게 숫자가 아니니까 NumberFormatException이 발생한다.

에러는 자바(서버)에서 발생한 오류다. 그렇기 때문에 서버에서 발생한 오류라고 생각하고 접근해야 한다.

JSTL은 동적으로(변수를 사용해서) 만들지 말고 그 자체로 사용해야 한다.

javaScript 말고 그냥 jsp파일에서 태그에서 bean 객체로 사용하는 것은 controller에서 넘어오면 그대로 상수를 갖다 쓰는 것이기 때문에 동적으로 쓰이는 것은 아니다.

위의 예시처럼 중간중간에 변수를 넣기 위한 +,"(따옴표) 와 같은 것을 그대로 인식해버리기 때문에 제대로 작동하지 않는다. 

이러한 경우가 동적으로 사용된 것이다.

	if(true)
	   pagingHTML += "<c:if test='true'><a>haha</a>";
	else
	   pagingHTML += "<c:if test='false'><a>hoho</a>";

pagingHTML += </c:if>;

이 경우에도 if(true), else, 세번의 pagingHTML += 와 ;(세미콜론) 을 무시하고 태그만 보는 것이다.

그러면 </c:if> 태그가 하나 부족하기 때문에 

org.apache.jasper.JasperException : unterminated [&lt;c:if] tag

라는 서버단의 에러가 발생한다.

이 경우도 동적으로 사용한 것이라고 볼 수 있지 않을까??

javaScript에서 오류가 발생한다면 보통 해당 기능만 비활성화 된 상태로 정상적으로 돌아간다.

F12번을 눌러 오류난 곳을 확인해야 한다.

##### c(core 태그)

<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core"%>

을 jsp파일 상단에 명시하고

pom.xml에도 jstl을 maven repository에서 가져와 작성하고

		<dependency>
			<groupId>javax.servlet</groupId>
			<artifactId>jstl</artifactId>
			<version>1.2</version>
		</dependency>

WEB-INF/lib 폴더에도 jstl-1.2.jar를 넣어줘야 한다.

###### forEach

for문과 같이 사용할 수 있다.

사용법 1

ex)

	<c:forEach var="index" begin='1' end='5'>
		<div>${index}</div>
	</c:forEach>
	
결과

	<div>1}</div>
	<div>2</div>
	<div>3</div>
	<div>4</div>
	<div>5</div>
	
	
begin과 end를 모두 포함한다.(1~5까지)

 사용법 2
 
	<c:forEach var="reviewVo" items="${bean}">
		<div>${reviewVo.reviewIndex}</div>
		<div>${reviewVo.title}</div>
		<div>${reviewVo.content}</div>
	</c:forEach>

controller로부터 받은 데이터를 반복문을 통해 태그에 넣을 수 있다.

###### if

<c:if test="조건문">
	// 조건이 true일 경우 실행 내용
</c:if>

ex)

	<c:if test="${mainImage.imageName != null }">
	
		// 실행되는 내용
		
	</c:if>

else를 사용할 수 없다.(<c:choose>태그를 사용해야한다.)

---

###### choose : if문에서 사용할 수 없는 else문의 기능을 사용할 수 있다.

<c:choose>
   <c:when test="조건1">
	실행문
   </c:when>

   <c:when test="조건2">
	실행문
   </c:when>

   <c:otherwise> // else와 같은 의미
	
   </c:otherwise>
</c:choose>


##### fmt 태그

숫자, 날짜, 시간 등을 원하는 대로 formmatting 할 수 있다.

	<%@ taglib prefix="fmt" uri="http://java.sun.com/jsp/jstl/fmt"%>

를 jsp파일 상단에 명시해야 한다.(uri에는 공백이 들어가면 안된다.)


사용법

	<fmt:태그종류 속성들 />



---

#### 비교연산자

* eq(==) : 문자열 또는 숫자가 같으면 참입니다. null 또는 빈 문자열 인지도 확인할 수 있습니다.

- <c:if test="${name == '홍길동'}">

- <c:if test="${name eq '홍길동'}">

- <c:if test="${name == null}">

- <c:if test="${name eq null}">

- <c:if test="${num == 5}">

- <c:if test="${num eq 5}">



* ne(!=) : 문자열 또는 숫자가 다르면 참입니다.

- <c:if test="${name != '홍길동'}">

- <c:if test="${name ne '홍길동'}">

- <c:if test="${num != 5}">

- <c:if test="${num ne 5}">



* empty : List 또는 배열이 비어있거나, 문자열이 null 또는 빈 문자열이면 참을 반환합니다. 숫자 0은 eq(==) 로 비교해야 합니다.

- <c:if test="${empty name}">



* not empty : List 또는 배열이 비어 있지 않을 경우, 문자열이 값이 있을 경우 참을 반환합니다.

- <c:if test="${not empty name}">



3. 논리연산자



비교연산자의 조합으로 논리 연산을 할 수 있는 논리연산자 입니다.



* and (&&) :  모두 참일때 참이 됩니다.

- <c:if test="${a > b and c < d}">

- <c:if test="${a > b && c < d}">



* or (||) : 둘중 하나라도 참이면 참이 됩니다.

- <c:if test="${a > b or c < d}">

- <c:if test="${a > b || c < d}">



* not (!) : 논리를 반전합니다.

- <c:if test="${not a == ''}">

- <c:if test="${! a == ''}">



* 괄호를 사용하여 논리연산의 우선 순위를 지정할 수 있습니다.

- <c:if test="${a > b && (b > c || d < e)}">


---

###### c 태그 종류

forEach : 배열이나 컬렉션 또는 map과 같은 집합체에 저장되어 있는 값들을 순차적으로 처리할 때 사용하는 태그

varStatus속성

index : items에서 지정한 집합체의 현재 반복 중인 항목의 index를 알려준다.(0부터 시작)

count : 반복문을 돌 떄 현재 몇 번째를 반복중인지 알려준다.(1부터 시작)

first : 현재 반복문이 처음인지 여부를 알려준다(boolean)

end : 현재 반복문이 마지막인지 여부를 알려준다(boolean)

begin : 반복에 사용될 것 중 첫 번째 항목의 index

end : 반복에 사용될 것 중 마지막 항목의 index

ex) 

직접 사용해보고 쓰자

---

jsp 파일 동적/정적 include

정적

	<%@include page="JSP file's path">

: 소스를 가져와 컴파일한다.



동적

	<jsp:include page="jsp file's path"/></jsp:include>

: 컴파일 된 이후 페이지로 가져온다.

---

##### EL(Expression Language)

##### pageContext 

	${pageContext.request.contextPath}

: server.xml 파일에 설정한 context의 path속성을 읽어온다.

: local 디렉토리의 workspace폴더에 있는 webapp(local 디렉토리의 workspace/src/main/webapp)을 root로 한다.

controller에서 실행한 

	servletRequest.getSession().getServletContext().getRealPath("/");
	
와 같은 디렉토리를 리턴한다.(HttpServletRequest / MultipartHttpServletRequest 모두 동일한 값이 나온다.)

path를 / 으로 설정한 경우

그 하위 폴더를 정확히 작성해야 정상적으로 mapping이 된다.

ex)

	href="${pageContext.request.contextPath}/resources/css/clndr.css?version=1
	
	
${pageContext.request.scheme}: http

${pageContext.request.serverName}: localhost

${pageContext.request.serverPort}: 8080

---
##### 경로

절대경로

/ : 루트 디렉토리)


상대경로

./ : 현재 디렉토리

../ : 부모 디렉토리


* front 관련 파일들의 root 경로는 webapp이다.

ex)

/resources/~~


/WEB-INF/views/~~

---


##### JSTL : JSP의 출력문법을 대체하는 언어

c(core 태그)

###### forEach

for문과 같이 사용할 수 있다.



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

---



###### 비교연산자

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

path를 / 으로 설정한 경우

그 하위 폴더를 정확히 작성해야 정상적으로 mapping이 된다.

ex)

	href="${pageContext.request.contextPath}/resources/css/clndr.css?version=1
	
	
${pageContext.request.scheme}: http

${pageContext.request.serverName}: localhost

${pageContext.request.serverPort}: 8080

---
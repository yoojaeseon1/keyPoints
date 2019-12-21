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

if

<c:if test="조건문">
	// 조건이 true일 경우 실행 내용
</c:if>

else를 사용할 수 없다.

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
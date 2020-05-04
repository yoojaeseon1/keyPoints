##### js파일 실행 안될 때

	<script
	src="${pageContext.request.contextPath}/resources/js/header_js/member_login.js?ver=10"></script>
	
와 같이 ver=숫자를 바꿔가면서 넣어주고

그래도 안되면 해당 jsp파일에 직접 script를 작성하자

---

##### ajax통신의 type을 DELETE,PUT,PATCH 으로 했을 때 controller에서 null 값을 받는 오류

java.lang.IllegalStateException: Optional int parameter 'reviewIndex' is present but cannot be translated into a null value due to being declared as a primitive type. Consider declaring it as object wrapper for the corresponding primitive type.

톰캣의 server.xml에서 

<Connector connectionTimeout="20000" port="8080" protocol="HTTP/1.1" redirectPort="8443" URIEncoding="UTF-8" parseBodyMethods="POST,PUT,DELETE,PATCH"/>

Connector 태그에 parseBodyMethods="POST,PUT,DELETE,PATCH" 를 추가해주면 된다.

---
##### 지금 사용하고 있는 Spring은 4버전

STS가 3버전인거다.

-----

##### 인코딩 방식 변경(UTF-8로)

window -> Preferences -> General -> Appearance -> Content Type 

-> Text클릭한 상태에서 맨 밑 Default encoding : UTF-8 쓰고 Update


.java 파일 중에 default 인코딩 방식이 바뀌지 않은 것들이 있으면

Content Type -> Text-> Java Source File의 인코딩 방식을 변경해주면 된다.

---

##### HTTP 메소드

GET : select

POST : insert

PUT : update(전부)

PATCH : update(일부분)

DELETE : delete

-----

##### Controller/Service/DAO/VO의 관계

DAO에서 SqlSession 인스턴스를 통해 Mapper.xml에 접근해서 쿼리문의 값을 가져온다.

Mapper의 쿼리문에서 #{변수명}은 해당 변수의 getter 메소드를 실행해 값을 가져오는 것이다.

Service에서 DAO에서 가져온 값을 반환하는 메소드를 작성한다.

Controller에서 Service 인스턴스를 통해 쿼리문의 값을 뷰로 넘겨준다.


정리

VO의 getter 메소드 <-> Mapper <-> DAO(@Repository) <-> Service(@Service) <-> Controller(@Controller(@RestController)) <-> View
 
-----
##### controller 클래스 위의 RequstMapping("path")

 : path로 시작하는 페이지 일 경우 이 컨트롤러를 실행한다.


redirect 하는 이유 : 하지 않으면 완료페이지에서 새로고침 할 경우 해당 액션이 계속 반복된다.(게시물 도배 등)

redirect 할 경우 controller의 메서드에서 Model 대신 RedirectAttributes rttr를 인자로 넣고

rttr.addFlashAttribute("msg", "success");

를 해준다 Flash를 할 경우 url에 표시되지 않는다.(redirect시점에 한번만 사용되는 데이터를 전송할 수 있게 한다.)

-----

##### mapper.xml에서

sql문을 작성할 때 #{page} 같은 동적 sql문은 page 속성의 getter인 getPage()함수를 호출하는 것이다.

jsp 페이지에서 ${page}도 똑같이 getPage()를 호출한다.

<![CDATA[ sql문 ]]> 를 쓰는 이유는 sql문에 <, >, & 같은 특수문자를 쓸 경우 에러가 발생하기 때문이다.(근데 나는 에러 안나는데..?)


-----

##### paging

paging은 get방식으로만 처리한다(다른 사람에게 URL로 전달하는 경우가 많기 때문에)

-----

##### model.addAttribute()를 해야만 jsp파일에서 해당 attribute를 가져다 쓸 수 있다.

-----

##### servlet-context에 <context:component-scan base-package="com.bit.yes" /> 를 추가해야 정상적으로 빈 객체를 찾을 수 있다.

com.bit.yes 하위에 있는 controller, DAO, service 객체를 찾을 수 있다.(하위 디렉토리에 모두 포함 시킬 수 있는 디렉토리로 지정해야 한다.)

-----

##### Response Header 확인하는 방법

웹 페이지 > F12 > network > 원하는 header 클릭해서 확인


-----

##### VO 인스턴스를 그대로 반환하면 toString()메소드가 실행되어 필드 값들이 JSON타입으로 반환된다.


		<dependency>
			<groupId>com.fasterxml.jackson.core</groupId>
			<artifactId>jackson-databind</artifactId>
			<version>2.8.4</version>
		</dependency>

를 pom.xml에 추가하여 인스턴스를 JSON타입으로 데이터를 변환하거나 반대의 작업을 하게 해준다.


-----

##### URI, URL

URL(Uniform Reource Locator) : Resource의 위치를 나타낸다.

URI(Uniform Resource Identifier) : 모든 정보의 Resource를 가리키는 식별자이다.

-----

##### 댓글 처리

JSON형식으로 보낼 때는 VO객체 있는 필드명으로 key값을 지정해야 한다.(테이블의 속성 값이 아니라(물론 똑같겠지))

{"bno":"10", "replyText":"댓글을 추가합니다.","replyer":"user00"}

필드 값 : bno, replyTest, replyer


-----

##### ResponseEntity 클래스

사용자에게 전송하는 데이터 + HTTP상태메세지(200 OK, 404 Not Found 등)을 함께 보내 더 자세한 정보를 얻고 싶을 때 사용한다.

entity = new ResponseEntity<>(service.listReply(bno), HttpStatus.OK); // 인자로 (보내고자 하는 데이터, HTTP 상태메세지) 를 입력했다.

return entity; // 데이터 + HTTP상태 메세지를 받을 수 있다.(데이터만 보내려면 ResponseEntity를 사용하지 않아도 된다.)


-----


##### HiddenHttpMethodFilter

GET/POST방식만을 지원하는 브라우저에서 REST방식을 사용할수 있도록 만드는 필터

web.xml에 설정을 추가해줘야 한다.

추가할 내용

	<filter>
		<filter-name>hiddenHttpMethodFilter</filter-name>
		<filter-class>org.springframework.web.filter.HiddenHttpMethodFilter</filter-class>
	</filter>
	<filter-mapping>
		<filter-name>hiddenHttpMethodFilter</filter-name>
		<url-pattern>/*</url-pattern>
	</filter-mapping>




-----

##### DAOImpl 에서 

session.selectList(namespace+".listPage", paramMap);

listPage : mapper에서 설정한 쿼리문의 id

paramMap : mapper의 쿼리문에서 사용하는 변수/자료구조

ex) 	

	<select id="listPage" resultType="ReplyVO">
		select
		*
		from 
		tbl_reply
		where
		bno = #{bno}
		order by rno desc
		limit #{cri.pageStart}, #{cri.perPageNum}
	</select>


// #{bno}, #{cri.pageStart}, #{cri.perPageNum}을 session으로부터 넘겨받아서 사용한다.


-----

##### REST(Representational State Transfer) 방식

- ★특정한 URI는 반드시 그에 상응하는 데이터 자체★라는 것을 의미

ex) /boards/123 : 게시물 중 123번이라는 고유한 의미(GET/POST 방식 모두 사용)

REST API : REST방식으로 제공되는 외부 연결 URI

Restful하다. : REST방식으로 서비스가 가능하다.

기능적으로는 REST방식(@RestController)과 이전의 방식(@Controller)의 차이는 거의 없지만 컨트롤러 자체의 용도를 지정한다는 점에서 변화가 있다.

-----

태그에 문제가 생겼을 때는 브라우저에서 F12를 눌러 Console에 오류가 발생했는지 확인하자(오타, 문법오류 등)

-----

##### Restlet Clinet

REST방식으로 JSON 데이터를 다양한 방식(GET,POST,PUT,PATCH,DELETE)으로 정상적으로 전송이 되는지 확인할 수 있다.

-----

##### 경로 입력할 때

"/"로 시작 : 절대경로


"/"로 시작 X : 상대경로(현재 view가 있는 페이지 + "/" +  입력한 경로)


-----

##### 비즈니스 : 고객이 사용하는 기능


AOP(Aspect Oriented Programming) 관련 용어들

- Aspect : 공통관심사에 대한 추상적인 명칭, 고객이 사용하는 비즈니스와는 직접적으로 관련은 없으나 비즈니스의 성능,보안 등과 관련이 있다.

ex) 로깅, 보안, 트랜잭션

- Advice : 실제로 기능을 구현한 객체(@Aspect를 적용하여 개발자가 제작한 코드)

- Join points : 공통관심사를 적용할 수 있는 대상. Spring AOP에서는 각 객체의 메소드가 이에 해당

- Pointcuts : 여러 메소드 중 실제 Advice가 적용될 대상 메소드

- target : 대상 메소드를 가지는 객체

- Proxy : Advice가 적용되었을 때 만들어지는 객체

- Instruction : target에는 없는 새로운 메소드나 인스턴스 변수를 추가하는 기능

- Weaving : Advice와 target이 결합되어서 Proxy객체를 만드는 과정


-----

##### Advice의 종류

Before Advice : target의 메소드 호출 전에 적용

After returning : target의 메소드 호출 이후에 적용

After throwing : targe의 예외 발생 후 적용

After : target의 메소드 호출 후 예외의 발생에 관계없이 적용

★Around : target의 메소드 호출 이전과 이후 모두 적용(메소드 호출 자체를 제어할 수 있음. 가장 광범위하게 사용됨)



-----

##### 트랜잭션의 처리

트랜잭션의 4가지 속성(ACID)

- 원자성(Atomicity) : A와 B로 구성된 트랜잭션의 결과로는 A,B 둘다 적용되거나, 둘다 적용되지 않거나 여야 한다.(다 되거나 다 안되거나)

- 일관성(Consistency) : 트랜잭션이 성공했다면 DB의 모든 데이터는 일관성을 유지해야 한다. 

트랜잭션으로 처리된 데이터와 일반 데이터 사이에는 전혀 차이가 없어야 한다.

- 격리(Isolation) : 트랜잭션이 처리되는 중간에 외부에서의 간섭이 없어야 한다.

- 영속성(Durability) : 트랜잭션이 성공적으로 처리되면, 그 결과는 영속적으로 보관되어야 한다.


원자성이 트랜잭션의 성격을 가장 잘 표현한 용어다.


-----

##### 파일 업로드

- 파일 업로드가 되는 url과 맵핑되는 메소드의 인자로 MultipartFile을 받으면

 웹 페이지에서 POST방식으로 전송했을 때 자동으로 메소드와 파일(MultipartFile 인스턴스)이 맵핑된다.

ex) 

	@RequestMapping(value="/uploadForm", method = RequestMethod.POST)
	public String uploadForm(MultipartFile file, Model model) throws Exception {
	
		logger.info("originalName : " + file.getOriginalFilename());
		logger.info("size : " + file.getSize());
		logger.info("contentType : " + file.getContentType());
		
		String savedName = uploadFile(file.getOriginalFilename(), file.getBytes());
		
		model.addAttribute("savedName", savedName);
		
		return "uploadResult";
		
	}

-----

##### Controller의 메서드에서 String형 리턴 값은 model에서 가져온 데이터를 해당 페이지에 전송해주는 역할이다.

ex)

return "uploadResult"; // uploadResult.jsp로 데이터를 전송한다.

리턴 값이 entity일 경우에는??


-----

##### MIME(Multipurpose Internet Mail Extensions) Type : 전자우편을 위한 인터넷 표준 포맷

- 전송되는 데이터의 타입 또는 전송되는 파일의 확장자

- 데이터와 함께 올바른 MIME 타입을 전송하도록 서버에서 정확히 설정해야 한다.

- 전통적으로 소문자로 쓴다.

- 웹 개발에서 자주 쓰이는 타입

application/octet-stream : 이진 파일을 위한 기본 값

text/plain : 텍스트 파일에 대한 기본 값

image/gif,jpeg,png,svg+xml : 이미지 타입 

multipart/form-data : 브라우저에서 서버로 HTML Form 태그의 내용을 전송 할 때 사용


-----

##### Controller의 메소드

entity = ResponseEntity<>("SUCCESS", HttpStatus.OK);

return entity



JSP파일의 ajax

.$ajax({

...

success:function(result)){
   // executed statement
}
});


에서 HTTP 상태코드가 200 OK 일때 

ajax의 result는 Contoller의 메서드에서 리턴한 "SUCCESS"가 된다.

-----

##### HandlerInterceptorAdapter 클래스(session을 활용해 로그인 처리를 할 수 있다.)

preHandle(request, response, handler) : 지정된 컨트롤러의 메소드가 실행되기 전에 가로채는(실행되는) 역할

postHandle(result, response, handler, modelAndView) : 지정된 컨트롤러의 메소드가 실행되고 view에 반영되기 전에 가로채는(실행되는) 역할

-----

##### EL문법의 검색 경로

page(JSP 페이지) -> request -> session -> application

-----

##### VO와 DTO

공통점 : 데이터의 수집과 전달에 사용할 수 있다.

차이점

VO(Value Object) : DB와 거리가 가깝다.(테이블의 구조를 이용해 작성되는 경우가 많다.)

DTO(Data Transfer Object) : 화면과 가깝다.(화면에서 전달되는 데이터를 수집하는 용도로 사용하는 경우가 많다.)

Spring MVC에서는 Controller에 전달되는 데이터를 검증하는 기능을 별도의 DTO를 구성해서 사용한다.

-----

##### JSP에서 사용하는 EL은 자동으로 HttpSession에 있는 attribute을 찾기 때문에 

addAttribute()를 하지 않아도 JSP파일에서 바로 사용할 수 있다.

-----

##### 쿠키

개발자도구 -> Application -> Cookies 에서 확인

JSESSIONID(세션 쿠키) : Tomcat에서 발행된 세션쿠키(브라우저가 실행 될 때 만들어지고 종료할 때 제거된다.(서버 on/off가 아니라))

__cfduid(공유기 환경에서의 쿠키 id, 고정IP인 경우 지정한 쿠키의 아이디로 명시된다.) 

 : IP공유(공유기) 환경에서 로그인을 통해 cookie를 생성했을 때의 cookie의 id

cookie의 아이디를 지정했더라도 공유기 환경에서는 cookie의 아이디가 __cfduid로 잡힌다.

브라우저를 종료해도 cookie.setMaxAge(seconds) 만큼 서버에서 유지되기 때문에 아이디는 해당 시간만큼 유지된다.


-----

##### controller의 파라미터로 VO(DTO)객체를 받았을 때

form으로부터 전송받는 태그의 id가 VO(DTO)객체의 필드와 일치할 경우 자동으로 바인딩 된다.


ex)

login.jsp

<form action="/user/loginPost" method="post">
	<div class="form-group has-feedback">
		<input type="text" name="uid" class="form-control" placeholder="USER ID"/>
		<span class="glyphicon glyphicon-lock form-control-feedback"></span>
	</div>
	<div class="form-group has-feedback">
		<input type="password" name="upw" class="form-control" placeholder="Password"/>
		<span class="glyphicon glyphicon-lock form-control-feedback"></span>
	</div>
	<div class="row">
		<div class="col-xs-8">
			<div class="checkbox icheck">
				<label>
					<input type="checkbox" name="useCookie"> Remember Me
				</label>
			</div>
		</div>
		<div class="col-xs-4">
			<button type="submit" class="btn btn-primary btn-block btn flat">Sign in</button>
		</div>
	</div>
</form>


UserController.java

	@RequestMapping(value="/loginPost", method=RequestMethod.POST)
	public void loginPOST(LoginDTO dto, HttpSession session, Model model) throws Exception{
		
		
		logger.info("dto : " + dto.toString());

	}


출력

INFO : org.zerock.controller.UserController - dto : LoginDTO [uid=user02, upw=user02, useCookie=false]

-----

##### 매핑(mapping)

Java 오브젝트 모델을 XML 문서 표현 (또는 그 반대)으로 나타내는 것일뿐이다.

매핑 도구를 사용하면 한 형식에서 다른 형식으로 변환 할 수 있습니다(단순히 정의, VO객체에 초기화 되지 않는다.)

-----

##### 바인딩(Binding)

응용 프로그램이 실행 중일 때 메모리 내에서 XML 문서를 객체 represantation으로 변환하는 프로세스다.(ex) VO객체에 일치하는 필드 값에 초기화)

-----

##### REST 방식 규칙

https://meetup.toast.com/posts/92


Rest방식은 @Controller처럼 controller에서 JSP파일(view)을 반환하는 것이 아니라

데이터 자체를 반환하는 것이다.

JSON타입의 데이터를 ajax방식으로 보낼 때 유용(댓글달기)

-----

##### HttpServletRequest의 getParameter(parameter) vs getAttrubute(parameter)

###### getParameter

JSP파일에서 <form> 태그안에 전송하는 태그에서 name이 parameter와 일치하는 값을 가져온다.


###### getAttribute

JSP파일의 스크립트릿에서 setAttribute("attribute", value) 를 통해 설정된 value값을 가져온다.

---

##### model.addAttribute / session.setAttribute 된 값 

모두 jsp파일에서 ${atrribute명}으로 가져올 수 있다. model과 session의 atrribute명이 겹치치 않게 코딩하자


---

##### ajax통신에서의 model.addAttribute()

ajax통신을 하는 controller의 메소드에서 model.addAttribute()를 해도 해당 페이지에서 적용된 attribute의 데이터를 사용할 수 없다.

model.addAttribute()를 하고 return "해당 페이지" 가 되야 하는데 해당 페이지로 데이터만 전송되는 거니까 addAttribute가 의미가 없다.


ex)

	@ResponseBody
	@RequestMapping(value = "/review_list/reviewLike", produces = "application/json; charset=utf-8")
	public ResponseEntity<String> showReviewLikeCount(HttpSession session, Model likeModel) throws SQLException {

		// 중략

		likeModel.addAttribute("userID", id); // 했지만 ajax통신을 통한 데이터가 전송된 페이지에서 사용할 수 없다.


		HttpHeaders responseHeaders = new HttpHeaders();
		List<Map<String, Object>> likeList = new ArrayList<>();
		Map<String, Object> temp = new HashMap<>();

		temp.put("likeCount", likeCount);
		temp.put("checked", bean.isChecked());

		likeList.add((Map<String, Object>) temp);

		JSONArray json = new JSONArray(likeList);

		return new ResponseEntity<String>(json.toString(), responseHeaders, HttpStatus.CREATED);
	}

json.toString()을 데이터로 보내는 것이지 return을 통한 페이지의 이동은 없기 때문에 model.addAttribute()는 무용지물이다.

---

##### local workspace의 디렉토리

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

##### 메소드의 return type

###### String

JSP파일(view)의 경로.

return 값 마지막에 .jsp를 붙여서 view 파일을 찾는다.

controller의 메소드에서 return하는 view 파일의 디렉토리는

루트가 /WEB-INF/views 이다.

return 다음에 오는 경로는 views를 기준으로 그 밑의 디렉토리를 명시하면 된다.

ex)

	return review/review_detail;
	
review_detail.jsp파일을 찾는다.(마지막에 .jsp를 붙여서 view파일을 찾는다.)

	return review/review_detail/;
	
review_detail/.jsp 파일을 찾기 때문에 없으면 오류가 난다.

---

###### URL로 이동하고 싶은 경우(jsp파일말고)



	return "forward:" + URL // 이동하는 URL의 controller 메소드에서 현재 메소드가 가지고 있는 request parameterrequest.getParameter()를 통한 쿼리스트링 사용을 할 수 있다.

또는

	return "redirect:" + URL // 이동하는 URL의 controller 메소드에서 현재 메소드가 가지고 있는  request parameter(request.getParameter()를 통한 쿼리스트링 사용)를 사용할 수 없다.


참고 사이트 : https://wondongho.tistory.com/65


---	

###### void

@RequestMapping(value="URI")

에 사용되는 URI과 view의 이름(return type이 String일 때의 return value)이 같을 경우에 사용할 수 있다.

---

##### request.getParameter("parameter")

GET/POST 방식으로 파라미터 값이 넘어올 때 그 값을 사용 할 수 있다.

@RequestParam("parameter")로 값을 가져오는게 더 편할 수 있다.

---

##### request.getAttribute("attribute")

page, request, response, session, application 과 같은 스코프 영역에서 값을 가져온다.

setAttribute된 attribute를 가져오는 것이 아닐까??

@ModelAttribute("attribute")로 가져오는게 더 편할 수 있다.

---

##### 현재 페이지의 URL 주소 가져오기

아래와 같은 주소가 있을 경우

http://localhost:8080/logout

INFO : com.bit.yes.controller.LoginController - URI : /logout
INFO : com.bit.yes.controller.HomeController - Welcome home! The client locale is ko_KR.
INFO : com.bit.yes.controller.LoginController - URL : http://localhost:8080/logout
INFO : com.bit.yes.controller.LoginController - contextPath : 
INFO : com.bit.yes.controller.LoginController - servletPath : /logout
INFO : com.bit.yes.controller.LoginController - before page : http://localhost:8080/

---



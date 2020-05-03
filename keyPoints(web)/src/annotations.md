#### @Autowired

의존성 주입을 Spring Container가 자동으로 해주도록 한다.

DAO / Service 인터페이스 등을 따로 구현한 클래스의 인스턴스로 초기화 하지 않아도 자동으로 의존성을 주입해준다.

선언한 인터페이스 별로 각각 @Autowired를 달아줘야 한다.




밑에 설명은 예전에 써둔 것인데 뭔 말인지 모르겠다.

 : 의존성 주입(get/set메서드를 만들지 않아도 설정파일을 통해 알아서 get/set 접근 메서드 대신 일을 해준다.)
	     root-context.xml의 namespace에서 context를 체크해줄 경우 사용할 수 있다.
	     (https://expert0226.tistory.com/195)

Spring에서 필요할 때 객체를 생성해서 사용할 수 있도록 하는 것이기 때문에 각각의 객체 별로

@Autowired를 달아줘야 한다.



-----


#### @RequestMapping(param) : param으로 시작하는 URI에 접근하면 해당 Controller 또는 Controller의 메소드를 실행한다.

Controller의 맨위에 있는 경우 - controller에 있는 모든 메소드의 requestMapping(value="URI") 일때

 URI 앞에 controller 맨위에 있던 @RequestMapping의 value를 추가해준다.

ex) 

	@RequestMapping("/sample")
	public class SampleContoller{
	
	}


Controller 내부의 메소드에 있는 경우 - Controller 맨위의 param/메소드에 mapping 되어있는 param 인 URI에 접근

ex) @RequestMapping("/list") : /sample/list 에 접근할 경우 해당 메소드 실행

controller 맨 위에 


ex)
@RequestMapping(value = "/all/{bno}", method = RequestMethod.GET)
	public ResponseEntity<List<ReplyVO>> list(@PathVariable("bno") Integer bno) {

	// executed statement
}

: {bno}는 해당 위치에 오는 URL을 bno로 인식하고 @PathVariable("bno")를 통해 Integer bno 변수에 초기화 하기위한 목적으로 사용한다.


속성

- value : 맵핑되는 URI

- method : 맵핑되는 전송방식(비울 경우 URL에 접근하는 모든 방식에서 해당 메소드가 실행된다.)

- produces : controller -> jsp로 전송하는 데이터(return 값)의 형식을 지정

produces = "text/plain;charset=UTF-8" // 리턴 타입이 String

produces = "application/json;charset=UTF-8" // 리턴타입이 Json



---

#### @RequestParam(param) 

URL의 쿼리스트링 값을 가져올 때 사용(1:1로 파라미터를 가져올 때, @PathVariable이랑 헷갈리지 말자)

- 메소드의 파라미터안에서만 사용할 수 있다.(메소드의 실행문에서는 사용 불가)



- parameter가 배열일 경우 이름 옆에 []까지 입력해야 한다.

ex) 

	@RequestParam("files[]") String[] files


---

#### @PathVariable

REST방식으로 URL에서 필요한 값을 가져올 수 있도록 해준다.

ex)

	@RequestMapping(value = "/review_list/{index}", method = RequestMethod.GET)
	public String showReviewDetail(@PathVariable int index, Model detailModel, Model mainModel, Model subModel)
			throws SQLException {

		detailIndex = index;	
		
		detailModel.addAttribute("bean", service.selectPage(index));
		mainModel.addAttribute("mainImage", service.reviewMainImage(index));
		subModel.addAttribute("subImages", service.reviewSubImage(index));
		return "review/review_detail";
	}

URL에서 index에 해당하는 값을 변수 index에 초기화 해준다.


-----


#### @ModelAttribute


model.addAttribute의 기능을 해주는 어노테이션이다.

	public String listReview(ReviewVo reviewVo, Model listModel, Model imageModel, HttpServletRequest request) throws Exception {

		reviewVo.setContent("hahahoho");	

		return "review/review_list";
	}


// 또는

	public String listReview(@ModelAttribute ReviewVo reviewVo, Model listModel, Model imageModel, HttpServletRequest request) throws Exception {

		reviewVo.setContent("hahahoho");	

		return "review/review_list";
	}



할 경우

	model.addAttribute("reviewVo", reviewVo);
	
가 실행된 것과 같다.

review_list.jsp 페이지에서 ${reviewVo.content} 로 값을 가져올 수 있다.(@modelAttribute의 인자를 적지 않으면 어노테이션을 안쓴 것과 동일하게 실행된다.)


	public String listReview(@ModelAttribute("reviewInfo") ReviewVo reviewVo, Model listModel, Model imageModel, HttpServletRequest request) throws Exception {

		reviewVo.setContent("hahahoho");	

		return "review/review_list";
	}

할 경우

	model.addAttribute("reviewInfo", reviewVo);
	
가 실행된 것과 같다.

review_list.jsp 페이지에서 ${reviewInfo.content} 로 값을 가져올 수 있다.


---


#### @RestController

REST(Representational State Transfer)방식

- ★특정한 URI는 반드시 그에 상응하는 데이터 자체★라는 것을 의미

ex) /boards/123 : 게시물 중 123번이라는 고유한 의미(GET/POST 방식 모두 사용)

REST API : REST방식으로 제공되는 외부 연결 URI

Restful하다. : REST방식으로 서비스가 가능하다.




-----

#### @RequestBody

전송된 JSON 데이터를 VO객체로 변환해 준다.(@ModelAttribute와 유사한 역할을 하지만 JSON에서 사용된다는 것이 차이점)

JSON타입으로 데이터를 받아야 하기 때문에 JSP파일에서 ajax($.ajax)방식으로 데이터를 전송한다.(POST방식($.post)이 아니라)

-----

#### @ResponseBody

- ajax통신을 할 때 controller에서 jsp로 보내기 위해서는 해당 메소드에 입력해야한다.

jsp -> controller의 메소드는 @ResponseBody가 없어도 되지만 controller의 메소드 -> jsp로는 불가능하다.

- 자바 객체를 HTTP 응답 body로 전송함

- 자바 객체를 HTTP 요청의 body 내용으로 매핑하는 역할

- 파일 전송의 경우 byte[]로 되어있는 파일 데이터를 그대로 전송하기 위해 사용한다.

-----

#### @PathVariable(@RequestMapping과 같이 사용)

URI의 경로에서 원하는 데이터를 추출하는 용도로 사용

메소드 위의 @RequestMapping(value="/{bno}")했을 때

인자에서 (@PathVariable("bno") Integer bno) 와 같은경식으로 path의 값을 가져올 수 있다.

REST방식으로 URL의 값을 가져올 때 사용한다.

-----

#### @Aspect

AOP 기능을 하는 클래스의 선언에 추가해줘야 한다.

-----

#### @Component

Spring의 빈으로 인식되도록 해준다.


-----

#### @Before

해당 메소드를 먼저 실행한 후 target메소드가 실행되도록 해준다.(AOP의 종류 중 Before Advice)

ex)

@Before("execution(* org.zerock.service.MessageService*.*(..))")
public void startLog(JoinPoint jp) {
		
	logger.info("---------------");
	logger.info("---------------");
	logger.info(Arrays.toString(jp.getArgs()));
		
		
}

execution으로 시작하는 구문은 Pointcut을 지정하는 문법으로, AspectJ 언어의 문법을 사용한다.

'org.zerock.service.MessageService'로 시작하는 모든 클래스의 '*'(모든) 메소드를 지정하고 있다.


STS에서는 AOP의 설정이 완료되면 모든 메소드에 화살표아이콘이 표시된다.


-----


#### @Around

메소드가 실행 된 전후(2번)로 Advice가 적용된다.

"@Before"와는 달리 인자로 ProceddingJoinPoint 인스턴스를 인자로 받고 Exception보다 상위인 Throwable을 처리한다.


ex)

	@Around("execution(* org.zerock.service.MessageService*.*(..))")
	public Object timeLog(ProceedingJoinPoint pjp) throws Throwable {
			
		long startTime = System.currentTimeMillis();
		
		logger.info(Arrays.toString(pjp.getArgs()));
		
		Object result = pjp.proceed();
		
		long endTime = System.currentTimeMillis();
		
		logger.info(pjp.getSignature().getName() + " : " + (endTime - startTime));
		
		return result;
		
			
	}


pjp.proceed() 메서드를 이용해 실제 메소드를 호출한다.(proceed 메서드를 호출하지 않으면 해당 기능(select, insert 등)이 실행되지 않는다.)

리턴타입을 반드시 Object로 해야한다.


-----

#### @Transactional

- ★serviceImpl클래스의 하나의 메서드에서 여러 개의 쿼리문이 실행되는 경우(=하나의 트랜잭션에 여러가지가 실행되는 경우)에

그 중 하나라도 오류가 발생하면 메서드 내에 있는 모든 쿼리문이 실행되지 않는다.

- 트랜잭션 설정을 하도록 해준다.

- 인터페이스, 클래스, 메서드에 선언할 수 있다.

- 적용의 우선순위 : 메서드 > 클래스 > 인터페이스
(메서드에 선언된 어노테이션이 우선순위가 가장 높다.)

- 일반적으로 클래스나 인터페이스에는 공톡적인 규칙을 선언하고, 메서드에는 특별한 설정을 추가하는 경우가 많다.

-----


#### @Resource

servlet-context.xml 파일에 bean으로 등록되어 있는 객체와 맵핑시켜준다.

ex)

@Resource(name="uploadPath") // servlet-context.xml파일에 id가 uploadPath인 bean과 맵핑시켜준다. 
String uploadPath;

-----

#### (#id).serialize()

ajax 통신에서

data:(#id).serialize() 와 같이 사용할 경우(#id 은 <form>태그의 id속성 값이다.)

해당 form태그 안에있는 input태그들의 값을

Cotroller에서 실행하는 메소드의 파라미터에 있는

해당 input태그들의 name과 일치하는 VO 인스턴스의 필드명이 mapping된다.

input 태그의 value 속성이 VO 인스턴스의 필드 값이 된다.

@ResponseBody 어노테이션을 메소드 위에 입력해줘야 mapping이 된다.
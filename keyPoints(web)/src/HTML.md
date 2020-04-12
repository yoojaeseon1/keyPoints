##### form

form 태그 안에 있는 input 태그의 value를 전송한다.

	<form method="GET" action="/reviewList">

		<input value="123"/>
		<input value="456"/>
		<input value="칠팔구"/>
		<button type="submit"></button>
	</form>
	
submit 타입의 버튼을 클릭해 전송할 수 있다.

또는 javaScript에서 windows.form의 아이디+form.submit() 을 통해 강제로 보낼 수도 있다.

###### 속성

action : 전송할 URL

method : 전송방식(GET/POST/DELETE/PUT/PATCH)

##### form

form 태그 안에 있는 input 태그의 value를 전송한다.

GET, POST 방식만 지원한다.

	<form method="GET" action="/reviewList">

		<input value="123"/>
		<input value="456"/>
		<input value="칠팔구"/>
		<button type="submit"></button>
	</form>
	
submit 타입의 버튼을 클릭해 전송할 수 있다.

document.form태그의id.submit() : 해당 id를 가지는 form태그를 전송한다.(버튼 없이 이렇게 메소드로 가능하다.)

---

###### 속성

action : 전송할 URL

method : 전송방식(GET/POST/DELETE/PUT/PATCH)

---

##### input 태그의 type="file" 

	<input type="file" value="">

input태그의 type속성이 file일 경우 read only이므로 value속성에 값을 세팅할 수 없다.

type이 text, hidden, check 일 경우엔 value에 값을 세팅할 수 있다.

---

##### 공백 추가하고 싶을 때

&nbsp; : Non-breaking Space

&nbsp;를 원하는 만큼 추가해주면 된다.

---
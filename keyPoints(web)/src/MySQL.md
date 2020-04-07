##### LIMIT

SELECT 문을 통해 나오는 튜플의 개수를 제한한다.

ex)

	SELECT * FROM reviewimages ORDER BY reviewIndex DESC LIMIT 10;
	
나오는 결과 값에서 처음부터 10개의 튜플만 반환한다.

	SELECT * FROM reviewimages ORDER BY reviewIndex DESC LIMIT 3, 10;
	
나오는 결과 값에서 4(index 3)번째부터 10개의 튜플을 반환한다.

---

##### CONCAT

파라미터로 받는 문자열을 합쳐준다.

MyBatis에서 like를 통한 검색시 CONCAT을 사용한다.

인자로 들어가는 문자열을 합쳐준다.

ex)

	title like CONCAT('%', 검색어, '%')

그냥 쿼리문에서는 처럼

	title like '%검색어%'
	
이라고 입력하면

Cause: java.sql.SQLException: Parameter index out of range (1 > number of parameters, which is 0).

에러가 발생한다.

---

##### sql 태그

	<sql id="sqlID">쿼리문</sql> 을 작성하면 

	<include refid="sqlID"></include> 를 사용해 재사용 할 수 있다.

##### include 태그

	<include refid="sqlID"></include>

를 통해 

	<sql id="sqlID">쿼리문</sql>
	
사전에 작성되어 있는 쿼리문을 재사용 할 수 있다.
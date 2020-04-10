##### LIMIT

SELECT 문을 통해 나오는 튜플의 개수를 제한한다.

ex)

	SELECT * FROM reviewimages ORDER BY reviewIndex DESC LIMIT 10;
	
나오는 결과 값에서 처음부터 10개의 튜플만 반환한다.

	SELECT * FROM reviewimages ORDER BY reviewIndex DESC LIMIT 3, 10;
	
나오는 결과 값에서 4(index 3)번째부터 10개의 튜플을 반환한다.

---

##### 테이블 정보 수정

###### 컬럼 추가

	alter table [테이블명] add [컬럼명] [타입] [옵션]; 

ex) alter table [테이블명] add [컬럼명] varchar(100) not null default '0'; 



###### 컬럼 삭제

alter table [테이블명] drop [컬럼명];



###### 컬럼명 변경 및 타입 변경

	alter table [테이블명] change [컬럼명] [변경할컬럼명] varchar(12);

같은 타입에 속성명만 변경하더라도 타입을 명시 해야한다.

###### 컬럼 타입 수정

	alter table [테이블명] modify [컬럼명] varchar(14);



###### 테이블명 수정

	alter table [테이블명] rename [변경할테이블명];



테이블 삭제

drop table [테이블명];


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

##### selectOne해서 넘어오는 값이 없을 경우

service 인스턴스를 통해 실행한 메소드에서 조건에 맞는 값이 없어 가져오지 못했을 경우

null을 리턴한다.

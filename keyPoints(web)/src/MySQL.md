##### varchar vs char

###### 공통점

- 대소문자를 구별하지 않는다.

- varchar(bytes) / char(bytes) : 해당 용량만큼의 문자열을 넣을 수 있다. 넘을 경우 그 만큼 잘린다.(알파벳 한 글자당 1byte, 한글 한 글자당 2byte)

###### 차이점

- char : 고정형 문자열

ex)

char(20) : 2byte만 넣어도 20bytes만큼의 메모리를 차지한다.
	
vharchar(20) : 2byte만 넣으면 2byte만 차지한다.(최대 용량이 20byte) 


char의 경우 차지하는 데이터의 용량을 계산할 필요가 없기 때문에 검색속도가 다른 타입보다 월등히 빠르다.
사이즈가 고정되어 있는 속성의 경우 char로 해주면 좋다.(ex)주민등록번호, 핸드폰번호, 아이디)

변동폭이 클 경우에는 varchar를 사용하면 메모리를 효율적으로 관리할 수 있다. (ex) 게시물의 본문)

--- 

##### int

int형은 따로 인자를 지정하지 않으면 int(11)로 만들어진다.

###### int(param)에서 param의 의미

ZEROFILL 옵션을 활성화했을 때 현재 값 나머지 길이를 0으로 채우는 길이

ex)

	num int(5),
	numZero int(5) ZEROFILL

---

num이 1 일 경우 -> 1

numZero가 1일 경우 -> 00001

5칸을 기준으로 빈 자릿수에 0을 채우게 된다.

하지만 num과 numZero의 실제 저장공간과 입력가능 한계는 동일하다.

만약 5자리를 초과하면 ZEROFILL의 의미는 없어진다.

---

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

##### 날짜(datetime) 검색

	select * from reviewboard where date(registeredDate) = "2020-04-02";

	select * from reviewboard where registeredDate >= "2020-04-02 00:00:00" and registeredDate <= "2020-04-02 23:59:59";
	
둘 다 같은 결과 값을 리턴한다.

하지만 밑에 쿼리문이 날짜를 파싱하는 단계가 없기 때문에 더 빠르다.

##### BETWEEN

	select * from reviewboard where date(registeredDate) between "2020-04-02" and "2020-04-10";
	
와 같이 사용 가능하다.

###### 주의사항

	between 작은값 and 큰값
	
의 순서로 와야 값을 정확하게 읽어올 수 있다.(거꾸로 하면 안나온다.)

---

##### command 창에서 접속하기

mysql -u 유저네임 -p DB네임 (엔터)
-> 비밀번호 입력

유저네임 : root

비밀번호 : 설정한 비밀번호

---

##### 1:n 관계에서의 외래키

1 : 부모 릴레이션

n : 자식 릴레이션


자식은 부모의 기본키를 외래키로 가져야 한다. 하지만 그 키를 참조하는 본인(자식)의 속성은 기본키면 안된다.

그러면 1:1 관계가 되는 것이고, 1:n 관계에서는 그렇게 될 수 없다.

본인의 키가 복합키 중 일부라면 괜찮다.

---

##### ER 다이어그램

실선(식별관계)

- 부모테이블의 기본키가 자식테이블의 기본/외래키가 되는 경우

- 부모가 있어야 자식이 생기는 경우(ex) 게시물에 추가되는 이미지/좋아요/댓글 등)

점선(비식별관계)

- 부모테이블의 기본키가 자식테이블의 기본 속성인 경우

- 부모가 없어도 자식이 생기는 경우


---

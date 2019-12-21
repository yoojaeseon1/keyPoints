##### root-context.xml

- sqlSession 연결 : DB의 id/password입력

- 프로젝트의 mapper파일들과 연결

---

<aop:aspectj-autoproxy></aop:aspectj-autoproxy>

: 자동으로 AspectJ 라이브러리를 이용해서 Proxy객체를 생성해 내는 용도로 사용

---

패키지를 인식할 수 있도록 설정한다

ex)

<context:component-scan base-package="org.zerock.service"></context:component-scan>

base-package="package route" 를 작성해주면 된다.


---

트랜잭션의 처리

	<bean id="transactionManager"
	class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
	<property name="dataSource" ref="dataSource"></property>
	</bean>

---

<tx:annotation-driven />

: @Transctional 어노테이션을 이용한 트랜잭션 관리가 가능하도록 해준다.



---

##### pom.xml

- 외부 라이브러리와의 연동


ex) 라이브러리 명

 <groupId> -> <artifactId>


라이브러리

jackson-databind 

: 객체를 JSON타입의 데이터로 변환하거나, 반대의 작업을 할 때 사용(JOSN을 이용해야하는 프로젝트에서는 반드시 필요)

예제의 프로젝트에서는 Map 인스턴스를 JSON형식으로 변환하여 view에 뿌려준다.

---

org.springframework -> spring-aop

org.springframework -> spring-tx


: Spring에서 AOP방식을 사용하기 위해 사용하는 라이브러리

---

aspectj : AOP의 기능을 적용하기위한 apectj 언어의 문법을 사용하기 위한 라이브러리


---

##### servlet-context.xml

login에 필요한 interceptor를 설정한다.

ex)

<beans:bean id="loginInterceptor" class="org.zerock.interceptor.LoginInterceptor"></beans:bean>

	<interceptors>
		<interceptor>
			<mapping path="/user/loginPost"/>
			<beans:ref bean="loginInterceptor"/>
		</interceptor>
	</interceptors>

mapping path에 접근할 때 interceptor가 실행되어 login여부, 권한 등을 확인 할 수 있다.
beans:ref에는 위에서 설정한 bean의 id를 입력해준다.


★ mapping path에 접근 -> beans:ref에서 설정된 bean id확인 -> bean id에 설정된 class(interceptor)에서 preHandle/postHandle 메소드 실행


---



---

##### applicationContext.xml

DB 연동과 관련된 설정을 한다.

ex)

	<bean id="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean"
		p:dataSource-ref="dataSource"
		  p:configLocation="classpath:/mybatis-config.xml"
		p:mapperLocations="classpath:/mapper/*.xml"
	/>

	<bean id="sqlSession" class="org.mybatis.spring.SqlSessionTemplate">
		<constructor-arg ref="sqlSessionFactory"></constructor-arg>
	</bean>
	
	

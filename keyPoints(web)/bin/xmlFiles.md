##### root-context.xml

- sqlSession ���� : DB�� id/password�Է�

- ������Ʈ�� mapper���ϵ�� ����

---

<aop:aspectj-autoproxy></aop:aspectj-autoproxy>

: �ڵ����� AspectJ ���̺귯���� �̿��ؼ� Proxy��ü�� ������ ���� �뵵�� ���

---

��Ű���� �ν��� �� �ֵ��� �����Ѵ�

ex)

<context:component-scan base-package="org.zerock.service"></context:component-scan>

base-package="package route" �� �ۼ����ָ� �ȴ�.


---

Ʈ������� ó��

	<bean id="transactionManager"
	class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
	<property name="dataSource" ref="dataSource"></property>
	</bean>

---

<tx:annotation-driven />

: @Transctional ������̼��� �̿��� Ʈ����� ������ �����ϵ��� ���ش�.



---

##### pom.xml

- �ܺ� ���̺귯������ ����


ex) ���̺귯�� ��

 <groupId> -> <artifactId>


���̺귯��

jackson-databind 

: ��ü�� JSONŸ���� �����ͷ� ��ȯ�ϰų�, �ݴ��� �۾��� �� �� ���(JOSN�� �̿��ؾ��ϴ� ������Ʈ������ �ݵ�� �ʿ�)

������ ������Ʈ������ Map �ν��Ͻ��� JSON�������� ��ȯ�Ͽ� view�� �ѷ��ش�.

---

org.springframework -> spring-aop

org.springframework -> spring-tx


: Spring���� AOP����� ����ϱ� ���� ����ϴ� ���̺귯��

---

aspectj : AOP�� ����� �����ϱ����� apectj ����� ������ ����ϱ� ���� ���̺귯��


---

##### servlet-context.xml

login�� �ʿ��� interceptor�� �����Ѵ�.

ex)

<beans:bean id="loginInterceptor" class="org.zerock.interceptor.LoginInterceptor"></beans:bean>

	<interceptors>
		<interceptor>
			<mapping path="/user/loginPost"/>
			<beans:ref bean="loginInterceptor"/>
		</interceptor>
	</interceptors>

mapping path�� ������ �� interceptor�� ����Ǿ� login����, ���� ���� Ȯ�� �� �� �ִ�.
beans:ref���� ������ ������ bean�� id�� �Է����ش�.


�� mapping path�� ���� -> beans:ref���� ������ bean idȮ�� -> bean id�� ������ class(interceptor)���� preHandle/postHandle �޼ҵ� ����


---



---

##### applicationContext.xml

DB ������ ���õ� ������ �Ѵ�.

ex)

	<bean id="sqlSessionFactory" class="org.mybatis.spring.SqlSessionFactoryBean"
		p:dataSource-ref="dataSource"
		  p:configLocation="classpath:/mybatis-config.xml"
		p:mapperLocations="classpath:/mapper/*.xml"
	/>

	<bean id="sqlSession" class="org.mybatis.spring.SqlSessionTemplate">
		<constructor-arg ref="sqlSessionFactory"></constructor-arg>
	</bean>
	
	

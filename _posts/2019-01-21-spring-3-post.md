---
title: "스프링 시작3 - 스프링 프레임워크 중요 환경 설정"
date: 2018-01-11 10:11:00 -0400
categories: 
  - spring
---

### 스프링 프레임워크 중요 환경 설정(web.xml, dispatcher_servlet.xml, context.xml) ###  
  
서블릿 배포 기술자이며 WAS가 최초 구동될 때, WEB-INF 디렉토리에 존재하는 web.xml을 읽고 웹 어플리케이션을 설정한다  
여기에는 spring_servlet_context.xml의 위치도 넣어주게 되어있다  
  
기본 구조(3.1버젼)  
'''
<?xml version="1.0" encoding="UTF-8"?>  
<web-app xmlns: xsi="http://www.w3.org/2001/XMLSchema-instance"  
 xmlns="http://xmlns.jcp.org/xml/ns/javaee"  
 xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee   
 http://xmlns.jcp.org/xml/ns/javaee/web-app_3_1.xsd" id="WebApp_ID" version="3.1">  
'''

여러가지 설정들  
  
</web-app>  
  
  
기본 구조(2.5버젼)  
'''
<?xml version="1.0" encoding="UTF-8"?>  
<web-app xmlns="http://java.sun.com/xml/ns/javaee"   
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"  
xsi:schemaLocation="http://java.sun.com/xml/ns/javaee http://java.sun.com/xml/ns/javaee/web-app_2_5.xsd"  
version="2.5">  
'''

여러가지 설정들  
  
</web-app>  
  
  
여러가지 설정들 리스트  
1) 필터  
<filter>  
<filter-name>CharacterEncodingFilter</filter-name>  
<filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>  
<init-param>  
<param-name>encoding</param-name>  
<param-value>UTF-8</param-value>  
</init-param>  
<init-param>  
<param-name>forceEncoding</param-name>  
<param-value>true</param-value>  
</init-param>  
</filter>  
<filter-mapping>  
<filter-name>CharacterEncodingFilter</filter-name>  
<url-pattern>/*</url-pattern>  
</filter-mapping>  
  
<filter>  
<filter-name>encodingFilter</filter-name>  
<filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>  
<init-param>  
<param-name>encoding</param-name>  
<param-value>utf-8</param-value>  
</init-param>  
</filter>  
<filter-mapping>  
<filter-name>encodingFilter</filter-name>  
<url-pattern>*.do</url-pattern>  
</filter-mapping>  
  
  
<filter>  
<filter-name>encodingFilter</filter-name>  
<filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>  
<init-param>  
<param-name>encoding</param-name>  
<param-value>UTF-8</param-value>  
</init-param>  
<init-param>  
<param-name>forceEncoding</param-name>  
<param-value>true</param-value>  
</init-param>  
</filter>  
<filter-mapping>  
<filter-name>encodingFilter</filter-name>  
<url-pattern>/tudu/*</url-pattern>  
</filter-mapping>  
  
  
  
2) dispatcher 서블릿  
<servlet>  
<servlet-name>shopping3-7</servlet-name>  
<servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>  
<load-on-startup>1</load-on-startup>  
</servlet>  
<servlet-mapping>  
<servlet-name>shopping3-7</servlet-name>  
<url-pattern>*.html</url-pattern>  
</servlet-mapping>  
<servlet>  
<servlet-name>action</servlet-name>  
<servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>  
<init-param>  
<param-name>contextConfigLocation</param-name>  
<param-value>/WEB-INF/config/*-servlet.xml</param-value>  
</init-param>  
<load-on-startup>1</load-on-startup>  
</servlet>  
<servlet-mapping>  
<servlet-name>action</servlet-name>  
<url-pattern>*.do</url-pattern>  
</servlet-mapping>  
  
  
<servlet>  
<servlet-name>dispatcher</servlet-name>  
<servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>  
<load-on-startup>1</load-on-startup>  
</servlet>  
<servlet-mapping>  
<servlet-name>dispatcher</servlet-name>  
<url-pattern>/tudu/*</url-pattern>  
</servlet-mapping>  
  
  
***<server-name>-context.xml 파일이 web.xml과 같은 위치에 있다면 init-param으로 dispatcher xml파일 이름 설정해 주지 않아도 자동으로 로드됨  
  
3) welcome 리스트  
<welcome-file-list>  
    <welcome-file>index.jsp</welcome-file>  
</welcome-file-list>  
  
4) context 관련  
<context-param>  
<param-name>contextConfigLocation</param-name>  
<param-value>classpath*:config/spring/context-*.xml</param-value>  
</context-param>  
<context-param>  
<param-name>contextConfigLocation</param-name>  
<param-value>/WEB-INF/security.xml /WEB-INF/applicationContext.xml</param-value>  
</context-param>  
  
<context-param>  
<param-name>contextConfigLocation</param-name>  
<param-value>classpath:META-INF/spring/application-context.xml</param-value>  
</context-param>  
  
  
5) 기타 context 관련  
<context-param>  
<param-name>log4jConfigLocation</param-name>  
<param-value>WEB-INF/log4j.xml</param-value>  
</context-param>  
  
  
6) context 로더  
<listener>  
<listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>  
</listener>  
  
<listener>  
<listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>  
</listener>  
  
  
7) 에러 페이지  
<error-page>  
<error-code>403</error-code>  
<location>/WEB-INF/jsp/noAuthority.jsp</location>  
</error-page>  
<error-page>  
<exception-type>java.lang.Exception</exception-type>  
<location>/tudu/500</location>  
</error-page>  
<error-page>  
<error-code>404</error-code>  
<location>/tudu/404</location>  
</error-page>  
  
  
8) 디스플레이 이름  
<display-name>Tudu Lists</display-name>  
  
  
9) 기타 필터  
<filter>  
<filter-name>springSecurityFilterChain</filter-name>  
<filter-class>org.springframework.web.filter.DelegatingFilterProxy</filter-class>  
</filter>  
<filter-mapping>  
<filter-name>springSecurityFilterChain</filter-name>  
<url-pattern>/*</url-pattern>  
</filter-mapping>  
  
<filter>  
<filter-name>springSecurityFilterChain</filter-name>  
<filter-class>org.springframework.web.filter.DelegatingFilterProxy</filter-class>  
</filter>  
<filter-mapping>  
<filter-name>springSecurityFilterChain</filter-name>  
<url-pattern>/tudu/*</url-pattern>  
</filter-mapping>  
<filter-mapping>  
<filter-name>springSecurityFilterChain</filter-name>  
<url-pattern>/ajax/*</url-pattern>  
</filter-mapping>  
<filter-mapping>  
<filter-name>springSecurityFilterChain</filter-name>  
<url-pattern>/servlet/*</url-pattern>  
</filter-mapping>  
  
<filter>  
<filter-name>Open Session In View Filter</filter-name>  
<filter-class>org.springframework.orm.jpa.support.OpenEntityManagerInViewFilter</filter-class>  
</filter>  
<filter-mapping>  
<filter-name>Open Session In View Filter</filter-name>  
<url-pattern>/ajax/*</url-pattern>  
</filter-mapping>  
  
<filter>  
<filter-name>GZipFilter</filter-name>  
<filter-class>net.sf.ehcache.constructs.web.filter.GzipFilter</filter-class>  
</filter>  
<filter-mapping>  
<filter-name>GZipFilter</filter-name>  
<url-pattern>/*</url-pattern>  
</filter-mapping>  
  
  
<filter>  
<filter-name>SimpleCachingHeadersPageCachingFilter</filter-name>  
<filter-class>net.sf.ehcache.constructs.web.filter.SimpleCachingHeadersPageCachingFilter</filter-class>  
<init-param>  
<param-name>suppressStackTraces</param-name>  
<param-value>false</param-value>  
</init-param>  
<init-param>  
<param-name>cacheName</param-name>  
<param-value>web-cache</param-value>  
</init-param>  
</filter>  
<filter-mapping>  
<filter-name>SimpleCachingHeadersPageCachingFilter</filter-name>  
<url-pattern>/rss</url-pattern>  
</filter-mapping>  
  
  
10) 기타 리스너  
<listener>  
<listener-class>org.springframework.security.web.session.HttpSessionEventPublisher</listener-class>  
</listener>  
  
<listener>  
<listener-class>org.springframework.web.util.Log4jConfigListener</listener-class>  
</listener>  
  
  
<listener>  
<listener-class>org.springframework.web.context.request.RequestContextListener</listener-class>  
</listener>  
  
  
<listener>  
<listener-class>net.sf.navigator.menu.MenuContextListener</listener-class>  
</listener>  
  
  
11) 기타 서블릿   
<servlet>  
<servlet-name>dwr</servlet-name>  
<servlet-class>org.directwebremoting.spring.DwrSpringServlet</servlet-class>  
<init-param>  
<param-name>debug</param-name>  
<param-value>true</param-value>  
</init-param>  
<load-on-startup>2</load-on-startup>  
</servlet>  
<servlet-mapping>  
<servlet-name>dwr</servlet-name>  
<url-pattern>/ajax/*</url-pattern>  
</servlet-mapping>  
<servlet>  
<servlet-name>rss</servlet-name>  
<servlet-class>tudu.web.servlet.RssFeedServlet</servlet-class>  
<load-on-startup>3</load-on-startup>  
</servlet>  
<servlet-mapping>  
<servlet-name>rss</servlet-name>  
<url-pattern>/servlet/rss</url-pattern>  
</servlet-mapping>  
  
<servlet>  
<servlet-name>backup</servlet-name>  
<servlet-class>tudu.web.servlet.BackupServlet</servlet-class>  
</servlet>  
<servlet-mapping>  
<servlet-name>backup</servlet-name>  
<url-pattern>/servlet/tudu_lists_backup.xml</url-pattern>  
</servlet-mapping>  
  
  
  
  
  
dispatcher_servlet.xml  
  
스프링에서 URL요청에 의해 contoller를 호출하게 되는게 그때 이 설정을 이용하여 controller가 동작하게 되고 결과에 대한 view페이지로 이동하게 됨  
web.xml에서 2) dispatcher 서블릿에서 설정한 파일이다  
  
  
기본구조  
<?xml version="1.0" encoding="UTF-8"?>  
<beans xmlns:context="http://www.springframework.org/schema/context"  
    xmlns:p="http://www.springframework.org/schema/p"  
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"  
    xmlns="http://www.springframework.org/schema/beans"  
    xmlns:mvc="http://www.springframework.org/schema/mvc"  
    xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans-3.0.xsd  
       http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context-3.0.xsd  
       http://www.springframework.org/schema/mvc http://www.springframework.org/schema/mvc/spring-mvc.xsd">  
  
여러가지 설정들...  
	  
</beans>  
  
  
1)component-scan  
<context:component-scan base-package="sms"></context:component-scan>  
  
  
<context:component-scan base-package="controller,dao,logic" />  
  
<context:component-scan base-package="tudu.web.mvc, tudu.web.rest"/>  
  
  
  
2)interceptor  
<mvc:interceptors>  
<mvc:interceptor>  
<mvc:mapping path="/**"/>  
<bean id="loggerInterceptor" class="sms.common.logger.LoggerInterceptor"></bean>  
</mvc:interceptor>  
</mvc:interceptors>  
  
  
<bean id="localeChangeInterceptor"  
          class="org.springframework.web.servlet.i18n.LocaleChangeInterceptor">  
        <property name="paramName" value="lang"/>  
 </bean>  
  
  
  
  
  
3)annotation-driven  
<mvc:annotation-driven />  
  
  
  
4)view resolver 관련  
<bean  
class="org.springframework.web.servlet.view.UrlBasedViewResolver"   
p:order="1"   
p:viewClass="org.springframework.web.servlet.view.JstlView"   
p:prefix="/WEB-INF/jsp/"   
p:suffix=".jsp">  
</bean>  
  
  
<!-- ViewResolver -->  
<bean id="internalResourceViewResolver"  
class="org.springframework.web.servlet.view.InternalResourceViewResolver">  
<property name="viewClass">  
<value>org.springframework.web.servlet.view.JstlView</value>  
</property>  
<property name="prefix">  
<value>/WEB-INF/jsp/</value>  
</property>  
<property name="suffix">  
<value>.jsp</value>  
</property>  
</bean>	  
  
  
<bean class="org.springframework.web.servlet.view.ContentNegotiatingViewResolver">  
  <property name="mediaTypes">  
            <map>  
                <entry key="html" value="text/html"/>  
                <entry key="json" value="application/json"/>  
            </map>  
        </property>  
        <property name="viewResolvers">  
            <list>  
                <bean class="org.springframework.web.servlet.view.UrlBasedViewResolver">  
                    <property name="viewClass" value="org.springframework.web.servlet.view.JstlView"/>  
                    <property name="prefix" value="/WEB-INF/views/"/>  
                    <property name="suffix" value=".jsp"/>  
                </bean>  
            </list>  
        </property>  
        <property name="defaultViews">  
            <list>  
                <bean class="org.springframework.web.servlet.view.json.MappingJacksonJsonView"/>  
            </list>  
        </property>  
</bean>  
  
  
<bean id="localeResolver"  
          class="org.springframework.web.servlet.i18n.CookieLocaleResolver"/>  
  
  
5) multipark resolver 관련  
<bean id="multipartResolver"  
class="org.springframework.web.multipart.commons.CommonsMultipartResolver"  
p:maxUploadSize="104857600"   
p:maxInMemorySize="10485760">  
</bean>  
  
<bean id="multipartResolver"  
          class="org.springframework.web.multipart.commons.CommonsMultipartResolver"/>  
  
  
  
  
  
6)기타 bean 관련  
<bean class="org.springframework.web.servlet.mvc.method.annotation.RequestMappingHandlerMapping"/>  
<bean class="org.springframework.web.servlet.mvc.method.annotation.RequestMappingHandlerAdapter"/>  
<!-- <bean class="org.springframework.web.servlet.mvc.annotation.DefaultAnnotationHandlerMapping"/> -->  
     
<bean class="org.springframework.web.servlet.view.BeanNameViewResolver" p:order="0" />  
<bean id="jsonView" class="org.springframework.web.servlet.view.json.MappingJacksonJsonView" />      
     
<bean class="org.springframework.web.servlet.mvc.support.ControllerClassNameHandlerMapping" />  
  
<bean class="org.springframework.jdbc.support.lob.DefaultLobHandler"></bean>  
  
<bean id="handlerMapping"  
          class="org.springframework.web.servlet.mvc.annotation.DefaultAnnotationHandlerMapping">  
        <property name="interceptors">  
            <list>  
                <ref bean="localeChangeInterceptor"/>  
            </list>  
        </property>  
</bean>  
  
<bean id="menu" class="net.sf.navigator.menu.MenuLoader">  
        <property name="menuConfig" value="/WEB-INF/menu-config.xml"/>  
</bean>  
  
  
7) view-controller  
<mvc:view-controller path="/login.html" view-name="masterLogin" />  
<mvc:view-controller path="/logout.html" view-name="logout" />  
  
  
  
  
  
  
  
  
  
context.xml  
  
주로 데이터베이스와 관련된 설정들이 이곳에 들어가게 된다  
web.xml에서 4) context 관련과 5) 기타 context 관련에서 설정한 파일이다  
  
  
기본 구조  
<?xml version="1.0" encoding="UTF-8"?>  
<beans xmlns="http://www.springframework.org/schema/beans"  
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"  
xmlns:context="http://www.springframework.org/schema/context"  
xmlns:p="http://www.springframework.org/schema/p"  
xmlns:tx="http://www.springframework.org/schema/tx"  
xmlns:aop="http://www.springframework.org/schema/aop"  
xsi:schemaLocation="http://www.springframework.org/schema/beans   
http://www.springframework.org/schema/beans/spring-beans.xsd  
http://www.springframework.org/schema/beans/spring-beans-3.0.xsd  
http://www.springframework.org/schema/context   
http://www.springframework.org/schema/context/spring-context.xsd  
http://www.springframework.org/schema/aop  
http://www.springframework.org/schema/aop/spring-aop-3.0.xsd  
http://www.springframework.org/schema/tx  
http://www.springframework.org/schema/tx/spring-tx-3.0.xsd">  
  
여러가지 설정들...  
  
</beans>  
  
  
  
1) datasource  
<!-- MySQL 설정 -->  
    <bean id="dataSource" class="org.apache.commons.dbcp.BasicDataSource" destroy-method="close">  
        <property name="driverClassName" value="com.mysql.jdbc.Driver"/>  
        <property name="url" value="jdbc:mysql://211.110.61.59/lguplus"/>  
        <property name="username" value="paymint"/>  
        <property name="password" value="paymint"/>  
    </bean>  
      
    <!-- 오라클 설정 -->  
    <!-- <bean id="dataSource" class="org.apache.commons.dbcp.BasicDataSource" destroy-method="close">  
        <property name="driverClassName" value="oracle.jdbc.driver.OracleDriver"/>  
        <property name="url" value="jdbc:oracle:thin:@localhost:1521:XE"/>  
        <property name="username" value="아이디"/>  
        <property name="password" value="비밀번호"/>  
    </bean> -->  
   
  
<!-- Data Source -->  
	<bean id="dataSource"  
		class="org.springframework.jdbc.datasource.DriverManagerDataSource">  
		<!-- JDBC드라이버명 설정 -->  
		<property name="driverClassName">  
			<value>com.mysql.jdbc.Driver</value>  
		</property>  
		<!-- JDBC접속 문자열 설정 -->  
		<property name="url">  
			<value>jdbc:mysql://localhost/spring?useUnicode=true&amp;characterEncoding=utf8  
			</value>  
		</property>  
		<!-- MySQL 유저ID 설정 -->  
		<property name="username">  
			<value>springuser</value>  
		</property>  
		<!-- MySQL 패스워드 설정 -->  
		<property name="password">  
			<value>springpassword</value>  
		</property>  
	</bean>  
  
  
<bean id="dataSource"  
          class="com.mchange.v2.c3p0.ComboPooledDataSource"  
          destroy-method="close">  
  
        <property name="driverClass" value="${datasource.driverclassname}"/>  
        <property name="jdbcUrl" value="${dataSource.url}"/>  
        <property name="user" value="${dataSource.username}"/>  
        <property name="password" value="${dataSource.password}"/>  
        <property name="initialPoolSize" value="10"/>  
        <property name="minPoolSize" value="10"/>  
        <property name="maxPoolSize" value="${dataSource.maxActive}"/>  
        <property name="idleConnectionTestPeriod" value="600"/>  
        <property name="acquireIncrement" value="2"/>  
        <property name="maxStatements" value="300"/>  
        <property name="numHelperThreads" value="10"/>  
    </bean>  
  
2) transaction  
<bean id="transactionManager"  
		class="org.springframework.jdbc.datasource.DataSourceTransactionManager"  
		p:dataSource-ref="dataSource">  
</bean>  
  
<bean id="transactionManager"  
          class="org.springframework.orm.jpa.JpaTransactionManager">  
        <property name="entityManagerFactory" ref="entityManagerFactory"/>  
</bean>  
  
  
  
3) sql session  
	<bean id="sqlSession" class="org.mybatis.spring.SqlSessionFactoryBean">  
		<property name="dataSource" ref="dataSource" />  
		<property name="mapperLocations" value="classpath:/mapper/**/*_SQL.xml" />  
	</bean>  
	  
	<bean id="sqlSessionTemplate" class="org.mybatis.spring.SqlSessionTemplate">  
        <constructor-arg index="0" ref="sqlSession"/>  
  
  
4) message source  
<!-- MessageSource -->  
<bean id="messageSource"  
	class="org.springframework.context.support.ResourceBundleMessageSource">  
	<property name="basenames">  
		<list>  
			<value>ApplicationResource</value>  
			<value>messages</value>  
		</list>  
	</property>  
</bean>  
  
  
<bean id="messageSource"  
          class="org.springframework.context.support.ReloadableResourceBundleMessageSource">  
        <property name="basename" value="WEB-INF/messages"/>  
</bean>  
  
5) context설정 파일들을 분리했을때 로드설정 부분  
<import resource="application-context-infrastructure.xml"/>  
<import resource="application-context-infrastructure-env.xml"/>  
<import resource="application-context-security.xml"/>  
<import resource="application-context-dwr.xml"/>  
6) componet-scan  
<context:component-scan base-package="tudu.service"/>  
7) tx  
<tx:annotation-driven />  
8) 기타 beans  
<!-- JPA annotations bean post processor -->  
    <bean class="org.springframework.orm.jpa.support.PersistenceAnnotationBeanPostProcessor"/>  
    <!-- Exception translation bean post processor -->  
    <bean class="org.springframework.dao.annotation.PersistenceExceptionTranslationPostProcessor"/>  
    <bean id="entityManagerFactory"  
          class="org.springframework.orm.jpa.LocalContainerEntityManagerFactoryBean">  
        <property name="dataSource" ref="dataSource"/>  
        <property name="jpaVendorAdapter">  
            <bean class="org.springframework.orm.jpa.vendor.HibernateJpaVendorAdapter">  
                <property name="database" value="${jpavendoradapter.database}"/>  
                <property name="databasePlatform" value="${jpavendoradapter.databaseplatform}"/>  
                <property name="showSql" value="${jpavendoradapter.showsql}"/>  
                <property name="generateDdl" value="${jpavendoradapter.generateddl}"/>  
            </bean>  
        </property>  
        <property name="persistenceXmlLocation" value="classpath:META-INF/persistence.xml"/>  
    </bean>  
  
출처: http://istoryful.tistory.com/5 [HULIA(휴리아)의 서비스개발&스킨제작 Story]  
출처: http://istoryful.tistory.com/5 [HULIA(휴리아)의 서비스개발&스킨제작 Story]  
출처: http://istoryful.tistory.com/5 [HULIA(휴리아)의 서비스개발&스킨제작 Story]  
출처: http://istoryful.tistory.com/5 [HULIA(휴리아)의 서비스개발&스킨제작 Story]  
출처: http://istoryful.tistory.com/5 [HULIA(휴리아)의 서비스개발&스킨제작 Story]  
출처: http://istoryful.tistory.com/5 [HULIA(휴리아)의 서비스개발&스킨제작 Story]  
출처: http://istoryful.tistory.com/5 [HULIA(휴리아)의 서비스개발&스킨제작 Story]  
출처: http://istoryful.tistory.com/5 [HULIA(휴리아)의 서비스개발&스킨제작 Story]  
출처: http://istoryful.tistory.com/5 [HULIA(휴리아)의 서비스개발&스킨제작 Story]  
출처: http://istoryful.tistory.com/5 [HULIA(휴리아)의 서비스개발&스킨제작 Story]  
출처: http://istoryful.tistory.com/5 [HULIA(휴리아)의 서비스개발&스킨제작 Story]  
출처: http://istoryful.tistory.com/5 [HULIA(휴리아)의 서비스개발&스킨제작 Story]  
출처: http://istoryful.tistory.com/5 [HULIA(휴리아)의 서비스개발&스킨제작 Story]  
출처: http://istoryful.tistory.com/5 [HULIA(휴리아)의 서비스개발&스킨제작 Story]

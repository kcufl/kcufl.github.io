---
title: "스프링 시작6 - 스프링 MVC 구조3"
date: 2018-01-11 10:49:00 -0400
categories: 
  - spring
---




### Spring - MVC ###


https://jongmin92.github.io/2018/03/12/Spring/spring-mvc/


  
DispatcherServlet 이란?  
  
Spring MVC는 DispatcherServlet의 등장으로 web.xml의 역할이 축소되었습니다. 이전에는 서블릿을 URL로 활용하기 위해서는 반드시 web.xml에 등록해야 했지만, 이제는 DispatcherServlet이 해당 어플리케이션으로 들어오는 요청을 모두 핸들링 해주기 때문입니다.  
  
web.xml의 역할이 축소되었지만, <servlet>으로 DispatcherServlet을 등록해줘야 하며, 이 객체의 URL 적용범위 또한 web.xml에 설정해야 합니다. 또한 encoding과 관련된 <filter>나 <listener>를 등록하기 위해서 web.xml은 필요합니다.  
  
그러나 web.xml에서 중요하게 사용되었던 <servlet> 매핑은 이제 DispatcherServlet이 대신 맡아서 처리하게 되었습니다. web.xml에 DispatcherServlet의 <url-pattern>을 '/'로 설정함으로써 동시에 이제 모든 요청은 DispatcherServlet으로 전달됩니다. 물론 DispatcherServlet을 web.xml에 등록해도 계속 서블릿을 web.xml에 매핑해서 사용할 수 있지만, 이런 옛 방식을 버리고 DispatcherServlet을 이용해 웹 개발을 한다면 앞으로 서블릿 파일을 만들 필요도 없어지고 동시에 놀라운 @MVC의 혜택을 얻을 수 있습니다.  
  
DispatcherServlet을 이용한다는 것은 스프링에서 제공하는 @MVC를 이용하겠단 뜻입니다. @MVC는 그동안 추상적으로 알아오고 발전했던 MVC(Model, View, Controller) 설계 영역을 노골적으로 분할하여 사용자가 무조건 MVC로 어플리케이션을 설계하게끔 유도하는 방식입니다. 즉, @MVC를 이용해 어플리케이션을 개발한다면 MVC 설계의 원칙대로 웹 어플리케이션을 제작할 수 있게 된다는 뜻입니다.  
  
그럼 간단하게 DispatcherServlet이 담당하는 역할이 무엇인지 알아봅시다. 먼저 DispatcherServlet에 대해 간단히 정의해보자면, 각각 분리하여 만든 Model, View, Controller를 조합하여 브라우저로 출력해주는 역할을 수행합니다.  
  
Spring MVC 구조  
  
  
등장 요소  
DispatcherServlet : 프런트 컨트롤러 담당, 모든 HTTP 요청을 받아들여 그 밖의 오브젝트 사이의 흐름을 제어, 기본적으로 스프링 MVC의 DispatcherServlet 클래스를 그대로 적용  
HandlerMapping : 클라이언트의 요청을 바탕으로 어느 컨트롤러를 실행할지 결정  
Model : 컨트롤러에서 뷰로 넘겨줄 오브젝트를 저장하기 위한 오브젝트, HttpServletRequest와 HttpSession처럼 String 형 키와 오브젝트를 연결해서 오브젝트를 유지  
ViewResolver : View 이름을 바탕으로 View 오브젝트를 결정  
View : 뷰에 화명 표시 처리를 의뢰  
비즈니스 로직 : 비즈니스 로직을 실행. 애플리케이션 개발자가 비즈니스 처리 사양에 맞게 작성  
컨트롤러(Controller) : 클라이언트 요청에 맞는 프레젠테이션 층의 애플리케이션 처리를 실행해야 함. 애플리케이션 개발자가 애플리케이션 처리 사양에 맞게 작성  
뷰 / JSP 등 : 클라이언트에 대해 화면 표시 처리. 자바에서는 JSP 등으로 작성하는 일이 많으며, 애플리케이션 개발자가 화면의 사양에 맞게 작성  
동작 순서  
DispatcherServlet은 브라우저로부터 요청을 받아들입니다.  
DispatcherServlet은 요청된 URL을 HandlerMapping 오브젝트에 넘기고 호출 대상의 컨트롤러 오브젝트를 얻어 URL에 해당하는 메서드를 실행합니다.  
컨트롤러 오브젝트는 비즈니스 로직으로 처리를 실행하고, 그 결과를 바탕으로 뷰에 전달할 오브젝트를 Model 오브젝트에 저장합니다. 끝으로 컨트롤러 오브젝트는 처리 결과에 맞는 View 이름을 반환합니다.  
DispatcherServlet은 컨트롤러에서 반환된 View 이름을 ViewResolver에 전달해서 View 오브젝트를 얻습니다.  
DispatcherServlet은 View 오브젝트에 화면 표시를 의뢰합니다.  
View 오브젝트는 해당하는 뷰를 호출해서 화면 표시를 의뢰합니다.  
뷰는 Model 오브젝트에서 화면 표시에 필요한 오브젝트를 가져와 화면 표시 처리를 실행합니다.  
참고  
스프링4 입문 - 한빛미디어

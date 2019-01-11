---
title: "스프링 시작1 - 프로젝트 기본 디렉토리 구조"
date: 2018-01-11 08:52:28 -0400
categories: 
  - spring
---

## 스프링 프로젝트 기본 디렉토리 구조 ##


src/main/java : 자바코드(컨트롤러, 모델)
src/main/resources : 자바 코드에서 사용할 리소스(mapper, sql)
src/test/java : 테스트 코드
src/test/resources : 테스트 코드에서 사용할 리소스
Maven Dependencies : 라이브러리 관리도구(maven에서 다운받은 jar파일)
src : web디렉토리
src/main/webapp/resources : js, css, image 등등을 관리
src/main/webapp/WEB-INF/classes : 컴파일된 클래스
src/main/webapp/WEB-INF/spring : 스프링 환경설정파일(root-context.xml, servlet-context.xml)
src/main/webapp/WEB-INF/views : html, jsp파일
src/main/webapp/ : 외부접근 가능
src/main/webapp/WEB-INF : 외부접근 불가, 컨트롤러를 경유해서 접근 가능
*WEB-INF폴더
외부에서 직접 접속이 차단되어있다. 그 이유는 컴파일된 클래스와 스프링 환경설정파일(DB연결정보)이 존재하기 때문이다
JSP 또한 외부로 접속하여 수정되는 것을 방지하기 위한 보안 때문에 외부접근이 금지되어있다.

pom.xml : maven에서 참조하는 설정파일
maven은 빌드와 관련된 정보를 프로젝트 객체모델(Project Object Model)이라는 이름으로 정의하고 사용하는데 pom이라는 이름으로된 pom.xml파일을 사용한다.

*maven의 로컬저장소 
C:\Users\사용자계정\.m2\repository
pom.xml에서 dependency태그를 추가하고 설정하고싶은 라이브러리를 추가하면 된다.
라이브러리는 maven repository에서 원하는 라이브러리를 검색하여 내용을 복사하여 추가해주면 maven이 알아서 jar파일을 로컬저장소에 다운받아준다. 
https://mvnrepository.com/



기존의 웹프로젝트의 경우에는 프로젝트에 필요한 모든 라이브러리 파일을 직접 다운로드 받아 해당 라이브러리 폴더에 적용시켜줘야했고, 각각의 프로젝트마다 다시 또 적용해야하는 불편함이 있었는데 스프링의 경우에는 denpendency태그를 적용시켜주면 알아서 다운로드 받고 해당 프로젝트에 적용할 있다. 또한 다른 프로젝트 생성 시에는 같은 denpendency태그만 적용시켜주면 별도의 다운로드가 필요없이 로컬저장소에 저장된 라이브러리를 자동으로 적용시켜준다.  

maven repository에서 mysql 검색 후 denpendency태그복사 후 pom.xml에 붙여넣기

Spring 이란
==========
풀네임은 Spring Framework로 자바 플랫폼을 위한 오픈소스 애플리케이션 프레임워크이다.

동적인 웹사이트를 개발하기 위한 여러 서비스를 제공한다.

대한민국에서 가장 많이 쓰이는 웹 프레임워크이며 공공기관에서도 권장하는 전자정부 표준 프레임워크이다.

***
장점
---
    - 경량 컨테이너
    - IoC (Invertion of Control, 제어역행)
    - Di (Dependency Injection, 의존성 주입)
    - AOP (Aspect-Oriented Programming, 관점지향 프로그래밍)

***
Spring Boot
-----------
Spring은 출시일이 오래된 만큼 많은 기능이 있어 프로젝트 초기설정이 매우 복잡하다. 따라서 Spring Boot를 통해 Spring의 많은 부분을 자동화하여 사용자가 편하게 Spring을 접하고 활용할 수 있도록 한다.

Spring Boot의 Starter dependency만 추가하면  바로 API를 정의하고, 내장된 Tomcat이나 Jetty로 웹 서버를 실행할 수 있다.

심지어 Spring 홈페이지의 [Spring Initializr] [link2]를 사용하면 바로 실행 가능한 코드를 만들어준다. 실행환경이나 의존성 관리 없이 바로 코딩을 시작하면 되서 엄청난 간편성을 제공한다.

***
차이점
----
    - Embbeded Tomcat을 사용하기 때문에, 따로 Tomcat을 설치하거나 버전관리 수고를 덜어준다.
    - Starter를 통한 Dependency 자동화로 Dependency들의 버전을 맞춰줄 필요가 사라지고 버전관리 또한 용이하게 되었다.
    - XML 설정을 하지 않아도 된다.
    - Jar 파일로 배포가 가능해 내장된 Tomcat을 포함한 배포가 손쉽게 가능하다.
    - Spring Actuator를 이용한 어플리케이션의 모니터링과 관리 기능을 제공한다.

***
Spring Boot Starter란?
----------------------
앞서 Spring Boot와의 차이점 중 Dependency 자동화에 대해 언급했다.

여기서 Starter란 무엇일까?

Starter란 특정 목적을 달성하기 위한 의존성 그룹이라고 생각하면 이해하기 쉽다.

Starter는 마치 npm처럼 간편하게 Dependency를 제공해주는데, 만약 우리가 JPA가 필요하다면 prom.xml (MAVEN)이나 build.gradle (Gradle)에
```
spring-boot-starter-data-jpa
```
만 추가해주면 Spring Boot가 그에 필요한 라이브러리들을 알아서 받아온다.

```
spring-boot-starter-*
```
Starter의 명명 규칙은 위와 같다. 따라서 * 이전까지 입력하면 웬만해서는 개발도구 (Vscode, IntelliJ)가 자동완성으로 가능한 Dependency들을 알려준다.
또한 명명규칙이 있어 그 규칙을 알면 원하는 라이브러리를 손쉽게 Import할 수 있다.

***
Spring과 Spring Boot의 배포방법
----------------------------
Spring Boot와의 차이점 중 배포방법도 차이가 존재한다.

Spring Boot는 Spring과 달리 실행 가능한 JAR (Executable Jar)로 빌드하여 프로젝트를 바로 실행시킬 수 있다. 이렇게 하면 Tomcat도 내장되어 즉각적인 실행이 가능한 것이다.

Spring은 WAR로 밖에 배포할 수 없다. 그럼에도 JAR가 아닌 WAR로 배포하는 경우도 생기는데, 이 둘의 차이점과 제약사항을 알아보자.

***
JAR? WAR?
---------
기본적으로 JAR, WAR 모두 Java의 jar 옵션 (Java -jar)을 이용해 생성된 압축(아카이브) 파일로, 어플리케이션을 쉽게 배포하고 동작시킬 수 있도록 관련 파일(리소스, 속성 파일 등)을 패키징 한 것이다.

JAR (Java Archive)   
* Java 어플리케이션이 동작할 수 있도록 프로젝트를 압축한 파일
* Class(리소스, 속성 파일), 라이브러리 파일을 포함
* JRE(Java Runtime Environment)만 있어도 실행 가능

WAR (Web Application Archive)   
* Servlet / Jsp 컨테이너에 배치할 수 있는 웹 어플리케이션 압축파일 포맷
* 웹 관련 자원을 포함 (JSP, Servlet, JAR, Class, XML, HTML, Javascript 등)
* 사전 정의된 구조 사용 (WEB-INF, META-INF)
* 실행을 위해 별도의 웹 서버(WEB) 또는 웹 컨테이너(WAS) 필요
* JAR 파일의 일종으로 오직 웹 어플리케이션 부분만을 패키징하기 위한 파일

***
JAR 파일 구조
-----------
Spring Boot 공식 문서에서 소개하는 JAR 파일은 BOOT-INF, META-INF, org 세 폴더로 이뤄져 있다.

BOOT-INF
* 개발자가 직접 작성한 Class 파일들(classes)과 의존성 포함을 위한 jar 파일들(lib)로 구성되어 있다.
* classpath.idx 파일은 classpath에 추가될 jar 파일들의 목록(lib 폴더 내 jar)을 정의한 것이다. 일반적인 jar 파일은 중첩된 jar 파일 구조를 지원하지 않는데 이러한 단점을 보완하기 위한 Spring Boot만의 방법이다.

META-INF
* 프로젝트 매니페스트 파일(MANIFEST.MF)을 포함하는 폴더이다. 매니페스트 파일은 파일 그룹을 위한 메타데이터(이름, 버전정보, 라이센스, 프로그램의 구성 등)를 포함하는 파일이다. 일반적인 JAR 파일의 MANIFEST에서 Main-Class는 Main 메서드가 존재하는 클래스로 설정되지만, Spring Boot의 Main-Class에서는 JarLauncher라는 클래스로 설정되어 있다. (WAR 파일에는 WarLauncher)
* JarLauncher를 통한 Jar의 실행순서는 다음과 같다.
  1. org.springframework.boot.loader.jar.JarFile: 내장 jar 인식
  2. org.springframework.boot.loader.Launcher
  3. Start-Class에 선언된 클래스의 Main 메서드 실행 (com.example.demo.DemoApplication)

org
* 위에 설명한 Spring Boot loader classes 모듈이 저장되어 있다.

***
WAR 파일 구조
-----------
WAR 파일은 WEB-INF, META-INF, org 폴더로 이루어져 있다. JAR과의 차이점은 BOOT-INF 대신 WEB-INF가 있다는 것이다.

WEB-INF
* 개발자가 직접 입력한 Class와 jar 파일, JSP일 경우 view 파일들까지 포함되어 있는 폴더이다. 따라서 외장 WAS나 JSP를 사용할 일이 있다면 WAR를 이용하여 배포해야 한다.

META-INF
* JAR와 동일하게 MANIFEST.MF가 존재한다.

WAR 단독으로 사용할 수 없는 이유는 Main-Class에 Spring Loader로 설정되어 있기 때문이다. 때문에 bootWar로 빌드를 한다면 WAR 단독으로 실행이 가능하다.

**Spring Boot에서 가이드하는 표준은 JAR이므로 특별히 JSP를 사용하거나 외장 WAS를 사용해야하는 일이 아니면 WAR이 아닌 JAR로 배포하도록 하자.**

***
참고자료
------
    [Spring과 Spring Boot 차이][link1]

    [Spring Initializr][link2]

    [link1]: https://velog.io/@courage331/Spring-과-Spring-Boot-차이

    [link2]: https://start.spring.io

    [link3]: https://hye0-log.tistory.com/27

    [link4]: https://hpotter1993.tistory.com/71


    
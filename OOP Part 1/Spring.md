Spring �̶�
==========
Ǯ������ Spring Framework�� �ڹ� �÷����� ���� ���¼ҽ� ���ø����̼� �����ӿ�ũ�̴�.

������ ������Ʈ�� �����ϱ� ���� ���� ���񽺸� �����Ѵ�.

���ѹα����� ���� ���� ���̴� �� �����ӿ�ũ�̸� ������������� �����ϴ� �������� ǥ�� �����ӿ�ũ�̴�.

***
����
---
    - �淮 �����̳�
    - IoC (Invertion of Control, �����)
    - Di (Dependency Injection, ������ ����)
    - AOP (Aspect-Oriented Programming, �������� ���α׷���)

***
Spring Boot
-----------
Spring�� ������� ������ ��ŭ ���� ����� �־� ������Ʈ �ʱ⼳���� �ſ� �����ϴ�. ���� Spring Boot�� ���� Spring�� ���� �κ��� �ڵ�ȭ�Ͽ� ����ڰ� ���ϰ� Spring�� ���ϰ� Ȱ���� �� �ֵ��� �Ѵ�.

Spring Boot�� Starter dependency�� �߰��ϸ�  �ٷ� API�� �����ϰ�, ����� Tomcat�̳� Jetty�� �� ������ ������ �� �ִ�.

������ Spring Ȩ�������� [Spring Initializr] [link2]�� ����ϸ� �ٷ� ���� ������ �ڵ带 ������ش�. ����ȯ���̳� ������ ���� ���� �ٷ� �ڵ��� �����ϸ� �Ǽ� ��û�� ������ �����Ѵ�.

***
������
----
    - Embbeded Tomcat�� ����ϱ� ������, ���� Tomcat�� ��ġ�ϰų� �������� ���� �����ش�.
    - Starter�� ���� Dependency �ڵ�ȭ�� Dependency���� ������ ������ �ʿ䰡 ������� �������� ���� �����ϰ� �Ǿ���.
    - XML ������ ���� �ʾƵ� �ȴ�.
    - Jar ���Ϸ� ������ ������ ����� Tomcat�� ������ ������ �ս��� �����ϴ�.
    - Spring Actuator�� �̿��� ���ø����̼��� ����͸��� ���� ����� �����Ѵ�.

***
Spring Boot Starter��?
----------------------
�ռ� Spring Boot���� ������ �� Dependency �ڵ�ȭ�� ���� ����ߴ�.

���⼭ Starter�� �����ϱ�?

Starter�� Ư�� ������ �޼��ϱ� ���� ������ �׷��̶�� �����ϸ� �����ϱ� ����.

Starter�� ��ġ npmó�� �����ϰ� Dependency�� �������ִµ�, ���� �츮�� JPA�� �ʿ��ϴٸ� prom.xml (MAVEN)�̳� build.gradle (Gradle)��
```
spring-boot-starter-data-jpa
```
�� �߰����ָ� Spring Boot�� �׿� �ʿ��� ���̺귯������ �˾Ƽ� �޾ƿ´�.

```
spring-boot-starter-*
```
Starter�� ��� ��Ģ�� ���� ����. ���� * �������� �Է��ϸ� �����ؼ��� ���ߵ��� (Vscode, IntelliJ)�� �ڵ��ϼ����� ������ Dependency���� �˷��ش�.
���� ����Ģ�� �־� �� ��Ģ�� �˸� ���ϴ� ���̺귯���� �ս��� Import�� �� �ִ�.

***
Spring�� Spring Boot�� �������
----------------------------
Spring Boot���� ������ �� ��������� ���̰� �����Ѵ�.

Spring Boot�� Spring�� �޸� ���� ������ JAR (Executable Jar)�� �����Ͽ� ������Ʈ�� �ٷ� �����ų �� �ִ�. �̷��� �ϸ� Tomcat�� ����Ǿ� �ﰢ���� ������ ������ ���̴�.

Spring�� WAR�� �ۿ� ������ �� ����. �׷����� JAR�� �ƴ� WAR�� �����ϴ� ��쵵 ����µ�, �� ���� �������� ��������� �˾ƺ���.

***
JAR? WAR?
---------
�⺻������ JAR, WAR ��� Java�� jar �ɼ� (Java -jar)�� �̿��� ������ ����(��ī�̺�) ���Ϸ�, ���ø����̼��� ���� �����ϰ� ���۽�ų �� �ֵ��� ���� ����(���ҽ�, �Ӽ� ���� ��)�� ��Ű¡ �� ���̴�.

JAR (Java Archive)   
* Java ���ø����̼��� ������ �� �ֵ��� ������Ʈ�� ������ ����
* Class(���ҽ�, �Ӽ� ����), ���̺귯�� ������ ����
* JRE(Java Runtime Environment)�� �־ ���� ����

WAR (Web Application Archive)   
* Servlet / Jsp �����̳ʿ� ��ġ�� �� �ִ� �� ���ø����̼� �������� ����
* �� ���� �ڿ��� ���� (JSP, Servlet, JAR, Class, XML, HTML, Javascript ��)
* ���� ���ǵ� ���� ��� (WEB-INF, META-INF)
* ������ ���� ������ �� ����(WEB) �Ǵ� �� �����̳�(WAS) �ʿ�
* JAR ������ �������� ���� �� ���ø����̼� �κи��� ��Ű¡�ϱ� ���� ����

***
JAR ���� ����
-----------
Spring Boot ���� �������� �Ұ��ϴ� JAR ������ BOOT-INF, META-INF, org �� ������ �̷��� �ִ�.

BOOT-INF
* �����ڰ� ���� �ۼ��� Class ���ϵ�(classes)�� ������ ������ ���� jar ���ϵ�(lib)�� �����Ǿ� �ִ�.
* classpath.idx ������ classpath�� �߰��� jar ���ϵ��� ���(lib ���� �� jar)�� ������ ���̴�. �Ϲ����� jar ������ ��ø�� jar ���� ������ �������� �ʴµ� �̷��� ������ �����ϱ� ���� Spring Boot���� ����̴�.

META-INF
* ������Ʈ �Ŵ��佺Ʈ ����(MANIFEST.MF)�� �����ϴ� �����̴�. �Ŵ��佺Ʈ ������ ���� �׷��� ���� ��Ÿ������(�̸�, ��������, ���̼���, ���α׷��� ���� ��)�� �����ϴ� �����̴�. �Ϲ����� JAR ������ MANIFEST���� Main-Class�� Main �޼��尡 �����ϴ� Ŭ������ ����������, Spring Boot�� Main-Class������ JarLauncher��� Ŭ������ �����Ǿ� �ִ�. (WAR ���Ͽ��� WarLauncher)
* JarLauncher�� ���� Jar�� ��������� ������ ����.
  1. org.springframework.boot.loader.jar.JarFile: ���� jar �ν�
  2. org.springframework.boot.loader.Launcher
  3. Start-Class�� ����� Ŭ������ Main �޼��� ���� (com.example.demo.DemoApplication)

org
* ���� ������ Spring Boot loader classes ����� ����Ǿ� �ִ�.

***
WAR ���� ����
-----------
WAR ������ WEB-INF, META-INF, org ������ �̷���� �ִ�. JAR���� �������� BOOT-INF ��� WEB-INF�� �ִٴ� ���̴�.

WEB-INF
* �����ڰ� ���� �Է��� Class�� jar ����, JSP�� ��� view ���ϵ���� ���ԵǾ� �ִ� �����̴�. ���� ���� WAS�� JSP�� ����� ���� �ִٸ� WAR�� �̿��Ͽ� �����ؾ� �Ѵ�.

META-INF
* JAR�� �����ϰ� MANIFEST.MF�� �����Ѵ�.

WAR �ܵ����� ����� �� ���� ������ Main-Class�� Spring Loader�� �����Ǿ� �ֱ� �����̴�. ������ bootWar�� ���带 �Ѵٸ� WAR �ܵ����� ������ �����ϴ�.

**Spring Boot���� ���̵��ϴ� ǥ���� JAR�̹Ƿ� Ư���� JSP�� ����ϰų� ���� WAS�� ����ؾ��ϴ� ���� �ƴϸ� WAR�� �ƴ� JAR�� �����ϵ��� ����.**

***
�����ڷ�
------
    [Spring�� Spring Boot ����][link1]

    [Spring Initializr][link2]

    [link1]: https://velog.io/@courage331/Spring-��-Spring-Boot-����

    [link2]: https://start.spring.io

    [link3]: https://hye0-log.tistory.com/27

    [link4]: https://hpotter1993.tistory.com/71


    
# JVM의 작동원리

1. [JAVA의 실행 순서](#JAVA의-실행-순서)
2. [JVM 구조](#JVM-구조)
3. [클래스 로더](#클래스-로더)
4. [JVM 메모리 구조] - 추가 예정


## JAVA의 실행 순서
- JVM의 메모리 구조 및 GC의 동작을 이해하기 위해서는 자바의 실행이 어떻게 이루어 지는지 큰 그림으로 이해할 필요가 있을 것 같다.
- 자바의 경우 고수준 프로그램 언어로 사용자가 작성한 소스코드를 컴퓨터가 이해할 수 있도록 변환하는 작업이 필요하다. 따라서 여느 프로그램 언어들과 마찬가지로 컴파일러가 필요하다.
> 컴파일러는 인간이 작성한 코드를 컴퓨터가 이해할 수 있도록 바이트 코드로 변환하는 역할을 한다.

![Alt Text](https://scaler.com/topics/images/how-does-java-programming-language-work.webp)
[자바 실행순서](https://www.scaler.com/topics/java/how-java-program-works/)  
1. **Java 파일**
   - 편집기를 통해 작성한 java 소스코드는 .java라는 확장자를 갖는다. 컴파일 되기 전 파일 형태
2. **Class 파일**
    - 컴파일러를 통해 바이트 코드로 변환된 파일로 .class라는 확장자를 갖는다. .class 파일은 시스템에 상관없이 어디에서나 실행될 수 있다.
    - 자바를 설치할 때 JDK를 설치하게 되는데, 여기에 컴파일러가 같이 포함되어 있다.
    - C언어에서 컴파일을 하게 되면, .o 파일이 생성되는데 이는 **바이너리 코드**[1]이며, JAVA언어에서 컴파일 했을 때 생성되는 **바이트 코드**와는 차이가 있다.
      - 바이너리 코드 : 0과 1로 이루어져 있으며,CPU가 사용하는 명령어 집합인 **기계어**가 바이너리 코드로 되어 있다. 기계어는 CPU 제조사마다 차이가 있다.
      - 바이트 코드 : CPU가 아닌 가상머신(Virtual Machine)이 이해할 수 있는 언어로, 가상머신이 이해할 수 있는 바이너리 코드이다. 따라서 최종적으로 컴퓨터(CPU)가 이해할 수 있도록 바이너리 코드로 변환하는 작업이 필요하다.(JIT 컴파일러)
3. **JVM**
   - 컴파일러를 통해 변환된 바이트 코드 파일(.class)은 JVM 위에서 실행된다. 바이트 코드가 실행되는 과정은 JVM 메모리 구조에서 자세하게 설명할 예정.
   - 자바로 작성된 애플리케이션은 모두 JVM에서만 실행되기 때문에, 자바 어플리케이션의 실행을 위해서는 JVM이 반드시 필요하다. 일반 애플리케이션 코드는 OS를 거치고 바로 하드웨어로 전달 되지만, Java는 JVM을 거치고 해당 하드웨어에 맞게 실행 시 해석(Interpret)되기 된다.(과거의 느린 속도를 보완하기 위해 탄생한 것이 JIT 컴파일러 - 바이트코드를 기계어로 변환)
   - Java 애플리케이션은 오직 JVM하고 상호작용을 하기 때문에 OS에는 독립적이지만, OS에서 실행가능한 JVM이 필요하다. (Java는 JVM 내에서 동작하기 때문에 JVM의 구조를 알아야 할 필요가 있다.)

## JVM 구조
- JVM은 Java 응용 프로그램을 실행하기 위한 런타임 엔진 역할을 한다. JVM을 통해 Java 소스코드에 있는 메서드를 실제로 호출하는 것이다. 따라서 자바를 실행하기 위한 최소한의 요구사항을 제공하는 JRE(Java Runtime Environment)안에 JVM이 포함되어 있다.
![Alt Text](https://scaler.com/topics/images/java-development-kit.webp)
[JRE와 JVM](https://www.scaler.com/topics/java/how-java-program-works/)
- 컴파일러를 통해 변환된 .class 파일(바이트 코드 파일)을 JVM에서 실행하면 먼저 바이트 코드를 메모리에 적재하는 작업이 필요하다. 이를 담당하는 것이 **클래스 로더**이다.
  - 클래스 로더는 크게 세 가지 활동을 담당한다.
    - Loading
    - Linking
    - Initialization

![Alt Text](https://media.geeksforgeeks.org/wp-content/uploads/jvm-3.jpg)
[JVM 구조](https://www.geeksforgeeks.org/jvm-works-jvm-architecture/)
### 1. Loading
- JVM은 바이트 코드를 한줄한줄 해석하면서 바이너리 코드로 변환하여 메소드 영역(Method Area)에 저장한다. 메소드 영역에는 클래스의 이름, 해당 클래스 파일이 다른 클래스, 인터페이스 등과 관련되어 있는지 여부, 변수 및 메서드 정보 등이 저장된다. 
### 2. Linking
- 읽어낸 클래스가 올바른 형식으로 구성되어 있는지, 유효한 컴파일러에 의해 생성되어 있는지 여부를 확인한다. **(코드의 유효성을 판단하는 작업은 반드시 필요하기 때문)**
- 클래스가 필요로 하는 메모리를 할당한다.
### 3. Initialization
- 클래스 변수들을 적절한 값으로 초기화 한다.

## 클래스 로더
- 자바는 모든 클래스를 메모리에 올리지 않고, 필요할 때마다 메로리를 사용하는 동적 로딩방식을 사용한다. 이를 담당하는 것이 클래스 로더이다. 클래스 로더는 계층적 구조로 나뉘어 있으며, 각 클래스 로더마다 불러오는 클래스가 다르다.
    ### 1) Bootstrap Class Loader
    - JVM 시작 시 가장 먼저 실행되는 클래스 로더이다. java.lang.Object 같은 기본적인 클래스를 로딩한다.
    ### 2) Extension Class Loader (Java 9 이후, Platform Class Loader로 이름 변경)
    - Java 8) 이름 그대로 Bootstrap Class Loader에서 보다 확장된 클래스들을 로딩한다. /jre/lib/ex 경로 내에 있는 클래스들을 찾아서 로딩한다. `URLClassLoader`를 상속한다.
    - Java 9 이후) BuiltinClassLoader를 상속
    ### 3) Application Class Loader
    - 사용자가 직접 정의한 클래스들은 대부분 여기에서 로딩한다.  


- 클래스 로더의 동작 방식[2]을 이해하려면 먼저 클래스 로더가 지켜야 할 세 가지 원칙을 알아야 한다.
    1) 위임 원칙(Delegation Principle)
        - 클래스 로딩이 필요할 때 자신의 상위 계층 클래스 로더에게 클래스 로딩 업무를 위임한다.
       ![Alt Text](https://i.imgur.com/kijdBjb.png)
       [클래스 로더가 위임하는 방식](https://homoefficio.github.io/2018/10/13/Java-%ED%81%B4%EB%9E%98%EC%8A%A4%EB%A1%9C%EB%8D%94-%ED%9B%91%EC%96%B4%EB%B3%B4%EA%B8%B0/)
    2) 가시범위 원칙(Visibility Principle)
        - 하위 클래스로더는 상위 클래스로더가 로딩한 클래스들을 볼 수 있지만 상위 클래스는 하위 클래스가 로딩한 클래스를 볼 수 없다.
        - 하위 클래스로더가 상위 클래스로더의 클래스, 예를 들어 Object 클래스를 볼 수 없다면, 사용자가 정의한 클래스도 상위 클래스가 로딩한 클래스를 사용할 수 없을 것이다.
        - 상위 클래스로더가 하위 클래스 로더를 볼 수 없는 이유는 상위와 하위를 구분하기 위해서 이다.
    3) 유일성의 원칙(Uniqueness Principle)
        - 로딩된 클래스는 중복되어 로딩되지 않도록 고유한 바이너리 이름을 부여 받는다.
        - 하위 클래스로더는 상위 클래스로더에게 이미 로딩된 클래스를 다시 로딩하지 않도록 하기 위함이다.
        - toString()으로 클래스를 출력할 때, java.lang.String, javax.swing.JSpinner$DefaultEditor, java.security.KeyStore$Builder$FileBuilder$1, java.net.URLClassLoader$3$ 등이 binary name이다. [binary name 명명법](https://docs.oracle.com/javase/specs/jls/se8/html/jls-13.html#jls-13.1)

## 클래스 로더의 동적 로딩
- JVM은 실행에 필요한 모든 클래스를 메소드 영역에 로딩하지 않는다. 클래스가 호출되는 시점에서 필요한 클래스들을 그때그때 로딩하는 작업을 한다.
- [이하 내용은 해당 게시글의 내용을 가져왔습니다.](https://steady-coding.tistory.com/593)
- ```java
    public class HelloWorld { 
        public static void main(String[] args) { 
                System.out.println("안녕하세요!"); 
        } 
    }
    ```
    JVM이 실행되고, 가장 먼저 Bootstrap 클래스 로더가 생성된다. 이 때, Object 클래스를 읽어온다. 클래스 로더는 HelloWorld.class를 읽은 후 HelloWorld 클래스에서 필요한 `java.lang.String`과 `java.lang.System`을 로딩한다.
    이처럼 하나의 클래스를 로딩하는 과정에서 동적으로 다른 클래스를 로딩하는 방식을 **로드 타임 동적로딩**이라고 한다.
- ```java
    public class RuntimeLoading { 
        public static void main(String[] args) { 
                try { 
                        Class cls = Class.forName(args[0]); 
                        Object obj = cls.newInstance(); 
                        Runnable r = (Runnable) obj; 
                        r.run(); 
                } catch (Exception e) {
                        e.printStackTrace();
                }
        }
    }
  ```
  Class.forName() 메서드를 실행하기 전까지는 RuntimeLoading 클래스가 어떤 클래스를 참조하는지 알 수 없다. 따라서 RuntimeLoading 클래스를 로딩할 때는 관련된 다른 클래스들을 로딩하지 않고, forName 메서드가 호출되는 순간에 매개변수에 해당하는 클래스를 그 순간 로딩한다. 이처럼 클래스를 로딩할 때가 아닌 코드가 실행되는 순간에 클래스를 로딩하는 것을 **런타임 동적 로딩**이라고 한다.

내용이 이해가 잘 가지 않더라도 이런게 있구나 정도만 이해하고 넘어가도 될 것 같다. 이후에 자바를 공부하면서 계속해서 나올 내용인 것 같으므로, 그 때 좀 더 자세하게 이해할 수 있을 것 같다.
    
        


참고 자료)  
https://inspirit941.tistory.com/294  
https://www.scaler.com/topics/java/how-java-program-works/


[1]: https://kingofbackend.tistory.com/122
[2]: https://homoefficio.github.io/2018/10/13/Java-%ED%81%B4%EB%9E%98%EC%8A%A4%EB%A1%9C%EB%8D%94-%ED%9B%91%EC%96%B4%EB%B3%B4%EA%B8%B0/


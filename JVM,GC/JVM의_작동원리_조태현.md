# JVM의 작동원리
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

https://inspirit941.tistory.com/294  
https://www.scaler.com/topics/java/how-java-program-works/

https://steady-coding.tistory.com/593 : 클래스 로더에 대한 설명



















[1]: https://kingofbackend.tistory.com/122

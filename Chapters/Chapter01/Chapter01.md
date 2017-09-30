# JAVA Basic Language
## Chapter 01. About JAVA

### 1.1 프로그래밍 언어
* 프로그래밍 언어 구분 <br>
    * 고급 언어 : 프로그래밍 언어 중, 사람이 상대적으로 이해하기 쉬운 언어. 기계어(0101010000...) 번역을 위한 컴파일(Compile) 과정 필요
    * 저급 언어 : 프로그래밍 언어 중, 기계어에 가까워 사람이 학습 / 이해하기 어려운 언어.


> 프로그램 : 프로그래밍 언어로 작성된 소스(source)를 기계어로 번역한 것.

<br>

### 1.2 JAVA
#### 1.2.1 자바
* 1995 Sun Microsystems 발표<br>

#### 1.2.2 자바의 특성
**1. 이식성이 높음**
  * JAVA 언어로 개발된 프로그램은 JRE(Java Runtime Environment)가 설치된 모든 운영체제에서 실행이 가능하다.
    * Source File > Compile > Byte Code File > Windows/Linux/Mac...<br>
    : 바이트 코드 파일을 각 운영체제 별 JVM이 분석해 실행한다.

**2. 객체 지향 언어**
  * OOP(Object Oriented Programming)
    * 한 프로그램에서 부품에 해당하는 객체를 생성하고, 이를 연결/조립해 프로그램을 완성하는 기법
    * 캡슐화, 상속, 다형성 보유

**3. 함수적 스타일 코딩**
  * 대용량 데이터 병렬 처리, 이벤트 처리에 용이한 코딩 기법
  * JAVA는 Lamda Expression을 통해 함수적 프로그래밍을 지원함.

**4. 메모리 자동 관리**
  * C++과 달리, JAVA는 객체 생성 시 자동으로 메모리 영역이 할당 되고 사용이 완료되면 Garbage Collector가 이를 제거한다.

**5. 멀티 스레드(Multi-Thread)구현**
  * OS에 따라 멀티 스레드 구현 방법은 다르지만, JAVA는 스레드 생성 및 제어 관련 API를 제공하고 있어서 운영체제와 상관 없이 멀티 스레드를 쉽게 구현할 수 있다.

**6. 동적 로딩(Dynamic Loading)지원**
  * 어플리케이션이 실행 될 때 객체가 일괄 생성되지 않고, 객체 필요 시점에 *클래스* 를 동적으로 로딩해 객체를 생성한다.<br>

#### 1.2.3 JVM
  * JAVA 프로그램은 완전한 기계어가 아닌, Byte Code(* . class 파일) 이므로, 각 운영체제 별 JVM상에서 이를 실행하게 된다.(java.exe)
  * 즉, 소스파일(* . java) >> 컴파일러(javac.exe) >> 바이트코드 파일(* . class) >> (OS별) JVM구동(java.exe)의 과정을 거치게 된다.

## Chapter 05. Reference Type (참조 타입)

## 5.1 데이터 타입 분류
* 기본 타입(Primitive Type)
  * 정수, 실수, 논리 타입 - 실제 값을 변수에 직접 저장
* 참조 타입(Reference Type)
  * 배열, 열거, 클래스, 인터페이스 - **메모리의 번지** 를 변수에 저장

## 5.2 메모리 사용 영역
* JVM Runtime Data Area
(그림)

### 5.2.1 메소드(Method) 영역
* 코드에서 사용되는 클래스(~.class)들을 클래스 로더로 읽어 각 클래스 별로 데이터를 저장
  * 생성자(Constructor)
  * 런타임 상수 풀(runtime constant pool)
  * 필드(Field)데이터
  * 메소드(Method) 데이터
  * 메소드(Method) 코드

### 5.2.2 힙(Heap) 영역
* 객체, 배열이 생성되는 영역 - JVM스택의 변수 / 다른 객체의 필드에서 참조
  * 참조하는 변수나 객체가 없을 경우 Garbage Collector 실행

### 5.2.3 JVM 스택(Stack) 영역
* 각 Thread가 start될 때 1개씩 생성
* primitive 타입 변수와 변수 값이 저장
  * reference 타입 변수일 경우 heap 영역이나 method 영역의 객체의 주소를 갖는다.
* method 호출 시 frame push(생성) ~ pop(제거)
  * frame 내부에는 local variables stack이 존재하고, 역시 push ~ pop 과정을 거친다.

<br>

## 5.3 참조 변수의 ==, != 연산

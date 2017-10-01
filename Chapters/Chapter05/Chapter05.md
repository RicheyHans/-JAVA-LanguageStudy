## Chapter 05. Reference Type (참조 타입)

## 5.1 데이터 타입 분류
* 기본 타입(Primitive Type)
  * 정수, 실수, 논리 타입 - 실제 값을 변수에 직접 저장
* 참조 타입(Reference Type)
  * 배열, 열거, 클래스, 인터페이스 - **메모리의 번지** 를 변수에 저장

<br>

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
* reference 타입 변수에서의 ==, != 연산은 동일 객체 참조 여부를 검사한다.
  * 즉, 동일한 heap 영역의 **메모리 주소** 를 갖고 있는지 여부 조사
* String 변수의 케이스

<br>

## 5.4 null과 NullPointerException
* null 변수 : 'heap 영역의 객체를 참조하지 않는다'는 의미의 변수
  * 초기값으로 사용 가능 -> stack 영역에 생성 가능

* ==, != 연산으로 null 여부 확인 가능(boolean)

* NullPointerException
  * **null을 가진 참조타입 변수는 사용이 불가능**(초기화만 가능)
    >null을 가진 배열 특정 인덱스에 값을 할당하는 경우<br>
    >null을 가진 String 변수의 길이를 구하는 경우

<br>

## 5.5 String 타입
* String 타입은 문자열 리터럴이 동일할 경우 동일 객체를 참조한다.
  ```
  String str1 = "한승범";
  String str2 = "한승범";
  ```
  > str1, str2는 동일 객체를 참조하며 == 연산 사용 시 true 출력

* **new 연산자 : heap 영역에 새로운 객체를 생성하는 객체 생성 연산자**
  ```
  String str1 = new String("한승범");
  String str2 = new String("한승범");
  ```
  > 이 경우 str1, str2는 다른 객체를 참조하므로 == 연산 사용 시 false 출력
  > 리터럴 비교 시, str1.equals(str2) 사용

* String 역시 null 대입이 가능하며, 참조 중인 변수에 null을 대입하면 해당 객체는 GC에 의해 제거

<br>

## 5.6 배열
### 5.6.1 배열의 정의
* 같은 타입의 데이터를 연속된 공간에 index를 부여해 나열한 자료 구조
* 한 번 생성된 배열은 할당된 공간(길이)를 변경할 수 없다.
### 5.6.2 배열 선언
  ```
  int[] intArray;
  String[] strArray;
  ```
  > 타입[ ] 변수;

### 5.6.3 값 목록으로 배열 생성
```
String[] naems = {"한승범", "조니뎁", "민경훈"};
```
> 타입[ ] 변수 = {값0, 값1, 값2, 값3...};

* **주의 사항**
  * 배열 변수 선언 후 중괄호를 이용한 생성은 허용되지 않는다.
    ```
    타입[] 변수;
    변수 = {값0, 값1, 값2, 값3...};   // 컴파일 에러
    ```
  * 단, 배열 선언 후 new 연산자를 통해 값 목록 생성 가능
    ```
    String[] naems = null;
    names = new String[]{"한승범", "조니뎁", "민경훈"};
    ```
  * 메서드의 파라미터가 배열 타입일 경우에도 **배열이 선언된 것으로 간주해** new 연산자를 사용해야 함
    ```
    int add(int[] scores){ // };
    int result = add(new int[]{ 1,2,3,4 } );
    ```

### 5.6.4 new 연산자로 배열 생성
* 값의 목록을 가지고 있지 않은 상태에서 미리 배열 생성 시
  ```
  int[] intArray = new int[5];
  ```
  > element 5개 저장 가능한 int타입 배열. 데이터 타입 별 기본값으로 자동 초기화 된다(0).

### 5.6.5 배열의 길이
* 배열 변수.length; 로 산출 가능
* 단, length는 읽기 전용이므로 값을 변경할 수 없음
  ```
  intArray.length = 10 //(X, 사용 불가)
  ```
### 5.6.6 커맨드라인 입력

### 5.6.7 다차원 배열
* 가로, 세로 인덱스를 사용해 중첩 배열 방식으로 구현
* 2행 x 3열의 2차원 행렬 생성
  ```
  int[][] scores = new int[2][3];
  ```
  구분|열0|열1|열2
  ---|---|---|---
  행0|(0,0)|(0,1)|(0,2)
  행1|(1,0)|(1,1)|(1,2)

  * 배열 scores는 **길이가 2 인 배열A**(임의)를 참조하며
  * 배열 A의 scores[0]는 **길이가 3인 배열** 을 다시 참조하는 구조.
    > 즉, scores.length 값은 2 이며
    > scores[0].length의 값은 3이다.

* 항목 나열을 통한 생성
  ```
  int[][] scores = { {95,80}, {100,77} };
  ```

### 5.6.8 객체를 참조하는 배열
* primitive 타입 배열은, 각 항목이 직접 값을 갖고 있지만 참조 타입(클래스, 인터페이스, String) 배열은 각항목에 메모리 주소를 갖는다.
  * String[] 배열은 각 항목에 문자열이 아닌 또다른 String 객체의 주소를 갖는다.<br>
    String 배열 요소의 연산자 비교 사용 시 == / equals의 관계도 리터럴과 객체 관계에 주의

### 5.6.9 배열 복사
* 배열은 크기 변경이 불가하므로 큰 배열 생성 후 항목 값을 복사해 사용한다.
* System.arraycopy() 메서드 사용
  ```
  System.arraycopy(arr1, 0, arr2, 0, arr1.length);
                //원본, 원본 시작 인덱스, 대상 배열, 대상 배열 시작 인덱스, 복사 개수
  ```
  > 참조 타입의 배열(String)일 경우, 복사 되는 것은 객체의 **메모리 주소** 이며 동일 객체를 참조
  > 이를 **shallow copy** 로 칭한다.

### 5.6.10 향상된 for문

<br>

## 5.7 열거 타입(enum)
* 열거 타입 : 한정된 값만을 갖는 데이터 타입
* 열거 타입 변수 : 몇 개의 열거 상수 중에서 하나의 상수를 저장하는 데이터 타입 변수
> 열거 타입 안에 선언된 각각의 **'열거 상수'는 메소드 영역** 에 생성되며, 이 각각의 열거 상수는 **heap영역에 생성된 '열거 상수 문자열' 객체** 를 참고하는 구조이다.

### 5.7.1 열거 타입 선언
```
public enum Week {
  MONDAY,
  TUESDAY,
  WEDNESDAY,
  THURSDAY,
  FRIDAY,
  SATURDAY,
  SUNDAY
}
```

### 5.7.2 열거 타입 변수
```
Week today = Week.SUNDAY;
```
* **열거 타입 변수** today 는 Stack 영역에 생성
* today에 저장되는 값은 Week.SUNDAY **열거 상수** 가 참조하는 **(문자열)객체의 메모리 주소**

```
즉, today에는 열거 상수 SUNDAY가 참조하는 (문자열)객체의 메모리 주소가 복사되어 대입된다.
```
> today == Week.SUNDAY 는 true가 산출된다.

```
Week week1 = Week.SUNDAY;
Week week2 = Week.SUNDAY;
```
> week1 과 week2에는 같은 문자열 객체의 메모리 주소가 대입되므로 week1 == week2 는 true

### 5.7.3 열거 객체 메서드
* name()
  * 열거 객체가 가진 문자열을 리턴
    ```
    Week today = Week.SUNDAY;
    String str = today.name();    // "SUNDAY"
    ```
* ordinal()
  * 열거 객체의 순번
    ```
    int ordinal = today.ordinal   // 6
    ```
* valueOf(String str)
  * 인수로 주어진 문자열과 동일한 문자열을 가지는 객체 리턴
    ```
    Week weekDay = Week.valueOf("SATURDAY");
    ```
* values()
  * 열거 타입의 모든 열거 객체를 배열로 리턴
    ```
    Week[] days = Week.values();
    days[0] == MONDAY....
    ```
* compareTo()
  * 열거 객체의 순번을 비교해 int값 리턴
    ```
    Week day1 = Week.MONDAY;     // 0번째
    Week day2 = Week.WEDNESDAY;  // 2번째
    int result1 = day1.compareTo(day2);   // -2
    int result2 = day2.compareTo(day1);   // 2
    ```

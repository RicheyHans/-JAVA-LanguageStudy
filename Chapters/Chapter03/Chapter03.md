## Chapter 03. Operators (연산자)

## 3.1 연산자와 연산식
* 연산식은 반드시 **한 개** 의 값을 산출한다.
<br>

## 3.2 연산 방향과 우선순위
* 동일 우선순위 연산자 우선순위
  * 대부분의 이항 연산자는 왼쪽에서 오른쪽으로
    ```
    100 * 2 / 3 % 5
    100*2, 200/3, 66%5 -> 1 산출
    ```
  * 단항, 부호, 대입 연산자의 경우 오른쪽에서 왼쪽으로
    ```
    a = b = c = 5
    c=5, b=c, a=c 순서로 연산
    ```
<br>

## 3.3 단항 연산자

### 3.3.1 부호 연산자(+,-)
부호 연산자는 정수/실수 리터럴에 쓰는 경우와 정수/실수 변수에 사용할 수 있다.
* 정수/실수 리터럴에 사용
  * 양수, 음수를 표현
    ```
    int i = +100;
    double d = -10.5;
    ```
* 정수/실수 변수에 사용(주의)
  * **+는 현재 부호를 유지, -는 부호를 변경한다(양수>음수, 음수>양수)**
  * 부호 연산자 사용 시, 결과 값은 int 타입으로 산출된다.
    * e.g. short s = 100; 일 경우, int result = -s; 로 사용

### 3.3.2 증감 연산자(++, --)
* ++a, --a 는 다른 연산을 수행하기 전에 값을 1 증가/감소 시킨다.
* a++, a--는 다른 연산을 수행한 후 값을 1 증가/감소 시킨다.

>단항 사용시에는 큰 영향이 없으나, 다른 연산과 함께 사용할 경우 결과 값이 달라지므로 주의

### 3.3.3 논리 부정 연산자(!)
* boolean 타입에만 사용 가능하다.
  * 피연산자가 true면 false, false면 true를 산출

### 3.3.4 비트 반전 연산자(~)
* 정수 타입 byte, short, int, long에만 사용
  * 비트 값을 0은 1, 1은 0으로 변환하며 MSB까지 반전되므로 부호가 반대인 값이 산출

* 피연산자는 연산 수행 전 int 변환 후 반전되므로 산출 데이터의 형태는 int여야 한다.
  ```
  byte v1 = 10;
  int v1Result = ~v1;   // byte로 선언 시 컴파일 에러
  ```
* 반대 부호의 정수 산출
  * 기본적인 방식은 변수에 '-'를 붙이는 것
  * 10을 비트 반전하면 -11 이 산출되므로, 여기에 정수 1을 더해준다.
    ```
    byte v1 = 10;
    int v1Result = ~v1 + 1;   // -10 저장
    ```
* Integer.toBinaryString() 활용
  * 정수값을 총 32비트 이진 문자열로 전환
  * 단, 앞의 비트가 0일 경우 생략되므로 아래와 같은 처리를 할 수 있다.
    ```
    public static String toBinaryString(int value){
      String str = Integer.toBinaryString(value);
      while(str.length() < 32){
        str = "0" + str;
      }
      return str;
    }
    ```

<br>

## 3.4 이항 연산자

### 3.4.1 산술 연산자(+ , - , * , %)
* long을 제외한 정수 타입 연산은 int로 산출된다.
* long을 포함한 정수 타입 연산은 long으로 산출된다.
* 실수를 포함한 연산은 실수로 산출된다.
* 주의사항
  * 정수끼리의 연산이 시행 해 실수 변수에 저장할 경우
    ```
    int int1 = 10, int2 = 4;
    double result = int1 / int2;
    ```
    > 10 /4 는 2.5이지만, int간의 연산이므로 2가 산출되고 이 값이 double에 저장되면서
    2.0이 할당된다. 2.5를 산출하기 위해서는 int1, int2 중 하나가 double로 캐스팅 되어야 한다.

  * 리터럴 연산과 변수 연산의 차이
    ```
    char c1 = 'A' + 1;
    char c2 = 'B';
    char c3 = c2 + 1;   // 컴파일 에러
    ```
    > c1의 경우 **리터럴 간의 계산**이므로 66이 연산되어 저장되므로 c1은 'B'가 대입된다.
    그러나 c3의 경우 char 변수 c2와 1의 연산이므로 **결과 값은 int로** 산출되어야 한다.
    이 경우에는 (char) (c2+1)로 캐스팅 해줘야 에러가 나지 않는다.

* NAN / Infinity 연산
  * / 또는 % 연산 시 좌측 피연산자가 정수일 경우, 우측 피연산자에 0을 대입하면 ArithmeticException 발생
  * / 또는 % 연산 시 좌측 피연산자가 정수일 경우, 우측 피연산자에 (실수)0.0 대입 시
    * 5 / 0.0 -> Infinity
    * 5 % 0.0 -> NaN
    > Double.isInfinite(a), Double.isNaN(a) 메소드 사용시 해당 값일 경우 true 산출 가능

    > NaN 검사 할 경우 반드시 isNaN으로 검사해야 하며, == 를 사용해서는 안된다.

### 3.4.2 문자열 연결 연산자(+)
* 피연산자 중 한쪽이 문자열일 경우, + 연산자는 문자열 연결 연산자로 사용된다.
  * 다른 피연산자를 문자열로 변환하고 서로 결합(우선순위 주의)
    ```
    String str1 = "JDK"+3+3.0;  // JDK3이 먼저 연산되며, JDK33.0 산출
    String str2 = 3+3.0+"JDK"   // 6.0JDK 산출
    ```
    > 동일 우선순위일 경우 왼쪽 먼저 실행된다.

### 3.4.3 비교 연산자(<, <=, >, >=, ==, !=)
* char 타입일 경우 유니코드 값으로 비교
  * ('A' < 'B') -> (65 < 66)

* 비교 연산자 역시 타입 변환을 통해 일치 시킨 후 연산한다.
  * 'A' == 65 -> true 산출 (A를 int로 형변환)
  * 3 == 3.0 -> true 산출 (3을 double로 형변환)
    * 단, 0.1과 0.1f는 예외 (0.1f는 정확하게 0.1이 될 수 없음)

* == 연산자는 **변수에 저장된** 값만을 비교한다.
  * String 변수의 경우 참조 객체의 메모리 값을 저장하기 때문에, String 변수 활용 시 예외적인 결과가 나올 수 있다.

    ```
    String str1 = "한승범";
    String str2 = "한승범";
    String str3 = new String("한승범");
    ```
    > str1과 str2는 문자열 리터럴이 동일해 하나의 객체를 사용하지만, str3은 별도의 객체이다.
    str1 == str2는 같은 객체 메모리 값을 보유하므로 true이지만, str2 == str3는 **다른 객체 메모리 값을 비교하므로 false가 출력된다.**

    문자열 리터럴 비교는 equals를 사용한다.
    ```
    boolean result = str1.equals(str2);
    ```

### 3.4.4 논리 연산자(pending)
### 3.4.5 비트 연산자(pending)

<br>

## 3.5 삼항 연산자
```
조건식 ? 값 또는 연산식 : 값 또는 연산식
```
> 조건식이 true일 경우 좌측, false일 경우 우측 값이 산출된다.

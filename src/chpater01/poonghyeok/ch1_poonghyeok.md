<div style="background : skyblue;">스터디를 진행하면서 중요한 부분을 정리해 두었습니다.</div>

> ### Chapter 1. 자바 언어 기초

1. ** 코드 주석 **
   ```java
   /**
   @author 
   */
   ```
위와 같은 주석은 **document 주석** 이다. API 도큐먼트를 작성 시 사용하고 작성자 등을 표시한다.
(평소 `//` 라인주석, 혹은 `/* */` 코드블럭만 사용했기 때문에 Class 파일을 확인할 때 아니면 도큐먼트 주석을 본 적이 없었다.)
   
---

> ### Chapte2. 변수와 타입

1. ** 타입별 크기 ( byte ) **
     - `byte`
          - 1byte ( 8bit )
          - $$
            \begin{aligned}
            -2^7<= range <= 2^7 -1\\
            \end{aligned}$$
     - `short`
          - 2byte ( 16bit )
          - $$
            \begin{aligned}
            -2^15<= range <= 2^15 -1\\
            \end{aligned}$$
     - `char`
          - 2byte ( 16bit )
          - $$
            \begin{aligned}
            0<= range <= 2^7 -1\\
            \end{aligned}$$
     -  `int`
          - 4byte ( 32bit )
          - $$
            \begin{aligned}
            -2^31<= range <= 2^31 -1\\
            \end{aligned}$$
     - `long`
          - 8byte ( 64bit )
          - $$
            \begin{aligned}
            -2^63<= range <= 2^63 -1\\
            \end{aligned}$$

   여기서 `byte`, `short`, `int`, `long` 은  부호가 있는 ( `signed` ) 정수형이므로 최상위 bit는 부호bit이고 나머지 bit가 값의 범위를 결정한다.
   부호 bit에서 **0이 양수**, **1이 음수**를 의미한다.

     - **음수**의 bit
          - 부호 bit를 제외하고 전부 값을 뒤집고 1을 더해준 뒤 10진수로 바꾸면 그 값이 부호를 제외한 10진수가 된다.
          - `-2` 의 bit 표현은 아래와 같다.
            `1`111 / 1110 ???
            부호 bit를 제외하고 전부 값을 뒤집으면
            `1`000
       > 여기 chapter3 비트 부분에서 보충할 것

2. ** 리터럴 표기법 ( n 진수 임을 명시하면서 작성 ) **
     - 2진수 : `0b` 또는 `0B`로 시작 0과 1로 작성
     - 8진수 : `0`으로 시작하고 0~7 숫자로 작성
     - 10진수 : 소수점이 없는 0 ~ 9 숫자로 작성
     - 16진수 : `0x` 나 `0X`로 시작, 0 ~ 9 와 10 ~ 15 에 해당하는 A,B,C,D,E,F 로 작성

3. **Long type**
     - 뒤에 l 이나 L 을 붙여 Long type임을 명시한다.
       `long num = 100000L` 과 같이 사용할 수 있다.

4. **Char Type**
     - ** 유니코드 **
          - 유니코드란?
            세계 각국의 문자를 0 ~ 65535 숫자로 매핑한 국제 표준
            'A'는 65로, '가'는 4403으로 대입
            <span style="background : orange;">유니코드가 정수로 char type도 정수에 속한다.</span>
     - Char type 초기화
          - js에서는 `''`로 초기화 하는데, JAVA에서는 공백 `' '`으로 초기화 한다.
          - 참고로, 공백은 유니코드 32에 해당한다.
5. ** 실수타입 **
     - float
          - 4byte
            $$
            \pm 1.4 * 10^{45}<= range <= \pm 3.4 * 10 ^ {38}\\
            $$

     - double
          - 8byte
            $$
            \pm 4.9 * 10^{-324}<= range <= \pm 108 * 10 ^ {308}\\
            $$

   double type이 float type 보다 큰 실수를 저장할 수 있고 정밀도 또한 더 높다.
     - java는 - 표준에 근거해서 doubletype의 값을 ** 부동 소수점 ** 방식으로 메모리에 저장한다.
       <br>
     - 부호, 가수, 지수 (exponent)
       $$
       \pm m * 10^n\\
       $$
       과 같은 형태
          - float은 부호(1bit) + 지수(8bit) + 가수(23bit) => 4byte
          - double은 부호(1bit) + 지수(11bit) + 가수(52bit) => 8byte
            <span style="background : orange;">부호는 1이 음수, 0이 양수</span>
          - 가수 부분의 bit수 차이가 정밀도 차이다.
               - double의 어원이 float보다 두배 더 높은 정밀도를 보인다고 해서 double이다. 유효숫자를 두배 이상 길게 가질 수 있다.
                 <br>
     - 실수 리터럴 선언
          - 컴파일러는 기본적으로 실수를 ** double type ** 으로 받아들인다.
          - 10진수 혹은 e나E를 사용해서 리터럴 선언 가능
            `double x = 5e2 (= 5 * 10 ^ 2 )`
          - float은 뒤에 f나 F를 명시하면 된다.
            <br>
- 문자열 type ( **String** )
     - `""` 로 감싼 문자는 유니코드로 변환이 안된다.
       따라서 char type은 무조건 `''`로 감싸야 한다.
       <br>
- 자동 타입 변환
     - 값의 허용범위가 작은 타입이 허용 범이가 큰 타입으로 대입될 때 자동으로 type이 변환된다.
     - 캐스팅(casting)은 자동이 아닌 ** 강제 ** 형변환이다.
     - byte < shor, char < int < long < float < double
          - 더 큰 허용범위를 가진 type으로 형변환이 되면 채워지지 않는 bit들은 전부 0으로 채워지게 된다.
          - char가 int에 들어갈 수 있는 이유도 int가 허용범위가 더 크기 때문이다.
            <span style="background : orange;">예외</span> byte는 char로 대입될 수 없다. char는 0 ~ 65...의 부호가 없는 정수이기 때문에 byte의 허용범위가 더작다고는 하지만 음수 부분을 char가 받아 줄 수 없다.
            <br>
- 강제 타입 변환 (casting)
     - 자동 타입 변환은 명시하지 않아도 알아서 처리 되지만, 강제 타입변환은 변환될 형을 명시하는 것이다.
     - 왜 강제로 형변환을 하는지 생각해보면 자동으로 형변환 처리를 해주지 않기 때문에 강제로 하는 것이다.
          - 더 작은 범위의 type은 큰 범위의 type으로 <span style="background : orange;">자동 형변환</span>이 된다.
          - 따라서 큰 범위를 작은 범위로 내려서 쓰기 위해 <span style="background : orange;">강제 형변환, casting</span>을 사용한다.
          - 단, 작은 범위로 형변환을 시키는 것이기 때문에 작은 범위가 커버할 수 있는 크기를 가진 큰 범위의 수를 casting 해야한다.
            그렇지 않으면, 작은 범위에 bit로 들어오지 못하면 나머지는 0도 1도 아니고 다 없어져 버리기 때문이다.
            (내 기준) 실무에선<span style="background : orange;">Object 객체에서 String 혹은 int형 castring</span>  이 사용되곤 한다.
            <br>
- 연산식에서의 자동 타입변환
  `byte result = 10 + 20` 의 경우, <span style="background : orange;">컴파일 단계</span> 에서 10 + 20을 미리 계산해서 result 에 대입하게 된다. 즉 미리 계산을 거치기 때문에 연산이 필요 없다. <br>단, 피연산자로 사용되는 경우엔 연산이 수행되고 `char` 혹은 `byte` 의 경우에는 모두 `int` 로 <span style="background : orange;">자동 형변환</span> 이 되어 연산을 수행한다.
   ```java
   byte x = 10, byte y = 20, byte c = x+y 
   ```
     - 위 식의 경우에, 이전 식과 똑같은 계산을 하지만 ` x + y` 와 같이 피연산자이기 때문에 `int` 형으로 변환되어 연산이 되고, 결과값 또한 `int` 이기 때문에 casting을 하지 않고 `byte c` 에 대입할 수 없다.
       <br>
- 실수 연산
     - `float` 과 `double` 을 연산하게 된다면 `float`은 `double` 로 변환되어 연산
     - 결과값을 `float` 으로 만들고 싶다면 `100f` 와 같이 `float` 임을 명시해서 연산한다.
       <span style="background : orange;"> int형 나눗셈 </span>
          - `int / int` 의 결과는 `int` 인데, 모르는 상태에서 `3.xx` 와 같은 실수형 결과가 나올 것이라고 착각하기 쉽다.
          - javascript는 실수 결과가 나오지만 java는 `몫 값` 만을 출력한다.
            <br>
- 문자열 연산
     - 기본타입과 문자열을 더하게 되면 문자열을 만들어준다.
       그래서 기본 타입을 문자열로 만들기 위해 `1 + " "` 와 같이 사용하기도 하는데 `String.valueOf(1)` 과 같이 사용하는 것이 권장된다.
       <br>
---
> ### Chapter 03. 연산자

- overflow 와 underflow
     - 허용 최대 최소 범위를 벗어나면 최소 또는 최대값으로 돌아간다.
       <br>
- 실수의 부동 소수점
     - `1 - 7*0.1` 과 같은 연산을 했을 떄, `0.3` 이 return 되지 않고 `0.2999993` 과 같은 값이 return 된다.
     - java에서 실수는 부동소수점을 이용하기 때문이다.
       `부동소수점` 이란?
       부동소수점(floating point) 또는 떠돌이 소수점 방식은 실수를 `컴퓨터상에서 근사하여 표현`할 때 소수점의 위치를 고정하지 않고 그 위치를 나타내는 수를 따로 적는 것으로, `유효숫자`를 나타내는 `가수`와 `소수점의 위치`를 풀이하는 `지수`로 나누어 표현
       <br>
- NaN , Infinity   처리
     - `정수형`으로 계산할 때는 0으로 나누거나 나머지를 구하는 연산에서 예외가 발생
     - `실수형`으로 계산할 때는 0으로 나눴을 경우 `Infinity` 혹은 나머지를 구할 경우`NaN` 이 return 된다.

- 비교연산자 예외
     - `3 == 3.0` 은 3을 double 형으로 자동 형변환 시켜서 `true` 처리가 되지만
       `0.1f == 0.1` 은 `false`처리가 된다. 부동소수점 방식은 소수점을 정확하게 표현할 수 없기 때문이다.

---
> ### 생략


- 논리 연산자, 비트논리 연산자, 비트 이동연산자, 조건문 반목문

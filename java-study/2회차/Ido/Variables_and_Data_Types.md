## 변수와 타입

### 변수란?
프로그램은 작업을 처리하는 과정에서 필요에 따라 데이터를 메모리에 저장하게 되는데, 이때 변수를 사용하게 됩니다. 즉 `변수는 값을 저장할 수 있는 메모리의 공간`을 의미합니다. 변수라는 이름을 갖게 된 이유는 프로그램에 의해서 수시로 값이 변동될 수 있기 때문입니다.
변수에는 다양한 타입의 값을 동시에 저장할 수 없고, 복수 개의 값을 저장할 수 없습니다.
> 변수란, 하나의 값을 저장할 수 있는 메모리 공간

### 변수의 선언과 초기화
#### 변수 선언
변수를 사용하기 위해서는 먼저 변수를 선언해야 합니다.
변수 선언은 어떤 타입의 데이터를 저장할 것인지 그리고 변수 이름이 무엇인지를 결정하는 것입니다.
같은 타입의 변수는 콤마를 이용해서 한번에 선언할 수도 있습니다.

```java
int age;
int x, y, z;
```

이렇게 선언한 변수 이름을 통해 프로그램이 해당 메모리 주소에 접근할 수 있게됩니다.
변수 이름은 자바의 명명 규칙(Naming Convention)을 따라서 작성해야 합니다.

|작성 규칙|예|
|---|---|
|첫 번째 글자는 문자이거나 '$', '_'이어야 하고 숫자로 시작할 수 없다. (필수)|가능: price, $price, _companyName<br>불가능: 1v, @speed, $#value|
|영어 대소문자가 구분된다. (필수)|firstname과 firstName은 다른 변수|
|예약어는 사용할 수 없다. (필수)|아래 표 참조|
|첫 문자는 영어 소문자로 시작하되, 다른 단어가 붙을 경우 첫 문자를 대문자로 한다. (관례)|maxSpeed, firstName, carBodyColor|
|문자 수(길이)의 제한은 없다.|thisIsNoCharacterLengthLimit|

#### 자바 예약어 (변수명으로 사용 불가)

|분류|예약어|
|---|---|
|기본 데이터 타입|boolean, byte, char, short, int, long, float, double|
|접근 지정자|private, protected, public|
|클래스와 관련된 것|class, abstract, interface, extends, implements, enum|
|객체와 관련된 것|new, instanceof, this, super, null|
|메서드와 관련된 것|void, return|
|제어문과 관련된 것|if, else, switch, case, default, for, do, while, break, continue|
|논리값|true, false|
|예외 처리와 관련된 것|try, catch, finally, throw, throws|
|기타|transient, volatile, package, import, synchronized, native, final, static, strictfp, assert|

#### 변수의 사용
변수를 사용한다는 것은 변수에 값을 저장하고 읽는 행위를 말합니다.
변수에 값을 저장할 때에는 대입 연산자(=)를 사용합니다. 일반 수학에서 '='은 같다는 의미지만,
대부분 프로그래밍 언어에서는 우측의 값을 좌측 변수에 저장한다는 의미를 갖습니다.
변수를 선언하고 처음 저장된 값을 초기값이라고 하고, 변수에 `초기값을 저장하는 행위`를 변수의 `초기화`라고 합니다.

```java
int score; // 변수 선언
scroe = 90; // 값 저장 (초기화)
...
int score = 90; // 변수의 선언과 초기화
```

#### 리터럴
변수의 초기값은 코드에서 직접 입력하는 경우가 많은데, 이렇게 소스 코드 내에서 직접 입력된 값을 리터털(literal)이라고 부릅니다. 리터럴은 값의 종류에 따라 정수 리터럴, 실수 리터럴, 문자 리터럴, 논리 리터럴로 구분됩니다.
> 리터럴은 상수(constant)와 같은 의미지만, 프로그램에서 상수는 '한 번 저장하면 변경할 수 없는 변수'로 정의하고 있기때문에 이와 구분하기 위해 '리터럴'이라는 용어를 사용합니다.

- 정수 리터럴
```java
소수점이 없는 정수 리터럴은 10진수
0, 75, -100

0으로 시작되는 리터럴은 8진수
02, -04

0x 또는 0x로 시작하고 0~9, a~f(A~F)로 구성된 리터럴은 16진수
0x5, 0xA, 0xB3, 0xAC08

정수 리터럴을 저장할 수 있는 타입은 byte, char, short, int, long 5개가 있음
```

- 실수 리터럴
```java
소수점이 있는 리터럴은 10진수 실수
0.25, -3.14

E(또는 e)가 있는 리터럴은 10진수 지수와 가수
5E7 // 5 * 10^7
0.12E-5 // 0.12 * 10^-5

실수 리터럴을 저장할 수 있는 타입은 float, double이 있음
```

- 문자 리터럴
```java
작은따옴표로 묶은 텍스트는 하나의 문자 리터럴
'A', '한', '\t', '\n'

빈 문자 처리
char c = ''; // 컴파일 에러
char c = ' '; // 공백(유니코드 32) 가능

문자 리터럴을 저장할 수 있는 타입은 char
```

- 문자열 리터럴
```java
큰따옴표로 묶은 텍스트는 문자열 리터럴
"문자열"
"한줄 내려 쓰기\n" // 이스케이프 문자 사용 가능

빈 문자 처리
String str = ""; // 가능

문자열 리터럴을 저장할 수 있는 타입은 String
```

- 논리 리터럴
```java
true와 false는 논리 리터럴
true, false

논리 리터럴을 저장할 수 있는 타입은 boolean
```

### 데이터 타입 (자료형)
#### 기본(원시: primitive) 타입
기본(원시) 타입이란 정수, 실수, 문자, 논리 리터럴을 직접 저장하는 타입을 말합니다.
정수 타입에는 byte, char, short, int, long이 있고, 실수 타입에는 float, double이 있습니다. 그리고 논리 타입에는 boolean이 있습니다.

메모리에는 0과 1을 저장하는 최소 기억 단위인 bit가 있습니다.
그리고 8개의 비트를 묶어 바이트(byte)라고 합니다.
기본 타입은 정해진 메모리 사용 크기(바이트 크기)로 값을 저장합니다.
정수 타입일 경우 -2^n-1 ~ (2^n-1)-1의 값을 저장할 수 있는데, n은 메모리 사용 크기(bit 수)입니다.
예를 들어 int 타입의 경우에는 4byte(32bit)이므로 -2^31 ~ (2^31)-1의 범위를 갖습니다.

#### 정수 타입

|정수 타입|byte|char|short|int|long|
|:---:|:---:|:---:|:---:|:---:|:---:|
|byte|1|2|2|4|8|

자바는 기본적으로 정수 연산을 4 byte(int 타입)으로 수행합니다.
그렇기 때문에 특별한 이유가 없는 한 정수 리터럴은 int 타입 변수에 저장하는 것이 좋습니다.
byte, short 타입은 int 타입보다 메모리를 절약할 수는 있지만,
값의 범위가 작은 편이기 때문에 연산 시에 범위를 초과하여 잘못된 결과를 얻을 확률이 큽니다.

char 타입의 경우 문자를 저장할 수 있는 변수 타입이지만,
작은따옴표로 감싼 문자에 해당하는 유니코드값을 저장하는 원리이기 때문에 정수 타입으로 분류됩니다.
그렇기 때문에 특정 문자의 유니코드를 안다면 10진수 또는 16진수로 저장이 가능합니다.
char 변수에 저장된 유니코드를 알고 싶다면 char 타입 변수를 int 타입 변수에 저장하면 됩니다.
> 유니코드(Unicode)는 세계 각국의 문자들을 코드값으로 매핑한 국제 표준 규약입니다.
자바는 모든 문자를 유니코드로 처리합니다.
http://www.unicode.org 에서 유니코드에 대한 자세한 정보를 얻을 수 있습니다.

```java
char c = 65;
char c = '\u0041';
char c = 'A';
int unicode = c; // 65
```

short 타입은 C언어와의 호환을 위해 사용되며 비교적 잘 사용되지 않습니다.
long 타입은 은행 및 우주와 관련된 수치가 큰 데이터를 다루는 프로그램에서 사용됩니다.
int 타입의 저장 범위를 넘어서는 정수는 반드시 'l' 또는 'L'을 붙여서 8byte 정수 데이터임을
컴파일러에게 알려주어야 합니다. 그렇지 않으면 컴파일 에러가 발생합니다.
> 소문자 'l'은 숫자 1과 혼동하기 쉬우므로 일반적으로 대문자 'L'을 사용합니다.

#### 실수 타입

|실수 타입|float|double|
|:---:|:---:|:---:|
|byte|4|8|

실수는 정수와 달리 부동 소수점(floating-point) 방식으로 저장됩니다.
부동 소수점 방식은 실수를 다음과 같은 형태로 표현한 것을 말합니다.
```java
float: 부호(1bit) + 지수(8bit) + 가수(23bit) = 32bit = 4byte
double: 부호(1bit) + 지수(11bit) + 가수(52bit) = 64bit = 8byte
```

![floating-point](https://velog.velcdn.com/images/kid/post/1a786617-a3ae-445c-adb1-c1094c34802a/image.png)

자바에서는 실수 리터럴의 기본 타입을 double로 간주합니다.
즉 실수 리터럴을 float 타입 변수에 그냥 저장할 수 없다는 것입니다.
실수 리터럴을 float 타입 변수에 저장하려면 리터럴 뒤에 소문자 'f' 또는 대문자 'F'를 붙여야 합니다.
```java
double var1 = 3.14;
float var2 = 3.14; // 컴파일 에러
float var3 = 3.14f;

만약 정수 리터럴에 10의 지수를 나타내는 e 또는 E를 포함하고 있으면
정수 타입 변수에 저장할 수 없고 실수 타입 변수에 저장해야 합니다.
int var4 = 3000000;
double var5 = 3e6; // 3000000
float var6 = 3e6f; // 3000000
```

#### 논리 타입
boolean 타입은 1byte로 표현되는 논리값을 저장할 수 있는 데이터 타입입니다.
주로 조건문과 제어문의 실행 흐름을 변경하는데 사용됩니다.

### 타입 변환 (형변환)
#### 자동 타입 변환 Promotion
프로그램 실행 중에 자동적으로 일어나는 타입 변환을 말합니다.
자동 타입 변환은 작은 크기를 가지는 타입이 큰 크기를 가지는 타입에 저장될 때 발생합니다.
크기별로 타입을 나열하면 다음과 같습니다.

![promotion&casting](https://velog.velcdn.com/images/kid/post/0b05894b-86fd-4872-b2b8-51eb29f5b68d/image.png)

여기에서 주의해야 할 부분은 4byte인 float 타입이 8byte인 long 타입보다 크다고 표시된 것인데,
이는 부동 소수점 방식으로 인해 표현할 수 있는 값의 범위가 float 타입이 더 크기 때문입니다.

```java
byte bytaValue = 10;
int intValue = byteValue; // 자동 타입 변환이 일어남
double doubleValue = intValue; // 10.0

// char 타입의 경우 자동 변환되면 유니코드 값이 int 타입에 저장됨
char charValue = 'A';
int unicode = charValue; // 65
```
자동 타입 변환이 발생되면 변환 이전의 값은 변환 이후에도 손실 없이 보존됩니다.
작은 그릇의 물을 큰 그릇으로 옮기는 것과 같습니다.

자동 타입 변환에서 단 하나의 예외가 있습니다.
char 타입은 2byte의 크기를 가지지만, char의 범위는 0~65535이므로 음수가 저장될 수 없습니다.
따라서 음수가 저장될 수 있는 byte 타입을 char 타입으로 자동 변환시킬 수 없습니다.
```java
byte byteValue = 65;
char charValue = byteValue; // 컴파일 에러
```

#### 강제 타입 변환 Casting
큰 그릇의 물을 작은 그릇으로 모두 옮길 수 없듯이 큰 크기의 타입은 작은 크기의 타입으로
자동 타입 변환을 할 수 없습니다. 하지만 큰 그릇의 물을 작은 그릇 사이즈로 나누어서 그 중 하나의 그릇만 작은 그릇에 넣는다면 가능합니다. 예를 들어 int 타입을 4개의 byte로 쪼갠 다음, 끝에 있는 1byte만 byte 타입 변수에 저장하는 것입니다. 강제 타입 변환은 캐스팅 연산자 ()를 사용합니다.
```java
int intValue = 123456789;
byte byteValue = (byte) intValue; // 강제 타입 변환
```

4byte 중 끝에 있는 1byte만 byte 타입 변수에 담기므로 원래 값은 보존되지 않습니다.
하지만 int 값이 마지막 1byte로만 표현이 가능하다면 캐스팅 후에도 값이 유지될 수 있습니다.
실수 타입은 정수 타입으로 강제 타입 변환 시, 소수점 이하 부분은 버려지고 정수 부분만 저장됩니다.
```java
double doubleValue = 3.14;
int intValue = (int) doubleValue; // 3
```

강제 타입 변환에서 주의할 점은 사용자로부터 입력받은 값을 변환할 때 값의 손실이 발생하지 않도록 해야한다는 것과 정수 타입을 실수 타입으로 변환할 때 정밀도 손실을 피해야한다는 것입니다.
```java
public class FromIntToFloat {
	public static void main(String[] args) {
    	int num1 = 123456780;
        int num2 = 123456780;
        
        float num3 = num2;
        num2 = int num3;
        
        int result = num1 - num2;
        System.out.println(result);
    }
}    
```
위의 예제에서 result의 값은 0이어야 할 것 같지만 0이 아닙니다.
float는 위에서 확인했듯이 1비트(부호) + 8비트(지수) + 23비트(가수)로 이루어져 있습니다.
하지만 123456780은 23비트로 표현할 수 없기 때문에 근사치로 변환되는데 이것이 정밀도 손실입니다.
해결책은 모든 int값을 실수 타입으로 안전하게 변환시키는 double 타입을 사용하는 것입니다.

#### 연산식에서의 자동 타입 변환
서로 다른 타입의 피연산자가 있을 경우 두 피연산자 중 크기가 큰 타입으로 자동 변환된 후 연산됩니다.
int 타입과 double 타입을 덧셈 연산하면 int 타입이 double 타입으로 자동 변환되고 연산의 결과도 double 타입으로 나오게 됩니다.
```java
int intValue = 10;
double doubleValue = 5.5;
double result = intValue + doubleValue; // result에 15.5가 저장
```

int 타입으로 연산을 해야한다면 double 타입을 int 타입으로 캐스팅 후 연산을 수행합니다.
```java
int intValue = 10;
double doubleValue = 5.5;
int result = intValue + (int) doubleValue; // result에 15가 저장
```

### 문제
#### 1. 자동 타입 변환에 대한 내용입니다. 컴파일 에러가 발생하는 것은 무엇입니까? *3*
```java
byte byteValue = 10;
char charValue = 'A';
```
1. int intValue = byteValue;
2. int intValue = charValue;
3. short shortValue = charValue;
4. double doubleValue = byteValue;

#### 2. 변수를 잘못 초기화한 것은 무엇입니까? *3*
1. int var = 10;
2. long var = 10000000000L;
3. char var = ''; // 작은따옴표 두 개가 붙어있음
4. double var = 10;
5. float var = 10;

#### 3. 연산에서의 타입 변환 내용입니다. 컴파일 에러가 생기는 것은 무엇입니까? *1*
```java
byte byteValue = 10;
float floatValue = 2.5F;
double doubleValue = 2.5;
```
1. byte result = byteValue + byteValue;
2. int result = 5 + byteValue;
3. float result = 5 + floatValue;
4. double result = 5 + doubleValue;

### 레퍼런스
- 이것이 자바다: 신용권의 Java 프로그래밍 정복
- 문자 타입 'char' 와 문자열 'String' 의 진실: https://kang-james.tistory.com/entry/JAVA-%ED%8C%8C%ED%97%A4%EC%B9%98%EA%B8%B0-%EB%AC%B8%EC%9E%90-%ED%83%80%EC%9E%85-char-%EC%99%80-%EB%AC%B8%EC%9E%90%EC%97%B4-String-%EC%9D%98-%EC%A7%84%EC%8B%A4
- Will Floating Point 8 Solve AI/ML Overhead?: https://semiengineering.com/will-floating-point-8-solve-ai-ml-overhead/
- Automatic Type Promotion in Java Method Overloading: https://www.scientecheasy.com/2020/07/type-promotion-method-overloading-java.html/
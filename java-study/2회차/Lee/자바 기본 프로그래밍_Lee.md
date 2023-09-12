# 2장 : 자바 기본 프로그래밍

## 클래스
- 클래스 안에 변수, 상수, 함수(메소드)등 모든 프로그램 요소를 작성한다.
**(단, 클래스 바깥에는 어떤 것도 작성해서는 안된다.)**
```java
public class Hello {
    필드(변수), 메소드(함수) 코드
}
```

public은 자바의 접근지정자로서 다른 모든 클래스에서 클래스 Hello를 자유롭게 사용할 수 있다는 선언이다.


## 주석문
- 주석문은 프로그램의 실행에 영향을 미치지 않으며 프로그램에 대한 설명이나 특이사항을 자유롭게 기록하기 위해 사용한다.
```
// : 한 라인 주석처리
/* */ : /*와 */사이 주석처리
```


## main() 메소드
자바 프로그램은 main()메소드에서부터 실행을 시작하며, 프로그램이 여러 클래스로 이루어지는 경우, 실행을 시작할 클래스에만 main()을 두면 되기 때문에 모든 클래스가 main()을 가질 필요는 없다.
```java
public class Hello {
    public static void main(String[] args) {

    }
}
```
**main()은 반드시 public, static, void 타입으로 선언되어야 하며, 한 클래스 안에 2개 이상의 main()를 작성하면 안 된다.**

<잘못된 예시>
```java
public class Hello {
    public static void main(String[] args) {

    }

    ...

    public static void main(String[] args) {

    }
}
```


## 메소드
- 클래스의 멤버 함수를 자바에서는 메소드라고 한다. 메소드의 이름은 개발자가 정하며, 개수에는 제한이 없다.
```java
public static int sum(int n, int m) { // 매개변수는 n, m
    return n + m;
}
```

<메소드 sum()을 호출하는 코드>
```java
int i = 20;
s = sum(i, 10);
```


## 변수 선언
- 변수란 프로그램 실행 동안 데이터를 저장하는 공간이다.
- 지역변수란 메소드 내에서 선언되어 사용되는 변수이며, 지역변수는 메소드 내에서만 사용되며, 메소드의 실행이 끝나면 소멸된다.
```java
int i;
char a;
```


## 문장
- 자바에서 모든 문장은 ';'로 끝나야 하고, 
- 자바 컴파일러는 ';'를 문장의 끝으로 인식하므로 한 문장이 반드시 한 줄에 작성될 필요는 없다.

```java
s = sum(i,
        20);
```


## 화면 출력
- 프로그램에서 사용하는 데이터를 출력하기 위해 'System.out.println()' 이나 'System.out.print()'을 이용하면 된다.

####<예시-1>
```java
public class Main {
  public static void main(String[] args) {
    System.out.println("Department of Computer Engineering");
    System.out.println("Department of Computer Engineering");
    }
  }
```

####<결과값-1>
```
Department of Computer Engineering
Department of Computer Engineering
```

####<예시-2>
```java
public class Main {
  public static void main(String[] args) {
    System.out.print("Department of Computer Engineering");
    System.out.print("Department of Computer Engineering");
    }
  }
```

####<결과값-2>
```
Department of Computer EngineeringDepartment of Computer Engineering
```

**'System.out.println()'은 출력 후 다음 행으로 이동하지만, 'System.out.print()'은 다음 행으로 넘어가지 않는다.**


## 식별자
- 식별자란 클래스, 변수, 상수, 메소드 등에 붙이는 이름을 말한다.
1. 특수문자, 공백은 식별자로 사용할 수 없으나 '_'(언더바), '$'(달러)는 예외로 사용할 수 있다.
2. 첫 번째 문자로 숫자를 사용할 수 없다.
3. 길이 제한이 없다.
4. 대소문자를 구별한다.

- 클래스 이름의 첫 번째 문자는 대문자로 시작한다. Ex. class HelloWorld {}
- 변수와 메소드 이름의 첫 번째 문자는 소문자로 표기하며 이후 각 단어의 첫 번째 문자만 대문자로 표기한다. Ex. int myAge;
- 상수는 이름 전체를 대문자로 표기한다. Ex. final double PI = 3.141592;


## 자바의 데이터 타입
- 자바는 영어든 한글이든 문자 하나는 2바이트의 크기를 차지하므로 자바가 가지고 있는 강점 중 하나이다.

### 기본 타입
- boolean
- char
- byte
- short
- int
- long
- float
- double
=> 정수 타입(byte, short, int, long), 실수 타입(float, double)
=> 문자열은 자바의 기본 타입에 속하지 않기 때문에, String클래스를 이용한다.
Ex. String srtName = "junate";

**Java10부터 var 키워드를 사용하면 변수 선언이 간편하다.**
```java
var price = 200;        // price는 int 타입으로 결정
var name = "juntae";    // name은 String 타입으로 결정
```

### 레퍼런스 타입(타입은 한 가지이지만, 용도는 3가지이다.)
- 레퍼런스란 C/C++의 포인터와 비슷한 개념이다. 그러나 C/C++와 달리 실제 주소값을 가지지 않지만 우선은 배열에 대한 레퍼런스는 배열에 대한 주소 값 정도, 클래스에 대한 레퍼런스는 클래스에 대한 주소 값 정도로 생각한다.
1. 배열(array)에 대한 레퍼런스
2. 클래스(class)에 대한 레퍼런스
3. 인터페이스(interface)에 대한 레퍼런스


## 리터럴(literal)
- 리터럴이란 프로그램에 직접 표현한 값을 말한다.

1. 정수 리터럴
2. 실수 리터럴
3. 문자 리터럴
4. 특수문자 리터럴
5. 논리 리터럴
6. null 리터럴
7. 문자열 리터럴


## 상수
- 상수를 만드는 방법은 변수 선언 시 final 키워드를 사용하며, 상수는 변수와 달리 실행 중에 값을 바꿀 수 없다.

<예시>
```java
public class Main {
  public static void main(String[] args) {
    final double PI = 3.141592;
    PI = 5;
  }
}
```

java: cannot assign a value to final variable PI 오류가 뜬다.


## 타입 변환
- 자동 타입 변환
치환문이나 수식 내에서 타입이 일치하지 않을 때, 컴파일러는 오류 대신 작은 타입을 큰 타입으로 자동 변환한다.

- 강제 타입 변환
개발자가 강제로 타입 변환을 지시합니다.


## 키 입력
- 자바 응용프로그램은 System.in을 통해 사용자로부터 키를 입력받을 수 있다.
- 사용자가 원하는 타입으로 변환해주는 Scanner 클래스를 사용하는 것이 효과적이다.

### Scanner 객체 생성, 닫기
- Scanner 객체 생성
```java
Scanner scanner = new Scanner(System.in);
```

- Scanner를 사용하기 위해서는 프로그램의 맨 앞줄에 다음의 import문이 필요하다.
```java
import java.util.Scanner;

public class Main{
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int age = scanner.nextInt();
        System.out.println(age);
        String name = scanner.next();
        System.out.println(name);
        scanner.close();
    }
}
```

- Scanner 클래스는 사용자가 입력하는 키 값을 공백 문자(' ', '\t', '\n')를 기준으로 분리하여 토큰 단위로 읽는다.

```
String next()
byte nextByte()
short nextShort()
int nextInt()
long nextLong()
float nextFloat()
double nextDouble()
boolean nextBoolean()
String nextLine()
```

- String next()과 String nextLine()의 차이점
1. Seoul Korea처럼 공백이 들어간 문자열을 입력받기 위해서는 nextLine()을 사용하면 된다.
2. nextLine()은 다른 입력 없이 Enter키만 입력하면 넘어가지만, next()는 다른 입력 없이 Enter키를 입력하면 다른 키가 입력될 때까지 기다린다.

- Scanner 객체 닫기
```java
scanner.close();
```
scanner객체가 닫히면, System.in도 함께 닫히므로 더 이상 System.in을 사용하여 키 입력을 받을 수 없다. => Scanner 객체를 여러 개 생성해도 모두 하나뿐인 System.in을 공유하므로 응용프로그램 전체에 Scanner 객체를 하나만 생성하고 공유하는 것이 바람직하다.
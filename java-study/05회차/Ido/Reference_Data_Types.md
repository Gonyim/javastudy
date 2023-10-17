# 참조 타입

<br>

## 데이터 타입 분류
자바의 데이터 타입은 크게 기본(원시) 타입과 참조 타입으로 분류됩니다.
기본 타입이란 정수, 실수, 문자, 논리 리터럴을 저장하는 타입을 말하고,
참조 타입은 객체(Object)의 주소를 참조하는 타입으로 배열, 열거, 클래스, 인터페이스 타입을 말합니다.

![datatypes-in-java](https://velog.velcdn.com/images/kid/post/665d4a18-acb0-4da4-a46c-bd1682d10544/image.png)

기본 타입으로 선언된 변수와 참조 타입으로 선언된 변수의 차이점은 저장되는 값에 있습니다.
기본 타입은 실제 값을 변수 안에 저장하지만, 참조 타입은 메모리의 번지를 값으로 갖습니다.
이 번지를 통해 객체를 참조한다는 뜻에서 참조 타입이라고 부르게 된 것입니다.

<br>

## 메모리 사용 영역
java.exe로 JVM이 시작되면 JVM은 운영체제에서 할당받은 메모리 영역(Runtime Data Area)을 다음과 같이 세부 영역으로 구분해서 사용합니다.

![jvm-architecture](https://velog.velcdn.com/images/kid/post/b720c329-5414-4b67-a908-9183a75a2220/image.png)


![runtime-data-area-in-java](https://velog.velcdn.com/images/kid/post/c9eac9a9-d911-4255-95a9-32d44d9abc22/image.png)

### 메소드 영역
메소드 영역에는 코드에서 사용되는 클래스(\*.class)들을 클래스 로더로 읽어 클래스별로 런타임 상수풀, 필드 데이터, 메소드 데이터, 메소드 코드, 생성자 코드 등을 분류해서 저장합니다.

- JVM을 시작할 때 생성
- 로딩된 클래스 바이트 코드 내용을 분석 후 저장
- 모든 스레드가 공유

### 힙 영역
힙 영역은 객체와 배열이 생성되는 영역입니다. 힙 영역에 생성된 객체와 배열을 JVM 스택 영역의 변수나 다른 객체의 필드에서 참조합니다. 참조하는 변수나 필드가 없다면 의미 없는 객체가 되기 때문에 JVM은 GC를 실행시켜 이 객체를 힙 영역에서 자동으로 제거합니다. 그래서 자바는 코드로 객체를 직접 제거시키는 방법을 제공하지 않습니다.

- JVM을 시작할 때 생성
- 객체/배열 저장
- 사용되지 않는 객체는 GC가 자동 제거

### JVM 스택 영역
JVM 스택 영역은 각 스레드마다 하나씩 존재하며 스레드가 시작될 때 할당됩니다. 자바 프로그램에서 추가적으로 스레드를 생성하지 않았다면 main 스레드만 존재하므로 JVM 스택도 하나입니다. JVM 스택은 메소드를 호출할 때마다 프레임을 추가하고 메소드가 종료되면 해당 프레임을 제거하는 동작을 수행합니다. printStackTrace() 메소드로 보여주는 Stack Trace의 각 라인은 하나의 프레임을 표현합니다. 

- 스레드별로 생성
- 메서드를 호출할 때마다 Frame을 스택에 추가 (push)
- 메서드가 종료되면 Frame을 제거 (pop)

<br>

## 참조 변수의 ==, != 연산
기본 타입 변수의 ==, != 연산은 변수의 값이 같은지, 아닌지를 조사하지만, 참조 타입 변수들의 ==, != 연산은 동일한 객체를 참조하는지, 다른 객체를 참조하는지 알아볼 때 사용됩니다.
참조 타입 변수의 값은 힙 영역의 객체 주소이므로 결국 주소 값을 비교하는 것으로 생각할 수 있습니다.

<br>

## null과 NullPointException
참조 타입 변수는 객체를 참조하지 않는다는 뜻으로 null값을 가질 수 있습니다.
null값도 초기값으로 사용할 수 있기 때문에 null로 초기화된 참조 변수는 스택 영역에 생성됩니다.

참조 변수를 사용하면서 가장 많이 발생하는 예외 중 하나로 NullPointerException이 있습니다. 이 예외는 참조 타입 변수가 null을 가지고 있을 경우, 참조할 객체가 없으므로 변수를 사용할 수 없기 때문에 발생하게 됩니다. 아래 코드에서 예외가 발생하는 상황을 확인할 수 있습니다.

#### 예제

```java
int[] intArray = null;
intArray[0] = 10; // NullPointerException

String str = null;
System.out.println("총 문자수: " + str.length()); // NullPointerException
``` 

<br>

## String 타입
String 변수에 저장한다는 표현은 문자열이 직접 변수에 저장되는 것이 아니라, 문자열은 힙 영역에 String 객체로 생성되고 변수가 그 객체의 주소를 참조하는 것을 의미합니다.
일반적으로 String 타입 변수를 초기화할 경우 문자열 리터럴을 사용하지만 new 연산자를 사용해서 직접 객체를 생성할 수도 있습니다. new 연산자는 힙 영역에 새로운 객체를 만들 때 사용하므로 객체 생성 연산자라고도 합니다. 문자열 리터럴로 생성하느냐 new 연산자로 생성하느냐에 따라 비교 연산자의 결과가 달라질 수 있습니다.

#### 예제

```java
class StringStorage {
    public static void main(String args[])
    {
        String s1 = "TAT";
        String s2 = "TAT";
        String s3 = new String("TAT");
        String s4 = new String("TAT");
 
        System.out.println(s1);
        System.out.println(s2);
        System.out.println(s3);
        System.out.println(s4);
    }
}
```

#### 참고

![string-in-java1](https://velog.velcdn.com/images/kid/post/78117016-2094-41ca-8d06-2059bda66311/image.png)

<br>

## 배열 타입
배열은 같은 타입의 데이터를 연속된 공간에 나열시키고, 각 데이터에 인덱스를 부여해 놓은 자료구조입니다. 인덱스는 각 항목의 데이터를 읽거나 저장하는데 사용되며 `변수[인덱스]` 이렇게 배열 이름 옆에 있는 대괄호 안에 작성합니다.

배열은 같은 타입의 데이터만 저장할 수 있습니다. 만약 다른 타입의 값을 저장하려고 하면 타입 불일치 컴파일 오류가 발생하게 됩니다. 또한 배열은 프로그램 실행 도중에 길이를 늘리거나 줄일 수 없습니다.

<br>

### 배열 선언
배열 변수 선언은 다음과 같이 두 가지 형태로 작성할 수 있습니다.

1. 타입\[] 변수;
	- `int[] intArray;`
    - `String[] strArray;`

2. 타입 변수\[];
	- `int intArray[];`
    - `String strArray[];`

<br>

### 값 목록으로 배열 생성
배열에 저장될 값이 여러개인 경우 중괄호를 사용해서 다음과 같이 객체를 만들 수 있습니다.

```java
String[] names = {"Java", "Python", "C", "JavaScript"};
```

하지만 위처럼 값의 목록으로 배열 객체를 생성할 때 주의할 점이 있습니다. 배열 변수를 이미 선언한 후에 다른 실행문에서 중괄호를 사용한 배열 생성은 허용되지 않는다는 것입니다.
그래서 배열 변수를 미리 선언한 후 값 목록들이 나중에 결정되는 상황이라면 다음과 같이 new 연산자를 사용해서 값 목록을 지정해주면 됩니다.

```java
String[] names = null;
names = {"Java", "Python", "C", "JavaScript"}; // 컴파일 에러
```

```java
String[] names = null;
names = new String[] {"Java", "Python", "C", "JavaScript"};
```

#### 예제
```java
public class Main {
    public static void main(String[] args) {
        int[] scores;
        scores = new int[] {95, 80, 90};
        
        int sum1 = 0;
        for (int i=0; i<3; i++) {
            sum1 += scores[i];
        }
        System.out.println("총합: " + sum1);

        int sum2 = add( new int[] {95, 80, 90} );
        System.out.println("총합: " + sum2);
    }

    public static int add(int[] scores) {
        int sum = 0;
        for (int i=0; i<3; i++) {
            sum += scores[i];
        }
        return sum;
    }
}
```

<br>

### new 연산자로 배열 생성
향후 값들을 저장할 배열을 미리 만들고 싶다면 new 연산자로 다음과 같이 배열 객체를 생성할 수 있습니다. `타입[] 변수 = new 타입[길이];` 여기에서 길이는 배열이 저장할 수 있는 값의 수를 말합니다. 다음은 길이가 5인 int 배열을 생성하는 코드입니다.

```java
int[] intArray = new int[5];
```

자바는 intArray\[0] ~ intArray\[4]까지 5개의 값을 저장할 수 있는 공간을 확보하고, 배열의 생성 번지를 리턴합니다. 리턴된 번지는 intArray 변수에 저장됩니다. new 연산자로 배열을 처음 생성할 경우, 배열은 기본값으로 초기화되므로 intArray\[0] ~ intArray\[4]까지 모두 0을 값으로 가지게 됩니다.

#### 타입별 배열의 초기값

|분류|데이터 타입|초기값|
|---|---|---|
|기본 타입 (정수)|byte|0|
||char|'\u0000'|
||short|0|
||int|0|
||long|0L|
|기본 타입 (실수)|float|0.0F|
||double|0.0|
|기본 타입 (논리)|boolean|false|
|참조 타입|class|null|
||interface|null|

<br>

### 배열 길이
코드에서 배열의 길이를 얻으려면 배열 객체의 length 필드를 읽으면 됩니다. 여기에서 필드는 객체 내부의 데이터를 의미합니다. 배열의 length 필드를 읽기 위해서는 다음과 같이 작성합니다.

```java
// 배열변수.length;
int[] intArray = {10, 20, 30};
int num = intArray.length;
```

배열의 length 필드는 for문을 사용해서 배열 전체를 루핑할 때 유용하게 사용할 수 있습니다.
만약 배열의 인덱스 범위를 초과해서 사용하면 ArrayIndexOutOfBoundsException이 발생하기 때문에 주의해야 합니다.

#### 예제

```java
public class Main {
    public static void main(String[] args) {
        int[] scores = {83, 90, 87};
        int sum = 0;
        for (int i=0; i<scores.length; i++) {
            sum += scores[i];
        }
        System.out.println("총합: " + sum);

        int avg = sum / scores.length;
        System.out.println("평균: " + avg);
    }
}
```

<br>

### 커맨드 라인 입력

```java
public static void main(String[] args) { ... }
```

명령 프롬프트에서 `java 클래스명` 으로 프로그램을 실행하면 JVM은 길이가 0인 String 배열을 먼저 생성하고 main() 메소드를 호출할 때 매개값으로 생성된 args 배열을 전달합니다.
`java 클래스명 문자열0 문자열1 문자열2 ... 문자열n-1` 으로 클래스명 뒤에 공백으로 구분된 문자열 목록을 주고 실행하면, 문자열 목록으로 구성된 배열을 매개값으로 전달합니다.
main() 메소드는 `String[] args` 매개 변수를 통해서 커맨드 라인에서 입력된 데이터의 수(배열의 길이)와 입력된 데이터(배열의 항목 값)을 알 수 있게 됩니다.

#### 예제

```java
public class Main {
    public static void main(String[] args) {
        if (args.length != 2) {
            System.out.println("프로그램의 사용법");
            System.out.println("java Main num1 num2");
            System.exit(0);
        }

        String strNum1 = args[0];
        String strNum2 = args[1];

        int num1 = Integer.parseInt(strNum1);
        int num2 = Integer.parseInt(strNum2);

        int result = num1 + num2;
        System.out.println(num1 + " + " + num2 + " = " + result);
    }
}
```

위 예제를 그냥 실행하면 매개값을 주지 않았으므로 길이가 0인 String 배열이 매개값으로 전달됩니다. 따라서 args.length는 0이므로 3라인의 if 조건식이 true가 되어 if문의 블록이 실행됩니다. 인텔리제이에서 프로그램을 실행할 때 매개값을 주고 실행하려면 메뉴에서 `[Run -> Edit Configurations...]`를 선택한 후 `Program arguments`안에 공백을 기준으로 매개값을 작성해주면 됩니다. `Alt + Shift + F10` 단축키를 사용할 수도 있습니다.

![program-arguments](https://velog.velcdn.com/images/kid/post/bf5d923e-a1a9-44aa-9093-130508aecbc6/image.png)

이렇게 매개값을 주고 실행하면 args는 `{"10", "20"}` 배열을 참조하게 됩니다. 문자열은 산술 연산을 할 수 없기 때문에 Integer.parseInt() 메소드를 이용해서 정수로 변환시켜줍니다. 만약 정수로 변환할 수 없는 문자열이 주어졌을 경우에는 NumberFormatException 예외가 발생합니다.
위의 이미지는 명령 프롬프트에서 다음과 같이 실행하는 것과 동일한 결과를 얻습니다.

```
java Main 10 20
```

<br>

### 다차원 배열

![multidimensional-arrays-in-java](https://velog.velcdn.com/images/kid/post/2e766ff1-618b-4197-930f-45b2b35ac72e/image.png)

자바는 2차원 배열을 중첩 배열 방식으로 구현합니다. 예를 들어 2(행) x 3(열) 행렬을 만들기 위해 다음과 같은 코드를 작성합니다.

```java
int[][] scores = new int[2][3];
```

이 코드는 메모리에 세 개의 배열 객체를 생성합니다. 각각 int 타입 배열 A, B, C 라고 가정하겠습니다. 배열 변수인 scores는 길이가 2인 배열 A를 참조합니다. 배열 A의 `scores[0]`은 다시 길이가 3인 배열 B를 참조합니다. 그리고 `scores[1]` 역시 길이가 3인 배열 C를 참조합니다. 즉 `scores[0]`과 `scores[1]`은 모두 배열을 참조하는 변수 역할을 하게 됩니다. 따라서 각 배열의 길이는 다음과 같이 얻을 수 있습니다.

```java
scores.length // 2 (배열 A의 길이)
scores[0].length // 3 (배열 B의 길이)
scores[1].length // 3 (배열 C의 길이)
```

다음과 같이 계단식 구조를 가지도록 만들 수도 있습니다.

```java
int[][] scores = new int[2][];
scores[0] = new int[2];
scores[1] = new int[3];
```

그룹화된 값의 목록을 가지고 있다면 다음과 같이 중괄호 안에 다시 중괄호를 사용할 수 있습니다.

```java
int[][] scores = {{95, 80}, {92, 96}};
int score = scores[0][0]; // 95
int score = scores[1][1]; // 96
```

<br>

### 배열 복사
배열은 한 번 생성하면 크기를 변경할 수 없기 때문에 더 많은 저장 공간이 필요하다면 더 큰 배열을 새로 만들고 이전 배열로부터 항목 값들을 복사해야 합니다. 복사는 얕은 복사, 깊은 복사로 나뉩니다.

- 얕은 복사: 참조하는 객체가 동일
- 깊은 복사: 참조하는 객체를 별도로 생성

#### 예제 - for

```java
public class Main {
    public static void main(String[] args) {
        int[] oldIntArray = {1, 2, 3};
        int[] newIntArray = new int[5];

        for (int i=0; i<oldIntArray.length; i++) {
            newIntArray[i] = oldIntArray[i];
        }

        for (int i=0; i<newIntArray.length; i++) {
            System.out.print(newIntArray[i] + ", ");
        }
    }
}
```

#### 예제 - System.arraycopy()

```java
public class Main {
    public static void main(String[] args) {
        String[] oldStrArray = {"java", "array", "copy"};
        String[] newStrArray = new String[5];

        System.arraycopy(oldStrArray, 0, newStrArray, 0, oldStrArray.length);

        for (int i=0; i<newStrArray.length; i++) {
            System.out.print(newStrArray[i] + ", ");
        }
    }
}
```

<br>

### 향상된 for문
자바 5부터 배열 및 컬렉션 객체를 좀 더 쉽게 처리할 목적으로 향상된 for문을 제공합니다. 향상된 for문은 반복 실행을 하기 위해 카운터 변수와 증감식을 사용하지 않습니다. 배열 및 컬렉션 항목의 개수만큼 반복하고, 자동적으로 for문을 빠져나갑니다.

#### 예제

```java
public class Main {
    public static void main(String[] args) {
        int[] scores = {83, 90, 87};
        int sum = 0;
        for (int score : scores) {
            sum += score;
        }
        System.out.println("총합: " + sum);

        int avg = sum / scores.length;
        System.out.println("평균: " + avg);
    }
}
```

<br>

## 열거 타입
데이터 중에는 몇 가지로 한정된 값만을 갖는 경우가 있습니다. 예를 들면 요일에 대한 데이터와 계절에 대한 데이터입니다. 이와 같이 한정된 값만을 갖는 데이터 타입이 열거 타입(enumeration type)입니다. 열거 타입은 몇 개의 열거 상수(enumeration constant) 중에서 하나의 상수를 저장하는 데이터 타입입니다.

<br>

### 열거 타입 선언
열거 타입을 선언하기 위해서는 먼저 열거 타입의 이름을 정하고 소스 파일(\*.java)을 생성해야 합니다.
열거 타입 이름은 다음과 같이 파스칼 표기법으로 작성하는 것이 관례입니다.

```java
Week.java
MemberGrade.java
ProductKind.java
```

소스 파일의 내용으로는 열거 타입을 선언하기 위한 키워드인 public enum을 사용하여 열거 타입 이름과 열거 상수를 선언합니다. 다음과 같이 열거 타입 이름은 소스 파일명과 대소문자가 모두 일치해야 하고, 열거 타입의 값으로 사용되는 열거 상수는 관례적으로 모두 대문자로 작성합니다.만약 여러 단어로 구성된 경우에는 단어 사이를 언더바 기호(\_)로 연결합니다.

```java
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

<br>

### 열거 타입 변수
열거 타입도 하나의 데이터 타입이므로 `열거타입 변수;`와 같이 변수를 선언하고 사용해야 합니다.
열거 타입 변수를 선언했다면 다음과 같이 열거 상수를 저장할 수 있습니다. 열거 상수는 단독으로 사용할 수 없고 반드시 `열거타입.열거상수`로 사용해야 합니다.

```java
Week today = Week.MONDAY;
```

열거 타입 또한 참조 타입이기 때문에 위 코드에서 today 변수에는 메소드 영역에 생성된 MONDAY 열거 상수가 참조하는 Week 객체의 번지가 저장됩니다. 즉, 얕은 복사가 발생합니다.

#### 예제 (Enum타입 Week.java 파일 생성해야함)

```java
import java.util.Calendar;

public class Main {
    public static void main(String[] args) {
        Week today = null; // 열거 타입 변수 선언

        Calendar cal = Calendar.getInstance();
        int week = cal.get(Calendar.DAY_OF_WEEK); // 일(1) ~ 토(7)까지의 숫자를 리턴

        switch (week) {
            case 1:
                today = Week.SUNDAY;
                break;
            case 2:
                today = Week.MONDAY;
                break;
            case 3:
                today = Week.TUESDAY;
                break;
            case 4:
                today = Week.WEDNESDAY;
                break;
            case 5:
                today = Week.THURSDAY;
                break;
            case 6:
                today = Week.FRIDAY;
                break;
            case 7:
                today = Week.SATURDAY;
                break;
        }

        System.out.println("오늘 요일: " + today);

        if (today == Week.MONDAY || today == Week.WEDNESDAY || today == Week.FRIDAY) {
            System.out.println("자바 스터디를 합니다.");
        } else {
            System.out.println("누워있습니다.");
        }
    }
}
```

<br>

### 열거 객체의 메소드
모든 열거 타입은 컴파일 시에 java.lang.Enum 클래스를 상속하게 되어있기 때문에 Enum 클래스에 선언된 메소드들을 사용할 수 있습니다.

|리턴 타입|메소드(매개 변수)|설명|
|---|---|---|
|String|name()|열거 객체의 문자열을 리턴|
|int|ordinal()|열거 객체의 순번(0부터 시작)을 리턴|
|int|compareTo()|열거 객체의 비교해서 순번 차이를 리턴|
|열거 타입|valueOf(String name)|주어진 문자열의 열거 객체를 리턴|
|열거 배열|values()|모든 열거 객체들을 배열로 리턴|

#### name()
name() 메소드는 열거 객체가 가지고 있는 문자열을 리턴합니다. 이때 리턴되는 문자열은 열거 타입을 정의할 때 사용한 상수 이름과 동일합니다. 아래 코드는 today가 참조하는 열거 객체에서 name() 메소드를 호출하여 문자열을 얻어내는 예제입니다. name() 메소드는 열거 객체 내부의 문자열인 "SUNDAY"를 리턴하고 name 변수에 저장합니다.

```java
Week today = Week.SUNDAY;
String name = today.name()
```

#### ordinal()
ordinal() 메소드는 전체 열거 객체 중 몇 번째 열거 객체인지 알려줍니다. 열거 객체의 순번은 타입을 정의할 때 주어진 순번을 말하고 0번부터 시작합니다. 다음 코드에서 ordinal() 메소드는 0을 리턴해서 ordinal 변수에 저장합니다.

```java
Week today = Week.MONDAY;
int ordinal = today.ordinal();
```

#### compareTo()
compareTo() 메소드는 매개값으로 주어진 열거 객체를 기준으로 해서 전후로 몇 번째에 위치하는지를 비교합니다. 만약 열거 객체가 매개값의 열거 객체보다 순번이 빠르다면 음수가, 느리다면 양수가 리턴됩니다. 다음 코드에서 day1.compareTo(day2)는 day2를 기준으로 day1의 상대적인 위치를 리턴합니다. day1(순번 0)이 day2(순번 2)보다 앞에 위치하고 순번 차이가 2이므로 result1에는 -2가 저장됩니다.

```java
Week day1 = Week.MONDAY;
Week day2 = Week.WEDNESDAY;
int result1 = day1.compareTo(day2); // -2
int result2 = day2.compareTo(day1); // 2
```

#### valueOf()
valueOf() 메소드는 매개값으로 주어지는 문자열과 동일한 문자열을 가지는 열거 객체를 리턴합니다. 이 메소드는 외부로부터 문자열을 입력받아 열거 객체로 변환할 때 유용하게 사용할 수 있습니다. 다음 코드에서 weekDay 변수는 Week.MONDAY 열거 객체를 참조하게 됩니다.

```java
Week weekDay = Week.valueOf("MONDAY");
```

#### values()
values() 메소드는 열거 타입의 모든 열거 객체들을 배열로 만들어 리턴합니다. 다음은 Week 열거 타입의 모든 열거 객체를 배열로 만들어 향상된 for문을 이용해서 반복하는 코드입니다. 배열의 인덱스는 열거 객체의 순번과 같고 각 인덱스 값은 해당 순번의 열거 객체 번지입니다.

```java
Week[] days = Week.values();
for (Week day : days) {
	System.out.println(day);
}
```

<br>

## 레퍼런스
- 이것이 자바다: 신용권의 Java 프로그래밍 정복
- JVM에 관하여 - Part 3, Run-Time Data Area: https://tecoble.techcourse.co.kr/post/2021-08-09-jvm-memory/
- Strings in Java: https://www.geeksforgeeks.org/strings-in-java/
- \[Java] 자바 배열을 복사하는 다양한 방법 (깊은복사, 얕은복사): https://coding-factory.tistory.com/548
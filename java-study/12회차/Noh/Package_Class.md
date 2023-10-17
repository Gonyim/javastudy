# java.lang패키지와 유용한 클래스

## java.lang패키지
* java.lang패키지는 자바프로그래밍에 가장 기본에 되는 클래스들을 포함하고 있다
    * 때문에 java.lang패키지의 클래스들은 import문 없이도 사용할 수 있게 되어있다
        * 그 동안 String클래스나 System클래스를 import문 없이 사용할 수 있었떤 이유가 바로 java.lang패키지에 속한 클래스들이기 때문이었던 것이다
### Object클래스
* Object클래스는 모든 클래스의 최고 조상이기 때문에 Object클래스의 멤버들을 모든 클래스에서 바로 사용 가능하다

| 메서드                  | 설명                                                                                   |
|-------------------------|----------------------------------------------------------------------------------------|
| `equals(Object obj)`    | 두 객체가 동등한지 여부를 비교하고, 동등하면 `true`를 반환합니다.                     |
| `hashCode()`            | 객체의 해시 코드를 반환합니다.                                                       |
| `toString()`            | 객체를 문자열로 표현한 값을 반환합니다.                                               |
| `getClass()`            | 객체의 클래스를 나타내는 `Class` 객체를 반환합니다.                                    |
| `clone()`               | 객체의 복사본을 생성하여 반환합니다.                                                 |
| `finalize()`            | 객체가 가비지 컬렉션될 때 호출되는 메서드입니다.                                      |
| `notify()`, `notifyAll()` | 스레드 간의 동기화를 위해 사용되는 메서드입니다. 멀티스레딩과 관련이 있습니다.     |
| `wait()`                | 스레드가 대기 상태로 전환되도록 합니다. 멀티스레딩과 관련이 있습니다.                  |
* Object클래스는 멤버변수는 없고 오직 11개의 메서드만 가지고 있다
  * 이 메서드들은 모든 인스턴스가 가져야 할 기본적인 것들이다

#### equals(Object obj)
* 매개변수로 객체의 참조변수를 받아서 비교하여 그 결과를 boolean값으로 알려주는 역할을 한다
```java
public boolean equals(Object obj) {
    return (this == obj);
        }
```
* 두 객체의 같고 다름을 참조변수의 값으로 판단한다
  * 그렇기 때문에 서로 다른 두 객체를 equals메서드로 비교하면 항상 false를 결과로 얻게 된다
    * 객체를 생성할 때, 메모리의 비어있는 공간을 찾아 생성하므로 서로 다른 두 개의 객체가 같은 주소를 갖는 일은 있을 수 없다
      * 두 개 이상의 참조변수가 같은 주소값을 갖는 것(한 객체를 참조하는 것)은 가능하다

#### hashCode()
* 이 메서드는 해싱(hashing)기법에 사용되는 '해시함수(hash function)'를 구현한 것이다
  * 해싱을 데이터관리기법 주으이 하낭니데 다량의 데이터를 저장하고 검색하는데 유용하다
    * 해시함수는 찾고자하는 값을 입력하면, 그 값이 저장된 위치를 알려주는 해시코드(hash code)를 반환한다
```java
class Student {
    private String name;
    private int id;

    public Student(String name, int id) {
        this.name = name;
        this.id = id;
    }

    @Override
    public int hashCode() {
        // 객체의 필드를 기반으로 해시 코드 생성
        int result = 17; // 기본 해시 코드
        result = 31 * result + name.hashCode(); // 문자열 필드의 해시 코드를 추가
        result = 31 * result + id; // 정수 필드의 해시 코드를 추가
        return result;
    }
}

```
#### toString()
* 이 메서드는 인스턴스에 대한 정보를 문자열(String)로 제공할 목적으로 정의한 것이다
  * 인스턴스의 정보를 제공한다는 것은 대부분의 경우 인스턴스 변수에 저장된 값들을 문자열로 표현한다는 뜻이다
```java
public String toString() {
    return getClass().getName()+"@"+Integer.toHexString(hashCode());
        }
```
* Object클래스에 정의된 toString()
  * toString()을 호출하면 클래스이름에 16진수의 해시코드를 얻게 될 것이다
    * getClass()와 hashCode() 역시 Object클래스에 정의된 것이므로 인스턴스 생성없이 바로 호출할 수 있다

#### clone()
* 이 메서드는 자신을 복제하여 새로운 인스턴스를 생성하는 일을 한다
  * 어떤 인스턴스에 대해 작업을 할 때, 원래의 인스턴스는 보존하고 clone메서드를 이용해서 새로운 인스턴스를 생성하여 작업을 하면 작업이전의 값이 보존되므로 작업에 실패해서 원래의 상태로 되돌리거나 변경되기 전의 값을 참고하는데 도움이 될 것이다
* Object클래스에 정의된 clone()은 단순히 인스턴스변수의 값만 복사하기 때문에 참조타입의 인스턴스 변수가 있는 클래스는 완전한 인스턴스 복제가 이루어지지 않는다

## String클래스
* 기존의 다른 언어에서는 문자열을 char형의 배열로 다루었으나 자바에서는 문자열을 위한 클래스를 제공한다 <br>
-> String클래스
* String클래스는 문자열을 저장하고 이를 다루는데 필요한 메서드를 함께 제공한다

### 1. **불변성 (Immutable):**
* `String` 클래스의 불변성은 한 번 생성된 문자열은 변경할 수 없다는 것을 의미한다
  * 새로운 문자열을 연결하면 이전 문자열은 변경되지 않고 새로운 문자열이 생성됩니다

```java
String str1 = "Hello";
String str2 = str1 + " World"; // "Hello World" 문자열이 새로 생성됩니다.
System.out.println(str1); // 출력: Hello (str1은 변경되지 않음)
```

### 2. **문자열 리터럴:**
* 문자열 리터럴은 메모리 내에서 공유되어 같은 문자열을 여러 변수가 참조할 때 메모리를 공유합니다

```java
String str1 = "Hello";
String str2 = "Hello"; // 동일한 문자열 리터럴을 참조하므로 같은 객체를 참조합니다.
System.out.println(str1 == str2); // 출력: true (같은 객체를 참조하므로 true)
```

### 3. **문자열 연산:**
* `+` 연산자를 사용하여 문자열을 연결할 수 있다

```java
String greeting = "Hello, " + "World!";
System.out.println(greeting); // 출력: Hello, World!
```

### 4. **문자열 메서드:**
* `String` 클래스는 다양한 메서드를 제공한다

```java
String str = "  Hello, World!  ";
System.out.println(str.length()); // 출력: 15 (문자열의 길이)
System.out.println(str.trim()); // 출력: "Hello, World!" (양 끝의 공백 제거)
System.out.println(str.toUpperCase()); // 출력: "  HELLO, WORLD!  " (대문자로 변환)
System.out.println(str.contains("World")); // 출력: true (특정 문자열 포함 여부 확인)
System.out.println(str.substring(7, 12)); // 출력: "World" (부분 문자열 추출)
```
### 1. **StringBuffer와 StringBuilder 클래스:**
- `StringBuffer`와 `StringBuilder` 클래스는 문자열을 효율적으로 수정할 수 있는 가변(mutable) 문자열을 제공한다
- `StringBuffer`는 스레드 안전(thread-safe)하게 동작하므로 멀티스레드 환경에서 사용할 때 적합하며, `StringBuilder`는 스레드 안전하지 않으므로 단일 스레드 환경에서 더 빠른 성능을 제공한다

**StringBuffer 예시:**
```java
StringBuffer buffer = new StringBuffer("Hello");
buffer.append(" World"); // 문자열을 덧붙임
buffer.insert(0, "Hi, "); // 지정된 위치에 문자열 삽입
buffer.replace(0, 3, "Hey"); // 지정된 범위의 문자열을 대체
String result = buffer.toString(); // StringBuffer를 다시 String으로 변환
System.out.println(result); // 출력: "Hey, World"
```

**StringBuilder 예시:**
```java
StringBuilder builder = new StringBuilder("Hello");
builder.append(" World"); // 문자열을 덧붙임
builder.insert(0, "Hi, "); // 지정된 위치에 문자열 삽입
builder.replace(0, 3, "Hey"); // 지정된 범위의 문자열을 대체
String result = builder.toString(); // StringBuilder를 다시 String으로 변환
System.out.println(result); // 출력: "Hey, World"
```

### 2. **Math 클래스:**
- `Math` 클래스는 기본적인 수학계산에 유용한 메서드로 구성되어 있다
  - Math클래스의 생성자는 접근 제어자가 private이기 때문에 다른 클래스에서 Math인스턴스를 생성할 수 없도록 되어있다
    - 그 이유는 클래스 내에 인스턴스 변수가 하나도 없어서 인스턴스를 생성할 필요가 없기 때문이다
      - Math클래스의 메서드는 모두 static이다

**Math 클래스 메서드 예시:**
```java
double x = 4.0;
double y = 2.0;

double sum = Math.addExact(5, 3); // 덧셈
double difference = Math.subtractExact(x, y); // 뺄셈
double product = Math.multiplyExact(6, 7); // 곱셈
double quotient = Math.floorDiv(10, 3); // 정수 나눗셈

double sqrt = Math.sqrt(x); // 제곱근 계산
double power = Math.pow(x, y); // 거듭제곱 계산
double absValue = Math.abs(-7.5); // 절댓값 계산

System.out.println("Sum: " + sum);
System.out.println("Difference: " + difference);
System.out.println("Product: " + product);
System.out.println("Quotient: " + quotient);
System.out.println("Square Root: " + sqrt);
System.out.println("Power: " + power);
System.out.println("Absolute Value: " + absValue);
```

### 3. **래퍼 클래스 (Wrapper Classes):**
- 래퍼 클래스는 기본 데이터 타입을 객체로 래핑하는 역할을 한다
  - 객체지향 개념에서 모든 것은 객체로 다루어져야한다
- 대표적인 래퍼 클래스로는 `Integer`, `Double`, `Boolean` 등이 있다

**래퍼 클래스 사용 예시:**
```java
Integer intValue = 42; // int를 래퍼 클래스로 래핑
Double doubleValue = 3.14; // double을 래퍼 클래스로 래핑
Boolean boolValue = true; // boolean을 래퍼 클래스로 래핑

int intFromWrapper = intValue.intValue(); // 래퍼 클래스에서 기본 타입으로 변환
double doubleFromWrapper = doubleValue.doubleValue();
boolean boolFromWrapper = boolValue.booleanValue();

System.out.println("Integer Value: " + intValue);
System.out.println("Double Value: " + doubleValue);
System.out.println("Boolean Value: " + boolValue);
```
## 유용한 클래스
1. **java.util.Objects 클래스:**
* Object클래스의 보조 클래스로 Math클래스처럼 모든 메서드가 'static'이다
  * 객체의 비교나 널 체크(null check)에 유용하다
     ```java
     String str = "Hello";
     String nullStr = null;

     // null 검사
     boolean isNull = Objects.isNull(nullStr); // true
     boolean nonNull = Objects.nonNull(str);    // true

     // 객체 비교
     boolean isEqual = Objects.equals(str, "Hello"); // true
     ```
* isNull()은 해당 객체가 널인지 확인해서 null이면 true를 반환하고 아니면 false를 반환한다
  * nonNull()은 inNull()과 정반대의 일을 한다
    * 즉, !Objects.isNull(obj)와 같다
2. **java.util.Random 클래스:**
- `java.util.Random` 클래스를 사용하여 난수를 생성할 수 있다

   ```java
   Random random = new Random();
   int randomNumber = random.nextInt(100); // 0부터 99까지의 난수 생성
   ```

3. **java.util.regex 패키지:**
- `java.util.regex` 패키지를 사용하여 정규 표현식을 처리할 수 있습니다. 
  - 문자열에서 숫자를 추출하는 예제

   ```java
   import java.util.regex.Matcher;
   import java.util.regex.Pattern;

   public class RegexExample {
     public static void main(String[] args) {
         String text = "The price of the product is $25.99";
         String regex = "\\$\\d+\\.\\d+"; // 정규 표현식 패턴
           
         Pattern pattern = Pattern.compile(regex);
         Matcher matcher = pattern.matcher(text);

         while (matcher.find()) {
             String match = matcher.group();
             System.out.println("Matched: " + match); // $25.99
         }
     }
   }
   ```
* 문자열에서 $기호로 시작하고 소수점을 포함하는 숫자를 추출하는 정규 표현식 패턴을 사용함
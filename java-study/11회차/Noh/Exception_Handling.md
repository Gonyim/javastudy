# 예외처리(exception handling)
### 프로그램 오류
```java
컴파일 에러 : 컴파일 시에 발생하는 에러
런타임 에러 : 실행 시에 발생하는 에러
논리적 에러 : 실행은 되지만, 의도와 다르게 동작하는 것
```
* 자바에서는 실행 시(runtime) 발생할 수 있는 프로그램 오류를 '에러(error)'와 '예외(exception)' 두 가지로 구분하였다
  * 에러는 메모리 부족(OutOfMemoryError)이나 스택오버플로우(StackOverflowError)와 같이 일단 발생하면 복구할 수 없는 심각한 오류이고, 예외는 발생하더라도 수습도리 수 있는 비교적 덜 심각한 것이다
    * 에러는 발생하면, 프로그램의 비정상적인 종료를 막을 길이 없지만, 예외는 발생하더라도 프로그래머가 이에 대한 적절한 코드를 미리 작성해 놓음으로써 프로그램의 비정상적인 종료를 막을 수 있다
```java
에러(error) : 프로그램 코드에 의해서 수습될 수 없는 심각한 오류
예외(exception) : 프로그램 코드에 의해서 수습될 수 있는 다소 미약한 오류
```
### 예외처리하기 - try-catch문
* 예외처리(exception handling)란, 프로그램 실행 시 발생할 수 있는 예기치 못한 예외의 발생에 대비한 코드를 작성하는 것이며, 예외처리의 목적은 예외의 발생으로 인한 실행 중인 프로그램의 갑작스런 비정상 종료를 막고, 정상적인 실행상태를 유지할 수 있도록 하는 것이다
```java
예외처리(exception handling)의
    정의 - 프로그램 실행 시 발생할 수 있는 예외에 대비한 코드를 작성하는 것
    목적 - 프로그램의 비정상 종료를 막고, 정상적인 실행상태를 유지하는 것
```
* 발생한 예외를 처리하지 못하면, 프로그램은 비정상적으로 종료되며, 처리되지 못한 예외(uncaught exception)는 JVM의 '예외처리기(UncaughtExceptionHandler)'가 받아서 예외의 원인을 화면에 출력한다
```java
try {
    // 예외가 발생할 가능성이 있는 문장들을 넣는다
} catch (Exception1 e1) {
    // Exception1이 발생했을 경우, 이를 처리하기 위한 문장을 적는다
        }
```
* 하나의 try블럭 다음에는 여러 종류의 예외를 처리할 수 있도록 하나 이상의 catch블럭이 올 수 있으며, 이 중 발생한 예외의 종류와 일치하는 단 한 개의 catch블럭만 수행된다
  * 발생한 예외의 종류와 일치하는 catch블럭이 없으면 예외는 처리되지 않는다
* if문과 달리, try블럭이나 catch블럭 내에 포함된 문장이 하나뿐이어도 괄호{}를 생략할 수 없다
* catch 블럭 내에 또 하나의 try-catch무이 포함된 경우, 같은 이름의 참조변수를 사용해서는 안된다
### try-catch문에서의 흐름
* try-catch문에서, 예외가 발생한 경우와 발생하지 않았을 때의 흐름(문장의 실행순서)이 달라지는데, 아래에 이 두 가지 경우에 따른 문장 실행순서를 정리하였다
```java
- try블럭 내에서 예외가 발생한 경우,
1. 발생한 예외와 일치하는 catch블럭이 있는 지 확인한다
2. 일치하는 catch블럭을 찾게 되면, 그 catch블럭 내의 문장들을 수행하고 전체 try-catch문을 빠져나가서 그 다음 문장을 계속해서 수행한다. 만일 일치하는 catch블럭을 찾지 못하면, 예외는 처리되지 못한다
- try블럭 내에서 예외가 발생하지 않은 경우,
1. catch블럭을 거치지 않고 전체 try-catch무을 빠져나가서 수행을 계속한다
```

#### 예외의 발생과 catch 블록
* `try` 블록 내에 예외가 발생할 수 있는 코드를 작성하고, 이 예외를 처리하는 `catch` 블록을 정의합니다
* catch블럭은 괄호()와 블럭{} 두 부분으로 나눠져 있는데, 괄호()내에는 처리하고자 하는 예외와 같은 타입의 참조변수 하나를 선언해야한다
  * 예외가 발생하면, 발생한 예외에 해당하는 클래스의 인스턴스가 만들어진다
  * 예외가 발생한 문장이 try블럭에 포함되어 있다면, 이 예외를 처리할 수 있는 catch블럭이 있는 지 찾게된다
* 첫 번째 catch블럭부터 차례로 내려가면서 catch블럭의 괄호() 내에 선어된 참조변수의 종류와 생성된 예외클래스의 인스턴스에 instanceof연산자를 이용해서 검사하게 되는데, 검사결과가 true인 catch블럭을 만날 때 까지 검사는 계속된다
  * 검사결과가 true인 catch블럭을 찾게 되면 블럭에 있는 문장들을 모두 수행한 후에 try-catch문을 빠져나가고 예외는  처리되지만, 검사결과가 true인 catch블럭이 하나도 없으면 예외는 처리되지 않는다
    * 모든 예외 클래스는 Exceptino클래스의 자손이므로, catch블럭의 괄호()에 Exception클래스 타입의 참조변수를 선언해놓으면 어떤 종류의 예외가 발생하더라도 이 catch블럭에 의해서 처리된다
```java
try {
    // 예외가 발생할 수 있는 코드
} catch (ExceptionType1 e1) {
    // 예외 처리 코드
} catch (ExceptionType2 e2) {
    // 예외 처리 코드
} finally {
    // 항상 실행되는 코드 (생략 가능)
}
```

#### printStackTrace()와 getMessage()
* 예외가 발생했을 때 생성되는 예외 클래스의 인스턴스에는 발생한 예외에 대한 정보가 담겨 있으며, getMessage()와 printStackTrace()를 통해서 이 정보들을 얻을 수 있다
  * catch블럭의 괄호()에 선언된 참조변수를 통해 이 인스턴스에 접근할 수 있다
    * 이 참조변수는 선언된 catch블럭 내에서만 사용 가능하다
```java
printStackTrace() : 예외발생 당시의 호출스택(Call Stack)에 있었던 메서드의 정보와 예외 메시지를 화면에 출력한다
getMessage() : 발생한 예외클래스의 인스턴스에 저장된 메시지를 얻을 수 있다
```

```java
catch (Exception e) {
    e.printStackTrace(); // 예외 정보 출력
    System.out.println("예외 메시지: " + e.getMessage()); // 예외 메시지 출력
}
```

#### 멀티 catch 블록
* Java 1.7부터 여러 catch블럭을 '|'기호를 이용해서, 하나의 catch블럭으로 합칠 수 있게 되었으며, 이를 '멀티 catch블럭'이라 한다
  * '멀티 catch블럭'을 이용하면 중복된 코드를 줄일 수 있다
    * '|'기호로 연결할 수 있는 예외 클래스의 개수에는 제한이 없다
      * 멀티 catch블럭에 사용되는 '|'는 논리 연산자가 아니라 기호이다

```java
try {
    // 예외가 발생할 수 있는 코드
} catch (ExceptionType1 | ExceptionType2 e) {
    // 예외 처리 코드
}
```

#### 예외 발생시키기
* 프로그래머가 직접 예외를 발생시킬 수 있습니다
    * `throw` 키워드를 사용하여 예외 객체를 생성하고 던질 수 있습니다

```java
1. 먼저, 연산자 new를 이용해서 발생시키려는 예외 클래스의 객체를 만든 다음
    Exception e = new Exception("고의로 발생시켰음");
2. 키워드 throw를 이용해서 예외를 발생시킨다
    throw e;
```

```java
public void customExceptionExample() throws CustomException {
    // 사용자 정의 예외 CustomException을 발생시킨다
    throw new CustomException("Custom exception occurred");
}
```

#### 메서드에 예외 선언하기
* 예외를 처리하는 방법에는 try-catch문을 사용하는 것 외에, 예외를 메서드에 선언하는 방법이 있다
* 메서드에 예외를 선언하려면, 메서드이 선언부에 키워드 throws를 사용해서 메서드 내에서 발생할 수 있는 예외를 적어주기만 하면된다
  * 예외가 여러 개일 경우에는 쉼표(,)로 구분한다
```java
void method() throws Exception1, Exception2, ... ExceptionN {
    // 메서드의 내용
        }
```
* 예외를 발생시키는 키워드 throw와 예외를 메서드에 선언할 때 쓰이는 throws를 잘 구별하자
* 만일 모든 예외의 최고조상인 Exception클래스를 메서드에 선언하면, 이 메서드는 몯느 종류의 예외가 발생할 가능성이 있다는 뜻이다
```java
void method() throws Exception {
    // 메서드의 내용
        }
```

#### finally 블록
* finally블럭은 예외의 발생여부에 상관없이 실행되어야할 코드를 포함시킬 목적으로 사용된다
* try-catch문의 끝에 선택적으로 덧붙여 사용할 수 있으며, try-catch-finally의 순서로 구성된다
```java
try {
    // 예외가 발생할 가능서잉 있는 문장들을 넣는다
} catch (Exception e) {
    // 예외처리를 위한 문장을 적는다
} finally {
    // 예외의 발생여부에 관계없이 항상 수행되어야하는 문장들을 넣는다
    // finally블럭은 try-catch문의 맨 마지막에 위치해야한다
}
```
* 예외가 발생한 경우에는 'try -> catch -> finally'의 순으로 실행되고, 예외가 발생하지 않은 경우에는 'try -> finally'의 순으로 실행된다

#### 자동 자원 반환 - try-with-resources 문
* Java 7부터 소위 "자동 리소스 관리"를 위한 `try-with-resources` 문이 도입되었습니다
  * 이를 사용하면 `AutoCloseable` 인터페이스를 구현한 리소스(파일, 데이터베이스 연결 등)를 자동으로 닫을 수 있습니다

```java
try (ResourceType resource = new ResourceType()) {
    // 리소스를 사용하는 코드
} catch (Exception e) {
    // 예외 처리 코드
} // 여기서 자동으로 리소스가 닫힘
```

#### 사용자 정의 예외 만들기
* 기존의 정의된 예외 클래스 외에 필요에 따라 프로그래머가 새로운 예외 클래스를 정의하여 사용할 수 있다
* 보통 Exception클래스 또는 RuntimeException클래스로부터 상속받아 클래스를 만들지만, 필요에 따라서 알맞은 예외 클래스를 선택할 수 있다
  * 가능하면 새로운 예외 클래스를 만들기보다 기존의 예외클래스를 활용하자!
```java
public class CustomException extends Exception {
    public CustomException(String message) { // 문자열을 매개변수로 받는 생성자
        super(message); // 조상인 Exception클래스의 생성자를 호출한다
    }
}
```

#### 예외 되던지기 (exception re-throwing)
* 예외를 잡은 후에 다시 던질 수 있습니다
  * 예외를 다른 코드 블록에서 처리하도록 할 수 있습니다

```java
try {
    // 예외가 발생할 수 있는 코드
} catch (Exception e) {
    // 예외를 다시 던짐
    throw e;
}
```

#### 연결된 예외 (chained exception)
* 예외를 연결하여 예외의 원인과 결과를 함께 전달할 수 있습니다
* `initCause()` 메서드를 사용하여 예외를 연결합니다

```java
try {
    // 예외가 발생할 수 있는 코드
} catch (Exception e) {
    // 새로운 예외 생성 및 연결
    IOException ioException = new IOException("I/O error");
    ioException.initCause(e);
    throw ioException;
}
```
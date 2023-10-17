## 예외와 예외 클래스

- 컴퓨터 하드웨어의 오동작 또는 고장으로 인해 응용프로그램 실행 오류가 발생하는 것을 자바에서는 에러`Error`라고 함
- 에러는 JVM 실행에 문제가 생겼다는 것이므로 프로그램을 아무리 견고하게 만들어도 결국 실행 불가하기 때문에 개발자가 대처할 방법이 없음
- 사용자의 잘못된 조작 또는 개발자의 잘못된 코딩으로 인해 발생하는 프로그램 오류를 예외`Exception`라고 부름
- 예외가 발생하면 프로그램이 곧바로 종료된다는 점에서 에러와 동일하지만, 예외 처리를 통해 정상 실행 상태가 유지되도록 할 수 있음

예외는 일반 예외, 실행 예외 두 가지 종류가 있습니다. 일반 예외는 컴파일러 체크 예외라고도 하는데, 자바 소스를 컴파일하는 과정에서 예외 처리 코드가 필요한지 검사하기 때문입니다. 만약 예외 처리 코드가 없다면 컴파일 오류가 발생합니다. 실행 예외는 컴파일하는 과정에서 예외 처리 코드를 검사하지 않는 예외를 말합니다. 컴파일 시 예외 처리를 확인하는 차이일 뿐, 두 가지 예외는 모두 예외 처리가 필요합니다.

> 자바에서는 예외를 클래스로 관리합니다.
그래서 모든 예외 클래스들은 java.lang.Exception 클래스를 상속받습니다.

JVM은 RuntimeException을 상속했는지 여부를 보고 실행 예외와 일반 예외를 구별합니다.

<br>

## 실행 예외
실행 예외는 자바 컴파일러가 체크를 하지 않기 때문에 개발자가 실행 예외에 대한 처리 코드를 넣지 않았을 경우, 해당 예외가 발생하면 프로그램이 곧바로 종료됩니다.

<br>

### NullPointException
빈번하게 발생하는 실행 예외입니다. 이 예외는 객체 참조가 없는 상태, 즉 null 값을 갖는 참조 변수로 객체 접근 연산자인 도트`.`를 사용했을 때 발생합니다.

```java
public class Main {
	public static void main(String[] args) {
    	String data = null;
        System.out.println(data.toString());
    }
}
```

<br>

### ArrayIndexOutOfBoundsException
배열에서 인덱스 범위를 초과하여 사용할 경우 발생합니다.

```java
public class Main {
	public static void main(String[] args) {
    	String data1 = args[0];
        String data2 = args[1];
        
        System.out.println("args[0]: " + data1);
        System.out.println("args[1]: " + data2);
    }
}
```

<br>

### NumberFormatException
프로그램을 개발하다 보면 문자열로 되어 있는 데이터를 숫자로 변경하는 경우가 자주 발생하는데 그럴 때 많이 사용되는 코드는 다음과 같습니다.

|변환 타입|메소드명(매개 변수)|설명|
|---|---|---|
|int|Integer.parseInt(String s)|주어진 문자열을 정수로 변환해서 리턴|
|double|Double.parseDouble(String s)|주어진 문자열을 실수로 변환해서 리턴|

Integer와 Double은 포장`Wrapper` 클래스라고 하는데, 이 클래스의 정적 메소드인 parseXXX() 메소드를 이용하면 문자열을 숫자로 변환할 수 있습니다. 이 메소드는 매개값인 문자열이 숫자로 변환될 수 있다면 숫자를 리턴하지만, 숫자로 변환될 수 없는 문자가 포함되어 있다면 java.lang.NumberFormatException을 발생시킵니다.

```java
public class Main {
	public static void main(String[] args) {
    	String data1 = "100";
        String data2 = "a100";
        
        int value1 = Integer.parseInt(data1);
        int value2 = Integer.parseInt(data2); // NumberFormatException
        
        int result = value1 + value2;
        System.out.println(data1 + "+" + data2 + "=" + result);
    }
}
```

<br>

### ClassCastException
타입 변환`Casting`은 상위 클래스와 하위 클래스 간에 발생하고 구현 클래스와 인터페이스 간에도 발생합니다. 그 외에 억지로 타입 변환을 시도할 경우 ClassCastException이 발생합니다.

```java
Animal animal = new Dog();
Cat cat = (Cat) animal;
```

<br>

## 예외 처리 코드
예외 처리 코드는 예외가 발생했을 경우 프로그램의 갑작스러운 종료를 막고, 정상 실행을 유지할 수 있도록 처리하는 코드입니다. 에외 처리 코드는 `try-catch-finally` 블록을 이용하고 생성자 내부와 메소드 내부에서 작성됩니다.

`try` 블록에는 예외 발생 가능 코드가 위치합니다. try 블록의 코드가 정상 실행되면 catch 블록의 코드는 실행되지 않고 finally 블록의 코드를 실행합니다. 만약 try 블록의 코드에서 예외가 발생하면 실행을 멈추고 `catch` 블록으로 이동하여 예외 처리 코드를 실행합니다. 그리고 finally 블록의 코드를 실행합니다. `finally` 블록은 옵션으로 생략이 가능합니다. 예외 발생 여부와 상관없이 항상 실행할 내용이 있을 경우에만 작성해주면 되고, try 블록과 catch 블록에서 return문을 사용하더라도 finally 블록은 항상 실행됩니다.

```java
try {
	예외 발생 가능 코드
} catch(예외클래스 e) {
	예외 처리
} finally {
	항상 실행;
}
```

<br>

## 예외 종류에 따른 처리 코드
### 다중 catch
try 블록 내부에서 다양한 종류의 예외가 발생할 수 있는데, 이 경우 다중 catch 블록을 작성합니다.

```java
public class Main {
	public static void main(String[] args) {
    	try {
        	String data1 = args[0];
            String data2 = args[1];
            int value1 = Integer.parseInt(data1);
            int value2 = Integer.parseInt(data2);
            int result = value1 + value2;
            System.out.println(data1 + "+" + data2 + "=" + result);
        } catch(ArrayIndexOutOfBoundsException e) {
        	System.out.println("실행 매개값의 수가 부족합니다.");
            System.out.println("[실행 방법]");
            System.out.println("java Main num1 num2);
        } catch(NumberFormatException e) {
        	System.out.println("숫자로 변환할 수 없습니다.");
        } finally {
        	System.out.println("다시 실행하세요.");
        }
    }
}
```

<br>

### catch 순서
다중 catch 블록은 상위 예외 클래스가 하위 예외 클래스보다 아래쪽에 위치하도록 작성해야 합니다. 만약 상위 예외 클래스의 catch 블록이 위에 있다면, 하위 예외 클래스의 catch 블록은 실행되지 않습니다. 하위 예외는 상위 예외를 상속했기 때문에 상위 예외 타입도 되기 때문입니다.

```java
// X
try {
	// ArrayIndexOutOfBoundsException 발생
    // 다른 Exception 발생
} catch(Exception e) {
	예외 처리1
} catch(ArrayIndexOutOfBoundsException e) {
	예외 처리2
}

// O
try {
	// ArrayIndexOutOfBoundsException 발생
    // 다른 Exception 발생
} catch(ArrayIndexOutOfBoundsException e) {
	예외 처리1
} catch(Exception e) {
	예외 처리2
}
```

<br>

### 멀티 catch
자바 7부터 하나의 catch 블록에서 여러 개의 예외를 처리할 수 있도록 멀티 catch 기능이 추가됐습니다. catch 괄호 안에 동일하게 처리하고 싶은 예외를 파이프`|`로 연결하면 됩니다.

```java
public class Main {
	public static void main(String[] args) {
    	try {
        	String data1 = args[0];
            String data2 = args[1];
            int value1 = Integer.parseInt(data1);
            int value2 = Integer.parseInt(data2);
            int result = value1 + value2;
            System.out.println(data1 + "+" + data2 + "=" + result);
        } catch(ArrayIndexOutOfBoundsException | NumberFormatException e) {
        	System.out.println("실행 매개값의 수가 부족하거나 숫자로 변환할 수 없습니다.");
        } catch(Exception e) {
        	System.out.println("알 수 없는 예외 발생");
        } finally {
        	System.out.println("다시 실행하세요.");
        }
    }
}
```

<br>

## 자동 리소스 닫기
자바 7부터 새로 추가된 `try-with-resources`를 사용하면 예외 발생 여부와 상관없이 사용했던 리소스 객체(각종 입출력 스트림, 서버 소켓, 소켓, 각종 채널)의 `close()` 메소드를 호출해서 안전하게 리소스를 닫아줍니다.

```java
// 자바 6까지 사용한 코드
FileInputStream fis = null;
try {
	fis = new FileInputStream("file.txt");
    ...
} catch(IOException e) {
	...
} finally {
	if(fis != null) {
    	try {
        	fis.close();
        } catch(IOException e) { }
    }
}

// try-with-resources
try(FileInputStream fis = new FileInputStream("file.txt"); {
	...
} catch(IOException e) {
	...
}
```

`try-with-resources`를 사용하기 위해서는 리소스 객체가 java.lang.AutoCloseable 인터페이스를 구현하고 있어야 합니다. AutoCloseable에는 `close()` 메소드가 정의되어 있는데 try-with-resources는 바로 이 close() 메소드를 자동 호출합니다.

> API 도큐먼트에서 AutoCloseable 인터페이스를 찾아보면 try-with-resources와 함께 사용할 수 있는 리소스들을 확인할 수 있습니다.

#### 예제
```java
// FileInputStream.java
public class FileInputStream implements AutoCloseable {
	private String file;
    
    public FileInputStream(String file) {
    	this.file = file;
    }
    
    public void read() {
    	System.out.println(file + "을 읽습니다.");
    }
    
    @Override
    public void close() throws Exception {
    	System.out.println(file + "을 닫습니다.");
    }
}

// Main.java
public class Main {
	public static void main(String[] args) {
    	try (FileInputStream fis = new FileInputStream("file.txt")) {
        	fis.read();
            throw new Exception(); // 강제 예외
        } catch (Exception e) {
        	System.out.println("예외 처리 코드가 실행되었습니다.");
        }
    }
}
```

<br>

## 예외 떠넘기기
메소드 내부에서 예외가 발생할 수 있는 코드를 작성할 때 try-catch 블록으로 예외를 처리하는 것이 기본이지만, 경우에 따라서는 메소드를 호출한 곳으로 예외를 떠넘길 수도 있습니다. 이때 사용하는 키워드가 `throws`입니다. throws 키워드는 메소드 선언부 끝에 작성되어 메소드에서 처리하지 않은 예외를 호출한 곳으로 떠넘기는 역할을 합니다.

```java
리턴타입 메소드명(매개변수, ... ) throws 예외클래스1, 예외클래스2, ... {
}

// 모든 예외
리턴타입 메소드명(매개변수, ... ) throws Exception {
}
```

> throws 키워드가 붙어있는 메소드는 반드시 try 블록 내에서 호출되어야 합니다.

```java
public void method1() {
	try {
    	method2();
    } catch(ClassNotFoundException e) {
    	System.out.println("클래스가 존재하지 않습니다.");
    }
}

public void method2() throws ClassNotFoundException {
	Class class = Class.forName("java.lang.String2");
}
```

main() 메소드에서도 throws 키워드를 사용해서 예외를 떠넘길 수 있는데, 그렇게 되면 JVM이 예외 내용을 콘솔에 출력하는 것으로 예외 처리를 하게 됩니다.

<br>

## 사용자 정의 예외와 예외 발생
애플리케이션 서비스와 관련된 예외를 애플리케이션 예외`Application Exception`라고 합니다. 애플리케이션 예외는 개발자가 직접 정의해서 만들어야 하므로 사용자 정의 예외라고도 합니다.

### 사용자 정의 예외 클래스 선언
사용자 정의 예외 클래스는 일반 예외, 실행 예외 두 가지 모두 선언할 수 있습니다. 일반 예외로 선언할 경우 Exception을 상속하면 되고, 실행 예외로 선언할 경우에는 RuntimeException을 상속하면 됩니다.

```java
public class XXXException extends [Exception | RuntimeException] {
	public XXXException() { }
    public XXXException(String message) {
    	super(message);
    }
}
```

> 사용자 정의 예외 클래스 이름은 Exception으로 끝나는 것이 좋음

사용자 정의 예외 클래스도 필드, 생성자, 메소드를 가질 수 있지만 대부분 생성자만을 포함합니다. 생성자는 두 개를 선언하는 것이 일반적인데, 하나는 매개 변수가 없는 기본 생성자이고 다른 하나는 예외 발생 원인(예외 메시지)를 전달하기 위해 String 타입 매개 변수를 갖는 생성자입니다.

String 타입 매개 변수를 갖는 생성자는 상위 클래스의 생성자를 호출하여 예외 메시지를 넘겨줍니다. 예외 메시지의 용도는 catch 블록의 예외 처리 코드에서 사용하기 위해서입니다.

```java
public class BalanceInsufficientException extends Exception {
	public BalanceInsufficientException() { }
    public BalanceInsufficientException(String message) {
    	super(message);
    }
}
```

<br>

### 예외 발생시키기
사용자 정의 예외 또는 자바 표준 예외를 발생시키는 방법은 다음과 같습니다.

```java
throw new XXXException();
throw new XXXException("메시지");
```

```java
public class Account {
	private long balance;
    
    public Account() { }
    
    public long getBalance() {
    	return balance;
    }
    public void deposit(int money) {
    	balance += money;
    }
    public void withdraw(int money) throws BalanceInsufficientException {
    	if (balance < money) {
        	throw new BalanceInsufficientException("잔고부족:" + (money-balance)+"모자람");
        }
        balance -= money;
    }
}
```

<br>

## 예외 정보 얻기
try 블록에서 예외가 발생되면 예외 객체는 catch 블록의 매개 변수에서 참조하게 되므로 매개 변수를 이용하면 예외 객체의 정보를 알 수 있습니다. 모든 예외 객체는 Exception 클래스를 상속하기 때문에 여러 메소드들을 호출할 수 있는데, 그 중 많이 사용되는 메소드는 `getMessage()`와 `printStackTrace()`입니다.

```java
public class Main {
	public static void main(String[] args) {
    	Account account = new Account();
        // 예금하기
        account.deposit(10000);
        System.out.println("예금액: " + account.getBalance();
        // 출금하기
        try {
        	account.withdraw(30000);
        } catch(BalanceInsufficientException e) {
        	String message = e.getMessage();
            System.out.println(message);
            System.out.println();
            e.printStackTrace();
        }
    }
}
```

<br>

## 레퍼런스
- 이것이 자바다: 신용권의 Java 프로그래밍 정복
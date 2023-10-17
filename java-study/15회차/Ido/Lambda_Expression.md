## 람다식이란?
람다식은 익명 함수를 생성하기 위한 식으로 객체 지향 언어보다는 함수 지향 언어에 가깝습니다. 자바는 함수적 프로그래밍을 위해 자바 8부터 람다식`Lambda Expressions`을 지원합니다.

> 함수적 프로그래밍은 병렬 처리와 이벤트 지향 프로그래밍에 적합합니다. 그래서 객체 지향 프로그래밍와 혼합함으로써 더욱 효율적인 프로그래밍이 가능하게 됩니다.

자바에서 람다식을 수용한 이유는 코드가 간결해지고, 컬렉션의 요소를 필터링하거나 매핑해서 원하는 결과를 쉽게 얻을 수 있기 때문입니다. 람다식의 형태는 매개 변수를 가진 코드 블록이지만, 런타임 시에는 익명 구현 객체를 생성합니다.

```java
람다식 -> 매개 변수를 가진 코드 블록 -> 익명 구현 객체

// Runnable의 익명 구현 객체 생성
Runnable runnable = new Runnable() {
	public void run() { ... }
};
// 위 코드를 람다식으로 표현
Runnable runnable = () -> { ... };
```

<br>

## 람다식 기본 문법
함수적 스타일의 람다식을 작성하는 방법은 다음과 같습니다.

```java
(타입 매개변수, ... ) -> { 실행문; ... }
```

`(타입 매개변수, ... )`는 오른쪽 중괄호 블록을 실행하기 위해 필요한 값을 제공하는 역할을 합니다. `->` 기호는 매개 변수를 이용해서 중괄호를 실행한다는 의미입니다.

```java
(int a) -> {System.out.println(a);}
```

매개 변수 타입은 런타임 시에 대입되는 값에 따라 자동으로 인식될 수 있기 때문에 람다식에서는 매개 변수의 타입을 일반적으로 언급하지 않습니다. 그래서 위 코드는 다음과 같이 작성할 수 있습니다.

```java
(a) -> {System.out.println(a);}

// 하나의 매개 변수만 있다면 괄호를 생략할 수 있고, 하나의 실행문만 있다면 중괄호도 생략 가능
a -> System.out.println(a);
```

중괄호를 실행하고 결과값을 리턴해야 한다면 다음과 같이 return문으로 결과값을 지정할 수 있습니다.

```java
(x, y) -> {return x + y};

// 중괄호에 return문만 있을 경우, 다음과 같이 작성하는 것이 정석
(x, y) -> x + y
```

<br>

## 타겟 타입과 함수적 인터페이스
자바는 메소드를 단독으로 선언할 수 없고 항상 클래스의 구성 멤버로 선언하기 때문에 람다식은 단순히 메소드를 선언하는 것이 아니라 이 메소드를 가지고 있는 객체를 생성해 냅니다.

```java
인터페이스 변수 = 람다식;
```

위와 같이 람다식은 인터페이스 변수에 대입됩니다. 인터페이스는 직접 객체화할 수 없기 때문에 구현 클래스가 필요한데, 람다식은 익명 구현 클래스를 생성하고 객체화합니다. 람다식은 대입될 인터페이스의 종류에 따라 작성 방법이 달라지기 때문에 람다식이 대입될 인터페이스를 람다식의 타겟 타입`target type`이라고 합니다.

<br>

### 함수적 인터페이스 @FunctionallInterface
람다식은 하나의 메소드를 정의하기 때문에 두 개 이상의 추상 메소드가 선언된 인터페이스는 람다식을 이용해서 구현 객체를 생성할 수 없습니다. 하나의 추상 메소드가 선언된 인터페이스만 람다식의 타겟 타입이 될 수 있는데, 이러한 인터페이스를 **함수적 인터페이스**라고 합니다. `@FunctionallInterface` 어노테이션을 붙이면 두 개 이상의 추상 메소드가 선언된 경우 컴파일 오류를 발생시킵니다.

```java
@FunctionallInterface
public interface MyFunctionallInterface {
	public void method();
    public void otherMethod(); // 컴파일 오류
}
```

람다식은 타겟 타입인 함수적 인터페이스가 가지고 있는 추상 메소드의 선언 형태에 따라서 작성 방법이 달라집니다.

<br>

### 매개 변수와 리턴값이 없는 람다식

```java
@FunctionallInterface
public interface MyFunctionallInterface {
	public void method();
}
```

위와 같이 매개 변수와 리턴값이 없는 추상 메소드를 가진 함수적 인터페이스를 타겟 타입으로 갖을 때, 람다식을 다음과 같이 작성합니다.

```java
MyFunctionallInterface fi = () -> { ... }
```

람다식이 대입된 인터페이스의 참조 변수는 다음과 같이 method()를 호출할 수 있습니다.

```java
fi.method();
```

<br>

### 매개 변수가 있는 람다식

```java
@FunctionallInterface
public interface MyFunctionallInterface {
	public void method(int x);
}
```

```java
MyFunctionallInterface fi = (x) -> { ... } 또는 x -> { ... }
```

```java
fi.method(5); // 람다식의 x 변수에 5가 대입되고 x는 중괄호에서 사용됨
```

<br>

### 리턴값이 있는 람다식

```java
@FunctionallInterface
public interface MyFunctionallInterface {
	public int method(int x, int y);
}
```

```java
MyFunctionallInterface fi = (x, y) -> { ...; return 값; }
```

중괄호에 return문만 있고, return문 뒤에 연산식이나 메소드 호출이 오는 경우 다음과 같이 작성할 수 있습니다.

```java
MyFunctionallInterface fi = (x, y) -> {
	return x + y;
}
// 아래와 같이 작성 가능
MyFunctionallInterface fi = (x, y) -> x + y;

MyFunctionallInterface fi = (x, y) -> {
	return sum(x + y);
}
// 아래와 같이 작성 가능
MyFunctionallInterface fi = (x, y) -> sum(x + y);
```

```java
int result = fi.method(2, 5);
```

<br>

## 클래스 멤버와 로컬 변수 사용
람다식의 실행 블록에서 클래스의 멤버 및 로컬 변수도 사용 가능합니다. 클래스의 멤버는 제약 사항 없이 사용 가능하지만, 로컬 변수는 제약 사항이 따릅니다.

<br>

### 클래스의 멤버 사용
this 키워드를 사용할 때에는 주의가 필요합니다. 일반적으로 익명 객체 내부에서 this는 익명 객체의 참조이지만, 람다식에서 this는 내부적으로 생성되는 익명 객체의 참조가 아니라 람다식을 실행한 객체의 참조가 됩니다.

#### 예제

```java
// MyFunctionallInterface.java
public interface MyFunctionallInterface {
	public void method();
}

// UsingThis.java
public class UsingThis {
	public int outterField = 10;
    
    class Inner {
    	int innerField = 20;
        
        void method() {
        	// 람다식
            MyFunctionallInterface fi = () -> {
            	// 바깥 객체의 참조를 얻기 위해서는 클래스명.this를 사용
            	System.out.println("outterField: " + outterField);
                System.out.println("outterField: " + UsingThis.this.outterField + "\n");
                
                // 람다식 내부에서 this는 Inner 객체를 참조
                System.out.println("innerField: " + innerField);
                System.out.println("innerField: " + this.innerField + "\n");
            };
            fi.method();
        }
    }
}

// Main.java
public class Main {
	public static void main(String[] args) {
    	UsingThis usingThis = new UsingThis();
        UsingThis.Inner inner = usingThis.new Inner();
        inner.method();
    }
}
```

<br>

### 로컬 변수 사용
람다식은 메소드 내부에서 주로 작성되기 때문에 로컬 익명 구현 객체를 생성하게 됩니다. 람다식에서 바깥 클래스의 필드나 메소드는 제한 없이 사용할 수 있으나, 메소드의 매개 변수 또는 로컬 변수를 사용하면 이 두 변수는 final 특성을 가져야 합니다. 따라서 매개 변수 또는 로컬 변수를 람다식에서 읽는 것은 허용되지만, 람다식 내부 또는 외부에서 변경할 수 없습니다.

#### 예제

```java
// MyFunctionallInterface.java
public interface MyFunctionallInterface {
	public void method();
}

// UsingLocalVariable.java
public class UsingLocalVariable {
	void method(int arg) { // arg는 final 특성을 가짐
    	int localVar = 40; // localVar는 final 특성을 가짐
        
        // arg = 31;
        // localVar = 41;
        
        // 람다식
        MyFunctionallInterface fi = () -> {
        	// 로컬 변수 읽기
            System.out.println("arg: " + arg);
            System.out.println("localVar: " + localVar + "\n");
        };
        fi.method();
    }
}

// Main.java
public class Main {
	public static void main(String[] args) {
    	UsingLocalVariable ulv = new UsingLocalVariable();
        ulv.method(20);
    }
}
```

<br>

## 표준 API의 함수적 인터페이스
자바에서 제공되는 표준 API에서 한 개의 추상 메소드를 가지는 인터페이스들은 모두 람다식을 이용해서 익명 구현 객체로 표현이 가능합니다.

```java
public class Main {
	public static void main(String[] args) {
    	Runnable runnable = () -> {
        	for (int i=0; i<10; i++) {
            	System.out.println(i);
            }
        };
        
        Thread thread = new Thread(runnable);
        thread.start();
    }
}
```

Thread 생성자를 호출할 때 다음과 같이 람다식을 매개값으로 대입할 수도 있습니다.

```java
Thread thread = new Thread(() -> {
	for (int i=0; i<10; i++) {
    	System.out.println(i);
    }
};
```

자바 8부터는 자주 사용되는 함수적 인터페이스를 java.util.function 표준 API 패키지로 제공합니다. 이 패키지에서 제공하는 함수적 인터페이스의 목적은 메소드 또는 생성자의 매개 타입으로 사용되어 람다식을 대입할 수 있도록 하는 것입니다. 함수적 인터페이스는 크게 5가지로 분류되는데, 구분 기준은 인터페이스에 선언된 추상 메소드의 매개값과 리턴값의 유무입니다.

|종류|추상 메소드 특징|
|---|---|
|Consumer|매개값 O 리턴값 X|
|Supplier|매개값 X 리턴값 O|
|Function|매개값 O 리턴값 O<br>주로 매개값을 리턴값으로 매핑(타입 변환)|
|Operator|매개값 O 리턴값 O<br>주로 매개값을 연산하고 결과를 리턴|
|Predicate|매개값 O 리턴값 boolean<br>매개값을 조사해서 true/false를 리턴|

<br>

### Consumer 함수적 인터페이스
리턴값이 없는 `accept()` 메소드를 가지고 있습니다. accept() 메소드는 단지 매개값을 소비하는 역할만 하고, 소비한다는 것은 사용만 하고 리턴값이 없다는 의미입니다. 매개 변수의 타입과 수에 따라서 아래와 같은 Consumer들이 있습니다.

|인터페이스명|추상 메소드|설명|
|---|---|---|
|Consumer< T >|void accept(T t)|객체 T를 받아 소비|
|BiConsumer<T, U>|void accept(T t, U u)|객체 T와 U를 받아 소비|
|DoubleConsumer|void accept(double value)|double 값을 받아 소비|
|IntConsumer|void accept(int value)|int 값을 받아 소비|
|LongConsumer|void accept(long value)|long 값을 받아 소비|
|ObjDoubleConsumer< T >|void accept(T t, double value)|객체 T와 double 값을 받아 소비|
|ObjIntConsumer< T >|void accept(T t, int value)|객체 T와 int 값을 받아 소비|
|ObjLongConsumer< T >|void accept(T t, long value)|객체 T와 long 값을 받아 소비|

`Consumer<T>` 인터페이스를 타겟 타입으로 하는 람다식은 다음과 같이 작성합니다. `accept()` 메소드는 매개값으로 T 객체 하나를 가지므로 람다식도 한 개의 매개 변수를 사용합니다.

```java
Consumer<String> consumer = t -> {t를 소비하는 실행문;};
```

`BiConsumer<T, U>` 인터페이스를 타겟 타입으로 하는 람다식은 다음과 같이 작성합니다.

```java
BiConsumer<String, String> consumer = (t, u) -> {t와 u를 소비하는 실행문;};
```

`DoubleConsumer` 인터페이스를 타겟 타입으로 하는 람다식은 다음과 같이 작성합니다. d는 고정적으로 double 타입이 됩니다.

```java
DoubleConsumer consumer = d -> {d를 소비하는 실행문;};
```

<br>

### Supplier 함수적 인터페이스
매개 변수가 없고 리턴값이 있는 `getXXX()` 메소드를 가지고 있습니다. 이 메소드들은 실행 후 호출한 곳으로 데이터를 리턴(공급)하는 역할을 합니다.

|인터페이스명|추상 메소드|설명|
|---|---|---|
|Supplier< T >|T get()|T 객체를 리턴|
|BooleanSupplier|boolean getAsBoolean()|boolean 값을 리턴|
|DoubleSupplier|double getAsDouble()|double 값을 리턴|
|IntSupplier|int getAsInt()|int 값을 리턴|
|LongSupplier|long getAsLong()|long 값을 리턴|

`Supplier<T>` 인터페이스를 타겟 타입으로 하는 람다식은 다음과 같이 작성합니다. 람다식의 중괄호는 반드시 한 개의 T 객체를 리턴하도록 해야 합니다.

```java
Supplier<String> supplier = () -> { ...; return "문자열";};
```

`IntSupplier` 인터페이스를 타겟 타입으로 하는 람다식은 다음과 같이 작성합니다.

```java
IntSupplier supplier = () -> { ...; return int값;};
```

<br>

### Function 함수적 인터페이스
매개값과 리턴값이 있는 `applyXXX()` 메소드를 가지고 있습니다. 이 메소드들은 매개값을 리턴값으로 매핑(타입 변환)하는 역할을 합니다.

|인터페이스명|추상 메소드|설명|
|---|---|---|
|Function<T, R>|R apply(T t)|객체 T를 객체 R로 매핑|
|BiFunction<T, U, R>|R apply(T t, U u)|객체 T와 U를 객체 R로 매핑|
|DoubleFunction< R >|R apply(double value)|double을 객체 R로 매핑|
|IntFunction< R >|R apply(int value)|int를 객체 R로 매핑|
|IntToDoubleFunction|double applyAsDouble(int value)|int를 double로 매핑|
|IntToLongFunction|long applyAsLong(int value)|int를 long으로 매핑|
|LongToDoubleFunction|double applyAsDouble(long value)|long을 double로 매핑|
|LongToIntFunction|int applyAsInt(long value)|long을 int로 매핑|
|ToDoubleBiFunction<T, U>|double applyAsDouble(T t, U u)|객체 T와 U를 double로 매핑|
|ToDoubleFunction< T >|double applyAsDouble(T t)|객체 T를 double로 매핑|
|ToIntBiFunction<T, U>|int applyAsInt(T t, U u)|객체 T와 U를 int로 매핑|
|ToIntFunction< T >|int applyAsInt(T t)|객체 T를 int로 매핑|
|ToLongBiFunction<T, U>|long applyAsLong(T t, U u)|객체 T와 U를 long으로 매핑|
|ToLongFunction< T >|long applyAsLong(T t)|객체 T를 long으로 매핑|

`Function<T, R>` 인터페이스를 타겟 타입으로 하는 람다식은 다음과 같이 작성해서 Student 객체를 학생 이름(String)으로 매핑할 수 있습니다. `apply()` 메소드는 매개값으로 T 객체 하나를 가지므로 람다식도 한 개의 매개 변수를 사용합니다. 그리고 리턴 타입이 R이므로 람다식 중괄호의 리턴값을 R 객체가 됩니다. 

```java
Function<Student, String> function = t -> {return t.getName();};
또는
Function<Student, String> function = t -> t.getName();
```

<br>

### Operator 함수적 인터페이스
Function과 동일하게 매개 변수와 리턴값이 있는 `applyXXX()` 메소드를 가지고 있습니다. 하지만 이 메소드들은 매개값을 리턴값으로 매핑하는 역할보다는 매개값을 이용해서 연산을 수행한 후 동일한 타입으로 리턴값을 제공하는 역할을 합니다.

|인터페이스명|추상 메소드|설명|
|---|---|---|
|BinaryOperator< T >|T apply(T t, T t)|T와 T를 연산한 후 T 리턴|
|UnaryOperator< T >|T apply(T t)|T를 연산한 후 T 리턴|
|DoubleBinaryOperator|double applyAsDouble(double, double)|두 개의 double 연산|
|DoubleUnaryOperator|double applyAsDouble(double)|한 개의 double 연산|
|IntBinaryOperator|int applyAsInt(int, int)|두 개의 int 연산|
|IntUnaryOperator|int applyAsInt(int)|한 개의 int 연산|
|LongBinaryOperator|long applyAsLong(long, long)|두 개의 long 연산|
|LongUnaryOperator|long applyAsLong(long)|한 개의 long 연산|

`IntBinaryOperator` 인터페이스를 타겟 타입으로 하는 람다식은 다음과 같이 작성합니다.

```java
IntBinaryOperator operator = (a, b) -> { ...; return int값; };
```

<br>

### Predicate 함수적 인터페이스
매개 변수와 boolean 리턴값이 있는 `testXXX()` 메소드를 가지고 있습니다. 이 메소드들은 매개값을 조사해서 true 또는 false를 리턴하는 역할을 합니다.

|인터페이스명|추상 메소드|설명|
|---|---|---|
|Predicate< T >|boolean test(T t)|객체 T를 조사|
|BiPredicate<T, U>|boolean test(T t, U u)|객체 T와 U를 비교 조사|
|DoublePredicate|boolean test(double value)|double 값을 조사|
|IntPredicate|boolean test(int value)|int 값을 조사|
|LongPredicate|boolean test(long value)|long 값을 조사|

```java
Predicate<Student> predicate = t -> {return t.getGender().equals("남자");};
또는
Predicate<Student> predicate = t -> t.getGender().equals("남자");
```

<br>

### andThen()과 compose() 디폴트 메소드
디폴트 및 정적 메소드는 추상 메소드가 아니기 떄문에 함수적 인터페이스에 선언되어도 여전히 함수적 인터페이스의 성질을 잃지 않습니다. 여기서 함수적 인터페이스 성질이란 하나의 추상 메소드를 가지고 있고, 람다식으로 익명 구현 객체를 생성할 수 있는 것을 의미합니다.

> Consumer, Function, Operator 종류의 함수적 인터페이스는 andThen()과 compose() 디폴트 메소드를 가지고 있습니다.

`andThen()`과 `compose()`는 두 개의 함수적 인터페이스를 순차적으로 연결하고, 첫 번째 처리 결과를 두 번째 매개값으로 제공해서 최종 결과값을 얻을 때 사용합니다. 두 메소드의 차이점은 어떤 함수적 인터페이스부터 먼저 처리하느냐입니다.

```java
인터페이스AB = 인터페이스A.andThen(인터페이스B);
최종결과 = 인터페이스AB.method();
```

인터페이스AB의 method()를 호출하면 우선 인터페이스A부터 처리하고 결과를 인터페이스B의 매개값으로 제공합니다. 인터페이스B는 제공받은 매개값을 가지고 처리한 후 최종 결과를 리턴합니다.

```java
인터페이스AB = 인터페이스A.compose(인터페이스B);
최종결과 = 인터페이스AB.method();
```

compose()를 사용하면 인터페이스B부터 처리하고 결과를 인터페이스A의 매개값으로 제공합니다. 인터페이스A는 제공받은 매개값을 가지고 처리한 후 최종 결과를 리턴합니다.

![](https://velog.velcdn.com/images/kid/post/06f753cd-9ffe-4a16-b48c-c46115ecf3c3/image.png)

#### Consumer의 순차적 연결

- 처리 결과를 리턴하지 않기 때문에 andThen() 디폴트 메소드는 함수적 인터페이스의 호출 순서만 정함

#### Function, Operator의 순차적 연결

- 먼저 실행한 함수적 인터페이스의 결과를 다음 함수적 인터페이스의 매개값으로 넘겨주고, 최종 처리 결과를 리턴

<br>

### and(), or(), negate() 디폴트 메소드와 isEqual() 정적 메소드

> Predicate 종류의 함수적 인터페이스는 and(), or(), negate() 디폴트 메소드를 가지고 있습니다.

위 메소드들은 각각 논리 연산자인 `&&`, `||`, `!`와 대응됩니다. `Predicate<T>` 함수적 인터페이스는 `isEqual()` 정적 메소드를 추가로 제공합니다.

```java
// Objects.equals(sourceObject, targetObject) 실행
Predicate<Object> predicate = Predicate.isEqual(targetObject);
boolean result = predicate.test(sourceObject);
```

isEqual() 메소드는 test() 매개값인 sourceObject와 isEqual()의 매개값인 targetObject를 java.util.Objects 클래스의 equals()의 매개값으로 제공하고, Objects.equals(sourceObject, targetObject)의 리턴값을 얻어 새로운 `Predicate<T>`를 생성합니다.

<br>

### minBy(), maxBy() 정적 메소드

> BinaryOperator< T > 함수적 인터페이스는 minBy(), maxBy() 정적 메소드를 제공합니다.

위 두 메소드는 매개값으로 제공되는 Comparator를 이용해서 최대 T와 최소 T를 얻는 `BinaryOperator<T>`를 리턴합니다.

|리턴 타입|정적 메소드|
|---|---|
|BinaryOperator< T >|minBy(Comparator<? super T> comparator)|
|BinaryOperator< T >|maxBy(Comparator<? super T> comparator)|

`Comparator<T>`에는 o1과 o2를 비교해서 o1이 작으면 음수를, o1과 o2가 동일하면 0을, o1이 크면 양수를 리턴하는 메소드가 선언되어 있습니다.

```java
@FunctionalInterface
public interface Comparator<T> {
	public int compare(T o1, T o2);
}
```

```java
(o1, o2) -> {...; return int값;};

// o1과 o2가 int 타입일 경우
(o1, o2) -> Integer.compare(o1, o2);

// 사용
binaryOperator = BinaryOperator.minBy((o1, o2) -> Integer.compare(o1, o2));
```

<br>

## 메소드 참조
매개 변수의 정보 및 리턴 타입을 알아내어 람다식에서 불필요한 매개 변수를 제거하기 위해서 메소드를 참조합니다. 람다식은 종종 기본 메소드를 단순히 호출만 하는 경우가 많습니다.

```java
(left, right) -> Math.max(left, right);
```

람다식은 두 개의 값을 Math.max() 메소드의 매개값으로 전달하는 역할만 하고 있는데, 이럴 경우 메소드 참조를 이용합니다.

```java
Math :: max; // 메소드 참조
```

메소드 참조도 람다식과 마찬가지로 인터페이스의 익명 구현 객체로 생성되므로 타겟 타입인 인터페이스의 추상 메소드가 어떤 매개 변수를 가지고, 리턴 타입이 무엇인가에 따라 달라집니다. IntBinaryOperator 인터페이스는 두 개의 int 매개값을 받아 int 값을 리턴하므로 위의 메소드 참조를 대입할 수 있습니다.

```java
IntBinaryOperator operator = Math :: max;
```

메소드 참조는 정적 또는 인스턴스 메소드를 참조할 수 있고, 생성자 참조도 가능합니다.

<br>

### 정적 메소드와 인스턴스 메소드 참조

```java
클래스 :: 메소드 // 정적 메소드
참조변수 :: 메소드 // 인스턴스 메소드
```

#### 예제

```java
// Calculator.java
public class Calculator {
	public static int staticMethod(int x, int y) {
		return x + y;
	}

	public int instanceMethod(int x, int y) {
		return x + y;
	}
}

// Main.java
import java.util.function.IntBinaryOperator;

public class Main {
	public static void main(String[] args) {
		IntBinaryOperator operator;

		// 정적 메소드 참조
		operator = (x, y) -> Calculator.staticMethod(x, y);
		System.out.println("결과1: " + operator.applyAsInt(1, 2));

		operator = Calculator :: staticMethod;
		System.out.println("결과2: " + operator.applyAsInt(3, 4));

		// 인스턴스 메소드 참조
		Calculator obj = new Calculator();
		operator = (x, y) -> obj.instanceMethod(x, y);
		System.out.println("결과3: " + operator.applyAsInt(5, 6));

		operator = obj :: instanceMethod;
		System.out.println("결과4: " + operator.applyAsInt(7, 8));
	}
}
```

<br>

### 매개 변수의 메소드 참조
다음과 같이 람다식에서 제공되는 a 매개 변수의 메소드를 호출해서 b 매개 변수를 매개값으로 사용하는 경우도 있습니다.

```java
(a, b) -> {a.instanceMethod(b);}

클래스 :: instanceMethod // 메소드 참조로 표현
```

아래 예제에서 a.compareToIgnoreCase(b)로 호출될 때 사전 순으로 a가 b보다 먼저 오면 음수를, 동일하면 0을, 나중에 오면 양수를 리턴합니다. 사용된 함수적 인터페이스는 두 String 매개값을 받고 int 값을 리턴하는 `ToIntBiFunction<String, String>`입니다.

#### 예제 - 두 문자열이 대소문자와 상관없이 동일한 알파벳인지 비교

```java
import java.util.function.ToIntBiFunction;

public class Main {
    public static void main(String[] args) {
        ToIntBiFunction<String, String> function;

        function = (a, b) -> a.compareToIgnoreCase(b);
        print(function.applyAsInt("Java", "JAVA"));

        function = String::compareToIgnoreCase;
        print(function.applyAsInt("Java", "JAVA"));
    }

    public static void print(int order) {
        if (order<0) {
            System.out.println("사전순으로 먼저 옵니다.");
        } else if (order==0) {
            System.out.println("동일한 문자열입니다.");
        } else {
            System.out.println("사전순으로 나중에 옵니다.");
        }
    }
}
```

<br>

### 생성자 참조
메소드 참조는 생성자 참조도 포함합니다. 생성자를 참조한다는 것은 객체 생성을 의미하는데, 단순히 메소드 호출로 구성된 람다식을 메소드 참조로 대치할 수 있듯이, 단순히 객체를 생성하고 리턴하도록 구성된 람다식은 생성자 참조로 대치할 수 있습니다.

```java
(a, b) -> {return new 클래스(a, b);}
```

클래스 이름 뒤에 `::` 기호를 붙이고 new 연산자를 작성하면 생성자 참조가 됩니다. 생성자가 오버로딩되어 여러 개 있을 경우, 컴파일러는 함수적 인터페이스의 추상 메소드와 동일한 매개 변수 타입과 개수를 가지고 있는 생성자를 찾아 실행합니다.

```java
클래스 :: new
```

#### 예제

```java
// Member.java
public class Member {
	private String name;
	private String id;

	public Member() {
		System.out.println("Member() 실행");
	}
	public Member(String id) {
		System.out.println("Member(String id) 실행");
		this.id = id;
	}
	public Member(String name, String id) {
		System.out.println("Member(String name, String id) 실행");
		this.name = name;
		this.id = id;
	}

	public String getId() { 
		return id;
	}
}

// Main.java
import java.util.function.BiFunction;
import java.util.function.Fuction;

public class ConstructorReferencesExample {
	public static void main(String[] args) {
		Function<String, Member> function1 = Member :: new;
		Member member1 = function1.apply("jack");

		BiFunction<String, String, Member> function2 = Member :: new;
		Member member2 = function2.apply("elon", "jack");
	}
}
```

<br>

## 레퍼런스
- 이것이 자바다: 신용권의 Java 프로그래밍 정복
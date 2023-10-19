# 람다식
* 람다식의 도입으로 인해, 자바는 객체지향언어인 동시에 함수형 언어가 되었다
## 람다식이란?
* 람다식(Lambda expression)은 간단히 말해서 메서드를 하나의 '식(expression)'으로 표현한 것이다
  * 람다식은 함수를 간략하면서도 명확한 식으로 표현할 수 있게 해준다
* 메서드를 람다식으로 표현함녀 메서드의 이름과 반호나값이 없어지므로, 람다식을 '익명 함수(anonymous function)'이라고도 한다
```java
int[] arr = new int[5];
Arrays.setAll(arr, (i) -> (int)(Math.random()*5)+1);
```
* '() -> (int)(Math.random()*5)+1'이 람다식이다
* 이 람다식이 하는 일을 메서드로 표현하면 아래 코드임!
```java
int method() {
    return (int) (Math.random()*5) + 1;
        }
```
* 람다식이 간결하면서도 이해하기 쉽다
  * 게다가 모든 메서드는 클래스에 포함되어야 하므로 클래스도 새로 마들어야 하고, 객체도 생성해야만 비로소 이 메서드를 호출할 수 있다
    * 그러나 람다식은 이 모든 과정없이 오직 람다식 자체만으로도 이 메서드의 역할을 대신할 수 있다
* 람다식은 메서드의 매개변수로 전달되어지는 것이 가능하고, 메서드의 결과로 변환될 수도 있다
  * 람다식으로 인해 메서드를 변수처럼 다루는 것이 가능해진 것이다
```java
Q. 메서드와 함수의 차이가 뭐죠?

A. 전통적으로 프로그래밍에서 함수라는 이름은 수학에서 따온 것입니다. 수학의 함수와 개념이 유사하기 때문이죠.
        그러나 객체지향개념에서는 함수(function)대신 객체의 행위나 동작을 의미하는 메서드(method)라는 용어를 사용합니다. 
        메서드는 함수와 같은 의미이지만, 특정 클래스에 반드시 속해야 한다는 제약이 있기 때문에 기존의 함수와 같은 의미의 다른 용어를 선택해서 사용한 것입니다. 그러나 이제 다시 람다식을 통해 메서드가 하나의 독립적인 기능을 하기 때문에 함수라는 용어를 사용하게 되었습니다.

```
## 람다식 작성하기
* 람다식은 '익명 함수' 답게 메서드에서 이름과 반환타입을 제거하고 매개변수 선언부와 몸통{} 사이에 '->'를 추가한다
```java
반환타입 메서드이름(매개변수 선언) {
    문장들
        }
        ->
~~반환타입 메서드이름~~ (매개변수 선언) -> {
    문장들
        }
```
* 두 값 중에서 큰 값을 반환하는 max를 람다식으로 변환
```java
int max(int a, int b) {
    return a > b ? a : b;
        }
```
-> 
```java
(int a, int b) -> {
    return a > b ? a : b;
        }
```
* 반환값이 있는 메서드의 경우, return문 대신 '식(experession)'으로 대신할 수 있다
  * 식의 연산결과가 자동적으로 반환값이 된다
    * 이때는 '문장(statement'이 아닌 '식'이므로 끝에 ';'을 붙이지 않는다
```java
(int a, int b) -> { return a > b ? a : b; }
```
-> 
```java
(int a, int b) -> a > b ? a: b;
```
* 람다식에 선언된 매개변수의 타입은 추론이 가능한 경우는 생략할 수 있는데, 대부분의 경우에 생략가능하다
  * 람다식에 반환타입이 없는 이유도 항상 추론이 가능하기 때문이다
```java
(int a, int b) -> a> b ? a : b
```
-> 
```java
(a, b) -> a > b ? a : b
```
* 두 매개변수 중 어느 하나의 타입만 생략하는 것은 허용되지 않는다
* 선언된 매개변수가 하나뿐인 경우에는 괄호()를 생략할 수 있다
  * 단, 매개변수의 타입이 있으면 괄호()를 생략할 수 없다
```java
(a) -> a * a
(int a) -> a * a
```
->
```java
a -> a * a // OK
int a -> a * a // 에러!
```
* 괄호{} 안에 문장이 하나일 때 는 괄호{}를 생략할 수 있다
  * 이때 문장의 끝에 ';'를 붙이지 않아야 한다
```java
(String name, int i) -> {
    System.out.println(name+"="+i);
        }
```
-> 
```java
(String name, int i) ->
    System.out.println(name+"="+i)
```
* 그러나 괄호{} 안의 문장이 return문일 경우 괄호{}를 생략할 수 없다
```java
(int a, int b) -> { return a > b ? a : b; } // OK
(int a, int b) -> return a > b ? a : b // 에러
```
| 일반 메서드                             | 람다식                            |
|------------------------------------|--------------------------------|
| ```java                            | ```java                         |
| public void printSomething() {     | () -> System.out.println("Hello!"); |
|     System.out.println("Hello!");  |                                |
| }                                  |                                |
| ```                                | ```                             |
|                                    |                                |
| ```java                            | ```java                         |
| public int add(int a, int b) {     | (a, b) -> a + b;                |
|     return a + b;                  |                                |
| }                                  |                                |
| ```                                | ```                             |
|                                    |                                |
| ```java                            | ```java                         |
| public boolean isEven(int number) {| number -> number % 2 == 0;     |
|     return number % 2 == 0;       |                                |
| }                                  |                                |
| ```                                | ```                             |
* [메서드를 람다식으로 변환한 예]
## 함수형 인터페이스(Functional Interface)
* 람다식은 익명 클래스의 객체와 동등하다
```java
(int a, int b) -> a > b ? a : b
```
-> 
```java
new Object() {
    int max(int a, int b) {
        return a > b ? a : b;
        }
}
```
* 참조변수가 있어야 객체의 메서드를 호출할 수 있으니까 일단 이 익명 객체의 주소를 f라인 참조변수에 저장!
```java
타입 f = (int a, int b) -> a > b ? a : b; // 참조변수의 타입을 뭘로 해야할까?
```
* 참조형이니까 클래스 또는 인터페이스가 가능하다
  * 그리고 람다식과 동등한 메서드가 정의되어 있는 것이어야 한다
    * 그래야만 참조변수로 익명 객체(람다식)의 메서드를 호출할 수 있기 때문이다
* max()라는 메서드가 정의된 MyFunction인터페이스가 정의되어 있다고 가정
```java
interface MyFunction {
    punlic abstract int max(int a, int b);
}
```
* 그럼 이 인터페이스를 구현한 익명 클래스의 객체는
```java
MyFunction f = new MyFunction() {
    public  int max(int a, int b) {
        return a > b ? a : b;
        }
};

int biv = f.max(5, 3); // 익명 객체의 메서드를 호출
```
이렇게 생성된다
* MyFunction인터페이스에 정의된 메서드 max()는 람다식 '(int a, int b) -> a > b ? a : b'과 메서드의 선언부가 일치한다
  * 그래서 위 코드의 익명 객체를 람다식으로 아래와 같이 대체할 수 있다
```java
MyFuction f = (int a, int b) -> a > b ? a : b; // 익명 객체를 람다식으로 대체
int big = f.max(5, 3); // 익명 객체의 메서드를 호출
```
* 이처럼 MyFunction인터페이스를 구혀한 익명 객체를 람다식으로 대체가 가능한 이유는, 람다식도 실제로는 익명 객체이고, MyFunction인터페이스를 구혀한 익명 객체의 메서드 max()와 람다식의 매개변수의 타입과 개수 그리고 반환값이 일치하기 때문이다

## java.util.function 패키지
* 이 패키지는 자바 8에서 추가된 함수형 인터페이스를 포함하고 있습니다
  * 대표적인 예로는 `Function`, `Predicate`, `Consumer`, `Supplier` 등이 있습니다

### Function의 합성
* `Function` 인터페이스에는 `andThen` 및 `compose` 두 가지 합성 메서드가 있습니다
  - `andThen`: 주어진 함수 뒤에 이 함수를 실행
  - `compose`: 주어진 함수 앞에 이 함수를 실행

```java
Function<Integer, Integer> multiply2 = x -> x * 2;
Function<Integer, Integer> add3 = x -> x + 3;

Integer result1 = multiply2.andThen(add3).apply(3);  // 9 (3*2 + 3)
Integer result2 = multiply2.compose(add3).apply(3);  // 12 (3+3) * 2
```

### Predicate의 결합
* `Predicate` 인터페이스는 `and`, `or`, `negate` 등의 논리 조합 메서드를 제공합니다

```java
Predicate<Integer> isEven = x -> x % 2 == 0;
Predicate<Integer> isGreaterThan5 = x -> x > 5;

boolean result = isEven.and(isGreaterThan5).test(8);  // true
```

### 메서드 참조
* 메서드 참조는 람다 표현식의 짧은 형식으로, 특정 메서드를 직접 참조할 때 사용됩니다

```java
List<String> names = Arrays.asList("Anna", "Bob", "Charlie");
names.forEach(System.out::println);
```

# 스트림(Stream)

### 스트림이란?
* 스트림은 데이터의 흐름을 나타내는 추상화된 개념입니다
  * 자바 8에서는 컬렉션의 데이터를 처리하거나 다양한 데이터 소스에서 데이터를 처리하는 데 사용됩니다

### 스트림 만들기
```java
Stream<String> namesStream = Stream.of("Anna", "Bob", "Charlie");
Stream<Integer> numbersStream = Arrays.stream(new Integer[]{1, 2, 3});
```

### 스트림의 중간연산
* 중간 연산은 스트림에 연산을 적용하지만, 스트림을 종료하지 않습니다.
  * `filter`, `map`, `distinct`, `sorted` 등이 있습니다

```java
Stream<String> filteredNames = namesStream.filter(name -> name.startsWith("A"));
```

### Optional<T>와 OptionalInt
* `Optional`은 값이 있거나 없을 수 있는 컨테이너 객체입니다
  * `OptionalInt`는 기본 int 타입의 특화된 버전입니다

```java
Optional<String> optionalName = namesStream.findFirst();
```

### 스트림의 최종연산
* 스트림을 종료하고 결과를 반환합니다
  * `collect`, `forEach`, `reduce`, `count` 등이 있습니다

### collect()
* `collect`는 스트림의 결과를 다양한 형태의 컬렉션으로 반환합니다
```java
List<String> nameList = namesStream.collect(Collectors.toList());
```

### Collector 구현하기
* `Collector` 인터페이스를 구현하여 사용자 정의 수집 연산을 만들 수 있습니다

### 스트림의 변환
* 스트림은 다른 타입의 스트림으로 변환될 수 있습니다
  * 예를 들어, `map`을 사용하여 스트림의 각 요소를 변환할 수 있습니다

```java
Stream<Integer> nameLengths = namesStream.map(String::length);
```
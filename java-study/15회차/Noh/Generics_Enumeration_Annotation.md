# 지네릭스(Generics)

## 지네릭스란?
* 지네릭스는 다양한 타입의 객체들을 다루는 메서드나 컬렉션 클래스에 컴파일 시의 타입체크(compile-time type check)를 해주는 기능이다
  * 객체의 타입을 컴파일 시에 체크하기 때문에 객체의 타입 안정성을 높이고 형변환의 번거로움이 줄어든다
    * 타입 안정성을 높인다는 것은 의도하지 않은 타입의 객체가 저장되는 것을 막고, 저장된 객체를 꺼내올 때 원래의 타입과 다른 타입으로 잘못 형변환되어 발생할 수 있는 오류를 줄여준다는 뜻이다
* ex) ArrayList와 같은 컬렉션 클래스는 다양한 종류의 객체를 담을 수 있긴 하지만 보통 한 종류의 객체를 담는 겨우가 더 많다 <br>
-> 그런데도 꺼낼 때 마다 타입체크를 하고 형변환을 하는 것은 아무래도 불편할 수 밖에 없다, 게다가 원하는 않는 종류의 객체가 포함되는 것을 막을 방법이 없다는 것도 문제다 <br>
-> 지네릭스가 해결해준다
```java
지네릭스의 장점
1. 타입 안정성을 제공한다
2. 타입체크와 형변환을 생략할 수 있으므로 코드가 간결해진다
```
* 다룰 객체의 타입을 미리 명시해줌으로써 번거로운 형변환을 줄여준다

## 지네릭 클래스의 선언
* 지네릭 타입은 클래스와 메서드에 선언할 수 있다
* 클래스에 선언하는 지네릭 타입
```java
class Box {
    Object item;
    
    void setItem(Object item) { this.item = item; }
    Object getItem() { return item; }
}
```
* 클래스 Box
```java
class Box<T> { // 지네릭 타입 T를 선언
    T item;
    
    void setItem(T item) { this.item = item; }
    T getItem() { return item; }
}
```
* Box 클래스를 지네릭 클래스로 변경하면 클래스 옆에 <T>를 붙이면 된다
  * 그리고 Object를 모두 T로 바꾼다

* Box<T>에서 T를 '타입 변수(type variable'라고 하며, 'Type'의 첫 글자에서 따온 것이다
  * 타입 변수는 T가 아닌 다른 것을 사용해도 된다
* ArrayList<E>의 경우, 타입 변수 E는 'Element(요소)'의 첫 글자를 따서 사용했다
* 타입 변수가 여러 개인 경우에는 Map<K, V>와 같이 콤마 ','를 구분자로 나열하면 된다
  * k는 Key(키)를 의미하고, V는 Value(값)을 의미한다
    * 무조건 'T'를 사용하기보다 가능하면, 상황에 맞게 의미있는 문자를 사용하는 것이 좋다 <br>
**이들은 기호의 종류만 다를 뿐 '임의의 참조형 타입'을 의미한다는 것은 모두 같다**

* 지네릭 클래스가 된 Box클래스의 객체를 생성할 때는 참조변수와 생성자에 타입 T대신에 사용될 실제 타입을 지정해주어야 한다
```markdown
Box<String> b = new Box<String>(); // 타입 T 대신, 실제 타입을 지정
b.setItem(new Object()); // 에러! String이외의 타입은 지정불가
b.setItem("ABC"); // String 타입이므로 가능
String item = ~~(Stirng)~~ b.getItem(); // 형변환이 필요없음
```
* T 대신 String 타입을 지정해줌
```java
class Box { // 지네릭 타입을 String으로 지정
    String item;
    
    void setItem(String item) { this.item = item; }
    String getItem() { return item; }
}
```
* 지네릭 클래스 Box<T>는 위와 같이 정의된 것과 같다

### 지네릭스의 용어
```java
class Box<T> {}
```
```java
Box<T> : 지네릭 클래스. 'T의 Box' 또는 'T Box'라고 읽는다
T : 타입 변수 또는 타입 매개변수(T는 타입 문자)
Box : 원시 타입(raw type)
```
### 지네릭스의 제한
* 지네릭 클래스 Box의 객체를 생성할 때, 객체별로 다른 타입을 지정하는 것은 적절하다
  * 지네릭스는 인스턴스별로 다르게 동작하도록 하려고 만든 기능이니까!
```java
Box<Apple> appleBox = new Box<Apple>(); // Apple객체만 저장가능
Box<Grape> grapeBox = new Box<Grape>(); // Grape객체만 저장가능
```
* 모든 객체에 대해 동일하게 동작해야하는 static멤버에 타입 변수 T를 사용할 수 없다
  * T는 인스턴스 변수로 간주되기 때문이다
    * static멤버는 인스턴스변수를 참조할 수 없다
```java
class Box<T> {
    static T item; // 에러!
    static int compare(T t1, T t2) { ... } // 에러
        ...
}
```
## 지네릭 클래스의 객체 생성과 사용
* 지네릭 클래스 Box<T>가 정의되어 있다고 가정
  * 이 Box<T>의 객체에는 한 가지 종류, 즉 T타입의 객체만 저장할 수 있다
    * ArrayList를 이용해서 여러 객체를 저장할 수 있도록 하였다

```java
import java.util.ArrayList;

class Box<T> {
    ArrayList<T> list = new ArrayList<>(T)();
    
    void add(T item) { list.add(item); }
    T get(int i) { return list.get(i); }
    ArrayList<T> getList() { return list; }
    int size() { return list.size(); }
    public String toString() { return list.toString(); }
}
```
* Box<T>의 객체를 생성할 때는 참조변수와 생성자에 대입된 타입(매개 변수화된 타입)이 일치해야 한다
```java
Box<Apple> appleBox = new Box<Apple>(); // OK
Box<Apple> appleBox = new Box<Grape>(); // 에러
```
* 두 타입이 상속관계에 있어도 마찬가지!
```java
// Apple이 Fruit의 자손이라고 가정

Box<Fruit> appleBox = new Box<Apple>; // 에러, 대입된 타입이 다르다
```
* 단, 두 지네릭 클래스의 타입이 상속관계에 있고, 대입된 타입이 같은 것은 괜찮다
```java
// FruitBox는 Box의 자손이라고 가정

Box<Apple> appleBox = new FruitBox<Apple>(); // OK, 다형성
```
* JDK1.7부터는 추정이 가능한 경우 타입을 생략할 수 있게 되었다
  * 참조변수의 타입으로부터 Box가 Apple타입의 객체만 저장한다는 것을 알 수 있기 때문에, 생성자에 반복해서 타입을 지정해주지 않아도 되는 것이다
```java
Box<Apple> appleBox = new Box<Apple>();
Box<Apple> appleBox = new Box<>(); // OK, JDK1.7부터 생략가능
```
* 생성된 Box<T>의 객체에 'void add(T item)'으로 객체를 추가할 때, 대입된 타입과 다른 타입의 객체는 추가할 수 없다
```java
Box<Apple> appleBox = new Box<Apple>();
appleBox.add(new Apple()); // OK
appleBox.add(new Grape()); // 에러, Box<Apple>에는 Apple객체만 추가가능
```
* 타입 T가 'Fruit'인 경우, 'void add(Fruit item)'가 되므로 Fruit의 자손들은 이 메서드의 매개변수가 될 수 있다
```java
// Apple이 Fruit의 자손이라고 가정

Box<Fruit> fruitBox = new Box<Fruit>();
fruitBox.add(new Fruit()); // OK
fruitBox.add(new Apple()); // OK, void add(Fruit item)
```
### 제한된 지네릭 클래스
* 타입 문자로 사용할 타입을 명시하면 한 종류의 타입만 저장할 수 있도록 제한할 수 있지만, 그래도 여전히 모든 종류의 타입을 지정할 수 있다는 것에는 변함이 없다
* 그렇다면, 타입 매개변수 T에 지정할 수 있는 타입의 종류를 제한할 수 있는 방법은?!?!
```java
FruitBox<Toy> fruitBox = new FruitBox<Toy>();
fruitBox.add(new Toy()); // OK, 과일상자에 장난감을 담을 수 있다
```
* 지네릭 타입에 'extends'를 사용하면, 특정 타입의 자손들만 대입할 수 있게 제한할 수 있다

```java
import java.util.ArrayList;

class FruitBox<T extends Fruit> { // Fruit의 자손만 타입으로 지정가능
    ArrayList<T> list = new ArrayList<T>();
  ...
}
```
* 여전히 한 종류의 타입만 담을 수 있지만, Fruit클래스의 자손들만 담을 수 있다는 제한이 더 추가된 것이다
```java
FruitBox<Apple> appleBox = new FruitBox<Apple>(); // OK
FruitBox<Toy> toyBox = new FruitBox<Toy>(); // 에러, Toy는 Fruit의 자손이 아님
```
* 게다가 add()의 매개변수의 타입 T도 Fruit와 그 자손 타입이 될 수 있다
```java
FruitBox<Fruit> fruitBox = new FruitBox<Fruit>(); // OK
fruitBox.add(new Apple()); // OK, Apple이 Fruit의 자손
fruitBox.add(new Grape()); // OK, Grape가 Fruit의 자손
```
* 다형성에서 조상타입의 참조변수로 자손타입의 객체를 가리킬 수 있는 것처럼, 매개변수화된 타입의 자손 타입도 가능한 것이다
* 타입 매개변수 T에 Object를 대입하면, 모든 종류의 객체를 저장할 수 있게 된다

* 만일 클래스가 아니라 인터페이스를 구현해야 한다는 제약이 필요하다면, 이때도 'extends'를 사용한다
  * 'implements'를 사용하지 않는다는 점에 주의!
```java
interface Eatable {}
class FruitBox<T extends Eatable> { ... }
```
* 클래스 Fruit의 자손이면서 Eatable인터페이스도 구현해야한다면 '&' 기호로 연결한다
```java
class FruitBox<T extends Fruit & Eatable> { ... }
```
* FruitBox에는 Fruit의 자손이면서 Eatable을 구현한 클래스만 타입 매개변수 T에 대입될 수 있다
### 와일드 카드
* 와일드 카드(`?`)는 모든 지네릭 타입을 대신할 수 있는 특별한 타입입니다
  * 와일드 카드는 유연한 매개변수로 메서드를 작성할 때 사용됩니다
```java
<? extends T> : 와일드 카드의 상한 제한, T와 그 자손들만 가능
<? super T> : 와일드 카드의 하한 제한, T와 그 조상들만 가능
<?> : 제한 없음, 모든 타입이 가능, <? extends Object>와 동일
```
* 지네릭 클래스와 달리 와일드 카드에는 '&'를 사용할 수 없다
  * 즉, <? extends T & E>와 같이 할 수 없다
```java
public void printList(List<?> list) {
    for (Object o : list) {
        System.out.println(o);
    }
}
```

### 지네릭 메서드
* 지네릭 메서드는 메서드 내에서 사용되는 데이터 타입을 파라미터로 지정할 수 있는 메서드입니다

```java
public <T> T exampleMethod(T t) {
    // ...
    return t;
}
```

### 지네릭 타입의 형변환
* 지네릭 타입에서 다른 타입으로 형변환을 할 때, 원시 타입으로 형변환하는 것은 피해야 합니다
  * 대신, 와일드 카드나 instanceof 연산자를 사용하여 안전한 형변환을 진행해야 합니다

# 열거형 (Enums)
**열거형**은 명명된 상수의 집합을 나타내는 데이터 타입입니다
* 열거형은 주로 관련된 상수를 그룹화하고 명명하는 데 사용됩니다

### 열거형이란?

```java
enum Day {
    SUNDAY, MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY, SATURDAY
}
```

### 열거형의 정의와 사용

```java
Day today = Day.MONDAY;
if (today == Day.MONDAY) {
    System.out.println("Today is Monday.");
}
```

### 열거형에 멤버 추가하기
* 열거형에 멤버를 추가할 수 있습니다
  * 각 멤버는 세미콜론(`;`)으로 끝나야 합니다

```java
enum Color {
    RED, GREEN, BLUE
}
```

# 애너테이션 (Annotations)
**애너테이션**은 메타데이터를 소스 코드에 추가하여 컴파일러와 다른 도구가 코드에 대한 정보를 처리하도록 지시합니다

## 애너테이션이란?
애너테이션은 다음과 같이 정의합니다:

```java
@interface MyAnnotation {
    String value() default "default value";
}
```

### 표준 애너테이션
* 자바에서는 다양한 표준 애너테이션을 제공합니다 
  * `@Override`, `@Deprecated`, `@SuppressWarnings` 등이 있습니다

### 메타 애너테이션
* 메타 애너테이션은 다른 애너테이션을 위한 애너테이션으로, 커스텀 애너테이션을 정의할 때 사용됩니다

```java
@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.METHOD)
@interface MyCustomAnnotation {
    String value();
}
```
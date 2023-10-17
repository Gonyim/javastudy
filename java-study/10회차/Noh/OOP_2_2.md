# 객체 지향 프로그래밍

## 추상클래스(abstract class)
### 추상클래스란?
* 미완성 클래스 / 완성되지 못한 채 남겨진 클래스
* 미완성이라는 것은 멤버의 개수에 관계된 것이 아니라, 단지 미완성 메서드(추상메서드)를 포함하고 있다는 의미이다
* 추상클래스로 인스턴스는 생성할 수 없다
  * 추상클래스는 상속을 통해서 자손클래스에 의해서만 완성될 수 있다
* 추상클래스 자체로는 클래스로서의 역할을 다 못 하지만, 새로운 클래스를 작성하는데 있어서 바탕이 되는 조상클래스로서 중요한 의미를 갖는다
```java
abstract class 클래스이름 {
    ...
}
```
* 추상클래스는 키워드 'abstract'를 붙이기만 하면된다
  * 이 클래스를 사용할 때, 클래스 선언부의 abstract를 보고 이 클래스에는 추상메서드가 있으니 상속을 통해서 구현해주어야 한다는 것을 알 수 있을 것이다
  * 추상클래스에도 생성자가 있으며, 멤버변수와 메서드도 가질 수 있다
### 추상메서드 (abstract method)
* 메서드는 선언부와 구현부로 구성되어 있다
  * 선언부만 작성하고 구현부는 작성하지 않은 채로 남겨 둔 것이 추상메서드이다
    * 즉, 설계만 해놓고 실제 수행될 내용은 작성하지 않았기 때문에 미완성 메서드인 것이다
* 메서드를 미완성 상태로 남겨 놓는 이유
  * 메서드의 내용이 상속받는 클래스에 따라 달라질 수 있기 때문에 조상 클래스에서는 선언부만을 작성하고, 주석을 덧붙여 어떤 기능을 수행할 목적으로 작성되었는 지 알려 주고, 실제 내용은 상속받는 클래스에서 구현하도록 비워두는 것이다
    * 그래서 추상클래스를 상속받는 자손 클래스는 조상의 추상 메서드를 상황에 맞게 적절히 구현해주어야 한다
```java
// 주석을 통해 어떤 기능을 수행할 목적으로 작성하였는 지 설명한다
abstract 리턴타입 메서드이름();
```
* 키워드 abstract를 앞에 붙여 주고, 추상메서드는 구현부가 없으므로 괄호{}대신 문장의 끝을 알리는 ';'을 적어준다
```java
abstract class Player { // 추상클래스
    abstract  void play(int pos); // 추상메서드 
    abstract  void stop(); // 추상메서드
}
class AudioPlayer extends Player {
    void play(int pos) { /* 내용생략 */ } // 추상메서드를 구현
    void stop() { /* 내용 생략 */ } // 추상메서드를 구현
}
abstract class AbstractPlayer extends Player {
    void play(int pos) { /* 내용 생략 */ } // 추상메서드를 구현
}
```
* 추상클래스로부터 상속받는 자손클래스는 오버라이딩을 통해 조상인 추상클래스의 추상메서드를 모두 구현해줘야한다
  * 조상으로부터 상속받은 추상메서드 중 하나라도 구현하지 않는다면, 자손클래스 역시 추상클래스로 지정해줘야한다

### 추상클래스의 작성
* 추상화는 기존의 클래스의 공통부분을 뽑아내서 조상 클래스를 만드는 것이라고 할 수 있다
* 추상화를 구체화와 반대되는 의미로 이해하면 보다 쉽게 이해할 수 있다
  * 상속계층도를 따라 내려갈수록 클래스는 점점 기능이 추가되어 구체화의 정도가 심해지며, 상속 계층도를 따라 올라갈수록 클래스는 추상화의 정도가 심해진다고 할 수 있다
    * 즉, 상속계층도를 따라 내려 갈수록 세분화되며, 올라갈수록 공통요소만 남게 된다

<img width="300" alt="image" src="https://github.com/nohheeyeon/TIL/assets/130336617/71bda9bb-7e1e-41e0-8815-f6774bfb61ee"> <br>

```java
// 추상 클래스 Animal
abstract class Animal {
    // 추상 메서드 speak 선언
    abstract void speak();
}

// 추상 클래스 Animal을 상속받은 구체 클래스 Dog
class Dog extends Animal {
    @Override
    void speak() {
        System.out.println("멍멍!");
    }
}

// 추상 클래스 Animal을 상속받은 구체 클래스 Cat
class Cat extends Animal {
    @Override
    void speak() {
        System.out.println("야옹!");
    }
}

public class AbstractClassExample {
    public static void main(String[] args) {
        Animal dog = new Dog();
        Animal cat = new Cat();

        dog.speak(); // "멍멍!" 출력
        cat.speak(); // "야옹!" 출력
    }
}
```

## 인터페이스(interface)
### 인터페이스란?
* 일종의 추상클래스다
* 인터페이스는 추상클래스처럼 추상메서드를 갖지만 추상클래스보다 추상화 정도가 높아서 추상클래스와 달리 몸통을 갖춘 일반 메서드 또는 멤버변수를 구성원으로 가질 수 없다
  * 오직 추상메서드와 상수만을 멤버로 가질 수 있으며, 그 외의 다른 어떠한 요소도 허용하지 않는다
* 인터페이스는 구현된 것은 아무 것도 없고 밑그림만 그려져 있는 '기본 설계도'라 할 수 있다
* 인터페이스도 추상클래스처럼 완성되지 않은 불완전한 것이기 때문에 그 자체만으로 사용되기 보다는 다른 클래스를 작성하는데 도움 줄 목적으로 작성된다

### 인터페이스의 작성
* 키워드로 interface를 사용
* interface에도 클래스와 같이 접근제어자로 public 또는 default를 사용할 수 있다

<!-- 왜 public과 default만 접근제어자로 사용 가능한 거지 -->

```java
interface 인터페이스이름 {
    public static rfinal 타입 상수이름 = 값;
    public abstract 메서드이름(매개변수목록);
}
```
* 일반적인 클래스의 멤버들과 달리 인터페이스의 멤버들이 가지고 있는 제약사항
```java
- 모든 멤버변수는 public static final 이어야 하며, 이를 생략할 수 있다
- 모든 메서드는 public abstract 이어야 하며,  이를 생략할 수 있다
```
-> 인터페이스에 정의된 모든 멤버에 예외없이 적용되는 사항이기 때문에 제어자를 생략할 수 있는 것이며, 편의상 생략하는 경우가 많다 <br>
-> 생략된 제어자는 컴파일 시에 컴파일러가 자동으로 추가해준다

### 인터페이스의 상속
* 인터페이스는 인터페이스로부터만 상속받을 수 있으며, 클래스와는 달리 다중상속, 즉 여러 개의 인터페이스로부터 상속을 받는 것이 가능하다
* 인터페이스는 클래스와 달리 Object클래스와 같은 최고 조상이 없다
<!-- 왜 -->
```java
interface Movable {
    /** 지정된 위치 (x, y)로 이동하는 기능의 메서드 */
    void move(int x, int y);
}
interface Attackable {
    /** 지정된 대상(u)을 공격하는 기능의 메서드 */
    void attact(Unit u);
}

interface Fightable extends Movable, Attackable { }
```
* 클래스의 상속과 마찬가지로 자손 인터페이스(Fightable)는 조상 인터페이스(Moveable, Attackable)에 정의된 멤버를 모두 상속받는다

### 인터페이스의 구현
* 인터페이스도 추상클래스처럼 그 자체로는 인스턴스를 생성할 수 없으며, 추상클래스가 상속을 통해 추상메서드를 완성하는 것처럼, 인터페이스도 자신에 정의된 추상메서드의 몸통을 만들어주는 클래스를 작성해야 하는데, 그 방법은 추상클래스가 자신을 상속받는 클래스를 정의하는 것과 다르지않다
  * But! 클래스는 확장한다는 의미의 키워드 'extends'를 사용하지만 인터페이스를 구현한다는 의미의 키워드 'implements'를 사용한다
```java
class 클래스이름 implements 인터페이스이름 {
    // 인터페이스에 정의된 추상메서드를 구현해야 한다
}

class Fighter implements Fightable {
    public void move(int x, int y) { ... }
    public void attack(Unit u) { ... }
}
```
-> 'Fighter클래스는 Fightable인터페이스를 구현한다.'라고 한다
* 만일 구현하는 인터페이스의 메서드 중 일부만 구현한다면, abstract를 붙여서 추상클래스로 선언해야 한다
```java
abstract class Fighter implements Fightable {
    public void move(int x, int y) { ... }
}
```
* 상속과 구현을 동시에 할 수도 있다
```java
class Fighter extends Unit implements Fightable {
    public void move(int x, int y) { ... }
    public void attack(Unit u) { ... }
}
```

### 인터페이스를 이용한 다중상속

```java
// 인터페이스 Animal 정의
interface Animal {
    void makeSound();
}

// 강아지를 나타내는 Dog 클래스
class Dog implements Animal {
    @Override
    public void makeSound() {
        System.out.println("멍멍!");
    }
}

// 고양이를 나타내는 Cat 클래스
class Cat implements Animal {
    @Override
    public void makeSound() {
        System.out.println("냥냥!");
    }
}

public class AnimalExample {
    public static void main(String[] args) {
        Animal dog = new Dog();
        Animal cat = new Cat();

        dog.makeSound();  // "멍멍!" 출력
        cat.makeSound();  // "냥냥!" 출력
    }
}
```
* Animal 인터페이스를 구현한 Dog 클래스와 Cat 클래스가 각각 makeSound() 메서드를 구현하고 있다
  * 이 두 클래스는 인터페이스를 통해 다중 상속을 구현하고, main 메서드에서 Animal 인터페이스를 참조 변수로 사용하여 강아지와 고양이의 소리를 출력합니다

### 인터페이스를 이용한 다형성
### 인터페이스의 장점
```java
- 개발시간을 단축시킬 수 있다
- 표준화가 가능하다
-서로 관계없는 클래스들에게 관계를 맺어줄 수 있다
- 독립적인 프로그래밍이 가능하다
```
### 인터페이스의 이해
### 디폴트 메서드와 static메서드
* 자바를 보다 쉽게 배울 수 있도록 규칙을 단순히 할 필요가 있어서 인터페이스의 모든 메서드는 추상 메서드이어야 한다는 규칙에 예외를 두지 않았다
  * 인터페이스와 관련된 static메서드는 별도의 클래스에 따로 두어야 했다
* 가장 대표적인 것 : java.util.Collection인터페이스
  * 이 인터페이스와 관련된 static메서드들이 인터페이스에는 추상 메서드만 선언할 수 있다는 원칙 때문에 별도의 클래스, Collections라는 클래스에 들어가게 되었다
  * 인터페이스 static메서드를 추가할 수 있었다면, Collections클래스는 존재하지 않았을 것이다
    * 인터페이스의 static메서드 역시 접근 제어자가 항상 public이며, 생략할 수 있다
#### 디폴트 메서드
* 새로 추가된 디폴트 메서드가 기존의 메서드와 이름이 중복되어 충돌하는 경우가 발생했을 때. 해결하는 규칙.
```java
1. 여러 인터페이스의 디폴트 메서드 간의 충돌
    - 인터페이스를 구현한 클래스에서 디폴트 메서들르 오버라이딩해야 한다
2. 디폴트 메서드와 조상 클래스의 메서드 간의 충돌
     - 조상 클래스의 메서드가 상속되고, 디폴트 메서드는 무시된다
```
## 내부 클래스(inner class)
### 내부 클래스란?
* 내부 클래스는 클래스 내에 선언된 클래스이다
  * 클래스에 다른 클래스를 선언하는 이유
    * 두 클래스가 서로 긴밀한 관계에 있기 때문
* 한 클래스를 다른 클래스의 내부 클래스로 선언하면 두 클래스의 멤버들 간에 서로 쉽게 접근할 수 있다는 장점과 외부에는 불필요한 클래스를 감춤으로써 코드의 복잡성을 줄일 수 있다는 장점을 얻을 수 있다
```java
내부 클래스의 장점
- 낸부 클래스에서 외부 클래스의 멤버들을 쉽게 접근할 수 있다
- 코드의 복잡성을 줄일 수 있다(캡슐화)
```
### 내부 클래스의 종류와 특징
* 내부 클래스의 종류는 변수의 선언위치에 따른 종류와 같다
  * 내부 클래스는 변수를 선언하는 것과 같은 위치에 선언할 수 있으며, 변수의 선언위치에 따라 인스턴스변수, 클래스변수(static변수), 지역변수로 구분되는 것과 같이 내부 클래스도 선언위치에 따라 구분된다

| 내부 클래스 종류                | 특징                                                                                   |
|--------------------------|----------------------------------------------------------------------------------------|
| 인스턴스 클래스(instance class) | 외부 클래스의 인스턴스와 연관된 객체를 생성하기 위한 클래스로, 외부 클래스의 인스턴스 필드와 메서드에 접근 가능합니다 |
| 스태틱 클래스(static class)    | 외부 클래스의 정적(static) 멤버와 관련된 클래스로, 외부 클래스의 정적 멤버에만 접근 가능합니다                |
| 지역 클래스(local class)      | 메서드 내부에서만 사용되는 클래스로, 해당 메서드 내부에서만 접근 가능하며 메서드의 지역 변수를 사용할 수 있습니다   |
| 익명 클래스(anonymous class)  | 이름 없이 선언되는 클래스로, 주로 인터페이스를 구현하거나 부모 클래스를 상속받는 익명 클래스로 사용됩니다        |

### 내부 클래스의 선언
```java
class Outer {
    int iv = 0;
    static int cv = 0;
    
    void myMethod() {
        int lv = 0;
    }
}
```
```java
class Outer {
    class InstanceInner {}
    static class StaticInner {}
  
    void myMethod() {
        class LocalInner {}
    }
}
```
* 외부 클래스(Outer)에 3개의 서로 다른 종류의 내부 클래스를 선언했다
* 내부 클래스의 선언위치에 따라 같은 선언위치의 변수와 동일한 유효범위(scope)와 접근성(accessibility)을 갖는다
### 내부 클래스의 제어자와 접근성
```java
class Outer {
    int iv = 0;
    static int cv = 0;
    
    void myMethod() {
        int lv = 0;
    }
}
```
```java
class Outer {
    private class InstanceInner {}
    protected static class StaticInner {}
  
    void myMethod() {
        class LocalInner {}
    }
}
```
* 인스턴스클래스와 스태틱 클래스는 외부 클래스의 멤버변수와 같은 위치에 선언되며, 또한 멤버변수와 같은 성질을 갖는다
  * 따라서 내부 클래스가 외부 클래스의 멤버와 같이 간주되고, 인스턴스 멤버와 static멤버 간의 규칙이 내부 클래스에도 똑같이 적용된다
* 내부 클래스도 클래스이기 때문에 abstract나 final과 같은 제어자를 사용할 수 있을 뿐만 아니라, 멤버변수들처럼 private, protected와 접근제어자도 사용이 가능하다
### 익명 클래스(anonymous class)
* 내부클래스들과는 달리 이름이 없다
* 클래스의 선언과 객체의 생성을 동시에 하기 때문에 단 한번만 사용될 수 있고 오직 하나의 객체만을 생성할 수 있는 일회용 클래스이다
```java
new 조상클래스이름() {
    // 멤버 선언
        }

new 구현인터페이스이름() {
    // 멤버 선언
        }
```
* 이름이 없기 때문에 생성자도 가질 수 없으며, 조상클래스의 이름이나 구현하고자 하는 인터페이스의 이름을 사용해서 정의하기 때문에 하나의 클래스로 상속받는 동시에 인터페이스를 구현하거나 둘 이상의 인터페이스를 구현할 수 없다
  * 오로지 단 하나의 클래스를 상속받거나 단 하나의 인터페이스만을 구현할 수 있다
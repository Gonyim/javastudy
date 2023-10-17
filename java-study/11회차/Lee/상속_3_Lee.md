# 5. 상속

## 메소드 오버라이딩
메소드 오버라이딩은 부모 클래스와 자식 클래스의 메소드 사이에 발생하는 관계로서, 부모 클래스에 선선된 메소드와 같은 이름, 같은 리턴 타입, 같은 매개 변수 리스트를 갖는 메소드를 자식 클래스에서 재작성하는 것이다.  
메소드 오버라이딩을 했을 때 외부에서나 내부에서 해당 메소드를 호출하면 부모 클래스의 메소드는 절대로 실행되지 않고 반드시 자식 클래스의 메소드가 실행된다.  
따라서 메소드 오버라이딩은 '부모 클래스 메소드 무시하기 혹은 덮어쓰기'로 표현할 수 있다.  
이런 처리를 **동적 바인딩**이라고 부르며, 메소드 오버라이딩은 동적 바인딩을 유발시킨다.

- 목적 : 다형성 실현
  - 오버라이딩은 부모 클래스에 선언된 메소드를, 각 자식 클래스들이 자신만의 내용으로 새로 구현하는 기능으로 '상속을 통해 하나의 인터페이스에 서로 다른 내용 구현'이라는 객체 지향의 다형성을 실현하는 도구이다.

- @Override
```java
class Shape {
    public void draw() {...}
}

class Line extends Shape {
    public void drow() {...}
}
```
위 코드에서는 Shape에 drow()가 없으므로 오버라이딩이 아닌 새로운 메소드가 작성된다.  
위와 같이 잘못 코딩했을 때 쉽게 발견하기 위해, @Override라는 주석문을 사용한다.  
@Override는 오버라이딩하는 메소드 앞에 붙이는 것으로 컴파일러에게 오버라이딩이 정확한지 확인하도록 지시한다.
```java
class Shape {
    public void draw() {...}
}

class Line extends Shape {
    @Override
    public void drow() {...}    // 컴파일 오류
}
```
***

### 메소드 오버라이딩의 제약 사항
메소드를 오버라이딩할 때 다음 조건을 지켜야 한다.
1. 부모 클래스의 메소드와 동일한 원형으로 작성한다
   - 부모 클래스의 메소드와 동일한 이름, 동일한 매개변수 타입과 개수, 동일한 리턴 타입을 갖는 메소드를 작성해야 한다.
2. 부모 클래스 메소드의 접근 지정자보다 접근의 범위를 좁혀 오버라이딩할 수 없다.
   - 접근 지정자는 public, protected, default, private 순으로 접근의 범위가 좁아진다. 부모 클래스에서 protected로 선언된 메소드는 자식 클래스에서 protected나 public으로만 오버라이딩할 수 있고 public으로 선언된 메소드는 자식 클래스에서 public으로만 오버라이딩할 수 있다.
3. static이나 private 또는 final로 선언된 메소드는 자식 클래스에서 오버라이딩할 수 없다.
***

### 동적 바인딩 : 오버라이딩된 메소드 호출
동적 바인딩은 실행할 메소드를 컴파일 시에 결정하지 않고 실행 시에 결정하는 것을 말하며, 자바에서는 동적 바인딩을 통한 오버라이딩된 메소드가 항상 실행되도록 보장한다.
```java
class Shape {
    protected String name;
    public void paint() {
        draw;
    }
    public void draw() {
        System.out.println("Shape");
    }
}
public class Circle extends Shape {
    @Override
    public void draw() {
        System.out.println("Circle");
    }
    public static void main(String [] args) {
        Shape b = new Circle();
        b.paint();
    }
}
```
paint()는 Circle에서 오버라이딩한 draw()를 호출

### 오버라이딩과 super 키워드
앞에서 봤듯이 동적 바인딩에 의해서 항상 자식 클래스에 오버라이딩한 메소드가 호출되었는데 부모 클래스의 메소드는 실행할 방법이 없는가?  
자식 클래스에서 super키워드를 사용하면 정적 바인딩을 통해 부모 클래스의 멤버에 접근할 수 있다.
```java
super.부모클래스의멤버
```
super를 이용하면 부모 클래스의 필드와 메소드 모두 이용가능하다.
```java
class Shape {
    protected String name;
    public void paint() {
        draw();
    }
    public void draw() {
        System.out.println(name);
    }
}
public class Circle extends Shape {
    protected String name;
    @Override
    public void draw() {
        name = "Circle";
        super.name = "Shape";
        super.draw();
        System.out.println(name);
    }
    public static void main(String[] args) {
        Shape b = new Circle();
        b.paint();
    }
}

실행 결과
Shape
Circle
```
***

※ 정리  
this, this(), super, super()의 차이점  
this와 super는 모두 레퍼런스로서 **this로는 현재 객체의 모든 멤버**를, **super로는 현재 객체 내에 있는 부모 클래스 멤버를 접근**할 수 있다.  
super로 메소드를 호출하면 정적 바인딩을 실행한다.
```java
this.객체내의멤버
super.객체내의부모클래스의멤버
```
this()와 super()는 모두 메소드 호출이며, **this()는 생성자에서 다른 생성자를 호출**할 때 사용하고, **super()는 자식 클래스의 생성자에서 부모 클래스의 생성자를 호출**할 때 사용한다.

### 오버로딩과 오버라이딩
오버로딩과 오버라이딩은 자바에서 다형성을 이루는 방법들이다.
|비교요소|메소드 오버로딩|메소드 오버라이딩|
|---|---|---|
|선언|같은 클래스나 상속 관계에서 동일한 이름의 메소드 중복 작성|자식 클래스에서 부모 클래스에 있는 메소드와 동일한 이름의 메소드 재작성|
|**관계**|동일한 클래스 내 혹은 상속 관계|상속 관계|
|목적|이름이 같은 여러 개의 메소드를 중복 작성하여 사용의 편리성 향상. 다형성 실현|부모 클래스에 구현된 메소드를 무시하고 자식 클래스에서 새로운 기능의 메소드를 재정의하고자 함. 다형성 실현|
|**★조건★**|메소드 이름은 반드시 동일하고, 매개변수 타입이나 개수가 달라야 성립|메소드의 이름, 매개변수 타입과 개수, 리턴 타입이 모두 동일하여야 성립|
|바인딩|정적 바인딩. 호출될 메소드는 컴파일 시에 결정|동적 바인딩. 실행 시간에 오버라이딩된 메소드를 찾아 호출|
***

## 추상 클래스
추상 클래스는 상속에서 부모 클래스로 사용된다.

### 추상 메소드
추상 메소드는 선언은 되어 있으나 코드가 구현되어 있지 않은, 즉 껍데기만 있는 메소드이다. 추상 메소드를 작성하려면 abstract 키워드와 함께 원형만 선언하고 코드는 작성하지 않는다.
```java
public abstract String getName();
public abstract void setName(String s);

public abstract String failName() { return "Fail"; }    // 컴파일 오류. 코드가 작성되어 있기 때문에 추상 메소드가 될 수 없다.
```
***

### 추상 클래스 만들기
추상 클래스가 되는 경우는 2가지로서, 모두 abstract 키워드를 선언해야 한다.
- 추상 메소드를 포함하는 클래스
```java
abstract class Shape1 {
    public Shape() { }
    public void paint() { draw(); }
    abstract public void draw();
}
```
- 추상 메소드가 없지만 abstract로 선언한 클래스
```java
abstract class Shape2 {
    String name;
    public void load(String name) {
        this.name = name;
    }
}
```
Shape1과 Shape2는 모두 추상 클래스이다.  
추상 메소드를 가지고 있으면 반드시 추상 클래스로 선언되어야 한다.
```java
class Fault {                   // 컴파일 오류. 추상 클래스로 선언되지 않음
    abstract public void f();   // 추상 메소드
}
```
***

### 추상 클래스는 객체를 생성할 수 없다
JVM은 추상 클래스의 객체(인스턴스)를 생성할 수 없다. 추상 클래스는 객체를 생성할 목적으로 만드는 클래스가 아니기 때문이다. 추상 클래스에는 실행 코드가 없는 미완성 상태인 추상 메소드가 있을 수 있기 때문에, 다음과 같이 추상 클래스의 객체를 생성하는 코드에는 컴파일 오류가 발생한다.
```java
abstract class Shape1 {
    public Shape() { }
    public void paint() { draw(); }
    abstract public void draw();
}

public class AbstractError {
    public static void main(String[] args) {
        Shape shape;            // 컴파일 오류 아님. 추상 클래스의 레퍼런스 변수를 선언하는 것은 오류가 아니다.
        shape = new Shape();    // 컴파일 오류. 추상 클래스 Shape의 객체를 생성할 수 없다.
    }
}
```
***

### 추상 클래스의 상속
추상 클래스를 단순히 상속받는 자식 클래스는 추상 클래스가 된다. 추상 메소드를 그대로 상속받기 때문이다. 그러므로 자식 클래스에 abstract를 붙여 추상 클래스임을 명시해야 컴파일 오류가 발생하지 않는다.
```java
abstract class Shape {
    public Shape() { }
    public void paint() { draw(); }
    abstract public void draw();
}

abstract class Line extends Shape {
    public String toString() { return "Line"; }
}
```
```java
abstract class Shape {
  public Shape() { }
  public void paint() { draw(); }
  abstract public void draw();
}

class Line extends Shape {          // draw()에 대해 오버라이딩을 했으므로 abstract를 붙이지 않아도 된다.
  @Override
  public void draw() {
    System.out.println("dd");
  }
  public String toString() { return "Line"; }
}
```

### 추상 클래스의 용도
추상 클래스를 상속받은 자식 클래스는 개발자에 따라 다양하게 구현된다. 모든 개발자들은 자식 클래스에서 추상 클래스에 선언된 추상 메소드를 모두 구현해야 된다.  
추상 클래스를 책의 목차라고 비유하면 자식 클래스는 목차에 따라 작성된 책과 같다.  
추상 클래스를 이용하면 응용프로그램의 설계와 구현을 분리할 수 있다. 추상 클래스로 기본 방향을 잡아놓고 자식 클래스에서 구현하면 구현 작업이 쉬워진다. 또한 추상 클래스는 **계층적 상속 관계**를 가지는 클래스들의 구조를 만들 때 적합하다.
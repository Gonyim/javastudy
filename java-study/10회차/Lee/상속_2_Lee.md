# 5. 상속

## 상속과 생성자

### 자식 클래스와 부모 클래스의 생성자 호출 및 실행
자식 클래스와 부모 클래스는 각각 생성자를 가지고 있다.  
1. 자식 클래스 객체가 생성될 때 자식 클래스의 생성자와 부모 클래스의 생성자 모두 실행된다.
   - 자식 클래스의 객체가 생성되면 이 객체 속에 자식 클래스와 멤버와 부모 클래스의 멤버가 모두 들어 있다. 생성자의 목적은 객체 초기화에 있으므로, 자식 클래스의 생성자는 생성된 객체 속에 들어 있는 자식 클래스의 멤버 초기화나 필요한 초기화를 수행하고, 부모 클래스의 생성자는 생성된 객체 속에 있는 부모 클래스의 멤버 초기화나 필요한 초기화를 각각 수행한다.
2. 자식 클래스의 생성자와 부모 클래스의 생성자 중 부모 클래스의 생성자가 먼저 실행된 후 자식 클래스의 생성자가 실행된다.

```java
class A {
    public A() {
        System.out.println("생성자A");
    }
}

class B extends A {
    public B() {
        System.out.println("생성자B");
    }
}

class C extends B {
    public C() {
        System.out.println("생성자C");
    }
}

public class D {
    public static void main(String[] args) {
        C c;
        c = new C();
    }
}
```
- 자식 클래스의 생성자가 먼저 호출되지만, 결국 부모 클래스의 생성자가 먼저 실행되고 자식 클래스의 생성자가 나중에 실행된다.
- 컴파일러는 자식 클래스의 생성자에 대해, 부모 클래스의 생성자를 호출한 뒤 자신의 코드를 실행하도록 컴파일한다. 부모 클래스가 먼저 초기화된 후, 이를 활용하는 자식 클래스가 초기화되어야 한다.
***

## 자식 클래스에서 부모 클래스 생성자 선택
부모 클래스에 여러 개의 생성자가 있는 경우, 자식 클래스의 생성자와 함께 실행될 부모 클래스의 생성자는 어떻게 결정되는가?  
원칙적으로, 자식 클래스의 개발자가 자식 클래스의 각 생성자에 대해, 함께 실행될 부모 클래스의 생성자를 지정해야 한다. 하지만, 개발자가 부모 클래스의 생성자를 명시적으로 지정하지 않는 경우, 컴파일러는 자동으로 부모 클래스의 기본 생성자를 호출하도록 컴파일한다.
- 부모 클래스의 기본 생성자가 자동 선택되는 경우
  - 개발자의 명시적 지시가 없으면, 자식 클래스의 생성자가 기본 생성자이든 매개변수를 가진 것이든, 부모 클래스에 만들어진 기본 생성자가 선택된다. 이 선택은 자바 컴파일러에 의해 강제로 이루어진다.
```java
class A {
    public A() {
        System.out.println("생성자A");
    }
    public A(int x) {
        ......
    }
}

class B extends A {
    public B() {
        System.out.println("생성자B");
    }
}

public class C {
    public static void main(String[] args) {
        B b;
        b = new B();
    }
}
```
클래스 A에는 2개의 생성자가 작성되어 있지만, 클래스 B의 기본 생성자가 호출되면 부모 클래스의 기본 생성자 A()가 자동으로 호출된다.
***

- super()를 이용하여 명시적으로 부모 클래스의 생성자 선택
  - 지금까지는 개발자가 명시적으로 선택하지 않았을 때, 컴파일러가 자동으로 부모 클래스의 기본 생성자를 호출했지만, 자식 클래스의 생성자에서 super()를 이용하면, 부모 클래스 생성자를 명시적으로 선택할 수 있다. super()는 부모 클래스 생성자를 호출하는 코드이다. 괄호 안에 인자를 전달하여 부모 클래스의 생성자를 호출할 수도 있다.
```java
class A {
    public A() {
        System.out.println("생성자A");
    }
    public A(int x) {
        ......
    }
}

class B extends A {
    public B() {
        System.out.println("생성자B");
    }
    public B(int x) {
        super(x);
        ......
    }
}

public class C {
    public static void main(String[] args) {
        B b;
        b = new B(3);
    }
}
```
**super()는 반드시 생성자의 첫 라인에 사용되어야 한다.**

```java
문제 1

class Point {
    private int x, y;
    public Point() {
        this.x = this.y = 0;
    }
    public Point(int x, int y) {
        this.x = x;
        this.y = y;
    }
    public void showPoint() {
        System.out.println("(" + x + "," + y +")");
    }
}

class ColorPoint extends Point {
        private String color;
        public ColorPoint(int x, int y, String color) {
            super(x, y);
            this.color = color;
        }
        public void showColorPoint() {
            System.out.print(color);
            showPoint();
        }
    }

public class SuperEx {
    public static void main(String[] args) {
        ColorPoint cp = new ColorPoint(3, 4, "blue");
        cp.showColorPoint();
    }
}
```
```java
문제 2

class A {
    public A() {
        System.out.println("생성자A");
    }
    public A(int x) {
        System.out.println("매개변수생성자A" + x);
    }
}

class B extends A {
    public B() {
        super(10);
        System.out.println("생성자B");
    }
    public B(int x) {
        System.out.println("매개변수생성자B" + x);
    }
}

public class C {
    public static void main(String[] args) {
        B b;
        b = new B();
    }
}
```
***

## 업캐스팅과 instanceof 연산자
캐스팅이란 타입 변환을 말한다. 자바에서 클래스에 대한 캐스팅은 업캐스팅과 다운캐스팅으로 나뉜다.
***

### 업캐스팅
자바에서 자식 클래스는 부모 클래스의 속성을 상속받기 때문에, 자식 클래스의 객체는 부모 클래스의 멤버를 모두 가진다. 그러므로 자식 클래스의 객체를 부모 클래스의 객체로 취급할 수 있다. 자식 클래스의 객체에 대한 레퍼런스를 부모 클래스 타입으로 변환하는 것을 업캐스팅이라고 한다.  
업캐스팅은 부모 클래스의 레퍼런스로 자식 클래스의 객체를 가리키게 한다.
```java
class Person {
    String name;
    String id;

    public Person(String name) {
        this.name = name;
    }
}

class Student extends Person {
    String grade;
    String department;

    public Student(String name) {
        super(name);
    }
}

public class UpcastingEx {
    public static void main(String[] args) {
        Person p;
        Student s = new Student("가나다");
        p = s;

        System.out.println(p.name);

        p.grade = "A";          // 컴파일 오류
        p.department = "ddd";   // 컴파일 오류

        s.name = "라마바";
        s.grade = "S";
    }
}
```
- 이 코드에서, 부모 클래스 타입의 레퍼런스 p가 자식 클래스 객체(s)를 가리키도록 치환되는 것이 업캐스팅이다. 업캐스팅을 통해 Person타입의 p는 Student 객체를 가리킨다. 하지만 레퍼런스 p로는 Person 클래스의 멤버만 접근할 수 있다. 왜냐하면 p는 Person 타입이기 때문이다. 업캐스팅한 레퍼런스로는 객체 내에 모든 멤버에 접근할 수 없고 부모 클래스의 멤버만 접근할 수 있다. 업캐스팅은 명시적 타입 변환을 하지 않아도 된다.
***

### 다운캐스팅
업캐스팅과 반대로 캐스팅하는 것을 다운캐스팅이라고 한다. 다운캐스팅은 업캐스팅과 달리 명시적으로 타입 변환을 지정해야 한다.
```java
public class Main {
  public static void main(String[] args) {
    Person p = new Student("가나다");
    Student s;
    s = (Student)p;         // 명시적 타입 변환 지정

    System.out.println(p.name);

    s.name = "라마바";
    s.grade = "S";
    System.out.println(s.name + s.grade);
  }
}
```
***

### 업캐스팅과 instanceof 연산자
업캐스팅을 한 경우, 레퍼런스가 가리키는 객체의 진짜 클래스 타입을 구분하기 어렵다.
```java
class Person {
    ......
}
class Student extends Person {
    ......
}
class Researcher extends Person {
    ......
}
class Professor extends Researcher {
    ......
}
```
```java
Person p = new Person();
Person p = new Student();       // 업캐스팅
Person p = new Researcher();    // 업캐스팅
Person p = new Professor();     // 업캐스팅
```
```java
void print(Person person) {
    ......
}
```
위의 코드에서 오직 아는 것은 Person을 상속받은 객체가 업캐스팅되어 넘어왔다는 사실밖에 없다. 매개변수 person에 전달된 객체가 어떤 클래스의 객체인지 구별할 방법이 필요하다.

### instanceof 연산자 사용
레퍼런스가 가리키는 객체가 어떤 클래스 타입인지 구분하기 위해, 자바에서는 instanceof 이항 연산자를 사용한다.
```java
레퍼런스 instanceof 클래스명
```
instanceof 연산자의 결과값은 boolean값으로 '레퍼런스'가 가리키는 객체가 해당 '클래스'타입의 객체이면 true이고 아니면 false로 계산한다.
```java
Person jee = new Student();
Person kim = new Professor();
Person lee = new Researcher();
if (jee instanceof Person)      // true
if (jee instanceof Student)     // true
if (kim instanceof Student)     // false
if (kim instanceof Professor)   // true
if (kim instanceof Researcher)  // true
if (lee instanceof Professor)   // false
```

```java
문제 1
class A { }
class B extends A { }
class C extends A { }
class D extends C { }
----------------------
A a;
B b = new B();
a = new D();
----------------------

다음과 같은 클래스 계층 구조가 있을 때 instanceof의 결과가 false인 것을 모두 고르시오.

1. if(b instanceof A)
2. if(a instanceof C)
3. if(a instanceof java.lang.Object)
4. if((new A()) instanceof D)
5. if((new C()) instanceof A)
6. if((new C()) instanceof C)
```
***

## 메소드 오버라이딩
메소드 오버라이딩은 부모 클래스와 자식 클래스의 메소드 사이에 발생하는 관계로서, 부모 클래스에 선선된 메소드와 같은 이름, 같은 리턴 타입, 같은 매개 변수 리스트를 갖는 메소드를 자식 클래스에서 재작성하는 것이다.  
메소드 오버라이딩을 했을 때 외부에서나 내부에서 해당 메소드를 호출하면 부모 클래스의 메소드는 절대로 실행되지 않고 반드시 자식 클래스의 메소드가 실행된다.  
따라서 메소드 오버라이딩은 '부모 클래스 메소드 무시하기 혹은 덮어쓰기'로 표현할 수 있다.  
이런 처리를 **동적 바인딩**이라고 부르며, 메소드 오버라이딩은 동적 바인딩을 유발시킨다.
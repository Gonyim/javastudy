# 객체지향 프로그래밍

## 상속(inheritance)
### 상속의 정의와 장점
* 상속이란, 기존의 클래스를 재사용하여 새로운 클래스를 작성하는 것이다
  * 보다 적은 양의 코드로 새로운 클래스를 작성할 수 있다
  * 코드를 공통적으로 간리할 수 있기 때문에 코드의 추가 및 변경이 매우 용이하다
    * 이러한 특징은 코드의 재사용성을 높이고 코드의 중복을 제거하여 프로그램의 생산성과 유지보수에 크게 기여한다
* 자바에서 상속을 구현하는 방법
  * 새로 작성하고자 하는 클래스의 이름 뒤에 상속받고자 하는 클래스의 이름을 키워드 'extends'와 함께 써주기만 하면 된다
```java
class Parent { }
class Child extends Parent {
    // ...
}
```
* 새로 작성하려는 클래스의 이름이 Child이고 상속받고자 하는 기존 클래스의 이름이 Parent인 경우
* 이 두 클래스는 서로 상속 관계에있다고 한다
* 상속해주는 클래스를 '조상 클래스'라 하고 상속받는 클래스를 '자손 클래스'라고 한다
```java
조상 클래스 : 부모(parent)클래스, 상위(super)클래스, 기반(base)클래스
자손 클래스 : 자식(chile)클래스, 하위(sub)클래스, 파생된(derived)클래스
```
* 클래스 Parent와 Child의 상속 관계도 <br>
![상속관계도](https://github.com/nohheeyeon/TIL/assets/130336617/2cbc6d0b-cc04-422b-a36f-5e2915bfec09)
  * 프로그램이 커질 수록 클래스 간의 관계가 복잡해지는데, 이 때 상속관계도로 표현하면 클래스 간의 관계를 보다 쉽게 이해할 수 있습니다
* 클래스 Parent와 Child의 다이어그램 <br>
  ![다이어그램](https://github.com/nohheeyeon/TIL/assets/130336617/3a3bf8e3-f2a4-4060-8af9-beea7a144e5c)
  * 자손 클래스는 조상 클래스의 모든 멤버를 상속받기 때문에, Child클래스는 Parent클래스의 멤버들을 포함한다고 할 수 있다
  * 클래스는 멤버들의 집합이므로 클래스 Parent와 Child의 관계를 다이어그램같이 표현할 수도 있다
* Parent클래스에 age라는 정수형 변수를 멤버변수로 추가
  * 자손인 Child 클래스에 새로운 멤버로 play() 메서드를 추가 <br>
![image](https://github.com/nohheeyeon/TIL/assets/130336617/49d6a67e-2206-4c0e-bf9a-2e917df9e1b7)
```java
class Parent {
    int age;
}

class Child extends Parent {
    void play() {
        System.out.println("놀자~");
    }
}
```
  * 자손 클래스는 조상의 멤버를 모두 상속받기 때문에, Child클래스는 자동적으로 age라는 멤버변수가 추가된 것과 같은 효과를 얻는다
  * Child클래스에 새로운 코드가 추가되어도 조상인 Parent클래스느 아무런 영향도 받지 않는다
    * 조상 클래스가 변경되면 자손 클래스는 자동적으로 영향을 받게 되지만, 자손 클래스가 변경되는 것은 조상 클래스에 아무런 영향을 주지 못 한다
*  자손 클래스는 조상 클래스의 모든 멤버를 상속 받으므로 항상 조상 클래스와 같거나 보다 많은 멤버를 갖는다
  * 상속에 상속을 거듭할수록 상속받는 클래스의 멤버 개수는 점점 늘어나게 됩니다
    * 상속을 받는다는 것은 조상 클래스를 확장(extend)한다는 의미로 해석할 수도 있으며 이 것이 상속에 사용되는 키워드가 'extends'인 이유이기도 하다
```java
* 생성자와 초기화 블럭은 상속되지 않는다. 멤버만 상속된다
* 자손 클래스의 멤버 개수는 조상 클래스보다 항상 같거나 같다
```
### 클래스 간의 관계 - 포함관계
* 클래스를 재사용하는 방법
  * 클래스 간에 '포함(Composite)' 관계를 맺어주는 것이다
    * 클래스 간의 포함관계를 맺어주는 것은 한 클래스의 멤버변수로 다른 클래스 타입의 참조변수를 선언하는 것을 뜻한다
```java
class Circle {
    int x; // 원점의 x좌표
    int y; // 원점의 y좌표
    int r; // 반지름(radius)
}
```
* 좌표 상의 한 점을 다루기 위한 Point 클래스
```java
class Point {
    int x; // x좌표
    int y; // y좌표
}
```
* Point클래스를 재사용해서 Circle클래스를 작성한다면!
```java
class Circle {
    Point c = new Point(); // 원점
    int r;
}
```
* 한 클래스를 작성하는데 다른 클래스를 멤버변수로 선언하여 포함시키는 것은 좋은 생각이다
  * 하나의 거대한 클래스를 작성하는 것 보다 단위별로 여러 개의 클래스를 작성한 다음, 이 단위 클래스들을 포함관계로 재사용하면 보다 간결하고 손쉽게 클래스를 작성할 수 있다
### 클래스간의 관계 결정하기
* 클래스를 작성하는데 있어서 상속관계를 맺어 줄 것인지 포함관계를 맺어 줄 것인 지 결정하는 것은 때때로 혼돈스러울 수 있다
* '~은 ~이다(is-a)'와 '~은 ~을 가지고 있다(has-a)'를 넣어서 문장을 만들어보면 클래스 간의 관계다 보다 명확해 진다
```java
원(Circle)은 점(Point)이다. - Circle is a Point. // 상속관계
원(Circle)은 점(Point)을 가지고 있다. - Circle has a Point. // 포함관계
```
### 단일상속(single inheritance)
* 자바에서는 단일 상속만을 허용한다
  * 둘 이상의 클래스로부터 상속을 받을 수 없다
```java
class TvDVD extends Tv, DVD { // 에러, 조상은 하나만 허용된다
    // ...
}
```
* 다중상속을 허용하면 여러 클래스로부터 상속받을 수 있기 때문에 복합적인 기능을 가진 클래스를 쉽게 작성할 수 있다는 장점이 있지만, 클래스간의 관계가 매우 복잡해진다는 것과 서로 다른 클래스로부터 상속받은 멤버 간의 이름이 같은 경우 구별할 수 있는 방법이 없다는 단점을 가지고 있다
* 단일 상속이 하나의 조상 클래스만을 가질 수 있기 때문에 다중상속에 비해 불편한 점도 있지만, 클래스 간의 관계가 보다 명확해지고 코드를 더욱 신뢰할 수 있게 만들어 준다는 점에서 다중상속보다 유리하다
### Object클래스 - 모든 클래스의 조상
* 모든 클래스 상속계층도의 최상위에 있는 조상클래스이다
  * 다른 클래스로부터 상속받지 않는 모든 클래스들은자동적으로 Object클래스로부터 상속받게 함으로써 이것을 가능하게 한다
```java
class Tv {
  ...
}
```
* 컴파일러는 자동적으로 'extends Object'를 추가하여 Tv클래스가 Object클래스로부터 상속받도록 한다
* 만일 다른 클래스로부터 상속을 받는다고 하더라도 상속계층도를 따라 조상클래스, 조상클래스의 조상클래스를 찾아 올라가다 보면 결국 마지막 최상위 조상은 Object클래스일 것이다
  * 이미 어떤 클래스로부터 상속받도록 작성된 클래스에 대해서는 컴파일러가 'extends Object'를 추가하지 않는다 <br>
<img width="300" alt="image" src="https://github.com/nohheeyeon/TIL/assets/130336617/71bda9bb-7e1e-41e0-8815-f6774bfb61ee"> <br>

```java
class Tv {
  ...
}

class SmartTv extends Tv {
  ...
}
```
* Tv클래스가 있고, Tv클래스를 상속받는 SmartTv가 있을 때의 상속계층도
  * 상속계층도를 단순화하기 위해서 Object클래스를 생략하는 경우가 많다
* 자바의 모든 클래스들은 Object클래스를 상속받기 때문에 Object클래스에 정의된 멤버들을 사용할 수 있다
  * toString()이나 equals(Object o)와 같은 메서드를 따로 정의하지 않고도 사용할 수 있었던 이유는 이 메서드들이 Object클래스에 정의된 것들이기 때문이다

## 오버라이딩(overriding)
### 오버라이딩이란?
* 조상클래스로부터 상속받은 메서드의 내용을 변경하는 것을 오버라이딩이라고 한다
* 상속받은 메서드를 그대로 사용하기도 하지만, 자손 클래스 자신에 맞게 변경해야하는 경우가 많다
    * 이럴 때 조상의 메서드를 오버라이딩한다
```java
class Vehicle {
  void run() {
              System.out.println("차량이 달립니다.");
    }
}

class Car extends Vehicle {
  @Override
  void run() {
              System.out.println("자동차가 주행합니다.");
    }
}

public class Main {
  public static void main(String[] args) {
              Vehicle vehicle1 = new Vehicle();
              Vehicle vehicle2 = new Car(); // 업캐스팅
        
              vehicle1.run(); // "차량이 달립니다." 출력
              vehicle2.run(); // "자동차가 주행합니다." 출력
    }
}
```
* Car 클래스는 Vehicle 클래스의 run 메서드를 오버라이딩하여 자체적인 구현을 함
* Vehicle2는 Car 클래스의 인스턴스이지만 Vehicle 타입의 참조변수에 할당되었으며, run 메서드가 Car 클래스의 버전을 실행하게 된다
### 오버라이딩의 조건
* 조상 클래스의 메서드를 자손 클래스에서 오버라이딩할 때
1. 선언부가 조상 클래스의 메서드와 일치해야 한다
2. 접근 제어자를 조상 클래스의 메서드보다 좁은 범위로 변경할 수 없다
3. 예외는 조상 클래스의 메서드보다 많이 선언할 수 없다
### 오버로딩 vs 오버라이딩
**오버로딩** 기존에 없는 새로운 메서드를 정의하는 것(new) <br>
**오버라이딩** 상속받은 메서드의 내용을 변경하는 것(change, modify)
```java
class Parent {
    void parentMethod() {}
  class Child extends Parent {
        void parentMethod() {}
        void parentMethod(int i) {}
    
        void childeMethod() {}
        void childeMethod(int i) {}
        void childeMethod() {}
    }
  }
}
```
### super
* super은 자손 클래스에서 조상 클래스로부터 상속받은 멤버를 참조하는데 사용되는 참조 변수이다
* 멤버변수와 지역변수의 이름이 같을 때 this를 붙여서 구별했듯이 상속받은 멤버와 자신의 멤버와 이름이 같을 때는 super를 붙여서 구별할 수 있다

### super() - 조상 클래스의 생성자
* this()와 마찬가지고 super() 역시 생성자이다
* this()는 같은 클래스의 다른 생성자를 호출하는데 사용되지만, super()는 조상 클래스의 생성자를 호출하는데 사용된다

## package와 import
## 패키지(package)

### 패키지의 개념
* 패키지란, 클래스의 묶음이다
  * 패키지에는 클래스 또는 인터페이스를 포함시킬 수 있으며, 서로 관련된 클래스들끼리 그룹 단위로 묶어 놓음으로써 클래스를 효율적으로 관리할 수 있다
    * 같은 이름의 클래스 일지라도 서로 다른 패키지에 존재하는 것이 가능하므로, 자신만의 패키지 체계를 유지함으로써 다른 개발자가 개발한 클래스 라이브러리의 클래스와 이름이 충돌하는 것을 피할 수 있다
### 패키지의 선언
* 패키지를 선언하는 것은 클래스나 인터페이스의 소스파일 (.java)의 맨 위에 한 줄만 적어주면 된다
```java
package 패키지명;
```
* 패키지 선언문은 반드시 소스파일에서 주석과 공백을 제외한 첫 번재 문장이어야하며, 하나의 소스파일에 단 한 번만 선언될 수 있다
  * 해당 소스파일에 포함된 모든 클래스나 인터페이스는 선언된 패키지에 속하게 된다
* 패키지명은 대소문자를 모두 허용하지만, 클래스명과 쉽게 구분하기 위해서 소문자로 하는 것을 원칙으로 하고 있다
* 모든 클래스는 반드시 하나의 패키지에 포함되어야하지만, 지금까지 소스파일을 작성할 때 패키지를 선언하지 않고도 아무런 문제가 없었던 이유는 자바에서 기본적으로 제공하는 '이름 없는 패키지(unnamed package)' 때문이다

### import문
* import문의 역할은 컴파일러에게 소스파일에 사용된 클래스의 패키지에 대한 정보를 제공하는 것이다
  * 컴파일 시에 컴파일러는 import문을 통해 소스파일에 사용된 클래스들의 패키지를 알아낸 다음, 모든 클래스이름 앞에 패키지명을 붙여 준다
```java
import 패키지명.클래스명;
또는
import 패키지명.*;
```
### static import문
* import문을 사용하면 클래스의 패키지명을 생략할 수 있는 것과 같이 static import문을 사용하면 static멤버를 호출할 때 클래스 이름을 생략할 수 있다
  * 특정 클래스의 static멤버를 자주 사용할 때 편리하며, 코드도 간결해진다

```java
import static java.lang.Math.*;

public class MathTest {
    public static void main(String[] args) {
        double result = sqrt(25.0);
        System.out.println("Square root: " + result);
    }
}
```

## 제어자(modifier)

### 제어자란?
* 제어자는 클래스, 변수 또느 메서드의 선언부에 함께 사용되어 부가적인 의미를 부여한다
* 제어자의 종류는 크게 접근 제어자와 그 외의 제어자로 나눌 수 있다
* 접근 제어자

| 접근 제어자 | 설명                                                                                      |
|-------------|-------------------------------------------------------------------------------------------|
| public      | 어떤 클래스에서든 접근이 가능합니다.                                                         |
| protected   | 같은 패키지 내에서는 접근이 가능하며, 다른 패키지의 자식 클래스에서도 접근이 가능합니다. |
| default     | 같은 패키지 내에서만 접근이 가능합니다.                                                       |
| private     | 해당 클래스 내에서만 접근이 가능하고, 외부 클래스에서는 접근이 불가능합니다.                |

* 그 외의 제어자

| 제어자     | 설명                                                                                   |
|------------|----------------------------------------------------------------------------------------|
| static     | 클래스 멤버(변수 또는 메서드)로 선언하며, 객체 생성 없이 사용할 수 있습니다.              |
| final      | 변수에 사용 시 값 변경이 불가능하며, 메서드에 사용 시 오버라이딩이 불가능합니다.          |
| abstract   | 추상 클래스 또는 추상 메서드를 선언하는 데 사용되며, 구체적인 구현이 없는 추상 메서드를 가집니다. |
| transient  | 직렬화할 수 없는 필드를 표시하며, 객체의 상태를 파일에 저장할 때 사용됩니다.         |
| volatile   | 멀티 스레딩 환경에서 변수의 값을 안전하게 읽고 쓸 수 있도록 합니다.                     |
| synchronized | 멀티 스레딩 환경에서 메서드 또는 블록을 동기화하여 스레드 간의 경쟁 상태를 방지합니다.     |
| strictfp   | 부동 소수점 연산의 표준을 정확히 따르도록 클래스 또는 메서드를 선언합니다.                 |
| native     | 자바 외부의 네이티브 코드(C, C++ 등)와 연결하여 사용하는 메서드를 선언합니다.            |

* 제어자는 클래스나 멤버변수와 메서드에 주로 사용되며, 하나의 대상에 대해서 여러 제어자를 조합하여 사용하는 것이 가능하다
  * 단, 접근 제어자는 한 번에 네 가지 중 하나만 선택해서 사용할 수 있다
    * (제어자들 간의 순서는 관계없지만 주로 접근 제어자를 제일 왼쪽에 놓는 경향이 있다)
    
### static - 클래스의, 공통적인
* static은 '클래스의' 또는 '공통적인'의 의미를 가지고 있다
* 인스턴스 변수는 하나의 클래스로부터 생성되었더라도 각기 다른 값을 유지하지만, 클래스 변수는 인스턴스에 관계없이 같은 값을 갖는다
  * 하나의 변수를 모든 인스턴스가 공유하기 때문이다
* static이 붙은 멤버변수와 메서드, 그리고 초기화 블럭은 인스턴스가 아닌 클래스에 관계된 것이기 때문에 인스턴스를 생성하지 않고도 사용할 수 있다
* 인스턴스메서드와 static메서드의 근본적인 차이는 메서드 내에서 인스턴스 멤버를 사용하는 가의 여부에 있다
```java
static이 사용될 수 있는 곳 - 멤버변수, 메서드, 초기화 블럭
```
```java
public class MyClass {
  // 정적(static) 멤버 변수
  public static int staticVariable = 5;

  // 정적(static) 메서드
  public static void staticMethod() {
    System.out.println("이것은 정적 메서드입니다.");
  }

  public static void main(String[] args) {
    // 객체를 생성하지 않고 정적 멤버에 접근
    int value = MyClass.staticVariable;
    System.out.println("정적 멤버 변수의 값: " + value);

    MyClass.staticMethod(); // 정적 메서드 호출
  }
}
```

### final - 마지막의, 변경될 수 없는
* final은 '마지막의' 또는 '변경될 수 없는'의 의미를 가지고 있으며 거의 모든 대상에 사용될 수 있다
* 변수에 사용되면 값을 변경할 수 없는 상수가 되며, 메서드에 사용되면 오버라이딩을 할 수 없게 되고 클래스에 사용되면 자신을 확장하는 자손클래스를 정의하지 못하게 된다
```java
final이 사용될 수 있는 곳 - 클래스, 메서드, 멤버변수, 지역변수
```
```java
public class Example {
    // final 멤버 변수 (상수)
    final int finalMemberVariable = 10;

    // final 메서드
    final void finalMethod() {
        final int finalLocalVar = 20; // final 지역 변수 (상수)
        System.out.println("final 멤버 변수: " + finalMemberVariable);
        System.out.println("final 지역 변수: " + finalLocalVar);
    }

    // final 내부 클래스
    final class FinalInnerClass {
        void innerMethod() {
            System.out.println("final 내부 클래스의 메서드");
        }
    }

    public static void main(String[] args) {
        Example example = new Example();
        example.finalMethod();

        // final 내부 클래스의 인스턴스 생성
        FinalInnerClass finalInner = example.new FinalInnerClass();
        finalInner.innerMethod();
    }
}

```
### abstract - 추상의, 미완성의
* abstract는 '미완성'의 의미를 가지고 있다
* 메서드의 선언부만 작성하고 실제 수행내용은 구현하지 않은 추상 메서드를 선언하는데 사용된다
```java
abstract가 사용 될 수 있는 곳 - 클래스, 메서드
```
```java
public abstract class MyAbstractClass { // 추상 클래스
    abstract void myAbstractMethod(); // 추상 메서드
}
```

### 접근 제어자(access modifier)
* 접근 제어자는 멤버 또는 클래스에 사용되어 ,해당하는 멤버 또는 클래스를 외부에서 접근하지 못하도록 제한하는 역할을 한다

| 접근 제어자    | 접근 범위                        |
| -------------- | --------------------------------- |
| public         | 모든 클래스에서 접근 가능        |
| private        | 같은 클래스 내에서만 접근 가능   |
| protected      | 같은 패키지 또는 하위 클래스에서 접근 가능 |
| (default)      | 같은 패키지 내에서만 접근 가능   |

```java
public class MyClass {
    public int publicVar;    // 다른 클래스에서 접근 가능
    private int privateVar;  // 같은 클래스에서만 접근 가능
    protected int protectedVar;  // 같은 패키지 또는 하위 클래스에서 접근 가능
    int defaultVar;          // 같은 패키지에서만 접근 가능

    public void myMethod() {
        // 여기서는 모든 변수에 접근 가능
        publicVar = 10;
        privateVar = 20;
        protectedVar = 30;
        defaultVar = 40;
    }
}

class AnotherClass {
    public void anotherMethod() {
        MyClass myObject = new MyClass();
        myObject.publicVar = 100;    // public 변수에 접근 가능
        // myObject.privateVar = 200; // private 변수에 접근 불가능
        // myObject.protectedVar = 300; // protected 변수에 접근 불가능
        // myObject.defaultVar = 400;   // default 변수에 접근 불가능
    }
}
```

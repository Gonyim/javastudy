# 4장 클래스와 객체

## 메소드 활용

### 메소드 형식
메소드는 클래스의 멤버 함수로서, 메소드 앞에 접근 지정자를 선언한다는 점을 제외하면 C/C++의 함수 작성법과 동일하다. 접근 지정자는 public, private, protected, default 4가지 유형으로 메소드가 다른 클래스에서 호출될 수 있는지 지정하기 위해 사용한다.
***

### 인자 전달
자바의 메소드 호출 시 인자 전달 방식은 '값에 의한 호출'(call-by-value)이다. 호출하는 실인자의 값이 복사되어 메소드의 매개변수에 전달된다.
- 기본 타입의 값이 전달되는 경우
    - 메소드의 매개변수가 기본 타입(byte, short, int, long, boolean 등)으로 선언된 경우, 호출자가 건네는 값이 매개변수에 복사되어 전달된다.
- 객체가 전달되는 경우
    - 메소드의 매개변수가 클래스 타입인 경우, 객체가 아니라 객체의 레퍼런스 값이 전달된다. 메소드 호출 시 객체가 전달되는 경우, 객체에 대한 레퍼런스만 전달이 되며, 객체가 통째로 복사되지 않는다는 점을 유념한다.
- 배열이 전달되는 경우
    - 배열이 메소드에 전달되는 경우도 객체 레퍼런스가 전달되는 경우와 동일하다. 배열이 통째로 전달되는 것이 아니며 배열에 대한 레퍼런스만 전달된다.

자바에서는 메소드의 매개변수로 객체나 배열을 전달할 때 레퍼런스만 전달하기 때문에, 객체나 배열이 통째로 넘어가지 않는다. 아무리 큰 객체나 배열도 하나의 정수 크기인 레퍼런스만 전달되므로, 매개변수 전달로 인한 시간이나 메모리의 오버헤드가 없는 장점이 있다. 하지만,  메소드에서 전달받은 객체의 필드나 배열의 원소 값을 변경할 수 있기 때문에 그것이 장점이자 주의할 점이다.
***

### 메소드 오버로딩
자바에서는 한 클래스 내에, 이름이 같지만 매개변수의 타입이나 개수가 서로 다른 여러 개의 메소드를 중복 작성할 수 있다. 이것을 메소드 오버로딩(메소드 중복)이라고 부른다. 여러 개의 메소드가 오버로딩되려면 두 조건을 모두 만족시켜야 한다.
1. 메소드 이름이 동일하여야 한다.
2. 매개변수의 개수나 타입이 서로 달라야 한다.

메소드 오버로딩은 자바 컴파일러에 의해 판단되며, 컴파일러가 이름이 같은 메소드들을 구분할 수 있으면 메소드 오버로딩이 성공한다. 자바 컴파일러는 각 호출문에 대해, 매개변수의 타입과 개수에 일치하는 메소드를 찾아낸다.

```java
메소드 오버로딩 성공 사례

class OverloadingSuccess {
    public int getSum(int i, int j) {
        return i + j;
    }
    public int getSum(int i, int j, int k) {
        return i + j + k;
    }
}
```

```java
메소드 오버로딩 실패 사례

class OverloadingFail {
    public int getSum(int i, int j) {
        return i + j;
    }
    public int getSum(int i, int j) {   // 위의 getSum()메소드와 매개변수의 개수, 타입이 모두 같기 때문에 메소드 오버로딩 실패
        return (double)(i + j);
    }
}
```
- 위의 실패 사례에서 메소드의 리턴 타입이 서로 다르니 두 메소드가 서로 다르다고 생각할 수 있지만, **리턴 타입은 메소드를 구분하는 기준으로 사용하지 않는다.**
***

## 객체의 소멸과 가비지 컬렉션

### 객체의 소멸
자바에는 객체를 생성하는 new 연산자는 있지만 객체를 소멸시키는 연산자는 없다. 그러므로 자바에서는 개발자가 마음대로 객체를 소멸시킬 수도 없다.

- 객체 소멸이란 new 연산자에 의해 생성된 객체 공간을 JVM에게 돌려주어 가용 메모리에 포함시키는 것이다. C++의 경우 delete연산자를 실행시켜 객체를 소멸시킨다.(자바에서는 Object클래스의 finalize()가 소멸자와 유사한 기능을 한다.) 자바는 할당받은 메모리를 반환해야 하는 코딩 부담도 없고 소멸자를 작성할 필요도 없다.
- 자바에서 new로 할당받은 후 사용하지 않게 된 객체 메모리는 가비지라고 부르며, JVM의 가비지 컬렉터가 적절한 시점에 자동으로 수집하여 가용 메모리에 반환시킨다.
***

### 가비지
가비지란 자바 응용프로그램에서 더 이상 사용되지 않게 된 객체나 배열 메모리이다. 자바 플랫폼이 가비지를 알아내는 방법은 참조하는 레퍼런스가 하나도 없는 객체나 배열을 가비지로 판단한다. 왜냐하면 이 객체는 응용 프로그램이 더 이상 접근할 수 없기 때문이다.
```java
a = new Person("봄");
b = new Person("여름");
b = a;      // b가 가리키던 객체는 가비지가 됨.
```
- 레퍼런스 b는 a가 가리키던 객체를 가리키게 되고, b가 가리키던 처음 객체는 아무도 참조하지 않게 되어 더 이상 접근할 수 없게 되었다. 이 객체가 바로 가비지이다.

```java
문제! 다음 코드에서 가비지가 되는 것은?

public class Garbage {
    public static void main(String[] args) {
        String a = new String("봄");
        String b = new String("여름");
        String c = new String("가을");
        String d, e;
        a = null;
        d = c;
        c = null;
    }
}
```
***

### 가비지 컬렉션
가비지는 더 이상 참조되지 않기 때문에 가비지가 차지하고 있는 메모리 공간은 회수되어야 한다. 가비지가 많아지게 되면 자바 플랫폼이 응용 프로그램에게 할당해줄 수 있는 가용 메모리 양이 줄어들게 된다. 자바 플랫폼은 가용 메모리가 일정 크기 이하로 줄어들게 되면 자동으로 가비지를 회수하여 가용 메모리를 늘린다. 이것을 가비지 컬렉션이라고 부르며, 가지비 컬렉션은 자바 플랫폼에 의해 준비된 가비지 컬렉션 스레드에 의해 처리된다.  
규모가 큰 자바 프로그램은 실행 중 비교적 많은 양의 가비지를 생산하기 때문에 가비지 컬렉터가 실행되는데, 이때 사용자의 눈에는 프로그램이 중단된 것처럼 보인다. 이런 이유로 자바는 실시간 처리 응용에는 부적합한 것으로 알려져 있다.
***

### 가비지 컬렉션 강제 요청
응용프로그램에서 System 또는 Runtime 객체의 gc() 메소드를 호출하면 가비지 컬렉션을 요청할 수 있다.
```java
System.gc();    // 가비지 컬렉션 강제 요청
```
이 문장을 호출한 즉시 가비지 컬렉터가 작동하는 것은 아니며, 가비지 컬렉션이 필요하다는 요청에 불과하다. 가비지 컬렉션은 자바 플랫폼이 전적으로 판단하여 적절한 시점에 작동시킨다.
***

## 접근 지정자
객체 지향 언어에는 접근 지정자를 두고 있다. 객체를 캡슐화하기 때문에, 객체에 다른 객체가 접근하는 것으로 허용할지, 말지를 지정할 필요가 있기 때문이다.

### 패키지
자바는 서로 관련 있는 클래스 파일들을 패키지에 저장하여 관리하도록 한다. 패키지는 디렉토리, 폴더와 같은 개념이다. 클래스 파일들을 여러 패키지에 분산 관리하는 것이 일반적이다.
***
### 자바의 4가지 접근 지정자
객체 지향 특성을 살리기 위해서는 캡슐화의 원칙이 지켜지도록 가능한 접근 범위를 작게 하여 접근 지정자를 선정하는 것이 좋다. 특히 필드에 대해서는 특별한 이유가 없는 한 public의 사용은 자제하고 가능한 private으로 선언한다. 대신 public 메소드를 만들어 private 필드를 조작하도록 한다. 외부에 공개할 필요가 없는 메소드 역시 public으로 선언하는 것을 자제한다.
- private, protected, public, 접근 지정자 생략(default 접근 지정)
***

### 클래스 접근 지정
클래스 접근 지정이란 다른 클래스에서 이 클래스를 활용할 수 있는지 허용 여부를 지정하는 것을 말한다.
1. public 클래스
   - 클래스 이름 앞에 public으로 선언된 클래스로서, 패키지에 상관없이 다른 어떤 클래스에게도 사용이 허용된다.
```java
public class World {
    ..........
}
```
2. default 클래스(접근 지정자 생략)
   - 접근 지정자 없이 클래스를 선언한 경우, default 접근 지정으로 선언되었다고 한다.
   - default 클래스는 같은 패키지 내의 클래스들에게만 사용이 허용된다.
   - 클래스를 접근할 수 없으면 당연히 그 클래스 내의 멤버도 접근할 수 없다.
```java
class World {
    ..........
}
```
***

### 멤버 접근 지정
멤버에 대한 접근 지정자는 private -> deafult -> protected -> public 순으로 공개의 범위가 넓어진다.

|멤버에 접근하는 클래스|private|default|protected|public|
|---|---|---|---|---|
|같은 패키지의 클래스|X|O|O|O|
|다른 패키지의 클래스|X|X|X|O|
|접근 가능 영역|클래스 내|동일 패키지 내|동일 패키지와 자식 클래스|모든 클래스|

1. public 멤버
   - public 멤버는 패키지를 막론하고 모든 클래스들이 접근 가능하다.
2. private 멤버
   - 비공개를 지시하는 것으로 private 멤버는 클래스 내의 멤버들에게만 접근이 허용된다.
3. protected 멤버
   - 보호된 공개를 지시하는 것으로, 2가지 유형의 클래스에만 접근을 허용한다.
   - 첫째, 같은 패키지의 모든 클래스에 접근이 허용된다.
   - 둘째, 다른 패키지에 있더라도 자식 클래스의 경우 접근이 허용된다.
```java
class A {
    void f() {
        B b = new B();
        b.n = 3;
        b.g();
    }
}

class B {       // 패키지 P
    protected int n;
    protected void g() {
        n = 5;
    }
}

class C {       // 패키지 P
    public void k() {
        B b = new B();
        b.n = 7;
        b.g();
    }
}

class D extends B {
    void f() {
        n = 3;
        g();
    }
}
```
4. default 멤버
   - 접근 지정자가 생략된 멤버의 경우, default 멤버라고 한다. 동일한 패키지 내에 있는 클래스들만 디폴트 멤버를 자유롭게 접근할 수 있다.
***

## static 멤버
예시 : 눈은 사람이라는 객체의 non-static 멤버이며, 공기는 static 멤버이다.(눈은 각 사람마다 있고 공유하지 않지만 공기는 오직 하나만 있고 모든 사람이 공유한다는 차이점이 있다.)

### static 멤버의 선언
```java
class StaticSimple {
    int n;                  // non-static 필드
    void g() {...}          // non-static 메소드 

    static int m;           // static 필드
    static void f() {...}   // static 메소드
}
```
***

### non-static 멤버와 static 멤버의 차이점
<공간적 특성>
- non-static 멤버
  - 멤버는 객체마다 별도 존재
    - 인스턴스 멤버라고도 부름

- static 멤버
  - 멤버는 클래스당 하나 생성
    - 멤버는 객체 내부가 아닌 별도의 공간(클래스 코드가 적재되는 메모리)에 생성
    - 클래스 멤버라고 부름

<시간적 특성>
- non-static 멤버
  - 객체 생성 시에 멤버 생성됨
    - 객체가 생길 때 멤버도 생성
    - 객체 생성 후 멤버 사용 가능
    - 객체가 사라지면 멤버도 사라짐

- static 멤버
  - 클래스 로딩 시에 멤버 생성
    - 객체가 생기기 전에 이미 생성
    - 객체가 생기기 전에도 사용 가능
    - 객체가 사라져도 멤버는 사라지지 않음
    - 멤버는 프로그램이 종료될 때 사라짐

<공유의 특성>
- non-static 멤버
  - 공유되지 않음
    - 멤버는 객체 내에 각각 공간 유지
- static 멤버
  - 동일한 클래스의 모든 객체들에 의해 공유됨
***

### static 멤버의 생성과 활용 1: 객체.static 멤버
```java
<static 멤버를 객체의 멤버로 접근>
class StaticSample {
    public int n;
    public void g() {
        m = 20;
    }
    public void h() {
        m = 30;
    }
    public static int m;
    public static void f() {
        m = 5;
    }
}

public class Ex {
    public static void main(String[] args) {
        StaticSample s1, s2;
        s1 = new StaticSample();
        s1.n = 5;
        s1.g();
        s1.m = 50;
        s2 = new StaticSample();
        s2.n = 8;
        s2.h();
        s2.f();
        System.out.println(s1.m);
    }
}
```
***

### static 멤버의 생성과 활용 2: 클래스명.static 멤버
```java
<static 멤버를 클래스 이름으로 접근>

class StaticSample {
    public int n;
    public void g() {
        m = 20;
    }
    public void h() {
        m = 30;
    }
    public static int m;
    public static void f() {
        m = 5;
    }
}

public class Ex {
    public static void main(String[] args) {
        StaticSample.m = 10;

        StaticSample s1;
        s1 = new StaticSample();
        System.out.println(s1.m);
        s1.f();
        StaticSample.f();
    }
}
```

### static의 활용
1. 전역 변수와 전역 함수를 만들 때 활용
- 응용프로그램 작성 시 모든 클래스에서 공유하는 전역 변수나 모든 클래스에서 호출할 수 있는 전역 함수가 필요한 경우가 있다. static은 이런 문제에 대한 해결책이다.
- static 멤버를 가진 대표적인 클래스로 java.lang.Math 클래스가 있다. 이 클래스는 객체를 생성하지 않고 바로 호출할 수 있는 static 타입의 멤버를 제공한다.
```java
Math m = new Math();    // 오류. 생성자 Math()는 private으로 선언되어 있어 객체 생성이 안 됨.
int n = m.abs(-5);

대신 다음과 같이 클래스 이름 Math로 static 멤버를 직접 호출한다.

int n = Math.abs(-5);
```

2. 공유 멤버를 만들고자 할 때 활용
- static으로 선언된 필드나 메소드는 하나만 생성되어 클래스의 객체들 사이에서 공유된다.
***

### static 메소드의 제약 조건
- static 메소드는 일반 메소드와 달리 다음 두 가지 제약 사항이 있다.
1. static 메소드는 static 멤버만 접근할 수 있다.
    - static 메소드는, 객체 없이도 존재하기 때문에, 객체와 함께 생성되는 non-static 멤버를 사용할 수 없고 static 멤버들만 사용 가능하다. 반면 non-static 메소드는 static 멤버들을 사용할 수 있다.
```java
class StaticMethod {
    int n;
    void f1(int x) {n = x;}
    void f2(int x) {m = x;}
    static int m;
    static void s1(int x) {n = x;}
    static void s2(int x) {f1(3);}
    static void s3(int x) {m = x;}
    static void s4(int x) {s3(3);}
}
```
2. static 메소드는 this를 사용할 수 없다.
    - static 메소드는 객체 없이도 존재하기 때문에, this를 사용할 수 없다.
```java
class StaticAndThis {
    int n;
    static int m;
    void f1(int x) {this.n = x;}
    void f2(int x) {this.m = x;}
    static void s1(int x) {this.n = x;}
    static void s2(int x) {this.m = x;}
}
```
***

## final

### final 클래스
final이 클래스 이름 앞에 사용되면 클래스를 상속받을 수 없을을 지정한다.
```java
final class FinalClass {
    ......
}
class SubClass extends FianlClass {     // 컴파일 오류. FinalClass 상속 불가
    ......
}
```
***

### final 메소드
final로 메소드를 선언하면 오버라이딩할 수 없는 메소드임을 선언한다.
```java
public class SuperClass {
    protected final int finalMethod() { ... }   // finalMethod()는 자식이 오버라이딩 불가
}
class SubClass extends SuperClass {             // SubClass가 SuperClass 상속
    protected int fianlMethod() { ... }         // 컴파일 오류. finalMethod() 오버라이딩 안 됨.
}
```
***

### final 필드
final로 필드를 선언하면 필드는 상수가 된다.
```java
public class FinalFieldClass {
    fianl int ROWS = 10;
    void f() {
        int[] intArray = new int[ROWS];
        ROWS = 30;      // 컴파일 오류. final 필드 값은 변경할 수 없다.
    }
}
```
상수 필드는 한 번 초기화되면 값을 변경할 수 없다. final 키워드를 public static과 함께 선언하면, 프로그램 전체에서 사용할 수 있는 상수가 된다.

```java
PI값을 모든 클래스에서 공유할 수 있는 상수로 선언하기

class SharedClass {
    public static final double PI = 3.14;
}
```
- SharedClass 내에서는 다음과 같이 PI를 사용한다.
```java
double area = PI*radius*radius;
```

- 다른 클래스에서는 다음과 같이 PI를 사용한다.
```java
double area = SharedClass.PI*radius*radius;
```
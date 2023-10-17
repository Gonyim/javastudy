# 5. 상속

## 상속의 개념
객체 지향에서 상속은 부모 클래스에 만들어진 필드와 메소드를 자식 클래스가 물려받는 것이다. 상속 선언을 하면, 자식 클래스는 부모 클래스에 만들어진 필드와 메소드를 만들지 않고도 만든 것과 같은 효과를 얻는다. 상속은 클래스 사이의 상속이지 객체 사이의 상속이 아니다.

### 상속의 필요성
예를 들어 4개의 클래스에 공통된 코드가 각각 다 들어있을 때, 코드를 수정하고 싶다면 4개의 클래스 안에 있는 모든 코드를 수정해야 한다.
***

### 객체 지향에서 상속의 장점
1. 클래스의 간결화 - 멤버의 중복 작성 불필요
2. 클래스 관리 용이 - 클래스들의 계층적 분류
3. 소프트웨어의 생산성 향상 - 클래스 재사용과 확장 용이
***

## 클래스 상속과 객체

### 자바의 상속 선언
```java
public class Person {
    ...
}
public class Student extends Person {   // Person을 상속받는 클래스 Student 선언
    ...
}
public class StudentWorker extends Student {    // Student를 상속받는 클래스 StudentWorkder 선언
    ...
}
```
Student 클래스는 Person 클래스의 멤버를 물려받으므로, Person 클래스에 선언된 필드나 메소드를 다시 반복하여 작성할 필요가 없고, 필드나 메소드를 추가 작성하면 된다. StudentWorker가 Student를 상속받으면 Person 클래스의 멤버도 자동 상속받는다.
***

### 상속과 객체
```java
class Point {
    private int x, y;   // 한 점을 구성하는 x, y 좌표
    public void set(int x, int y) {
        this.x = x;
        this.y = y;
    }
    public void showPoint() {   // 점의 좌표 출력
        System.out.println("("+ x + "," + y + ")");
    }
}

class ColorPoint extends Point {    // Point를 상속받은 ColorPoint 선언
    private String color;           // 점의 색
    public void setColor(String color) {
        this.color = color;
    }
    public void showColorPoint() {  // 컬러 점의 좌표 출력
        System.out.print(color);
        showPoint();    // Point 클래스의 showPoint()호출
    }
}

public class ColorPointEx {
    public static void main(String [] args) {
        Point p = new Point();  // Point 객체 생성
        p.set(1, 2);            // Point 클래스의 set() 호출
        p.showPoint();

        ColorPoint cp = new ColorPoint();   // ColorPoint 객체 생성
        cp.set(3, 4);                       // Point 클래스의 set() 호출
        cp.setColor("red");                 // ColorPoint 클래스의 setColor() 호출
        cp.showColorPoint();                // 컬러와 좌표 출력
    }
}


실행 결과
(1,2)
red(3,4)
```
***

### 상속과 객체 사이의 관계
- 상속 선언
- 서브 클래스 객체 생성
- 서브 클래스 객체 활용
- 서브(자식) 클래스에서 슈퍼(부모) 클래스 멤버 접근
***

### 자바 상속의 특징
1. 자바에서는 클래스의 다중 상속을 지원하지 않는다.(C++에서는 클래스 다중 상속을 지원한다.)
   - 그러므로 extends 다음에는 클래스 이름을 하나만 지정할 수 있다.
2. 자바에서는 상속의 횟수에 제한을 두지 않는다.
3. 자바에서 계층 구조의 최상위에 java.lang.Object 클래스가 있다.
   - 자바에서 모든 클래스는 Object를 상속받도록 선언하지 않아도 Object 클래스를 자동으로 상속받도록 컴파일된다. Object 클래스만이 유일하게 슈퍼(부모)클래스를 가지지 않는다.
   - 따라서 모든 클래스의 조상은 java.lang.Object 이다.
***

## 상속과 protected 접근 지정자

### 슈퍼(부모) 클래스에 대한 접근 지정
슈퍼 클래스 멤버에 대한 접근 지정
|슈퍼 클래스 멤버에 접근하는 클래스 종류|private|default|protected|public|
|---|---|---|---|---|
|같은 패키지에 있는 클래스|X|O|O|O|
|다른 패키지에 있는 클래스|X|X|X|O|
|같은 패키지에 있는 서브 클래스|X|O|O|O|
|다른 패키지에 있는 서브 클래스|X|X|O|O|
(O : 접근 가능, X : 접근 불가)

- 슈퍼(부모)클래스의 private 멤버
  - 부모 클래스의 멤버가 private으로 선언되면, 자식 클래스를 포함하여 다른 어떤 클래스에서도 접근할 수 없다.
- 슈퍼(부모)클래스의 default 멤버
  - 부모 클래스의 멤버가 default로 선언되면, 패키지에 있는 모든 클래스가 접근 가능하다. 자식 클래스라도 다른 패키지에 있다면, 부모 클래스의 default 멤버는 접근할 수 없다.
- 슈퍼(부모)클래스의 public 멤버
  - 부모 클래스의 멤버가 public으로 선언되면, 같은 패키지에 있든 다른 패키지에 있든 모든 클래스에서 접근할 수 있다.
***

### 부모 클래스의 protected 멤버
부모 클래스의 protected 멤버는 두 가지 경우에 접근을 허용한다.  
- default와 protected 비교할 줄 알아야 함!
1. 같은 패키지에 속한 모든 클래스들
2. 같은 패키지든 다른 패키지든 상속받는 서브 클래스

```java
public class A {
    private int pri;
    int def;
    protected int pro;
    public int pub;
}

public class B extends A {
    void set() {
        pri = 1;
        def = 2;
        pro = 3;
        pub = 4;
    }
}
```
- 부모 클래스와 자식 클래스가 동일한 패키지에 있는 경우
  - 부모 클래스의 private 멤버 접근 안 됨
- 부모 클래스와 자식 클래스가 서로 다른 패키지에 있는 경우
  - 부모 클래스의 private, default 멤버 접근 안 됨

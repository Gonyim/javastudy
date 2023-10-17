# 4장 클래스와 객체

## 자바 클래스 만들기
- 클래스 : 클래스는 객체를 만들어 내기 위한 설계도 혹은 틀이다.
- 객체 : 클래스 모양 그대로 생성된 실체가 객체이며, 객체를 클래스의 인스턴스라고도 부른다.
- 붕어빵 틀은 클래스, 붕어빵은 객체라고 할 수 있다.
- 사람을 클래스, 김권이, 김이도, 노희연, 민성철, 이준태는 객체라고 할 수 있다. (이름, 나이, 혈액형, MBTI, 밥 먹기 등 동일한 속성을 가지지만 속성 값은 서로 다르다.)
***

## 클래스 구성
- 클래스는 class 키워드를 사용하여 선언하고, 멤버는 필드(멤버 변수)와 메소드(멤버 함수)이다.

- 원을 추상화한 클래스 Circle을 작성한 코드
```java
public class Circle {   // public : 접근 권한, class : 클래스 선언, Circle : 클래스 이름
    ----------필드(변수)----------
    public int radius;  // 원의 반지름 필드
    public String name; // 원의 이름 필드
    ------------메소드------------
    public Circle() {   // 원의 생성자 메소드
    }
    public double getArea() {   // 원의 면적 계산 메소드
        return 3.14*radius*radius;
    }
}
```
- 클래스 선언
    - class 키워드와 클래스 이름으로 선언하고 중괄호안에 필드와 메소드를 모두 작성한다.
- 필드와 메소드
    - 객체 내에 값을 저장할 멤버 변수를 필드라고 한다. Circle 클래스에는 radius와 name 두 개의 필드가 있다. 메소드 함수이며 객체의 행동을 구현한다. getArea() 메소드는 Circle 객체의 반지름(radius)를 이용하여 면적을 계산하여 알려준다.
- 접근 지정자
    - Circle이나 필드, 메소드에 붙은 public을 접근 지정자라고 한다. public은 다른 클래스에서 활용하거나 접근할 수 있음을 선언한다. 접근 지정자를 생략할 때 디폴트 접근이라고 부른다.
- 생성자(Constructor)
    - 클래스의 이름과 동일한 메소드를 특별히 생성자라고 한다. 생성자는 객체가 생성될 때 자동으로 호출되는 특별한 메소드이다.
    - 쉽게 말해 객체가 생성될 때 필드를 초기화하거나 생성 당시에 꼭 필요한 작업을 위해 두는 것이다.

```java
public class Circle {
    public int radius;
    public String name;
        
    public Circle() {
    }

    public double getArea() {
        return 3.14 * radius * radius;
        }
}
    
public static void main(String[] args) {
    Circle pizza = new Circle();
        
    pizza.radius = 10;
    pizza.name = "얼굴을 피자";
    double area = pizza.getArea();
}
```
***

## 생성자
- 생성자는 객체가 생성될 때 객체의 초기화를 위해 실행되는 메소드이다.
- 모든 객체 지향 언어에 존재한다.
- 생성자는 객체가 생성되는 순간에 자동으로 호출되는 메소드로서, 객체에 필요한 초기화를 실행하는 코드를 담아야 한다.

```java
public class Circle {
    public int radius;
    public String name;

    public Circle() {
        radius = 1;
        name = "";
    }

    public Circle(int r, String n) {
        radius = r;
        name = n;
    }

    public double getArea() {
        return 3.14 * radius * radius;
    }

    public static void main(String[] args) {
        Circle pizza = new Circle(10, "피자");

        double area = pizza.getArea();
        System.out.println(pizza.name + "의 면적은 " + area);

        Circle donut = new Circle();
        donut.name = "도넛";
        area = donut.getArea();
        System.out.println(donut.name + "의 면적은 " + area);
    }
}
```
***

### 생성자의 특징
1. 생성자의 이름은 클래스 이름과 동일하게 작성해야 한다.
2. 생성자는 여러 개 작성(오버로딩)할 수 있다.
3. 생성자는 new를 통해 객체를 생성할 때 한 번만 호출된다. => 객체 생성은 반드시 new를 통해서만 이루어지며, 이때 생성자는 자동으로 한번만 호출된다.
4. 생성자에 리턴 타입을 지정할 수 없다. => 리턴 값이 없다고 해서, void를 리턴 타입으로 지정하면 안 된다.
```java
public void Circle() {
}
```
5. 생성자의 목적은 객체가 생성될 때, 필요한 초기 작업을 위함이다.
6. **생성자는 객체가 생성될 때 반드시 호출된다.** => 그러므로 하나 이상 선언되어야 하며, 개발자가 생성자를 작성하지 않았을 경우 컴파일러가 자동으로 기본 생성자를 삽입해준다.
***

### 기본 생성자
- 기본 생성자란 매개변수와 실행 코드가 없어 아무 일도 하지 않고 단순 리턴하는 생성자이다. 디폴트 생성자라고도 부른다.
```java
class Circle {
    public Circle() {
    }
}
```
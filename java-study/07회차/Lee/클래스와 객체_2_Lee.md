# 4장 클래스와 객체

## 기본 생성자

### 기본 생성자가 자동으로 생성되는 경우
- 객체가 생성될 때 반드시 생성자가 실행되기 때문에 생성자가 없는 클래스는 있을 수 없다.
```java
# 생성자가 하나도 만들어져 있지 않은 클래스
public class Circle {
    int radius;
    void set(int r) { radius = r; }
    double getArea() { return 3.14*radius*radius; }

    public static void main(String[] args) {
        Circle pizza = new Circle();
        pizza.set(2);
    }
}

# 자바 컴파일러에 의해 자동으로 기본 생성자 삽입
public class Circle {
    int radius;
    void set(int r) { radius = r; }
    double getArea() { return 3.14*radius*radius; }

    public Circle() {}   // 자동 삽입된 기본 생성자

    public static void main(String[] args) {
        Circle pizza = new Circle();    // 호출
        pizza.radius(2);
    }
}
```

### 기본 생성자가 자동으로 생성되지 않은 경우
- 생성자가 하나라도 존재하는 클래스에는 컴파일러가 기본 생성자를 삽입해 주지 않는다.
```java
public class Circle {
    int radius;
    void set(int r) { radius = r; }
    double getArea() { return 3.14*radius*radius; }
    
    public Circle(int r) {      // 생성자가 있기 때문에 기본 생성자 자동 생성하지 않음
        radius = r;
    }

    public static void main(String[] args) {
        Circle pizza = new Circle(10);      // 호출 가능
        Circle donut = new Circle();        // 오류
    }
}
```
- 기본 생성자를 자동 생성하지 않는 것은 클래스를 만든 개발자의 의도를 지켜주기 위함이다.
- Circle 클래스에 Circle(int r)생성자가 있다는 것은, 객체를 생성할 때 new Circle(10)과 같이 반드시 반지름 값으로 초기화하도록 강제하고 있다는 의미이다. 즉 반지름 값 없이 new Circle()로 객체를 생성하지 말라는 개발자의 뜻이다. 따라서 자바 컴파일러는 Circle 클래스의 의도를 훼손하지 않기 위해 기본 생성자를 자동으로 생성해주지 않는다.

## this 레퍼런스
- this는 자바의 중요한 키워드로서 객체 자신을 가리키는 레퍼런스이다.
1. this는 객체 자신에 대한 레퍼런스이다.
2. this와 this()는 다르다.
3. this는 메소드에서 사용되며 현재 객체를 가리킨다.
4. static 메소드에서는 사용할 수 없다.

### this의 개념
- this는 현재 객체 자신에 대한 레퍼런스이다. 정확히 말하면 현재 실행되고 있는 메소드가 속한 객체에 대한 레퍼런스이다.

```java
this를 사용하는 전형적인 예
public class Circle {
    int radius;     // 멤버 radius
    public Circle(int r) { this.radius = r; }   // this.radius는 현재 객체의 멤버 radius를 접근한다.
    public int getRadius() { return radius; }   // return this.radius; 와 동일
}
```
***

### this의 필요성
앞의 예시에서 Circle 클래스에서 메소드 getRadius()는 this를 사용하지 않았다. 클래스 내에서 멤버 radius를 접근할 때는 굳이 this.radius로 할 필요가 없다.

매개변수의 이름은 그 자체로서 코드를 읽는 사람에게 용도를 나타내므로 적합한 이름을 붙여줘야 한다. 따라서 Circle(int r) 생성자의 매개변수를 r 대신 radius로 변경하는 것이 좋다.
```java
public class Circle {
    int radius;     // 멤버 radius
    public Circle(int radius) { radius = radius; }
}
```
하지만 이렇게 변경했을 경우 문제가 생긴다.

2개의 radius가 모두 Circle(int radius)의 매개변수 radius에 접근하기 때문에 멤버 radius를 변경하지 못한다.
이때 다음과 같이 this를 이용하면 된다.

```java
public class Circle {
    int radius;
    public Circle(int radius) { this.radius = radius; }     // this.radius : 멤버 radius, radius : 매개변수 radius
}
```

- 메소드가 객체 자신의 레퍼런스를 리턴해야 하는 경우
```java
public Circle getMe() { return this; }  // getMe() 메소드는 객체 자신의 레퍼런스를 리턴한다.
```
***

### this의 상세 설명
```java
public class Circle {
    int radius;
    public Circle(int radius) {
        this.radius = radius;
    }
    public void set(int radius) {
        this.radius = radius;
    }

    public static void main(String[] args) {
        Circle ob1 = new Circle(1);
        Circle ob2 = new Circle(2);
        Circle ob3 = new Circle(3);

        ob1.set(4)
        ob2.set(5)
        ob3.set(6)
    }
}
```
- main()는 3개의 Circle 객체를 생성한다. 객체가 있어야 this를 사용할 수 있다.
***

## this()로 다른 생성자 호출
- this()는 클래스 내에서 생성자가 다른 생성자를 호출할 때 사용하는 코드이다.
```java
public class Book {
    String title;
    String author;

    void show() { System.out.println(title + " " + author); }

    public Book() {
        this("", "");
        System.out.println("생성자 호출됨");
    }

    public Book(String title) {     // 다음 this문 실행
        this(title, "작자미상");    // 멤버 title과 author는 춘향전과 작자미상으로 초기화된다.
    }

    public Book(String title, String author) {
        this.title = title;
        this.author = author;
    }

    public static void main(String [] args) {
        Book littlePrince = new Book("어린왕자", "생텍쥐페리");
        Book loveStory = new Book("춘향전");
        Book emptyBook = new Book();
        loveStory.show();
    }
}
```
***

### this() 사용 시 주의사항
- this()는 반드시 **생성자 코드에서만 호출**할 수 있다.
- this()는 반드시 **같은 클래스 내 다른 생성자를 호출**할 때 사용된다.
- **this()는 반드시 생성자의 첫 번째 문장이 되어야 한다.**
```java
public Book() {
    System.out.println("생성자 호출됨");
    this("", "");   // 컴파일 오류. this()는 생성자의 첫 번째 문장이어야 한다.
}
```
***

### 객체 치환 시 주의할 점
```java
public class Circle {
    int radius;
    public Circle(int radius) { this.radius = radius; }
    public void set(int radius) { this.radius = radius; }

    public static void main(String [] args) {
        Circle ob1 = new Circle(1);
        Circle ob2 = new Circle(2);
        Circle s;

        s = ob2;
        ob1 = ob2;
        System.out.println("ob1.radius=" + ob1.radius);
        System.out.println("ob2.radius=" + ob2.radius);
    }
}
```
- ob1의 레퍼런스가 ob2의 레퍼런스와 동일하게 되어 ob2의 객체를 함께 가리키게 된다. 그러고 나면 원래 ob1이 가리키던 객체는 아무도 가리키지 않게 되어 프로그램에서 접근할 수 없는 상태가 된다. 이 객체를 가비지라고 부른다. 가비지는 자바 가상 머신에 의하여 자동으로 수거되어 재사용된다.
***

## 객체 배열
- 자바에서는 기본 타입 데이터뿐 아니라, 객체를 원소로 하는 객체 배열도 만들 수 있다. C/C++과 달리, 자바의 객체 배열은 객체에 대한 레퍼런스를 원소로 갖는 배열이다.

```java
Circle [] c;        // Circle 배열에 대한 레퍼런스 변수 c 선언
c = new Circle[5];  // 레퍼런스 배열 생성

for(int i=0; i<c.length; i++)
    c[i] = new Circle(i);   // 배열의 각 원소 객체 생성
```
***

### 배열 선언 및 생성
객체 배열을 만드는 과정을 예시로 설명

1. 배열에 대한 레퍼런스 선언
```java
Circle [] c;

Circle [5] c;   // 오류. 배열의 크기를 지정하면 컴파일 오류가 발생한다.
```
***

2. 레퍼런스 배열 생성
- 배열의 원소는 객체가 아니라 레퍼런스이다.
- Circle 객체에 대한 레퍼런스 배열이 생성되며, 변수 c가 이를 가리킨다. Circle 개체들은 아직 존재하지 않는다.
```java
c = new Circle[5];  // Circle 객체에 대한 레퍼런스 5개 생성
```
***

3. 객체 생성
- Circle 객체를 하나씩 생성하여 배열 c[]의 각 레퍼런스에 대입한다.
- 배열의 크기만큼 Circle 객체를 생성하여 레퍼런스 배열에 하나씩 대입한다.
```java
for(int i=0; i<c.length; i++)   // c.length는 배열 c의 크기로서 5
    c[i] = new Circle(i);       // i번째 Circle 객체 생성
```
***

### 배열의 원소 객체 접근
배열 c의 i번째 객체에 접근하기 위해서는 c[i] 레퍼런스를 사용하면 된다.
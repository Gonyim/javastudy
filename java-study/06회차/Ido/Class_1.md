# 클래스 \[1/2]

<br>

## 객체 지향 프로그래밍
### 객체란?

![object-in-java](https://velog.velcdn.com/images/kid/post/0dd420ad-3aee-4dda-a004-4777a693d93f/image.png)

객체(Object)란 물리적으로 존재하거나 추상적으로 생각할 수 있는 것 중에서 자신의 속성을 가지고 있고 다른 것과 식별 가능한 것을 말합니다. 예를 들어 물리적으로 존재하는 자동차, 자전거, 책, 사람과 추상적인 학과, 강의, 주문 등이 모두 객체가 될 수 있습니다. 객체는 속성과 동작으로 구성되어 있습니다. 예를 들어 사람은 이름, 나이 등의 속성과 웃다, 걷다 등의 동작이 있고, 자동차는 색상, 모델명 등의 속성과 달린다, 멈춘다 등의 동작이 있습니다. 자바는 이 속성과 동작들을 각각 필드(field)와 메소드(method)라고 부릅니다.

<br>

### 객체의 상호작용
객체의 상호작용은 객체 간의 메소드 호출을 의미하며 매개값과 리턴값을 통해서 데이터를 주고 받는 것을 의미합니다. 현실 세계에서 일어나는 모든 현상은 객체와 객체 간의 상호작용으로 이루어져 있습니다. 예를 들어 사람은 계산기의 기능을 이용하고, 계산기는 계산 결과를 사람에게 알려주는 상호작용을 합니다. 소프트웨어에서도 마찬가지로 객체들은 각각 독립적으로 존재하고, 다른 객체와 서로 상호작용 하면서 동작합니다. 이때 객체들 사이의 상호작용 수단이 메소드이고, 객체가 다른 객체의 기능을 이용하는 것이 메소드 호출입니다.

```java
리턴값 = 계산기객체.메소드(매개값1, 매가값2, ...);
int result = Calculator.add(10, 20);
```

메소드 호출은 위와 같은 형태를 가지고 있습니다. 객체에 도트(.) 연산자를 붙이고 메소드 이름을 작성하면 됩니다. 도트 연산자는 객체의 필드와 메소드에 접근할 때 사용됩니다. 리턴값은 메소드가 실행되고 호출한 곳으로 돌려주는 값이고, 매개값은 메소드를 실행하기 위해 필요한 데이터입니다.

<br>

### 객체 간의 관계

![객체-간의-관계](https://velog.velcdn.com/images/kid/post/282e6b84-669a-46df-97c5-4667f1162d8c/image.png)

객체는 개별적으로 사용될 수 있지만, 대부분 다른 객체와 관계를 맺고 있습니다. 이 관계의 종류에는 집합 관계, 사용 관계, 상속 관계가 있습니다. 

- 집합 관계: 자동차가 엔진, 타이어, 핸들 등으로 구성된 것처럼 완성품과 부품의 관계
- 사용 관계: 사람이 자동차를 사용하듯이 객체 간의 상호작용을 의미
- 상속 관계: 상위(기계) 객체를 기반으로 하위(자동차) 객체를 생성하는 관계

<br>

### 객체 지향 프로그래밍의 특징
#### 캡슐화 Encapsulation

![encapsulation-in-java](https://velog.velcdn.com/images/kid/post/c251c4c4-dc90-461d-ae6b-740fe43c04c6/image.png)

캡슐화란 객체의 필드, 메소드를 하나로 묶고, 실제 구현 내용을 감추는 것을 말합니다. 외부 객체는 객체 내부의 구조를 알지 못하며 객체가 제공하는 필드와 메소드만 이용할 수 있습니다. 이렇게 필드와 메소드를 캡슐화하여 보호하는 이유는 외부의 잘못된 사용으로 인해 객체가 손상되지 않도록 하는데 있습니다. 자바는 접근 제한자(Access Modifier)를 사용해서 객체의 필드와 메소드의 사용 범위를 제한할 수 있습니다.

##### 접근 제한자

|접근 제한|	적용 대상|	접근할 수 없는 클래스|
|:---:|:---:|:---:|
|public|클래스, 필드, 생성자, 메소드|없음|
|protected|필드, 생성자, 메소드|자식 클래스가 아닌 다른 패키지에 소속된 클래스|
|default|클래스, 필드, 생성자, 메소드|다른 패키지에 소속된 클래스|
|private|필드, 생성자, 메소드|모든 외부 클래스|

#### 상속 Inheritance

![inheritance-in-java](https://velog.velcdn.com/images/kid/post/54b89d81-0fb5-4882-9591-fd658dfb91b5/image.png)

상속은 상위 객체를 재사용해서 하위 객체를 쉽고 빨리 설계할 수 있도록 도와줍니다. 필드1, 필드2, 메소드1, 메소드2를 가지는 객체를 설계한다고 했을 때, 이미 필드1과 메소드1이 있는 객체가 있다면 이것을 상속하고 필드2와 메소드2만 설계하는 것이 효율적입니다. 상속은 상위 객체의 수정 사항을 모든 하위 객체에게 적용하므로 유지 보수에 들어가는 시간을 최소화시켜주기도 합니다.

#### 다형성 Polymorphism

![polymorphism-in-java](https://velog.velcdn.com/images/kid/post/2c78f5dd-7f34-4149-a018-02466a0080d6/image.png)

다형성은 같은 타입이지만 실행 결과가 다양한 객체를 이용할 수 있는 성질을 말합니다. 다형성은 하나의 타입에 여러 객체를 대입함으로써 다양한 기능을 이용할 수 있도록 해주고 객체의 부품화를 가능하게 합니다. 예를 들어 자동차를 설계할 때 타이어 인터페이스 타입을 적용했다면 이 인터페이스를 구현한 실제 타이어들은 어떤 것이든 상관없이 장착(대입)이 가능합니다. 자바는 다형성을 위해 부모 클래스 또는 인터페이스의 타입 변환을 허용합니다.

##### 예제

```java
class Polymorph { 
  
    void operator(String str1, String str2) 
    { 
        String s = str1 + str2; 
        System.out.println("Concatenated String = " + s); 
    } 
  
    void operator(int a, int b) 
    { 
        int c = a + b; 
        System.out.println("Sum = " + c); 
    } 
} 
  
class Main { 
    public static void main(String[] args) 
    { 
        ComplitetimePolymorph obj = new ComplitetimePolymorph();
        obj.operator("Hey", "Prepster");
        obj.operator(10, 20);
    } 
} 

```

<br>

## 객체 생성과 클래스 변수

```java
new 클래스();
```

new는 클래스로부터 객체를 생성시키는 연산자입니다. new 연산자 뒤에는 생성자가 오는데, 생성자는 클래스() 형태를 가지고 있습니다. new 연산자로 생성된 객체는 메모리 힙 영역에 생성됩니다. 현실 세계에서 물건의 위치를 모르면 사용할 수 없듯이, 프로그램에서도 메모리 내에 생성된 객체의 위치를 모르면 사용할 수 없기 때문에 new 연산자는 객체를 생성시킨 후 객체의 주소를 리턴합니다. 이 주소를 참조 타입인 클래스 변수에 저장해 두면 변수를 통해 객체를 사용할 수 있습니다.

#### 예제

```java
class Student {
}

public class Main {
	public static void main(String[] args) {
    	Student s = new Student();
        System.out.println("변수가 String 객체를 참조합니다.");
    }
}
```

클래스는 두 가지 용도가 있습니다. 하나는 라이브러리(API) 용이고 다른 하나는 실행용입니다. 라이브러리 클래스는 다른 클래스에서 이용할 목적으로 설계됩니다. 프로그램 전체에서 사용되는 클래스가 100개라면 99개는 라이브러리이고 단 하나가 실행 클래스입니다. 실행 클래스는 프로그램의 실행 진입점인 main() 메소드를 제공하는 역할을 합니다.

<br>

### 클래스의 구성 멤버

```java
public class ClassName {
	// 필드 Field: 객체의 데이터가 저장되는 곳
    int fieldName;
    
    // 생성자 Constructor: 객체 생성 시 초기화 역할 담당
    ClassName() { ... }
    
    // 메소드 Metohd: 객체의 동작에 해당하는 실행 블록
    void methodName() { ... }
```

클래스에는 객체가 가져야 할 구성 멤버가 선언됩니다. 구성 멤버에는 필드, 생성자, 메소드가 있습니다. 이 구성 멤버들은 생략되거나 복수 개가 작성될 수 있습니다.

<br>

## 필드
필드는 객체의 고유 데이터, 부품 객체, 상태 정보를 저장하는 곳입니다. 선언 형태는 변수와 비슷하지만 필드를 변수라고 부르지는 않습니다. 변수는 생성자와 메소드 내에서만 사용되고 생성자와 메소드가 실행 종료되면 자동 소멸되지만, 필드는 생성자와 메소드 전체에서 사용되며 객체가 소멸되지 않는 한 객체와 함께 존재합니다.

### 필드 선언
필드 선언은 클래스 중괄호 블록 어디서든 존재할 수 있습니다. 생성자 선언과 메소드 선언의 앞과 뒤 어디든 상관없이 선언이 가능합니다. 하지만 생성자와 메소드 중괄호 블록 내부에 선언하면 로컬 변수가 되기 때문에 주의해야 합니다. 필드 선언은 변수의 선언 형태와 동일합니다.

```java
String company = "현대자동차";
int maxSpeed = 300;
boolean engineStart;
```

<br>

### 필드 사용
클래스 내부의 생성자나 메소드에서 사용할 경우 단순히 필드 이름으로 읽고 변경하면 되지만, 클래스 외부에서 사용할 경우 우선적으로 클래스로부터 객체를 생성한 뒤 필드를 사용해야 합니다. 그 이유는 필드는 객체에 소속된 데이터이므로 객체가 존재하지 않으면 필드도 존재하지 않기 때문입니다.

#### 예제

```java
public class Car {
	// 필드
    String company = "현대자동차";
    String model = "아반떼";
    String color = "검정";
    int maxSpeed = 350;
    int speed;
}

public class CarExample {
	public static void main(String[] args) {
    	// 객체 생성
        Car myCar = new Car();
        
        // 필드값 읽기
        System.out.println("현재속도: " + myCar.speed);
        
        // 필드값 변경
        myCar.speed = 60;
        System.out.println("현재속도: " + myCar.speed);
    }
}
```

<br>

## 생성자
생성자는 new 연산자와 같이 사용되어 클래스로부터 객체를 생성할 때 호출되어 객체의 초기화를 담당합니다. 객체 초기화는 필드를 초기화하거나 메소드를 호출해서 객체를 사용할 준비를 하는 것을 의미합니다. 생성자를 실행시키지 않고는 클래스로부터 객체를 만들 수 없습니다.

### 기본 생성자
모든 클래스는 생성자가 반드시 존재하며 하나 이상을 가질 수 있습니다. 생성자 선언을 생략했다면 컴파일러가 기본 생성자`[public] 클래스() {}`를 바이트 코드에 자동으로 추가시킵니다.

<br>

### 생성자 선언

```java
클래스(매개 변수 선언, ... ) {
	// 객체의 초기화 코드
}
```

생성자는 메소드와 비슷한 모양을 가지고 있지만 리턴 타입이 없고 클래스 이름과 동일합니다. 객체의 초기화 코드 부분에는 필드에 초기값을 저장하거나 메소드를 호출하여 객체 사용 전에 필요한 준비를 합니다. 매개 변수는 new 연산자로 생성자를 호출할 때 외부의 값을 생성자 블록 내부로 전달하는 역할을 하게 됩니다.

#### 예제

```java
public class Car {
	// 생성자
    Car(String Color, int cc) {
    }
}

public class CarExample {
	public static void main(String[] args) {
    	Car myCar = new Car("검정", 3000);
        // Car myCar = new Car(); 생성자를 명시적으로 선언해줬기 때문에 기본 생성자 호출 불가
    }
}
```

<br>

### 필드 초기화
객체가 생성될 때 필드는 기본 초기값으로 자동 설정이 되는데, 만약 다른 값으로 초기화를 하고 싶다면 두 가지 방법이 있습니다. 필드를 선언할 때 초기값을 주는 방법과 생성자에서 초기값을 주는 방법입니다. 객체 생성 시점에 외부에서 제공되는 다양한 값들로 초기화되어야 한다면 두 번째 방법을 사용할 수 있습니다.

#### 예제

```java
public class Korean {
	// 필드
    String nation = "대한민국";
    String name;
    Stirng ssn;
    
    // 생성자
    public Korean(String n, String s) {
    	name = n;
        ssn = s;
    }
}

public class KoreanExample {
	public static void main(String[] args) {
    	Korean k1 = new Korean("박자바", "011225-1234567");
        System.out.println("k1.name : " + k1.name);
        System.out.println("k1.ssn : " + k1.ssn);
        
        Korean k2 = new Korean("김자바", "930525-0654321");
        System.out.println("k2.name : " + k2.name);
        System.out.println("k2.ssn : " + k2.ssn);
```

위 예제처럼 매개 변수의 이름이 너무 짧으면 코드의 가독성이 좋지 않기 때문에 가능하면 초기화시킬 필드 이름과 비슷하거나 동일한 이름을 사용하는 것이 좋습니다. 관례적으로는 필드와 동일한 이름을 사용합니다. 이 경우 동일한 이름의 매개 변수가 사용 우선순위가 높기 때문에 생성자 내부에서 해당 필드에 접근할 수 없습니다. 이때 필드 앞에 객체 자신의 참조인 "this."를 붙여서 사용하는 것으로 해결이 가능합니다.

```java
public Korean(String name, String ssn) {
	this.name = name;
    this.ssn = ssn;
}
```

<br>

### 생성자 오버로딩
Car 객체를 생성할 때 외부에서 제공되는 데이터가 없다면 기본 생성자로 Car 객체를 생성해야 하고, 외부에서 model, color 데이터 등이 제공될 경우에도 Car 객체를 생성할 수 있어야 합니다. 생성자가 하나뿐이라면 이러한 요구 조건을 수용할 수 없기 때문에 자바는 생성자 오버로딩을 제공합니다. 생성자 오버로딩이란 매개 변수를 달리하는 생성자를 여러 개 선언하는 것을 의미합니다.

```java
public class Car {
	Car() { ... }
    Car(String model) { ... }
    Car(String model, String color) { ... }
    Car(String model, String color, int maxSpeed) { ... }
    
    // 오버로딩이 아님
    Car(String model, String color) { ... }
    Car(String color, String model) { ... }
}
```

#### 예제

```java
public class Car {
	// 필드
    String company = "현대자동차";
    String model;
    String color;
    int maxSpeed;
    
    // 생성자
    Car() {
    }
    
    Car(String model) {
    	this.model = model;
    }
    
    Car(String model, String color) {
    	this.model = model;
        this.color = color;
    }
    
    Car(String model, String color, int maxSpeed) {
    	this.model = model;
        this.color = color;
        this.maxSpeed = maxSpeed;
    }
}

public class CarExample {
	public static void main(String[] args) {
    	Car car1 = new Car();
        Car car2 = new Car("자가용");
        Car car3 = new Car("자가용", "빨강");
        Car car4 = new Car("택시", "검정", 200);
    }
}
```

<br>

### 다른 생성자 호출
생성자 오버로딩이 많아질 경우 생성자 간의 중복된 코드가 발생할 수 있는데, 이 경우 필드 초기화 내용은 한 생성자에만 집중적으로 작성하고 나머지 생성자는 그 생성자를 호출하는 방법으로 개선할 수 있습니다. 생성자에서 다른 생성자를 호출할 때에는 다음과 같이 this() 코드를 사용합니다. this()는 반드시 생성자의 첫줄에서만 사용할 수 있습니다.

```java
클래스( {매개변수선언, ... } ) {
	this( 매개변수, ..., 값, ... ); // 클래스의 다른 생성자 호출
    실행문;
}
```

```java
// this() 사용 전
Car(String model) {
	this.model = model;
    this.color = "은색";
    this.maxSpeed = 250;
}

Car(String model, String color) {
	this.model = model;
    this.color = color;
    this.maxSpeed = 250;
}

Car(String model, String color, int maxSpeed) {
	this.model = model;
    this.color = color;
    this.maxSpeed = maxSpeed;
}

// this() 사용 후
Car(String model) {
	this(model, "은색", 250);
}

Car(String model, String color) {
	this(model, color, 250);
}

Car(String model, String color, int maxSpeed) {
	this.model = model;
    this.color = color;
    this.maxSpeed = maxSpeed;
}
```

<br>

## 메소드
메소드는 객체의 동작에 해당하는 중괄호 블록을 말합니다. 메소드를 호출하게 되면 중괄호 블록에 있는 모든 코드들이 일괄적으로 실행됩니다. 메소드는 객체 간의 데이터 전달 수단으로 사용됩니다. 외부로부터 매개값을 받을 수도 있고, 실행 후 어떤 값을 리턴할 수도 있습니다.

### 메소드 선언
메소드 선언은 선언부(리턴타입, 메소드이름, 매개변수선언)와 실행 블록으로 구성됩니다.

```java
리턴타입 메소드이름(매개변수선언) {
	실행 블록
}
```

#### 리턴 타입
리턴값이 없는 메소드는 리턴 타입에 void, 리턴값이 있는 메소드는 리턴값의 타입을 입력합니다. 리턴값이 있느냐 없느냐에 따라 메소드를 호출하는 방법도 조금 달라집니다.

```java
void powerOn() { ... }
double divide(int x, int y) { ... }

// 호출
powerOn();
double result = divide(10, 20);

// 리턴값이 중요하지 않고 메소드 실행이 중요하다면 생략 가능
divide(10, 20);
```

#### 매개 변수의 수를 모를 경우
메소드를 선언할 때 매개 변수의 개수를 알 수 없는 경우가 있는데, 해결책은 매개 변수를 배열 타입으로 선언하는 것입니다.

```java
int sum1(int[] values) {}

// 1:
int[] values = {1, 2, 3};
int result = sum1(values);

// 2:
int result = sum1(new int[] {1, 2, 3, 4, 5});
```

매개 변수를 배열 타입으로 선언하면 메소드를 호출하기 전에 위 코드처럼 배열을 생성해야 하는 불편한 상황이 생깁니다. 그래서 배열을 생성하지 않고 리스트만 넘겨주는 방법도 있습니다. 다음과 같이 sum2() 메소드의 매개 변수를 "..." 을 사용해서 선언하게 되면 넘겨준 값의 수에 따라 자동으로 배열을 생성합니다.

```java
int sum2(int ... values) {}

int result = sum2(1, 2, 3);
```

<br>

### 리턴문
#### 리턴값이 있는 메소드
리턴 타입이 있는 메소드는 return문을 사용해서 값을 지정해야 합니다. 만약 return문이 없다면 컴파일 오류가 발생하고, return문이 실행되면 메소드는 즉시 종료됩니다.

```java
return 리턴값;
```

#### 리턴값이 없는 메소드
void로 선언된 리턴값이 없는 메소드에서도 return문을 사용할 수 있습니다. 다음과 같이 return문을 사용하면 메소드 실행을 강제 종료시킵니다.

```java
return;
```

<br>

### 메소드 호출
#### 객체 내부에서 호출
클래스 내부에서 다른 메소드를 호출할 경우에는 다음과 같은 형태로 작성합니다.

```java
메소드(매개값, ... );

// 리턴값이 있는 메소드를 호출하고 리턴값을 받고 싶다면
타입 변수 = 메소드(매개값, ... );
```

##### 예제

```java
class Calculator {
    int plus(int x, int y) {
        int result = x + y;
        return result;
    }

    double avg(int x, int y) {
        double sum = plus(x, y);
        double result = sum / 2;
        return result;
    }

    void execute() {
        double result = avg(7, 10);
        println("실행결과: " + result);
    }

    void println(String message) {
        System.out.println(message);
    }
}

public class Main {
    public static void main(String[] args) {
        Calculator cal = new Calculator();
        cal.execute();
    }
}
```

#### 객체 외부에서 호출
외부 클래스에서 메소드를 호출하는 방법은 다음과 같습니다.

```java
클래스 참조변수 = new 클래스(매개값, ... );
참조변수.메소드(매개값, ... ); // 리턴값이 없거나, 있어도 리턴값을 받지 않을 경우
타입 변수 = 참조변수.메소드(매개값, ... ); // 리턴값이 있고, 리턴값을 받고 싶을 경우
```

<br>

### 메소드 오버로딩
클래스 내에 같은 이름의 메소드를 여러 개 선언하는 것을 메소드 오버로딩이라고 합니다. 메소드 오버로딩의 조건은 매개 변수의 타입, 개수, 순서 중 하나가 달라야 합니다. 메소드 오버로딩이 필요한 이유는 매개값을 다양하게 받아 처리할 수 있도록 하기 위해서입니다.

```java
class 클래스 {
	리턴 타입 메소드이름 (타입 변수, ... ) { ... }
    // 무관 | 동일 | 매개 변수의 타입, 개수, 순서가 달라야 함
    리턴 타입 메소드이름 (타입 변수, ... ) { ... }
}
```

메소드 오버로딩의 가장 대표적인 예는 System.out.println() 메소드입니다. println() 메소드는 호출할 때 주어진 매개값의 타입에 따라서 오버로딩된 메소드를 호출합니다.

```java
void println() { ... }
void println(boolean x) { ... }
void println(char x) { ... }
void println(char[] x) { ... }
void println(double x) { ... }
void println(float x) { ... }
void println(int x) { ... }
void println(long x) { ... }
void println(Object x) { ... }
void println(String x) { ... }
```

#### 예제

```java
class Calculator {
    // 정사각형 넓이
    double areaRectangle(double width) {
        return width * width;
    }

    // 직사각형 넓이
    double areaRentangle(double width, double height) {
        return width * height;
    }
}

public class Main {
    public static void main(String[] args) {
        Calculator cal = new Calculator();

        // 정사각형 넓이 구하기
        double result1 = cal.areaRectangle(10);

        // 직사각형 넓이 구하기
        double result2 = cal.areaRentangle(10, 20);
    }
}
```

<br>

## 레퍼런스
- 이것이 자바다: 신용권의 Java 프로그래밍 정복
- Class and Object Concept in Java: https://www.atnyla.com/tutorial/class-and-object-concept/0/53
- 그놈의 객체지향 프로그래밍(OOP)이란?: https://likelionsungguk.github.io/20-12-24/%EA%B0%9D%EC%B2%B4%EC%A7%80%ED%96%A5-%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D%28OOP%29%EC%9D%B4%EB%9E%80
- 객체 지향 프로그래밍의 4가지 특징ㅣ추상화, 상속, 다형성, 캡슐화: https://www.codestates.com/blog/content/%EA%B0%9D%EC%B2%B4-%EC%A7%80%ED%96%A5-%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D-%ED%8A%B9%EC%A7%95
- Encapsulation in Java: https://prepinsta.com/java/encapsulation/
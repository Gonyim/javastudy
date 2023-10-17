# 클래스 \[2/2]

<br>

## 인스턴스 멤버와 this

- **인스턴스 멤버**: 객체를 생성한 후 사용할 수 있는 필드와 메소드
- **this**: 객체 외부에서 인스턴스 멤버에 접근하기 위해 참조 변수를 사용하듯이 객체 내부에서는 인스턴스 멤버에 접근하기 위해 this를 사용

#### 예제

```java
class Car {
    // 필드
    String model;
    int speed;

    // 생성자
    Car(String model) {
        this.model = model;
    }

    //메소드
    void setSpeed(int speed) {
        this.speed = speed;
    }

    void run() {
        for (int i=10; i <= 50; i+=10) {
            this.setSpeed(i);
            System.out.println(this.model + "가 달립니다.(시속:" + this.speed + "km/h)");
        }
    }
}

public class Main {
    public static void main(String[] args) {
        Car myCar = new Car("포르쉐");
        Car yourCar = new Car("벤츠");

        myCar.run();
        yourCar.run();
    }
}
```

<br>

## 정적 멤버와 static

- **정적 멤버**: 클래스에 고정된 멤버로서 객체를 생성하지 않고 사용할 수 있는 필드와 메소드
(객체 소속이 아닌 클래스 소속이기 때문에 클래스 멤버라고도 함)

### 정적 멤버 선언

```java
public class 클래스 {
	// 정적 필드
    static 타입 필드 [= 초기값];
    
    // 정적 메소드
    static 리턴 타입 메소드(매개변수선언, ... ) { ... }
}
```

정적 멤버는 클래스에 고정되어있어서 클래스 로더가 바이트 코드(클래스)를 로딩해서 메소드 메모리 영역에 적재할 때 클래스별로 관리됩니다. 따라서 클래스의 로딩이 끝나면 바로 사용할 수 있습니다.

<br>

### 정적 멤버 사용

```java
클래스.필드;
클래스.메소드(매개값, ... );
```

정적 멤버는 원칙적으로 클래스 이름으로 접근해야 하지만 참조 변수로도 접근이 가능합니다.

#### 예제

```java
class Calculator {
	static double pi = 3.14159;
    
    static int plus(int x, int y) {
    	return x + y;
    }
    
    static int minus(int x, int y) {
    	return x - y;
    }
}

public class Main {
	public static void main(String[] args) {
    	double result1 = 10 * 10 * Calculator.pi;
        int result2 = Calculator.plus(10, 10);
        int result3 = Calculator.minus(10, 10);
    }
}
```

<br>

### 정적 초기화 블록
정적 필드는 `static double pi = 3.14159`같이 초기화하는 것이 일반적이지만 복잡한 초기화 작업이 필요하다면 정적 블록을 사용할 수 있습니다.

#### 예제

```java
class Television {
	static String company = "Samsung";
    static String model = "LCD";
    static String info;
    
    static {
    	info = company + "-" + model;
    }
}

public class Main {
	public static void main(String[] args) {
    	System.out.println(Television.info);
    }
}
```

<br>

### 정적 메소드와 블록 선언 시 주의할 점

- 객체가 없어도 실행된다는 특징 때문에 이들 내부에 인스턴스 멤버를 사용할 수 없음
- 객체 자신의 참조인 this 키워드 사용 불가

인스턴스 멤버를 정적 메소드나 정적 블록에서 사용하고 싶다면 다음과 같이 객체를 먼저 생성하고 참조 변수로 접근합니다.

```java
static void Example() {
	ClassName obj = new ClassName();
    obj.field = 10;
    obj.method();
```

<br>

### 싱글톤
프로그램에서 단 하나의 객체만 만들도록 보장해야 하는 경우, 이 객체를 싱글톤이라고 합니다. 싱글톤을 만들려면 private 접근 제한자를 사용하여 클래스 외부에서 new 연산자로 생성자를 호출할 수 없도록 막아야 합니다. 

#### 예제

```java
class Singleton {
	private static Singleton singleton = new Singleton();
    
    private Singleton() {}
    
    static Singleton getInstance() {
    	return singleton;
    }
}

public class Main {
	public static void main(String[] args) {
    	Singleton obj1 = new Singleton(); // 컴파일 에러
        Singleton obj2 = Singleton.getInstance();
    }
}
```

<br>

## final 필드와 상수
### final 필드

```java
final 타입 필드 [= 초기값];
```

**final 필드**는 초기값이 저장되면 이것이 최종적인 값이 되어서 프로그램 실행 도중에 수정할 수 없습니다. final 필드의 초기값을 줄 수 있는 방법에는 두 가지가 있습니다.

1. 필드 선언 시에 초기화
2. 생성자를 사용한 초기화

#### 예제

```java
class Person {
	final String nation = "Korea"; // 첫 번째 방법
    final String ssn; // 두 번째 방법
    String name;
    
    public Person(String ssn, String name) {
    	this.ssn = ssn;
        this.name = name;
    }
}

public class Main {
	public static void main(String[] args) {
    	Person person = new Person("123456-1234567", "계백");
        person.name = "을지문덕";
        
        // final 필드 수정 불가
        person.nation = "usa";
        person.ssn = "123123-1231234";
    }
}     
```

<br>

### 상수 static final
원주율이나 지구의 둘레 등 불변의 값을 저장하는 필드를 의미합니다. 상수는 객체마다 저장되지 않고 클래스에만 포함되며, 한 번 초기값이 저장되면 변경할 수 없습니다. 상수 이름은 대문자로 작성하는 것이 관례이고 언더바를 사용해서 단어 사이를 연결합니다.

#### 예제

```java
class Earth {
	static final double EARTH_RADIUS = 6400;
    static final double EARTH_SURFACE_AREA;
    
    static {
    	EARTH_SURFACE_AREA = 4 * Math.PI * EARTH_RADIUS * EARTH_RADIUS;
    }
}

public class Main {
	public static void main(String[] args) {
    	System.out.println("지구의 반지름: " + Earth.EARTH_RADIUS + "km");
        System.out.println("지구의 표면적: " + Earth.EARTH_SURFACE_AREA + "km^2");
    }
}
```

<br>

## 패키지

- 자바는 수많은 클래스를 체계적으로 관리하기 위해 패키지를 사용
- 물리적인 형태는 파일 시스템의 폴더
- 클래스를 유일하게 만들어주는 식별자 역할
- com.mycompany에 소속된 `Car.class`를 com\yourcompany 폴더로 이동시키면 클래스 사용 불가

### 패키지 선언
컴파일러는 클래스에 포함되어 있는 패키지 선언을 보고 파일 시스템의 폴더를 자동 생성합니다.

```java
package 상위패키지.하위패키지;

public class ClassName { ... }
```

```java
package com.samsung.projectname
package com.hyundai.projectname
package com.lg.projectname
package org.apache.projectname
```

**import문**을 사용해서 다른 패키지를 불러오고 그 패키지에 속한 클래스를 사용할 수도 있습니다. 

```java
package com.mycompany;
import com.hankook.Tire;
[또는 import com.hankook.*;]

public class Car {
	Tire tire = new Tire();
]
```

```java
// 서로 다른 패키지에서 동일한 클래스명을 가질 시에는 패키지 이름 전체를 작성합니다.
import com.hankook.Tire;
import com.kumho.Tire;

com.kumho.Tire tire = new com.kumho.Tire();
```

<br>

## 접근 제한자

|접근 제한|	적용 대상|	접근할 수 없는 클래스|
|:---:|:---:|:---:|
|public|클래스, 필드, 생성자, 메소드|없음|
|protected|필드, 생성자, 메소드|자식 클래스가 아닌 다른 패키지에 소속된 클래스|
|default|클래스, 필드, 생성자, 메소드|다른 패키지에 소속된 클래스|
|private|필드, 생성자, 메소드|모든 외부 클래스|

<br>

## Getter와 Setter 메소드

- **Getter**: 메소드로 필드값을 가공한 후 외부로 전달하는 역할
- **Setter**: 매개값을 검증해서 유효한 값만 데이터로 저장하는 역할

#### 예제

```java
class Car {
    // 필드
    private int speed;
    private boolean stop;

    // 메소드
    public int getSpeed() {
        return speed;
    }

    public void setSpeed(int speed) {
        if (speed < 0) {
            this.speed = 0;
            return;
        } else {
            this.speed = speed;
        }
    }

    public boolean isStop() {
        return stop;
    }

    public void setStop(boolean stop) {
        this.stop = stop;
        this.speed = 0;
    }
}

public class Main {
    public static void main(String[] args) {
        Car car = new Car();

        // 잘못된 속도 변경
        car.setSpeed(-50);
        System.out.println("현재 속도: " + car.getSpeed());

        // 올바른 속도 변경
        car.setSpeed(50);
        System.out.println("현재 속도: " + car.getSpeed());

        // 멈춤
        if (!car.isStop()) {
            car.setStop(true);
        }
        System.out.println("현재 속도: " + car.getSpeed());
    }
}
```

<br>

## 어노테이션
어노테이션은 메타데이터라고 볼 수 있는데, 메타데이터란 애플리케이션이 처리해야 할 데이터가 아니라 컴파일 과정과 실행 과정에서 코드를 어떻게 컴파일하고 처리할 것인지를 알려주는 정보입니다. 어노테이션은 `@AnnotationName`과 같은 형태로 작성하고 세 가지 용도로 사용됩니다.

- 컴파일러에게 코드 문법 에러를 체크하도록 정보를 제공
- 소프트웨어 개발 툴 빌드나 배치 시 코드를 자동으로 생성할 수 있도록 정보를 제공
- 실행 시(런타임 시) 특정 기능을 실행하도록 정보를 제공

### 어노테이션 타입 정의와 적용

```java
public @interface AnnotationName {
	String elementName1();
    int elementName2() default 5;
}
```

위와 같이 @interface를 사용해서 어노테이션을 정의하며, 그 뒤에 사용할 어노테이션 이름을 작성합니다. 어노테이션은 엘리먼트를 멤버로 가질 수 있고 각 엘리먼트는 타입과 이름으로 구성됩니다. 이렇게 정의한 어노테이션을 코드에서 적용할 때에는 다음과 같이 사용합니다.

```java
@AnnotationName(elementName1="값", elementName2=3;);
or
@AnnotationName(elementName1="값");
```

<br>

### 어노테이션 적용 대상
어노테이션을 적용할 수 있는 대상은 java.lang.annotation.ElementType 열거 상수로 다음과 같이 정의되어 있습니다.

|ElementType 열거 상수|적용 대상|
|---|---|
|TYPE|클래스, 인터페이스, 열거 타입|
|ANNOTATION_TYPE|어노테이션|
|FIELD|필드|
|CONSTRUCTOR|생성자|
|METHOD|메소드|
|LOCAL_VARIABLE|로컬 변수|
|PACKAGE|패키지|

`@Target` 키워드를 사용해서 어노테이션이 적용될 대상을 지정할 수 있습니다.

```java
@Target({ElementType.TYPE, ElementType.FIELD, ElementType.METHOD})
public @interface AnnotationName {
}
```

다음과 같이 클래스, 필드, 메소드만 어노테이션을 적용할 수 있고 생성자는 적용할 수 없습니다.

```java
@AnnotationName
public class ClassName {
	@AnnotationName
    private String fieldName;
    
    // @AnnotationName - @Target에 CONSTRUCT가 없어서 생성자는 적용 못함
    public ClassName() {}
    
    @AnnotationName
    public void methodName() {}
}
```

<br>

### 어노테이션 유지 정책
어노테이션 정의 시 사용 용도에 따라 @AnnotationName을 어느 범위까지 유지할 것인지 지정해야 합니다. java.lang.annotation.RetentionPolicy 열거 상수로 정의되어 있습니다.

|RetentionPolicy 열거 상수|설명|
|---|---|
|SOURCE|소스상에서만 어노테이션 정보를 유지합니다. 소스 코드를 분석할 때만 의미가 있으며, 바이트 코드 파일에는 정보가 남지 않습니다.|
|CLASS|바이트 코드 파일까지 어노테이션 정보를 유지합니다. 하지만 리플렉션을 이용해서 어노테이션 정보를 얻을 수는 없습니다.|
|RUNTIME|바이트 코드 파일까지 어노테이션 정보를 유지하면서 리플렉션을 이용해서 런타임 시에 어노테이션 정보를 얻을 수 있습니다.|

> 리플렉션: 런타임 시에 클래스의 메타 정보를 얻는 기능

어노테이션 유지 정책을 지정할 때에는 @Retention 어노테이션을 사용합니다. 

```java
@Target({ElementType.TYPE, ElementType.FIELD, ElementType.METHOD})
@Retention(RetentionPolicy.RUNTIME)
public @interface AnnotationName {
}
```

<br>

### 런타임 시 어노테이션 정보 사용하기
어노테이션 자체는 아무런 동작을 가지지 않는 표식일 뿐이지만 리플렉션을 이용해서 어노테이션의 적용 여부와 엘리먼트 값을 읽고 적절히 처리할 수 있습니다. 클래스에 적용된 어노테이션 정보를 얻으려면 java.lang.Class를 이용하고 필드, 생성자, 메소드에 적용된 어노테이션 정보를 얻으려면 java.lang.reflect 패키지의 Field, Constructor, Method 타입의 배열을 얻어야 합니다.

|리턴 타입|메소드명(매개 변수)|설명|
|---|---|---|
|Field\[]|getFields()|필드 정보를 Field 배열로 리턴|
|Constructor\[]|getConstructors()|생성자 정보를 Constructor 배열로 리턴|
|Method\[]|getDeclaredMethods()|메소드 정보를 Method 배열로 리턴|

그런 다음 Class, Field, Constructor, Method가 가지고 있는 메소드를 호출해서 적용된 어노테이션 정보를 얻을 수 있습니다.

|리턴 타입|메소드명(매개 변수)|
|---|---|
|boolean|isAnnotationPresent(Class<? extends Annotation> annotationClass)|
||지정한 어노테이션이 적용되었는지 여부. Class에서 호출했을 때 상위 클래스에 적용된 경우에도 true를 리턴합니다.|
|Annotation|getAnnotation(Class< T > annotationClass)|
||지정한 어노테이션이 적용되어 있으면 어노테이션을 리턴하고 그렇지 않다면 null을 리턴합니다. Class에서 호출했을 때 상위 클래스에 적용된 경우에도 어노테이션을 리턴한다.|
|Annotation\[]|getAnnotations()|
||적용된 모든 어노테이션을 리턴한다. Class에서 호출했을 때 상위 클래스 적용된 어노테이션도 모두 포함됩니다. 적용된 어노테이션이 없을 경우 길이가 0인 배열을 리턴합니다.|
|Annotation\[]|getDeclareAnnotations()|
||직접 적용된 모든 어노테이션을 리턴합니다. Class에서 호출했을 때 상위 클래스에 적용된 어노테이션은 포함되지 않습니다.|

#### 예제

```java
# PrintAnnotation.java

import java.lang.annotation.ElementType;
import java.lang.annotation.Retention;
import java.lang.annotation.RetentionPolicy;
import java.lang.annotation.Target;

@Target({ElementType.METHOD})
@Retention(RetentionPolicy.RUNTIME)
public @interface PrintAnnotation {
    String value() default "-";

    int number() default 15;
}
```

```java
# Main.java

import java.lang.reflect.Method;

class Service {
    @PrintAnnotation
    public void method1() {
        System.out.println("실행 내용1");
    }

    @PrintAnnotation("*")
    public void method2() {
        System.out.println("실행 내용2");
    }

    @PrintAnnotation(value="#", number=20)
    public void method3() {
        System.out.println("실행 내용3");
    }
}

public class Main {
    public static void main(String[] args) {
        // Service 클래스로부터 메소드 정보를 얻음
        Method[] declareMethods = Service.class.getDeclaredMethods();

        // Method 객체를 하나씩 처리
        for (Method method : declareMethods) {
            // PrintAnnotation이 적용되었는지 확인
            if (method.isAnnotationPresent(PrintAnnotation.class)) {
                // PrintAnnotation 객체 얻기
                PrintAnnotation printAnnotation = method.getAnnotation(PrintAnnotation.class);

                // 메소드 이름 출력
                System.out.println("[" + method.getName() + "]");
                // 구분선 출력
                for (int i=0; i< printAnnotation.number(); i++) {
                    System.out.print(printAnnotation.value());
                }
                System.out.println();

                try {
                    // 메소드 호출
                    method.invoke(new Service());
                } catch (Exception e) {}
                System.out.println();
            }
        }
    }
}
```

<br>

## 레퍼런스
- 이것이 자바다: 신용권의 Java 프로그래밍 정복
- 싱글톤(Singleton) 패턴이란?: https://tecoble.techcourse.co.kr/post/2020-11-07-singleton/
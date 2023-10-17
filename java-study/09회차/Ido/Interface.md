## 인터페이스의 역할

- 개발 코드와 객체가 서로 통신하는 접점 역할
- 객체의 사용 방법을 정의한 타입
- 객체의 교환성을 높여주기 때문에 다형성을 구현하기 위해 매우 중요함

<br>

## 인터페이스 선언

```java
interface 인터페이스명 {
	// 상수
    타입 상수명 = 값;
    // 추상 메소드
    타입 메소드명(매개변수, ... );
    // 디폴트 메소드
    default 타입 메소드명(매개변수, ... ) { ... }
    // 정적 메소드
    static 타입 메소드명(매개변수) { ... }
}
```

인터페이스 선언은 class 키워드 대신 interface 키워드를 사용합니다.
클래스는 필드, 생성자, 메소드를 구성 멤버로 가지는데 비해 인터페이스는 상수와 메소드만을 구성 멤버로 가집니다. 그리고 인터페이스는 객체로 생성할 수 없기 때문에 생성자를 가질 수 없습니다.

> 자바 7 이전까지는 인터페이스의 메소드는 추상 메소드로만 선언이 가능했지만,
자바 8부터는 디폴트 메소드와 정적 메소드도 선언이 가능합니다.

<br>

### 상수 필드

- 인터페이스는 상수 필드만 선언 가능
- 인터페이스에 선언된 필드는 모두 `public static final` 특성을 가짐

<br>

### 추상 메소드

- 인터페이스를 통해 호출된 메소드는 최종적으로 객체에서 실행되기 때문에 인터페이스의 메소드는 실행 블록이 필요 없는 추상 메소드로 선언됨
- 인터페이스에 선언된 추상 메소드는 모두 `public abstract` 특성을 가짐

<br>

### 디폴트 메소드

- 자바 8부터 추가됨
- 클래스의 인스턴스 메소드와 동일한 형태
- 기본적으로 `public` 특성을 가짐

<br>

### 정적 메소드

- 자바 8부터 추가됨
- 클래스의 정적 메소드와 동일한 형태
- 기본적으로 `public` 특성을 가짐

<br>

#### 예제

```java
public interface RemoteControl {
	// 상수
    int MAX_VOLUME = 10;
    int MIN_VOLUME = 0;
    
    // 추상 메소드
    void turnOn();
    void turnOff();
    void setVolume(int volume);
    
    // 디폴트 메소드
    default void setMute(boolean mute) {
    	if(mute) {
        	System.out.println("음소거");
        } else {
        	System.out.println("음소거 해제");
        }
    }
    
    // 정적 메소드
    static void changeBattery() {
    	System.out.println("건전지 교체");
    }
}
```

<br>

## 인터페이스 구현
인터페이스가 호출하는 객체는 인터페이스에서 정의된 추상 메소드와 동일한 메소드 이름, 매개 타입, 리턴 타입을 가진 실체 메소드를 가지고 있어야 합니다. 이러한 객체를 인터페이스의 구현(implement) 객체라고 하고, 구현 객체를 생성하는 클래스를 구현 클래스라고 합니다.

<br>

### 구현 클래스

```java
public class 구현클래스명 implements 인터페이스명 {
	// 인터페이스에 선언된 추상 메소드와 실체 메소드 선언
}
```

구현 클래스는 보통의 클래스와 동일한데, 인터페이스 타입으로 사용할 수 있음을 알려주기 위해 클래스 선언부에 implement 키워드를 추가하고 인터페이스명을 명시합니다. 구현 클래스가 작성되면 new 연산자로 객체를 생성할 수 있습니다.

```java
인터페이스 변수 = 구현객체;
```

```java
// Television.java
public class Television implements RemoteControl {
	// 필드
    private int volume;
    
    // turnOn() 추상 메소드의 실체 메소드
    public void turnOn() {
    	System.out.println("TV를 켭니다.");
    }
    // turnOff() 추상 메소드의 실체 메소드
    public void turnOff() {
    	System.out.println("TV를 끕니다.");
    }
    // setVolume() 추상 메소드의 실체 메소드
    public void setVolume(int volume) {
    	if (volume > RemoteControl.MAX_VOLUME) {
        	this.volume = RemoteControl.MAX_VOLUME;
        } else if (volume < RemoteControl.MIN_VOLUME {
        	this.volume = RemoteControl.MIN_VOLUME;
        } else {
        	this.volume = volume;
        }
        System.out.println("현재 TV 볼륨: " + this.volume);
    }
}

// Audio.java
public class Audio implements RemoteControl {
	// 필드
    private int volume;
    
    // turnOn() 추상 메소드의 실체 메소드
    public void turnOn() {
    	System.out.println("Audio를 켭니다.");
    }
    // turnOff() 추상 메소드의 실체 메소드
    public void turnOff() {
    	System.out.println("Audio를 끕니다.");
    }
    // setVolume() 추상 메소드의 실체 메소드
    public void setVolume(int volume) {
    	if (volume > RemoteControl.MAX_VOLUME) {
        	this.volume = RemoteControl.MAX_VOLUME;
        } else if (volume < RemoteControl.MIN_VOLUME {
        	this.volume = RemoteControl.MIN_VOLUME;
        } else {
        	this.volume = volume;
        }
        System.out.println("현재 Audio 볼륨: " + this.volume);
    }
}

// Main.java
public class Main {
	public static void main(String[] args) {
    	RemoteControl rc;
        rc = new Television();
        rc = new Audio();
    }
}
```

<br>

### 익명 구현 객체
자바는 소스 파일을 만들지 않고도 구현 객체를 만들 수 있는 방법을 제공합니다.
익명 구현 객체는 UI 프로그래밍에서 이벤트를 처리할 때나, 임시 작업 스레드를 만들 때 활용합니다.

> 자바 8부터 지원하는 람다식은 인터페이스의 익명 구현 객체를 만듭니다.

```java
public class Main {
	public static void main(String[] args) {
    	RemoteControl rc = new RemoteControl() {
        	public void turnOn() { 
            	실행문;
            }
            public void turnOff() { 
            	실행문;
            }
            public void setVolume(int volume) { 
            	실행문;
            }
        };
    }
}
```

익명 구현 객체의 중괄호 안에는 인터페이스에서 선언된 모든 추상 메소드들의 실체 메소드를 작성해야 합니다. 그렇지 않으면 컴파일 에러가 발생합니다. 추가적으로 필드와 메소드를 선언할 수 있지만 익명 객체 안에서만 사용할 수 있고 인터페이스 변수로 접근할 수 없습니다.

> 하나의 실행문이므로 끝에 세미콜론을 붙여야 합니다.

<br>

### 다중 인터페이스 구현 클래스
객체를 다수의 인터페이스 타입으로 사용할 수 있습니다. 다중 인터페이스를 구현할 경우, 구현 클래스는 모든 인터페이스의 추상 메소드에 대해 실체 메소드를 작성해야 합니다. 만약 하나라도 없으면 추상 클래스로 선언해야 합니다.

#### 예제

```java
// Searchable.java
public interface Searchable {
	void search(String url);
}

// SmartTelevision.java
public class SmartTelevision implements RemoteControl, Searchable {
	private int volume;
    
    public void turnOn() {
    	System.out.println("TV를 켭니다.");
    }
    public void turnOff() {
    	System.out.println("TV를 끕니다.");
    }
    public void setVolume(int volume) {
    	if (volume > RemoteControl.MAX_VOLUME) {
        	this.volume = RemoteControl.MAX_VOLUME;
        } else if (volume < RemoteControl.MIN_VOLUME {
        	this.volume = RemoteControl.MIN_VOLUME;
        } else {
        	this.volume = volume;
        }
        System.out.println("현재 TV 볼륨: " + this.volume);
    }
    
    public void search(String url) {
    	System.out.println(url + " 을 검색합니다.");
    }
}
```

<br>

## 인터페이스 사용
### 추상 메소드 사용

```java
public class Main {
	public static void main(String[] args) {
    	RemoteControl rc = null; // 인터페이스 변수 선언
        
        rc = new Television(); // Television 객체를 인터페이스 타입에 대입
        rc.turnOn();
        rc.turnOff();
        
        rc = new Audio(); // Audio 객체를 인터페이스 타입에 대입
        rc.turnOn();
        rc.turnOff();
    }
}
```

<br>

### 디폴트 메소드 사용

디폴트 메소드는 인터페이스에 선언되지만, 인터페이스에서 바로 사용할 수 없습니다. 디폴트 메소드는 추상 메소드가 아닌 인스턴스 메소드이므로 구현 객체가 있어야 사용할 수 있습니다. 예를 들어 RemoteControl 인터페이스는 setMute() 라는 디폴트 메소드를 가지고 있지만 다음과 같이 호출할 수 없습니다.

```java
RemoteControl.setMute(true);
```

다음은 올바른 방법입니다.

```java
RemoteCotrol rc = new Television();
rc.setMute(true);
```

디폴트 메소드는 인터페이스의 모든 구현 객체가 가지고 있는 기본 메소드라고 생각하면 되고, 오버라이딩을 통해서 객체에 맞게 수정할 수 있습니다.

<br>

### 정적 메소드 사용
인터페이스의 정적 메소드는 인터페이스로 바로 호출이 가능합니다.

```java
public class Main {
	public static void main(String[] args) {
    	RemoteControl.changeBattery();
    }
}
```

<br>

## 타입 변환과 다형성
상속에서 부모 타입에 어떤 자식 객체를 대입하느냐에 따라 실행 결과가 달라졌듯이, 인터페이스 타입에 어떤 구현 객체를 대입하느냐에 따라 실행 결과가 달라집니다. 상속은 같은 종류의 하위 클래스를 만드는 기술이고 인터페이스는 사용 방법이 동일한 클래스를 만드는 기술이라는 개념적 차이점이 있습니다.

```java
I i = new A();
I i = new B(); // 수정

// 수정이 필요 없음
i.method1();
i.method2();
```

인터페이스는 메소드의 매개 변수로 많이 쓰입니다. 인터페이스 타입으로 매개 변수를 선언하면 메소드 호출 시 매개값으로 여러 가지 종류의 구현 객체를 적용할 수 있기 때문에 실행 결과가 다양하게 나옵니다. 이것이 인터페이스 매개 변수의 다형성입니다.

```java
// 매개값으로 Television 객체 또는 Audio 객체를 선택적으로 줄 수 있음
public void useRemoteControl(RemoteControl rc) { ... }
```

<br>

### 자동 타입 변환

```java
인터페이스 변수 = 구현객체;
```

인터페이스 구현 클래스를 상속해서 자식 클래스를 만들었다면 자식 객체 역시 인터페이스 타입으로 자동 타입 변환시킬 수 있습니다. 자동 타입 변환을 이용하면 필드의 다형성과 매개 변수의 다형성을 구현할 수 있습니다.

<br>

### 필드의 다형성
#### 예제

```java
// Tire.java
public interface Tire {
	public void roll();
}

// HankookTire.java
public class HankookTire implements Tire {
	@Override
    public void roll() {
    	System.out.println("한국 타이어가 굴러갑니다.");
    }
}

// KumhoTire.java
public class KumhoTire implements Tire {
	@Override
    public void roll() {
    	System.out.println("금호 타이어가 굴러갑니다.");
    }
}

// Car.java
public class Car {
	// 인터페이스 타입 필드 선언과 초기 구현 객체 대입
	Tire frontLeftTire = new HankookTire();
    Tire frontRightTire = new HankookTire();
    Tire backLeftTire = new HankookTire();
    Tire backRightTire = new HankookTire();
    
    // 인터페이스의 roll() 메소드 호출
    void run() {
    	frontLeftTire.roll();
        frontRightTire.roll();
        backLeftTire.roll();
        backRightTire.roll();
    }
}

// Main.java
public class Main {
	public static void main(String[] args) {
    	Car myCar = new Car();
        
        myCar.run();
        
        myCar.frontLeftTire = new KumhoTire();
        myCar.frontRightTire = new KumhoTire();
        
        myCar.run();
    }
}
```

<br>

### 인터페이스 배열로 구현 객체 관리
#### 예제

```java
// Car.java
public class Car {
	Tire[] tires = {
    	new HankookTire(),
        new HankookTire(),
        new HankookTire(),
        new HankookTire()
    };
    
    void run() {
    	for (Tire tire : tires) {
        	tire.roll();
        }
    }
}

// Main.java
public class Main {
	public static void main(String[] args) {
    	Car myCar = new Car();
        
        myCar.run();
        
        myCar.tires[0] = new KumhoTire();
        myCar.tires[1] = new KumhoTire();
        
        myCar.run();
    }
}
```

<br>

### 매개 변수의 다형성
자동 타입 변환은 필드의 값을 대입할 때에도 발생하지만, 주로 메소드를 호출할 때 많이 발생합니다.
매개 변수의 타입이 인터페이스일 경우, 어떠한 구현 객체도 매개값으로 사용할 수 있고 어떤 구현 객체가 제공되느냐에 따라 메소드의 실행 결과가 다양해집니다.

#### 예제

```java
// Driver.java
public class Driver {
	public void drive(Vehicle vehicle) {
    	vehicle.run;
    }
}

// Vehicle.java
public interface Vehicle {
	public void run();
}

// Bus.java
public class Bus implements Vehicle {
	@Override
    public void run() {
    	System.out.println("버스가 달립니다.");
    }
}

// Taxi.java
public class Taxi implements Vehicle {
	@Override
    public void run() {
    	System.out.println("택시가 달립니다.");
    }
}

// Main.java
public class Main {
	public static void main(String[] args) {
    	Driver driver = new Driver();
        
        Bus bus = new Bus();
        Taxi taxi = new Taxi();
        
        driver.drive(bus); // Vehicle vehicle = bus;
        driver.drive(taxi); // Vehicle vehicle = taxi;
    }
}
```

<br>

### 강제 타입 변환
구현 객체가 인터페이스 타입으로 자동 변환하면 인터페이스에 선언된 메소드만 사용 가능하다는 제약 사항이 있기 때문에 강제 타입 변환을 사용해서 다시 구현 클래스 타입으로 변환할 수 있습니다.

#### 예제

```java
// Vehicle.java
public interface Vehicle {
	public void run();
}

// Bus.java
public class Bus implements Vehicle {
	@Override
    public void run() {
    	System.out.println("버스가 달립니다.");
    }
    
    public void charkFare() {
    	System.out.println("승차요금을 체크합니다.");
    }
}

// Main.java
public class Main {
	public static void main(String[] args) {
    	Vehicle vehicle = new Bus();
        
        vehicle.run();
        // vehicle.checkFare();
        
        Bus bus = (Bus) vehicle; // 강제 타입 변환
        
        bus.run();
        bus.checkFare();
    }
}
```

<br>

### 객체 타입 확인
#### 예제

```java
public class Driver {
	public void drive(Vehicle vehicle) {
    	if (vehicle instanceof Bus) {
        	Bus bus = (Bus) vehicle;
            bus.checkFare();
        }
        vehicle.run();
    }
}
```

<br>

## 인터페이스 상속
인터페이스도 다른 인터페이스를 상속할 수 있습니다. 인터페이스는 클래스와는 달리 다중 상속을 허용합니다.

```java
public interface 하위인터페이스 extends 상위인터페이스1, 상위인터페이스2 { ... }
```

하위 인터페이스를 구현하는 클래스는 하위 인터페이스의 메소드뿐만 아니라 상위 인터페이스의 모든 추상 메소드에 대한 실체 메소드를 가지고 있어야 합니다. 그렇기 때문에 구현 클래스로부터 객체를 생성하고 나서 다음과 같이 하위 및 상위 인터페이스 타입으로 변환이 가능합니다.

```java
하위인터페이스 변수 = new 구현클래스(...);
상위인터페이스1 변수 = new 구현클래스(...);
상위인터페이스2 변수 = new 구현클래스(...);
```

하위 인터페이스 타입으로 변환이 되면 상/하위 인터페이스에 선언된 모든 메소드를 사용할 수 있으나 상위 인터페이스로 타입 변환되면 상위 인터페이스에 선언된 메소드만 사용이 가능합니다.

<br>

## 디폴트 메소드와 인터페이스 확장
### 디폴트 메소드의 필요성
기존 인터페이스의 이름과 추상 메소드의 변경 없이 디폴트 메소드만 추가할 수 있기 때문에 이전에 개발한 구현 클래스를 그대로 사용할 수 있으면서 새롭게 개발하는 클래스는 디폴트 메소드를 활용할 수 있습니다. 이렇게 기존 인터페이스를 확장해서 새로운 기능을 추가하기 위해서 디폴트 메소드가 필요합니다.

#### 예제

```java
// MyInterface.java
public interface MyInterface {
	public void method1();
}

// MyclassA.java
public class MyClassA implements MyInterface {
	@Override
    public void method1() {
    	System.out.println("MyClassA-method1() 실행");
    }
}

// MyInterface.java
public interface MyInterface {
	public void method1();
    
    public default void method2() { // 디폴트 메소드 추가
    	System.out.println("MyInterface-method2() 실행");
    }
}

// MyclassB.java
public class MyClassA implements MyInterface {
	@Override
    public void method1() {
    	System.out.println("MyClassB-method1() 실행");
    }
    
    @Override
    public void method2() { // 디폴트 메소드 재정의
    	System.out.println("MyclassB-method2() 실행");
    }
}

// Main.java
public class Main {
	public static void main(String[] args) {
    	MyInterface mi1 = new MyClassA();
        mi1.method1();
        mi1.method2();
        
        MyInterface mi2 = new MyclassB();
        mi2.method1();
        mi2.method2();
    }
}
```

<br>

### 디폴트 메소드가 있는 인터페이스 상속
부모 인터페이스에 디폴트 메소드가 정의되어 있을 경우, 자식 인터페이스에서 디폴트 메소드를 활용하는 방법은 세 가지가 있습니다.

1. 단순히 상속만 받는다.
2. 재정의해서 실행 내용을 변경한다.
3. 추상 메소드로 재선언한다.

<br>

## 레퍼런스
- 이것이 자바다: 신용권의 Java 프로그래밍 정복
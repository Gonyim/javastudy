# 5. 상속

### 추상 클래스의 용도
추상 클래스를 이용하면 응용프로그램의 설계와 구현을 분리할 수 있다. 추상 클래스는 추상 메소드를 선언할 뿐 어떻게 구현할지는 지시하지 않는다. 어떤 인자가 전달되고 어떤 타입의 값이 리턴되는지만 지정할 뿐이며, 구현은 자식 클래스의 몫이다.
***

## 인터페이스
인터페이스는 서로 다른 하드웨어 장치들이 상호 데이터를 주고받을 수 있는 규격을 의미한다. 인터페이스의 개념은 소프트웨어에도 적용이 되는데, 소프트웨어를 규격화된 모듈로 만들고, 서로 인터페이스가 맞는 모듈을 조립하듯이 응용프로그램을 작성할 수 있다.

### 자바의 인터페이스
자바의 인터페이스는 interface 키워드를 사용하여 클래스를 선언하듯이 선언한다.
- 인터페이스 구성
  - 5종류의 멤버로 구성되며, 필드(멤버 변수)를 만들 수 없다.
    - 상수와 추상 메소드(Java 7까지)
    - default 메소드(Java 8부터)
    - private 메소드(Java 9부터)
    - static 메소드(Java 9부터)
  - 추상 메소드는 public abstract로 정해져 있으며, 생략될 수 있고, 다른 접근 지정으로 지정될 수 없다. default, private, static 메소드들은 모두 인터페이스 내에 코드가 작성되어 있어야 한다.
    - default 메소드의 접근 지정은 public으로 고정되어 있다.
    - private 메소드는 인터페이스 내에서만 호출 가능하다.
    - static 메소드의 경우 접근 지정이 생략되면 public이며, private으로 지정될 수 있다.
- 인터페이스는 객체를 생성할 수 없다
  - 인터페이스에 구현되지 않은 추상 메소드를 가질 수 있기 때문에 객체를 생성할 수 없다.
```java
new ExInterface();      // 오류. 객체 생성 불가
```
- 인터페이스 타입의 레퍼런스 변수는 선언 가능하다
```java
ExInterface smile;      // smile은 인터페이스에 대한 레퍼런스 변수
```
- 인터페이스끼리 상속된다(다중 상속 가능)
  - 인터페이스는 다른 페이스를 상속할 수 있다.
- 인터페이스를 상속받아 클래스를 작성하면 인터페이스의 모든 추상 메소드를 구연하여야 한다
  - 자바의 인터페이스는 상속받을 자식 클래스에게 구현할 메소드들의 원형을 모두 알려주어, 클래스가 스스로의 목적에 맞게 메소드를 구현하도록 하는 것이 목적이다.
***

### 인터페이스 구현
인터페이스 구현이란 implements 키워드를 사용하여 인터페이스의 모든 추상 메소드를 구현한 클래스를 작성하는 것을 말한다.
```java
interface PhoneInterface {      // 인터페이스 선언
    final int TIMEOUT = 10000;  // 상수 필드 선언
    void sendCall();            // 추상 메소드
    void receiveCall();        // 추상 메소드
    default void printLogo() {  // default 메소드
        System.out.println("** PHONE **");
    }
}

class ExPhone implements PhoneInterface {   // 인터페이스 구현
    // PhoneInterface의 모든 추상 메소드 구현
    @Override
    public void sendCall() {
        System.out.println("띠리링");
        }
    @Override
    public void receiveCall() {
        System.out.println("전화왔습니다.");
        }
    // 메소드 추가 작성
    public void flash() {
        System.out.println("불이 켜졌습니다.");
        }
}

public class InterfaceEx {
    public static void main(String[] args) {
        ExPhone phone = new ExPhone();
        phone.printLogo();
        phone.sendCall();
        phone.receiveCall();
        phone.flash();
    }
}
```
***

### 인터페이스 상속
클래스는 인터페이스를 상속받을 수 없고, **인터페이스끼리만 상속이 가능하다**.  
상속을 통해 기존 인터페이스에 새로운 규격을 추가한 새로운 인터페이스를 만들 수 있으며, 인터페이스의 상속은 extends 키워드를 사용한다.
```java
인터페이스의 상속

interface PhoneInterface {      // 인터페이스 선언
    final int TIMEOUT = 10000;  // 상수 필드 선언
    void sendCall();            // 추상 메소드
    void receiveCall();        // 추상 메소드
    default void printLogo() {  // default 메소드
        System.out.println("** PHONE **");
    }
}

interface MobilePhoneInterface extends PhoneInterface {     // 인터페이스 상속
    void sendSMS();     // 추상 메소드
    void receiveSMS();  // 추상 메소드
    void interNet();    // 추상 메소드
}
```

```java
인터페이스의 다중 상속

interface PhoneInterface {      // 인터페이스 선언
    void sendCall();            // 추상 메소드
    void receiveCall();        // 추상 메소드
}

interface MP3Interface {
    void play();                // 추상 메소드
    void stop();                // 추상 메소드
}

interface MP3PhoneInterface extends PhoneInterface, MP3Interface {  // 다중 상속
    void soundUp();             // 추상 메소드
    void soundDown();           // 추상 메소드
}

여기에서 MP3PhoneInterface은 총 6개의 멤버를 가진 인터페이스가 된다.
```
***

### 인터페이스의 목적
자바에서 인터페이스를 두는 진정한 목적은 무엇일까?  
모바일 전화기가 가지고 있어야 하는 기능(메소드)을 가진 인터페이스를 MobilePhoneInterface라고 했을 때 삼성이나 애플은 MobilePhoneInterface 인터페이스를 구현하여 GalaxyPhone 클래스를 만들고, IPhone 클래스를 만든다. GalaxyPhone과 IPhone 클래스 모두 MobilePhoneInterface 인터페이스에 나열된 메소드와 동일한 이름의 메소드를 구현하겠지만, 각자 구현한 내용은 다를 것이다. 여기에서 인터페이스로 인한 다형성이 실현되는 것이다.  
여기에서 모바일 단말기 응용 소프트웨어 개발자는 GalaxyPhone과 IPhone 클래스에는 MobilePhoneInterface 인터페이스의 메소드가 모두 구현되어 있을 것이므로 메소드를 호출하여 쉽게 제어할 수 있다.  
쉽게 말해서, 인터페이스는 스펙을 주어 클래스들이 그 기능을 서로 다르게 구현할 수 있도록 하는 클래스의 규격 선언이며, 클래스의 다형성을 실현하는 도구이다.
***

### 다중 인터페이스 구현
클래스는 하나 이상의 인터페이스를 구현할 수 있다. 이 경우 ,(콤마)로 각 인터페이스를 구분하여 나열하며, **각 인터페이스에 선언된 모든 추상 메소드를 구현해야 한다**. 그렇지 않으면 컴파일 오류가 발생한다.
```java
interface PhoneInterface {
    void sendCall();
    void receiveCall();
}

interface AIInterface {
    void recognizeSpeech();
    void synthesizeSpeech();
}

class AIPhone implements PhoneInterface, AIInterface {  // 인터페이스 구현
    // PhoneInterface의 모든 메소드를 구현한다.
    public void sendCall() { ... }
    public void receiveCall() { ... }

    // AIInterface의 모든 메소드를 구현한다.
    public void recognizeSpeech() { ... }
    public void synthesizeSpeech() { ... }

    // 추가적으로 다른 메소드를 작성할 수 있다.
    public int touch() { ... }
}
```
***

### 클래스 상속과 함께 인터페이스 구현
클래스 상속을 받으면서 동시에 인터페이스를 구현할 수 있다. 다중 상속, 다중 인터페이스 구현은 유용하나 너무 남용하게 되면 클래스, 인터페이스 간의 관계가 너무 복잡해져 프로그램 전체 구조를 파악하기 어려울 수 있으므로 주의하는 것이 좋다.
```java
interface PhoneInterface {      // 인터페이스 선언
    final int TIMEOUT = 10000;  // 상수 필드 선언
    void sendCall();            // 추상 메소드
    void receiveCall();        // 추상 메소드
    default void printLogo() {  // default 메소드
        System.out.println("** PHONE **");
    }
}
interface MobilePhoneInterface extends PhoneInterface {     // 인터페이스 상속
    void sendSMS();
    void receiveSMS();
}
interface MP3Interface {    // 인터페이스 선언
    void play();
    void stop();
}
class PDA {     // 클래스 작성
    public int calculate(int x, int y) {
        return x + y;
    }
}

// SmartPhone 클래스는 PDA를 상속받고,
// MobilePhoneInterface와 MP3Interface 인터페이스에 선언된 추상 메소드를 모두 구현한다.
class SmartPhone extends PDA implements MobilePhoneInterface, MP3Interface {
    // MobilePhoneInterface의 추상 메소드 구현
    @Override
    public void sendCall() {
        System.out.println("띠리링");
    }
    @Override
    public void receiveCall() {
        System.out.println("전화왔습니다.");
    }
    @Override
    public void sendSMS() {
        System.out.println("문자 발신");
    }
    @Override
    public void receiveSMS() {
        System.out.println("문자 수신");
    }

    // MP3Interface의 추상 메소드 구현
    @Override
    public void play() {
        System.out.println("음악 시작");
    }
    @Override
    public void stop() {
        System.out.println("음악 중지");
    }

    // 추가로 작성하는 메소드
    public void Schedule() {
        System.out.println("일정 관리");
    }
}

public class InterfaceEx {
    public static void main(String[] args) {
        SmartPhone phone = new SmartPhone();
        phone.printLogo();
        phone.sendCall();
        phone.play();
        System.out.println("3과 5를 더하면" + phone.calculate(3, 5));
        phone.schedule();
    }
}
```
***

### 인터페이스와 추상 클래스 비교
인터페이스와 추상 클래스 공통점  
  - 객체를 생성할 수 없고, 상속을 위한 슈퍼 클래스로만 사용된다.
  - 클래스의 다형성을 실현하기 위한 목적이다.
***

인터페이스와 추상 클래스 차이점  
- 추상 클래스  
  - 목적
    - 추상 클래스는 자식 클래스에서 필요로 하는 대부분의 기능을 구현하여 두고 자식 클래스가 상속받아 활용할 수 있도록 하되, 자식 클래스에서 구현할 수 밖에 없는 기능만을 추상 메소드로 선언하여, 자식 클래스에서 구현하도록 한다.(다형성)  
  - 구성
    - 추상 메소드와 일반 메소드 모두 포함
    - 상수, 변수 필드 모두 포함

- 인터페이스
  - 목적
    - 인터페이스는 객체의 기능을 모두 공개한 표준화 문서와 같은 것으로, 개발자에게 인터페이스를 상속받는 클래스의 목적에 따라 인터페이스의 모든 추상 메소드를 만들도록 하는 목적(다형성)
  - 구성
    - 변수 필드(멤버 변수)는 포함하지 않음
    - 상수, 추상 메소드, 일반 메소드, default 메소드, static 메소드 모두 포함
    - protected 접근 지정 선언 불가
    - 다중 상속 지원
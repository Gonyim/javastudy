## 중첩 클래스와 중첩 인터페이스란?
객체 지향 프로그램에서 어떤 클래스는 여러 클래스와 관계를 맺지만 어떤 클래스는 특정 클래스와 관계를 맺습니다. 클래스가 여러 클래스와 관계를 맺는 경우에는 독립적으로 선언하는 것이 좋으나, 특정 클래스와 관계를 맺을 경우에는 관계 클래스를 클래스 내부에 선언하는 것이 좋습니다. 이때 클래스 내부에 선언한 클래스를 `중첩 클래스(Nested Class)`라고 합니다.

- 두 클래스의 멤버들을 서로 쉽게 접근할 수 있음
- 외부에 불필요한 관계 클래스를 감춤으로써 코드의 복잡성을 줄일 수 있음

```java
class ClassName {
	class NestedClassName {
    	...
    }
}
```

인터페이스도 클래스 내부에 선언할 수 있는데, 이런 인터페이스를 `중첩 인터페이스`라고 합니다. 인터페이스를 클래스 내부에 선언하는 이유는 해당 클래스와 긴밀한 관계를 맺는 구현 클래스를 만들기 위해서입니다. 구현 인터페이스는 주로 UI 프로그래밍에서 이벤트를 처리할 목적으로 많이 활용됩니다.

```java
public class View {
	public interface OnClickListener {
    	public void onClick(View v);
    }
}
```

<br>

## 중첩 클래스
중첩 클래스는 클래스 내부에 선언되는 위치에 따라서 두 가지로 분류됩니다.

- 멤버 클래스: 클래스의 멤버로서 선언되는 중첩 클래스
- 로컬 클래스: 메소드 내부에서 선언되는 중첩 클래스

`멤버 클래스`는 클래스나 객체가 사용 중이라면 언제든지 재사용이 가능하지만, `로컬 클래스`는 메소드 실행 시에만 사용되고 메소드가 실행 종료되면 없어집니다.

![중첩-클래스](https://velog.velcdn.com/images/kid/post/aa1a5f00-89b8-4e1a-8508-e4a694c31740/image.png)

> 멤버 클래스도 하나의 클래스이기 때문에 컴파일하면 바이트 코드 파일이 별도로 생성됩니다.

<br>

### 인스턴스 멤버 클래스
인스턴스 멤버 클래스는 static 키워드 없이 선언된 클래스를 말합니다. 인스턴스 멤버 클래스는 인스턴스 필드와 메소드만 선언이 가능하고 정적 필드와 메소드는 선언할 수 없습니다.

```java
Class A {
	Class B {
    	B() {} // 생성자
        int field1; // 인스턴스 필드
        // static int field2; 정적 필드 X
        void method1() {} // 인스턴스 메소드
        //static void method2() {} 정적 메소드 X
    }
}
```

A 클래스 외부에서 인스턴스 멤버 클래스 B의 객체를 생성하려면 우선 A 객체를 생성해야 합니다.

```java
A a = new A();
A.B b = a.new B();
b.field1 = 3;
b.method1();
```

<br>

### 정적 멤버 클래스
정적 멤버 클래스는 static 키워드로 선언된 클래스를 말합니다. 정적 멤버 클래스는 모든 종류의 필드와 메소드를 선언할 수 있습니다.

```java
Class A {
	static Class C {
    	C() {} // 생성자
        int field1; // 인스턴스 필드
        static int field2; // 정적 필드
        void method1() {} // 인스턴스 메소드
        static void method2() {} // 정적 메소드
    }
}
```

A 클래스 외부에서 정적 멤버 클래스 C의 객체를 생성하기 위해서는 A 객체를 생성할 필요가 없습니다.

```java
A.C c = new A.C();
c.field1 = 3;
c.method1();
A.C.field2 = 3;
A.C.method2();
```

<br>

### 로컬 클래스
중첩 클래스는 메소드 내에서도 선언할 수 있습니다. 이것을 로컬 클래스라고 하는데, 로컬 클래스는 접근 제한자 및 static 키워드를 붙일 수 없습니다. 로컬 클래스는 메소드 내부에서만 사용되므로 접근을 제한할 필요가 없기 때문입니다. 로컬 클래스 내부에는 인스턴스 필드와 메소드만 선언할 수 있습니다.

```java
void method() {
	class D {
    	D() {} // 생성자
        int field1; // 인스턴스 필드
        // static int field2; 정적 필드 X
        void method1() {} // 인스턴스 메소드
        //static void method2() {} 정적 메소드 X
    }
    D.d = new D();
    d.field1 = 3;
    d.method();
}
```

로컬 클래스는 메소드가 실행될 때 메소드 내에서 객체를 생성하고 사용해야 합니다. 주로 다음과 같이 비동기 처리를 위해 스레드 객체를 만들 때 사용합니다. (스레드는 나중에 학습 예정)

```java
void method() {
	class DownloadThread extends Thread { ... }
    DownloadThread thread = new DownloadThread();
    thread.start();
}
```

#### 예제

```java
// A.java
/** 바깥 클래스 **/
class A {
    A() {
        System.out.println("A 객체 생성됨");
    }

    /** 인스턴스 멤버 클래스 **/
    class B {
        B() {
            System.out.println("B 객체 생성됨");
        }
        int field1;
        void method1() {}
    }

    /** 정적 멤버 클래스 **/
    static class C {
        C() {
            System.out.println("C 객체 생성됨");
        }
        int field1;
        static int field2;
        void method1() {}
        static void method2() {}
    }

    void method() {
        /** 로컬 클래스 **/
        class D {
            D() {
                System.out.println("D 객체 생성됨");
            }
            int field1;
            void method1() {}
        }
        D d = new D();
        d.field1 = 3;
        d.method1();
    }
}

// Main.java
public class Main {
    public static void main(String[] args) {
        A a = new A();

        // 인스턴스 멤버 클래스 객체 생성
        A.B b = a.new B();
        b.field1 = 3;
        b.method1();

        // 정적 멤버 클래스 객체 생성
        A.C c = new A.C();
        c.field1 = 3;
        c.method1();
        A.C.field2 = 3;
        A.C.method2();

        // 로컬 클래스 객체 생성을 위한 메소드 호출
        a.method();
    }
}
```

<br>

## 중첩 클래스의 접근 제한
### 바깥 필드와 메소드에서 사용 제한
멤버 클래스가 인스턴스 또는 정적으로 선언됨에 따라 바깥 클래스와 필드와 메소드에 사용 제한이 생깁니다.

```java
public class A {
	// 인스턴스 필드
    B field1 = new B(); // O
    C field2 = new C(); // O
    
    // 인스턴스 메소드
    void method1() {
    	B var1 = new B(); // O
        C var2 = new C(); // O
    }
    
    // 정적 필드 초기화
    static B field3 = new B(); // X
    static C field4 = new C(); // O
    
    // 정적 메소드
    static void method2() {
    	B var1 = new B(); // X
        C var2 = new C(); // O
    }
    
    // 인스턴스 멤버 클래스
    class B {}
    
    // 정적 멤버 클래스
    static class C {}
}
```

<br>

### 멤버 클래스에서 사용 제한
멤버 클래스가 인스턴스 또는 정적으로 선언됨에 따라 멤버 클래스 내부에서 바깥 클래스와 필드와 메소드를 접근할 때에도 사용 제한이 따릅니다.

```java
public class A {
	int field1;
    void method1() {}
    
    static int field2;
    static void method2() {}
    
    class B {
    	void method() {
        	// 모든 필드와 메소드에 접근 가능
        	field1 = 10;
            method1();
            
            field2 = 10;
            method2();
        }
    }
    
    static class C {
    	void method() {
        	// 인스턴스 필드와 메소드 접근 불가
            field1 = 10;
            method1();
            
            field2 = 10;
            method2();
        }
    }
}
```

<br>

### 로컬 클래스에서 사용 제한
로컬 클래스 내부에서는 바깥 클래스의 필드나 메소드를 제한 없이 사용할 수 있습니다. 문제는 메소드의 매개 변수나 로컬 변수를 로컬 클래스에서 사용할 때입니다. 로컬 클래스의 객체는 메소드 실행이 끝나도 힙 메모리에 존재해서 계속 사용될 수 있습니다. 매개 변수나 로컬 변수는 메소드 실행이 끝나면 스택 메모리에서 사라지기 때문에 로컬 객체에서 사용할 경우 문제가 발생합니다.

자바는 이 문제를 해결하기 위해 컴파일 시 로컬 클래스에서 사용하는 매개 변수나 로컬 변수의 값을 로컬 클래스 내부에 복사해 두고 사용합니다. 그리고 매개 변수나 로컬 변수가 수정되어 값이 변경되면 로컬 클래스에 복사해 둔 값과 달라지는 문제를 해결하기 위해 매개 변수나 로컬 변수를 final로 선언해서 수정을 막습니다.

> 결론적으로 로컬 클래스에서 사용 가능한 것은 final로 선언된 매개 변수와 로컬 변수

- 자바 7 이전까지는 final 키워드 없이 선언된 매개 변수나 로컬 변수를 로컬 클래스에서 사용하면 컴파일 에러가 발생했음
- 자바 8부터는 final 선언을 하지 않아도 final의 특성을 갖게됨
- final 키워드 존재 여부의 차이점은 로컬 클래스의 복사 위치
- final 키워드가 있다면 로컬 클래스의 메소드 내부에 지역 변수로 복사되고, 없다면 로컬 클래스의 필드로 복사됨

```java
void outMethod(final int arg1, int arg2) {
	final int var1 = 1;
    int var2 = 2;
    
    class LocalClass {
    	void method() {
        	int result = arg1+arg2+var1+var2;
        }
    }
}

// 복사 결과
class LocalClass {
	int arg2 = 매개값;
    int var2 = 2;
    
    void method() {
    	int arg1 = 매개값;
        int var1 = 1;
        int result = arg1+arg2+var1+var2;
    }
}
```

> 내부 복사 위치보다 로컬 클래스에서 사용된 매개 변수와 로컬 변수는 모두 final 특성을 갖는다는 것이 중요함

<br>

### 중첩 클래스에서 바깥 클래스 참조 얻기
클래스 내부에서 this는 객체 자신의 참조입니다. 중첩 클래스에서 this 키워드를 사용하면 바깥 클래스의 객체 참조라 아니라, 중첩 클래스의 객체 참조가 됩니다. 따라서 중첩 클래스 내부에서 `this.필드`, `this.메소드()`로 호출하면 중첩 클래스의 필드와 메소드가 사용됩니다. 중첩 클래스 내부에서 바깥 클래스의 객체 참조를 얻으려면 바깥 클래스의 이름을 this 앞에 붙여줍니다.

```java
바깥클래스.this.필드
바깥클래스.this.메소드();
```

<br>

## 중첩 인터페이스
중첩 인터페이스는 클래스의 멤버로 선언된 인터페이스를 의미하고, 특히 UI 프로그래밍에서 이벤트를 처리할 목적으로 많이 활용합니다. 아래 예제는 Button을 클릭했을 때 Button 클래스 내부에 선언된 중첩 인터페이스를 구현한 객체만 받아서 이벤트를 처리합니다.

#### 예제

```java
// Button.java
public class Button {
    OnClickListener listener;

    void setOnClickListener(OnClickListener listener) { // 매개 변수의 다형성
        this.listener = listener;
    }

    void touch() { // 구현 객체의 메소드 호출
        listener.onClick();
    }
    
    interface OnClickListener { // 중첩 인터페이스
        void onClick();
    }
}

// CallListener.java
public class CallListener implements Button.OnClickListener {
    @Override
    public void onClick() {
        System.out.println("전화를 겁니다.");
    }
}

// MessageListener.java
public class MessageListener implements Button.OnClickListener {
    @Override
    public void onClick() {
        System.out.println("메시지를 보냅니다.");
    }
}

// Main.java
public class Main {
    public static void main(String[] args) {
        Button btn = new Button();

        btn.setOnClickListener(new CallListener());
        btn.touch();

        btn.setOnClickListener(new MessageListener());
        btn.touch();
    }
}
```

<br>

## 익명 객체
익명 객체는 단독으로 생성할 수 없고 클래스를 상속하거나 인터페이스를 구현해야만 생성할 수 있습니다. 익명 객체는 필드의 초기값이나 로컬 변수의 초기값, 매개 변수의 매개값으로 주로 대입됩니다. 주로 UI 이벤트 처리 객체나 스레드 객체를 간편하게 생성할 목적으로 활용합니다.

<br>

### 익명 자식 객체 생성

```java
class Child extends Parent { } // 자식 클래스 선언

class A {
	Parent field = new Child(); // 필드에 자식 객체 대입
    void method() {
    	Parent localVar = new Child(); // 로컬 변수에 자식 객체 대입
    }
}

// 위의 경우를 익명 객체로 생성
class A {
	Parent field = new Parent() {
    	int childField;
        void childMethod() { ... }
        @Override
        void parentMethod() { ... }
    };
}
```

```java
부모클래스 [필드|변수] = new 부모클래스(매개값, ... ) {
	// 필드
    // 메소드
};
```

부모클래스(매개값, ... ) {}은 부모 클래스를 상속해서 중괄호와 같이 자식 클래스를 선언하라는 뜻이고, new 연산자는 이렇게 선언된 자식 클래스를 객체로 생성합니다.

익명 자식 객체에 새롭게 정의된 필드와 메소드는 익명 자식 객체 내부에서만 사용되고, 외부에서는 필드와 메소드에 접근할 수 없습니다. 익명 자식 객체는 부모 타입 변수에 대입되므로 부모 타입에 선언된 것만 사용할 수 있기 때문입니다.

```java
class A {
	Parent field = new Parent() {
    	int childField;
        void childMethod() {}
        @Override
        void parentMethod() {
        	childField = 3;
            childMethod();
        }
    };
    
    void method() {
    	field.childField = 3; // X
        field.childMethod(); // X
        field.parentMethod(); // O
    }
}
```

<br>

### 익명 구현 객체 생성

```java
인터페이스 [필드|변수] = new 인터페이스() {
	// 인터페이스에 선언된 추상 메소드의 실체 메소드 선언
    // 필드
    // 메소드
};
```

<br>

### 익명 객체의 로컬 변수 사용
익명 객체 내부에서는 바깥 클래스의 필드나 메소드는 제한 없이 사용할 수 있습니다. 문제는 메소드의 매개 변수나 로컬 변수를 익명 객체에서 사용할 때입니다. 메소드 내에서 생성된 익명 객체는 메소드 실행이 끝나도 힙 메모리에 존재해서 계속 사용할 수 있습니다. 매개 변수나 로컬 변수는 메소드 실행이 끝나면 스택 메모리에서 사라지기 때문에 익명 객체에서 사용할 수 없게 됩니다.
 
위에서 살펴본 로컬 클래스와 익명 클래스는 클래스 이름의 존재 여부만 다를 뿐 동작 방식은 동일하기 때문에 같은 문제가 발생합니다. 그래서 익명 객체 내부에서 메소드의 매개 변수나 로컬 변수를 사용할 경우, 이 변수들은 final 특성을 가져야 합니다.

#### 예제

```java
// Calculatable.java
public interface Calculatable {
	public int sum();
}

// Anonymous.java
public class Anonymous {
	private int field;
    
    public void method(final int arg1, int arg2) {
    	final int var1 = 0;
        int var2 = 0;
        
        field = 10;
        
        // arg1 = 20;
        // arg2 = 20;
        
        // var1 = 30;
        // var2 = 30;
        
        Calculatable cal = new Calculatable() {
        	@Override
            public int sum() {
            	int result = field + arg1 + arg2 + var1 + var2;
                return result;
            }
        };
        
        System.out.println(cal.sum());
    }
}

// Main.java
public class Main {
	public static void main(String[] args) {
    	Anonymous anony = new Anonymous();
        anony.method(0, 0);
    }
}
```

<br>

## 레퍼런스
- 이것이 자바다: 신용권의 Java 프로그래밍 정복
- 중첩 클래스와 중첩 인터페이스: https://velog.io/@petit-prince/%EC%9D%B4%EA%B2%83%EC%9D%B4-%EC%9E%90%EB%B0%94%EB%8B%A4-9-%EC%A4%91%EC%B2%A9-%ED%81%B4%EB%9E%98%EC%8A%A4%EC%99%80-%EC%A4%91%EC%B2%A9-%EC%9D%B8%ED%84%B0%ED%8E%98%EC%9D%B4%EC%8A%A4
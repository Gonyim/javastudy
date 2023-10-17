## 멀티 스레드 개념
### 프로세스와 스레드
운영체제에서는 실행 중인 하나의 애플리케이션을 프로세스`process`라고 부릅니다. 자세히는 사용자가 애플리케이션을 실행하면 운영체제로부터 실행에 필요한 메모리를 할당받아 애플리케이션의 코드를 실행하는데 이것을 프로세스라고 합니다. 하나의 애플리케이션은 다중 프로세스`멀티 프로세스`를 만들기도 하는데, 크롬 브라우저를 두 개 실행했다면 두 개의 크롬 프로세스가 생성된 것입니다.

운영체제는 멀티 태스킹`두 가지 이상의 작업을 동시에 처리하는 것`을 할 수 있도록 CPU 및 메모리 자원을 프로세스마다 적절히 할당해주고, 병렬로 실행시킵니다. 멀티 태스킹이 꼭 멀티 프로세스를 뜻하지는 않습니다. 미디어 플레이어와 메신저처럼 한 프로세스 내에서 멀티 태스킹을 할 수 있도록 만들어진 애플리케이션들도 있기 때문입니다. 이렇게 하나의 프로세스에서 두 가지 이상의 작업을 처리할 때 `멀티 스레드`가 사용됩니다.

![MultiProcessing Vs MultiThreading](https://velog.velcdn.com/images/kid/post/735f8c6d-7b9e-4f87-8e74-23db2a181d3e/image.png)

> thread는 사전적 의미로 한 가닥의 실이라는 뜻인데, 한 가지 작업을 실행하기 위해 순차적으로 실행할 코드를 실처럼 이어 놓았다고 해서 유래된 이름

- 멀티 프로세스가 애플리케이션 단위의 멀티 태스킹이라면 멀티 스레드는 애플리케이션 내부에서의 멀티 태스킹이라고 볼 수 있음
- `멀티 프로세스`는 운영체제엇 할당받은 자신의 메모리를 가지고 실행하기 때문에 서로 독립적
- `멀티 스레드`는 하나의 프로세스 내부에 생성되기 때문에 하나의 스레드가 예외를 발생시키면 프로세스 자체가 종료될 수 있음 (다른 스레드에게 영향을 미치게 됨)

<br>

### 메인 스레드
모든 자바 애플리케이션은 메인 스레드`main thread`가 `main()` 메소드를 실행하면서 시작됩니다. 메인 스레드는 필요에 따라 작업 스레드들을 만들어서 병렬로 코드를 실행할 수 있습니다.

- 싱글 스레드 애플리케이션에서는 메인 스레드가 종료되면 프로세스도 종료됨
- 멀티 스레드 애플리케이션에서는 실행 중인 스레드가 하나라도 있다면 프로세스가 종료되지 않음

<br>

## 작업 스레드 생성과 실행
자바에서는 작업 스레드도 객체로 생성됩니다. java.lang.Thread 클래스를 직접 객체화해서 생성할 수도 있고, Thread를 상속해서 하위 클래스를 만들어 생성할 수도 있습니다.

<br>

### Thread 클래스로부터 직접 생성
클래스로부터 작업 스레드 객체를 직접 생성하려면 Runnable을 매개값으로 갖는 생성자를 호출합니다.

```java
Thread thread = new Thread(Runnable target);
```

> Runnable은 작업 스레드가 실행할 수 있는 코드를 가지고 있는 객체라고 해서 붙여진 이름

Runnable은 인터페이스 타입이기 때문에 구현 객체를 만들어 대입해야 합니다. Runnable에는 `run()` 메소드가 정의되어 있는데, 구현 클래스는 해당 메소드를 재정의해서 작업 스레드가 실행할 코드를 작성합니다.

```java
class Task implements Runnable {
	public void run() {
    	스레드가 실행할 코드;
    }
}
```

Runnable은 작업 내용을 가지고 있는 객체이고 실제 스레드는 아닙니다. Runnable 구현 객체를 생성한 후, 이것을 매개값으로 Thread 생성자를 호출하면 작업 스레드가 생성됩니다.

```java
Runnable task = new Task();

Thread thread = new Thread(task);
```

Thread 생성자를 호출할 때 Runnable 익명 객체를 매개값으로 사용할 수 있습니다.

```java
Thread thread = new Thread(new Runnable() {
	public void run() {
    	스레드가 실행할 코드;
    }
});
```

Runnable 인터페이스는 하나의 메소드만 정의되어 있기 때문에 함수적 인터페이스입니다. 그래서 다음과 같이 람다식을 매개값으로 사용할 수도 있습니다. (자바 8부터 사용 가능)

```java
Thread thread = new Thread(() -> {
	스레드가 실행할 코드;
});
```

작업 스레드는 생성되는 즉시 실행되지 않고, `start()` 메소드를 호출해야 실행됩니다. start() 메소드가 호출되면, 작업 스레드는 매개값으로 받은 `run()` 메소드를 실행하면서 자신의 작업을 처리합니다.

```java
thread.start();
```

#### 예제 - 0.5초 주기로 비프(beep)음을 발생시키면서 동시에 프린팅하는 작업

```java
import java.awt.*;
import java.io.IOException;

public class Main {
    public static void main(String[] args) throws IOException {
        Thread thread = new Thread(new Runnable() {
            @Override
            public void run() {
                Toolkit toolkit = Toolkit.getDefaultToolkit();
                for(int i=0; i<5; i++) {
                    toolkit.beep();
                    try {
                        Thread.sleep(500);
                    } catch (Exception e) {
                        e.printStackTrace();
                    }
                }
            }
        });
        thread.start();

        for (int i=0; i<5; i++) {
            System.out.println("띵");
            try {
                Thread.sleep(500);
            } catch (Exception e) {
                e.printStackTrace();
            }
        }
    }
}
```

<br>

### Thread 하위 클래스로부터 생성
Thread 클래스를 상속하고 run 메소드를 재정의해서 스레드가 실행할 코드를 작성하면, Thread의 하위 클래스로 작업 스레드를 정의하면서 작업 내용을 포함시킬 수 있습니다.

```java
public class WorkerThread extends Thread {
	@Override
    public void run() {
    	스레드가 실행할 코드;
    }
}
Thread thread = new WorkerThread();

// 익명 객체 사용
Thread thread = new Thread() {
	public void run() {
    	스레드가 실행할 코드;
    }
};
```

#### 예제

```java
// BeepThread.java
public class BeepThread extends Thread {
    @Override
    public void run() {
        Toolkit toolkit = Toolkit.getDefaultToolkit();
        for(int i=0; i<5; i++) {
            toolkit.beep();
            try {
                Thread.sleep(500);
            } catch (Exception e) {
                e.printStackTrace();
            }
        }
    }
}

// Main.java
public class Main {
    public static void main(String[] args) {
        Thread thread = new BeepThread();
        thread.start();

        for (int i=0; i<5; i++) {
            System.out.println("띵");
            try {
                Thread.sleep(500);
            } catch (Exception e) {
                e.printStackTrace();
            }
        }
    }
}
```

<br>

### 스레드의 이름
스레드는 자신의 이름을 가지고 있습니다. 큰 역할을 하는 것은 아니고 디버깅할 때 어떤 스레드가 어떤 작업을 하는지 확인하는 목적으로 가끔 사용됩니다. 메인 스레드는 `main`이라는 이름을 가지고 있고, 직접 생성한 스레드는 자동적으로 `Thread-n`이라는 이름이 설정됩니다. 다른 이름으로 설정하고 싶다면 Thread 클래스의 `setName()` 메소드를 사용합니다.

```java
thread.setName("스레드 이름");
```

스레드 이름을 알고 싶을 경우에는 `getName()` 메소드를 사용합니다.

```java
thread.getName();
```

스레드 객체의 참조를 알고 싶다면 Thread의 정적 메소드인 `currentThread()`로 코드를 실행하는 현재 스레드의 참조를 얻을 수 있습니다.

```java
Thread thread = Thread.currentThread();
```

<br>

## 스레드 우선순위
멀티 스레드는 동시성`Concurrency` 또는 병렬성`Parallelism`으로 실행됩니다. **동시성**은 다중 작업을 위해 하나의 코어에서 멀티 스레드가 번갈아가며 실행하는 성질을 말하고, **병렬성**은 다중 작업을 위해 멀티 코어에서 개별 스레드를 동시에 실행하는 성질입니다. 싱글 코어 CPU를 이용한 멀티 스레드 작업은 병렬적으로 실행되는 것처럼 보이지만, 번갈아가며 실행하는 동시성 작업입니다.

스레드의 개수가 코어의 수보다 많을 경우, 스레드를 어떤 순서에 의해 동시성으로 실행할 것인가를 결정해야 하는데, 이것을 `스레드 스케줄링`이라고 합니다. 자바의 스레드 스케줄링은 우선순위`Priority` 방식과 순환 할당`Round-Robin` 방식을 사용합니다. **우선순위 방식**은 우선순위가 높은 스레드가 실행 상태를 더 많이 가지도록 하는 것이고, **순환 할당 방식**은 시간 할당량`Time Slice`를 정해서 하나의 스레드를 정해진 시간만큼 실행하고 다시 다른 스레드를 실행하는 방식입니다.

- `우선순위 방식`은 스레드 객체에 우선 순위 번호를 부여할 수 있기 때문에 개발자가 제어 가능
- `순환 할당 방식`은 JVM에 의해서 정해지기 때문에 코드로 제어 불가

우선순위는 1에서 10까지 부여되고, 숫자가 높을수록 우선순위가 높습니다. 우선순위를 부여하지 않으면 기본적으로 5의 우선순위를 할당받습니다. 우선순위를 변경하고 싶다면 Thread 클래스가 제공하는 `setPriority()` 메소드를 사용합니다.

```java
thread.setPriority(우선순위);

// Thread 클래스의 상수 사용
thread.setPriority(Thread.MAX_PRIORITY); // 10
thread.setPriority(Thread.NORM_PRIORITY); // 5
thread.setPriority(Thread.MIN_PRIORITY); // 1
```

<br>

## 동기화 메소드와 동기화 블록
### 공유 객체를 사용할 때의 주의할 점
싱글 스레드 프로그램에서는 한 개의 스레드가 객체를 독차지해서 사용하면 되지만, 멀티 스레드 프로그램에서는 스레드들이 객체를 공유해서 작업하는 경우가 있습니다. 이 경우에 스레드 A를 사용하던 객체가 스레드 B에 의해 상태가 변경될 수 있기 때문에 스레드 A가 의도했던 것과는 다른 결과를 산출할 수도 있습니다.

#### 예제

```java
// Main.java
public class Main {
    public static void main(String[] args) {
        Calculator calculator = new Calculator();

        User1 user1 = new User1(); // User1 스레드 생성
        user1.setCalculator(calculator); // 공유 객체 설정
        user1.start(); // User1 스레드 시작

        User2 user2 = new User2(); // User2 스레드 생성
        user2.setCalculator(calculator); // 공유 객체 설정
        user2.start(); // User2 스레드 시작
    }
}

// Calculator.java
public class Calculator {
    private int memory;

    public int getMemory() {
        return memory;
    }

    public void setMemory(int memory) { // 계산기 메모리에 값을 저장하는 메소드
        this.memory = memory; // 매개값을 memory 필드에 저장
        try {
            Thread.sleep(2000); // 스레드를 2초간 일시 정지
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        System.out.println(Thread.currentThread().getName() + ": " + this.memory);
    }
}

// User1.java
public class User1 extends Thread {
    private Calculator calculator;

    public void setCalculator(Calculator calculator) {
        this.setName("User1"); // 스레드 이름을 User1로 설정
        this.calculator = calculator; // 공유 객체인 Calculator를 필드에 저장
    }

    public void run() {
        calculator.setMemory(100); // Calculator의 메모리에 100을 저장
    }
}

// User2.java
public class User2 extends Thread {
    private Calculator calculator;

    public void setCalculator(Calculator calculator) {
        this.setName("User2"); // 스레드 이름을 User2로 설정
        this.calculator = calculator; // 공유 객체인 Calculator를 필드에 저장
    }

    public void run() {
        calculator.setMemory(50); // Calculator의 메모리에 50을 저장
    }
}
```

<br>

### 동기화 메소드 및 동기화 블록
스레드가 사용 중인 객체를 다른 스레드가 변경할 수 없도록 하려면 스레드 작업이 끝날 때까지 객체에 잠금을 걸어서 다른 스레드가 사용할 수 없도록 해야 합니다. 멀티 스레드 프로그램에서 단 하나의 스레드만 실행할 수 있는 코드 영역을 임계 영역`critical section`이라고 합니다. 자바는 임계 영역을 지정하기 위해 동기화`synchronized` 메소드와 동기화 블록을 제공합니다.

```java
public synchronized void method() {
	임계 영역; // 단 하나의 스레드만 실행
}
```

동기화 메소드는 메소드 전체 내용이 임계 영역이므로 스레드가 동기화 메소드를 실행하는 즉시 객체에는 잠금이 일어나고, 스레드가 동기화 메소드를 실행 종료하면 잠금이 풀립니다. 메소드 전체 내용이 아니라 일부 내용만 임계 영역으로 만들고 싶다면 다음과 같이 동기화 블록을 만듭니다.

```java
public void method() {
	// 여러 스레드가 실행 가능한 영역
    ...
    
    synchronized(공유객체) { // 공유 객체가 객체 자신이면 this 사용 가능
    	임계 영역 // 단 하나의 스레드만 실행
    }
}
```

#### 예제

```java
// Calculator.java
public class Calculator {
    private int memory;

    public int getMemory() {
        return memory;
    }

    public synchronized void setMemory(int memory) { // 계산기 메모리에 값을 저장하는 메소드
        this.memory = memory; // 매개값을 memory 필드에 저장
        try {
            Thread.sleep(2000); // 스레드를 2초간 일시 정지
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        System.out.println(Thread.currentThread().getName() + ": " + this.memory);
    }
}
```

```java
// 동기화 블록 사용
public void setMemory(int memory) {
    synchronized (this) {
        this.memory = memory;
        try {
            Thread.sleep(2000);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        System.out.println(Thread.currentThread().getName() + ": " + this.memory);
    }
}
```

스레드가 동기화 블록으로 들어가면 this`Calculator 객체`를 잠그고 동기화 블록을 실행합니다. 동기화 블록을 모두 실행할 때까지 다른 스레드들은 this`Calculator 객체`의 모든 동기화 메소드 또는 동기화 블록을 실행할 수 없게 됩니다.

<br>

## 스레드 상태
`start()` 메소드를 호출하면 곧바로 스레드가 실행되는 것이 아니라 실행 대기 상태`아직 스케줄링이 되지 않아서 실행을 기다리고 있는 상태`가 됩니다. **실행 대기 상태**에 있는 스레드 중에서 스레드 스케줄링으로 선택된 스레드가 CPU를 점유하고 `run()` 메소드를 실행합니다. 이때를 **실행 상태**라고 합니다. 실행 상태의 스레드는 메소드를 모두 실행하기 전에 스케줄링에 의해 다시 실행 대기 상태로 돌아갈 수 있습니다. 그리고 실행 대기 상태에 있는 다른 스레드가 선택되어 실행 상태가 됩니다. 이렇게 실행 대기 상태와 실행 상태를 번갈아가면서 자신의 `run()` 메소드를 조금씩 실행합니다. 메소드가 종료되면 스레드의 실행이 멈추게 되고 **종료 상태**가 됩니다. 경우에 따라서 실행 상태에서 일시 정지 상태로 가기도 하는데, **일시 정지 상태**는 스레드가 실행할 수 없는 상태입니다.

이러한 스레드의 상태를 확인할 수 있도록 자바 5부터 Thread 클래스에 `getState()` 메소드가 추가되었습니다. 스레드 상태에 따라서 Thread.state 열거 상수를 리턴합니다.

|상태|열거 상수|설명|
|---|---|---|
|객체 생성|NEW|스레드 객체가 생성, 아직 start() 메소드가 호출되지 않은 상태|
|실행 대기|RUNNABLE|실행 상태로 언제든지 갈 수 있는 상태|
|일시 정지|WAITING<br>TIMED_WAITING<br>BLOCKED|다른 스레드가 통지할 때까지 기다리는 상태<br>주어진 시간 동안 기다리는 상태<br>사용하고자 하는 객체의 락이 풀릴 때까지 기다리는 상태|
|종료|TERMINATED|실행을 마친 상태|

<br>

## 스레드 상태 제어
실행 중인 스레드의 상태를 변경하는 것을 **스레드 상태 제어**라고 합니다. 상태 제어가 잘못되면 프로그램은 불안정해집니다.

#### 스레드의 상태 변화를 가져오는 메소드

|메소드|설명|
|---|---|
|interrupt()|일시 정지 상태의 스레드에서 InterruptException 예외를 발생시켜, 예외 처리<br>코드(catch)에서 실행 대기 상태로 가거나 종료 상태로 갈 수 있도록 한다.|
|notify()<br>notifyAll()|동기화 블록 내에서 wait() 메소드에 의해 일시 정지 상태에 있는 스레드를 실행 대기<br>상태로 만든다.|
|resume()|suspend() 메소드에 의해 일시 정지 상태에 있는 스레드를 실행 대기 상태로 만든다.<br> - Deprecated (대신 notify(), notifyAll() 사용)|
|sleep(long mills)<br>sleep(long mills, int nanos)|주어진 시간 동안 스레드를 일시 정지 상태로 만든다. 주어진 시간이 지나면 자동적으로<br>실행 대기 상태가 된다.|
|join()<br>join(long mills)<br>join(long mills, int nanos)|join() 메소드를 호출한 스레드는 일시 정지 상태가 된다. 실행 대기 상태로 가려면,<br>join() 메소드를 멤버로 가지는 스레드가 종료되거나, 매개값으로 주어진 시간이 지나야 한다.|
|wait()<br>wait(long mills)<br>wait(long mills, int nanos)|동기화 블록 내에서 스레드를 일시 정지 상태로 만든다. 매개값으로 주어진 시간이<br>지나면 자동적으로 실행 대기 상태가 된다. 시간이 주어지지 않으면 notify(), notifyAll()<br>메소드에 의해 실행 대기 상태로 갈 수 있다.|
|suspend()|스레드를 일시 정지 상태로 만든다. resume() 메소드를 호출하면 다시 실행 대기 상태<br>가 된다. - Deprecated (대신 wait() 사용)|
|yield()|실행 중에 우선순위가 동일한 다른 스레드에게 실행을 양보하고 실행 대기 상태가 된다.|
|stop()|스레드를 즉시 종료시킨다. - Deprecated|

`wait()`, `notify()`, `notifyAll()` 은 Object 클래스의 메소드이고, 그 이외의 메소드들은 모두 Thread 클래스의 메소드들입니다.

<br>

### 주어진 시간동안 일시 정지 sleep()

```java
try {
	Thread.sleep(1000);
} catch (InterruptException e) {
	// interrupt() 메소드가 호출되면 실행
}
```

<br>

### 다른 스레드에게 실행 양보 yield()
`yield()` 메소드를 호출한 스레드는 실행 대기 상태로 돌아가고 동일한 우선순위 또는 높은 우선순위를 갖는 다른 스레드가 실행 기회를 가집니다.

```java
public void run() {
	while (true) {
    	if (work) {
    		System.out.println("ThreadA 작업 내용");
    	} else {
    		Thread.yield();
    	}
	}
}
```

<br>

### 다른 스레드의 종료를 기다림 join()
스레드는 다른 스레드와 독립적으로 실행하는 것이 기본이지만, 계산 작업을 하는 스레드가 모든 계산 작업을 마쳤을 때, 계산 결과값을 받아 이용하는 경우와 같이 다른 스레드가 종료될 때까지 기다렸다가 실행해야 하는 경우가 발생할 수도 있습니다.

```java
// ThreadA
threadB.start();
threadB.join(); // ThreadB가 종료될 때까지 일시 정지 상태
```

<br>

### 스레드 간 협업 wait(), notify(), notifyAll()
두 개의 스레드의 정확한 교대 작업이 필요한 경우, 자신의 작업이 끝나면 상대방 스레드를 일시 정지 상태에서 풀어주고, 자신은 일시 정지 상태로 만들어야 합니다. 이 방법의 핵심은 공유 객체입니다. 공유 객체는 두 스레드가 작업할 내용을 각각 동기화 메소드로 구분하고, 한 스레드가 작업을 완료하면 `notify()` 메소드를 호출해서 일시 정지 상태에 있는 다른 스레드를 실행 대기 상태로 만들고, 자신은 두 번 작업을 하지 않도록 `wait()` 메소드를 호출하여 일시 정지 상태로 만듭니다.

```java
// WorkObject.java
public class WorkObject { // 두 스레드의 작업 내용을 동기화 메소드로 작성한 공유 객체
    public synchronized void methodA() {
        System.out.println("ThreadA의 methodA() 작업 실행");
        notify(); // 일시 정지 상태에 있는 ThreadB를 실행 대기 상태로 만듬
        try {
            wait(); // ThreadA를 일시 정지 상태로 만듬
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }

    public synchronized void methodB() {
        System.out.println("ThreadB의 methodB() 작업 실행");
        notify(); // 일시 정지 상태에 있는 ThreadA를 실행 대기 상태로 만듬
        try {
            wait(); // ThreadB를 일시 정지 상태로 만듬
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }
}

// ThreadA.java
public class ThreadA extends Thread {
    private WorkObject workObject;

    public ThreadA(WorkObject workObject) {
        this.workObject = workObject; // 공유 객체를 매개값으로 받아 필드에 저장
    }

    @Override
    public void run() {
        for (int i=0; i<10; i++) { // 공유 객체의 methodA()를 10번 호출
            workObject.methodA();
        }
    }
}

// ThreadB.java
public class ThreadB extends Thread {
    private WorkObject workObject;

    public ThreadB(WorkObject workObject) {
        this.workObject = workObject; // 공유 객체를 매개값으로 받아 필드에 저장
    }

    @Override
    public void run() {
        for (int i=0; i<10; i++) { // 공유 객체의 methodB()를 10번 호출
            workObject.methodB();
        }
    }
}

// Main.java
public class Main {
    public static void main(String[] args) {
        WorkObject sharedObject = new WorkObject(); // 공유 객체 생성

        ThreadA threadA = new ThreadA(sharedObject);
        ThreadB threadB = new ThreadB(sharedObject);

        threadA.start();
        threadB.start();
    }
}
```

<br>

### 스레드의 안전한 종료 interrupt(), stop 플래그
사용자가 동영상을 끝까지 보지 않고 멈춤을 요구할 때처럼 경우에 따라서는 실행 중인 스레드를 즉시 종료할 필요가 있습니다.

> `stop()` 메소드는 사용 중이던 자원들이 불안전한 상태로 남겨지기 때문에 deprecated되었습니다.

#### stop 플래그
스레드는 `run()` 메소드가 끝나면 자동적으로 종료되므로, 메소드가 정상적으로 종료되도록 유도하는 것이 좋은 방법입니다.

```java
public class XXXThread extends Thread {
	private boolean stop; // stop 플래그 필드
    
    public void run() {
    	while (!stop) { // stop이 true가 되면 run() 종료
        	스레드가 반복 실행하는 코드;
        }
        // 스레드가 사용한 자원 정리
    }
}
```

#### interrupt()
`interrupt()` 메소드는 스레드가 일시 정지 상태에 있을 때 InterruptException 예외를 발생시키는 역할을 합니다. 

```java
// Main.java
public class Main {
    public static void main(String[] args) {
        Thread thread = new PrintThread2();
        thread.start();

        try {
            Thread.sleep(1000);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        thread.interrupt();
    }
}

// PrintThread2.java
public class PrintThread2 extends Thread {
    public void run() {
        try {
            while (true) {
                System.out.println("실행 중");
                Thread.sleep(1);
            }
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        System.out.println("자원 정리");
        System.out.println("실행 종료");
    }
}
```

interrupt() 메소드는 스레드가 일시 정지 상태가 되면 예외를 발생시키기 때문에 Thread.sleep()을 사용했습니다. 일시 정지를 만들지 않고도 interrupt() 호출 여부를 알 수 있는 방법이 있는데, interrupt() 메소드가 호출되었다면 스레드의 `interrupted()`와 `isInterrupted()` 메소드는 true를 리턴합니다. `interrupted()`는 정적 메소드이고, `isInterrupted()`는 인스턴스 메소드입니다.

```java
// PrintThread2.java
public class PrintThread2 extends Thread {
    public void run() {
        while (true) {
        	System.out.println("실행 중");
            if (Thread.interrupted()) {
            	break;
            }
        }

        System.out.println("자원 정리");
        System.out.println("실행 종료");
    }
}
```

<br>

## 데몬 스레드
데몬`daemon` 스레드는 주 스레드의 작업을 돕는 보조적인 역할을 수행하는 스레드입니다. 그래서 주 스레드가 종료되면 데몬 스레드는 강제적으로 자동 종료됩니다. 이 부분을 제외하면 일반 스레드와 큰 차이가 없습니다. 스레드를 데몬으로 만들기 위해서는 주 스레드가 데몬이 될 스레드의 setDaemon(true)를 호출합니다.

```java
public static void main(String[] args) {
	AutoSaveThread thread = new AutoSaveThread();
    thread.setDaemon(true);
    thread.start();
    ...
}
```

실행 중인 스레드가 데몬 스레드인지 구별하는 방법은 `isDaemon()` 메소드의 리턴값으로 알 수 있습니다.

> start() 메소드가 호출된 후 setDaemon(true)를 호출하면 IllegalThreadStateException이 발생하기 때문에 strat() 메소드 호출 전에 setDaemon(true)를 호출해야 합니다.

<br>

## 스레드 그룹
스레드 그룹은 관련된 스레드를 묶어서 관리할 목적으로 이용됩니다.

- JVM이 실행되면 system 스레드 그룹 생성
- JVM 운영에 필요한 스레드들을 system 스레드 그룹에 포함시킴
- system의 하위 스레드 그룹으로 main을 만들고 메인 스레드를 main 스레드 그룹에 포함시킴

스레드는 반드시 하나의 스레드 그룹에 포함되므로, 명시적으로 스레드 그룹에 포함시키지 않으면 기본적으로 자신을 생성한 스레드와 같은 스레드 그룹에 속하게 됩니다. 그래서 작업 스레드는 일반적으로 main 스레드 그룹에 속합니다.

<br>

### 스레드 그룹 이름 얻기

```java
ThreadGroup group = Thread.currentThread().getThreadGroup();
String groupName = group.getName();
```

Thread의 정적 메소드인 `getAllStackTraces()`를 이용하면 프로세스 내에서 실행하는 모든 스레드에 대한 정보를 얻을 수 있습니다.

```java
Map<Thread, StackTraceElement[]> map = Thread.getAllStackTraces();
```

getAllStackTraces() 메소드는 Map 타입의 객체를 리턴하는데, 키는 스레드 객체이고 값은 스레드의 상태 기록들을 갖고 있는 StackTraceElement\[] 배열입니다.

<br>

### 스레드 그룹 생성

```java
ThreadGroup tg = new ThreadGroup(String name);
ThreadGroup tg = new ThreadGroup(ThreadGroup parent, String name);
```

새로운 스레드 그룹을 생성한 후, 이 그룹에 스레드를 포함시키려면 Thread 객체를 생성할 때 생성자 매개값으로 스레드 그룹을 지정합니다.

```java
Thread t = new Thread(ThreadGroup group, Runnable target);
Thread t = new Thread(ThreadGroup group, Runnable target, String name);
Thread t = new Thread(ThreadGroup group, Runnable target, String name, long stackSize);
Thread t = new Thread(ThreadGroup group, String name);
```

Runnable 타입의 target은 구현 객체를 의미하고, String 타입의 name은 스레드의 이름입니다. 그리고 long 타입의 stackSize는 JVM이 해당 스레드에 할당할 stack 크기입니다.

<br>

### 스레드 그룹의 일괄 interrupt()
스레드 그룹의 interrupt() 메소드는 포함된 모든 스레드의 interrupt() 메소드를 내부적으로 호출해줍니다.

> 예외 처리는 해주지 않기 때문에 개별 스레드가 예외 처리를 해야 합니다.

#### 스레드 그룹이 가지고 있는 주요 메소드

|리턴 타입|메소드|설명|
|---|---|---|
|int|activeCount()|현재 그룹 및 하위 그룹에서 활동 중인 모든 스레드의 수를 리턴한다.|
|int|activeGroupCount()|현재 그룹에서 활동 중인 모든 하위 그룹의 수를 리턴한다.|
|void|checkAccess()|현재 스레드가 스레드 그룹을 변경할 권한이 있는지 체크하고, 만약 권한이 없으면 SecurityException을 발생시킨다.|
|void|destroy()|현재 그룹 및 하위 그룹을 모두 삭제한다. 단, 그룹 내에 포함된 모든 스레드들이 종료 상태가 되어야 한다.|
|boolean|isDestroyed()|현재 그룹이 삭제되었는지 여부를 리턴한다.|
|int|getMaxPriority()|현재 그룹에 포함된 스레드가 가질 수 있는 최대 우선순위를 리턴한다.|
|void|setMaxPriority(int pri)|현재 그룹에 포함된 스레드가 가질 수 있는 최대 우선순위를 설정한다.|
|String|getName()|현재 그룹의 이름을 리턴한다.|
|ThreadGroup|getParent()|현재 그룹의 부모 그룹을 리턴한다.|
|boolean|parentOf(ThreadGroup g)|현재 그룹이 매개값으로 지정한 스레드 그룹의 부모인지 여부를 리턴한다.|
|boolean|isDaemon()|현재 그룹이 데몬 그룹인지 여부를 리턴한다.|
|void|setDaemon(boolean daemon)|현재 그룹을 데몬 그룹으로 설정한다.|
|void|list()|현재 그룹에 포함된 스레드와 하위 그룹에 대한 정보를 출력한다.|
|void|interrupt()|현재 그룹에 포함된 모든 스레드들을 interrupt한다.|

<br>

## 스레드풀
스레드풀`ThreadPool`은 작업 처리에 사용되는 스레드를 제한된 개수만큼 정해놓고 작업 큐`Queue`에 들어오는 작업들을 하니씩 스레드가 맡아 처리합니다. 작업 처리가 끝난 스레드는 다시 작업 큐에서 새로운 작업을 가져와 처리합니다. 그렇기 때문에 작업 처리 요청이 증폭되어도 스레드의 전체 개수가 늘어나지 않으므로 애플리케이션의 성능이 급격히 저하되지 않습니다.

자바는 스레드풀을 생성하고 사용할 수 있도록 java.util.concurret 패키지에서 `ExecutorService` 인터페이스와 `Executors` 클래스를 제공합니다. Executors의 정적 메소드를 이용해서 ExecutorService 구현 객체를 만들 수 있는데, 이것이 바로 스레드풀입니다.

![Thread Pool](https://velog.velcdn.com/images/kid/post/b99377c4-d23f-497f-aebd-489267f1fdd5/image.png)

<br>

### 스레드풀 생성 및 종료
#### 스레드풀 생성
ExecutorService 구현 객체는 Executors 클래스의 두 가지 메소드 중 하나를 이용해서 생성합니다.

|메소드명(매개 변수)|초기 스레드 수|코어 스레드 수|최대 스레드 수|
|---|---|---|---|
|newCachedThreadPool()|0|0|Integer.MAX_VALUE|
|newFixedThreadPool(int nThreads)|0|nThreads|nThreads|

초기 스레드 수는 객체가 생성될 때 기본적으로 생성되는 스레드 수이고, 코어 스레드 수는 스레드 수가 증가된 후 사용되지 않는 스레드를 스레드풀에서 제거할 때 최소한 유지해야 할 스레드 수입니다. 최대 스레드 수는 스레드풀에서 관리하는 최대 스레드 수입니다.

- `newCachedThreadPool()` 메소드로 생성된 스레드풀은 1개 이상의 스레드가 추가되었을 경우 60초 동안 추가된 스레드가 아무 작업을 하지 않으면 추가된 스레드를 종료하고 풀에서 제거함
- `newFixedThreadPool(int nThreads)` 메소드로 생성된 스레드풀은 스레드가 작업을 처리하지 않고 놀고 있더라도 스레드 개수가 줄지 않음

```java
ExecutorService executorService = Executors.newCachedThreadPool();
```

```java
ExecutorService executorService = Executors.newFixedThreadPool(
	Runtime.getRuntime().availableProcessors() // CPU 코어의 수만큼 최대 스레드 사용
);
```

코어 스레드 개수와 최대 스레드 개수를 설정하고 싶다면 `ThreadPoolExecutor` 객체를 생성하면 됩니다. 위의 두 메소드도 내부적으로 ThreadPoolExecutor 객체를 생성해서 리턴합니다.

```java
ExecutorService threadPool = new ThreadPoolExecutor(
	3, // 코어 스레드 개수
    100, // 최대 스레드 개수
    120L, // 놀고 있는 시간
    TimeUnit.SECONDS, // 놀고 있는 시간 단위
    new SynchronousQueue<Runnable>() // 작업 큐
);
```

<br>

#### 스레드풀 종료

|리턴 타입|메소드명(매개 변수)|설명|
|---|---|---|
|void|shutdown()|현재 처리 중인 작업뿐만 아니라 작업 큐에 대기하고 있는 모든 작업을<br>처리한 뒤에 스레드풀을 종료시킨다.|
|List< Runnable >|shutdownNow()|현재 작업 처리 중인 스레드를 interrupt해서 작업 중지를 시도하고<br>스레드풀을 종료시킨다. 리턴값은 작업 큐에 있는 미처리된 작업<br>(Runnable)의 목록이다.|
|boolean|awaitTermination(<br>long timeout,<br>TimeUnit unit)|shutdown() 메소드 호출 이후, 모든 작업 처리를 timeout 시간 내<br>에 완료하면 true를 리턴하고, 완료하지 못하면 작업 처리 중인 스레드<br>를 interrupt하고 false를 리턴한다.|

<br>

### 작업 생성과 처리 요청
#### 작업 생성
하나의 작업은 Runnable 또는 Callable 구현 클래스로 표현합니다. 둘의 차이점은 작업 처리 완료 후 리턴값이 있느냐 없느냐입니다.

```java
Runnable task = new Runnable() {
	@Override
    public void run() {
    	작업 내용
    }
}

Callable<T> task = new Callable<T>() {
	@Override
    public T call() throws Exception {
    	작업 내용
        return T;
    }
}
```

<br>

#### 작업 처리 요청
작업 처리 요청은 ExecutorService의 작업 큐에 Runnable 또는 Callable 객체를 넣는 행위입니다.

|리턴 타입|메소드명(매개 변수)|설명|
|---|---|---|
|void|execute(Runnable command)|- Runnable을 작업 큐에 저장<br>- 작업 처리 결과를 받지 못함|
|Future< ? ><br>Future< V ><br>Future< V >|submit(Runnable task)<br>submit(Runnable task, V result)<br>submit(Callable< V > task)|- Runnable 또는 Callable을 작업 큐에 저장<br>- 리턴된 Future를 통해 작업 처리 결과를 얻을 수 있음|

- `execute()`는 작업 처리 결과를 받지 못하고 `submit()`은 작업 처리 결과를 받을 수 있도록 Future를 리턴함
- `execute()`는 작업 처리 도중 예외가 발생하면 스레드가 종료되고 스레드풀에서 제거됨
- `submit()`은 작업 처리 도중 예외가 발생하더라도 스레드는 종료되지 않고 다음 작업을 위해 재사용됨
- 스레드의 생성 오버헤더를 줄이기 위해서 `submit()`을 사용하는 것이 좋음

<br>

### 블로킹 방식의 작업 완료 통보
Future 객체는 작업이 완료될 때까지 기다렸다가`블로킹되었다가` 최종 결과를 얻는데 사용됩니다. 그래서 Future를 지연 완료`pending completion` 객체라고 합니다. Future를 이용한 블로킹 방식의 작업 완료 통보에서 주의할 점은 처리하는 스레드가 작업을 완료하기 전까지는 `get()` 메소드가 블로킹되므로 다른 코드를 실행할 수 없습니다. 만약 UI를 변경하고 이벤트를 처리하는 스레드가 get() 메소드를 호출하면 작업을 완료하기 전까지 UI를 변경할 수도, 이벤트를 처리할 수도 없게 됩니다. 그렇기 때문에 get() 메소드를 호출하는 스레드는 새로운 스레드이거나 스레드풀의 또 다른 스레드가 되어야 합니다.

```java
new Thread(new Runnable) {
	@Override
    public void run() {
    	try {
        	future.get();
        } catch (Exception e) {
        	e.printStackTrace();
        }
    }
}).start();

executorService.submit(new Runnable() {
	@Override
    public void run() {
    	try {
        	future.get();
        } catch (Exception e) {
        	e.printStackTrace();
        }
    }
});
```

<br>

### 콜백 방식의 작업 완료 통보
콜백은 애플리케이션이 스레드에게 작업 처리를 요청한 후, 스레드가 작업을 완료하면 특정 메소드를 자동 실행하는 기법입니다. 이때 자동 실행되는 메소드를 콜백 메소드라고 합니다.

![](https://velog.velcdn.com/images/kid/post/86b6af49-cdac-43da-88f8-251173b94d0e/image.png)

블로킹 방식은 작업 처리를 요청한 후 작업이 완료될 때까지 블로킹되지만, 콜백 방식은 작업 처리를 요청한 후 결과를 기다릴 필요 없이 다른 기능을 수행할 수 있습니다. 그 이유는 작업 처리가 완료되면 자동적으로 콜백 메소드가 실행되어 결과를 알 수 있기 때문입니다.

ExecutorService는 콜백을 위한 별도의 기능을 제공하지 않습니다. 하지만 Runnable 구현 클래스를 작성할 때 콜백 기능을 구현할 수 있습니다. 먼저 콜백 메소드를 가진 클래스가 있어야 하는데, 직접 정의해도 좋고 java.nio.channels.CompletionHandler를 이용해도 좋습니다.

```java
CompletionHandler<V, A> callback = new CompletionHandler<V, A>() {
	@Override
    public void completed(V result, A attachment) {
    }
    @Override
    public void failed(Throwable exc, A attachment) {
    }
};
```

`completed()`는 작업을 정상 처리 완료했을 때 호출되는 콜백 메소드이고, `failed()`는 작업 처리 도중 예외가 발생했을 때 호출되는 콜백 메소드입니다.

```java
Runnable task = new Runnable() {
	@Override
    public void run() {
    	try {
        	// 작업 처리
            V result = 코드;
            callback.completed(result, null);
        } catch (Exception e) {
        	callback.failed(e, null);
        }
    }
};
```

<br>

## 레퍼런스
- 이것이 자바다: 신용권의 Java 프로그래밍 정복
- Tug of War: MultiProcessing Vs MultiThreading: https://medium.com/@noueruzzaman/tug-of-war-multiprocessing-vs-multithreading-55341c1f2103
- Java 에서 스레드 풀(Thread Pool) 을 사용해 보자: https://tecoble.techcourse.co.kr/post/2021-09-18-java-thread-pool/
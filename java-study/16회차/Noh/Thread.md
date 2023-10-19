# 쓰레드(Thread)
## 프로세스와 쓰레드
* 프로세스(process)란 간단히 말해서 '실행 중인 프로그램(program)'이다
  * 프로그램을 실행하면 OS로부터 실행에 필요한 자원(메모리)을 할당받아 프로세스가 된다 <br>
<img width="684" alt="image" src="https://github.com/nohheeyeon/TIL/assets/130336617/9337cf66-5748-4869-81b8-4f68daf02f56"> <br>

* 프로세스는 프로그램을 수행하는데 필요한 데이터와 메모리 등의 자원 그리고 쓰레드로 구성되어 있으며 프로세스의 자원을 이용해서 실제로 작업을 수행하는 것이 바로 쓰레드다
  * 그래서 모든 프로세스에는 최소한 하나 이상의 쓰레드가 존재하며, 둘 이상의 쓰레드를 가진 프로세스를  '멀티쓰레드 프로세스(multi-threaded process)'라고 한다 <br>
<img width="625" alt="image" src="https://github.com/nohheeyeon/TIL/assets/130336617/401851f1-9def-4c7d-a895-5f0fd877bb17"> <br>
* 쓰레드를 프로세스라는 작업공간(공장)에서 작업을 처리하는 일꾼(worker)으로 생각하면 이해하기 쉽다!
* 하나의 프로세스가 가질 수 있는 쓰레드의 개수를 제한되어 있지 않으나 쓰레드가 작업을 수행하는데 개별적인 메모리 공간(호출스택)을 필요로 하기 때문에 프로세스의 메모리 한계에 따라 생성할 수 있는 쓰레드의 수가 결정된다
  * 실제로는 프로세스의 메모리 한계에 다다를 정도로 많은 쓰레드를 생성하는 일을 없을 것이니 걱정하지 않아도 된다
#### 멀티태스킹과 멀티쓰레딩
* 현재 우리가 사용하고 있는 윈도우나 유닉스를 포함한 대부분의 OS는 멀티태스킹(multi-tasking, 다중작업)을 지원하기 때문에 여러 개의 프로세스가 동시에 실행될 수 있다
  * 이와 마찬가지로 멀티쓰레딩은 하나의 프로세스 내에서 여러 쓰레드가 동시에 작업을 수행하는 것이다
* CPU의 코어(core)가 한 번에 단 하나의 작업만 수행할 수 있으므로, 실제로 동시에 처리되는 작업의 개수는 코어의 개수와 일치한다
  * 그러나 처리해야하는 쓰레드의 수는 언제나 코어의 개수보다 훨씬 많기 때문에 각 코어가 아주 짧은 시간 동안 여러 작업을 번갈아 가며 수행함으로써 여러 작업들이 모두 동시에 수행되는 것처럼 보이게 한다
    * 그래서 프로세스의 성능이 단순히 쓰레드의 개수에 비례하는 것은 아니며, 하나의 쓰레드를 가진 프로세스 보다 두 개의 쓰레드를 가진 프로세스가 오히려 더 낮은 성능을 보일 수도 있다
#### 멀티쓰레딩의 장단점
* 멀티쓰레딩의 장점
```java
- CPU의 사용률을 향상시킨다
- 자원을 보다 효율적으로 사용할 수 있다
- 사용자에 대한 응답성이 향상된다
- 작업이 분리되어 코드가 간결해진다
```
* 메신저로 채팅하면서 파일을 다운로드 받거나 음성대화를 나눌 수 있는 것이 가능한 이유가 바로 멀티쓰레드로 작성되어 있기 때문이다
* 여러 사용자에게 서비스를 해주는 서버 프로그램의 경우 멀티쓰레드로 작성하는 것은 필수적이어서 하나의 서버 프로세스가 여러 개의 쓰레드를 생성해서 쓰레드와 사용자의 요청이 일대일로 처리되도록 프로그래밍해야한다
* 만일 싱글쓰레드로 서버 프로그램을 작성한다면 사용자의 요청 마다 새로운 프로세스를 생성해야하는데 프로세스를 생성하는 것은 쓰레드를 생성하는 것에 비해 더 많은 시간과 메모리 공간이 필요하기 때문에 많은 수의 사용자 요청을 서비스하기 어렵다
  * 쓰레드를 가벼운 프로세스, 즉 경량 프로세스(LWP, light-weight process)라고 부르기도 한다
* 멀티쓰레딩에 장점만 있는 것은 아니어서 멀티쓰레드 프로세스는 여러 쓰레드가 같은 프로세스 내에서 자원을 공유하면서 작업을 하기 때문에 발생할 수 있는 동기화(synchronization), 교착상태(deadlock)와 같은 문제들ㅇ르 고려해서 신중히 프로그래밍해야한다
  * 교착상태란 두 쓰레드가 자원을 점유한 상태에서 서로 상대편이 점유한 자원을 사용하려고 기다리느라 진행이 멈춰있는 상태를 말한다
## 쓰레드의 구현과 실행
* 쓰레드를 구현하는 방법은 Thread클래스를 상속받는 방법과 Runnable인터페이스를 구현하는 방법, 모두 두 가지가 있다
  * 어느 쪽을 선택해도 별 차이는 없지만 Thread클래스를 상속받음녀 다른 클래스를 상속받을 수 없기 때문에, Runnable인터페이스를 구현하는 방법이 일반적이다
* Runnable인터페이스를 구현하는 방법은 재사용성(reusability)이 높고 코드의 일관성(consistency)을 유지할 수 있기 때문에 보다 객체지향적인 방법이라 할 수 있겠다
```java
1. Thread클래스를 상속

class MyThread extends Thread {
    punlic void run() { // 작업내용 } // Thread클래스의 run()을 오버라이딩
}
```
```java
2. Runnable인터페이스를 구현

class MyThread implements Runnable {
    public void run() { // 작업내용 } // Runnable인터페이스의 run()을 구현
}
```
* Runnable인터페이스는 오로지 run()만 정의되어 있는 간단한 인터페이스이다
* Runnable인터페이스를 구현하기 위해서 해야 할 일은 추상메서드인 run()의 몸통{}을 만들어주는 것 뿐이다
```java
public interface Runnable {
    public abstract void run();
}
```
* 쓰레드를 구현한다는 것은, 그저 쓰레드를 통해 작업하고자 하는 내용으로 run()의 몸통{}을 채우는 것일 뿐이다
#### 쓰레드의 실행 - start()
* 쓰레드를 생성했다고 해서 자동으로 실행되는 것은 아니다
  * start()를 호출해야만 쓰레드가 실행된다
```java
t1.start(); // 쓰레드 t1을 실행시킨다
t2.start(); // 쓰레드 t2를 실행시킨다
```
* start()가 호출되었다고 해서 바로 실행되는 것이 아니라, 일단 실행대기 상태에 있다가 자신의 차례가 되어야 실행된다
  * 물론 실행대기 중인 쓰레드가 하나도 없으면 곧바로 실행상태가 된다
    * 쓰레드의 실행순서롤 OS의 스케쥴러가 작성한 스케쥴에 의해 결정된다
* 한 번 실행이 종료된 쓰레드는 다시 실행할 수 없다
  * 하나의 쓰레드에 대해 start()가 한 번만 호출될 수 있다는 뜻이다
* 만일 쓰레드의 작업을 한 번 더 수행해야 한다면 새로운 쓰레드를 생성한 다음에 start()를 호출해야 한다
  * 하나의 쓰레드에 대해 start()를 두 번 이상 호출하면 실행시에 IllegalThrfeadStateException이 발생한다
```java
ThreadEx1_1 t1 = new ThreadEx1_1();
t1.start();
t1.start();
```
->
```java
ThreadEx1_1 t1 = new ThreadEx1_1();
t1.start();
t1 = new ThreadEx1_1(); // 다시 생성
t1.start(); // OK
```
## start()와 run()
* main메서드에서 run()을 호출하는 것은 생성된 쓰레드를 실행시키는 것이 아니라 단순히 클래스에 선언된 메서드를 호출하는 것일 뿐이다
* 반면에 start()는 새로운 쓰레드가 작업을 실행하는데 필요한 호출스택(call stack)을 생성한 다음에 run()을 호출해서 생성된 호출스택이 run()이 첫 번째로 올라가게 한다
* 모든 쓰레드는 독립적인 작업을 수행하기 위해 자신만의 호출스택을 필요로 하기 때문에, 새로운 쓰레드를 생성하고 실행시킬 때마다 새로운 호출스택이 생성되고 쓰레드가 종료되면 작업에 사용된 호출스택은 소멸된다 <br>
<img width="505" alt="image" src="https://github.com/nohheeyeon/TIL/assets/130336617/13d2ad34-d653-44be-9a0e-01e76eaa0340"> <br>
* [새로운 쓰레드를 생성하고 start()를 호출한 후 호출스택의 변화]
1. main메서드에서 쓰레드의 start()를 호출한다
2. start()는 새로운 쓰레드를 생성하고, 쓰레드가 작업하는데 사용될 호출스택을 생성한다
3. 새로 생성된 호출스택에 run()이 호출되어, 쓰레드가 독립된 공간에서 작업을 수행한다
4. 이제는 호출스택이 2개이므로 스케줄러가 정한 순서에 의해서 번갈아 가면서 실행된다

* 호출스택에서는 가장 위에 있는 메서드가 현재 실행중인 메서드이고 나머지 메서드들은 대기상태에 있다는 것을 기억하고 있을 것이다
  * 그러나 쓰레드가 둘 이상일 때는 호출스택의 최상위에 있는 메서드일지라도 대기상태에 있을 수 있다
* 스케줄러는 실행대기 중인 쓰레드들의 우선순위를 고려하여 실행순서와 실행시간을 결정하고, 각 쓰레드들은 작성된 스케줄에 따라 자신의 순서가 되면 지정된 시간동안 작업을 수행한다
  * 이 때 주어진 시간동안 작업을 마치지 못한 쓰레드는 다시 자신의 차례가 돌아올 때 까지 대기상태로 있게되며, 작업을 마친 쓰레드, 즉 run()의 수행이 종료된 쓰레드는 호출스택이 모두 비워지면서 이 쓰레드가 사용하던 호출스택을 사라진다
    * 이는 마치 자바프로그램을 실행하면 호출스택이 생성되고 main메서드가 처음으로 호출되고, main메서드가 종료되면 호출스택이 비워지면서 프로그램도 종료되는 것과 같다
#### main쓰레드
* main메서드의 작업을 수행하는 것도 쓰레드이며, 이를 main쓰레드라고 한다
  * 프로그램을 실행하면 기본적으로 하나의 쓰레드를 생성하고, 그 쓰레드가 main메서드를 호출해서 작업이 수행되도록 하는 것이다
* main메서드가 수행을 마쳤다하더라도 다른 쓰레드가 아직 작업을 마치지 않은 상태라면 프로그램이 종료되지 않는다
```java
실행 중인 사용자 쓰레드가 하나도 없을 때 프로그램은 종료된다.
```
* 쓰레드는 '사용자 쓰레드(user thread'와 '데몬 쓰레드(daemon thread)', 두 종류가 있다
  * 사용자 쓰레드(user thread)는 'non-daemon thread'라고도 한다
## 싱글쓰레드와 멀티쓰레드
* 두 개의 작업을 하나의 쓰레드(th1)로 처리하는 경우와 두 개의 쓰레드(th1, th2)로 처리하는 경우를 가정!
* 하나의 쓰레드로 두 작업을 처리하는 경우는 한 작업을 마친 후에 다른 작업을 시작하지만, 두 개의 쓰레드로 작업을 하는 경우에는 짧은 시간동안 2개의 쓰레드(th1, th2)가 번갈아 가면서 작업을 수행해서 동시에 두 작업이 처리되는 것과 같이 느끼게 한다 <br>
<img width="221" alt="image" src="https://github.com/nohheeyeon/TIL/assets/130336617/a12c95c1-452f-4ca3-9f02-b99dee0e5c03"> <br>
* (a) 하나의 쓰레드로 두 개의 작업을 수행하는 경우
* (b) 두 개의 쓰레드로 두 개의 작업을 수행하는 경우

* 하나의 쓰레드로 두 개의 작업을 수행한 시간과 두개의 쓰레드로 두 개의 작업을 수행한 시간은 거의 같다
  * 오히려 두 개의 쓰레드로 작업한 시간이 싱글쓰레드로 작업한 시간보다 더 걸리게 되는데, 그 이유는  쓰레드간의 작업전환(context switching)에 시간이 걸리기 때문이다
* 작업 전환을 할 때는 현재 진행 중인 작업의 상태, 예를 들면 다음에 실행해야할 위치(PC, 프로그램 카운터) 등의 정보를 저장하고 읽어 오는 시간이 소요된다
  * 쓰레드의 스위칭에 비해 프로세스의 스위칭이 더 많은 정보를 저장해야하므로 더 많은 시간이 소요된다
    * 프로세스 또는 쓰레드 간의 작업 전환을 '컨텍스트 스위칭(context switching)'이라고 한다
* 싱글 코어에서 단순히 CPU만을 사용하는 계산작업이라면 오히려 멀티쓰레드보다 싱글쓰레드로 프로그래밍하는 것이 더 효율적이다
## 쓰레드의 우선순위
* 쓰레드는 우선순위(priority)라는 속성(멤버변수)을 가지고 있는데, 이 우선순위이 값에 따라 쓰레드가 얻는 실행시간이 달라진다
  * 쓰레드가 수행하는 작업의 중요도에 따라 쓰레드의 우선순위를 서로 다르게 지정하여 특정 쓰레드가 더 많은 작업시간을 갖도록 할 수 있다
* 예를 들어 파일전송기능이 있는 메신저의 경우, 파일다운로드를 처리하는 쓰레드보다 채팅내용을 전송하는 쓰레드의 우선순위가 더 높아야 사용자가 채팅하는데 불편함이 없을 것이다
  * 대신 파일다운로드 작업에 걸리는 시간은 더 길어질 것이다
* 이 처럼 시각적인 부분이나 사용자에게 빠르게 반응해야하는 작업을 하는 쓰레드의 우선 순위는 다른 작업을 수행하는 쓰레드에 비해 높아야 한다
#### 쓰레드의 우선순위 정하기
```java
void setPriority(int newPriority) // 쓰레드의 우선순위를 지정한 값으로 변경한다
int getPriority() // 쓰레드의 우선순위를 반환한다

public static final int MAX_PRIORITY = 10 // 최대우선순위
public static final int MIN_PRIORITY = 1 // 최소우선순위
public static final int NORM_PRIORITY = 5 // 보통우선순위
```
* 쓰레드가 가질 수 있는 우선순위의 범위는 1~10이며 숫자가 높을수록 우선순위가 높다
* 한 가지 더 알아두어야 할 것은 쓰레드의 우선순위는 쓰레드를 생성한 쓰레드로부터 상속받는다는 것이다
  * main메서드를 수행하는 쓰레드는 우선순위가 5이므로 main메서드 내에서 생성하는 쓰레드의 우선순위는 자동적으로 5가 된다
## 쓰레드 그룹(thread group)
* 쓰레드 그룹은 서로 관련된 쓰레드를 그룹으로 다루기 위한 것으로, 폴더를 생성해서 관련된 파일들을 함께 넣어서 관리하는 것처럼 쓰레드 그룹을 생성해서 쓰레드를 그룹으로 묶어서 관리할 수 있다
* 폴더 안에 폴더를 생성할 수 있듯이 쓰레드 그룹에 다른 쓰레드 그룹을 포함 시킬 수 있다
  * 쓰레드 그룹은 보안상의 이유로 도입된 개념으로, 자신이 속한 쓰레드 그룹이나 하위 쓰레드 그룹은 벼경할 수 있지만 다른 쓰레드 그룹의 쓰레드를 변경할 수는 없다
* ThreadGroup을 사용해서 생성할 수 있다

| 생성자 / 메서드                                   | 설명                                                                                                                |
| -------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------- |
| `ThreadGroup(String name)`                         | 지정한 이름으로 새로운 스레드 그룹을 생성합니다.                                                                 |
| `ThreadGroup(ThreadGroup parent, String name)`     | 지정한 부모 스레드 그룹 아래에 이름을 가진 스레드 그룹을 생성합니다.                                            |
| `int activeCount()`                                | 현재 활성화된 스레드 그룹 내의 스레드의 추정 카운트를 반환합니다.                                            |
| `int activeGroupCount()`                           | 현재 활성화된 스레드 그룹 내의 스레드 그룹의 추정 카운트를 반환합니다.                                       |
| `void checkAccess()`                               | 현재 스레드가 스레드 그룹에 대한 액세스 권한을 가지지 않으면 SecurityException을 발생시킵니다.               |
| `void destroy()`                                   | 스레드 그룹을 파괴합니다. 이 메서드는 해당 스레드 그룹과 그 하위 스레드 그룹, 스레드를 모두 중단시킵니다.    |
| `ThreadGroup getParent()`                          | 현재 스레드 그룹의 부모 스레드 그룹을 반환합니다.                                                               |
| `boolean parentOf(ThreadGroup g)`                   | 현재 스레드 그룹이 지정한 스레드 그룹의 상위 스레드 그룹인지 확인합니다.                                      |
| `void list()`                                      | 현재 스레드 그룹 및 해당 스레드 그룹 내의 모든 스레드 및 하위 스레드 그룹을 표준 출력에 출력합니다.            |
| `void interrupt()`                                 | 스레드 그룹 내의 모든 스레드에 인터럽트 신호를 보냅니다.                                                     |
| `Thread[] activeGroupCount(Thread[] arr)`           | 활성화된 스레드 그룹 내의 모든 스레드를 배열로 반환합니다.                                                     |
| `Thread[] activeGroupCount(Thread[] arr, boolean recurse)` | 활성화된 스레드 그룹 내의 모든 스레드를 배열로 반환합니다. `recurse`를 true로 설정하면 하위 스레드 그룹도 포함됩니다. |
| `int getMaxPriority()`                             | 현재 스레드 그룹 내의 최대 스레드 우선순위를 반환합니다.                                                       |
| `void setMaxPriority(int pri)`                     | 현재 스레드 그룹 내의 최대 스레드 우선순위를 설정합니다.                                                       |
| `void setDaemon(boolean daemon)`                   | 현재 스레드 그룹을 데몬 스레드 그룹으로 설정하거나 일반 스레드 그룹으로 설정합니다.                          |
| `boolean isDaemon()`                               | 현재 스레드 그룹이 데몬 스레드 그룹인지 확인합니다.                                                           |
| `void resume()`                                    | 스레드 그룹 내의 모든 스레드의 작업을 재개합니다.                                                             |
| `void suspend()`                                   | 스레드 그룹 내의 모든 스레드의 작업을 일시 중지합니다.                                                       |

## 데몬 쓰레드(daemon thread)
* 데몬 쓰레드는 다른 일반 쓰레드(데몬 쓰레드가 아닌 쓰레드)의 작업을 돕는 보조적인 역할을 수행하는 쓰레드이다
  * 일반 쓰레드가 모두 종료되면 데몬 쓰레드는 강제적으로 자동 종료되는데, 그 이유는 데몬쓰레드는 일반 쓰레드의 보조역할을 수행하므로 일반 쓰레드가 모두 종료되고 나면 데몬 쓰레드의 존재의 의미가 없기 때문이다
    * 이 점을 제외하고는 데몬 쓰레드와 일반 쓰레드는 다르지 않다
      * 데몬 쓰레드의 예로는 가비지 컬렉터, 워드프로세서의 자동저장, 화면자동갱신 등이 있다

* 데몬 쓰레드는 무한루프와 조건문을 이용해서 실행 후 대기하고 있다가 특정 조건이 만족되면 작업을 수행하고 다시 대기하도록 작성한다
* 데몬 쓰레드는 일반 쓰레드의 작성방법과 실행방법이 같으며 다만 쓰레드를 생성한 다음 실행하기 전에 setDaemon(true)를 호출하기만 하면 된다
  * 데몬 쓰레드가 생성한 쓰레드는 자동적으로 데몬 쓰레드가 됨!
```java
boolean isDaemon() : 쓰레드가 데몬쓰레드인지 확인한다, 데몬 쓰레드이면 true를 반환한다

void setDaemon(boolean on) : 쓰레드를 데몬 쓰레드로 또는 사용자 쓰레드로 변경한다, 매개변수 on의 값을 true로 지정하면 데몬 쓰레드가 된다 
```

### 쓰레드의 실행 제어

- **start() 메서드**: `start()` 메서드를 호출하여 쓰레드를 실행시킵니다
- **join() 메서드**: `join()` 메서드를 사용하여 다른 쓰레드가 해당 쓰레드의 실행이 끝날 때까지 기다릴 수 있습니다
- **sleep() 메서드**: `sleep()` 메서드를 사용하여 일정 시간 동안 쓰레드를 일시 중지할 수 있습니다
- **interrupt() 메서드**: `interrupt()` 메서드를 사용하여 쓰레드를 인터럽트하고 종료시킬 수 있습니다

```java
// Thread 클래스를 상속받아서 쓰레드 생성
class MyThread extends Thread {
    public void run() {
        for (int i = 0; i < 5; i++) {
            System.out.println("Thread: " + i);
            try {
                Thread.sleep(1000); // 1초 대기
            } catch (InterruptedException e) {
                System.out.println("Thread interrupted.");
            }
        }
    }
}

public class Main {
    public static void main(String[] args) {
        MyThread thread = new MyThread();
        thread.start(); // 쓰레드 시작
    }
}
```

### 쓰레드의 동기화

* 쓰레드 간의 동기화를 위해 `synchronized`, `wait()`, `notify()`, `Lock`, `Condition`, `volatile` 등의 메커니즘을 사용합니다

#### synchronized를 이용한 동기화

* `synchronized` 키워드를 사용하여 메서드나 블록을 동기화하면 한 번에 하나의 쓰레드만 해당 코드 블록에 접근할 수 있습니다

```java
public synchronized void synchronizedMethod() {
    // 동기화된 메서드
}
```

#### wait()과 notify()

* `wait()` 메서드는 쓰레드를 일시 정지시키고, `notify()` 메서드는 다시 실행을 재개합니다
  * 이러한 메서드를 사용하여 쓰레드 간의 협력이 가능합니다

```java
// Producer-Consumer 문제 해결을 위한 예제
public synchronized void produce() throws InterruptedException {
    while (isFull()) {
        wait(); // 버퍼가 가득 차 있으면 대기
    }
    // 데이터를 생산하고 버퍼에 추가
    notify(); // 소비자 스레드에게 알림
}

public synchronized void consume() throws InterruptedException {
    while (isEmpty()) {
        wait(); // 버퍼가 비어있으면 대기
    }
    // 데이터를 소비하고 버퍼에서 제거
    notify(); // 생산자 스레드에게 알림
}
```

#### Lock과 Condition을 이용한 동기화

* `Lock` 인터페이스와 `Condition` 클래스를 사용하여 더 세밀한 쓰레드 동기화를 제어할 수 있습니다

```java
Lock lock = new ReentrantLock();
Condition condition = lock.newCondition();

lock.lock();
try {
    while (isFull()) {
        condition.await(); // 버퍼가 가득 차 있으면 대기
    }
    // 데이터를 생산하고 버퍼에 추가
    condition.signal(); // 소비자 스레드에게 알림
} finally {
    lock.unlock();
}
```

#### volatile

* `volatile` 키워드를 사용하여 변수를 메모리에 저장하고 갱신할 때 캐시를 사용하지 않도록 할 수 있습니다

```java
private volatile boolean flag = true;

public void stopThread() {
    flag = false;
}
```

### fork & join 프레임워크

* `ForkJoinPool`, `ForkJoinTask`, `RecursiveTask` 등을 사용하여 병렬 프로그래밍을 구현할 수 있습니다
```java
import java.util.concurrent.RecursiveTask;
import java.util.concurrent.ForkJoinPool;

class MyTask extends RecursiveTask<Integer> {
    private final int start;
    private final int end;

    public MyTask(int start, int end) {
        this.start = start;
        this.end = end;
    }

    @Override
    protected Integer compute() {
        if (end - start <= 1) {
            return start + end;
        } else {
            int mid = (start + end) / 2;
            MyTask leftTask = new MyTask(start, mid);
            MyTask rightTask = new MyTask(mid + 1, end);
            leftTask.fork();
            int rightResult = rightTask.compute();
            int leftResult = leftTask.join();
            return leftResult + rightResult;
        }
    }
}

public class Main {
    public static void main(String[] args) {
        ForkJoinPool pool = ForkJoinPool.commonPool();
        MyTask task = new MyTask(1, 1000);
        int result = pool.invoke(task);
        System.out.println("Result: " + result);
    }
}
```
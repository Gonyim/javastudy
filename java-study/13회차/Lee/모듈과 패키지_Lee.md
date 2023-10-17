# 6. 패키지

## 패키지의 개념과 필요성
자바에서 FileIO, Graphic, UI 디렉토리를 패키지(Package)라고 부른다.  
자바에서 패키지란 서로 관련 있는 클래스나 인터페이스의 컴파일된 클래스 파일들을 한 곳에 묶어 놓은 것이다.  
자바 JDK는 개발자들에게 많은 클래스들을 패키지 형태로 제공하는데, JDK 9부터는 패키지들을 모듈(module)이라는 단위로 묶어, 100개에 가까운 모듈을 제공한다. 모듈은 JDK 설치 디렉토리 밑의 jmods 디렉토리에 .jmod 확장자를 가진 압축 파일 형태로 제공된다. 모듈 중 가장 기본이 되면서 응용프로그램에서 많이 사용되는 클래스들을 담고 있는 것이 java.base 모듈이다.
```
📦Project
 ┣ 📂FileIO
 ┃ ┣ 📜Tools.class      // Project/FileIO/Tools.class
 ┃ ┗ 📜Webfile.class
 ┣ 📂Graphic
 ┃ ┣ 📜Line.class
 ┃ ┗ 📜Shape.class
 ┗ 📂UI
   ┣ 📜GUI.class
   ┣ 📜Main.class
   ┗ 📜Tools.class      // Project/UI/Tools.class
 ```
A, B, C의 개발자가 IO부분, Graphic부분, UI부분을 각각 개발할 때 A와 C가 동일한 이름의 Tools라는 클래스를 작성하는 경우, 3명이 작성한 클래스 파일을 모두 하나의 디렉토리에 합치게 되면 Tools.class 파일이 중복되는 문제가 발생한다. 개발자마다 자신의 디렉토리에 저장한다면, Tools.class 파일의 경로명이 서로 다르기 때문에 다른 파일로 인식된다.

## import와 클래스 경로
1. import 문은 반드시 소스 코드의 앞부분에 작성되어야 한다.
2. 한 패키지에 있는 여러 클래스를 import하고자 하는 경우, *을 사용하여 한 번에 선언할 수 있다.
```java
import java.util.*;
public class ImportClassEx {
    ......
}
```

## 패키지 만들기
자바 소스 파일(.java)이 컴파일되어 생기는 클래스 파일(.class)은 반드시 패키지에 소속되어야 한다. 클래스가 소속될 패키지 명은 package 키워드를 이용하여 소스 파일의 첫 줄에 선언한다.
```java
package 패키지명;
```
```java
package UI;             // Tools 클래스를 컴파일하여 UI 패키지에 저장할 것을 지시

public class Tools {    // 이 클래스의 경로명은 UI.Tools가 된다.
    ......
}
```
다른 패키지에 있는 클래스에서 위에 있는 Tools 클래스를 사용하고자 한다면, 다음 import문이 필요하다.
```java
package Graphic;    // Line 클래스를 Graphic 패키지에 저장

import UI.Tools;    // Tools 클래스의 경로명 알림

public class Line {
    public void draw() {
        Tools t = new Tools();
    }
}
```
***

### 디폴트 패키지(default package)
package 선언문을 사용하지 않고 자바 클래스나 인터페이스를 작성하면, 자바 컴파일러는 클래스나 인터페이스를 디폴트 패키지에 소속시킨다. 디폴트 패키지는 현재 디렉토리이다.

### 패키지의 특징
1. 패키지 계층 구조
   - 상속 관계에 있는 클래스나 인터페이스의 경우, 자식 클래스 파일을 부모 클래스 파일이 저장된 패키지의 서브 디렉토리에 패키지를 만들어 저장하여 **계층화시키면 더욱 관리하기가 쉽다.**
2. 패키지별 접근 제한
   - default 접근 지정으로 선언된 클래스나 멤버는 동일 패키지 내의 클래스들이 자유롭게 접근하도록 허용한다. 패키지에 포함된 클래스들끼리는 자유롭게 접근하게 하고, 다른 패키지의 클래스들은 접근을 막음으로써 패키지를 **접근 권한의 범위**로도 이용할 수 있다.
3. 동일한 이름의 클래스를 다른 패키지에 작성 가능
   - 같은 패키지 내에서는 동일한 이름을 가진 클래스나 인터페이스가 존재할 수 없다. 그러나 다른 패키지에서는 가능하다.
4. 소프트웨어의 높은 재사용성
   - 클래스와 인터페이스를 잘 분류하여 패키지로 관리하면, 나중에 같거나 유사한 기능을 수행하는 클래스나 인터페이스는 재작성할 필요 없이 프로그램에 포함하여 쉽게 사용할 수 있다. 큰 규모의 프로젝트 수행 시 많은 도움이 되며, 소프트웨어 회사에서 이러한 패키지들은 큰 자산이다.
***

## 모듈 개념
모듈은 패키지들을 담는 컨테이너로 모듈 파일(.jmod)로 저장한다.
```
📦Java 8
 ┣ 📂패키지 A
 ┃ ┣ 📜클래스 파일 1.class
 ┃ ┣ 📜클래스 파일 2.class
 ┃ ┗ 📜클래스 파일 3.class
 ┣ 📂패키지 B
 ┃ ┣ 📜클래스 파일 4.class
 ┃ ┗ 📜클래스 파일 5.class
 ┗ 📂패키지 C
   ┗ 📜클래스 파일 6.class

📦Java 9 이후
 ┣ 📂모듈 M
 ┃ ┣ 📂패키지 A
 ┃ ┃ ┣ 📜클래스 파일 1.class
 ┃ ┃ ┗ 📜클래스 파일 2.class
 ┃ ┣ 📂패키지 B
 ┃ ┃ ┗ 📜클래스 파일 3.class
 ┃ ┗ 📜이미지 등 리소스
 ┗ 📂모듈 N
   ┣ 📂패키지 K
   ┃ ┣ 📜클래스 파일 4.class
   ┃ ┗ 📜클래스 파일 5.class
   ┣ 📂패키지 L
   ┃ ┗ 📜클래스 파일 6.class
   ┗ 📜이미지 등 리소스
```

### 자바 모듈화의 목적
자바 모듈화는 여러 목적이 있지만, 자바 컴포넌트들을 필요에 따라 조립하여 사용하기 위함이다. 필요 없는 모듈이 로드되지 않게 하여, 컴퓨터 시스템에 불필요한 부담을 줄인다. 특히 하드웨어가 열악한 소형 IoT 장치에서도 자바 응용프로그램이 실행되고 성능을 유지하게 한다.
***

## 자바 JDK에서 제공하는 패키지

### 주요 패키지
- java.lang
  - System을 비롯하여 문자열, 함수, 입출력 등과 같이 자바 프로그래밍에 필요한 기본적인 클래스와 인터페이스를 제공한다. 이 패키지의 클래스들은 특별히 import 문을 사용하지 않아도 자동으로 import된다.
- java.util
  - 날짜, 시간, 벡터, 해시맵 등 다양한 유틸리티 클래스와 인터페이스를 제공한다.
- java.io
  - 키보드, 모니터, 프린터, 파일 등에 입출력 하는 클래스와 인터페이스를 제공한다.
- java.awt와 javax.swing
  - 자바 AWT(Abstract Windowing Toolkit)와 swing 패키지로서 GUI 프로그래밍에 필요한 클래스와 인터페이스를 제공한다.

※ 개발자는 항상 자바 API 문서를 열어놓고 작업하는 것이 좋다.
***

## Object 클래스

### Object 생성과 특징
Object는 java.lang 패키지에 속한 클래스이며, 모든 클래스에 강제로 상속된다. Object만이 아무 클래스도 상속받지 않는 유일한 클래스로 계층 구조 상 최상위 클래스이다.  

Object의 주요 메소드
|메소드|설명|
|---|---|
|boolean equals(Object obj)|obj가 가리키는 객체와 현재 객체를 비교하여 같으면 true 리턴|
|Class getClass()|현 객체의 런타임 클래스를 리턴|
|int hashCode()|현 객체에 대한 해시 코드 값 리턴|
|String toString()|현 객체에 대한 문자열 표현을 리턴|
|void notify()|현 객체에 대해 대기하고 있는 하나의 스레드를 깨운다.|
|void notifyAll()|현 객체에 대해 대기하고 있는 모든 스레드를 깨운다.|
|void wait()|다른 스레드가 깨울 때까지 현재 스레드를 대기하게 한다.|
***

### 클래스에 toString() 만들기
개발자는 클래스를 작성할 때, Object의 toString()을 오버라이딩하여 자신만의 문자열을 리턴할 수 있다.
```java
public String toString();   // public으로 선언해야 함에 특히 주의!
```
***

### 객체 비교와 equals() 메소드
기본 타입의 값을 비교하기 위해서는 == 연산자를 사용하지만, 객체 비교를 위해서는 반드시 equals() 메소드를 사용해야 한다.

- == 연산자
  - == 연산자는 두 객체의 내용물이 같은지 비교하는 것이 아니라, 두 레퍼런스가 같은지, 즉 두 레퍼런스가 동일한 객체를 가리키는지 비교한다.
```java
Point a = new Point(2, 3);
Point b = new Point(2, 3);
Point c = a;
if(a == b)  // false
    System.out.println("a==b");
if(a == c)  // true
    System.out.println("a==c");


실행 결과
a==c
```

- boolean equals(Object obj)
  - Object의 equals(Object obj)는 인자로 건네진 객체 obj와 자기 자신을 비교하여 두 객체의 내용이 같은지를 비교하는 메소드이다.
```java
String a = new String("Hello");
String b = new String("Hello");
if(a == b)  // false
    System.out.println("a==b");
if(a.equals(b))  // true
    System.out.println("a와 b는 둘 다 Hello입니다.");


실행 결과
a와 b는 둘 다 Hello입니다.
```
a와 b는 서로 다른 객체를 가리키므로 두 레퍼런스는 서로 다르며, 따라서 a==b의 결과도 false이다. 하지만, a와 b가 가리키는 문자열은 같기 때문에 a.equals(b)의 결과는 true이다.
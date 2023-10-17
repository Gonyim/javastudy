## 자바 API 도큐먼트
API는 라이브러리`library`라고 부르기도 하는데, 프로그램 개발에 자주 사용되는 클래스 및 인터페이스의 모음을 말합니다. 이 API들은 <JDK 설치 경로> \jre\lib\rt.jar 라는 압축 파일에 저장되어 있습니다. `API 도큐먼트`는 쉽게 API를 찾아 이용할 수 있도록 문서화한 것입니다.

> http://docs.oracle.com/javase/8/docs/api/

![API-도큐먼트-1](https://velog.velcdn.com/images/kid/post/0c92fd0e-4440-46cc-bb51-0fa76e26d513/image.png)

API 도큐먼트는 세 개의 프레임으로 나뉘어져 있습니다.

- 좌측 상단 프레임: 패키지 전체 목록
- 좌측 하단 프레임: 패키지에 속하는 클래스와 인터페이스 목록
- 중앙 프레임: 선택한 클래스나 인터페이스에 대한 상세 설명

![API-도큐먼트-2](https://velog.velcdn.com/images/kid/post/775df226-51e0-4f06-ac10-9e97c28d923a/image.png)

중앙 프레임의 내용은 다시 크게 세 부분으로 나뉩니다.

- 상단 부분: 클래스가 포함된 패키지 정보, 상속 정보, 인터페이스 구현 정보 표시
- 중앙 부분: 클래스의 설명과 사용 방법을 간략하게 보여줌
- 하단 부분: 필드, 생성자, 메소드의 목록

<br>

## java.lang과 java.util 패키지
### java.lang 패키지
`java.lang` 패키지는 자바 프로그램의 기본적인 클래스를 담고 있는 패키지입니다. 그렇기 때문에 java.lang 패키지에 있는 클래스와 인터페이스는 import 없이 사용할 수 있습니다.

> 지금까지 사용한 String과 System 클래스도 java.lang 패키지에 포함되어 있습니다.

|클래스||용도|
|---|---|---|
|Object||- 자바 클래스의 최상위 클래스로 사용|
|System||- 표준 입력 장치(키보드)로부터 데이터를 입력받을 때 사용<br>- 표준 출력 장치(모니터)로 출려갛기 위해 사용<br>- 자바 가상 기계를 종료시킬 때 사용<br>- 가비지 컬렉터를 실행 요청할 때 사용|
|Class||- 클래스를 메모리로 로딩할 때 사용|
|String||- 문자열을 저장하고 여러 가지 정보를 얻을 때 사용|
|StringBuffer, StringBuilder||- 문자열을 저장하고 내부 문자열을 조작할 때 사용|
|Math||- 수학 함수를 이용할 때 사용|
|Wrapper|Byte, Short, Character<br>Integer, Float, Double<br>Boolean, Long|- 기본 타입의 데이터를 갖는 객체를 만들 때 사용<br>- 문자열을 기본 타입으로 변환할 때 사용<br>- 입력값 검사에 사용|

<br>

### java.util 패키지

|클래스|용도|
|---|---|
|Arrays|- 배열을 조작(비교, 복사, 정렬, 찾기)할 때 사용|
|Calendar|- 운영체제의 날짜와 시간을 얻을 때 사용|
|Date|- 날짜와 시간 정보를 저장하는 클래스|
|Objects|- 객체 비교, 널(null) 여부 등을 조사할 때 사용|
|StringTokenizer|- 특정 문자로 구분된 문자열을 뽑아낼 때 사용|
|Random|- 난수를 얻을 때 사용|

> java.util 패키지는 컬렉션 클래스들이 대부분을 차지하고 있습니다.

<br>

## Object 클래스
자바의 모든 클래스는 Object 클래스의 자식이거나 자손 클래스입니다. Object 클래스는 필드가 없고, 메소드들로 구성되어 있습니다. 이 메소드들은 모든 클래스에서 사용이 가능합니다.

<br>

### 객체 비교 equals()

```java
public boolean equals(Object obj) { ... }
```

`equals()` 메소드의 매개 타입은 Object인데, 이것은 모든 객체가 매개값으로 대입될 수 있음을 말합니다. equals() 메소드는 비교 연산자인 `==`과 동일한 결과를 리턴합니다. Object의 equals() 메소드는 직접 사용되지 않고 하위 클래스에서 재정의하여 논리적으로 동등 비교할 때 이용됩니다. 논리적으로 동등하다는 것은 같은 객체이건 다른 객체이건 상관없이 객체가 저장하고 있는 데이터가 동일함을 의미합니다.

#### 예제

```java
// Member.java
public class Member {
	public String id;
    
    public Member(String id) {
    	this.id = id;
    }
    
    @Override
    public boolean equals(Object obj) {
    	if (obj instanceof Member) {
        	Member member = (Member) obj;
            if (id.equals(member.id)) {
            	return true;
            }
        }
        return false;
    }
}

// Main.java
public class Main {
	public static void main(String[] args) {
    	Member obj1 = new Member("blue");
        Member obj2 = new Member("blue");
        Member obj3 = new Member("red");
        
        if (obj1.equals(obj2)) {
        	System.out.println("obj1과 obj2는 동등합니다.");
        } else {
        	System.out.println("obj1과 obj2는 동등하지 않습니다.");
        }
        
        if (obj1.equals(obj3)) {
        	System.out.println("obj1과 obj3는 동등합니다.");
        } else {
        	System.out.println("obj1과 obj3는 동등하지 않습니다.");
        }
    }
}
```

<br>

### 객체 해시코드 hashCode()
객체 해시코드란 객체를 식별할 하나의 정수값입니다. Object의 `hashCode()` 메소드는 객체의 메모리 번지를 이용해서 해시코드를 만들어 리턴하기 때문에 객체마다 다른 값을 가지고 있습니다. 컬렉션 프레임워크에서 HashSet, HashMap, Hashtable은 다음과 같은 방법으로 두 객체가 동등한지 비교하기 때문에 논리적 동등 비교 시에는 hashCode() 메소드를 오버라이딩 해야 합니다.

우선 hashCode() 메소드를 실행해서 리턴된 해시코드 값이 같은지를 봅니다. 해시코드 값이 다르면 다른 객체로 판단하고, 값이 같으면 equals() 메소드로 다시 비교합니다. 그렇기 때문에 hashCode() 메소드에서 true가 나와도 equals()의 리턴값이 다르면 다른 객체가 됩니다.

```java
// Key.java
public class Key {
	public int number;
    
    public Key(int number) {
    	this.number = number;
    }
    
    @Override
    public boolean equals(Object obj) {
    	if (obj instanceof Key) {
        	Key compareKey = (Key) obj;
            if (this.number == compareKey.number) {
            	return true;
            }
        }
        return false;
    }
}

// Main.java
public class Main {
	public static void main(String[] args) {
    	// Key 객체를 식별키로 사용해서 String 값을 저장하는 HashMap 객체 생성
        HashMap<Key, String> hashMap = new HashMap<Key, String>();
        
        // 식별키 "new Key(1)"로 "홍길동"을 저장함
        hashMap.put(new Key(1), "홍길동");
        
        // 식별키 "new Key(1)"로 "홍길동"을 읽어옴
        String value = hashMap.get(new Key(1));
        System.out.println(value); // null
    }
}

// "홍길동"을 읽으려면 재정의한 hashCode() 메소드를 Key 클래스에 추가
// Key.java
public class Key {
	public int number;
    
    public Key(int number) {
    	this.number = number;
    }
    
    @Override
    public boolean equals(Object obj) {
    	if (obj instanceof Key) {
        	Key compareKey = (Key) obj;
            if (this.number == compareKey.number) {
            	return true;
            }
        }
        return false;
    }
    
    @Override
    public int hashCode() {
    	return number;
    }
}
```

<br>

### 객체 문자 정보 toString()
Object 클래스의 `toString()` 메소드는 객체의 문자 정보를 리턴합니다. 객체의 문자 정보란 객체를 문자열로 표현한 값을 말합니다. 기본적으로 "클래스명@16진수해시코드"로 구성된 문자 정보를 리턴합니다.

```java
Object obj = new Object();
System.out.println(obj.toString());

// java.lang.Object@de6ced
```

Object 하위 클래스는 toString() 메소드를 재정의하여 간결하고 유익한 정보를 리턴할 수 있습니다.

> java.util 패키지의 Date 클래스는 toString() 메소드를 재정의하여 현재 시스템의 날짜와 시간 정보를 리턴하고, String 클래스는 저장하고 있는 문자열을 리턴합니다.

#### 예제

```java
// SmartPhone.java
public class SmartPhone {
	private String company;
    private String os;
    
    public SmartPhone(String company, String os) {
    	this.company = company;
        this.os = os;
    }
    
    @Override
    public String toString() {
    	return company + ", " + os;
    }
}

// Main.java
public class Main {
	public static void main(String[] args) {
    	SmartPhone myPhone = new SmartPhone("구글", "안드로이드");
        
        String strObj = myPhone.toString();
        System.out.println(strObj);
        System.out.println(myPhone); // myPhone.toString() 자동 호출
    }
}
```

> System.out.println() 메소드의 매개값이 객체일 경우 해당 객체의 toString() 메소드를 호출해서 리턴값을 받고 출력합니다.

<br>

### 객체 복제 clone()
객체 복제는 원본 객체의 필드값과 동일한 값을 가지는 새로운 객체를 생성하는 것입니다. 객체를 복제하는 이유는 원본 객체를 안전하게 보호하기 위해서입니다.

#### 얕은 복제 thin clone
얕은 복제란 단순히 필드값을 복사해서 객체를 복제하는 것입니다. 필드값만 복제하기 때문에 필드가 기본 타입일 경우 값 복사가 일어나고, 필드가 참조 타입일 경우에는 객체의 번지가 복사됩니다. Object의 clone() 메소드는 자신과 동일한 필드값을 가진 얕은 복제된 객체를 리턴합니다.

이 메소드로 객체를 복제하려면 원본 객체는 반드시 `java.lang.Cloneable` 인터페이스를 구현하고 있어야 합니다. 이유는 클래스 설계자가 복제를 허용한다는 의도적인 표시를 하기 위함입니다. 그래서 Cloneable 인터페이스를 구현하지 않으면 clone() 메소드를 호출할 때 `CloneNotSupportedException` 예외가 발생하여 복제가 실패합니다.

#### 예제

```java
// Member.java
public class Member implements Cloneable {
    public String id;
    public String name;
    public String password;
    public int age;
    public boolean adult;

    public Member(String id, String name, String password, int age, boolean adult) {
        this.id = id;
        this.name = name;
        this.password = password;
        this.age = age;
        this.adult = adult;
    }
    
    public Member getMember() {
    	Member cloned = null;
        try {
        	cloned = (Member) clone();
        } catch (CloneNotSupportedException e) { }
        return cloned;
    }
}

// Main.java
public class Main {
	public static void main(String[] args) {
    	// 원본 객체 생성
        Member original = new Member("blue", "홍길동", "12345", 25, true);
        
        // 복제 객체를 얻은 후에 패스워드 변경
        Member cloned = original.getMember();
        cloned.password = "67890";
        
        System.out.println("[복제 객체의 필드값]");
        System.out.println("id: " + cloned.id);
        System.out.println("name: " + cloned.name);
        System.out.println("password: " + cloned.password);
        System.out.println("age: " + cloned.age);
        System.out.println("adult: " + cloned.adult);
        
        System.out.println();
        
        System.out.println("[원본 객체의 필드값]");
        System.out.println("id: " + original.id);
        System.out.println("name: " + original.name);
        System.out.println("password: " + original.password);
        System.out.println("age: " + original.age);
        System.out.println("adult: " + original.adult);
    }
}
```

#### 깊은 복제 deep clone
깊은 복제는 참조하고 있는 객체도 복제합니다. 깊은 복제를 하려면 Object의 clone() 메소드를 재정의해서 참조 객체를 복제하는 코드를 직접 작성해야 합니다.

#### 예제

```java
// Member.java
import java.util.Arrays;

public class Member implements Cloneable {
    public String name;
    public int age;
    public int[] scores;
    public Car car;

    public Member(String name, int age, int[] scores, Car car) {
        this.name = name;
        this.age = age;
        this.scores = scores;
        this.car = car;
    }

    @Override
    protected Object clone() throws CloneNotSupportedException {
        // 먼저 얕은 복사를 해서 name, age를 복제
        Member cloned = (Member) super.clone(); // Object의 clone() 호출
        // scores 깊은 복제
        cloned.scores = Arrays.copyOf(this.scores, this.scores.length);
        // car 깊은 복제
        cloned.car = new Car(this.car.model);
        // 깊은 복제된 Member 객체 리턴
        return cloned;
    }

    public Member getMember() {
        Member cloned = null;
        try {
            cloned = (Member) clone(); // 재정의된 clone() 메소드 호출
        } catch (CloneNotSupportedException e) { }
        return cloned;
    }
}

// Car.java
public class Car {
    public String model;

    public Car(String model) {
        this.model = model;
    }
}

// Main.java
public class Main {
    public static void main(String[] args) {
        // 원본 객체 생성
        Member original = new Member("홍길동", 25, new int[] {90, 90}, new Car("소나타"));

        // 복제 객체를 얻은 후에 참조 객체의 값을 변경
        Member cloned = original.getMember();
        cloned.scores[0] = 100;
        cloned.car.model = "그랜저";

        System.out.println("[복제 객체의 필드값]");
        System.out.println("name: " + cloned.name);
        System.out.println("age: " + cloned.age);
        System.out.print("scores: {");
        for (int i=0; i<cloned.scores.length; i++) {
            System.out.print(cloned.scores[i]);
            System.out.print((i==(cloned.scores.length-1))?"":", ");
        }
        System.out.println("}");
        System.out.println("car: " + cloned.car.model);

        System.out.println();

        System.out.println("[복제 객체의 필드값]");
        System.out.println("name: " + original.name);
        System.out.println("age: " + original.age);
        System.out.print("scores: {");
        for (int i=0; i<original.scores.length; i++) {
            System.out.print(original.scores[i]);
            System.out.print((i==(original.scores.length-1))?"":", ");
        }
        System.out.println("}");
        System.out.println("car: " + original.car.model);
    }
}
```

<br>

### 객체 소멸자 finalize()
참조하지 않는 배열이나 객체는 가비지 컬렉터가 힙 영역에서 자동적으로 소멸시킵니다. 가비지 컬렉터는 객체를 소멸시키기 직전에 마지막으로 객체의 소멸자`fianlize()`를 실행시킵니다. 소멸자는 기본적으로 실행 내용이 없는데 만약 객체가 소멸되기 전에 마지막으로 사용했던 자원(데이터 연결, 파일 등)을 닫고 싶거나, 중요한 데이터를 저장하고 싶다면 Object의 finalize()를 재정의해서 사용할 수 있습니다.

<br>

## Objects 클래스
Object와 유사한 이름을 가진 `java.util.Objects` 클래스는 객체 비교, 해시코드 생성, null 여부, 객체 문자열 리턴 등의 연산을 수행하는 정적 메소드들로 구성된 Object의 유틸리티 클래스입니다.

|리턴 타입|메소드(매개 변수)|설명|
|---|---|---|
|int|compare(T a, T b, Comparator< T > c)|두 객체 a와 b를 Comparator를 사용해서 비교|
|boolean|deepEquals(Object a, Object b)|두 객체의 깊은 비교(배열의 항목까지)|
|boolean|equals(Object a, Object b)|두 객체의 얕은 비교(번지만)|
|int|hash(Object... values|매개값이 저장된 배열의 해시코드 생성|
|int|hashCode(Object o)|객체의 해시코드 생성|
|boolean|isNull(Object obj)|객체가 null인지 조사|
|boolean|nonNull(Object obj)|객체가 null이 아닌지 조사|
|T|requireNonNull(T obj)|객체가 null인 경우 예외 발생|
|T|requireNonNull(T obj,<br>String message)|객체가 null인 경우 예외 발생(주어진 예외 메시지 포함)|
|T|requireNonNull(T obj,<br>Supplier< String > messageSupplier|객체가 null인 경우 예외 발생(람다식이 만든 예외 메시지 포함)|
|String|toString(Object o)|객체의 toString() 리턴값 리턴|
|Stirng|toString(Object o, String nullDefault)|객체의 toString() 리턴값 리턴, 첫 번째 매개값이 null일 경우 두 번째 매개값 리턴|

<br>

### 객체 비교 compare(T a,T b, Comparator< T >c)
`Object.compare(T a,T b, Comparator<T>c)`는 메소드 두 객체를 비교자`Comparator`로 비교해서 int 값을 리턴합니다. `java.util.Comparator<T>`는 제네릭 인터페이스 타입으로 두 객체를 비교하는 compare(T a, T b) 메소드가 정의되어 있습니다. 여기서 T는 비교할 객체 타입을 의미하고 a가 b보다 작으면 음수, 같으면 0, 크면 양수를 리턴하도록 구현 클래스를 만들어야 합니다.

#### 예제

```java
import java.util.Comparator;
import java.util.Objects;

public class Main {
    public static void main(String[] args) {
        Student s1 = new Student(1);
        Student s2 = new Student(1);
        Student s3 = new Student(2);

        int result = Objects.compare(s1, s2, new StudentComparator());
        System.out.println(result);
        result = Objects.compare(s1, s3, new StudentComparator());
        System.out.println(result);
    }

    static class Student {
        int sno;
        Student(int sno) {
            this.sno = sno;
        }
    }

    static class StudentComparator implements Comparator<Student> {
        @Override
        public int compare(Student a, Student b) {
            /*
            if (a.sno < b.sno) return -1;
            else if (a.sno == b.sno) return 0;
            else return 1;
            */
            return Integer.compare(a.sno, b.sno);
        }
    }
}
```

<br>

### 동등 비교 equals()와 deepEquals()
`Objects.equals(Object a, Object b)`는 다음과 같은 결과를 리턴합니다.

|a|b|Objects.equals(a, b)|
|---|---|---|
|not null|not null|a.equals(b)의 리턴값|
|not null|null|false|
|null|not null|false|
|null|null|true|

`Objects.deepEquals(Object a, Object b)` 역시 두 객체의 동등을 비교합니다.

|a|b|Objects.deepEquals(a, b)|
|---|---|---|
|not null (not array)|not null (not array)|a.equals(b)의 리턴값|
|not null (array)|not null (array)|Arrays.deepEquals(a, b)의 리턴값|
|not null|null|false|
|null|not null|false|
|null|null|true|

<br>

### 해시코드 생성 hash(), hashCode()
`Objects.hash(Object... values)` 메소드는 매개값으로 주어진 값들을 이용해서 해시 코드를 생성하는 역할을 하는데, 주어진 매개값들로 배열을 생성하고 `Arrays.hashCode(Object[])`를 호출해서 해시코드를 얻고 이 값을 리턴합니다. 이 메소드는 클래스가 hashCode()를 재정의할 때 리턴값을 생성하기 위해 주로 사용합니다. 클래스가 여러 가지 필드를 가지고 있을 때 이 필드들로부터 해시코드를 생성하게 되면 동일한 필드값을 가지는 객체는 동일한 해시코드를 가집니다.

#### 예제

```java
import java.util.Objects;

public class Main {
    public static void main(String[] args) {
        Student s1 = new Student(1, "홍길동");
        Student s2 = new Student(1, "홍길동");
        System.out.println(s1.hashCode());
        System.out.println(Objects.hashCode(s2));
    }

    static class Student {
        int sno;
        String name;
        Student(int sno, String name) {
            this.sno = sno;
            this.name = name;
        }
        @Override
        public int hashCode() {
            return Objects.hash(sno, name);
        }
    }
}
```

<br>

### 널 여부 조사 isNull(), nonNull(), requireNonNull()
`Objects.isNull(Object obj`는 매개값이 null일 경우 true를 리턴합니다. 반대로 nonNull(Object obj)는 매개값이 not null일 경우 true를 리턴합니다. requireNonNull()는 다음 세 가지로 오버로딩되어 있습니다.

|리턴 타입|메소드(매개 변수)|설명|
|---|---|---|
|T|requireNonNull(T obj)|not null => obj<br>null => NullPointerException|
|T|requireNonNull(T obj,<br>String message)|not null => obj<br>null => NullPointerException(message)|
|T|requireNonNull(T obj,<br>Supplier< String > msgSupplier)|not null => obj<br>null => NullPointerException(msgSupplier.get())|

첫 번째 매개값이 not null이면 첫 번째 매개값을 리턴하고, null이면 모두 NullPointerException 예외를 발생시킵니다. 두 번째 매개값은 NullPointerException의 예외 메시지를 제공합니다.

#### 예제

```java
public class Main {
	public static void main(String[] args) {
    	String str1 = "홍길동";
        String str2 = null;
        
        System.out.println(Objects.requireNonNull(str1));
        
        try {
        	String name = Objects.requireNonNull(str2);
        } catch(Exception e) {
        	System.out.println(e.getMessage());
        }
        
        try {
        	String name = Objects.requireNonNull(str2, "이름이 없습니다.");
        } catch(Exception e) {
        	System.out.println(e.getMessage());
        }
        
        try {
        	String name = Objects.requireNonNull(str2, ()->"이름이 없습니다!");
        } catch(Exception e) {
        	System.out.println(e.getMessage());
        }
    }
}
```

<br>

### 객체 문자 정보 toString()
`Objects.toString()`은 객체의 문자 정보를 리턴하는데, 다음 두 가지로 오버로딩되어 있습니다.

|리턴 타입|메소드(매개 변수)|설명|
|---|---|---|
|String|toString(Object o)|not null => o.toString()<br>null => "null"|
|String|toString(Object o, String nullDefault)|not null => o.toString()<br>null => nullDefault|

첫 번째 매개값이 not null이면 toString()으로 얻은 값을 리턴하고, null이면 "null" 또는 두 번째 매개값인 nullDefault를 리턴합니다.

#### 예제

```java
public class Main {
	public static void main(String[] args) {
    	String str1 = "홍길동";
        String str2 = null;
        
        System.out.println(Objects.toString(str1));
        System.out.println(Objects.toString(str2));
        System.out.println(Objects.toString(str2, "이름이 없습니다."));
    }
}
```

<br>

## System 클래스
자바 프로그램은 JVM 위에서 실행되기 때문에 운영체제의 모든 기능을 자바 코드로 직접 접근하기 어려운데, java.lang 패키지에 속하는 System 클래스를 이용하면 운영체제의 일부 기능`프로그램 종료, 키보드로부터 입력, 모니터로 출력, 메모리 정리, 현재 시간 읽기, 시스템 프로퍼티 읽기, 환경 변수 읽기 등`을 이용할 수 있습니다. System 클래스의 모든 필드와 메소드는 정적`static` 멤버로 구성되어 있습니다.

<br>

### 프로그램 종료 exit()
`exit()` 메소드는 현재 실행하고 있는 프로세스를 강제 종료시키는 역할을 합니다. exit() 메소드는 int 매개값을 지정하도록 되어 있는데, 이 값을 종료 상태값이라고 합니다. 일반적으로 정상 종료일 경우 0으로 지정하고 비정상 종료일 경우 0 이외의 다른 값을 줍니다.

```java
System.exit(0);
```

System.exit()가 실행되면 자바 보안 관리자의 checkExit() 메소드가 자동 호출되는데, 이 메소드를 재정의해서 특정 값이 입력되었을 경우에만 종료시킬 수도 있습니다. 다음 예제는 종료 상태값으로 5가 입력되면 JVM을 종료하도록 보안 관리자를 설정합니다.

```java
System.setSecurityManager(new SecurityManager() {
	@Override
    public void checkExit(int status) {
    	if (status != 5) {
        	throw new SecurityException();
        }
    }
});
```

<br>

### 쓰레기 수집기 실행 gc()
JVM은 메모리가 부족할 때와 CPU가 한가할 때에 가비지 컬렉터를 실행시켜 사용하지 않는 객체를 자동 제거합니다. 이 가비지 컬렉터를 가능한한 빨리 실행해 달라고 요청할 수 있는데 이것이 `System.gc()` 메소드입니다. 이 메소드는 메모리가 열악하지 않은 환경이라면 사용할 일이 거의 없습니다.

<br>

### 현재 시각 읽기 currentTimeMills(), nanoTime()
System 클래스의 `currentTimeMills()` 메소드와 `nanoTime()` 메소드는 컴퓨터의 시계로부터 현재 시간을 읽어서 밀리세컨드(1/1000초) 단위와 나노세컨드(1/10^9) 단위의 long 값을 리턴합니다.

```java
long time = System.currentTimeMills();
long time = System.nanoTime();
```

리턴값은 주로 프로그램의 실행 소요 시간 측정에 사용됩니다.

```java
public class Main {
	public static void main(String[] args) {
    	long time1 = System.nanoTime(); // 시작 시간 읽기
        
        int sum = 0;
        for (int i=1; i<=100000; i++) {
        	sum += i;
        }
        
        long time2 = System.nanoTime(); // 끝 시간 읽기
        
        System.out.println("1~100000까지의 합: " + sum);
        System.out.println("계산에 " + (time2-time1) + " 나노초가 소요되었습니다.);
    }
}
```

<br>

### 시스템 프로퍼티 읽기 getProperty()
시스템 프로퍼티는 JVM이 시작할 때 자동 설정되는 시스템의 속성값을 말합니다. 키`Key`와 값`Value`로 구성되어 있고, 운영체제의 종류 및 자바 프로그램을 실행시킨 사용자 아이디,JVM의 버전, 운영체제에서 사용되는 파일 경로 구분자 등이 여기에 속합니다.

|키|설명|값|
|---|---|---|
|java.version|자바의 버전|1.8.0_20|
|java.home|사용하는 JRE의 파일 경로|< jdk 설치경로 >\jre|
|os.name|Operating system name|Windows 11|
|file.separator|File separator ("/" on UNIX)|\|
|user.name|사용자의 이름|사용자계정|
|user.home|사용자의 홈 디렉토리|C:\Users\사용자계정|
|user.dir|사용자가 현재 작업 중인 디렉토리 경로|다양|

```java
String value = System.getProperty(String key);
String osName = System.getProperty("os.name");
```

<br>

### 환경 변수 읽기 getenv()
환경 변수는 운영체제에서 이름`Name`과 값`Value`으로 관리되는 문자열 정보입니다.

```java
String value = System.getenv(String name);
String javaHome = System.getenv("JAVA_HOME");
```

<br>

## Class 클래스
자바는 클래스와 인터페이스의 메타 데이터를 java.lang 패키지에 소속된 Class 클래스로 관리합니다. 여기서 메타 데이터란 클래스의 이름, 생성자 정보, 필드 정보, 메소드 정보를 말합니다.

<br>

### Class 객체 얻기 getClass(), forName()
Class 객체를 얻기 위해서는 Object 클래스가 가지고 있는 `getClass()` 메소드를 사용하면 됩니다.

```java
Class c = obj.getClass();
```

getClass() 메소드는 해당 클래스로 객체를 생성했을 때만 사용할 수 있는데, 객체를 생성하기 전에 직접 Class 객체를 얻을 수도 있습니다. 이때 `forName()`을 사용합니다. forName() 메소드는 클래스 전체 이름(패키지가 포함된 이름)을 매개값으로 받고 Class 객체를 리턴합니다.

```java
try {
	Class c = Class.forName(String className);
} catch (ClassNotFoundException e) {
}
```

<br>

### 리플렉션 getDeclaredConstructors(), getDeclaredFields(), getDeclaredMethods()
Class 객체를 이용해서 클래스의 생성자, 필드, 메소드 정보를 알아내는 것을 리플렉션`Reflection`이라고 합니다. Class 객체는 리플렉션을 위해 `getDeclaredConstructors()`, `getDeclaredFields()`, `getDeclaredMethods()`를 제공합니다.

```java
Constructor[] constructors = getDeclaredConstructors();
Field[] fields = getDeclaredFields();
Method[] methods = getDeclaredMethods();
```

Constructor, Field, Method는 모두 java.lang.reflect 패키지에 소속되어 있습니다. getDeclaredFields(), getDeclaredMethods()는 클래스에 선언된 멤버만 가져오고 상속된 멤버는 가져오지 않습니다. 상속된 멤버도 얻고 싶다면 `getFields()`, `getMethods()`를 사용합니다. getFields(), getMethods()는 public 멤버만 가져옵니다.

<br>

### 동적 객체 생성 newInstance()
Class 객체를 이용하면 new 연산자를 사용하지 않아도 동적으로 객체를 생성할 수 있습니다. 이 방법은 코드 작성 시에 클래스 이름을 결정할 수 없고, 런타임 시에 클래스 이름이 결정되는 경우에 유용하게 사용됩니다.

```java
try {
	Class c = Class.forName("런타임 시 결정되는 클래스 이름");
    Object obj = c.newInstance();
} catch (ClassNotFoundException e) {
} catch (InstantiationException e) {
} catch (IllegalAccessException e) {
}
```

`newInstance()` 메소드는 기본 생성사를 호출해서 객체를 생성하기 때문에 반드시 클래스에 기본 생성자가 존재해야 합니다. 만약 매개 변수가 있는 생성자를 호출하고 싶다면 리플렉션으로 Constructor 객체를 얻어 newInstance() 메소드를 호출합니다. newInstance() 메소드는 두 가지 예외가 발생할 수 있는데, `InstantiationException` 예외는 해당 클래스가 추상 클래스이거나 인터페이스일 경우 발생하고, `IllegalAccessException` 예외는 클래스나 생성자가 접근 제한자로 인해 접근할 수 없을 경우 발생합니다.

newInstance() 메소드의 리턴 타입은 Object이므로 클래스 타입으로 변환해야만 메소드를 사용할 수 있습니다. 하지만 위의 경우 클래스 타입을 모르는 상태이므로 변환이 불가능합니다. 이 문제를 해결하기 위해서는 인터페이스 사용이 필요합니다.

#### 예제

```java
// Action.java
public interface Action {
    public void execute();
}

// SendAction.java
public class SendAction implements Action {
    @Override
    public void execute() {
        System.out.println("데이터를 보냅니다.");
    }
}

// ReceiveAction.java
public class ReceiveAction implements Action {
    @Override
    public void execute() {
        System.out.println("데이터를 받습니다.");
    }
}

// Main.java
public class Main {
    public static void main(String[] args) {
        try {
            Class c = Class.forName("SendAction");
            // Class c = Class.forName("ReceiveAction");
            Action action = (Action) c.newInstance();
            action.execute();
        } catch (ClassNotFoundException e) {
            e.printStackTrace();
        } catch (InstantiationException e) {
            e.printStackTrace();
        } catch (IllegalAccessException e) {
            e.printStackTrace();
        }
    }
}
```

<br>

## 레퍼런스
- 이것이 자바다: 신용권의 Java 프로그래밍 정복
- Java에서 String이 깊은 복사처럼 동작하는 이유: https://velog.io/@sjsrkdgks/Java%EC%97%90%EC%84%9C-String%EC%9D%B4-%EA%B9%8A%EC%9D%80-%EB%B3%B5%EC%82%AC%EC%B2%98%EB%9F%BC-%EB%8F%99%EC%9E%91%ED%95%98%EB%8A%94-%EC%9D%B4%EC%9C%A0
- Java finalize() 은퇴식: https://jaeyeong951.medium.com/finalize-%EC%9D%80%ED%87%B4%EC%8B%9D-4a52fb855910
## 왜 제네릭을 사용해야 하는가?
컬렉션, 람다식, 스트림, NIO에서 널리 사용되는 제네릭`Generic` 타입은 Java 5부터 새로 추가되었습니다. 제네릭 타입을 이용함으로써 잘못된 타입이 사용될 수 있는 문제를 컴파일 과정에서 제거할 수 있게 되었습니다. 제네릭은 클래스와 인터페이스, 그리고 메소드를 정의할 때 타입을 파라미터로 사용할 수 있도록 합니다. 타입 파라미터는 코드 작성 시 구체적인 타입으로 대체되어 다양한 코드를 생성하도록 도와줍니다.

#### 컴파일 시 강한 타입 체크를 할 수 있다.
자바 컴파일러는 제네릭 코드에 대해 강한 타입 체크를 합니다. 그래서 실행 시 타입 에러가 나는 것을 방지할 수 있습니다.

#### 타입 변환을 제거한다.
비제네릭 코드는 불필요한 타입 변환을 하기 때문에 프로그램 성능에 악영향을 미칠 수 있습니다.

```java
List list = new ArrayList();
list.add("hello");
String str = (String) list.get(0); // 타입 변환을 해야함
```

```java
List<String> list = new ArrayList<String>();
list.add("hello");
String str = list.get(0); // 타입 변환을 하지 않음
```

<br>

## 제네릭 타입 class< T >, interface< T >
제네릭 타입은 타입을 파라미터로 가지는 클래스와 인터페이스를 의미합니다.

```java
public class 클래스명<T> { ... }
public interface 인터페이스명<T> { ... }
```

타입 파라미터는 변수명과 동일한 규칙으로 작성할 수 있는데, 일반적으로 대문자 알파벳 한 글자로 표현합니다. 제네릭 타입을 실제 코드에서 사용하려면 타입 파라미터에 구체적인 타입을 지정해야 합니다.

```java
public class Box {
	private Object object;
    public void set(Object object) {
    	this.object = object;
    }
    public Object get() {
    	return object;
    }
}
```

```java
Box box = new Box();
box.set("hello"); // 자동 타입 변환
String str = (String) box.get(); // 강제 타입 변환
```

위와 같이 Object 타입을 사용하면 모든 종류의 자바 객체를 저장할 수 있지만, 타입 변환이 빈번하게 발생하게 됩니다.

```java
public class Box<T> {
	private T t;
    public T get() {
    	return t;
    }
    public void set(T t) {
    	this.t = t;
    }
}
```

```java
Box<String> box = new Box<String>();
```

타입 파라미터 T를 사용해서 Object 타입을 대체해주면 T는 Box 클래스로 객체를 생성할 때 구체적인 타입으로 변경됩니다.

```java
// 타입 변환이 일어나지 않음
Box<String> box = new Box<String>();
box.set("hello");
String str = box.get();
```

<br>

## 멀티 타입 파라미터 class<K, V ...>, interface<K, V ...>
제네릭 타입은 두 개 이상의 멀티 타입 파라미터를 사용할 수 있습니다. 이 경우 각 타입 파라미터를 콤마로 구분합니다.

```java
public class Product<T, M> {
	private T kind;
    private M model;
    
    public T getKind() {
    	return this.kind;
   	}
    public M getModel() {
    	return this.model;
    }
    
    public void setKind(T kind) {
    	this.kind = kind;
    }
    public void setModel(M model) {
    	this.model = model;
    }
}
```

```java
public class Main {
	public static void main(String[] args) {
    	Product<Tv, String> product1 = new Product<Tv, String>();
        product1.setKind(new Tv());
        product1.setModel("스마트Tv");
        Tv tv = product1.getKind();
        String tvModel = product1.getModel();
        
        Product<Car, String> product2 = new Product<Car, String>();
        product2.setKind(new Car());
        product2.setModel("디젤");
        Car car = product2.getKind();
        String carModel = product2.getModel();
    }
}
```

위와 같이 제네릭 타입 변수 선언과 객체 생성을 동시에 할 때 타입 파라미터 자리에 타입을 지정하는 코드가 중복되어 다소 복잡해질 수 있습니다. 그래서 자바 7부터는 다이아몬드 연산자를 사용해서 다음과 같이 간단하게 작성 가능합니다.

```java
Product<Tv, String> product = new Product<>();
```

<br>

## 제네릭 메소드 <T, R> R method(T t)
제네릭 메소드는 매개 타입과 리턴 타입으로 타입 파라미터를 갖는 메소드를 의미합니다. 제네릭 메소드를 선언하는 방법은 리턴 타입 앞에 <> 기호를 추가하고 타입 파라미터를 기술한 다음, 리턴 타입과 매개 타입으로 타입 파라미터를 사용합니다.

```java
public <타입파라미터, ...> 리턴타입 메소드명(매개변수, ...) { ... }

pubic <T> Box<T> boxing(T t) { ... }
```

제네릭 메소드는 두 가지 방식으로 호출할 수 있습니다. 코드에서 타입 파라미터의 구체적인 타입을 명시적으로 지정해도 되고, 컴파일러가 매개값의 타입을 보고 구체적인 타입을 추정하도록 할 수도 있습니다.

```java
리턴타입 변수 = <구체적타입> 메소드명(매개값); // 명시적으로 구체적 타입을 지정
리턴타입 변수 = 메소드명(매개값); // 매개값을 보고 구체적 타입을 추정

Box<Integer> box = <Integer>boxing(100); // 타입 파라미터를 명시적 Integer로 지정
Box<Integer> box = boxing(100); // 타입 파라미터를 Integer로 추정
```

<br>

## 제한된 타입 파라미터 <T extends 최상위타입>
타입 파라미터에 지정되는 구체적인 타입을 제한할 필요가 종종 있습니다. 예를 들어 숫자를 연산하는 제네릭 메소드는 매개값으로 Number 타입 또는 하위 클래스 타입의 인스턴스만 가져야 합니다. 이것이 제한된 타입 파라미터`bounded type parameter`가 필요한 이유입니다. 제한된 타입 파라미터를 선언하려면 타입 파라미터 뒤에 extends 키워드를 붙이고 상위 타입을 명시하면 됩니다. 상위 타입은 클래스뿐만 아니라 인터페이스도 가능하고, 인터페이스라고 해서 implements를 사용하지 않습니다.

```java
public <T extends 상위타입> 리턴타입 메소드(매개변수, ...) { ... }
```

타입 파라미터에 지정되는 구체적인 타입은 상위 타입이거나 하위 또는 구현 클래스만 가능합니다. 주의할 점은 메소드의 중괄호 안에서 타입 파라미터 변수로 사용 가능한 것은 상위 타입의 멤버(필드, 메소드)로 제한됩니다. 하위 타입에만 있는 필드와 메소드는 사용할 수 없습니다.

```java
public <T extends Number> int compare(T t1, T t2) {
	double v1 = t1.doubleValue(); // Number의 doubleValue() 메소드 사용
    double v2 = t2.doubleValue(); // Number의 doubleValue() 메소드 사용
    return Double.compare(v1, v2);
}
```

`doubleValue()` 메소드는 Number 클래스에 정의되어 있는 메소드로 숫자를 double 타입으로 변환합니다. `Double.compare()` 메소드는 첫 번째 매개값이 작으면 -1을, 같으면 0을, 크면 1을 리턴합니다.

<br>

## 와일드카드 타입 <?>, <? extends ...>, <? super ...>
코드에서 `?`를 일반적으로 와일드카드라고 부릅니다. 제네릭 타입을 매개값이나 리턴 타입으로 사용할 때 구체적인 타입 대신에 와일드카드를 다음과 같이 세 가지 형태로 사용할 수 있습니다.

- 제네릭타입<?>: Unbounded Wildcards(제한 없음)
	- 타입 파라미터를 대치하는 구체적인 타입으로 모든 클래스나 인터페이스 타입이 올 수 있습니다.

- 제네릭타입<? extends 상위타입>: Upper Bounded Wildcards(상위 클래스 제한)
	- 타입 파라미터를 대치하는 구체적인 타입으로 상위 타입이나 하위 타입만 올 수 있습니다.

- 제네릭타입<? super 상위타입>: Lower Bounded Wildcards(하위 클래스 제한)
	- 타입 파라미터를 대치하는 구체적인 타입으로 하위 타입이나 상위 타입이 올 수 있습니다.

#### 예제

```java
// Main.java
import java.util.Arrays;

public class Main {
    public static void main(String[] args) {
        Course<Person> personCourse = new Course<Person>("일반인과정", 5);
        personCourse.add(new Person("일반인"));
        personCourse.add(new Worker("직장인"));
        personCourse.add(new Student("학생"));
        personCourse.add(new HighStudent("고등학생"));

        Course<Worker> workerCourse = new Course<>("직장인 과정", 5);
        workerCourse.add(new Worker("직장인"));

        Course<Student> studentCourse = new Course<>("학생 과정", 5);
        studentCourse.add(new Student("학생"));
        studentCourse.add(new HighStudent("고등학생"));

        Course<HighStudent> highStudentCourse = new Course<>("고등학생 과정", 5);
        highStudentCourse.add(new HighStudent("고등학생"));

        registerCourse(personCourse);
        registerCourse(workerCourse);
        registerCourse(studentCourse);
        registerCourse(highStudentCourse);
        System.out.println();

        // registerCourseStudent(personCourse);
        // registerCourseStudent(workerCourse);
        registerCourseStudent(studentCourse);
        registerCourseStudent(highStudentCourse);
        System.out.println();

        registerCourseWorker(personCourse);
        registerCourseWorker(workerCourse);
        // registerCourseWorker(studentCourse);
        // registerCourseWorker(highStudentCourse);
    }

    public static void registerCourse(Course<?> course) {
        System.out.println(course.getName() + " 수강생: " + Arrays.toString(course.getStudents()));
    }

    public static void registerCourseStudent(Course<? extends Student> course) {
        System.out.println(course.getName() + " 수강생: " + Arrays.toString(course.getStudents()));
    }

    public static void registerCourseWorker(Course<? super Worker> course) {
        System.out.println(course.getName() + " 수강생: " + Arrays.toString(course.getStudents()));
    }
}

// Course.java
public class Course<T> {
    private String name;
    private T[] students;

    public Course(String name, int capacity) {
        this.name = name;
        students = (T[]) (new Object[capacity]);
    }

    public String getName() {
        return name;
    }
    public T[] getStudents() {
        return students;
    }
    public void add(T t) { // 배열이 비어있는 부분을 찾아서 수강생을 추가하는 메소드
        for (int i=0; i<students.length; i++) {
            if (students[i] == null) {
                students[i] = t;
                break;
            }
        }
    }
}
```

<br>

## 제네릭 타입의 상속과 구현
제네릭 타입도 다른 타입과 마찬가지로 부모 클래스가 될 수 있습니다.

```java
public class ChildProduct<T, M> extends Product<T, M> { ... }
```

자식 제네릭 타입은 추가적으로 타입 파라미터를 가질 수 있습니다.

```java
public class ChildProduct<T, M, C> extends Product<T, M> { ... }
```

제네릭 인터페이스를 구현한 클래스도 제네릭 타입이 됩니다.

```java
// Storage.java
public interface Storage<T> {
	public void add(T item, int index);
	public T get(int index);
}

// StorageImpl.java
public class StorageImpl<T> implements Storage<T> {
	private T[] array;

	public StorageImpl(int capacity) {
		this.array = (T[]) (new Object[capacity]);
	}
	
	@Override
	public void add(T item, int index) {
		array[index] = item;
	}

	@Override
	public T get(int index) {
		return array[index];
	}
}
```

<br>

## 레퍼런스
- 이것이 자바다: 신용권의 Java 프로그래밍 정복
## 스트림 소개
스트림`Stream`은 자바 8부터 추가된 컬렉션(배열 포함)의 저장 요소를 하나씩 참조해서 람다식으로 처리할 수 있도록 해주는 반복자입니다.

### 반복자 스트림

```java
import java.util.*;

public class Main {
	public static void main(String[] args) {
    	List<String> list = Arrays.asList("홍길동", "김자바", "아무개");
        
        // Iterator
        Iterator<String> iterator = list.iterator();
        while (iterator.hasNext()) {
        	String name = iterator.next();
            System.out.println(name);
        }
        
        System.out.println();
        
        // Stream
        Stream<String> stream = list.stream();
        stream.forEach(name -> System.out.println(name));
    }
}
```

<br>

### 스트림의 특징

- 람다식으로 요소 처리 코드를 제공
- 내부 반복자를 사용하므로 병렬 처리가 쉬움
- 중간 처리와 최종 처리 작업 수행

<br>

#### 람다식으로 요소 처리 코드를 제공
Stream이 제공하는 대부분의 요소 처리 메소드는 함수적 인터페이스 매개 타입을 가지기 때문에 람다식 또는 메소드 참조를 이용해서 요소 처리 내용을 매개값으로 전달할 수 있습니다.

```java
import java.util.*;

class Student {
	private String name;
    private int score;
    
    public Student (String name, int score) {
    	this.name = name;
        this.scroe = score;
    }
    
    public String getName() {
    	return name;
    }
    
    public int getScore() {
    	return score;
    }
}

public class Main {
	public static void main(String[] args) {
    	List<Student> list = Arrays.asList(
        	new Student("홍길동", 90),
            new Student("김자바", 92)
        );
        
        Stream<Student> stream = list.stream();
        stream.forEach(s-> {
        	String name = s.getName();
            int score = s.getScore();
            System.out.println(name + "-" + score);
        });
    }
}
```

<br>

#### 내부 반복자를 사용하므로 병렬 처리가 쉬움

> 외부 반복자 (external iterator): 개발자가 코드로 직접 컬렉션의 요소를 반복해서 가져오는 코드 패턴
index를 이용하는 for문, Iterator를 이용하는 while문은 모두 외부 반복자를 이용하는 것임

> 내부 반복자 (internal iterator): 컬렉션 내부에서 요소들을 반복시키고, 요소당 처리해야 할 코드만 제공하는 코드 패턴

![](https://velog.velcdn.com/images/kid/post/477c41c4-40ff-4a22-8f7f-44a51a62cc70/image.png)

내부 반복자를 사용하면 컬렉션 내부에서 어떻게 요소를 반복시킬 것인가는 컬렉션에게 맡겨두고, 개발자는 요소 처리 코드에만 집중할 수 있다는 이점을 얻을 수 있습니다. 내부 반복자는 요소들의 반복 순서를 변경하거나, 멀티 코어 CPU를 최대한 활용하기 위해 요소들을 분배시켜 병렬 작업을 할 수 있게 도와주기 때문에 하나씩 처리하는 순차적 외부 반복자보다 효율적으로 요소를 반복시킬 수 있습니다.

<br>

#### 중간 처리와 최종 처리 작업 수행
스트림은 컬렉션의 요소에 대해 중간 처리와 최종 처리를 수행합니다. 중간 처리에서는 매핑, 필터링, 정렬을 수행하고 최종 처리에서는 반복, 카운팅, 평균, 총합 등의 집계 처리를 수행합니다.

![](https://velog.velcdn.com/images/kid/post/886131a9-8398-47a1-8058-ac5b3eada277/image.png)

#### 예제

```java
public class Main {
	public static void main(String[] args) {
    	List<Student> studentList = Arrays.asList(
        	new Student("홍길동", 10),
            new Student("김자바", 20),
            new Student("아무개", 30)
        );
        
        double avg = studentList.stream()
        	// 중간 처리 (학생 객체를 점수로 매핑)
            .mapToInt(Student :: getScore)
            // 최종 처리 (평균 점수)
            .average().getAsDouble();
            
        System.out.println("평균 점수: " + avg);
    }
}
```

<br>

## 스트림의 종류

![](https://velog.velcdn.com/images/kid/post/5fb4c3ef-81bd-4b60-9662-c79e4f854d9f/image.png)

BaseStream 인터페이스에는 모든 스트림에서 사용할 수 있는 공통 메소드들이 정의되어 있고, 하위 스트림들을 통해서 사용합니다. 스트림 인터페이스의 구현 객체는 주로 컬렉션과 배열에서 얻지만, 다음과 같은 소스로부터 스트림 구현 객체를 얻을 수도 있습니다.

|리턴 타입|메소드(매개 변수)|소스|
|---|---|---|
|Stream< T >|java.util.Collection.stream()<br>java.util.Collection.parallelStream()|컬렉션|
|Stream< T ><br>IntStream<br>LongStream<br>DoubleStream|Arrays.stream(T\[]), Stream(T\[])<br>Arrays.stream(int\[]), IntStream.of(int\[])<br>Arrays.stream(long\[]), LongStream.of(long\[])<br>Arrays.stream(double\[]), DoubleStream.of(double\[])|배열|
|IntStream|IntStream.range(int, int)<br>IntStream.rangeClosed(int, int)|int 범위|
|LongStream|LongStream.range(long, long)<br>LongStream.rangeClosed(long, long)|long 범위|
|Stream< Path >|Files.find(Path, int, BiPredicate, FileVisitOption)<br>Files.list(Path)|디렉토리|
|Stream< String >|Files.lines(Path, Charset)<br>BufferdReader.lines()|파일|
|DoubleStream<br>IntStream<br>LongStream|Random.doubles(...)<br>Random.ints()<br>Random.longs()|랜덤 수|

<br>

## 스트림 파이프라인
데이터의 합계, 평균값, 최대값, 최소값 등은 대표적인 리덕션의 결과물입니다.

> 리덕션 Reduction: 대량의 데이터를 가공해서 축소하는 것

컬렉션의 요소를 리덕션의 결과물로 바로 집계할 수 없을 경우에는 집계하기 좋도록 필터링, 매핑, 정렬, 그룹핑 등의 중간 처리가 필요합니다.

### 중간 처리와 최종 처리
스트림은 파이프라인으로 중간 처리와 최종 처리를 해결합니다.

> 파이프라인 pipelines: 여러 개의 스트림이 연결되어 있는 구조

중간 스트림이 생성될 때 요소들이 바로 중간 처리`필터링` `매핑` `정렬`되는 것이 아니라, 최종 처리가 시작되기 쩐까지 중간 처리는 지연됩니다. 최종 처리가 시작되면 비로소 컬렉션의 요소가 하나씩 중간 스트림에서 처리되고 최종 처리까지 오게 됩니다.

```java
Stream<Member> maleFemaleStream = list.stream();
Stream<Member> maleStream = maleFemaleStream.filter(m -> m.getGender()==Member.MALE);
IntStream ageStream = maleStream.mapToInt(Mamber :: getAge);
OptionalDouble optionalDouble = ageStream.average();
double ageAvg = optionDouble.getAsDouble();

// 로컬 변수 생략
double ageAvg = list.stream() // 오리지날 스트림
	.filter(m -> m.getGender()==Member.MALE) // 중간 처리 스트림
    .mapToInt(Mamber :: getAge) // 중간 처리 스트림
    .average() // 최종 처리
    .getAsDouble();
```

<br>

### 중간 처리 메소드와 최종 처리 메소드

![](https://velog.velcdn.com/images/kid/post/e80350fc-00c8-4b45-bde5-b02c99539d4d/image.png)

![](https://velog.velcdn.com/images/kid/post/5e329b60-f255-4ec5-b0fa-844e380b1a17/image.png)

> 리턴 타입이 스트림이라면 중간 처리 메소드이고, 기본 타입이거나 `OptionalXXX`라면 최종 처리 메소드

<br>

## 필터링 distinct(), filter()
필터링은 중간 처리 기능으로 요소를 걸러내는 역할을 합니다. 필터링 메소드인 `distinct()` `filter()` 는 모든 스트림이 가지고 있는 공통 메소드입니다.

|메소드(매개 변수)|설명|
|---|---|
|distinct()|중복 제거|
|filter(Predicate)<br>filter(IntPredicate)<br>filter(LongPredicate)<br>filter(DoublePredicate)|조건 필터링|

> distinct() 메소드는 Stream의 경우 Object.equals(Object)가 true이면 중복을 제거
나머지는 동일값일 경우 중복을 제거함

> filter() 메소드는 매개값으로 주어진 Predicate가 true를 리턴하는 요소만 필터링

#### 예제

```java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        List<String> names = Arrays.asList("홍길동", "김자바", "아무개", "홍길동");

        names.stream()
                .distinct()
                .forEach(n -> System.out.println(n));
        System.out.println();

        names.stream()
                .filter(n -> n.startsWith("홍"))
                .forEach(n -> System.out.println(n));
        System.out.println();

        names.stream()
                .distinct()
                .filter(n -> n.startsWith("홍"))
                .forEach(n -> System.out.println(n));
    }
}
```

<br>

## 매핑 flatMapXXX(), mapXXX(), asXXXStream(), boxed()
매핑은 중간 처리 기능으로 스트림의 요소를 다른 요소로 대체하는 작업을 의미합니다. 스트림에서 제공하는 매핑 메소드는 `flatXXX()` `mapXXX()` `asDoubleStream()` `asLongStream()` `boxed()`가 있습니다.

### flatMapXXX() 메소드
요소를 대체하는 복수 개의 요소들로 구성된 새로운 스트림을 리턴합니다.

![](https://velog.velcdn.com/images/kid/post/749ada5d-6aef-4f9c-ab78-5777a9e0e9e5/image.png)

|리턴 타입|메소드(매개 변수)|요소 -> 대체 요소|
|---|---|---|
|Stream< R >|flatMap(Function<T, Stream< R >>)|T -> Stream< R >|
|DoubleStream|flatMap(DoubleFunction< DoubleStream >)|double -> DoubleStream|
|IntStream|flatMap(IntFunction< IntStream >)|int -> IntStream|
|LongStream|flatMap(LongFunction< LongStream >)|long -> LongStream|
|DoubleStream|flatMapToDouble(Function<T, DoubleStream>)|T -> DoubleStream|
|IntStream|flatMapToInt(Function<T, IntStream>)|T -> IntStream|
|LongStream|flatMapToLong(Function<T, LongStream>)|T -> LongStream|

<br>

### mapXXX() 메소드
요소를 대체하는 요소로 구성된 새로운 스트림을 리턴합니다.

![](https://velog.velcdn.com/images/kid/post/9546105f-95ee-439c-82ea-6cf13b93f0fc/image.png)

|리턴 타입|메소드(매개 변수)|요소 -> 대체 요소|
|---|---|---|
|Stream< R >|map(Function<T, R>)|T -> R|
|DoubleStream|mapToDouble(ToDoubleFucntion< T >)|T -> double|
|IntStream|mapToInt(ToIntFunction< T >)|T -> int|
|LongStream|mapToLong(ToLongFunction< T >)|T -> long|
|DoubleStream|map(DoubleUnaryOperator)|double -> double|
|IntStream|mapToInt(DoubleToIntFunction)|double -> int|
|LongStream|mapToLong(DoubleToLongFunction)|double -> long|
|Stream< U >|mapToObj(DoubleFunction< U >)|double -> U|
|IntStream|map(IntUnaryOperator)|int -> int|
|DoubleStream|mapToDouble(IntToDoubleFunction)|int -> double|
|LongStream|mapToLong(IntToLongFunction)|int -> long|
|Stream< U >|mapToObj(IntFunction< U >)|int -> U|
|LongStream|map(LongUnaryOperator)|long -> long|
|DoubleStream|mapToDouble(LongToDoubleFunction)|long -> double|
|IntStream|mapToInt(LongToIntFunction)|long -> Int|
|Stream< U >|mapToObj(LongFunction< U >)|long -> U|

<br>

### asDoubleStream(), asLongStream(), boxed() 메소드

|리턴 타입|메소드(매개 변수)|설명|
|---|---|---|
|DoubleStream|asDoubleStream()|int -> double<br>long -> double|
|LongStream|asLongStream()|int -> long|
|Stream< Interger ><br>Stream< Long ><br>Stream< Double >|boxed()|int -> Integer<br>long -> Long<br>double -> Double|

<br>

## 정렬 sorted()
스트림은 요소가 최종 처리되기 전에 중간 단계에서 요소를 정렬해서 최종 처리 순서를 변경할 수 있습니다.

|리턴 타입|메소드(매개 변수)|설명|
|---|---|---|
|Stream< T >|sorted()|객체를 Comparable 구현 방법에 따라 정렬|
|Stream< T >|sorted(Comparator< T >)|객체를 주어진 Comparator에 따라 정렬|
|DoubleStream|sorted()|double 요소를 오름차순으로 정렬|
|IntStream|sorted()|int 요소를 오름차순으로 정렬|
|LongStream|sorted()|long 요소를 오름차순으로 정렬|

> 객체 요소일 경우에는 클래스가 Comparable을 구현하지 않으면 sorted() 메소드를 호출했을 때 ClassCastException이 발생합니다.

#### 예제

```java
import java.util.*;
import java.util.stream.IntStream;

class Student implements Comparable<Student> {
    private String name;
    private int score;

    public Student(String name, int score) {
        this.name = name;
        this.score = score;
    }

    public String getName() {
        return name;
    }

    public int getScore() {
        return score;
    }

    @Override
    public int compareTo(Student o) {
        return Integer.compare(score, o.score);
    }
}

public class Main {
    public static void main(String[] args) {
        // 숫자 요소일 경우
        IntStream intStream = Arrays.stream(new int[]{5, 3, 2, 1, 4});
        intStream
                .sorted() // 오름차순 정렬
                .forEach(n -> System.out.print(n + ", "));
        System.out.println();

        // 객체 요소일 경우
        List<Student> studentList = Arrays.asList(
                new Student("홍길동", 30),
                new Student("김자바", 10),
                new Student("아무개", 20)
        );

        studentList.stream()
                .sorted()
                .forEach(s -> System.out.print(s.getScore() + ", "));
        System.out.println();

        studentList.stream()
                .sorted(Comparator.reverseOrder())
                .forEach(s -> System.out.print(s.getScore() + ", "));
    }
}
```

<br>

## 루핑 peek(), forEach()
두 메소드는 루핑한다는 기능에서는 동일하지만, `peek()`은 중간 처리 메소드이고, `forEach()`는 최종 처리 메소드입니다.

```java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        int[] intArr = {1, 2, 3, 4, 5};

        System.out.println("[peek()을 마지막에 호출한 경우]");
        Arrays.stream(intArr)
                .filter(a -> a%2==0)
                .peek(n -> System.out.println(n)); // 동작하지 않음

        System.out.println("[최종 처리 메소드를 마지막에 호출한 경우]");
        int total = Arrays.stream(intArr)
                .filter(a -> a%2==0)
                .peek(n -> System.out.println(n))
                .sum();
        System.out.println("총합: " + total);

        System.out.println("[forEach()를 마지막에 호출한 경우]");
        Arrays.stream(intArr)
                .filter(a -> a%2==0)
                .forEach(n -> System.out.println(n));
    }
}
```

<br>

## 매칭 allMatch(), anyMatch(), noneMatch()
스트림 클래스는 최종 처리 단계에서 요소들이 특정 조건에 만족하는지 조사할 수 있도록 세 가지 매칭 메소드를 제공합니다.

- `allMatch()`: 모든 요소들이 조건을 만족하는지 조사
- `anyMatch()`: 최소한 한 개의 요소가 조건을 만족하는지 조사
- `noneMatch()`: 모든 요소들이 조건을 만족하지 않는지 조사

|리턴 타입|메소드(매개 변수)|제공 인터페이스|
|---|---|---|
|boolean|allMatch(Predicate< T > predicate)<br>anyMatch(Predicate< T > predicate)<br>noneMatch(Predicate< T > predicate)|Stream|
|boolean|allMatch(IntPredicate predicate)<br>anyMatch(IntPredicate predicate)<br>noneMatch(IntPredicate predicate)|IntStream|
|boolean|allMatch(LongPredicate predicate)<br>anyMatch(LongPredicate predicate)<br>noneMatch(LongPredicate predicate)|LongStream|
|boolean|allMatch(DoublePredicate predicate)<br>anyMatch(DoublePredicate predicate)<br>noneMatch(DoublePredicate predicate)|DoubleStream|

<br>

## 기본 집계 sum(), count(), average(), max(), min()
집계는 최종 처리 기능으로 요소들을 처리해서 하나의 값으로 산출하는 것을 의미합니다. 집계는 대량의 데이터를 가공해서 축소하기 때문에 리덕션이라고 볼 수 있습니다.

### 스트림이 제공하는 기본 집계

|리턴 타입|메소드(매개 변수)|설명|
|---|---|---|
|long|count()|요소 개수|
|OptionalXXX|findFirst()|첫 번째 요소|
|Optional< T ><br>OptionalXXX|max(Comparator< T >)<br>max()|최대 요소|
|Optional< T ><br>OptionalXXX|min(Comparator< T >)<br>min()|최소 요소|
|OptionalDouble|average()|요소 평균|
|int, long, double|sum()|요소 총합|

<br>

### Optional 클래스
Optional 클래스는 집계 값이 존재하지 않을 경우 디폴트 값을 설정할 수도 있고, 집계 값을 처리하는 Consumer도 등록할 수 있습니다.

|리턴 타입|메소드(매개 변수)|설명|
|---|---|---|
|boolean|isPresent()|값이 저장되어 있는지 여부|
|T<br>double<br>int<br>long|orElse(T)<br>orElse(double)<br>orElse(int)<br>orElse(long)|값이 저장되어 있지 않을 경우 디폴트 값 지정|
|void|ifPresent(Consumer)<br>ifPresent(DoubleConsumer)<br>ifPresent(IntConsumer)<br>ifPresent(LongConsumer)|값이 저장되어 있을 경우 Consumer에서 처리|

```java
List<Integer> list = new ArrayList<>();
double avg = list.stream()
	.mapToInt(Integer :: intValue)
    .average()
    .getAsDouble();
System.out.println("평균: " + avg);
```

위 코드에서 컬렉션의 요소가 추가되지 않아 저장된 요소가 없는 상황이 생길 수 있습니다. 그럴 경우 평균값도 구할 수 없기 때문에 NoSuchElementException 예외가 발생합니다.

요소가 없을 경우 예외를 피하는 세 가지 방법이 있습니다.

```java
// 방법 1 - Optional 객체를 얻어 isPresent() 메소드로 평균값 여부 확인:
OptionalDouble optional = list.stream()
	.mapToInt(Integer :: intValue)
    .average();
if (optional.isPresent()) {
	System.out.println("평균: " + optional.getAsDouble());
} else {
	System.out.println("평균: 0.0");
}

// 방법 2 - orElse() 메소드로 디폴트 값 정해놓기
double avg = list.stream()
	.mapToInt(Integer :: intValue)
    .average()
    .orElse(0.0);
System.out.println("평균: " + avg);

// 방법 3 - ifPresent() 메소드로 평균값이 있을 경우에만 람다식 실행
list.stream()
	.mapToInt(Integer :: intValue)
    .average()
    .ifPresent(a -> System.out.println("평균: " + a));
```

<br>

## 커스텀 집계 reduce()
스트림은 기본 집계 메소드인 `sum()` `average()` `count()` `max()` `min()`을 제공하지만, 다양한 집계 결과물을 만들 수 있도록 `reduce()` 메소드도 제공합니다.

|인터페이스|리턴 타입|메소드(매개 변수)|
|---|---|---|
|Stream|Optional< T ><br>T|reduce(BinaryOperator< T > accumulator)<br>reduce(T identity, BinaryOperator< T > accumulator)|
|IntStream|OptionalInt<br>int|reduce(IntBinaryOperator op)<br>reduce(int identity, IntBinaryOperator op)|
|LongStream|OptionalLong<br>long|reduce(LongBinaryOperator op)<br>reduce(long identity, LongBinaryOperator op)|
|DoubleStream|OptionalDouble<br>double|reduce(DoubleBinaryOperator op)<br>reduce(double identiry, DoubleBinaryOperator op)|

```java
// 예제 1:
int sum = studentList.stream()
	.map(Student :: getScore)
    .reduce((a, b) -> a+b)
    .get();

// 예제 2:
int sum = studentList.stream()
	.map(Student :: getScore)
    .reduce(0, (a, b) -> a+b);
```

<br>

## 수집 collet()
스트림은 요소들을 필터링 또는 매핑한 후 요소들을 수집하는 최종 처리 메소드 `collect()`를 제공합니다. 이 메소드를 이용하면 필요한 요소만 컬렉션으로 담을 수 있습니다.

### 필터링한 요소 수집

|리턴 타입|메소드(매개 변수)|인터페이스|
|---|---|---|
|R|collect(Collector<T, A, R> collector)|Stream|

> 타입 파라미터 T는 요소, A는 누적기 (accumulator), R은 요소가 저장될 컬렉션을 의미함

|리턴 타입|Collectors의 정적 메소드|설명|
|---|---|---|
|Collector<T, ?, List< T >>|toList()|T를 List에 저장|
|Collector<T, ?, Set< T >>|toSet()|T를 Set에 저장|
|Collector<T, ?, Collection< T >>|toCollection(<br>&nbsp;Supplier<Collection< T >><br>)|T를 Supplier가 제공한 Collection에 저장|
|Collector<T, ?, Map<K, U>>|toMap(<br>&nbsp;Function<T, K> keyMapper,<br>&nbsp;Function<T, U> valueMapper)|T를 K와 U로 매핑해서 K를 키로,<br>U를 값으로 Map에 저장|
|Collector<T, ?, ConcurrentMap<K, U>>|toConcurrentMap(<br>&nbsp;Function<T, K> keyMapper,<br>&nbsp;Function<T, U> valueMapper)|T를 K와 U로 매핑해서 K를 키로,<br>U를 값으로 ConcurrentMap에 저장|

> ConcurrentMap은 스레드에 안전함

<br>

### 사용자 정의 컨테이너에 수집
List, Set, Map과 같은 컬렉션이 아니라 사용자 정의 컨테이너 객체에 요소들을 수집할 수도 있습니다.

|인터페이스|리턴 타입|메소드(매개 변수)|
|---|---|---|
|Stream|R|collect(Supplier< R >, BiConsumer<R, ?, super T>, BiConsumer<R, R>)|
|IntStream|R|collect(Supplier< R >, ObjIntConsumer< R >, BiConsumer<R, R>)|
|LongStream|R|collect(Supplier< R >, ObjLongConsumer< R >, BiConsumer<R, R>)|
|DoubleStream|R|collect(Supplier< R >, ObjDoubleConsumer< R >, BiConsumer<R, R>)|

- 첫 번째 `Supplier`는 요소들이 수집될 컨테이너 객체(R)를 생성하는 역할을 합니다. 순차 처리(싱글 스레드) 스트림에서는 단 한 번 실행되고 하나의 컨테이너 객체를 생성합니다. 병렬 처리(멀티 스레드) 스트림에서는 여러 번 실행되고 스레드별로 여러 개의 컨테이너 객체를 생성합니다. 하지만 최종적으로 하나의 컨테이너 객체로 결합됩니다.
- 두 번째 `XXXConsumer`는 컨테이너 객체(R)에 요소(T)를 수집하는 역할을 합니다. 스트림에서 요소를 컨테이너에 수집할 때마다 실행됩니다.
- 세 번째 `BiConsumer`는 컨테이너 객체(R)를 결합하는 역할을 합니다. 순차 처리 스트림에서는 호출되지 않고, 병렬 처리 스트림에서만 호출되어 스레드별로 생성된 컨테이너 객체를 결합해서 최종 컨테이너 객체를 완성합니다.

<br>

### 요소를 그룹핑해서 수집
`collect()` 메소드는 단순히 요소를 수집하는 기능 이외에 컬렉션의 요소들을 그룹핑해서 Map객체를 생성하는 기능도 제공합니다. collect()를 호출할 때 Collectors의 `groupingBy()` 또는 `groupingByConcurrent()`가 리턴하는 Collector를 매개값으로 대입하면 됩니다.

> groupingBy()는 스레드에 안전하지 않은 Map을 생성하고,
groupingByConcurrent()는 스레드에 안전한 ConcurrentMap을 생성합니다.

![](https://velog.velcdn.com/images/kid/post/c8d38eba-134c-4859-919a-9e2aa8ad8839/image.png)

<br>

### 그룹핑 후 매핑 및 집계
Collectors는 집계를 위해 다양한 Collector를 리턴하는 메소드를 제공합니다.

![](https://velog.velcdn.com/images/kid/post/347873a6-37cf-4990-ae64-b6bbda4e8598/image.png)

<br>

## 병렬 처리
병렬 처리`Parallel Operation`란 멀티 코어 CPU 환경에서 하나의 작업을 분할해서 각각의 코어가 병렬적으로 처리하는 것을 의미합니다. 자바 8부터 요소를 병렬 처리할 수 있도록 하기 위해 병렬 스트림을 제공합니다.

### 동시성(Concurrency)과 병렬성(Parallelism)

- 동시성: 멀티 스레드가 번갈아가며 실행하는 성질
- 병렬성: 멀티 코어를 이용해서 동시에 실행하는 성질 (데이터 병렬성과 작업 병렬성으로 구분)

![](https://velog.velcdn.com/images/kid/post/24299b22-f841-4acb-a63b-e40dec565ec5/image.png)

#### 데이터 병렬성
전체 데이터를 쪼개어 서브 데이터들로 만들고, 이 서브 데이터들을 병렬 처리해서 작업을 빨리 끝내는 것을 의미합니다. 예를 들어 쿼드 코어 CPU일 경우 4개의 서브 요소들로 나누고, 4개의 스레드가 각각의 서브 요소들을 병렬 처리합니다. 

> 자바 8에서 지원하는 병렬 스트림은 데이터 병렬성을 구현한 것입니다.

#### 작업 병렬성
서로 다른 작업을 병렬 처리하는 것을 의미합니다. 대표적인 예는 웹 서버입니다. 웹 서버는 각각의 브라우저에서 요청한 내용을 개별 스레드에서 병렬로 처리합니다.

<br>

### 포크조인(ForkJoin) 프레임워크
병렬 스트림은 요소들을 병렬 처리하기 위해 포크조인 프레임워크를 사용합니다.

- 병렬 스트림을 이용하면 런타임 시에 포크조인 프레임워크가 동작
- 포크 단계에서 전체 데이터를 서브 데이터로 분리
- 서브 데이터를 멀티 코어에서 병렬로 처리
- 조인 단계에서 서브 결과를 결합해서 최종 결과를 만들어냄

![](https://velog.velcdn.com/images/kid/post/d0d6bdfb-a68d-4d1a-8168-710812e0fe3d/image.png)

포크조인 프레임워크는 포크와 조인 기능 이외에 스레드풀인 `ForkJoinPool`을 제공합니다. 각각의 코어에서 서브 요소를 처리하는 것은 개별 스레드가 해야 하므로 스레드 관리가 필요한데, ExecutorService의 구현 객체인 ForkJoinPool을 사용해서 작업 스레드를 관리합니다.

<br>

### 병렬 스트림 생성
병렬 스트림을 이용할 경우에는 백그라운드에서 포크조인 프레임워크가 사용되기 때문에 간단히 병렬 처리를 할 수 있습니다. 병렬 스트림은 다음 두 가지 메소드로 얻습니다.

![](https://velog.velcdn.com/images/kid/post/2bbf9e7b-f041-4b88-840c-b3e774050511/image.png)

`parallelStream()` 메소드는 컬렉션으로부터 병렬 스트림을 바로 리턴합니다. `parallel()` 메소드는 순차 처리 스트림을 병렬 처리 스트림으로 변환해서 리턴합니다.

<br>

### 병렬 처리 성능

#### 요소의 수와 요소당 처리 시간

- 컬렉션에 요소의 수가 적고 요소당 처리 시간이 짧으면 순차 처리가 오히려 빠를 수 있음
- 병렬 처리는 스레드풀 생성, 스레드 생성이라는 추가적인 비용이 발생하기 때문

#### 스트림 소스의 종류

- ArrayList, 배열은 인덱스로 요소를 관리하기 때문에 포크 단계에서 요소를 쉽게 분리할 수 있음
- HashSet, TreeSet은 요소 분리가 쉽지 않고, LinkedList도 링크를 따라가야 하므로 쉽지 않음

#### 코어의 수

- 싱글 코어 CPU일 경우에는 순차 처리가 더 빠름
- 병렬 스트림을 사용할 경우 스레드의 수만 증가하고 동시성 작업으로 처리되기 때문에 별로임
- 코어의 수가 많으면 많을수록 병렬 작업 처리 속도는 빨라짐

<br>

## 레퍼런스
- 이것이 자바다: 신용권의 Java 프로그래밍 정복
- Stream이란?: https://steady-coding.tistory.com/314
- \[Java] 스트림과 병렬처리 - 필터링, 매핑, 정렬: https://jang8584.tistory.com/237
- 이것은 자바다 16장(스트림과 병렬처리): https://velog.io/@ansalstmd/%EC%9D%B4%EA%B2%83%EC%9D%80-%EC%9E%90%EB%B0%94%EB%8B%A4-16%EC%9E%A5%EC%8A%A4%ED%8A%B8%EB%A6%BC%EA%B3%BC-%EB%B3%91%EB%A0%AC%EC%B2%98%EB%A6%AC
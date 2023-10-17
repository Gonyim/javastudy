## 컬렉션 프레임워크 소개
자바에서는 객체들을 효율적으로 추가, 삭제, 검색할 수 있도록 java.util 패키지에 컬렉션과 관련된 인터페이스와 클래스들을 포함시켜 놓았는데, 이들을 총칭해서 컬렉션 프레임워크`Collection Framework`라고 부릅니다. 컬렉션은 객체를 수집해서 저장하는 역할을 하고, 프레임워크는 사용 방법을 미리 정해 놓은 라이브러리를 의미합니다. 컬렉션 프레임워크는 몇 가지 인터페이스를 통해서 다양한 컬렉션 클래스를 이용할 수 있도록 돕습니다. 주요 인터페이스로는 `List` `Set` `Map`이 있습니다.

![JCF](https://velog.velcdn.com/images/kid/post/b5485b5a-0173-4830-8cd6-b0f295f437cc/image.png)

- List, Set은 객체를 추가, 삭제, 검색하는 방법에 많은 공통점이 있기 때문에 이 인터페이스들의 공통된 메소드들만 모아 Collection 인터페이스로 정의해 두고 있음
- Map은 키와 값을 하나의 쌍으로 묶어서 관리하는 구조로 되어 있어, List, Set과는 사용 방법이 다름

|인터페이스 분류|특징|구현 클래스|
|---|---|---|
|List|- 순서를 유지하고 저장<br>- 중복 저장 가능|ArrayList, Vector,<br>LinkedList|
|Set|- 순서를 유지하지 않고 저장<br>- 중복 저장 안됨|HashSet, TreeSet|
|Map|- 키와 값의 쌍으로 저장<br>- 키는 중복 저장 안됨|HashMap, Hashtable,<br>TreeMap, Properties|

<br>

## List 컬렉션

- 객체를 일렬로 늘어놓은 구조
- 인덱스로 객체 관리함
- 객체 자체를 저장하는 것이 아닌 번지를 참조 (동일한 객체를 중복 저장할 때는 동일한 번지)
- ArrayList, Vector, LinkedList 등이 있음

#### 공통적으로 사용 가능한 메소드

|기능|메소드|설명|
|---|---|---|
|객체 추가|boolean add(E e)<br>void add(int index, E element)<br>E set(int index, E element)|- 주어진 객체를 맨 끝에 추가<br>- 주어진 인덱스에 객체를 추가<br>- 주어진 인덱스에 저장된 객체를 주어진 객체로 바꿈|
|객체 검색|boolean contains(Object o)<br>E get(int index)<br>boolean isEmpty()<br>int size()|- 주어진 객체가 저장되어 있는지 여부<br>- 주어진 인덱스에 저장된 객체를 리턴<br>- 컬렉션이 비어 있는지 조사<br>- 저장되어 있는 전체 객체 수를 리턴|
|객체 삭제|void clear()<br>E remove(int index)<br>boolean remove(Object o)|- 저장된 모든 객체를 삭제<br>- 주어진 인덱스에 저장된 객체를 삭제<br>- 주어진 객체를 삭제|

List 인터페이스는 제네릭 타입이기 때문에 리턴 타입에 E 타입 파라미터가 올 수 있습니다. 구체적인 타입은 구현 객체를 생성할 때 결정됩니다.

```java
List<String> list = ...;
list.add("홍길동"); // 맨 끝에 객체 추가
list.add(1, "김자바"); // 지정된 인덱스에 객체 추가
String str = list.get(1); // 인덱스로 객체 찾기
list.remove(0); // 인덱스로 객체 삭제
list.remove("신용권"); // 객체 삭제
```

<br>

### ArrayList

- 배열은 생성할 때 크기가 고정되고 사용 중에 크기 변경 불가
- `ArrayList`는 저장 용량`capacity`을 초과한 객체들이 들어오면 자동적으로 크기가 늘어남
- 저장할 객체 타입을 타입 파라미터로 표기하고 기본 생성자를 호출
- 매개값을 입력하면 크기 지정 가능

```java
// 초기 용량은 10
List<String> list = new ArrayList<String>();
```

ArrayList에서 특정 인덱스의 객체를 제거하면 바로 뒤 인덱스부터 마지막 인덱스까지 모두 앞으로 1씩 당겨집니다. 마찬가지로 특정 인덱스에 객체를 삽입하면 해당 인덱스부터 마지막 인덱스까지 모두 1씩 밀려납니다. 따라서 빈번한 객체 삭제와 삽입이 일어나는 곳에서는 ArrayList보다 LinkedList를 사용하는 것이 좋습니다.

> 인덱스 검색이나, 맨 마지막에 객체를 추가하는 경우에는 ArrayList의 성능이 더 좋음

#### 예제

```java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        List<String> list = new ArrayList<>();

        list.add("java");
        list.add("JDBC");
        list.add("Servlet/JSP");
        list.add(2, "Database");
        list.add("iBATIS");

        int size = list.size(); // 저장된 총 객체 수 얻기
        System.out.println("총 객체수: " + size);
        System.out.println();

        String skill = list.get(2);
        System.out.println("2: " + skill);
        System.out.println();

        for (int i=0; i<list.size(); i++) {
            String str = list.get(i);
            System.out.println(i + ":" + str);
        }
        System.out.println();

        list.remove(2);
        list.remove(2);
        list.remove("iBATIS");
        
        for (int i=0; i<list.size(); i++) {
            String str = list.get(i);
            System.out.println(i + ":" + str);
        }
    }
}
```

```java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        List<String> list1 = Arrays.asList("홍길동", "김자바", "아무개");
        for (String name : list1) {
            System.out.println(name);
        }

        List<Integer> list2= Arrays.asList(1, 2, 3);
        for (int value : list2) {
            System.out.println(value);
        }
    }
}
```

<br>

### Vector

```java
List<E> list = new Vector<E>();
```

Vector는 ArrayList와 동일한 내부 구조를 가지고 있습니다. Vector는 동기화된 메소드로 구성되어 있기 때문에 멀티 스레드가 동시에 실행할 수 없다는 것이 차이점입니다. 그래서 멀티 스레드 환경에서 안전하게 객체를 추가, 삭제할 수 있습니다. 이것을 스레드가 안전`Thread Safe`하다고 표현합니다.

#### 예제

```java
import java.util.*;

class Board {
    String subject;
    String content;
    String writer;

    public Board(String subject, String content, String writer) {
        this.subject = subject;
        this.content = content;
        this.writer = writer;
    }
}

public class Main {
    public static void main(String[] args) {
        List<Board> list = new Vector<>();

        list.add(new Board("제목1", "내용1", "글쓴이1"));
        list.add(new Board("제목2", "내용1", "글쓴이2"));
        list.add(new Board("제목3", "내용3", "글쓴이3"));
        list.add(new Board("제목4", "내용4", "글쓴이4"));
        list.add(new Board("제목5", "내용5", "글쓴이5"));
        
        list.remove(2);
        list.remove(3);
        
        for (int i=0; i<list.size(); i++) {
            Board board = list.get(i);
            System.out.println(board.subject + "\t" + board.content + "\t" + board.writer);
        }
    }
}
```

<br>

### LinkedList

```java
List<E> list = new LinkedList<E>();
```

ArrayList는 내부 배열에 객체를 저장해서 인덱스로 관리하지만, LinkedList는 인접 참조를 링크해서 체인처럼 관리합니다.

![LinkedList](https://velog.velcdn.com/images/kid/post/3ae1fb67-b92e-49d4-bf4a-39c630785230/image.png)

|구분|순차적으로 추가/삭제|중간에 추가/삭제|검색|
|---|---|---|---|
|ArrayList|빠름|느림|빠름|
|LinkedList|느림|빠름|느림|

<br>

## Set 컬렉션

- List 컬렉션은 저장 순서를 유지하지만, Set 컬렉션은 저장 순서가 유지되지 않음
- 객체를 중복해서 저장할 수 없음 (null도 마찬가지)
- 집합의 개념
- HashSet, LinkedHashSet, TreeSet 등이 있음

#### 공통적으로 사용 가능한 메소드

|기능|메소드|설명|
|---|---|---|
|객체<br>추가|boolean add(E e)|- 주어진 객체를 저장, 객체가 성공적으로 저장되면 true를 리턴하고 중복 객체면 false를 리턴|
|객체<br>검색|boolean contains(Object o)<br>boolean isEmpty()<br>Iterator< E > iterator()<br>int size()|- 주어진 객체가 저장되어 있는지 여부<br>- 컬렉션이 비어 있는지 조사<br>- 저장된 객체를 한 번씩 가져오는 반복자 리턴<br>- 저장되어 있는 전체 객체 수 리턴|
|객체<br>삭제|void clear()<br>boolean remove(Object o)|- 저장된 모든 객체를 삭제<br>- 주어진 객체를 삭제|

Set 컬렉션은 객체를 인덱스로 관리하지 않기 때문에 전체 객체를 대상으로 한 번씩 반복해서 가져오는 반복자`Iterator`를 제공합니다. 반복자는 Iterator 인터페이스를 구현한 객체를 의미하고, `iterator()` 메소드를 호출해서 얻을 수 있습니다.

|리턴 타입|메소드명|설명|
|---|---|---|
|boolean|hasNext()|가져올 객체가 있으면 true를 리턴하고 없으면 false를 리턴|
|E|next()|컬렉션에서 하나의 객체를 가져옴|
|void|remove()|Set 컬렉션에서 객체를 제거|

```java
Set<String> set = ...;
Iterator<String> iterator = set.iterator();

while (iterator.hasNext()) {
	String str = iterator.next();
}
```

```java
// Iterator를 사용하지 않을 경우
Set<String> set = ...;

for (String str : set) {
	System.out.println(str);
}
```

<br>

### HashSet

```java
Set<E> set = new HashSet<E>();
```

HashSet은 객체를 저장하기 전에 먼저 객체의 `hashCode()` 메소드를 호출해서 해시코드를 얻습니다. 그리고 이미 저장되어 있는 객체들의 해시코드와 비교합니다. 만약 동일한 해시코드가 있다면 다시 `equals()` 메소드로 두 객체를 비교해서 true가 나오면 동일한 객체로 판단하고 중복 저장을 하지 않습니다.

> String 클래스의 경우, 같은 문자열일 경우 hashCode()의 리턴값을 같게, equals()의 리턴값은 true가 나오도록 재정의되어 있습니다.

#### 예제 - hashCode(), equals() 오버라이딩

```java
import java.util.*;

class Member {
    public String name;
    public int age;

    public Member(String name, int age) {
        this.name = name;
        this.age = age;
    }

    @Override
    public boolean equals(Object obj) {
        if (obj instanceof Member) {
            Member member = (Member) obj;
            return member.name.equals(name) && (member.age==age);
        } else {
            return false;
        }
    }

    @Override
    public int hashCode() {
        return name.hashCode() + age;
    }
}

public class Main {
    public static void main(String[] args) {
        Set<Member> set = new HashSet<>();

        // 인스턴스는 다르지만 내부 데이터가 동일하므로 객체가 1개만 저장됨
        set.add(new Member("홍길동", 20));
        set.add(new Member("홍길동", 20));

        System.out.println("총 객체수: " + set.size());
    }
}
```

<br>

## Map 컬렉션

- 키`key`와 값`value`로 구성된 `Entry`객체를 저장하는 구조
- 키와 값은 모두 객체임
- 키는 중복 저장될 수 없고, 값은 중복 저장 가능
- 기존 키와 동일한 키로 값을 저장하면 새로운 값으로 대치됨
- HashMap, Hashtable, LinkedHashMap, Properties, TreeMap 등이 있음

#### 공통적으로 사용 가능한 메소드

|기능|메소드|설명|
|---|---|---|
|객체<br>추가|V put(K key, V value)|주어진 키로 값을 저장. 새로운 키일 경우 null을 리턴하고 동일한<br>키가 있을 경우 값을 대체하고 이전 값을 리턴|
|객체<br>검색|- boolean containKet(Object key)<br>- boolean containValue(Object value)<br>- Set<Map.Entry<K, V>> entrySet()<br>- V get(Object key)<br>- boolean isEmpty()<br>- Set< K > ketSet()<br>- int size()<br>- Collection< V > values()|- 주어진 키가 있는지 여부<br>- 주어진 값이 있는지 여부<br>- 키와 값의 쌍으로 구성된 모든 Map.Entry 객체를 Set에 담아 리턴<br>- 주어진 키가 있는 값을 리턴<br>- 컬렉션이 비어있는지 여부<br>- 모든 키를 Set 객체에 담아서 리턴<br>- 저장된 키의 총 수를 리턴<br>- 저장된 모든 값을 Collection에 담아서 리턴|
|객체<br>삭제|- void clear()<br>- V remove(Object key)|- 모든 Map.Entry(키와 값)을 삭제<br>- 주어진 키와 일치하는 Map.Entry를 삭제하고 값을 리턴|

#### 전체 객체 탐색하기

```java
// 방법 1 - keySet() 메소드:
Map<K, V> map = ...;
Set<K> keySet = map.keySet();
Iterator<K> keyIterator = keySet.iterator();

while (keyIterator.hasNext()) {
	K key = keyIterator.next();
    V value = map.get(key);
}

// 방법 2 - entrySet() 메소드:
Set<Map.Entry<K, V>> entrySet = map.entrySet();
Iterator<Map.Entry<K, V>> entryIterator = entrySet.iterator();

while (entryIterator.hasNext()) {
	Map.Entry<K, V> entry = entryIterator.next();
    K key = entry.getKey();
    V value = entry.getValue();
}
```

<br>

### HashMap

```java
Map<K, V> map = new HashMap<K, V>();
```

HashMap의 키로 사용할 객체는 `hashCode()`와 `equals()` 메소드를 재정의해야 합니다. 키와 값의 타입은 기본 타입을 사용할 수 없고 클래스 및 인터페이스 타입만 가능합니다.

> hashCode()의 리턴값이 같고, equals() 메소드가 true를 리턴하도록 재정의

#### 예제

```java
import java.util.*;

class Student {
	public int sno;
    public String name;
    
    public Student(int sno, String name) {
    	this.sno = sno;
        this.name = name;
    }
    
    public boolean equals(Object obj) {
    	if (obj instanceof Student) {
        	Student student = (Student) obj;
            return (sno==student.sno) && (name.equals(student.name));
        } else {
        	return false;
        }
    }
    
    public int hashCode() {
    	return sno + name.hashCode();
    }
}

public class Main {
	public static void main(String[] args) {
    	Map<Student, Integer> map = new HashMap<>();
        
        map.put(new Student(1, "홍길동"), 90);
        map.put(new Student(1, "홍길동"), 95);
        
        System.out.println("총 Entry 수: " + map.size());
    }
}
```

<br>

### Hashtable
Hashtable은 HashMap과 동일한 내부 구조를 가지고 있습니다. 그래서 Hashtable 역시 키로 사용할 객체는 `hashCode()`와 `equals()` 메소드를 재정의해서 사용합니다. Hashtable은 동기화된 메소드로 구성되어 있어서 **멀티 스레드 환경에서 안전하다는 것이 HashMap과의 차이점**입니다.

<br>

### Properties
Properties는 Hashtable의 하위 클래스이기 때문에 Hashtable의 모든 특징을 그대로 가지고 있습니다. Hashtable은 키와 값을 다양한 타입으로 지정할 수 있고, Properties는 String 타입만 가능하다는 것이 차이점입니다.

> Properties는 애플리케이션의 옵션 정보, 데이터베이스 연결 정보, 국제화(다국어) 정보가 저장된 프로퍼티(~.properties) 파일을 읽을 때 주로 사용함

프로퍼티 파일은 키와 값이 `=` 기호로 연결되어 있는 텍스트 파일로 ISO 8859-1 문자셋으로 저장됩니다.

<br>

## 검색 기능을 강화시킨 컬렉션
컬렉션 프레임워크는 검색 기능을 강화시킨 TreeSet과 TreeMap을 제공합니다. 이 컬렉션들은 이진 트리`binary tree`를 이용해서 계층적 구조를 가지면서 객체를 저장합니다.

### 이진 트리 구조

- 여러 개의 노드가 트리 형태로 연결된 구조
- 루트 노드`root node`라고 불리는 하나의 노드에서 시작
- 위 아래로 연결된 두 노드는 부모-자식 관계. 부모 노드는 최대 두 개의 자식 노드와 연결

![binary tree](https://velog.velcdn.com/images/kid/post/cd6aad03-0165-4b32-8861-c3a8613292b5/image.png)

<br>

### TreeSet

```java
TreeSet<E> treeSet = new TreeSet<E>();
```

TreeSet은 노드값인 value와 왼쪽과 오른쪽 자식 노드를 참조하기 위한 두 개의 변수로 구성됩니다. 객체를 저장하면 부모값과 비교해서 낮은 것은 왼쪽 자식 노드, 높은 것은 오른쪽 자식 노드에 자동으로 정렬됩니다.

위처럼 TreeSet 클래스 타입으로 대입하면 TreeSet이 가지고 있는 메소드들을 사용할 수 있습니다.

#### 검색 관련 메소드

|리턴 타입|메소드|설명|
|---|---|---|
|E|first()|제일 낮은 객체를 리턴|
|E|last()|제일 높은 객체를 리턴|
|E|lower(E e)|주어진 객체보다 바로 아래 객체를 리턴|
|E|higher(E e)|주어진 객체보다 바로 위 객체를 리턴|
|E|floor(E e)|주어진 객체와 동등한 객체가 있으면 리턴<br>만약 없다면 주어진 객체의 바로 아래 객체를 리턴|
|E|ceiling(E e)|주어진 객체와 동등한 객체가 있으면 리턴<br>만약 없다면 주어진 객체의 바로 위 객체를 리턴|
|E|pollFirst()|제일 낮은 객체를 꺼내오고 컬렉션에서 제거|
|E|pollLast|제일 높은 객체를 꺼내오고 컬렉션에서 제거|

#### 정렬 관련 메소드

|리턴 타입|메소드|설명|
|---|---|---|
|Iterator< E >|descendingIterator()|내림차순으로 정렬된 Iterator를 리턴|
|NevigableSet< E >|descendingSet()|내림차순으로 정렬된 NevigableSet을 반환|

#### 범위 검색 관련 메소드

|리턴 타입|메소드|설명|
|---|---|---|
|NevigableSet< E >|headSet (<br>&nbsp;E toElement,<br>&nbsp;boolean inclusive<br>)|주어진 객체보다 낮은 객체들을 NevigableSet으로 리턴<br>주어진 객체 포함 여부는 두 번째 매개값에 따라 달라짐|
|NevigableSet< E >|tailSet (<br>&nbsp;E fromElement,<br>&nbsp;boolean inclusive<br>)|주어진 객체보다 높은 객체들을 NevigableSet으로 리턴<br>주어진 객체 포함 여부는 두 번째 매개값에 따라 달라짐|
|NevigableSet< E >|subSet (<br>&nbsp;E fromElement,<br>&nbsp;boolean fromInclusive,<br>&nbsp;E toElement,<br>&nbsp;boolean toInclusive<br>)|시작과 끝으로 주어진 객체 사이의 객체들을 NevigableSet<br>으로 리턴. 시작과 끝 객체의 포함 여부는 두 번째, 네 번째<br>매개값에 따라 달라짐|

#### 예제 - subSet()

```java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        TreeSet<String> treeSet = new TreeSet<>();
        treeSet.add("apple");
        treeSet.add("forever");
        treeSet.add("description");
        treeSet.add("ever");
        treeSet.add("zoo");
        treeSet.add("base");
        treeSet.add("guess");
        treeSet.add("cherry");

        System.out.println("[c~f 사이의 단어 검색]");
        NavigableSet<String> rangeSet = treeSet.subSet("c", true, "f", true);
        for (String word : rangeSet) {
            System.out.println(word);
        }
    }
}
```

<br>

### TreeMap

```java
TreeMap<K, V> treeMap = new TreeMap<K, V>();
```

TreeMap에 객체를 저장하면 부모 키값과 비교해서 낮은 것은 왼쪽 자식 노드, 높은 것은 오른쪽 자식 노드에 Map.Entry 객체가 자동으로 정렬됩니다.

#### 검색 관련 메소드
|리턴 타입|메소드|설명|
|---|---|---|
|Map.Entry<K, V>|firstEntry()|제일 낮은 Map.Entry를 리턴|
|Map.Entry<K, V>|lastEntry()|제일 높은 Map.Entry를 리턴|
|Map.Entry<K, V>|lowerEntry(K key)|주어진 키보다 바로 아래 Map.Entry를 리턴|
|Map.Entry<K, V>|higherEntry(K key)|주어진 키보다 바로 위 Map.Entry를 리턴|
|Map.Entry<K, V>|floorEntry(K key)|주어진 키와 동등한 키가 있으면 해당 Map.Entry를 리턴<br>없다면 주어진 키 바로 아래의 Map.Entry를 리턴|
|Map.Entry<K, V>|ceilingEntry(K key)|주어진 키와 동등한 키가 있으면 해당 Map.Entry를 리턴<br>없다면 주어진 키 바로 위의 Map.Entry를 리턴|
|Map.Entry<K, V>|pollFirstEntry()|제일 낮은 Map.Entry를 꺼내오고 컬렉션에서 제거|
|Map.Entry<K, V>|pollLastEntry()|제일 높은 Map.Entry를 꺼내오고 컬렉션에서 제거|

#### 정렬 관련 메소드

|리턴 타입|메소드|설명|
|---|---|---|
|NavigableSet< K >|descendingKeySet()|내림차순으로 정렬된 키의 NavigableSet을 리턴|
|NavigableMap<K, V>|descendingMap()|내림차순으로 정렬된 Map.Entry의 NavigableMap을 리턴|

#### 범위 검색 관련 메소드

|리턴 타입|메소드|설명|
|---|---|---|
|NevigableMap< E >|headMap (<br>&nbsp;K toKey,<br>&nbsp;boolean inclusive<br>)|주어진 키보다 낮은 Map.Entry들을 NavigableMap으로 리턴<br>주어진 키의 Map.Entry 포함 여부는 두 번째 매개값에 따라 달라짐|
|NevigableMap< E >|tailMap (<br>&nbsp;K fromKey,<br>&nbsp;boolean inclusive<br>)|주어진 키보다 높은 Map.Entry들을 NavigableMap으로 리턴<br>주어진 키의 Map.Entry 포함 여부는 두 번째 매개값에 따라 달라짐|
|NevigableMap< E >|subMap (<br>&nbsp;K fromKey,<br>&nbsp;boolean fromInclusive,<br>&nbsp;K toKey,<br>&nbsp;boolean toInclusive<br>)|시작과 끝으로 주어진 키 사이의 Map.Entry들을 NevigableMap<br>컬렉션으로 반환. 시작과 끝 키의 Map.Entry 포함 여부는 두 번째,<br>네 번째 매개값에 따라 달라짐|

<br>

### Comparable과 Comparator
TreeSet과 TreeMap은 정렬을 위해 java.lang.Comparable을 구현한 객체를 요구합니다.

> Integer, Double, String은 모두 Comparable 인터페이스를 구현하고 있음

그래서 사용자 정의 클래스도 Comparable을 구현하면 자동 정렬이 가능하게 됩니다. Comparable에는 `compareTo()` 메소드가 정의되어 있는데, 다음과 같이 리턴값을 만들도록 재정의해야 합니다.

|리턴 타입|메소드|설명|
|---|---|---|
|int|compareTo(T o)|주어진 객체와 같으면 0을 리턴<br>주어진 객체보다 적으면 음수를 리턴<br>주어진 객체보다 크면 양수를 리턴|

TreeSet의 객체와 TreeMap의 키가 Comparable을 구현하고 있지 않으면 ClassCastException이 발생합니다. Comparable 비구현 객체를 정렬하려면 생성자의 매개값으로 정렬자`Comparator`를 제공하는 방법이 있습니다.

```java
TreeSet<E> treeSet = new TreeSet<E>(new AscendingComparator());
TreeMap<K, V> treeMap = new TreeMap<K, V>(new DescendingComparator());
```

정렬자는 Comparator 인터페이스를 구현한 객체를 의미하고, Comparator 인터페이스에는 다음과 같이 메소드가 정의되어 있습니다.

|리턴 타입|메소드|설명|
|---|---|---|
|int|compare(T o1, T o2)|o1과 o2가 동등하다면 0을 리턴<br>o1이 o2보다 앞에 오게 하려면 음수를 리턴<br>o1이 o2보다 뒤에 오게 하려면 양수를 리턴|

<br>

## LIFO와 FIFO 컬렉션
컬렉션 프레임워크에는 LIFO 자료구조를 제공하는 스택`Stack` 클래스와 FIFO 자료구조를 제공하는 큐`Queue` 인터페이스를 제공합니다.

![stack&queue](https://velog.velcdn.com/images/kid/post/5b7b5703-aceb-4c53-b70e-4d329b983dd7/image.png)

- 스택을 응용한 대표적인 예: JVM 스택 메모리
- 큐를 응용한 대표적인 예: 스레드풀의 작업 큐

<br>

### Stack

```java
Stack<E> stack = new Stack<E>();
```

#### 주요 메소드

|리턴 타입|메소드|설명|
|---|---|---|
|E|push(E item)|주어진 객체를 스택에 넣음|
|E|peek()|스택의 맨 위 객체를 가져옴 (객체 제거 X)|
|E|pop()|스택의 맨 위 객체를 가져옴 (객체 제거 O)|

#### 에제

```java
import java.util.*;

class Coin {
	private int value;
    
    public Coin(int value) {
    	this.value = value;
    }
    
    public int getValue() {
    	return value;
    }
}

public class Main {
	public static void main(String[] args) {
    	Stack<Coin> coinBox = new Stack<>();
        
        coinBox.push(new Coin(100));
        coinBox.push(new Coin(50));
        coinBox.push(new Coin(500));
        coinBox.push(new Coin(10));
        
        while (!coinBox.isEmpty()) {
        	Coin coin = coinBox.pop();
            System.out.println("꺼내온 동전: " + coin.getValue() + "원");
        }
    }
}
```

<br>

### Queue

- Queue 인터페이스를 구현한 대표적인 클래스는 LinkedList

```java
Queue<E> queue = new LinkedList<E>();
```

#### 주요 메소드

|리턴 타입|메소드|설명|
|---|---|---|
|boolean|offer(E e)|주어진 객체를 넣음|
|E|peek()|객체 하나 가져옴 (객체 제거 X)|
|E|poll()|객체 하나 가져옴 (객체 제거 O)|

#### 예제

```java
import java.util.*;

class Message {
    public String command;
    public String to;

    public Message(String command, String to) {
        this.command = command;
        this.to = to;
    }
}

public class Main {
    public static void main(String[] args) {
        Queue<Message> messageQueue = new LinkedList<>();

        messageQueue.offer(new Message("sendMail", "홍길동"));
        messageQueue.offer(new Message("sendSMS", "김자바"));
        messageQueue.offer(new Message("sendKakaotalk", "아무개"));

        while (!messageQueue.isEmpty()) {
            Message message = messageQueue.poll();
            switch (message.command) {
                case "sendMail":
                    System.out.println(message.to + "님에게 메일을 보냅니다.");
                    break;
                case "sendSMS":
                    System.out.println(message.to + "님에게 SMS를 보냅니다.");
                    break;
                case "sendKakaotalk":
                    System.out.println(message.to + "님에게 카카오톡을 보냅니다.");
                    break;
            }
        }
    }
}
```

<br>

## 동기화된 컬렉션

- Vector, Hashtable은 동기화된 메소드로 구성되어 있어서 멀티 스레드 환경에서 안전
- ArrayList, HashSet, HashMap은 안전하지 않음

경우에 따라서 ArrayList, HashSet, HashMap을 싱글 스레드 환경에서 사용하다가 멀티 스레드 환경으로 전달할 필요가 있을텐데, 이런 경우 Collections의 `synchronizedXXX()` 메소드를 사용해서 비동기화된 컬렉션을 동기화된 메소드로 래핑할 수 있습니다.

|리턴 타입|메소드(매개 변수)|설명|
|---|---|---|
|List< T >|synchronizedList(List< T > list)|List를 동기화된 List로 리턴|
|Map<K, V>|synchronizedMap(Map<K, V> m)|Map을 동기화된 Map으로 리턴|
|Set< T >|synchronizedSet(Set< T > s)|Set을 동기화된 Set으로 리턴|

```java
// ArrayList를 동기화된 List로 변환
List<T> list = Collections.synchronizedList(new ArrayList<T>());

// HashMap을 동기화된 Map으로 변환
Map<K, V> map = Collections.synchronizedMap(new HashMap<K, V>());

// HashSet을 동기화된 Set으로 변환
Set<E> set = Collections.synchronizedSet(new HashSet<E>());
```

<br>

## 병렬 처리를 위한 컬렉션
자바는 멀티 스레드가 컬렉션의 요소를 병렬적으로 처리할 수 있도록 java.util.concurrent 패키지의 ConcurrentHashMap, ConcurrentLinkedQueue 컬렉션을 제공합니다.

```java
Map<K, V> map = new ConcurrentHashMap<K, V>();
Queue<E> queue = new ConcurrentLinkedQueue<E>();
```

ConcurrentHashMap은 부분`segment` 잠금을 사용합니다.

> 부분 잠금: 스레드가 처리하는 요소가 포함된 부분만 잠금하고 나머지 부분은 다른 스레드가 변경할 수 있도록 하는 것

ConcurrentLinkedQueue는 락-프리`lock-free` 알고리즘을 구현한 컬렉션입니다.

> 락-프리 알고리즘: 여러 개의 스레드가 동시에 접근할 경우, 잠금을 사용하지 않고도 최소한 하나의 스레드가 안전하게 요소를 저장하거나 얻도록 해줌

<br>

## 레퍼런스
- 이것이 자바다: 신용권의 Java 프로그래밍 정복
- Java Collection Framework: https://medium.com/@logishudson0218/java-collection-framework-896a6496b14a
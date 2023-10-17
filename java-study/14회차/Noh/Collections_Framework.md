# 컬렉션 프레임웍(Collections Framework)
* '데이터 군(群)을 저장하는 클래스들을 표준화한 설계'를 뜻한다
* 컬렉션(collection)은 다수의 데이터, 즉 데이터 그룹을 프레임웍은 표준화된 프로그래밍 방식을 의미한다
  * Java API문서에서는 컬렉션 프레임웍을 '데이터 군(Group)을 다루고 표현하기 위한 단일화된 구조(architecture)'라고 정의하고 있다
## 컬렉션 프레임웍의 핵심 인터페이스
* 컬렉션 프레임웍에서는 컬렉션데이터 그룹을 크게 3가지 타입이 존재한다고 인식하고 각 컬렉션을 다루는데 필요한 기능을 가진 3개의 인터페이스를 정의하였다
  * 그리고 인터페이스 List와 Set의 공통된 부분을 다시 뽑아서 새로운 인터페이스인 Collectionㅇ르 추가로 정의하였다
<br>  
<img width="500" alt="image" src="https://github.com/nohheeyeon/TIL/assets/130336617/dfdaa6ce-7180-41a1-803c-9b5757529324"> <br>
[컬렉션 프레임웍의 핵심 인터페이스간의 상속 계층도]

* 인터페이스 List와 Set를 구현한 컬렉션 클래스들은 서로 많은 공통부분이 있어서, 공통된 부분을 다시 뽑아 Collection인터페이스를 정의할 수 있었지만 Map인터페이스는 이들과는 전혀 다른 형태로 컬렉션을 다루기 때문에 같은 상속계층도에 포함되지 못했다

**List 인터페이스:**

| 특징                  | 설명                                                                                      |
|-----------------------|-------------------------------------------------------------------------------------------|
| 데이터 순서           | 순서가 있어서 인덱스를 사용하여 데이터를 저장하고 검색합니다.                           |
| 데이터 중복 허용      | 데이터 중복을 허용합니다.                                                               |
| 구현 클래스 예시     | ArrayList, LinkedList, Vector 등                                                        |

**Set 인터페이스:**

| 특징                  | 설명                                                                                      |
|-----------------------|-------------------------------------------------------------------------------------------|
| 데이터 순서           | 순서가 없어서 인덱스로 관리되지 않습니다.                                              |
| 데이터 중복 불허      | 데이터 중복을 허용하지 않습니다. 모든 요소가 유일해야 합니다.                         |
| 구현 클래스 예시     | HashSet, TreeSet, LinkedHashSet 등                                                      |
**Map 인터페이스:**

| 특징                  | 설명                                                                                      |
|-----------------------|-------------------------------------------------------------------------------------------|
| 키-값 쌍             | 키-값(key-value) 쌍으로 데이터를 저장하고 검색합니다.                                |
| 유일한 키             | 키는 유일해야 하며, 각 키에 대한 값이 저장됩니다.                                    |
| 구현 클래스 예시     | HashMap, TreeMap, HashTable, LinkedHashMap 등                                         |

* 키(Key)란, 데이터 집합 중에서 어떤 값(Value)을 찾는데 열쇠(Key)가 된다는 의미에서 붙여진 이름이다
  * 그래서 키(Key)는 중복을 허용하지 않는다
* 컬렉션 프레임웍의 모든 컬렉션 클래스들은 List, Set, Map 중의 하나를 구현하고 있으며, 구현한 인터페이스의 이름이 클래스의 이름에 포함되어있어서 이름만으로도 클래스의 특징을 쉽게 알 수 있도록 되어있다

### Collection인터페이스
* List와 Set의 조상인 Collection인터페이스에 정의되어있는 메서드

| 메서드                          | 설명                                           |
|--------------------------------|------------------------------------------------|
| `boolean add(E e)`              | 요소를 컬렉션에 추가합니다.                   |
| `boolean addAll(Collection<? extends E> c)` | 다른 컬렉션의 모든 요소를 현재 컬렉션에 추가합니다. |
| `void clear()`                   | 컬렉션의 모든 요소를 제거합니다.             |
| `boolean contains(Object o)`     | 지정된 요소가 컬렉션에 포함되어 있는지 확인합니다. |
| `boolean containsAll(Collection<?> c)` | 지정된 컬렉션의 모든 요소가 현재 컬렉션에 포함되어 있는지 확인합니다. |
| `boolean isEmpty()`              | 컬렉션이 비어 있는지 확인합니다.              |
| `Iterator<E> iterator()`         | 컬렉션을 반복하는 데 사용할 수 있는 `Iterator` 객체를 반환합니다. |
| `boolean remove(Object o)`       | 지정된 요소를 컬렉션에서 제거합니다.          |
| `boolean removeAll(Collection<?> c)` | 지정된 컬렉션의 모든 요소를 컬렉션에서 제거합니다. |
| `boolean retainAll(Collection<?> c)` | 컬렉션의 요소 중에서 지정된 컬렉션의 요소만을 보존하고 나머지 요소를 제거합니다. |
| `int size()`                    | 컬렉션의 요소 수를 반환합니다.               |
| `Object[] toArray()`            | 컬렉션의 모든 요소를 배열로 반환합니다.     |
| `<T> T[] toArray(T[] a)`        | 컬렉션의 모든 요소를 지정된 배열에 저장하고 해당 배열을 반환합니다. |

* Collection인터페이스는 컬렉션 클래스에 저장된 데이터를 읽고, 추가하고 삭제하는 등 컬렉션을 다루는데 가장 기본적인 메서드들을 정의하고 있다
  * 위의 표에서 반환 타입이 boolean인 메서드들은 작업을 성공하거나 사실이면 true를, 그렇지 않으면 false를 반환한다

### List인터페이스
* List인터페이스는 중복을 허용하면서 저장순서가 유지되는 컬렉션을 구현하는데 사용된다
  <br>
<img width="400" alt="image" src="https://github.com/nohheeyeon/TIL/assets/130336617/7b13102e-b9c6-4e1a-8526-d0e42b2a5e32"> <br>
[List의 상속계층도]

* List인터페이스에 정의된 메서드

| 메서드                          | 설명                                           |
|--------------------------------|------------------------------------------------|
| `boolean add(E e)`              | 요소를 리스트에 추가합니다.                   |
| `void add(int index, E element)` | 지정된 위치에 요소를 추가합니다.               |
| `boolean addAll(Collection<? extends E> c)` | 다른 컬렉션의 모든 요소를 리스트에 추가합니다. |
| `boolean addAll(int index, Collection<? extends E> c)` | 다른 컬렉션의 모든 요소를 지정된 위치에 추가합니다. |
| `void clear()`                   | 리스트의 모든 요소를 제거합니다.             |
| `boolean contains(Object o)`     | 지정된 요소가 리스트에 포함되어 있는지 확인합니다. |
| `boolean containsAll(Collection<?> c)` | 지정된 컬렉션의 모든 요소가 리스트에 포함되어 있는지 확인합니다. |
| `boolean equals(Object o)`        | 다른 객체와 리스트가 동일한지 확인합니다.     |
| `E get(int index)`                | 지정된 인덱스의 요소를 반환합니다.            |
| `int hashCode()`                 | 리스트의 해시 코드를 반환합니다.             |
| `int indexOf(Object o)`           | 지정된 요소의 첫 번째 등장 인덱스를 반환합니다. |
| `boolean isEmpty()`              | 리스트가 비어 있는지 확인합니다.              |
| `Iterator<E> iterator()`         | 리스트를 반복하는 데 사용할 수 있는 `Iterator` 객체를 반환합니다. |
| `int lastIndexOf(Object o)`       | 지정된 요소의 마지막 등장 인덱스를 반환합니다. |
| `ListIterator<E> listIterator()`  | 리스트를 앞뒤 양방향으로 반복하는 데 사용할 수 있는 `ListIterator` 객체를 반환합니다. |
| `ListIterator<E> listIterator(int index)` | 지정된 인덱스에서 시작하여 리스트를 앞뒤 양방향으로 반복하는 데 사용할 수 있는 `ListIterator` 객체를 반환합니다. |
| `E remove(int index)`            | 지정된 인덱스의 요소를 제거하고 그 요소를 반환합니다. |
| `boolean remove(Object o)`       | 지정된 요소를 리스트에서 제거합니다.          |
| `boolean removeAll(Collection<?> c)` | 지정된 컬렉션의 모든 요소를 리스트에서 제거합니다. |
| `default boolean removeIf(Predicate<? super E> filter)` | 지정된 조건을 만족하는 요소를 리스트에서 제거합니다. |
| `default void replaceAll(UnaryOperator<E> operator)` | 모든 요소에 대해 주어진 연산자를 적용합니다. |
| `E set(int index, E element)`    | 지정된 인덱스의 요소를 새로운 요소로 대체하고 이전 요소를 반환합니다. |
| `int size()`                    | 리스트의 요소 수를 반환합니다.               |
| `default void sort(Comparator<? super E> c)` | 요소를 지정된 순서로 정렬합니다. |
| `default Spliterator<E> spliterator()` | 리스트를 분할하는 데 사용할 수 있는 `Spliterator` 객체를 반환합니다. |
| `List<E> subList(int fromIndex, int toIndex)` | 지정된 범위의 요소로 구성된 부분 리스트를 반환합니다. |
| `Object[] toArray()`            | 리스트의 모든 요소를 배열로 반환합니다.     |
| `<T> T[] toArray(T[] a)`        | 리스트의 모든 요소를 지정된 배열에 저장하고 해당 배열을 반환합니다. |

### Set인터페이스
* Set인터페이스는 중복을 허용하지 않고 저장순서가 유지되지 않는 컬렉션 클래스를 구현하는데 사용된다
  * Set인터페이스를 구현한 클래스로는 HashSet, TreeSet 등이 있다
<img width="214" alt="image" src="https://github.com/nohheeyeon/TIL/assets/130336617/f1ffdd15-7694-4149-aeaa-6d6363a57bca"> <br>
[Set의 상속계층도]

* Set인터페이스에 정의된 메서드

| 메서드                            | 설명                                                   |
|----------------------------------|--------------------------------------------------------|
| `boolean add(E e)`               | 요소를 집합에 추가합니다.                             |
| `boolean addAll(Collection<? extends E> c)` | 다른 컬렉션의 모든 요소를 집합에 추가합니다. |
| `void clear()`                   | 집합의 모든 요소를 제거합니다.                      |
| `boolean contains(Object o)`     | 지정된 요소가 집합에 포함되어 있는지 확인합니다.   |
| `boolean containsAll(Collection<?> c)` | 지정된 컬렉션의 모든 요소가 집합에 포함되어 있는지 확인합니다. |
| `boolean equals(Object o)`        | 다른 객체와 집합이 동일한지 확인합니다.             |
| `int hashCode()`                 | 집합의 해시 코드를 반환합니다.                      |
| `boolean isEmpty()`              | 집합이 비어 있는지 확인합니다.                       |
| `Iterator<E> iterator()`         | 집합을 반복하는 데 사용할 수 있는 `Iterator` 객체를 반환합니다. |
| `boolean remove(Object o)`       | 지정된 요소를 집합에서 제거합니다.                   |
| `boolean removeAll(Collection<?> c)` | 지정된 컬렉션의 모든 요소를 집합에서 제거합니다.  |
| `boolean retainAll(Collection<?> c)` | 지정된 컬렉션과 공통된 요소만 남기고 다른 요소는 제거합니다. |
| `int size()`                     | 집합의 요소 수를 반환합니다.                         |
| `Object[] toArray()`             | 집합의 모든 요소를 배열로 반환합니다.                |
| `<T> T[] toArray(T[] a)`         | 집합의 모든 요소를 지정된 배열에 저장하고 해당 배열을 반환합니다. |

### Map인터페이스
* Map인터페이스는 키(key)와 값(value)을 하나의 쌍으로 묶어서 저장하는 컬렉션 클래스를 구현하는데 사용된다
  * 키는 중복될 수 없지만 값을 중복을 허용한다
    * 기존에 저장된 데이터와 중복된 키와 값을 저장하면 기존의 값은 없어지고 마지막에 저장된 값이 남게 된다
* Map인터페이스를 구현한 클래스로는 HashTable, HashMap, LinkedHashMap, SortedMap, TreeMap 등이 있다
  * Map이란 개념은 어떤 두 값을 연결한다는 의미에서 붙여진 이름이다

* Map인터페이스의 메서드

| 메서드                                          | 설명                                                                |
|------------------------------------------------|---------------------------------------------------------------------|
| `void clear()`                                  | 맵의 모든 키-값 매핑을 제거합니다.                                |
| `boolean containsKey(Object key)`               | 지정된 키가 맵에 포함되어 있는지 확인합니다.                       |
| `boolean containsValue(Object value)`           | 지정된 값이 맵에 포함되어 있는지 확인합니다.                       |
| `Set<Map.Entry<K, V>> entrySet()`                | 맵의 키-값 매핑을 포함하는 `Set` 뷰를 반환합니다.                  |
| `boolean equals(Object o)`                      | 다른 객체와 맵이 동일한지 확인합니다.                              |
| `V get(Object key)`                            | 지정된 키에 해당하는 값을 반환합니다.                              |
| `int hashCode()`                               | 맵의 해시 코드를 반환합니다.                                        |
| `boolean isEmpty()`                            | 맵이 비어 있는지 확인합니다.                                       |
| `Set<K> keySet()`                              | 맵의 키를 포함하는 `Set` 뷰를 반환합니다.                          |
| `V put(K key, V value)`                        | 지정된 키와 값을 맵에 추가하거나 기존 매핑의 값을 대체합니다.       |
| `void putAll(Map<? extends K, ? extends V> m)` | 다른 맵의 모든 키-값 매핑을 이 맵에 추가합니다.                  |
| `V remove(Object key)`                         | 지정된 키와 연결된 값을 제거합니다.                               |
| `int size()`                                   | 맵의 키-값 매핑 수를 반환합니다.                                   |
| `Collection<V> values()`                       | 맵의 값들을 포함하는 `Collection` 뷰를 반환합니다.                |

* values()에서는 반환타입이 Collection이고, keySet()에서는 반환타입이 Set인 것에 주목!
  *  Map인터페이스에서 값(value)은 중복을 허용하기 때문에 Collection타입으로 반환하고, 키(key)는 중복을 허용하지 않기 때문에 Set타입으로 반환한다

## ArrayList
* ArrayList는 List인터페이스를 구현하기 때문에 데이터의 저장순서가 유지되고 중복을 허용한다는 특징을 갖는다
* ArrayList는 기존의 Vector를 개선한 것으로 Vector와 구현원리와 기능적인 측면에서  동일하다고 할 수 있다
* ArrayList는 Object배열을 이용해서 데이터를 순차적으로 저장한다
  * 배열에 더 이상 저장할 공간이 없으면 보다 큰 새로운 배열을 생성해서 기존의 배열에 저장된 내용을 새로운 배열로 복사한 다음에 저장된다

```java
import java.util.AbstractList;
import java.util.RandomAccess;

public class ArrayList extends AbstractList
        implements List, RandomAccess, Cloneable, java.io.Serializable {
  ...
        transient Object[] elementData; // Object배열
}
```
* transient는 직렬화(serialization)와 관련된 제어자이다
* ArrayList는 elementData라는 이름의 Object배열을 멤버변수로 선언하고 있다는 것을 알 수 있다
  * 선언된 배열의 타입이 모든 객체의 최고조상은 Object이기 때문에 모든 종류의 객체를 담을 수 있다

## LinkedList
* 배열은 가장 기본적인 형태의 자료구조로 구조가 간단하며 사용하기 쉽고 데이터를 읽어 오는데 걸리는 시간(접근시간, access time)이 가장 빠르다는 장점을 가지고 있다
* 단점
```java
1. 크기를 변경할 수 없다
- 크기를 변경할 수 없으므로 새로운 배열을 생성해서 데이터를 복사해야한다
- 실행속도를 향상시키기 위해서는 충분히 큰 크기의 배열을 생성해야 하므로 메모리가 낭비된다

2. 비순차적인 데이터의 추가 또는 삭제에 시간이 많이 걸린다
- 차례대로 데이터를 추가하고 마지막에서부터 데이터를 삭제하는 것은 빠르지만,
- 배열의 중간에 데이터를 추가하려면, 빈자리를 만들기 위해 다른 데이터들을 복사해서 이동해야 한다
```
* 이러한 배열의 단점을 보완하기 위해서 LinkedList라는 자료구조가 고안되었다
  * 배열은 모든 데이터가 연속적으로 존재하지만 링크드 리스트는 불연속적으로 존재하는 데이터를 서로 연결(link)한 형태로 구성되어 있다
<img width="457" alt="image" src="https://github.com/nohheeyeon/TIL/assets/130336617/7f1d263d-efb8-4275-a6ac-36674ab8619a">
* 링크드 리스트의 각 요소(node)들은 자신과 연결된 다음 요소에 대한 참조(주소값)와 데이터로 구성되어 있다
```java
class Node {
    Node next; // 다음 요소의 주소를 저장
    Object obj; // 데이터를 저장
}
```

### Stack과 Queue

#### Stack
* Stack은 후입선출(LIFO, Last-In-First-Out) 구조를 가진 자료구조이다
* 데이터를 스택의 맨 위에 추가하고, 맨 위에서 데이터를 꺼내는 것을 제공한다

```java
import java.util.Stack;

public class StackExample {
    public static void main(String[] args) {
        Stack<String> stack = new Stack<>();
        stack.push("One");
        stack.push("Two");
        stack.push("Three");

        while (!stack.isEmpty()) {
            System.out.println(stack.pop());
        }
    }
}
```

#### Queue
* Queue는 선입선출(FIFO, First-In-First-Out) 구조를 가진 자료구조이다
* 데이터를 큐의 뒤쪽에 추가하고, 앞에서부터 데이터를 꺼내는 것을 제공한다

```java
import java.util.LinkedList;
import java.util.Queue;

public class QueueExample {
    public static void main(String[] args) {
        Queue<String> queue = new LinkedList<>();
        queue.add("One");
        queue.add("Two");
        queue.add("Three");

        while (!queue.isEmpty()) {
            System.out.println(queue.poll());
        }
    }
}
```

### Iterator, ListIterator, Enumeration

#### Iterator
* Iterator는 컬렉션의 요소를 읽고 삭제하는 데 사용되는 인터페이스이다
* Iterator를 사용하면 컬렉션을 읽을 때 안전하게 요소를 열거할 수 있다

```java
import java.util.ArrayList;
import java.util.Iterator;
import java.util.List;

public class IteratorExample {
    public static void main(String[] args) {
        List<String> list = new ArrayList<>();
        list.add("Apple");
        list.add("Banana");
        list.add("Orange");

        Iterator<String> iterator = list.iterator();
        while (iterator.hasNext()) {
            String fruit = iterator.next();
            System.out.println(fruit);
        }
    }
}
```

#### ListIterator
* ListIterator는 List 인터페이스에서 제공되며, 양방향으로 컬렉션을 순회하고 수정할 수 있습니다

```java
import java.util.ArrayList;
import java.util.List;
import java.util.ListIterator;

public class ListIteratorExample {
    public static void main(String[] args) {
        List<String> list = new ArrayList<>();
        list.add("One");
        list.add("Two");
        list.add("Three");

        ListIterator<String> listIterator = list.listIterator();
        while (listIterator.hasNext()) {
            System.out.println(listIterator.next());
        }
        while (listIterator.hasPrevious()) {
            System.out.println(listIterator.previous());
        }
    }
}
```

#### Enumeration
* Enumeration은 구식이지만 여전히 많은 레거시 코드에서 사용됩니다
  * 이것은 컬렉션을 열거하고 읽는 데 사용됩니다

```java
import java.util.Enumeration;
import java.util.Vector;

public class EnumerationExample {
    public static void main(String[] args) {
        Vector<String> vector = new Vector<>();
        vector.add("One");
        vector.add("Two");
        vector.add("Three");

        Enumeration<String> enumeration = vector.elements();
        while (enumeration.hasMoreElements()) {
            System.out.println(enumeration.nextElement());
        }
    }
}
```

### Arrays

* `java.util.Arrays` 클래스는 배열과 관련된 여러 유용한 메서드를 제공합니다
  * 배열을 정렬하고, 검색하고, 복사하는 등 다양한 작업을 수행할 수 있습니다

```java
import java.util.Arrays;

public class ArraysExample {
    public static void main(String[] args) {
        int[] numbers = {3, 1, 4, 1, 5, 9, 2, 6, 5, 3, 5};

        // 배열 정렬
        Arrays.sort(numbers);

        // 배열 검색
        int index = Arrays.binarySearch(numbers, 4);
        System.out.println("Index of 4: " + index);

        // 배열 복사
        int[] copy = Arrays.copyOf(numbers, 7);
        System.out.println("Copied Array: " + Arrays.toString(copy));
    }
}
```

### Comparator와 Comparable
* Comparator와 Comparable은 객체 비교에 사용되는 인터페이스입니다
* Comparable: 객체가 자연스러운 순서를 갖도록 할 때 사용하는 인터페이스로, 객체 자신에게 구현됩니다
* Comparator: 객체 간 비교 규칙을 지정할 때 사용하는 인터페이스로, 별도의 클래스로 구현합니다
  * 객체 간 비교 방식을 변경하거나 여러 비교 기준을 정의할 수 있습니다
```java
class Student implements Comparable<Student> {
    private int id;
    private String name;

    public Student(int id, String name) {
        this.id = id;
        this.name = name;
    }

    public int getId() {
        return id;
    }

    public String getName() {
        return name;
    }

    @Override
    public int compareTo(Student otherStudent) {
        return Integer.compare(this.id, otherStudent.id);
    }

    @Override
    public String toString() {
        return "Student{" +
                "id=" + id +
                ", name='" + name + '\'' +
                '}';
    }
}

public class ComparatorExample {
    public static void main(String[] args) {
        List<Student> students = new ArrayList<>();
        students.add(new Student(3, "Alice"));
        students.add(new Student(1, "Bob"));
        students.add(new Student(2, "Charlie"));

        // 정렬 기준을 제공하는 Comparator를 사용하여 정렬
        Comparator<Student> nameComparator = Comparator.comparing(Student::getName);
        Collections.sort(students, nameComparator);

        for (Student student : students) {
            System.out.println(student);
        }
    }
}
```

* Student 클래스는 Comparable을 구현하여 id를 기준으로 정렬
  * ComparatorExample에서는 이름을 기준으로 정렬하도록 설정

### HashSet, TreeSet, HashMap, Hashtable, TreeMap

#### HashSet
* HashSet은 중복을 허용하지 않고, 순서를 보장하지 않는 Set 컬렉션입니다
* 해시 기반으로 요소를 저장하기 때문에 빠른 검색 시간을 제공합니다
```java
import java.util.HashSet;
import java.util.Set;

public class HashSetExample {
    public static void main(String[] args) {
        Set<String> set = new HashSet<>();
        set.add("Apple");
        set.add("Banana");
        set.add("Orange");

        for (String fruit : set) {
            System.out.println(fruit);
        }
    }
}
```
#### TreeSet
* TreeSet은 중복을 허용하지 않고, 정렬된 순서를 가지는 Set 컬렉션입니다
* 이진 검색 트리 구조로 요소를 저장하므로 정렬된 상태로 유지됩니다
```java
import java.util.TreeSet;
import java.util.Set;

public class TreeSetExample {
    public static void main(String[] args) {
        Set<String> set = new TreeSet<>();
        set.add("Banana");
        set.add("Orange");
        set.add("Apple");

        for (String fruit : set) {
            System.out.println(fruit);
        }
    }
}
```
#### HashMap
* HashMap은 해시 테이블을 기반으로 하며, 키-값(key-value) 쌍을 저장하는 맵 컬렉션입니다 
* 순서를 보장하지 않으며, 중복된 키를 허용하지 않습니다
```java
import java.util.HashMap;
import java.util.Map;

public class HashMapExample {
    public static void main(String[] args) {
        Map<String, Integer> map = new HashMap<>();
        map.put("Alice", 25);
        map.put("Bob", 30);
        map.put("Charlie", 22);

        System.out.println(map.get("Bob"));
    }
}
```

#### Hashtable
* Hashtable은 HashMap과 유사하지만, 스레드 안전한 버전입니다
* 동기화되기 때문에 멀티 스레드 환경에서 사용될 수 있습니다
```java
import java.util.Hashtable;

public class HashtableExample {
    public static void main(String[] args) {
        // Hashtable 생성
        Hashtable<Integer, String> hashtable = new Hashtable<>();

        // 요소 추가
        hashtable.put(1, "One");
        hashtable.put(2, "Two");
        hashtable.put(3, "Three");

        // 요소 조회
        String value = hashtable.get(2);
        System.out.println("Value at key 2: " + value);

        // 요소 제거
        hashtable.remove(1);

        // 전체 요소 출력
        System.out.println("Hashtable contents: " + hashtable);
    }
}
```
* 'Hashtable'을 생성하고 키-값 쌍을 추가, 조회, 제거하는 방법!
#### TreeMap
* TreeMap은 이진 검색 트리를 기반으로 하며, 키-값(key-value) 쌍을 저장하는 정렬된 맵 컬렉션입니다
* 키에 대한 순서를 기반으로 요소가 정렬됩니다
```java
import java.util.TreeMap;
import java.util.Map;

public class TreeMapExample {
    public static void main(String[] args) {
        Map<String, Integer> map = new TreeMap<>();
        map.put("Bob", 30);
        map.put("Charlie", 22);
        map.put("Alice", 25);

        for (Map.Entry<String, Integer> entry : map.entrySet()) {
            System.out.println(entry.getKey() + ": " + entry.getValue());
        }
    }
}
```

### Properties

* `java.util.Properties` 클래스는 키-값 쌍을 저장하는 데 주로 사용되며, 주로 설정 파일을 읽고 쓰는 데 활용됩니다

```java
import java.util.Properties;

public class PropertiesExample {
    public static void main(String[] args) {
        Properties properties = new Properties();
        properties.setProperty("name", "Alice");
        properties.setProperty("age", "30");

        String name = properties.getProperty("name");
        System.out.println("Name: " + name);
    }
}
```
### Collections

* `java.util.Collections` 클래스에는 컬렉션과 관련된 다양한 유틸리티 메서드가 포함되어 있으며, 컬렉션을 조작하고 관리하는 데 유용합니다

- **`sort` 메서드**: 컬렉션 요소를 정렬합니다

```java
import java.util.ArrayList;
import java.util.Collections;
import java.util.List;

public class CollectionsExample {
    public static void main(String[] args) {
        List<String> list = new ArrayList<>();
        list.add("Banana");
        list.add("Orange");
        list.add("Apple");

        Collections.sort(list);
        System.out.println(list);
    }
}
```

- **`reverse` 메서드**: 컬렉션 요소의 순서를 뒤집습니다

```java
import java.util.ArrayList;
import java.util.Collections;
import java.util.List;

public class CollectionsExample {
    public static void main(String[] args) {
        List<String> list = new ArrayList<>();
        list.add("Banana");
        list.add("Orange");
        list.add("Apple");

        Collections.reverse(list);
        System.out.println(list);
    }
}
```

- **`shuffle` 메서드**: 컬렉션 요소를 무작위로 섞습니다

```java
import java.util.ArrayList;
import java.util.Collections;
import java.util.List;

public class CollectionsExample {
    public static void main(String[] args) {
        List<String> list = new ArrayList<>();
        list.add("Banana");
        list.add("Orange");
        list.add("Apple");

        Collections.shuffle(list);
        System.out.println(list);
    }
}
```

### 컬렉션 클래스 정리 & 요약

* Java 컬렉션 프레임워크는 다양한 컬렉션 타입과 관련 클래스를 제공합니다

* 몇 가지 주요 컬렉션 인터페이스와 클래스를 요약한 표

| 인터페이스/클래스 | 특징 |
|--------------------|------|
| Collection | 모든 컬렉션 클래스의 부모 인터페이스 |
| List | 순서가 있는 컬렉션, 중복 요소 허용 |
| ArrayList | List 인터페이스 구현, 동적 배열 |
| LinkedList | List 인터페이스 구현, 이중 연결 리스트 |
| Set | 중복 요소 허용하지 않는 컬렉션 |
| HashSet | Set 인터페이스 구현, 해시 테이블 |
| TreeSet | Set 인터페이스 구현, 이진 검색 트리 |
| Map | 키-값 쌍을 저장하는 컬렉션 |
| HashMap | Map 인터페이스 구현, 해시맵 |
| TreeMap | Map 인터페이스 구현, 정렬된 맵 |
| Queue | 선입선출(FIFO) 구조의 컬렉션 |
| PriorityQueue | Queue 인터페이스 구현, 우선순위 큐 |

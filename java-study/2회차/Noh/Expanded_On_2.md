### 1. 카멜 케이스와 스네이크 케이스

- **카멜 케이스 (Camel Case):**
    - 카멜 케이스는 식별자의 이름을 작성할 때 첫 단어를 소문자로 시작하고, 이후 단어의 첫 글자를 대문자로 작성하는 방식입니다.
    - 주로 메서드명, 변수명, 필드명 등에 사용됩니다.

```java
int myVariableName;
void calculateTotalPrice() { /*...*/ }
```

- **스네이크 케이스 (Snake Case):**
    - 스네이크 케이스는 단어를 모두 소문자로 작성하고 단어 사이를 언더스코어(`_`)로 구분하는 방식입니다.
    - 주로 상수명에 사용됩니다.

```java
final int MAX_VALUE = 100;
final double PI_VALUE = 3.14;
```

### 2. Final 변수

- `final` 키워드로 선언된 변수는 값을 한 번 할당하면 변경할 수 없는 상수가 됩니다. 이것은 변수에 할당된 값을 보호하고 수정을 방지하는 데 사용됩니다.

```java
final int MAX_VALUE = 100;
```

### 3. 변수의 생존 기간

- 변수의 생존 기간은 변수의 범위(scope)에 따라 달라집니다.
    - **지역 변수 (Local Variable):** 선언된 블록 내에서만 존재하며 블록을 빠져나가면 소멸합니다.

```java
void myMethod() {
    int localVar = 42; // 지역 변수
} // localVar는 메서드 블록을 빠져나가면 소멸
```

- **인스턴스 변수 (Instance Variable):** 객체의 생명 주기와 동일하게 존재하며 객체가 소멸할 때 함께 소멸합니다.

```java
class MyClass {
    int instanceVar = 42; // 인스턴스 변수
}
```

### 4. 업캐스팅/다운캐스팅

- **업캐스팅 (Upcasting):** 하위 클래스의 객체를 상위 클래스의 참조 변수에 저장하는 것을 말합니다. 이는 묵시적 형변환이 일어납니다.

```java
class Animal { }
class Dog extends Animal { }

Animal myAnimal = new Dog(); // 업캐스팅
```

- **다운캐스팅 (Downcasting):** 상위 클래스의 참조 변수를 하위 클래스의 타입으로 변환하는 것을 말합니다. 명시적 형변환이 필요합니다.

```java
Animal myAnimal = new Dog();
Dog myDog = (Dog) myAnimal; // 다운캐스팅
```

### 5. char 값 할당과 공백

- `char` 타입의 변수에는 문자 뿐만 아니라 공백 문자도 할당할 수 있습니다.

```java
char spaceChar = ' '; // 공백 할당
```

### 6. 유니코드 확인

- `char` 변수에 할당된 문자의 유니코드 값을 확인하려면 `(int)` 캐스팅을 사용할 수 있습니다.

```java
char character = 'A';
int unicode = (int) character; // 'A'의 유니코드 값 (65)을 얻음
```

### 7. 형변환과 정밀도 손실

- 형변환 시 데이터의 손실이 발생할 수 있으며, 이를 방지하기 위해서는 데이터의 범위를 고려하고 적절한 형변환을 수행해야 합니다. 정밀도 손실을 피하기 위해 실수형 형변환에 주의해야 합니다.

### 8. main() 메서드

- Java 프로그램은 실행을 시작할 클래스에 하나의 `main()` 메서드만 있어야 합니다. 중복된 `main()` 메서드를 작성할 수 없습니다.

### 9. var 키워드

- Java 10부터 도입된 `var` 키워드는 지역 변수의 자료형을 자동으로 추론하는 데 사용됩니다.

```java
var number = 42; // int로 추론됨
```

### 10. Scanner 객체 닫기

- `Scanner` 객체를 사용한 후에는 `close()` 메서드를 호출하여 자원을 해제하는 것이 좋습니다.

```java
Scanner scanner = new Scanner(System.in);
// 작업 수행
scanner.close(); // Scanner 객체 닫기
```

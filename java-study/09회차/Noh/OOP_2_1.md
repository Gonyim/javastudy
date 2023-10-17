 # 객체지향 프로그래밍
 
## 캡슐화와 접근 제어자
* 클래스나 멤버, 주로 멤버에 접근제어자를 사용하는 이유는 클래스의 내부에 선언된 데이터를 보호하기 위해서이다
  * 데이터가 유효한 값을 유지하도록, 또는 비밀번호와 같은 데이터를 외부에서 함부로 변경하지 못하도록 하기 위해서는 외부로부터의 접근을 제한하는 것이 필요하다
    * 이 것을 데이터 감추기(data hiding)라고 하며, 객체지향개념의 캡슐화(encapsulation)에 해당하는 내용이다
* 클래스 내에서만 사용되는, 내부 작업을 위해 임시로 사용되는 멤버변수나 부분작업을 처리하기 위한 메서드 등의 멤버들을 클래스 내부에 감추기 위해서이다
* 외부에서 접근할 필요가 없는 멤버들을 prinvate으로 지정하여 외부에 노출시키지 않음으로써 복잡성을 줄일 수 있다
  * 이 것 역시 캡슐화에 해당한다
```java
접근 제어자를 사용하는 이유
- 외부로부터 데이터를 보호하기 위해서
- 외부에는 불필요한, 내부적으로만 사용되는, 부분을 감추기 위해서
```
* 시간을 표시하기 위한 클래스 Time
```java
public class Time {
    public int hour;
    public int minute;
    public int second;
}
```
* 이 클래스의 인스턴스를 생성한 다음, 멤버변수에 직접 접근하여 값을 변경할 수 있을 것이다
```java
        Time t = new Time();
        t.hour = 25; // 멤버변수에 직접 접근
```

## 다형성
* 여러 가지 형태를 가질 수 있는 능력
  * 자바에서는 한 타입의 참조변수로 여러 타입의 객체를 참조할 수 있도록 함으로써 다형성을 프로그램적으로 구현하였다
    * 조상클래스 타입의 참조변수로 자손클래스의 인스턴스를 참조할 수 있도록 하였다는 것이다

**다형성의 핵심** 조상 타입의 참조변수를 사용하여 다양한 자손 클래스의 객체를 다룰 수 있습니다
```java
class Animal {
    void sound() {
        System.out.println("동물 소리를 내다.");
    }
}

class Dog extends Animal {
    @Override
    void sound() {
        System.out.println("개가 짖습니다.");
    }

    void fetch() {
        System.out.println("개가 물건을 가지고 옵니다.");
    }
}

class Cat extends Animal {
    @Override
    void sound() {
        System.out.println("고양이가 야옹 소리를 내다.");
    }
}

public class PolymorphismExample {
    public static void main(String[] args) {
        Animal myPet; // 조상 타입의 참조변수

        myPet = new Dog(); // Dog 객체를 Animal 참조변수로 참조
        myPet.sound(); // "개가 짖습니다." 출력

        myPet = new Cat(); // Cat 객체를 Animal 참조변수로 참조
        myPet.sound(); // "고양이가 야옹 소리를 내다." 출력

        // myPet.fetch(); // 에러! Animal 타입으로는 fetch 메서드에 접근 불가
    }
}

```

* myPet은 Animal 타입의 참조변수
  * 이 참조변수로 Dog 클래스와 Cat 클래스의 객체를 차례로 참조하고 있음
    * 이렇게 조상 타입의 참조변수를 사용하면, 다형성을 활용하여 다양한 객체를 관리할 수 있음

* myPet이 Dog 객체를 참조할 때 myPet.sound()를 호출하면 Dog 클래스의 sound 메서드가 실행됨
* myPet이 Cat 객체를 참조할 때 myPet.sound()를 호출하면 Cat 클래스의 sound 메서드가 실행됨
  * myPet은 Animal 타입으로 선언되었기 때문에 fetch 메서드에 접근할 수 없습니다.
```java
조상타입의 참조변수로 자손타입의 인스턴스를 참조할 수 있다
반대로 자손타입의 참조변수로 조상타입의 인스턴스를 참조할 수는 없다
```

### 참조변수의 형변화
* 기본형 변수와 같이 참조변수도 형변환이 가능하다
  * 단, 서로 상속관계에 있는 클래스 사이에서만 가능하다
    * 자손타입의 참조변수를 조상타입의 참조변수로, 조상타입의 참조변수를 자손타입의 참조변수로의 형변환만 가능하다
* 기본형 변수의 형변환에서 작은 자료형에서 큰 자료형의 형변환으 생략이 가능하듯이, 참조형 변수의 형변환에서는 자손타입의 참조변수를 조상타입으루 형변환하는 경우에는 형변환을 생략할 수 있다
```java
자손타입 -> 조상타입(Up-casting) : 형변환 생략가능
자손타입 <- 조상타입(Down-casting) : 형변환 생략불가
```
* 참조변수간의 형변환 역시 캐스트연산자를 사용하며, 괄호()안에 변환하고자 하는 타입의 이름(클래스명)을 적어주면된다

### instanceof 연산자
* 참조변수가 참조하고 있는 인스턴스의 실제 타입을 알아보기 위해 instanceof연산자를 사용한다
  * 주로 조건문에 사용되며, instanceof의 왼쪽에는 참조변수를 오른쪽에는 타입(클래스명)이 피연산자로 위치한다
    * 연산의 결과로 boolean값인 true와 false 중의 하나를 반환한다
```java
어떤 타입에 대한 instanceof연산의 결과가 true란느 것은 검사한 타입으로 형변환이 가능하다는 것을 뜻한다
```
```java
class Animal {
    void sound() {
        System.out.println("동물 소리를 내다.");
    }
}

class Dog extends Animal {
    @Override
    void sound() {
        System.out.println("개가 짖습니다.");
    }

    void fetch() {
        System.out.println("개가 물건을 가지고 옵니다.");
    }
}

public class TypeCastingExample {
    public static void main(String[] args) {
        Animal myPet = new Dog(); // Dog 객체를 Animal 참조변수로 참조

        myPet.sound(); // "개가 짖습니다." 출력

        if (myPet instanceof Dog) {
            Dog myDog = (Dog) myPet; // Dog 타입으로 형변환
            myDog.fetch(); // "개가 물건을 가지고 옵니다." 출력
        }
    }
}
```
* myPet이 Animal 타입의 참조변수로 선언되고 Dog 객체를 참조하고 있습니다
  * 다형성을 활용하여 sound() 메서드를 호출합니다
    * myPet이 실제로 Dog 객체를 참조하고 있는지 확인하기 위해 instanceof 연산자를 사용
      * 만약 myPet이 Dog 객체를 참조하고 있다면, Dog 타입으로 형변환하고 fetch() 메서드를 호출

### 참조변수와 인스턴스의 연결
* 참조변수가 어떤 클래스의 인스턴스를 가리키는지를 나타낸다
* 참조변수는 해당 클래스 또는 해당 클래스의 상위 클래스 또는 인터페이스의 인스턴스를 참조할 수 있습니다
  * 이것은 객체 지향 프로그래밍의 "하위 클래스는 상위 클래스의 형태를 띈다"라는 개념과 관련이 있습니다
```java
class Animal {
    void makeSound() {
        System.out.println("동물 소리를 내다.");
    }
}

class Dog extends Animal {
    @Override
    void makeSound() {
        System.out.println("멍멍!");
    }
}

class Cat extends Animal {
    @Override
    void makeSound() {
        System.out.println("야옹!");
    }
}

public class PolymorphismExample {
    public static void main(String[] args) {
        Animal myPet; // Animal 타입의 참조변수 선언

        myPet = new Dog(); // Dog 객체를 참조변수에 할당
        myPet.makeSound(); // "멍멍!" 출력

        myPet = new Cat(); // Cat 객체를 참조변수에 할당
        myPet.makeSound(); // "야옹!" 출력
    }
}

```
* myPet 참조변수가 new Dog()로 초기화된 경우 Dog 클래스의 인스턴스를 가리키고, new Cat()으로 초기화된 경우 Cat 클래스의 인스턴스를 가리킨다

### 매개변수의 다형성
* 메서드나 함수의 매개변수가 여러 다른 데이터 타입을 받을 수 있는 더 일반적인 형태의 매개변수를 가질 수 있음을 의미
  * 코드의 재사용성과 유연성이 증가하며, 다양한 데이터를 처리할 수 있게 됩니다

```java
1. 동일한 메서드나 함수를 여러 다른 데이터 타입에 대해 사용할 수 있습니다
2. 매개변수로 전달된 객체의 실제 타입에 따라 실행 시간에 해당 메서드나 함수가 다른 동작을 수행할 수 있습니다
3. 코드의 일반성과 재사용성을 높일 수 있습니다
```

* 매개변수의 다형성을 사용하여 `Animal` 타입의 매개변수를 받는 메서드를 만들면, 이 메서드는 `Animal` 타입 또는 그 하위 클래스인 `Dog` 또는 `Cat` 객체를 인수로 받을 수 있습니다
  * 메서드 내에서 해당 객체의 실제 타입을 확인하거나 다양한 작업을 수행할 수 있습니다

```java
class Animal {
    void makeSound() {
        System.out.println("동물 소리를 내다.");
    }
}

class Dog extends Animal {
    @Override
    void makeSound() {
        System.out.println("멍멍!");
    }
}

class Cat extends Animal {
    @Override
    void makeSound() {
        System.out.println("야옹!");
    }
}

public class PolymorphismExample {
    static void performSound(Animal animal) {
        animal.makeSound();
    }

    public static void main(String[] args) {
        Animal myPet = new Dog();
        performSound(myPet); // "멍멍!" 출력

        myPet = new Cat();
        performSound(myPet); // "야옹!" 출력
    }
}
```
* `performSound` 메서드는 `Animal` 타입의 매개변수를 받고 있습니다
  * `Dog`나 `Cat` 객체를 매개변수로 받아 각각의 소리를 출력할 수 있습니다
    * 동일한 메서드를 다양한 타입의 객체에 대해 사용할 수 있어 코드의 재사용성이 향상됩니다

### 여러 종류의 객체를 배열로 다루기
* 다형성(Polymorphism)을 이용하여 여러 클래스의 객체를 하나의 배열에 담아 관리하는 것을 의미한다
  * 조상타입의 참조변수로 자손타입의 객체를 참조하는 것이 가능
```java
class Animal {
    void sound() {
        System.out.println("동물 소리를 냅니다.");
    }
}

class Dog extends Animal {
    void sound() {
        System.out.println("멍멍!");
    }
}

class Cat extends Animal {
    void sound() {
        System.out.println("야옹!");
    }
}

public class Main {
    public static void main(String[] args) {
        // Animal 배열을 생성하고 다양한 동물 객체를 담습니다.
        Animal[] animals = new Animal[3];
        animals[0] = new Dog();
        animals[1] = new Cat();
        animals[2] = new Dog();

        // 배열을 반복하면서 각 동물의 소리를 출력합니다.
        for (Animal animal : animals) {
            animal.sound(); // 다형성을 활용하여 각 객체의 sound 메서드 호출
        }
    }
}

```
* Animal 클래스는 부모 클래스로서 Dog와 Cat 클래스가 상속받고 있습니다
  * 배열 animals는 Animal 타입으로 선언되었지만, 다형성 덕분에 Dog와 Cat 객체를 모두 담을 수 있습니다
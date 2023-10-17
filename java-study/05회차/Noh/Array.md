## 배열(Array)

### 배열이란?
* 배열은 같은 타입의 여러 변수를 하나의 묶음으로 다루는 것
* 무조건 '같은 타입'이여야 한다
  *  서로 다른 타입의 변수들로 구성된 배열은 만들 수 없다
* 변수와 달리 배열은 각 저장공간이 연속적으로 배치되어 있다는 특징이 있다
```java
int socre1, score2, score3, score4, score5 ; // 학생 5명의 점수를 저장
```
```java
int[] score = new int[5]; // 5개의 int 값을 저장할 수 있는 배열을 생성
// 값을 저장할 수 있는 공간은 score[0]부터 score[4]까지 모두 5개
// 변수 score는 배열을 다루는데 필요한 참조변수일 뿐 값을 저장하기 위한 공간은 아니다
```

### 배열의 선언과 생성
* 배열을 선언하는 방법
  * 원하는 타입의 변수를 선언하고 변수 또는 타입에 배열임을 의미하는 대괄호[]를 붙이면 된다
    * 대괄호[]는 타입 뒤에 붙여도 되고 변수이름 뒤에 붙여도 됩니다
```java
// 타입[] 변수이름;
int[] scroe;
String[] name;
// 타입 변수이름[];
int score[];
String name[];
```
#### 배열의 생성
* 배열을 선언한 다음에는 배열을 생성해야한다
* 배열을 선언하는 것은 단지 생성된 배열을 다루기 위한 참조변수를 위한 공간이 만들어질 뿐이고, 배열을 생성해야만 비로소 값을 저장할 수 있는 공간이 만들어지는 것이다
* 배열을 생성하가ㅣ 위해서는 연산자 'new'와 함께 배열의 타입과 길이를 지정해주어야 한다
```java
타입[] 변수이름; // 배열을 선언 (배열을 다루기 위한 참조변수 선언)
변수이름 = new 타입[길이] // 배열을 생성 (실제 저장공간을 생성)
```
* 길이가 5인 int배열
```java
int[] score; // int타입의 배열을 다루기 위한 참조변수 score선언
score = new int[5]; // int타입의 값 5개를 저장할 수 있는 배열
```
* 배열의 선언과 생성을 동시에 하며 간략히 한 줄로 할 수 있다
```java
타입[] 변수이름 = new 타입[길이]; // 배열의 선언과 생성을 동시에
int[] score = new int[5]; // 길이가 5인 int 배열
```
* 배열의 선언과 생성과정을 단계별로
```java
1. int[] score;
// int형 배열 참조변수 score를 선언한다. 데이터를 저장할 수 있는 공간은 아직 마련되지 않았다.
2. score = new int[5];
// 연산자 'new'에 의해서 메모리의 빈 공간에 5개의 int형 데이터를 저장할 수 있는 공간이 마련된다
// -> 각 배열요소는 자동적으로 int의 기본값(default)인 0으로 초기화된다
// -> 대입 연산자 '='에 의해 배열의 주소가 int형 배열 참조변수 score에 저장된다
```
  * 참조변수의 이름을 따서 '배열 score' 라고 부르면 된다
  * 
### 배열의 길이와 인덱스
* 생성된 배열의 각 저장공간을 '배열의 요소(element)'라고 하며, '배열이름[인덱스]'의 형식으로 배열의 요소에 접근한다
  * 인덱스(index)는 배열의 요소마다 붙여진 일련번호로 각 요소를 구별하는데 사용된다
```java
"인덱스(index)의 범위는 0부터 '배열길이-1'까지."
```
-> 길이가 5인 배열은 모두 5개의 요소(저장공간)을 가지며 인덱스의 범위는 1부터 5까지가 아닌 0부터 4까지, 즉 0, 1, 2, 3, 4가 된다
* 배열에 값을 저장하고 읽어오는 방법은 변수와 같다
  * 단지 변수이름 대신 '배열이름[인덱스]'를 사용한다는 점만 다르다

```java
score[3] = 100; // 배열 score의 4번재 요소에 100을 저장한다
int value = score[3]; // 배열 score의 4번재 요소에 저장된 값을 읽어서 value에 저장
```
* index로 상수 대신 변수나 수식도 사용할 수 있다
```java
for (int i=0;i<5;i++) {
    score[i] = i * 10;
        }
```
* -> index로 상수 대신 변수 i를 사용하고, for문으로 변수 i의 값을 0부터 4까지 증가시킨다
  * for문의 제어변수 i는 배열의 index로 사용하기에 딱 알맞아서, 배열을 다룰 때 for문은 거의 필수적이다 

```java
// 만일 괄호[] 안에 수식이 포함된 경우, 이 수식이 먼저 계산된다
// -> 그래야지 배열의 몇 번째 요소인 지 알 수 있기 때문이다
int tmp = score[i+1];
```
ex) score[3]의 값이 100이고, 변수 i의 값이 2일 때
```java
int tmp = score[i+1];
-> int tmp = score[2+1];
-> int tmp = score[3];
-> int tmp = 100;
```
* 배열을 다룰 때 index의 범위를 벗어난 값을 index로 사용하지 않아야 한다는 걸 주의해야 한다
```java
int[] score = new int[5]; // 길이가 5인 int 배열. index의 범위는 0~4
        ...
score[5] = 100; // index의 범위를 벗어난 값을 index로 사용
```
  * 컴파일러는 이런 실수를 걸러주지 못 한다
    *  배열의 index로 변수를 많이 사용하는데, 변수의 값을 실행 시에 대입되므로 컴파일러는 이 값의 범위를 확인할 수 없다
      * 무사히 컴파일을 마쳤더라도 실행 시에 에러가 발생한다 (ArrayIndexOutOfException)

#### 배열의 길이
* 배열의 요소의 개수, 즉 값을 저장할 수 있는 공간의 개수다
* 배열의 길이는 양의 정수여야 하며 최대값은 int타입의 최대값, 약 20억이다
* 길이가 0인 배열도 생성이 가능하다
  * 길이가 0이라는 얘기는 값을 저장할 수 있는 공간이 하나도 없다는 뜻인데, 이런 배열을 생성하는 것이 무슨 의미?!
```java
int[] arr = new int[0]; // 길이가 0인 배열도 생성이 가능하다!
```
```java
1. 반복문 초기화: 길이가 0인 배열은 반복문을 초기화하거나 조건을 검사할 때 사용됩니다. 예를 들어, 특정 조건을 만족하지 않는 경우 반복문을 실행하지 않고 루프를 건너뛰기 위해 길이가 0인 배열을 활용할 수 있습니다.

```java
for (int i = 0; i < array.length; i++) {
    // 어떤 작업 수행
}
```

2. 예외 처리: 길이가 0인 배열은 예외 처리를 단순화할 수 있습니다. 특정 조건에서 배열을 생성하지 않고 빈 배열을 사용하여 예외를 처리할 수 있습니다.

```java
if (condition) {
    throw new MyException("예외 발생");
} else {
    int[] emptyArray = new int[0];
}
```

3. API 호출: 일부 라이브러리 및 API에서 반환 값으로 빈 배열을 사용합니다. 이렇게 하면 특정 조건을 만족하지 않는 경우 빈 결과를 반환할 수 있습니다.

```java
public int[] findNumbers() {
    if (condition) {
        return new int[0]; // 길이가 0인 배열 반환
    } else {
        // 결과 배열 반환
    }
}
```

4. 초기화 작업: 종종 초기에 빈 배열을 생성하고 나중에 필요에 따라 요소를 추가하는 방식으로 작업을 수행할 수 있습니다. 이는 동적으로 데이터를 수집하거나 필터링하는 작업에 유용합니다.

```java
int[] result = new int[0]; // 초기에 빈 배열 생성

for (int number : numbers) {
    if (condition) {
        // 필요한 경우 요소를 추가
    }
}
```

#### 배열이름.length
* 자바에서는 JVM이 모든 배열의 길이를 별도로 관리하며, '배열이름.length'를 통해서 배열의 길이에 대한 정보를 얻을 수 있다
```java
int[] arr = new int[5]; // 길이가 5인 int배열
int tmp = arr.length; // arr.length의 값은 5이고 tmp에 5가 저장된다
// 배열은 한 번 생성하면 길이를 변경할 수 없기 때문에 '배열이름.length'는 상수다 -> 값을 읽을 수 만 있을 뿐 변경할 수 없다
```
* 모든 경우에 배열의 길이를 직접 적어주는 것보다 '배열이름.length'를 사용하는 것이 코드의 관리가 쉽고 에러가 발생할 확률이 적어진다

#### 배열의 길이 변경하기
* 배열은 한 번 선어되고 나면 길이를 변경할 수 없다 <br>
-> 만약 배열에 저장할 공간이 부족하다면? <br>
-> 더 큰 길이의 새로운 배열을 생성한 다음, 기존의 배열에 저장된 값들을 새로운 배열에 복사
* 처음부터 배열의 길이를 넉넉하게 잡아줘서 새로 배열을 생성해야하는 상황이 가능한 적게 발생하도록 해야한다
  * 배열의 길이를 너무 크게 잡으면 메모리를 낭비하게 되므로, 기존의 2배정도의 길이로 생성하는 것이 좋다

### 배열의 초기화
* 배열은 생성과 동시에 자동적으로 자신의 타입에 해당하는 기본값으로 초기화되므로 배열을 사용하기 전에 따로 초기화를 해주지 않아도 되지만, 원하는 값을 저장하려면 각 요소마다 값을 지정해줘야한다
```java
int[] score = new int[5]; // 길이가 5인 int형 배열을 생성
score[0] = 50; // 각 요소에 직접 값을 저장
score[1] = 60;
score[2] = 70;
score[3] = 80;
score[4] = 90;
```
* 배열의 길이가 큰 경우에는 요소 하나하나에 값을 지정하기 보다는 for문을 사용하는 것이 좋다
```java
int[] score = new int[5]; // 길이가 5인 int 형 배열을 생성
for(int i=0;i<score.length;i++)
    score[i = i * 10 + 50;]
```
* 배열의 생성과 초기화를 동시에
```java
int[] score = new int[]{50, 60, 70, 80, 90}
```

#### 배열의 출력
* for문 사용
```java
int[] iArr = {1--, 95, 80, 70, 60};

// 배열의 요소를 순서대로 하나씩 출력
for(int i =0;i<iArr.length;i++) {
    System.out.println(iArr[i]);
        }
```
* 'Arrays.toString(배열이름)'
```java
int[] iArr = {100, 95, 80, 70, 60};
// 배열 iArr의 모든 요소를 출력 [100, 95, 80, 70, 60]
System.out.println(Arrays.toString(iArr));
```
### 배열의 복사
* `System.arraycopy()` 메서드를 사용하거나, 새로운 배열을 만들어 값을 복사할 수 있습니다
* for문 이용
```java
int[] arr = new int[5];
        ...
int tmp = new int[arr.length*2]; // 기존 배열보다 길이가 2배인 배열 생성

for(int i=0;i<arr.length;i++)
    tmp[i] = arr[i]; // arr[i]의 값을 tmp[i]에 저장

arr = tmp; // 참조변수 arr이 새로운 배열을 가리키게 한다
```

#### System.arraycopy()를 이용한 배열의 복사
* for문 대신 System클래스의 arraycopy()를 사용하면 보다 간단하고 빠르게 배열을 복사할 수 있다
* for문은 배열의 요소 하나하나에 접근해서 복사하지만, arraycopy()는 지정된 범위의 값들을 한 번에 통째로 복사한다
  * 각 요소들이 연속적으로 저장되어 있다는 배열의 특성때문에 이렇게 처리하는 것이 가능한 것이다
```java
배열의 복사는 for문보다 System.arraycopy()를 사용하는 것이 효율적이다
```
```java
for(int i=0;i<num.length;i++) {newNum[i]=num[i]};
arraycopy()를 호출할 때는 어느 배열의 몇 번째 요소에서 어느 배열로 몇 번째 요소로 몇 개의 값을 복사할 것인 지 지정해줘야한다
System.arraycopy(num, 0, newNum, 0, num.length);
// num[0]에서 newNum[0]으로 num.length개의 데이터를 복사
```

### 배열의 활용
* 배열은 데이터를 저장, 검색, 정렬 및 필터링하는 데 사용됩니다
* 배열은 다른 자료 구조를 구현하는 데 기반이 되는 중요한 개념입니다
  * 총합과 평균
  * 최대값과 최소값
  * 섞기(shuffle)
  * 임의의 값으로 배열 채우기
    * random()
  * 정렬하기(sort)
  * 빈도수 구하기

## String 배열

### String 배열의 선언과 생성
* `String` 배열은 문자열을 저장하는 데 사용됩니다
* 선언 및 생성 방법은 기본 데이터 유형 배열과 유사합니다
* 참조형 변수의 기본값은 null

```java
String[] names = new String[3]; // 크기가 3인 String 배열 생성
```

+) 타입에 따른 변수의 기본값(default value)

| 데이터 타입       | 기본값           |
| ---------------- | ---------------- |
| byte             | 0                |
| short            | 0                |
| int              | 0                |
| long             | 0L               |
| float            | 0.0f             |
| double           | 0.0              |
| char             | '\u0000' (널 문자) |
| boolean          | false            |
| 참조 타입 (클래스, 배열) | null             |

### String 배열의 초기화
* `String` 배열을 초기화하려면 각 요소에 문자열을 할당하면 됩니다
* int배열과 동일한 방법
```java
String[] name = new String[3]; // 길이가 3인 String 배열을 생성
name[0] = "Kim";
name[1] = "Park";
name[2] = "Noh";
```
* String클래스만 큰따옴표만으로 간략히 표현하는 것이 허용된다
```java
String[] names = new String[]{"Alice", "Bob", "Charlie"}; // 배열 선언 및 초기화
String[] names = {"Alice", "Bob", "Charlie"}; //new String[]을 생략할 수 있음
```

### char 배열과 String 클래스
* `char` 배열은 문자의 배열로, 문자열을 처리하는 데 사용됩니다
* `String` 클래스는 문자열을 다루는 다양한 메서드와 함께 제공되며, 문자열 처리에 편리하게 사용됩니다
* 사실 문자열이라는 용어는 '문자를 연이어 늘어놓은 것'을 의미하므로 문자배열인 char배열과 같은 뜻이다
  * 자바에서 char배열이 아닌 String클래스를 이용해서 문자열을 처리하는 이유는 String클래스가 char배열에 여러가지 기능을 추가하여 확장한 것이기 때문이다
* char배열과 String클래스의 한 가지 중요한 차이는 String객체(문자열)은 읽을 수만 있을 뿐 내용을 변경할 수 없다는 것이다
```java
String str = "java";
str = str + "8"; // "java8" 이라는 새로운 문자열이 str에 저장된다
System.out.println(str); // java8
```
-> 문자열 str의 내용이 변경되는 것 같지만, 문자열은 변경할 수 없으므로 새로운 내용의 문자열이 생성된다

#### String클래스의 주요 메서드

| 메서드                    | 설명                                                  |
| ------------------------- | ----------------------------------------------------- |
| `int length()`            | 문자열의 길이를 반환합니다.                            |
| `char charAt(int index)`  | 지정한 인덱스에 있는 문자를 반환합니다.               |
| `boolean isEmpty()`       | 문자열이 비어 있는지 여부를 확인합니다.              |
| `String substring(int beginIndex)` | 지정한 인덱스부터 끝까지의 부분 문자열을 반환합니다. |
| `String substring(int beginIndex, int endIndex)` | 지정한 범위의 부분 문자열을 반환합니다. |
| `boolean contains(CharSequence sequence)` | 문자열이 지정한 문자열 또는 문자 시퀀스를 포함하는지 여부를 확인합니다. |
| `boolean startsWith(String prefix)` | 문자열이 지정한 접두사로 시작하는지 여부를 확인합니다. |
| `boolean endsWith(String suffix)` | 문자열이 지정한 접미사로 끝나는지 여부를 확인합니다. |
| `int indexOf(String str)` | 지정한 문자열이 처음으로 등장하는 인덱스를 반환합니다. |
| `int lastIndexOf(String str)` | 지정한 문자열이 마지막으로 등장하는 인덱스를 반환합니다. |
| `String replace(char oldChar, char newChar)` | 문자열 내에서 지정한 문자를 다른 문자로 대체합니다. |
| `String toUpperCase()` | 문자열을 대문자로 변환한 새 문자열을 반환합니다. |
| `String toLowerCase()` | 문자열을 소문자로 변환한 새 문자열을 반환합니다. |
| `String trim()` | 문자열의 앞뒤 공백을 제거한 새 문자열을 반환합니다. |
| `String[] split(String regex)` | 정규 표현식을 기반으로 문자열을 분할하여 배열로 반환합니다. |
| `boolean equals(Object obj)` | 다른 객체 또는 문자열과 현재 문자열을 비교하여 동등한지 여부를 확인합니다. |
| `boolean equalsIgnoreCase(String anotherString)` | 대소문자를 무시하고 문자열을 비교하여 동등한지 여부를 확인합니다. |
| `String concat(String str)` | 현재 문자열에 지정한 문자열을 연결한 새 문자열을 반환합니다. |
| `static String valueOf(int value)` | 다양한 데이터 유형을 문자열로 변환합니다. |

* charAt메서드
  * 문자열에서 지정된 index에 있는 한 문자를 가져온다
  * 배열에서 '배열이름[index]'로 index에 위치한 갑ㅈㅅ을 가져오는 것과 같다고 생각하면 된다
  * 배열과 마찬가지로 charAt메서드의 index값은 0부터 시작한다
```java
String str = "ABCDE";
char ch = str.charAt(3); // 문자열 str의 4번째 문자 'D'를 ch에 저장
```

* substing()
  * 문자열의 일부를 뽑아낼 수 있다
  * **범위의 끝은 포함되지 않는다 ex) index의 범위가 1~4라면 4는 범위에 포함되지 않는다**
```java
String str = "012345";
String tmp = str.substring(1,4); // str에서 index범위 1~4 범위 1~4의 문자들을 반환
System.out.println(tmp); // "123"이 출력된다
```

* equal()
  * 문자열의 내용이 같은 지 다른 지 확인하는데 사용된다
  * 기본형 변수의 값을 비교하는 경우 '=='연산자를 사용하지만, 문자열의 내용을 비교할 때는 equals()를 사용해아 한다
  * 이 메서드는 대소문자를 구분한다
    * 대소문자를 구분하지 않고 비교하려면 equals()대신 equalsIgnoreCase()를 사용해야한다
```java
String str = "abc";
if(str.equals("abc")) { // str와 "abc"가 내용이 같은 지 확인한다 
        ...
        }
```

#### char배열과 String클래스의 반환
```java
char[] chArr = {'A', 'B', 'C', 'D'};
String str = new String(chArr); // char배열 -> String
char[] tmp = str.toCharArray(); // String -> char배열
```

### 커맨드 라인을 통해 입력받기
* Scannser클래스의 nextLine() 외에도 화면을 통해 상요자로부터 값을 입력받을 수 있는 간단한 방법임 -> 커맨드라인을 이용한 방법
* 프로그램을 실행할 ㄸ ㅐ클래스 이름 뒤에 공백문자로 구분하여 여러 개의 문자열을 프로그램에 전달할 수 있다
* 만약 실행할 프로그램의 main메서드가 담긴 클래스의 이름이 MainTest라고 가정하면
```java
c:jdk1.8\work\ch5\java MainTest abc 123
// 커맨드라인을 통해 입력된 두 문자열은 String배열에 담겨서 MainTest클래스의 main메서드의 매개변수(args)에 전달된다
```

```java
public class CommandLineInput {
    public static void main(String[] args) {
        for (String arg : args) {
            System.out.println(arg);
        }
    }
}
```

## 다차원 배열 (multi-dimensional)

* 메모리의 용량이 허요하는 한, 차원의 제한은 없다

### 2차원 배열의 선언과 인덱스
* 2차원 배열은 행과 열로 구성되며, 각 요소는 두 개의 인덱스를 사용하여 접근됩니다

| 데이터 유형       | 배열 이름       | 선언 예시                |
| ------------------ | --------------- | ------------------------ |
| 정수형 2차원 배열 | `int[][]`      | `int[][] matrix;`        |
| 문자열 2차원 배열 | `String[][]`   | `String[][] names;`      |
| 실수형 2차원 배열 | `double[][]`   | `double[][] scores;`     |
| 객체형 2차원 배열 | `ClassName[][]` | `Person[][] people;`     |
* 3차원 이상의 고차원 배열의 선언은 대괄호[]의 개수를 차원의 수 만큼 추가해주면 된다
* 2차원 배열은 주로 테이블 형태의 데이터를 담는데 사용되며, 만일 4행 3열의 데이터를 담기 위한 배열을 생성하려면
```java
int[][] score = new int[4][3]; // 4행 3열의 2차원 배열을 생성한다
```

```java
int[][] matrix = new int[3][4]; // 3x4 크기의 2차원 배열 생성
```
| int | int | int |
| --- | --- | --- |
| int | int | int |
| int | int | int |
| int | int | int |

#### 2차원 배열의 index

```java
score[0][0] = 100; // 배열 score의 1행 1열에 100을 저장
System.out.println(score[0][0]); // 배열 score의 1행 1열의 값을 출력
```

### 2차원 배열의 초기화
* 2차원 배열을 초기화하려면 각 요소에 값을 할당하면 됩니다
* 중첩된 `for` 루프를 사용하여 초기화할 수 있습니다

```java
int [][] arr = new int[][]{
        {1,2,3}, 
        {4,5,6}
}
```
```java
for (int i=0;i<score.length;i++) {
    for int j=0;j<score[i].length;j++ {
        score[i][j] = 10;
        }
}
```

### 가변 배열
* 가변 배열은 각 행의 길이가 서로 다른 배열입니다
  -> 이를 통해 다양한 데이터 구조를 모델링할 수 있습니다

```java
int[][] jaggedArray = new int[3][];
jaggedArray[0] = new int[]{1, 2};
jaggedArray[1] = new int[]{3, 4, 5};
jaggedArray[2] = new int[]{6};
```

### 다차원 배열의 활용
* 다차원 배열은 행렬, 이미지, 게임 보드 등 다양한 응용 프로그램에서 사용됩니다
  * 좌표에 X표하기
  * 빙고
  * 행렬의 곱셈
  * 단어 맞추기
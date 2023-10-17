## String 클래스
### String 생성자
자바의 문자열은 `java.lang` 패키지의 String 클래스의 인스턴스로 관리됩니다. 소스상에서 문자열 리터럴은 String 객체로 자동 생성되지만, String 클래스의 다양한 생성자를 이용해서 직접 String 객체를 생성할 수도 있습니다. 어떤 생성자를 이용해서 String 객체를 생성할지는 제공되는 매개값의 타입에 따라 다릅니다.

> String 클래스는 비권장(Deprecated)된 생성자를 제외하고 약 13개의 생성자를 제공합니다.

#### 사용 빈도수가 높은 생성자들

```java
// 배열 전체를 String 객체로 생성
String str = new String(byte[] bytes);
// 지정한 문자셋으로 디코딩
String str = new String(byte[] bytes, String charsetName);

// 배열의 offset 인덱스 위치부터 length만큼 String 객체로 생성
String str = new String(byte[] bytes, int offset, int length);
// 지정한 문자셋으로 디코딩
String str = new String(byte[] bytes, int offset, inf length, String charsetName);
```

#### 예제 - 바이트 배열을 문자열로 변환

```java
public class Main {
	public static void main(String[] args) {
    	byte[] bytes = {72, 101, 108, 108, 111, 32, 74, 97, 118, 97};
        
        String str1 = new String(bytes);
        System.out.println(str1);
        
        String str2 = new String(bytes, 6, 4);
        System.out.println(str2);
    }
}
```

```java
public class Main {
	public static void main(String[] args) {
    	byte[] bytes = new byte[100];
        
        System.out.print("입력: ");
        int readByteNo = System.in.read(bytes);
        
        String str = new String(bytes, 0, readByteNo-2);
        System.out.println(str);
    }
}
```

> System.in.read() 메소드는 키보드에서 입력한 내용을 매개값으로 주어진 바이트 배열에 저장하고 읽은 바이트 수를 리턴합니다.

<br>

### String 메소드
#### 사용 빈도수가 높은 메소드

|리턴 타입|메소드명(매개 변수)|설명|
|---|---|---|
|char|charAt(int index)|특정 위치의 문자 리턴|
|boolean|equals(Object anObject)|두 문자열을 비교|
|byte\[]|getBytes()|byte\[]로 리턴|
|byte\[]|getBytes(Charset charset)|주어진 문자셋으로 인코딩한 byte\[]로 리턴|
|int|indexOf(String str)|문자열 내에서 주어진 문자열의 위치를 리턴|
|int|length()|총 문자의 수를 리턴|
|String|replace(CharSequence target,<br>CharSequence replacement)|target 부분을 replacement로 대치한 새로운 문자열을 리턴|
|String|substring(int beginIndex)|beginIndex 위치에서 끝까지 잘라낸 새로운 문자열을 리턴|
|String|substring(int beginIndex,<br>int endIndex)|beginIndex 위치에서 endIndex 전까지 잘라낸 새로운 문자열을 리턴|
|String|toLowerCase()|알파벳 소문자로 변환한 새로운 문자열을 리턴|
|String|toUpperCase()|알파벳 대문자로 변환한 새로운 문자열을 리턴|
|String|trim()|앞뒤 공백을 제거한 새로운 문자열을 리턴|
|String|valueOf(int i)<br>valueOf(double d)|기본 타입값을 문자열로 리턴|

<br>

#### 문자 추출 charAt()
`charAt()` 메소드는 매개값으로 주어진 인덱스의 문자를 리턴합니다.

```java
Stirng str = "자바 프로그래밍";
char ch = str.charAt(1);
```

#### 문자열 비교 equals()
`equals()`는 Object의 번지 비교 메소드이지만, String 클래스에서는 문자열을 비교하도록 재정의되어 있습니다.

```java
public class Main {
	public static void main(String[] args) {
    	String str1 = new String("김자바");
        String str2 = "김자바";
        
        if (str1 == str2) {
        	System.out.println("같은 String 객체를 참조");
        } else {
        	System.out.println("다른 String 객체를 참조");
        }
        
        if (str1.equals(str2)) {
        	System.out.println("같은 문자열을 가짐");
        } else {
        	System.out.println("다른 문자열을 가짐");
        }
    }
}
```

#### 바이트 배열로 변환 getBytes()
`getBytes()` 메소드는 네트워크로 문자열을 전송하거나, 문자열을 암호화할 때 문자열을 바이트 배열로 변환하기 위해서 사용됩니다. 시스템의 기본 문자셋으로 인코딩된 바이트 배열을 리턴하는데, 특정 문자셋으로 인코딩된 바이트 배열을 얻으려면 두 번째 방법을 사용합니다.

```java
byte[] bytes = "문자열".getBytes();
byte[] bytes = "문자열".getBytes(Charset charset);
```

> getBytes(Charset charset) 메소드는 잘못된 문자셋을 매개값으로 줄 경우 java.lang.UnsupportedEncodingException 예외가 발생하므로 예외 처리가 필요합니다.

#### 문자열 찾기 indexOf()
`indexOf()` 메소드는 매개값으로 주어진 문자열이 시작되는 인덱스를 리턴합니다. 만약 주어진 문자열이 포함되어 있지 않으면 -1을 리턴합니다.

```java
String str = "자바 스터디";
int index = str.indexOf("스터디");
```

#### 문자열 길이 length()
`length()` 메소드는 문자열의 길이(문자의 수)를 리턴합니다.

```java
String str = "자바 프로그래밍";
int length = str.length();
```

#### 문자열 대치 replace()
`replace()` 메소드는 첫 번째 매개값인 문자열을 찾아 두 번째 매개값인 문자열로 대치한 새로운 문자열을 생성하고 리턴합니다.

```java
String oldStr = "자바 스터디";
String newStr = oldStr.replace("스터디", "프로그래밍");
```

> String 객체의 문자열은 변경이 불가한 특성을 갖기 때문에 replace() 메소드가 리턴하는 문자열은 원래 문자열의 수정본이 아니라 완전히 새로운 문자열입니다.

#### 문자열 잘라내기 substring()
`substirng()` 메소드는 주어진 인덱스에서 문자열을 추출합니다. 매개값의 수에 따라서 `substring(int beginIndex)`, `substring(int beginIndex, int endIndex)` 두 가지 형태로 사용됩니다.

```java
String ssn = "880815-1234567";
String firstNum = ssn.substring(0, 6);
String secondNum = ssn.substring(7);
```

#### 알파벳 소/대문자 변경 toLowerCase(), toUpperCase()
`toLowerCase()` 메소드는 문자열을 모두 소문자로 바꾼 새로운 문자열을 생성한 후 리턴하고, `toUpperCase()` 메소드는 문자열을 모두 대문자로 바꾼 새로운 문자열을 생성한 후 리턴합니다.

```java
String og = "Java Programming";
String lowerCase = og.toLowerCase();
String upperCase = og.toUpperCase();
```

> equalsIgnoreCase() 메소드를 사용해서 대소문자 구분없이 문자열 비교 가능

#### 문자열 앞뒤 공백 잘라내기 trim()
`trim()` 메소드는 문자열의 앞뒤 공백을 제거한 새로운 문자열을 생성하고 리턴합니다.

```java
Stinrg oldStr = "    자바    ";
String newStr = oldStr.trim();
```

#### 문자열 변환 valueOf()
`valueOf()` 메소드는 기본 타입의 값을 문자열로 변환하는 기능을 가지고 있습니다. String 클래스에 다음과 같이 오버로딩되어 있기 때문에 가능합니다.

```java
static String valueOf(boolean b)
static String valueOf(char c)
static String valueOf(int i)
static String valueOf(long l)
static String valueOf(double d)
static String valueOf(float f)
```

```java
Stirng str1 = String.valueOf(10);
Stirng str2 = String.valueOf(10.5);
Stirng str3 = String.valueOf(true);
```

<br>

## StringTokenizer 클래스
문자열이 특정 구분자`delimiter`로 연결되어 있을 경우, 구분자를 기준으로 부분 문자열을 분리하기 위해서는 String의 `split()` 메소드를 이용하거나, java.util 패키지의 `StringTokenizer` 클래스를 이용할 수 있습니다. split()은 정규 표헌식으로 구분하고, StringTokenizer는 문자로 구분한다는 차이점이 있습니다.

<br>

### split() 메소드
String 클래스의 `split()` 메소드는 정규 표현식을 구분자로 해서 문자열을 분리한 후, 배열에 저장하고 리턴합니다.

```java
String[] result = "문자열".split("정규표현식");
```

```java
String text = "봄&여름,가을-겨울";
String[] seasons = text.split("&|,|-");
```

<br>

### StringTokenizer 클래스
문자열이 한 종류의 구분자로 연결되어 있을 경우 `StringTokenizer` 클래스를 사용하면 간단하게 문자열`토큰`을 분리해 낼 수 있습니다. 객체를 생성할 때 첫 번째 매개값으로 전체 문자열을 주고, 두 번째 매개값으로 구분자를 줍니다.

```java
StringTokenizer st = new StringTokenizer("문자열", "구분자");
```

```java
String text = "봄/여름/가을/겨울";
StringTokenizer st = new StringTokenizer(text, "/");
```

> 만약 구분자를 생략하면 공백이 기본 구분자가 됩니다.

다음 메소드들을 이용해서 전체 토큰 수, 남아있는 토큰 여부를 확인한 다음, 토큰을 읽습니다.

|메소드||설명|
|---|---|---|
|int|countTokens()|꺼내지 않고 남아있는 토큰의 수|
|boolean|hasMoreTokens()|남아있는 토큰이 있는지 여부|
|String|nextToken()|토큰을 하나씩 꺼내옴|

#### 예제

```java
import java.util.StringTokenizer;

public class Main {
    public static void main(String[] args) {
        String text = "봄 여름 가을 겨울";

        // 1: 전체 토큰 수를 얻어 for문으로 루핑
        StringTokenizer st = new StringTokenizer(text);
        int countTokens = st.countTokens();
        for (int i=0; i<countTokens; i++) {
            String token = st.nextToken();
            System.out.println(token);
        }

        System.out.println();

        // 2: 남아있는 토큰을 확인하고 while문으로 루핑
        st = new StringTokenizer(text);
        while (st.hasMoreTokens()) {
            String token = st.nextToken();
            System.out.println(token);
        }
    }
}
```

<br>

## StringBuffer, StringBuilder 클래스
String은 내부의 문자열을 수정할 수 없습니다. 그래서 문자열을 결합하는 `+` 연산자를 많이 사용하면 할수록 그만큼 String 객체의 수가 늘어나기 때문에 프로그램 성능을 느리게 하는 요인이 됩니다. 문자열을 변경하는 작업이 많을 경우에는 String 클래스를 사용하는 것보다 java.lang 패키지의 `StringBuffer` 또는 `StringBuilder` 클래스를 사용하는 것이 좋습니다.

- 두 클래스는 내부 버퍼`buffer: 데이터를 임시로 저장하는 메모리`에 문자열을 저장해 두고, 그 안에서 추가, 수정, 삭제 작업을 할 수 있도록 설계되어 있음
- 새로운 객체를 만들지 않고 문자열을 조작할 수 있음
- `StringBuffer`는 멀티 스레드 환경에서 사용할 수 있도록 동기화가 적용되어 있어 스레드에 안전함
- `StringBuilder`는 단일 스레드 환경에서만 사용하도록 설계되어 있음

### StringBuilder
StringBuilder 클래스는 몇 가지 생성자를 제공합니다. 기본 생성자인 `StringBuilder()`는 16개의 문자들을 저장할 수 있는 초기 버퍼를 만들고, `StringBuilder(int capacity)` 생성자는 capacity로 주어진 개수만큼 문자들을 저장할 수 있는 초기 버퍼를 만듭니다. StringBuilder는 버퍼가 부족할 경우 자동으로 버퍼 크기를 늘리기 때문에 초기 버퍼의 크기는 크게 중요하지 않습니다. `StringBuilder(String str)` 생성자는 str로 주어진 매개값을 버퍼의 초기값으로 저장합니다.

```java
StringBuilder sb = new StringBuilder();
StringBuilder sb = new StringBuilder(16);
StringBuilder sb = new StringBuilder("Java");
```

객체가 생성되면 다음 메소드를 이용해서 문자 추가, 삭제 등의 작업을 합니다.

|메소드|설명|
|---|---|
|append(...)|문자열 끝에 주어진 매개값을 추가|
|insert(int offset, ...)|문자열 중간에 주어진 매개값을 추가|
|delete(int start, int end)|문자열의 일부분을 삭제|
|deleteCharAt(int index)|문자열에서 주어진 index의 문자를 삭제|
|replace(int start, int end, String str)|문자열의 일부분을 다른 문자열로 대치|
|reverse()|문자열의 순서를 뒤바꿈|
|setCharAt(int index, char ch)|문자열에서 주어진 index의 문자를 다른 문자로 대치|

> append()와 insert() 메소드는 매개 변수가 다양한 타입으로 오버로딩되어 있기 때문에 대부분의 값을 문자로 추가할 수 있습니다.

<br>

## 정규 표현식과 Pattern 클래스
### 정규 표현식 작성 방법

|기호|설명|
|---|---|
|\[]|한 개의 문자<br>\[abc] - a, b, c 중 하나의 문자<br>\[^abc] - a, b, c 이외의 하나의 문자<br>\[a-zA-Z] - a~z, A~Z 중 하나의 문자|
|\\d|한 개의 숫자, \[0-9]와 동일|
|\\s|공백|
|\\w|한 개의 알파벳 또는 한 개의 숫자, \[a-zA-Z_0-9]와 동일|
|?|없음 또는 한 개|
|\*|없음 또는 한 개 이상|
|+|한 개 이상|
|{n}|정확히 n개|
|{n,}|최소한 n개|
|{n, m}|n개부터 m개까지|
|()|그룹핑|


#### 전화번호, 이메일 정규 표현식

```
(02|010)-\d{3,4}-\d{4}
\w+@\w+\.\w+(\.\w+)?
```

<br>

### Pattern 클래스
정규 표현식으로 문자열을 검증할 때 java.util.regex.Pattern 클래스의 정적 메소드인 `matches()` 메소드를 사용합니다.

```java
boolean result = Pattern.matches("정규식", "검증할 문자열");
```

#### 예제

```java
public class Main {
	public static void main(String[] args) {
    	String regExp = "(02|010)-\d{3,4}-\d{4}";
        String data = "010-123-4567";
        boolean result = Pattern.matches(regExp, data);
        if (result) {
        	System.out.println("정규식과 일치합니다.");
        } else {
        	System.out.println("정규식과 일치하지 않습니다.");
        }
        
        regExp = "\w+@\w+\.\w+(\.\w+)?";
        data = "java@navercom";
        result = Pattern.matches(regExp, data);
        if (result) {
        	System.out.println("정규식과 일치합니다.");
        } else {
        	System.out.println("정규식과 일치하지 않습니다.");
        }
    }
}
```

<br>

## Arrays 클래스
Arrays 클래스는 배열 조작`배열의 복사, 항목 정렬, 항목 검색 등` 기능을 가지고 있습니다.

|리턴 타입|메소드 이름|설명|
|---|---|---|
|int|binarySearch(배열, 찾는값)|전체 배열 항목에서 찾는 값이 있는 인덱스 리턴|
|타겟 배열|copyOf(원본배열, 복사할길이)|원본 배열의 0번 인덱스에서 복사할 길이만큼 복사한 배열 리턴, 복사할 길이는 원본 배열의 길이보다 커도 되며, 타겟 배열의 길이가 됨|
|타겟 배열|copyOfRange(원본배열, 시작인덱스, 끝인덱스)|원본 배열의 시작 인덱스에서 끝 인덱스까지 복사한 배열 리턴|
|boolean|deepEquals(배열, 배열)|두 배열의 깊은 비교(중첩 배열의 항목까지 비교)|
|boolean|equals(배열, 배열)|두 배열의 얕은 비교(중첩 배열의 항목은 비교하지 않음)|
|void|fill(배열, 값)|전체 배열 항목에 동일한 값을 저장|
|void|fill(배열, 시작인데스, 끝인덱스, 값)|시작 인덱스부터 끝 인덱스까지의 항목에만 동일한 값을 저장|
|void|sort(배열)|배열의 전체 항목을 오름차순으로 정렬|
|String|toString(배열)|"\[값1, 값2, ...]"와 같은 문자열 리턴|

<br>

### 배열 복사
#### 예제 - Arrays와 System.arraycopy()

```java
public class Main {
	public static void main(String[] args) {
    	char[] arr1 = {'J', 'A', 'V', 'A'};
        
        // 방법 1:
        char[] arr2 = Arrays.copyOf(arr1, arr1.length); // arr1 전체를 arr2로 복사
        System.out.println(Arrays.toString(arr2));
        
        // 방법 2:
        char[] arr3 = Arrays.coptOfRange(arr1, 1, 3) // arr[1]~[2]를 arr3[0]~[1]로 복사
        System.out.println(Arrays.toString(arr3));
        
        // 방법 3:
        char[] arr4 = new char[arr1.length];
        System.arraycopy(arr1, 0, arr4, 0, arr1.length); // arr1 전체를 arr4로 복사
        System.out.println(Arrays.toString(arr4));
    }
}
```

<br>

### 배열 항목 비교
#### 예제

```java
import java.util.Arrays;

public class Main {
    public static void main(String[] args) {
        int[][] og = {{1,2}, {3,4}};

        // 얕은 복사 후 비교
        int[][] cloned1 = Arrays.copyOf(og, og.length);
        System.out.println("배열 번지 비교: " + og.equals(cloned1));
        System.out.println("1차 배열 항목값 비교: " + Arrays.equals(og, cloned1));
        System.out.println("중첩 배열 항목값 비교: " + Arrays.deepEquals(og, cloned1));

        System.out.println();

        // 깊은 복사 후 비교
        int[][] cloned2 = Arrays.copyOf(og, og.length);
        cloned2[0] = Arrays.copyOf(og[0], og[0].length);
        cloned2[1] = Arrays.copyOf(og[1], og[1].length);
        System.out.println("배열 번지 비교: " + og.equals(cloned2));
        System.out.println("1차 배열 항목값 비교: " + Arrays.equals(og, cloned2));
        System.out.println("중첩 배열 항목값 비교: " + Arrays.deepEquals(og, cloned2));
    }
}
```

<br>

### 배열 항목 정렬
기본 타입 또는 String 배열은 `Arrays.sort()` 메소드의 매개값으로 지정해주면 자동으로 오름차순으로 정렬이 되지만, 사용자 정의 클래스 타입일 경우에는 클래스가 Comparable 인터페이스를 구현하고 있어야 정렬이 됩니다.

#### 예제

```java
import java.util.Arrays;

class Member implements Comparable<Member> {
    String name;
    Member(String name) {
        this.name = name;
    }
    @Override
    public int compareTo(Member o) {
        return name.compareTo(o.name);
    }
}

public class Main {
    public static void main(String[] args) {
        int[] scores = {99, 97, 98};
        Arrays.sort(scores);
        for (int i=0; i<scores.length; i++) {
            System.out.println("scores[" + i + "]=" + scores[i]);
        }
        System.out.println();

        String[] names = {"홍길동", "아무개", "김자바"};
        Arrays.sort(names);
        for (int i=0; i<names.length; i++) {
            System.out.println("names[" + i + "]=" + names[i]);
        }
        System.out.println();

        Member m1 = new Member("홍길동");
        Member m2 = new Member("아무개");
        Member m3 = new Member("김자바");
        Member[] members = {m1, m2, m3};
        Arrays.sort(members);
        for (int i=0; i<members.length; i++) {
            System.out.println("members[" + i + "].name=" + members[i].name);
        }
    }
}
```

<br>

### 배열 항목 검색
배열 검색은 특정 값이 위치한 인덱스를 얻는 것입니다. 배열 항목을 검색하려면 `Arrays.sort()` 메소드로 항목들을 정렬한 후, `Arrays.binarySearch()` 메소드로 항목을 찾아야 합니다.

<br>

## 포장(Wrapper) 클래스
자바는 기본 타입의 값을 갖는 객체를 생성할 수 있습니다. 기본 타입의 값을 내부에 두고 포장하기 때문에 포장 객체라고 부릅니다. 포장하고 있는 기본 타입 값은 외부에서 변경할 수 없는 것이 특징입니다. 내부의 값을 변경하고 싶다면 새로운 객체를 만들어야 합니다.

|기본 타입|포장 클래스|
|---|---|
|byte|Byte|
|char|Character|
|short|Short|
|int|Integer|
|long|Long|
|float|Float|
|double|Double|
|boolean|Boolean|

<br>

### 박싱과 언박싱 Boxing, Unboxing

- 박싱: 기본 타입의 값을 포장 객체로 만드는 과정
- 언박싱: 포장 객체에서 기본 타입의 값을 얻어내는 과정

#### 박싱

```java
// 생성자 O
Integer obj = new Integer(100);

// 생성자 X
Integer obj = Integer.valueOf(100);
```

#### 언박싱
"기본타입명+Value()" 메소드를 호출하면 됩니다.

```java
int value = obj.intValue();
```

<br>

### 자동 박싱과 언박싱

- 자동 박싱: 포장 클래스 타입에 기본값이 대입될 경우 발생
	- int 타입의 값을 Integer 클래스 변수에 대입하면 자동 박싱이 일어나 힙 영역에 Integer 객체 생성

```java
Integer obj = 100;
```

- 자동 언박싱: 기본 타입에 포장 객체가 대입될 경우 발생
	- Integer 객체를 int 타입 변수에 대입하거나, Integer 객체와 int 타입값을 연산하면 Integer 객체로부터 int 타입의 값이 자동 언박싱되어 연산됨

```java
Integer obj = new Integer(100);
int value1 = obj;
int value2 = obj + 100;
```

<br>

### 문자열을 기본 타입 값으로 변환
포장 클래스의 주요 용도는 기본 타입의 값을 박싱해서 포장 객체로 만드는 것이지만, 문자열을 기본 타입 값으로 변환할 때에도 많이 사용됩니다. 대부분의 포장 클래스에는 `parse+기본타입` 명으로 되어있는 정적 메소드가 있는데, 이 메소드는 문자열을 매개값으로 받아 기본 타입 값으로 변환합니다.

#### 예제

```java
public class Main {
	public static void main(String[] args) {
    	int value1 = Integer.parseInt("10");
        double value2 = Double.parseDouble("3.14");
        boolean value3 = Boolean.parseBoolean("true");
        
        System.out.println("value1: " + value1);
        System.out.println("value2: " + value2);
        System.out.println("value3: " + value3);
    }
}
```

<br>

### 포장 값 비교

|타입|값의 범위|
|---|---|
|boolean|true, false|
|char|\u0000 ~ \u007f|
|byte, short, int|-128 ~ 127|

박싱된 값이 위의 표에 나와있는 값이라면 `==`와 `!=` 연산자로 내부의 값을 바로 비교할 수 있습니다. 그 외의 경우에는 박싱된 값을 비교하기 위해 `equals()` 메소드로 내부 값을 비교하거나, 직접 내부 값을 언박싱해서 비교해야 합니다.

> 포장 객체에 정확히 어떤 값이 저장될지 모르는 상황이라면 ==와 != 연산자는 사용하지 않는 것이 좋습니다.

<br>

## Math, Random 클래스
### Math 클래스

|메소드|설명|예제 코드|리턴값|
|---|---|---|---|
|int abs(int a)<br>double abs(double a)|절대값|int v1 = Math.abs(-5);<br>double v2 = Math.abs(-3.14)|v1 = 5<br>v2 = 3.14|
|double ceil(double a)|올림값|double v1 = Math.ceil(5.3);<br>double v2 = Math.ceil(-5.3);|v1 = 6.0<br>v2 = -5.0|
|double floor(double a)|버림값|double v1 = Math.floor(5.3);<br>double v2 = Math.floor(-5.3);|v1 = 5.0<br>v2 = -6.0|
|int max(int a, int b)<br>double max(double a, double b)|최대값|int v1 = Math.max(5, 9);<br>double v2 = Math.max(5.3, 2.5);|v1 = 9<br>v2 = 5.3|
|int min(int a, int b)<br>double min(double a, double b)|최소값|int v1 = Math.min(5, 9);<br>double v2 = Math.min(5.3, 2.5);|v1 = 5<br>v2 = 2.5|
|double random()|랜덤값|double v1 = Math.random(); |0.0<=v1<1.0|
|double rint(double a)|가까운 정수의 실수값|double v1 = Math.rint(5.3);<br>double v2 = Math.rint(5.7);|v1 = 5.0<br>v2 = 6.0|
|long round(double a)|반올림값|long v1 = Math.round(5.3);<br>long v2 = Math.round(5.7);|v1 = 5<br>v2 = 6|

<br>

### Random 클래스
Random 클래스를 이용하면 boolean, int, long, float, double 타입의 난수를 얻을 수 있습니다. 난수를 만드는 알고리즘에 사용되는 종자값을 설정해서 종자값이 같다면 같은 난수를 얻도록 만들 수도 있습니다.

|생성자|설명|
|---|---|
|Random()|호출 시마다 다른 종자값(현재시간 이용)이 자동 설정됨|
|Random(long seed)|매개값으로 주어진 종자값이 설정됨|

|리턴값|메소드(매개 변수)|설명|
|---|---|---|
|boolean|nextBoolean()|boolean 타입의 난수를 리턴|
|double|nextDouble()|double 타입의 난수를 리턴(0.0 <= ~ < 1.0)|
|int|nextInt()|int 타입의 난수를 리턴(-2^31 <= ~ < 2^31-1)|
|int|nextInt(int n)|int 타입의 난수를 리턴(0 <= ~ < n)|

```java
// Math 클래스를 사용한 로또 번호 뽑기
int num = (int) (Math.random() * 45) + 1;

// Random 클래스를 사용한 로또 번호 뽑기
Random random = new Random();
int num = random.nextInt(45) + 1;
```

<br>

## Data, Calendar 클래스
### Date 클래스
Date 클래스는 객체 간에 날짜 정보를 주고 받을 때 주로 사용되고, `Date()` 생성자는 컴퓨터의 현재 날짜를 읽어 Date 객체로 만듭니다.

```java
Date now = new Date();
```

특정 문자열 포맷으로 날짜 정보를 얻고 싶다면 `java.text.SimpleDateFormat` 클래스를 이용합니다.

```java
Date now = new Date();
SimpleDateFormat sdf = new SimpleDateFormat("yyyy년 MM월 dd일");
String strNow = sdf.format(now);
```

<br>

### Calendar 클래스
Calendar 클래스는 추상 클래스이므로 new 연산자를 사용해서 인스턴스를 생성할 수 없습니다.

> 날짜와 시간을 계산하는 방법이 지역과 문화, 나라에 따라 다르기 때문

Calendar 클래스의 정적 메소드인 `getInstance()` 메소드를 이용하면 현재 운영체제에 설정되어 있는 시간대를 기준으로 한 Calendar 하위 객체를 얻을 수 있습니다.

```java
Calendar now = Calendar.getInstance();

// get() 메소드를 이용해서 날짜와 시간에 대한 정보 얻기
// 매개값은 Calendar 클래스에 선언되어 있는 상수
int year = now.get(Calendar.YEAR);
int month = now.get(Calendar.MONTH) + 1;
int day = now.get(Calendar.DAY_OF_MONTH);
int week = now.get(Calendar.DAY_OF_WEEK);
int amPm = now.get(Calendar.AM_PM);
int hour = now.get(Calendar.HOUR);
int minute = now.get(Calendar.MINUTE);
int second = now.get(Calendar.SECOND);
```

Calendar 클래스에 오버로딩된 다른 getInstance() 메소드를 이용해서 다른 시간대의 Calendar를 얻을 수도 있습니다.

```java
TimeZone timeZone = TimeZone.getTimeZone("America/Los_Angeles");
Calendar now = Calendar.getInstance(timeZone);
```

> String 배열로 리턴되는 TimeZone.getAvailableIDs() 메소드를 호출해서 시간대 문자열 목록을 확인할 수 있습니다.

<br>

## Format 클래스
형식 클래스는 java.text 패키지에 포함되어 있고, 숫자 형식을 위해 `DecimalFormat`, 날짜 형식을 위해 `SimpleDateFormat`, 매개 변수화된 문자열 형식을 위해 `MessageFormat` 등을 제공합니다.

<br>

### 숫자 형식 클래스 DecimalFormat

![DecimalFormat](https://velog.velcdn.com/images/kid/post/3b80b93c-f655-43cd-bc8a-f2259a961377/image.png)

```java
DecimalFormat df = new DecimalFormat("#,###.0");
String result = df.format(1234567.89);
```

<br>

### 날짜 형식 클래스 SimpleDateFormat

![SimpleDateFormat](https://velog.velcdn.com/images/kid/post/163ff41d-c27f-4567-88ba-6217b68681ec/image.png)

```java
SimpleDateFormat sdf = new SimpleDateFormat("yyyy년 MM월 dd일");
String strDate = sdf.format(new Date());
```

<br>

### 문자열 형식 클래스 MessageFormat
MessageFormat 클래스를 사용하면 문자열에 데이터가 들어갈 자리를 표시해 두고, 프로그램이 실행하면서 동적으로 데이터를 삽입해 문자열을 완성시킬 수 있습니다.

#### 예제 - 매개 변수화된 문자열 형식

```java
import java.text.MessageFormat;

public class Main {
    public static void main(String[] args) {
        String id = "java";
        String name = "신용권";
        String tel = "010-1234-5678";

        String text = "회원 ID: {0} \n회원 이름: {1} \n회원 전화: {2}";
        String result1 = MessageFormat.format(text, id, name, tel);
        System.out.println(result1);
        System.out.println();

        String sql = "insert into member values({0}, {1}, {2})";
        Object[] arguments = {"'java'", "'신용권'", "'010-1234-5678'"};
        String result2 = MessageFormat.format(sql, arguments);
        System.out.println(result2);
    }
}
```

<br>

## java.time 패키지
자바 8부터 날짜와 시간을 나타내는 여러 가지 API를 새롭게 추가했습니다.

|패키지|설명|
|---|---|
|java.time|날짜와 시간을 나타내는 핵심 API인 LocalDate, LocalTime, LocalDateTime, ZonedDateTime을 포함하고 있음. 이 클래스들은 ISO-8601에 정의된 달력 시스템에 기초함|
|java.time.chrono|ISO-8601에 정의된 달력 시스템 이외에 다른 달력 시스템이 필요할 때 사용할 수 있는 API들이 포함되어 있음|
|java.time.format|날짜와 시간을 파싱하고 포맷팅하는 API들이 포함되어 있음|
|java.time.temporal|날짜와 시간을 연산하기 위한 보조 API들이 포함되어 있음|
|java.time.zone|타임존을 지원하는 API들이 포함되어 있음|

<br>

### 날짜와 시간 객체 생성
java.time 패키지에는 다음과 같이 날짜와 시간을 표현하는 5개의 클래스가 있습니다.

|클래스명|설명|
|---|---|
|LocalDate|로컬 날짜 클래스|
|LocalTime|로컬 시간 클래스|
|LocalDateTime|로컬 날짜 및 시간 클래스(LocalDate + LocalTime)|
|ZonedDateTime|특정 타임존(TimeZone)의 날짜와 시간 클래스|
|Instant|특정 시점의 Time-Stamp 클래스|

<br>

#### LocalDate
`now()`는 컴퓨터의 현재 날짜 정보를 저장한 객체를 리턴하고, `of()`는 매개값으로 주어진 날짜 정보를 저장한 객체를 리턴합니다.

```java
LocalDate currDate = LocalDate.now();
LocalDate targetDate = LocalDate.of(int year, int month, int dayOfMonth);
```

#### LocalTime

```java
LocalTime currTime = LocalTime.now();
LocalTime targetTime = LocalTime.of(int hour, int minute, int second, int nanoOfSecond);
```

#### LocalDateTime

```java
LocalDateTime currDateTime = LocalDateTime.now();
LocalDateTime targetDateTime = LocalDateTime.of(int year, int month, int dayOfMonth, int hour, int minute, int second, int nanoOfSecond);
```

#### ZonedDateTime
ISO-8601 달력 시스템에서 정의하고 있는 타임존의 날짜와 시간을 저장하는 클래스입니다.

```java
ZonedDateTime utcDateTime = ZonedDateTime.now(ZoneId.of("UTC"));
ZonedDateTime seoulDateTime = ZonedDateTime.now(ZoneId.of("Asia/Seoul"));
```

#### Instant
날짜와 시간의 정보를 얻거나 조작하는데 사용되지 않고, 특정 시점의 타임스탬프로 사용됩니다. 주로 특정한 두 시점 간의 시간적 우선순위를 따질 때 사용합니다.

```java
Instant instant1 = Instant.now();
Instant instant2 = Instant.now();
if (instant1.isBefore(instant2)) {
	System.out.println("instant1이 빠릅니다.");
} else if (instant1.isAfter(instant2)) {
	System.out.println("instant1이 늦습니다.");
} else {
	System.out.println("동일한 시간입니다.);
}
System.out.println("차이(nanos): " + instant1.until(instant2, ChronoUnit.NANOS));
```

<br>

### 파싱과 포맷팅
날짜와 시간 클래스는 문자열을 파싱`Parsing`해서 날짜와 시간을 생성하는 메소드와 날짜와 시간을 포맷팅`Formatting`된 문자열로 변환하는 메소드를 제공합니다.

<br>

#### 파싱 메소드

|클래스 & 리턴 타입|메소드(매개 변수)|
|---|---|
|LocalDate<br>LocalTime<br>LocalDateTime<br>ZonedDateTime|parse(CharSequence)<br>parse(CharSequence, DateTimeFormatter)|

```java
LocalDate localDate = LocalDate.parse("2023-10-09");
```

![DateTimeFormatter](https://velog.velcdn.com/images/kid/post/80a95f67-9ea9-40a4-ab3a-aabed74fc913/image.png)

#### 포맷팅 메소드

|클래스|리턴 타입|메소드(매개 변수)|
|---|---|---|
|LocalDate<br>LocalTime<br>LocalDateTime<br>ZonedDateTime|String|format(DateTimeFormatter formatter)|

```java
LocalDateTime now = LocalDateTime.now();
DateTimeFormatter dateTimeFormatter = DateTimeFormatter.ofPattern("yyyy년 M월 d일 h시 m분");
String nowStr = now.format(dateTimeFormatter);
```

<br>

## 레퍼런스
- 이것이 자바다: 신용권으로 Java 프로그래밍 정복
- 자바 String / StringBuffer / StringBuilder 차이점 & 성능 비교: https://inpa.tistory.com/entry/JAVA-%E2%98%95-String-StringBuffer-StringBuilder-%EC%B0%A8%EC%9D%B4%EC%A0%90-%EC%84%B1%EB%8A%A5-%EB%B9%84%EA%B5%90
- \[JAVA] Format 클래스: https://jammdev.tistory.com/142
- Java 8 Date Parsing and Formatting with Examples: https://www.javaguides.net/2018/07/java-8-date-parsing-and-formatting-with-examples.html
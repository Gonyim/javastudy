# 날짜와 시간
## Calendar와 Date
* Date는 날짜와 시간을 다룰 목적으로 JDK1.0부터 제공되어온 클래스이다
  * Date클래스의 기능 부족으로 인해 Calendar라는 새로운 클래스를 그 다음 버젼인 JDK1.1부터 제공하기 시작
    * Calendar에서 발견된 몇 가지 단점들로 인해 JDK1.8부터 'java.time패키지'로 기존의 단점들을 개선한 새로운 클래스들이 추가되었다
      * 여기서 말하는 Date클래스는 java.util패키지에 속한 것이다
        * java.sql패키지의 Date클래스와 혼동 X!

### Calendar와 GregorianCalendar
* Calendar는 추상클래스이기 때문에 직접 객체를 생성할 수 없고, 메서드를 통해서 완전히 구현된 클래스의 인스턴스를 얻어야 한다
```java
Calendar cal = new Calendar(); // 에러! 추상클래스는 인스턴스를 생성할 수 없다
```
```java
Calendar cal = Calendar.getInstance();
// getInstance() 메서드는 Calendar 클래스를 구현한 클래스의 인스턴스를 반환한다
```
* Calendar를 상속받아 완전히 구현한 클래스로는 GregorianCalendar와 BuddhistCalendar가 있는데 getInstance()는 시스템의 국가와 지역설정을 확인해서 태국인 경우에는 BuddhistCalendar의 인스턴스를 반환하고, 그 외에는 GregorianCalendar의 인스턴스를 반환한다
* GregorianCalendar는 Calendar를 상속받아 오늘날 전세계 공통으로 사용하고 있는 그레고리력에 맞게 구현한 것으로 태국을 제외한 나머지 국가에서는 GregorianCalendar를 사용하면 된다
```java
Q. 왜 태국은 안됨? ㅜㅡㅜ

A. 태국은 그레고리력을 사용하지만 다른 국가와는 다른 형식과 규칙을 따르는 경우가 있다
그렇기 때문에 태국에서는 'BuddhistCalendar'클래스를 사용하는 것이 더 적절하다
-> 'BuddhistCalendar'클래스는 태국의 불교 달력에 맞게 날짜와 시간을 처리할 수 있도록 구현되어 있다
```
* 인스턴스를 직접 생성해서 사용하지 않고 이처럼 메서드를 통해서 인스턴스를 반환받게 하는 이유는 최소한의 변경으로 프로그램이 동작할 수 있도록 하기 위한 것이다
```java
class MyApplication {
    punlic static void main(String args[]) {
        Calendar cal = new GregorianCalendar(); // 경우에 따라 이 부분을 변경해야한다
            ...
    }
}
```
* 인스턴스를 생성하도록 프로그램이 작성되어 있다면, 다른 종류의 역법(calendar)을 사용하는 국가에서 실행한다던가, 새로운 역법이 추가된다던가 하는 경우, 즉 다른 종류의 인스턴스를 필요로 하는 경우에 MyApplication을 변경해야 하는데 비해 아래 코드와 같이 메서드를 통해서 인스턴스를 얻어오도록하면 MyApplication을 변경하지 않아도 된다
```java
class MyApplication {
    public static void main(String args[]) {
        Calendar cal = Calendar.getInstance();
            ...
    }
}
```
* 대신 getInstance()의 내용은 달라져야 하겠지만, MyApplication이 변경되지 않아도 된다는 것이 중요하다
* getInstance()메서드가 static인 이유는 메서드 내의 코드에서 인스턴스 변수를 사용하거나 인스턴스 메서드를 호출하지 않기 때문이며, 또 다른 이유는 getInstance()가 static이 아니라면 위와 같이 객체를 생성한 다음에 호출해야하는데 Calendar는 추상클래스이기 때문에 객체를 생성할 수 없기 때문이다

### Date와 Calendar간의 변환
* Calendar가 새로 추가되면서 Date는 대부분의 메서드가 'deprecated'되었으므로 잘 사용되지 않는다
  * 그럼에도 불구하고 여전히 Date를 필요로 하는 메서드들이 있기 때문에 Calendar를 Date로 또는 그 반대로 변환할 일이 생긴다
    * Java API 문서를 보면 더 이상 사용을 권장하지 않는 대상에 'deprecated'가 붙어있다
```java
1. Calendar를 Date로 변환
Calendar cal = Calendar.getInstance();
        ...
Date d = new Date(cal.getTimeInMillis()); // Date(long date)
        
2. Date를 Calendar로 변환
Date d = new date();
        ...
Calendar cal = Calendar.getInstance();
cal.setTime(d)
```
* Date를 Calendar로 변환

```java
import java.util.Calendar;
import java.util.Date;

public class DateToCalendarExample {
    public static void main(String[] args) {
        // Date 객체 생성
        Date date = new Date();

        // Calendar 객체 생성 및 Date를 Calendar로 변환
        Calendar calendar = Calendar.getInstance();
        calendar.setTime(date);

        // Calendar 객체를 이용하여 날짜 및 시간 조작
        calendar.add(Calendar.DAY_OF_MONTH, 1); // 1일 더하기

        // 변환된 Calendar 객체 사용
        int year = calendar.get(Calendar.YEAR);
        int month = calendar.get(Calendar.MONTH) + 1; // 월은 0부터 시작하므로 1을 더해줌
        int day = calendar.get(Calendar.DAY_OF_MONTH);
        int hour = calendar.get(Calendar.HOUR_OF_DAY);
        int minute = calendar.get(Calendar.MINUTE);
        int second = calendar.get(Calendar.SECOND);

        System.out.println("Year: " + year);
        System.out.println("Month: " + month);
        System.out.println("Day: " + day);
        System.out.println("Hour: " + hour);
        System.out.println("Minute: " + minute);
        System.out.println("Second: " + second);
    }
}
```

* Calendar를 Date로 변환

```java
import java.util.Calendar;
import java.util.Date;

public class CalendarToDateExample {
    public static void main(String[] args) {
        // Calendar 객체 생성
        Calendar calendar = Calendar.getInstance();

        // Calendar 객체를 Date로 변환
        Date date = calendar.getTime();

        // 변환된 Date 객체 사용
        System.out.println("Date: " + date);
    }
}
```
## 형식화 클래스
* 형식화 클래스는 java.text패키지에 포함되어 있으며 숫자, 날짜, 텍스트 데이터를 일정한 형식에 맞게 표현할 수 있는 방법을 객체지향적으로 설계하여 표준화하였다
  * 형식화 클래스는 형식화에 사용될 패턴을 정의하는데, 데이터를 정의된 패턴에 맞춰 형식화할 수 있을 뿐만 아니라 역으로 형식화된 데이터에서 원래의 데이터를 얻어낼 수도 있다
    * 이 것은 마치 "123"과 같은 문자열을 Integer.parseInt()를 사용해서 123이라는 숫자로 변환하는 것과 같은 일이 가능하다는 것을 의미한다
      * 즉, 형식화된 데이터의 패턴만 정의해주면 복잡한 문자열에서도 substring()을 사용하지 않고도 쉽게 원하는 값을 얻어낼 수 있다는 것이다
### DecimalFormat
* 형식화 클래스 중에서 숫자를 형식화 하는데 사용되는 것이 DecimalFormat이다
* DecimalFormat을 이용하면 수잦 데이터를 정수, 부동소수점, 금액 등의 다양한 형식으로 표현할 수 있으며, 반대로 일정한 형식의 텍스트 데이터를 숫자로쉽게 변환하는 것도 가능하다 <br>

| 기호 | 의미 | 패턴 | 결과 (1234567.89) |
| --- | --- | --- | --- |
| 0 | 숫자 (0부터 9까지) | `"00000.00"` | 1234567.89 |
| # | 숫자 (0부터 9까지), 숫자가 없으면 표시하지 않음 | `"#####.##"` | 1234567.89 |
| . | 소수점 | `"####.##"` | 1234567.89 |
| , | 그룹 구분 기호 (숫자를 천 단위로 그룹화) | `"#,###.##"` | 1,234,567.89 |
| % | 퍼센트를 나타내는 기호 (숫자를 100으로 나눈 값에 100을 곱함) | `"####.##%"` | 123456789% |
| E | 지수 표기법을 사용하여 숫자를 표시 (예: 1.23E+04) | `"0.####E0"` | 1.2346E6 |
| '...' | 작은 따옴표로 둘러싼 텍스트는 리터럴로 취급되며 패턴에 포함됨 | `"Today is 'yyyy-MM-dd'"` | Today is yyyy-MM-dd |
| \u2022 | 특수 기호를 이스케이프하기 위해 사용되는 역 슬래시 | `"#,###.00 \u2022"` | 1,234,567.89 • |

[Java API -> DecimalFormat](https://docs.oracle.com/javase/7/docs/api/index.html)

* DecimalFormat을 사용하는 방법
  * 먼저 원하는 출력형식의 패턴을 작성하여 DecimalFormat인스턴스를 생성한 다음, 출력하고자 하는 문자열로 format메서드를 호출하면 원하는 패턴에 맞게 변환된 문자열을 얻게 된다
```java
double number = 1234567.89;
DecimalFormat df = new DecimalFormat("#.#E0");
String result = df.format(number);
```
```java
import java.text.DecimalFormat;

public class DecimalFormatExample {
    public static void main(String[] args) {
        // 숫자 포맷을 지정
        DecimalFormat decimalFormat = new DecimalFormat("#,###.00");

        // 형식화하려는 숫자
        double number = 1234567.89;

        // 숫자를 형식화하여 문자열로 변환
        String formattedNumber = decimalFormat.format(number);

        // 결과 출력
        System.out.println("Formatted Number: " + formattedNumber);
    }
}
```
* 1234567389를 "#.###.00"형식으로 포맷하여 출력한다
  * 결과는 "1,234,567.89"가 됩니다
    * Decimal 포맷을 사용하여 숫자를 원하는 형식으로 표시할 수 있다

### SimpleDateFormat
* SimpleDteFormat을 사용하여 Date와 Calendar만으로 날짜 데이터를 원하는 형태로 다양하게 출력하는 것이다

| 기호 | 의미                             | 예시    |
| ---- | -------------------------------- | ------- |
| y    | 연도 (년)                        | 2023    |
| M    | 월 (1-12 또는 "MMM"과 함께 월 이름) | 7 또는 Jul |
| d    | 일 (월별)                        | 15      |
| h    | 시간 (1-12)                      | 9       |
| H    | 시간 (0-23)                      | 15      |
| m    | 분                               | 30      |
| s    | 초                               | 45      |
| S    | 밀리초                           | 789     |
| E    | 요일 (축약된 이름 또는 전체 이름) | Tue 또는 Tuesday |
| D    | 연중 일 수                       | 245     |
| F    | 월별 주                         | 2       |
| w    | 연중 주                         | 42      |
| a    | 오전/오후                        | AM 또는 PM |
| '    | 따옴표 (텍스트 리터럴)           | '오늘은' |

[Java API -> SimpleDateFormat](https://docs.oracle.com/javase/7/docs/api/index.html)

* SimpleDateFormat을 사용하는 방법
  * 먼저 원하는 출력형식의 패턴을 작성하여 SimpleDateFormat인스턴스를 생성한 다음, 출력하고자 하는 Date인스턴스를 가지고 format(Date d)를 호출하면 지정한 출력형식에 맞게 변환된 문자열을 얻게 된다
```java
Date today = new Date();
SimpleDateFormat df = new SimpleDateFormat("yyyy-MM-dd");

// 오늘 날짜를 yyyy-MM-dd형태로 변환하여 반환한다
String result = df.format(today);
```
```java
import java.text.SimpleDateFormat;
import java.util.Date;

public class SimpleDateFormatExample {
    public static void main(String[] args) {
        // 원하는 날짜 형식을 갖는 SimpleDateFormat 객체를 생성한다
        SimpleDateFormat dateFormat = new SimpleDateFormat("yyyy년 MM월 dd일 HH시 mm분 ss초");

        // 현재 날짜와 시간을 가져온다
        Date currentDate = new Date();

        // SimpleDateFormat을 사용하여 날짜를 형식화한다
        String formattedDate = dateFormat.format(currentDate);

        // 형식화된 날짜를 출력한다
        System.out.println("형식화된 날짜: " + formattedDate);
    }
}

```

### ChoiceFormat
* ChoiceFormat은 특정 범위에 속하는 값을 문자열로 변환해준다
  * 연속적 또는 불연속적인 범위의 값들을 처리하는데 있어서 if문이나 switch문은 적절하지 못 한 경우가 많다
    * 이럴 때 ChoiceFormat을 잘 사용하면 복잡하게 처리될 수 밖에 없었던 코드를 간단하고 직관적으로 만들 수 있다
```java
import java.text.ChoiceFormat;

public class ChoiceFormatExample {
    public static void main(String[] args) {
        double[] limits = {1, 2, 3, 4, 5};
        String[] formats = {"Poor", "Fair", "Good", "Very Good", "Excellent"};
        ChoiceFormat choiceFormat = new ChoiceFormat(limits, formats);

        double score = 3.2;
        String result = choiceFormat.format(score); // ChoiceFormat를 사용하여 점수 형식화
        System.out.println("Score: " + score + " -> " + result);
    }
}

```

### MessageFormat
* MessageFormat은 데이터를 정해진 양식에 맞춰 출력할 수 있도록 도와준다
  * 데이터가 들어갈 자리를 마련해 놓은 양식을 미리 작성하고 프로그램을 이용해서 다수의 데이터를 같은 양식으로 출력할 때 사용하면 좋다
    * 예룰 들어 고객들에게 보낼 안내문을 출력할 때 같은 안내문 양식에 받는 사람의 이름과 같은 데이터만 달라지도록 출력할 때, 또는 하나의 데이터를 다양한 양식으로 출력할 때 사용한다
* SimpleDateFormat의 parse처럼 MessageFormat의 parse를 이용하면 지정된 양식에서 필요한 데이터만을 손쉽게 추출해 낼 수도 있다
```java
import java.text.MessageFormat;

public class MessageFormatExample {
    public static void main(String[] args) {
        String pattern = "Hello, {0}! Your balance is {1,number,currency}.";
        String name = "희연";
        double balance = 12345.67;

        String formattedMessage = MessageFormat.format(pattern, name, balance);

        System.out.println(formattedMessage);
    }
}

```
* 메시지 패턴에 '{0}'과 '{1, number, currency}'와 같은 포맷 지정자를 사용하여 문자열을 형식화한다
* 'MessageFormat.format()'메서드를 호출할 때 메시지 패턴과 대입할 값을 전달하여 형식화된 문자열을 생성하고 출력한다
```java
Hello, 희연! Your balance is $12,345.67.
```

## java.time패키지
* Java의 탄생부터 지금까지 날짜와 시간을 다루는데 사용해왔던, Date와 Calendar가 가지고 있던 단점들을 해소하기 위해 드디어 JDK1.8부터 'java.time패키지'가 추가되었다

| 패키지                | 설명                                           |
| ---------------------- | ---------------------------------------------- |
| `java.time`            | 자바 8에서 추가된 날짜와 시간 API의 기본 패키지 |
| `java.time.chrono`     | 다른 달력 시스템과 연관된 클래스들을 포함함     |
| `java.time.format`     | 날짜와 시간 형식화 및 파싱을 위한 클래스들    |
| `java.time.temporal`   | 시간과 날짜에 대한 계산 및 조작을 위한 인터페이스 및 클래스들 |
| `java.time.zone`       | 시간대 및 시간대 규칙을 관리하는 클래스들    |

* String클래스처럼 '불변(immutable)'이라는 것이다
  * 날짜나 시간을 변경하는 메서드들은 기존의 객체를 변경하는 대신 항상 변경된 새로운 객체를 반환한다
    * 기존 Calendar클래스는 변경가능하므로, 멀티 쓰레드 환경에서 안전하기 못하다
* 멀티 쓰레드 환경에서는 동시에 여러 쓰레드가 같은 객체에 접근할 수 있기 때문에, 변경 가능한 객체는 데이터가 잘못될 가능성이 있으며, 이를 쓰레드에 안전(thread-safe)하지 않다고 한다

### java.time패키지의 핵심 클래스
* 날짜와 시간을 하나로 표현하는 Calendar클래스와 달리, java.time패키지에서는 날짜와 시간을 별도의 클래스로 분리해놓았다
  * 시간을 표현할 때는 LocalTime클래스를 사용하고, 날짜를 표현할 때는 LocalDate클래스를 사용한다
    * 날짜와 시간이 모두 필요할 때는 LocalDateTime클래스를 사용하면 된다
```java
LocalDate + LocalTime -> LocalDateTime
```
* 시간대(time-zone)까지 다뤄야 한다면, ZonedDateTIME클래스를 사용한다
```java
LocalDateTime + 시간대 -> ZonedDateTIME
```

### Period와 Duration
* Period는 두 날짜 간의 차이를 표현하기 위한 것이고, Duration은 시간의 차이를 표현하기 위한 것이다
```java
날짜 - 날짜 = Period
시간 - 시간 = Duration
```

### 객체 생성하기 - now(), of()
* java.time패키지에 속한 클래스의 객체를 생성하는 가장 기본적인 방법은 now()와 of()를 사용하는 것이다
* now()는 현재 날짜와 시간을 저장하는 객체를 생성한다
```java
import java.time.LocalDate;
import java.time.LocalDateTime;
import java.time.LocalTime;
import java.time.ZonedDateTime;

public class Localdatetest{
    public static void main(String[] args) {
        LocalDate date = LocalDate.now();
        LocalTime time = LocalTime.now();
        LocalDateTime dateTime = LocalDateTime.now();
        ZonedDateTime dateTimeInKr = ZonedDateTime.now();

        System.out.println(date);
        System.out.println(time);
        System.out.println(dateTime);
        System.out.println(dateTimeInKr);

    }
}

```
```java
2023-10-11
00:36:09.593758700
2023-10-11T00:36:09.593758700
2023-10-11T00:36:09.594752300+09:00[Asia/Seoul]
```

* of()는 단순히 해당 필드의 값을 순서대로 지정해주기만 하면 된다
* 각 클래스마다 다양한 종류의 of()가 정의되어 있다
```java
import java.time.LocalDate;
import java.time.LocalTime;

public class Localdatetest{
    public static void main(String[] args) {
        LocalDate date = LocalDate.of(2023, 10, 11);
        LocalTime time = LocalTime.of(12, 38, 15);

        System.out.println(date);
        System.out.println(time);

    }
}
```

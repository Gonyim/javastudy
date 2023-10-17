# 조건문과 반복문

* 프로그램의 흐름(flow)을 바꾸는 역할을 하는 문장들을 '제어문(flow)'이라고 한다

### 조건문 - if, switch

* 조건문은 조건식과 문장을 포함하는 블럭{}으로 구성되어 있으며, 조건식의 연산결과에 따라 실행할 문장이 달라져서 프로그램의 실행흐름을 변경할 수 있다
* 조건문은 if문과 switch문, 두 가지가 있으며 주로 if문이 많이 사용된다
* 처리할 경우의 수가 많을 때는 if문보다 switch문이 효율적이지만, switch문은 if문보다 제약이 많다

#### if문
* 가장 기본적인 조건문
* '만일(if) 조건식이 참(ture)이면 괄호{} 안의 문장들을 수행하라.'
```java
if (조건식) {
    // 조건식이 참(true)일 때 수행될 문장들을 적는다.
        }
```

##### 조건식

| 조건식                        | 설명                                                         |
| ----------------------------- | ------------------------------------------------------------ |
| `x == y`                      | 변수 `x`와 `y`의 값이 같은지 비교합니다.                   |
| `x != y`                      | 변수 `x`와 `y`의 값이 다른지 비교합니다.                   |
| `x < y`                       | 변수 `x`가 `y`보다 작은지 비교합니다.                       |
| `x <= y`                      | 변수 `x`가 `y`보다 작거나 같은지 비교합니다.               |
| `x > y`                       | 변수 `x`가 `y`보다 큰지 비교합니다.                         |
| `x >= y`                      | 변수 `x`가 `y`보다 크거나 같은지 비교합니다.               |
| `x && y`                      | 논리 AND 연산자로, `x`와 `y`가 모두 `true`일 때 `true`를 반환합니다. |
| `x \|\| y`                   | 논리 OR 연산자로, `x`와 `y` 중 하나라도 `true`이면 `true`를 반환합니다. |
| `!(x)`                        | 논리 NOT 연산자로, `x`가 `true`이면 `false`, `false`이면 `true`를 반환합니다. |

* 자바에서 조건식의 결과는 반드시 true 또는 false이어야 한다
* 조건문을 작성할 때 등가비교 연산자 '=='와 대입 연산자 '='를 실수하기 쉽다
```java
// 'x가 0일 때 참'인 조건식은 'x==0'인데, 실수로 'x=0'이라고 적는 경우!
if (x=0) {...} // x에 0이 저장되고, 결과는 0이 된다
-> if (0) {...} // 결과가 true 또는 false가 아니므로 에러가 발생한다
```
##### 블럭 {}
* 블럭(block) : 괄호{}를 이용해서 여러 문장을 하나의 단위로 묶을 수 있는 것
  * '}' 다음에 문장의 끝을 의미하는 ';'을 붙이지 않는다는 것에 주의!
* 블럭 내의 문장들은 탭(tap)으로 들여쓰기(indentation)를 해서 블럭 안에 속한 문장이라는 것을 알기 쉽게 해주는 것이 좋다
```java
if (score > 60) {
    System.out.println("합격입니다.");
        }
```
* 블럭 안에는 보통 여러 문장을 넣지만, 한 문장만 넣거나 아무런 문장도 넣지 않을 수 있다
* 만일 블럭 내의 문장이 하나뿐 일 때는 괄호{}를 생략할 수 있다
```java
if(score > 60)
    System.out.println("합격입니다.");
```

* 한 줄로 작성도 가능하다
```java
if(score > 60) System.out.println("합격입니다.");
```

* 괄호는 가능하면 생략하지 않고 사용하는 것이 바람직하다 <br>
  -> 나중에 새로운 문장들이 추가되면 괄호{}로 문장들을 감싸 주어야하는데, 이 때 괄호{}를 추가하는 것을 잊기 쉽다
```java
if (score > 60)
    System.out.println("합격입니다."); // 문장1. if문에 속한 문장
    System.out.println("축하드립니다."); // 문장2. if문에 속한 문장이 아님
```
* 괄호로 묶어주지 않았기 때문에 '문장2'는 if문에 속한 문장이 아니다
* 들여쓰기를 했기 때문에 if문에 속한 것으로 착각하기 쉽지만 단지 들여쓰기를 했다고 if문에 속한 문장이 되는 것이 아니다 <br>
-> 괄호{}로 묶어줘야만 두 문장 모두 if문에 속한 문장이 된다

```java
import java.util.*;

public class FlowEx2 {
    public static void main(String[] args) {
        int input;

        System.out.println("숫자를 하나 입력하세요.>");

        Scanner scanner = new Scanner(System.in);
        String tmp = scanner.nextLine(); // 화면에 입력받은 내용을 tmp에 저장
        input = Integer.parseInt("입력하신 숫자는 0입니다.");

        if(input==0) {
            System.out.println("입력하신 숫자는 0입니다.");
        }

        if(input!=0)
            System.out.println("입력하신 숫자는 0이 아닙니다.");
            System.out.println("입력하신 숫자는 %d입니다.", input);
    }
}
```
#### if-else문
* if문에 'else블럭'이 더 추가되었다
* 'else'의 뜻이 '그 밖의 다른'이므로 조건식의 결과가 참이 아닐 때, 즉 거짓일 때 else블럭의 문장을 수행하라는 뜻이다
```java
if (조건식) {
    // 조건식이 참(true)일 때 수행될 문장들을 적는다
        } else {
    // 조건식이 거짓(false)일 때 수행될 문장들을 적는다
        }
```
* 조건식의 결과에 다라 이 두 개의 블럭{} 중 어느 한 블럭{}의 내용이 수행되고 전체 if문을 벗어나게 된다<br>
-> 두 블럭{}의 내용이 모두 수행되거나, 모두 수행되지 않는 경우는 있을 수 없다
```java
import java.util.*;

public class FlowEx3 {
    public static void main(String[] args) {
        System.out.println("숫자를 하나 입력하세요.>");

        Scanner scanner = new Scanner(System.in);
        int input = scanner.nextInt(); // 화면을 통해 입력받은 숫자를 input에 저장

        if (input==0) {
            System.out.println("입력하신 숫자는 0입니다.");
        } else { // input !=0인 경우
            System.out.println("입력하신 숫자는 0이 아닙니다.");
        }
    }
}
```
* if-else문 역시 블럭 내의 문장이 하나분인 경우 괄호{} 생략이 가능하다

#### if-else if문
* 처리해야할 경우의 수가 셋 이상인 경우
```java
if (조건식1) {
    // 조건식1의 여뇨산결과가 참일 때 수행될 문장들을 적는다
        } else if (조건식2) {
    // 조건식2의 연산결과가 참일 때 수행될 문장들을 적는다
        } else if (조건식3) { // 여러 개의 else if를 사용할 수 있다
    // 조건식3의 연산결과가 참일 때 수행도리 문장들을 적는다.
        } else { // 마지막에는 보통 else블럭으로 끝나며, else블럭을 생략가능하다
    // 위의 어느 조건식도 만족하지 않을 때 수행될 문장들을 적는다
        }
```
* 첫번째 조건식부터 순서대로 평가해서 결과가 참인 조건식을 만나면, 해당 블럭{}만 수행하고 'if-else if'문 전체를 벗어난다
* 결과가 참인 조건식이 하나도 없으면, 마지마겡 있는 else블럭의 문장들이 수행된다
* else 블럭은 생략이 가능하다
  * else블럭이 생략되었을 때는 if-else if문의 어떤 블럭도 수행되지 않을 수 있다
#### 중첩 if문
* if문의 블럭 내에 또 다른 if문을 포함시키는 것이 가능한 것
* 중첩의 횟수에는 거의 제한이 없다
```java
if (조건식1) {
    // 조건식1의 연산결과가 ture일 때 수행될 문장들을 적는다
        if (조건식2) {
            // 조건식1과 조건식2가 모두 ture일 때 수행될 문장들
        } else {
            // 조건식1이 true이고, 조건식2가 false일 때 수행되는 문장들
        }
        } else {
    // 조건식1일 false일 때 수행되는 문장들
        }
```
* 내부의 if문은 외부의 if문보다 안쪽으로 들여쓰기를 해서 두 if문의 범위가 명확히 구분될 수 있도록 작성해야한다
```java
if (num >= 0)
    if (num != 0)
        sign = '+';
else
    sign = '-';
```
(X)
```java
if (num >= 0) {
    if (num != 0) {
        sign = '+';
    } else {
        sign = '-';
        }
}
```
* 괄호가 생략되었을 때 else블럭은 가까운 if문에 속한 것으로 간주되기 때문에 실제로는 오른쪽과 같이 안쪽 if문의 else블럭이 되어버린다
#### switch문
* if문과 달리 switch문은 단 하나의 조건식으로 많은 경우의 수를 처리할 수 있고, 표현도 간결하므로 알아보기 쉽다
  * 그래서 처리할 경우의 수가 많은 경우에는 if문 보다 switch문으로 작성하는 것이 좋다
    * 다만 switch문은 제약조건이 있기 때문에, 경우의 수가 많아도 어쩔 수 없이 if문으로 작성해야 하는 경우가 있다
* switch문 실행 순서
  1. 조건식을 계산한다
  2. 조건식의 결과와 일치하는 case문으로 이동한다
  3. 이후의 문장들을 수행한다
  4. break문이나 switch문의 끝을 만나면 switch문 전체를 빠져나간다
```java
switch (조건식) {
    case 값1 :
        // 조건식의 결과가 값1과 같ㅇ르 경우 수행될 문장들
        break;
    case 값 2 :
        // 조건식의 결과가 값2와 같을 경우 수행될 문장들
        break;
    default :
        // 조건식의 결과와 일치하는case문이 없을 때 수행될 문장들
        }
```
* 조건식의 결과와 일치하는 case문이 하나도 없는 경우에는 default문으로 이동한다 <br>
-> default문은 if문의 else블럭과 같은 역할을 한다고 보면 이해하기 쉽다!
* default문의 위치는 어디라도 상관없으나, 보통 마지막에 놓기 때문에 break문을 쓰지 않아도 된다
* break문은 각 case문의 영역을 구분하는 역할을 한다
  * 만일 break문을 생략하면 case문 사이의 구분이 없어지므로 다른 break문을 만나거나 switch문 블럭{}의 끝을 만날 때까지 나오는 모든 문장들을 수행한다 <br>
  -> 각 case문의 마지막에 break문을 빼먹는 실수를 하지 않도록 주의해야한다
* 고의적으로 break문을 생략하는 경우도 있다
```java
switch (level) {
    case 3 :
        grantDelete(); // 삭제권한을 준다
    case 2 :
        grantWrite(); // 쓰기권한을 준다
    case 1 :
        grantRead(); // 읽기권한을 준다
        }
```
##### switch문의 제약조건
* 결과값이 반드시 정수
  * 이 값과 일치하는 case문으로 이동하기 때문에 case문의 값 역시 정수
* 중복되지 않아야 한다
  * 같은 값의 case문이 여러 개이면, 어디로 이동해야할 지 알 수 없기 때문
* 반드시 상수이어야 한다
  * 변수나 실수, 문자열은 case문의 값으로 사용할 수 없다
```java
switch문의 제약조건
1. switch문의 조건식 결과는 정수 또는 문자열이어야 한다
2. case문의 값은 정수 상수만 가능하며, 중복되지 않아야 한다
```
##### switch문의 중첩
* if문 처럼 switch문도 중첩이 가능하다
* 
물론, 반복문과 관련된 내용을 더 자세하게 설명하겠습니다.

### 반복문 - for, while, do-while

반복문은 어떤 작업을 반복적으로 수행할 때 사용

#### for 문

`for` 문은 초기화, 조건식, 증감식을 사용하여 반복문을 제어

```java
for (초기화; 조건식; 증감식) {
    // 조건식이 참일 때 수행될 문장들
}
```

ex)

```java
for (int i = 1; i <= 5; i++) {
    System.out.println("Iteration " + i);
}
```

* `for` 문에서 각 부분의 역할
  - 초기화: 반복문에 사용될 변수를 초기화
  - 조건식: 반복문을 계속할지 여부를 판단하는 조건을 지정
  - 증감식: 각 반복에서 변수를 증가 또는 감소시키는 작업을 수행

#### while 문

`while` 문은 조건이 `true`인 동안 반복을 수행

```java
while (조건식) {
    // 조건식이 참일 때 수행될 문장들
}
```

ex)

```java
int count = 0;
while (count < 3) {
    System.out.println("Count: " + count);
    count++;
}
```

#### do-while 문

`do-while` 문은 최소한 한 번의 반복을 보장하며, 조건 검사는 반복의 끝에서 수행

```java
do {
    // 반복될 문장들
} while (조건식);
```

ex)

```java
int number = 5;
do {
    System.out.println("Number: " + number);
    number--;
} while (number > 0);
```

#### break 문

`break` 문은 반복문을 중단하고 해당 루프를 빠져나오는 데 사용

```java
for (int i = 0; i < 5; i++) {
    if (i == 3) {
        break; // i가 3일 때 반복문 종료
    }
    System.out.println("Iteration " + i);
}
```

#### continue 문

`continue` 문은 현재 반복의 나머지 부분을 건너뛰고 다음 반복으로 진행

```java
for (int i = 0; i < 5; i++) {
    if (i == 2) {
        continue; // i가 2일 때 현재 반복을 건너뛰고 다음 반복으로 진행
    }
    System.out.println("Iteration " + i);
}
```

#### 이름 붙은 반복문

* 이름 붙은 반복문은 중첩된 반복문에서 특정 반복문을 참조할 때 사용
* 이름 붙은 반복문은 레이블을 지정하여 구분하며, 일반적으로 중첩된 반복문에서 `break` 또는 `continue`를 사용할 때 유용

```java
outerLoop: for (int i = 0; i < 5; i++) {
    innerLoop: for (int j = 0; j < 3; j++) {
        if (i == 2 && j == 1) {
            break outerLoop; // 외부 반복문을 종료
        }
        System.out.println("i: " + i + ", j: " + j);
    }
}
```
-> `break outerLoop`는 외부 반복문을 종료하게 만듭니다

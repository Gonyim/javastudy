# 조건문과 반복문
## 조건문
### if
![if](https://velog.velcdn.com/images/kid/post/0a0288fb-c256-42b8-818e-2053b7f00b68/image.png)

if문은 조건식의 결과에 따라서 블록의 실행 여부가 결정됩니다.
조건식에는 ture 또는 false 값을 산출할 수 있는 연산식이나, boolean 변수가 올 수 있습니다.
조건식이 true이면 블록을 실행하고 false이면 블록을 실행하지 않습니다.
if문 안에 있는 중괄호 블록은 실행문이 하나 밖에 없다면 생략할 수 있으나,
중괄호 블록이 없으면 코드의 가독성이 떨어질 수 있기 때문에 되도록 작성하는 것을 권장합니다.

#### 예제
```java
public class Main {
    public static void main(String[] args) {
        String language = "Java";

        if (language == "Java") {
            System.out.println("자바 최고 ㅎ");
        }
    }
}
```

<br>

### if-else
![if-else](https://velog.velcdn.com/images/kid/post/93062a01-e684-4254-95fd-7bda7c257388/image.png)

if문은 else 블록과 함께 사용되어 조건식의 결과에 따라 실행 블록을 선택할 수 있습니다.
조건식이 true이면 if문의 블록이 실행되고, false라면 else 블록이 실행됩니다. 조건식의 결과에 따라 두 개의 블록 중 어느 한 블록의 내용만 실행하고 전체 if문을 벗어나게 됩니다.

#### 예제
```java
public class Main {
    public static void main(String[] args) {
        int score = 85;

        if (score > 90) {
            System.out.println("점수가 90점보다 높습니다.");
        } else {
            System.out.println("점수가 90점 이하입니다.");
        }
    }
}
```

<br>

### if-else if-else
![if-else-if-else](https://velog.velcdn.com/images/kid/post/fb69eed2-c1b5-45cc-9b90-fbc41aa096fd/image.png)

조건문이 여러 개인 if문도 있습니다. 처음 if문의 조건식이 false일 경우에 다른 조건식의 결과에 따라 실행 블록을 선택할 수 있는데, if문의 끝에 else if를 붙이는 방법으로 사용합니다.
else if문의 수는 제한이 없고 마지막에는 else 블록을 추가할 수 있습니다. 모든 조건식이 false일 경우에는 else 블록을 실행하고 if문을 벗어나게 됩니다.

#### 예제
```java
public class Main {
    public static void main(String[] args) {
        int num = (int) (Math.random() * 6) + 1;

        if (num == 1) {
            System.out.println("1번이 나왔습니다.");
        } else if (num == 2) {
            System.out.println("2번이 나왔습니다.");
        } else if (num == 3) {
            System.out.println("3번이 나왔습니다.");
        } else if (num == 4) {
            System.out.println("4번이 나왔습니다.");
        } else if (num == 5) {
            System.out.println("5번이 나왔습니다.");
        } else {
            System.out.println("6번이 나왔습니다.");
        }
    }
}
```

<br>

### 중첩 if
if문의 블록 내부에는 또 다른 if문을 사용할 수 있습니다. 중첩의 단계는 제한이 없습니다.
if문만 중첩되는 것은 아니며, switch문, for문, while문, do-while문도 서로 중첩이 가능합니다.
예를 들어 if문 안에 for문을 넣을 수도 있고, while문 안에 if문을 넣을 수도 있습니다.

#### 예제
```java
public class Main {
    public static void main(String[] args) {
        int score = (int) (Math.random() * 20) + 81;
        System.out.println("점수: " + score);

        String grade;

        if (score >= 90) {
            if (score >= 95) {
                grade = "A+";
            } else {
                grade = "A";
            }
        } else {
            if (score >= 85) {
                grade = "B+";
            } else {
                grade = "B";
            }
        }

        System.out.println("학점: " + grade);
    }
}
```

<br>

### switch
![switch](https://velog.velcdn.com/images/kid/post/a36c2f05-bf1a-4218-9567-63de943c943b/image.png)

switch문은 if문과 마찬가지로 조건 제어문입니다. 하지만 switch문은 if문처럼 조건식이 true일 경우
실행문을 실행하는 것이 아니라, 변수가 어떤 값을 갖느냐에 따라 실행문이 선택됩니다.
if문은 조건식의 결과가 ture, false 두 가지밖에 없기 때문에 경우의 수가 많아질수록 else-if를 반복적으로 추가해줘야 하므로 코드가 복잡해질 수 있습니다. 하지만 switch문은 변수의 값에 따라서 실행문이 결정되기 때문에 같은 기능의 if문보다 코드가 간결해집니다.

switch문은 괄호 안의 값과 동일한 값을 갖는 case의 실행문을 실행시킵니다. 만약 괄호 안의 값과 동일한 값을 갖는 case가 없다면 default로 가서 실행문을 실행시킵니다. default는 생략이 가능합니다.

case 끝에 break를 붙이면 다음 case를 실행하지 않고 switch문을 빠져나가고,
break가 없다면 다음 case를 연달아 실행하는데 이때에는 case값과는 상관없이 실행됩니다.

Java 6까지는 switch문의 괄호에 정수 타입 변수나 정수값을 산출하는 연산식만 쓸 수 있었지만,
Java 7부터는 String 타입의 변수도 넣을 수 있게 되었습니다.

#### 예제
```java
public class Main {
    public static void main(String[] args) {
        int num = (int) (Math.random() * 6) + 1;

        switch (num) {
            case 1:
                System.out.println("1번이 나왔습니다.");
                break;
            case 2:
                System.out.println("2번이 나왔습니다.");
                break;
            case 3:
                System.out.println("3번이 나왔습니다.");
                break;
            case 4:
                System.out.println("4번이 나왔습니다.");
                break;
            case 5:
                System.out.println("5번이 나왔습니다.");
                break;
            default:
                System.out.println("6번이 나왔습니다.");
                break;
        }
    }
}
```

<br>

## 반복문
### for
![for](https://velog.velcdn.com/images/kid/post/d23bc560-a46d-4df5-8dc8-e3c885b3e581/image.png)

프로그램을 작성하다 보면 똑같은 실행문을 반복적으로 실행해야 하는 경우가 많이 발생합니다.
for문은 그러한 상황에 반복해야 하는 횟수를 알고 있을 때 주로 사용되는 제어문입니다.
```java
for ((1)초기화식; (2)조건식; (4)증감식) {
	(3)실행문;
}
```

for문의 흐름을 간단히 설명하면 다음과 같습니다.

1. 초기화식이 실행됩니다.
2. 그 후 조건식이 true이면 실행문을 실행시키고, false이면 for문을 벗어납니다.
3. 실행문이 모두 실행되면 증감식을 실행시키고 다시 조건식을 평가합니다.
4. 평가 결과가 true이면 (3) > (4) > (2) 순서로 다시 진행합니다.

초기화식은 조건식과 실행문, 증감식에서 사용할 변수를 초기화하는 역할을 합니다.
그렇기 때문에 다음과 같이 초기화식을 생략하거나, 둘 이상의 초기화식을 가질 수 있습니다.
```java
public class Main {
    public static void main(String[] args) {
        int i = 1;
        for (; i<=10; i++) {
            System.out.println(i);
        }

        for (int j=0, k=10; j<=5 && k >=5; j++, k--) {
            System.out.println(j + k);
        }
    }
}
```

for문을 작성할 때 주의해야할 점은 실수 타입 변수를 사용하는 것입니다.
아래의 코드는 부동 소수점에 의해 정밀도 손실이 일어나기 때문에 9번의 루프만 실행됩니다.
```java
public class Main {
    public static void main(String[] args) {
        for (float x=0.1f; x<=1.0f; x+=0.1f) {
            System.out.println(x);
        }
    }
}
```

#### 예제 - 중첩 for문을 활용한 구구단
```java
public class Main {
    public static void main(String[] args) {
        for (int i=1; i<=9; i++) {
            for (int j=2; j<=9; j++) {
                System.out.print(j + " x " + i + " = " + String.format("%2d", i * j));
                System.out.print("    ");
            }
            System.out.println();
        }
    }
}
```

<br>

### while
![while](https://velog.velcdn.com/images/kid/post/ffe0735d-7119-48fe-8442-f3af6f258f10/image.png)

for문이 정해진 횟수만큼 반복한다면, while문은 조건식이 true일 경우에 계속해서 반복합니다.
그렇기 때문에 while(true) {...}같은 방식으로 사용하게 되면 무한 루프를 돌게 됩니다.
조건식에는 비교 또는 논리 연산식을 주로 쓰고, 조건식이 false가 되면 while문을 벗어납니다.

#### 예제
```java
public class Main {
    public static void main(String[] args) {
        int i = 1;
        while (i <= 10) {
            System.out.println(i);
            i++;
        }
    }
}
```

<br>

### do-while
![do-while](https://velog.velcdn.com/images/kid/post/01cdb773-696d-4b40-8a62-2fe0dd4dbf06/image.png)

do-while문은 조건식에 의해 반복 실행한다는 점에서 while문과 동일합니다.
while문은 시작할 때부터 조건식을 검사하여 실행문의 실행 여부를 결정하지만,
do-while문은 실행문을 우선 실행시키고 결과에 따라서 실행을 반복할지 결정합니다.
예를 들어 사용자로부터 입력받은 내용을 검증하여 계속 반복할 것인지 판단하는 프로그램이 있다면,
조건식은 사용자의 입력을 받은 이후에 평가되어야 하므로 실행문을 우선적으로 실행합니다.

#### 예제
```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        System.out.println("프로그램을 종료하려면 q를 입력하세요.");

        Scanner sc = new Scanner(System.in);
        String input;

        do {
            System.out.print("> ");
            input = sc.nextLine();
            System.out.println(input);
        } while (!input.equals("q"));

        System.out.println();
        System.out.println("프로그램을 종료합니다.");
    }
}
```

<br>

### break
![break](https://velog.velcdn.com/images/kid/post/8e34dd1c-ae3f-4268-bea3-ca2235ae1d2f/image.png)

![labeled-break](https://velog.velcdn.com/images/kid/post/7257b8d6-1be6-4a35-8ac2-f7506dc6ad53/image.png)

break문은 반복문인 for문, while문, do-while문을 실행 중지할 때 사용됩니다.
또한 switch문에서도 break문을 사용하여 중지가 가능합니다.
반복문이 중첩되어 있는 경우 break문은 가장 가까운 반복문만 종료하고 바깥쪽 반복문은 종료시키지 않습니다. 중첩된 반복문에서 바깥쪽 반복문까지 종료시키려면 반복문에 이름(라벨)을 붙이고,
"break (라벨);" 을 사용하면 됩니다.

#### 예제
```java
public class Main {
    public static void main(String[] args) {
        while (true) {
            int num = (int) (Math.random()*6) + 1;
            System.out.println(num);
            if (num == 6) {
                break;
            }
        }
        System.out.println("프로그램 종료");
    }
}
```

#### 예제 - 라벨을 사용한 break
```java
public class Main {
    public static void main(String[] args) {
        Outter: for (char upper='A'; upper<='Z'; upper++) {
            for (char lower='a'; lower<='z'; lower++) {
                System.out.println(upper + "=" + lower);
                if (lower == 'g') {
                    break Outter;
                }
            }
        }
        System.out.println("프로그램 종료");
    }
}
```

<br>

### continue
![continue](https://velog.velcdn.com/images/kid/post/380993db-5618-41ad-9d4d-40a51daf99d4/image.png)

continue문은 반복문인 for문, while문, do-while문에서만 사용되는데, 블록 내부에서 continue문이 실행되면 for문의 증감식 또는 while문, do-while문의 조건식으로 이동합니다.
주로 if문과 함께 사용되는데, 특정 조건을 만족하는 경우에 그 이후의 문장을 실행하지 않고 다음 반복으로 넘어가게 됩니다. break문과 마찬가지로 라벨을 사용할 수 있습니다.

#### 예제
```java
public class Main {
    public static void main(String[] args) {
        for (int i=1; i<=10; i++) {
            if (i%2 != 0) {
                continue;
            }
            System.out.println(i);
        }
    }
}
```

<br>

### 레퍼런스
- 이것이 자바다: 신용권의 Java 프로그래밍 정복
- Java Flow Control: https://www.programiz.com/java-programming/if-else-statement
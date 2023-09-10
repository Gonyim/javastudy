# 1장 : 자바 시작

## 자바의 특징
1. 플랫폼 독립성
2. 객체 지향
3. 클래스로 캡슐화
4. 소스와 클래스 파일
5. 실행 코드 배포
6. 패키지
7. 멀티스레드
8. 가비지 컬렉션
9. 실시간 응용 시스템에 부적합하다.
- 실행 도중 예측할 수 없는 시점에 가비지 컬렉션이 실행되므로
10. 자바 프로그램은 안전하다.
11. 프로그램 작성이 쉽다.
12. 실행 속도를 개선하기 위해 JIT 컴파일러가 사용된다.

## 인텔리제이 설치 : <https://wiken.io/ken/6746/>

### 인텔리제이 초기 세팅
1. fly - 4개 체크
2. mouse - 휠로 글씨 크기 변경
3. compiler - Build project Automatically 체크
4. advanced - allow auto-make to start ~~ 체크
5. encoding - 전부 UTF-8로 변경, Transparent 체크
6. indent - Java - Tabs and Indents(탭 했을 때 공간) : 2, 2, 4로 변경
7. indent - HTML - Tabs and Indents(탭 했을 때 공간) : 2, 2, 4로 변경
8. indent - JSON - Tabs and Indents(탭 했을 때 공간) : 2, 2, 4로 변경
9. shift연타 - registry... - compiler automake postpone ... : 500으로 변경
10. Help - Edit Custom VM Options - 첫번째줄(가용하는 램크기) - 두번째줄에 -Dfile.encoding=UTF-8 입력 후 저장
11. Invalidate Caches - 전부 체크 후 Just Restart 클릭
12. 유튜브 참고 : https://www.youtube.com/@bang_gusuk_coder/playlists

## JDK, JRE
- JDK(Java Development Kit)는 자바 개발자에게 무료로 배포하는 소프트웨어로 자바 컴파일러 등의 개발 도구와 JRE(Java Runtime Environment)로 구성된다. JRE는 자바 응용프로그램이 실행될 때 필요한 소프트웨어들로 개발자가 활용할 수 있는 자바 API(이미 컴파일된 다양한 클래스 라이브러리)와 자바 가상 머신를 포함한다.

## 자바 API(17.ver)
- <https://docs.oracle.com/en/java/javase/17/docs/api/index.html/>

## 자바 프로그램 개발
- **자바에서는 클래스 이름과 소스 파일의 이름이 일치해야 한다.**
- 자바 소스 파일의 확장자는 .java이며, 클래스 명에 대소문자를 구분한다.
- public class Main : 이름이 Main인 클래스를 선언한다. 모든 클래스는 '{'으로 시작해서 '}'으로 끝난다.
- public static void main(String[] args) : main() 메소드를 선언하는 코드이다. 자바에서는 함수를 메소드라고 부르며, '{'으로 시작해서 '}'으로 끝난다. 클래스는 여러 개의 메소드를 포함할 수 있고, 프로그램 실행은 반드시 main() 메소드부터 시작한다.
- 하나의 클래스 파일에는 반드시 하나의 자바 클래스가 컴파일되어 있다.
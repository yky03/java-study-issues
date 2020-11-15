# 목표
자바 소스 파일(.java)을 JVM으로 실행하는 과정 이해하기.

# 학습할 것
- JVM이란 무엇인가
- 컴파일 하는 방법
- 실행하는 방법
- 바이트코드란 무엇인가
- JIT 컴파일러란 무엇이며 어떻게 동작하는지
- JVM 구성 요소
- JDK와 JRE의 차이


- - -

## JVM이란 무엇인가

- 자바 가상 머신(Java Virtual Machine) 의 약자로써 작성한 Java 프로그램을 실행시키는 역할을 함
- 스택 기반의 가상머신
- 가비지 컬렉션 사용
- 플렛폼에 독립적
- Class 파일을 Jvm으로 로딩하고 Bytecodee를 해석하는 작업, 메모리 등의 리소스를 할당하고 관리

## 컴파일 하는 방법

- javac test.java (test.class 파일이 생성됨)

## 실행하는 방법

- java test (test.class 파일이 실행됨)
- 소스파일 -> 실행파일 -> JVM영역 [ Class loader -> Byte code Verifler -> Just-in-Time Compiler -> Runtime System ] -> 운영체제 -> Hardware

Link : [JVM이 자바프로그램을 실행하는 과정](https://medium.com/pocs/jvm%EC%9D%B4-%EC%9E%90%EB%B0%94%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%A8%EC%9D%84-%EC%8B%A4%ED%96%89%ED%95%98%EB%8A%94-%EA%B3%BC%EC%A0%95)

## 바이트코드란 무엇인가

- 바이트코드는 특정 하드웨어가 아닌 가상 컴퓨터에서 돌아가는 실행 프로그램을 위한 이진 표현법이다. 
- 하드웨어가 아닌 소프트웨어에 의해 처리되기 때문에, 보통 기계어보다 더 추상적이다.

- 자바 바이트코드(Java bytecode)는 자바 가상 머신이 실행하는 명령어의 형태이다. 
- 각각의 바이트코드는 1바이트로 구성되지만 몇 개의 파라미터가 사용되는 경우가 있어 총 몇 바이트로 구성되는 경우가 있다.
- 256개의 명령코드 모두가 사용되지는 않는다.

Link : [바이트코드 위키백과](https://ko.wikipedia.org/wiki/%EB%B0%94%EC%9D%B4%ED%8A%B8%EC%BD%94%EB%93%9C)
Link : [자바 바이트코드 위키백과](https://ko.wikipedia.org/wiki/%EC%9E%90%EB%B0%94_%EB%B0%94%EC%9D%B4%ED%8A%B8%EC%BD%94%EB%93%9C)

## JIT 컴파일러란 무엇이며 어떻게 동작하는지

- JIT 컴파일(just-in-time compilation) 또는 동적 번역(dynamic translation)은 프로그램을 실제 실행하는 시점에 기계어로 번역하는 컴파일 기법.
- Just In Time Compiler(JIT)은 실행할때 컴파일함.
- 파일 전체를 한번에 기계어로 변환함.
- 미리 컴파일해놓고 실행하므로 처리속도가 빠름.

Link : [JIT 컴파일 위키백과](https://ko.wikipedia.org/wiki/JIT_%EC%BB%B4%ED%8C%8C%EC%9D%BC)

## JVM 구성 요소

- 메소드영역(클래스변수)
- 힙 영역(인스턴스,객체)
- 스택영역(매개변수,지역변수)
- PC레지스터(스레드마다 하나씩존재, 현재 수행중인 JVM주소 저장)
- Native 메소드 스택(JNI표준규약 제공)영역으로 이루어짐

Link : [자바 메모리 구조](https://hoonmaro.tistory.com/19)

## JDK와 JRE의 차이

- JRE : 자바 런타임 환경으로써 자바 클래스 라이브러리 -> JVM + JAVA 패키지 클래스
- JDK : 자바 개발 키트로써 자바의 모든 기능을 갖춘 SDK(소프트웨어 개발 키트) -> JRE + 개발/디버깅 툴
- JVM : 클래스 로더 시스템 + 런타임 데이터 영역 + 실행 엔진

Link : [JDK와 JRE의 차이](https://c10106.tistory.com/3135)


## 마크다운 문법 참고
Link : [마크다운 markdown 작성법](https://gist.github.com/ihoneymon/652be052a0727ad59601)



# 목표  
자바의 패키지에 대해 학습하세요.  

# 학습할 것(필수)  
- package 키워드  
- import 키워드  
- 클래스패스  
- CLASSPATH 환경변수  
- classpath 옵션  
- 접근지시자  

- - -


## package 키워드 

-패키지란 클래스들을 하나로 묶어놓은 것이다.  
-클래스 간의 이름 중복으로 발생하는 충돌을 막아준다.  
-클래스를 기능 별로 분류할 수 있어 필요한 클래스의 식별이 용이하다.  

- 빌트인패키지  
```
자바는 개발자들이 사용할 수 있도록 여러 많은 패키지 및 클래스를 제공한다.
가장 자주 쓰이는 패키지로는 **java.lang**과 **java.util**이 있다.
java.lang은 자주 사용하는 패키지이지만 한번도 **import**하여 사용한적이 없다.
**즉, 자바에서 java.lang 패키지는 아주 기본적인 것들이기 때문에 import로 불러오지 않아도 자바가 알아서 java.lang의 클래스를 불러온다.**

//ex) String, System  
import java.lang.String;
import java.lang.System;

public class Main{
	public static void main(String[] args){
		String str = this is from java.lang.String";
		System.out.println(str);
	}
}
```

[패키지 참고](https://blog.hexabrain.net/120)  
[접근 제어자 참고](https://kils-log-of-develop.tistory.com/430)  
[빌트인패키지 참고](https://www.notion.so/ed8e346f88f54849a06ff968b1877ca5)  


## import 키워드  

```
import 패키지 이름/패키지 경로.*; // ex) import com.tutorial.*  
```
```
-자바의 기본 패키지  
java.lang : 기본적인 클래스 제공 (자동으로 import)   
java.awt : GUI에 관한 클래스 제공  
java.io : 데이터 입출력에 관한 클래스 제공  
java.util : 유용한 유틸리티 클래스 제공  
java.net : 네트워크 관련 클래스 제공   
java.text : 텍스트 관련 클래스 제공  
java.sql : 데이터베이스 관련 클래스 제공   
java.applet : 애플릿 구현에 필요한 클래스 제공  
```

[import 참고](https://blog.hexabrain.net/120)



## 클래스패스  

클래스패스란 말 그대로 클래스를 찾기위한 경로이다. 자바에서 클래스패스의 의미도 똑같다.  
즉, JVM이 프로그램을 실행할 때, 클래스파일을 찾는 데 기준이 되는 파일 경로.    

* rt.jar  
: runtime java, jvm이 돌아갈 때 기본적인 자바의 기본 패키지 API를 담고 있음.  

[클래스패스 참고](https://effectivesquid.tistory.com/entry/%EC%9E%90%EB%B0%94-%ED%81%B4%EB%9E%98%EC%8A%A4%ED%8C%A8%EC%8A%A4classpath%EB%9E%80)



## CLASSPATH 환경변수  

-환경변수란 프로세스가 컴퓨터에서 동작하는 방식에 영향을 미치는 동적인 값들이다.  
-사용자변수란 OS내의 사용자 별로 다르게 설정 가능한 환경변수이다.  
-시스템변수란 시스템 전체에 모두 적용되는 환경변수이다.  

* Path 환경변수를 지정해주면 어느 경로에서 실행해도 그실행경로에 자동으로 접근하여 프로그램을 실행할 수 있다.   
- 자바는 보통 새 시스템 변수에 JDK경로를 변수로 입력해준다. ( 변수 이름 : JAVA_HOME , 변수 값 : C:jdk-11.0.1)  
- 그 다음 Path 에 %JAVA_HOME%\bin\ 을 추가해준다.(cmd열고 javac 명령어를 치면 해당 경로에 접근해서 실행하지 않아도 동작함을 확인할 수 있다.)  
- IDE를 사용한다면 환경변수를 설정해줄 필요가 없다.(하지만 서버에서는 GUI는 리소스만 차지하며 CLI환경에서 작업할 일이 많으므로 환경변수도 잡아두는것을 추천한다.)  


[환경변수 참고](https://hyoje420.tistory.com/7)

## classpath 옵션  
```
-classpath(cp) path(파일 절대 경로):
 컴파일러가 컴파일 하기 위해서 필요로 하는 참조할 클래스 파일들을 찾기 위해서 컴파일시 파일 경로를 지정해주는 옵션. 
 
 ex) Hello.java파일이 C:Java 디렉터리에 존재하고, 필요한 클래스 파일들이 C:JavaEngclasses에 위치한다면,
 javac -classpath C:JavaEngclasses C:JavaHello.java 

만약 참조할 클래스 파일들이 C:JavaEngclasses외의 다른 디렉터리에도 존재한다면 C:JavaKorclasses 일경우, 
javac -classpath C:JavaEngclasses;C;JavaKorclasses C:JavaHello.java

그리고, 현재 디렉터리역시 포함하고 싶다면,
javac -classpath .;C:JavaEngclasses;C;JavaKorclasses C:JavaHello.java

기본적으로, dos에서는 .는 현재 디렉터리를 의미하고, ..는 현재 디렉터리의 상위디렉터리를 의미한다. 
또한 classpath 대신 단축어인 cp를 사용해도 된다.  
javac -cp C:JavaEngclasses C:JavaHello.java 
```

[클래스패스 옵션 정리](https://payoff.tistory.com/401)


## 접근지시자  

* 접근제어자  
-public : 누구나 접근 가능하다.  
-protected : 같은 패키지에 있거나, 상속 받는 경우 사용할 수 있다.  
-package-private : 아무 접근제어자를 적어주지 않은 경우(디폴트)이며, package-private라 불린다. 같은 패키지 내에서 접근 가능하다.  
-private : 해당 클래스 내에서만 접근 가능하다.  

* 허용 범위  
private < default(package-private) < protected < public  





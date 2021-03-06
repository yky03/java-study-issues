# 목표
자바가 제공하는 다양한 연산자를 학습하세요.

# 학습할 것
- 산술 연산자
- 비트 연산자
- 관계 연산자
- 논리 연산자
- instanceof
- assignment(=) operator
- 화살표(->) 연산자
- 3항 연산자
- 연산자 우선 순위
- (optional) Java 13. switch 연산자


- - -

## 산술 연산자
*, /, +, - : 사칙연산을 하기 위한 연산자
% : 나머지 값을 활용하기 위한 연산자

## 비트 연산자
-비트 논리 연산자  
~ : 해당 데이터의 각 비트를 변환한다.(비트 부정, ) 1->0 ,0->1  
& : AND  
| : OR  
^ : XOR  

-비트 이동 연산자(쉬프트연산자)    
x<<y : 정수 x의 각 비트를 y만큼 왼쪽으로 이동시킵니다. (빈자리는 0으로 채워집니다.)   
x>>y : 정수 x의 각 비트를 y만큼 오른쪽으로 이동시킵니다. (빈자리는 정수 a의 최상위 부호비트와 같은 값으로 채워집니다.      
x>>>y : 정수 x의 각 비트를 y만큼 오른쪽으로 이동시킵니다. (빈자리는 0으로 채워집니다.)   

## 관계 연산자
==, !=, >, <, >=, <=, instanceof : 값의 비교(참과 거짓을 판단하는 연산자)  

## 논리 연산자
!, &, |, &&, || : 논리적NOT, AND, OR연산  

## instanceof
객체타입을 확인하는데 사용하는 연산자 : 형변환이 가능한 지 해당 여부를 true or false로 반환.  
왼쪽 참조 변수값이 오른쪽 참조 변수 타입이면 참, 아니면 거짓  

ex)  
```
class A{}  
class B extends A{}
...
A a = new A();
B b = new B();

a instanceof A : true
b instanceof A : true
a instanceof B : false // 부모가 있어야 자식이 있는데, 부모가 자식이 되려했기 때문에 false
b instanceof B : true
```

[참고1](https://neul-carpediem.tistory.com/20)
[참고2](https://blog.naver.com/hsm622/222150928707)
[참고3](https://improver.tistory.com/140)
[참고4](https://coding-factory.tistory.com/521)

## assignment(=) operator
: 대입 또는 할당 연산자라고 부른다. 오른쪽의 피연산자를 왼쪽의 피연산자를 왼쪽의 피연산자의 값으로 할당한다.  
자기 자신에 담을 경우 사용한다.  
ex)  
int a = 10;  
System.our.println(a+=10); //20  

## 화살표(->) 연산자
JAVA8부터 람다식 구문 중 일부인 화살표 구문을 사용하여 코드 수를 줄이고 가독성을 향상시킬 수 있음.  

* 익명의 인터페이스 구현에도 용이함  
```
Runnable r = new Runnable() {
            @Override
            public void run() {
                System.out.print("Run method");
            }
        };
```
->
```
Runnable r = ()-> System.out.print("Run method");
```

## 3항 연산자
(조건식) ? (A) : (B)  
조건식이 true 이면 A, false이면 B 실행 -> if else 문 대신 사용하면 코드가 깔끔해짐.  

## 연산자 우선 순위
* 연산에는 아래와 같이 우선순위가 있음.(괄호 등을 묶어서 표현하면 가독성 향상)  

1)최우선 연산자 : . , [] , ()  
2)단항 연산자 : ! , ~ , +/- , ++/-- , (case 자료형) , instanceof  
3)산술 연산자 : + , - , * , / , %  
4)Shift 연산자 : << , >> , >>>  
5)관계 연산자 : < , > , <= , >= , == , !=  
6)비트 연산자 : & , | , ^  
7)논리 연산자 : && , ||  
8)삼항 연산자 : (조건항) ? 참 항 : 거짓 항  
9)배정 대입 연산자 : = , *= , /= , %= , += , -= , <<== , >>== , >>>==  
10)증감 후위 연산자 : ++/--  
11)순차 연산자 : ,  


## (optional) Java 13. switch 연산자
java7 -> 정수 뿐만 아니라 문자열 사용 가능  
java12 -> Switch Expressions -> 콜론(:)과 break문의 조합이 아닌 화살표(->)만으로 작성이 가능하며 리턴도 가능.  
JAVA13 -> Switch 피드백을 받아 수정 -> break로 값을 반환하는 문법이 yield로 변경됨.  
13까지는 preview , 14부터 표준화
기존 switch문은 그대로 있고, switch operator 가 추가된것!
ex)
```
int code = 1;
String result = switch (code) {
  case 1: break "1번";
  case 2: break "2번";
  default : break "디폴트";
  }
```
->
```
int code = 1;
String result = switch (code) {
  case 1: yield "1번";
  case 2: yield "2번";
  default : yield "디폴트";
  }
```

[Document참고1](http://openjdk.java.net/jeps/325)
[Document참고2](https://openjdk.java.net/jeps/354)
[참고3](http://openjdk.java.net/jeps/325)
[참고4](http://openjdk.java.net/jeps/325)
[참고5](https://namu.wiki/w/Java)
[참고6](https://blog.naver.com/hsm622/222150928707)




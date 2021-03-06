
# 목표  
자바의 람다식에 대해 학습하세요.  

# 학습할 것(필수)  
- 람다식 사용법  
- 함수형 인터페이스  
- Variable Capture  
- 메소드, 생성자 레퍼런스  

# Today Keyword  
- 

- - -

## 람다식 사용법   

-람다식이란  
: 식별자 없이 실행가능한 함수.  

```java
(매개변수, ...) -> { 실행문 ... }
```
```java
@FunctionalInterface
interface Say{
    int someting(int a,int b);
}
class Person{
    public void hi(Say line) {
	int number = line.someting(3,4);
	System.out.println("Number is "+number);
    }
}
```
```java
// 람다식 사용x
Person rin = new Person();
rin.hi(new Say() {
    public int someting(int a, int b) {
	System.out.println("My Name is Coding-Factory");
	System.out.println("Nice to meet you");
	System.out.println("parameter number is "+a+","+b);
	return 7;
    }
});
```
```java
// 람다식 사용o
Person rin = new Person();
rin.hi((a,b) ->{
	System.out.println("This is Coding-Factory!");
	System.out.println("Tank you Lamda");
	System.out.println("parameter number is "+a+","+b);
    return 7;
});
```

[람다식참고](https://coding-factory.tistory.com/265)  


## 함수형 인터페이스   

-함수형 인터페이스란  
: 1개의 추상 메소드를 갖고 있는 인터페이스를 말한다.  

```java
public interface FunctionalInterface {
    public abstract void doSomething(String text);
}
```
-> 함수형 인터페이스를 사용하는 이유는 자바의 람다식은 함수형 인터페이스로만 접근이 되기 때문이다.  
```java
// 익명 클래스
FunctionalInterface func = new FunctionalInterface() {
    @Override
    public void doSomething(String text) {
        System.out.println(text);
    }
};
func.doSomething("do something");
```
```java
// 람다식
public interface FunctionalInterface {
     public abstract void doSomething(String text);
}

FunctionalInterface func = text -> System.out.println(text);
func.doSomething("do something");
// 실행 결과
// do something
```

- 기본 함수형 인터페이스  
```
Runnable : 인자를 받지 않고 리턴값도 없는 인터페이스입니다.  
Supplier : 인자를 받지 않고 T 타입의 객체를 리턴합니다.  
Consumer : T 타입의 객체를 인자로 받고 리턴 값은 없습니다.  
Function<T, R> : T타입의 인자를 받고, R타입의 객체를 리턴합니다.  
Predicate : T타입 인자를 받고 결과로 boolean을 리턴합니다.  
```
[함수형인터페이스참고](https://codechacha.com/ko/java8-functional-interface/)  


## Variable Capture   
```
변수 캡쳐 (Variable Capture)
- 로컬 변수 캡쳐
    - final이거나 effective final인 경우에만 참조할 수 있다.
        - 변수를 변경되도록 수정해보면 이것은 effective final 인지 아닌지 확인가능하다.
        - 변경이 되면 effective final 이 아니게 되며, 람다에서 사용할 수 없게 된다.
    - 그렇지 않을 경우 concurrency 문제가 생길 수 있어서 컴파일이 불가능하다.
- effective final
    - 이것 역시 자바 8 부터 지원하는 기능으로 "사실상" final인 변수.
    - final 키워드 사용하지 않은 변수를 익명 클래스 구현체 또는 람다에서 참조할 수 있다.
- 익명 클래스 구현체와 달리 "쉐도윙" 하지 않는다.
    - 익명 클래스는 새로 스콥을 만들지만, 람다는 람다를 감싸고 있는 스콥과 같다.

*익명 클래스에 컨텍스트를 넘겨주는 것이 클로저입니다. 
*컴파일러는 이 필요한 정보를 복사해서 넘겨주는데 이를 Variable capture 라고 합니다.
```

[변수캡쳐 참고](https://www.notion.so/758e363f9fb04872a604999f8af6a1ae)  
[람다변수범위참고](https://futurecreator.github.io/2018/08/02/java-lambda-variable-scope/)  

## 메소드, 생성자 레퍼런스  

- 메서드,생성자 레퍼런스란  
:   
함수의 축약형이다.  
명시적으로 메서드를 참조함으로써 가독성을 높이고, 람다를 편리하게 사용할 수 있게 해준다.   
메서드, 생성자 레퍼런스는 메서드명 앞에 구분자(::)를 붙이는 방식으로 사용한다.  

```java
(String s) -> System.out.println(s)

System.out::println // method reference !!
```
```java
Consumer<String> func = text -> System.out.println(text);
func.accept("Hello");
// 실행 결과
// Hello
```
```java
Consumer<String> func = System.out::println;
func.accept("Hello");
// 실행 결과
// Hello
```

```
메소드 레퍼런스는 사용하는 패턴에 따라 다음과 같이 분류할 수 있습니다.

Static 메소드 레퍼런스 : Static method를 메소드 레퍼런스로 사용하는 케이스입니다.  
Instance 메소드 레퍼런스 : Instance 메소드 레퍼런스의 메소드는 static이 아니고 객체의 메소드를 의미합니다.
Constructor 메소드 레퍼런스 : Constructor 메소드 레퍼런스는 Constructor를 생성해주는 코드입니다.
[메소드 레퍼런스 예제 참고할것](https://codechacha.com/ko/java8-method-reference/)  
```

[메소드 레퍼런스 이해하기](https://codechacha.com/ko/java8-method-reference/)  
[메서드, 생성자 레퍼런스 정의와 생성방법](https://m.blog.naver.com/gngh0101/221346557597)  

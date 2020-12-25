# 목표
자바의 상속에 대해 학습하세요.

# 학습할 것(필수)  
- 자바 상속의 특징    
- super 키워드  
- 메소드 오버라이딩  
- 다이나믹 메소드 디스패치 (Dynamic Method Dispatch)  
- 추상 클래스  
- final 키워드  
- Object 클래스  


- - -


## 자바 상속의 특징

-상속이란 
: 부모 클래스에서 정의된 필드와 메소드를 자식 클래스가 물려받는 것.(extends 키워드를 사용하며 부모클래스의 기능을 사용할때 사용)  

-자바 상속의 특징  
: 다중상속을 지원하지 않는다, 상속의 횟수에 제한이 없다, 최상위 클래스는 Object클래스이다.(자바의 모든 클래스들은 java.lang.Object의 자손 클래스)  

-접근지정자 protected  
: 같은 패키지 혹은 다른 패키지라도 상속받은 클래스에서 접근 가능하다.  


[상속참고](https://jyoel.tistory.com/39)  


## super 키워드  

-super  
:  부모 클래스 객체를 즉시 참조할때 사용하는 참조변수  
super.변수명 -> 부모 클래스 멤버변수 접근  
super.method() -> 부모 클래스 메소드 호출    
super() -> 부모 클래스 생성자 호출  


## 메소드 오버라이딩  

*자바에서 다형성을 지원하는 방법으로 메소드 오버로딩과 오버라이딩이 있다.    

-다형성  
: 객체지향 개념에서의 다형성이란 여러 가지 형태를 가질 수 있는 능력, 자바에서는 한 타입의 참조변수로 여러 타입의 객체를 참조할 수 있도록 하는 능력.  

-오버라이딩  
: 상위 클래스가 가지고 있는 메소드를 하위 클래스에서 상속받아 메소드를 재정의 하는 기술을 오버라이딩(@Override)이라 함.  

-오버로딩  
: 같은 이름의 함수를 여러 개 정의하고, 매개변수의 유형과 개수를 다르게 하여 다양한 유형의 호출에 응답하게 한다.  


[리팩토링구루 다형성으로 조건문 개선](https://refactoring.guru/replace-conditional-with-polymorphism)    
[오버로딩 오버라이딩 차이](https://hyeonstorage.tistory.com/185)  

## 다이나믹 메소드 디스패치  

-다이나믹 메소드 디스패치  
: 재정의 된 메서드에 대한 호출이 컴파일 타임이 아닌 런타임에 해석되는 프로세스로써,    
오버라이드 된 메서드가 참조에 의해 호출될때 java는 참조하는 객체 유형에 따라 실행할 메소드 버전을 판별합니다.  

```
class Animal {
   public void move() {
      System.out.println("Animals can move");
   }
}

class Dog extends Animal {
   public void move() {
      System.out.println("Dogs can walk and run");
   }
}

public class TestDog {

   public static void main(String args[]) {
   
      Animal a = new Animal(); // Animal reference and object
      Animal b = new Dog(); // Animal reference but Dog object

      a.move(); // runs the method in Animal class
      b.move(); // runs the method in Dog class
   }
}
```


[다이나믹 메소드 패치 정의](https://riptutorial.com/ko/java/topic/9204/%EB%8B%A4%EC%9D%B4%EB%82%B4%EB%AF%B9-%EB%A9%94%EC%86%8C%EB%93%9C-%EB%94%94%EC%8A%A4%ED%8C%A8%EC%B9%98)  
[다이나믹 메소드 패치 예제](https://www.tutorialspoint.com/Dynamic-method-dispatch-or-Runtime-polymorphism-in-Java)  


## 추상 클래스  

-추상클래스  
: 클래스 내 '추상 메소드'가 하나 이상 포함되거나 abstract로 정의된 경우를 말합니다.  

-인터페이스  
: 모든 메소드가 추상 메소드인 경우(자바8에서는 default 키워드를 이용해서 일반 메소드의 구현도 가능!)  

추상 클래스와 인터페이스는 상속받는 클래스 혹은 구현하는 인터페이스 안에 있는 추상 메소드를 구혐하도록 강제한다.  
비슷한 기능이지만 존재의 목적이 다르다.  

추상 클래스는 그 추상클래스를 상속받아서 기능을 이용하고, 확장!시키는 데 있습니다.  
반면 인터페이스는  함수의 껍데기만 있는데 그 함수의 구현을 강제!하기 위해서 입니다.(구현 객체의 같은 동작 보장, 팀 프로젝트시 기능별로 미리 작업 가능)  


[추상클래스와 인터페이스의 차이](https://brunch.co.kr/@kd4/6)  

## final 키워드  

-final  
: 여러 컨텍스트에서 단 한번만 할당될 수 있는 entity를 정의할 때 사용.  

-적용범위
1) final 변수  
: 객체, 변수값 변경 불가능  
2) final 메소드  
: 상속받은 클래스에서 오버라이드가 불가능(자바코어 라이브러리에 많음)    
3) final 클래스  
: 상속 자체가 안됨(유틸형식(String 클래스도)의 클래스나 여러 상수 값을 모아둔 Constants 클래스에 많이 사용)  



## Object 클래스  

Object : 자바 API의 모든 클래스와 사용자가 정의한 모든 클래스의 최상위 클래스이다.(모든 자바 클래스들은 Object클래스로부터 상속받음)  

즉 어떤 클래스에서든 객체에서 접근 및 오버라이딩이 가능하다는 의미도 된다.  

평소에 잘 보지 않던 최상위 클래스의 메소드 및 Document를 참고하면 좋을 것 같다.  

```
boolean equals(Object ob) : 두 객체가 같은지 비교  
String toString() : 현재 객체의 문자열을 반환  
protected Object clone() : 객체를 복사  
protected void finalize() : 가비지 컬렉션 직전에 객체의 리소스를 정리할때 호출  
Class getClass() : 객체의 클래스형을 반환  
int hashCode() : 객체의 코드값을 반환  
void notify() : wait된 스레드 실행을 재개할 때 호출  
void norifyAll() : wait된 모든 스레드 실행을 재개할 때 호출  
void wait() : 스레드를 일시적으로 중지할 때 호출  
void wait(long timeout) : 주어진 시간만큼 스레드를 일시적으로 중지할 때 호출  
void wait(long timeout, int nanos) : 주어진 시간만큼 스레드를 일시적으로 중지할 때 호출  
```

![233BA837529F47710A](https://t1.daumcdn.net/cfile/tistory/233BA837529F47710A)


[Object 정의 및 메소드 참고](https://hyeonstorage.tistory.com/178)  
[Object API Document](https://docs.oracle.com/javase/7/docs/api/java/lang/Object.html)  




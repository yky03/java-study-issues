# 목표  
자바의 인터페이스에 대해 학습하세요.  

# 학습할 것(필수)  
- 인터페이스 정의하는 방법  
- 인터페이스 구현하는 방법  
- 인터페이스 레퍼런스를 통해 구현체를 사용하는 방법  
- 인터페이스 상속  
- 인터페이스의 기본 메소드 (Default Method), 자바 8    
- 인터페이스의 static 메소드, 자바 8  
- 인터페이스의 private 메소드, 자바 9  

# Today Keyword  
- 
-
-

- - -


## 인터페이스 정의하는 방법  

- 인터페이스 정의 및 선언방법    
: 동일한 목적 하에 동일한 기능을 수행하게끔 강제하는것. 
(interface 키워드로 만들고 implements 키워드를 사용해 하위클래스에서 구현한다. -> 다형성을 이용하여 개발코드 수정을 줄이고 유지보수성을 높인다.)  

```
public interface RemoteControl {
    //상수
    int MAX_VOLUME = 10;
    int MIN_VOLUME = 0;
    
    //추상 메소드
    void turnOn();                                    //메소드 선언부만 작성 (추상 메소드) , 컴파일 과정에서 public abstract 자동으로 붙음
    void turnOff();            
    void setVoulume(int volume);
    
    //디폴트 메소드
    default void setMute(boolean mute) {              //실행 내용까지 작성  , 컴파일 과정에서 public 자동으로 붙음
        if(mute) {
            System.out.println("무음 처리합니다.");
        } else {
            System.out.println("무음 해제합니다.");
        }
    }
    
    //정적 메소드
    static void changeBattery() {                     // 컴파일 과정에서 public 자동으로 붙음
        System.out.println("건전지를 교환합니다.");
    }
}

```

[인터페이스 선언 및 구현 방법 예제](https://gbs1995.tistory.com/15)

## 인터페이스 구현하는 방법  

```
public class 구현클래스명 implements 인터페이스명 {

@Override
//인터페이스에 선언된 추상 메소드의 실체 메소드 선언(강제)

@Override
//인터페이스에 선언된 디폴트 메소드의 실체 메소드 선언(선택)

}
```

- 인터페이스 활용    
: DB커넥션 등 인터페이스 껍데기를 만들고 mysql커넥션구현체, oracle커넥션구현체 를 각각 만들어 필요할때 구현체만 대체해서 사용 가능.  

[인터페이스 사용 이유](https://mainia.tistory.com/2139)


## 인터페이스 레퍼런스를 통해 구현체를 사용하는 방법  

인터페이스의 경우 내부 추상 메서드가 정의 되어있지 않으므로 new 키워드를 통해 인스턴스화 할 수 없으며 이를 구현한 구현체를 사용하여 사용할 수 있다.  
상속과 마찬가지로 인터페이스와 이를 구현한 구현체에서 다형성이 적용되어질 수 있기에 인터페이스 자체를 타입으로 지정할 수 있다.  

```
interface Human {
  void say()
}

class User implements Human {
  @Override
  public void say() {
    System.out.println("Hi!")
  }
}
```
```
class App {
  public static void main(String[] args) {
    Human jongnan = new User();
    jongnan.say();
  }
}
```
[레퍼런스 구현체 예제 참고](https://github.com/jongnan/Java_Study_With_Whiteship/blob/master/week8/week8.md)


## 인터페이스 상속  

인터페이스 또한 인터페이스로부터 extends 키워드를 사용하여 상속을 받을 수 있다. 클래스 상속과는 다르게 상속에 있어 애매함이 없기에 다중 상속이 된다.  

```
interface Human {
  void move();
  void say();
}

interface Weapon {
  void attack();
}

interface Citizen extends Human {
}

interface Soldier extends Human, Weapon {
}
```

[인터페이스 상속 예제 참고](https://github.com/jongnan/Java_Study_With_Whiteship/blob/master/week8/week8.md)


## 인터페이스의 기본 메소드 (Default Method), 자바 8  

인터페이스에 신규 메소드를 모든 구현클래스 수정없이 추가하고자 할 때 사용한다.  
구현클래스에서 오버로이딩도 가능하며, 전부 구현하지 않고 필요한 클래스만 구현해도 컴파일오류가 발생하지 않는다.  

```
public interface IPrinterable {
    public void print();
    public default void cancel(){
        System.out.println("Printer Cancel");
    };
}
```

[디폴트 메소드 예제](http://blog.naver.com/PostView.nhn?blogId=wideeyed&logNo=220838738788)  

## 인터페이스의 static 메소드, 자바 8  

java8부터 static 메소드도 선언할 수 있게 됨.  

```
//선언부
public interface ICalculator {
 
    int add(int x, int y);
    int sub(int x, int y);
 
    default int mul(int x, int y) {
 
        return x * y;
    }
 
    static void print(int value) {
 
        System.out.println(value);
    }
}
```
```
//호출부
//static 메소드를 사용하는데 주의해야할 점은 기존 클래스의 static 메소드처럼 class이름.메소드로 호출하는게 아니라 interface이름.메소드로 호출해야 함
public class CalcTest {
 
    public static void main(String[] args) {
 
        ICalculator cal = new Calculator();
 
        // Calculator.print(100);
          ICalculator.print(100); // interface의 static 메소드는 반드시 interface명.메소드 형식으로 호출
    }
}
```

[static 메소드 예제](https://atoz-develop.tistory.com/entry/JAVA-8-interface-default-%ED%82%A4%EC%9B%8C%EB%93%9C%EC%99%80-static-%EB%A9%94%EC%86%8C%EB%93%9C)  

## 인터페이스의 private 메소드, 자바 9  

*java9 부터 사용 가능하며 아래의 특징이 있다.
- 메소드 body가 있고 abstract 가 아니다.  
- static 이거나 non-static 일 수 있다.  
- 구현 클래스와 인터페이스가 상속되지 않는다.  
- 인터페이스에서 다른 메소드를 호출 할 수 있다.  

```
public interface MyInterface{
 private static int staticMethod(){
  return 42;
 }
 private int nonStaticMethod(){
  return 0;
 }
}
```

Java 9부터 중복적인 코드를 제거하고 캡슐화를 위해 private 메소드를 사용할 수 있게 되었다. 8에서 default와 static 메소드를 사용하는데 있어 중복적인 코드가 존재할 수 있다.  
이를 없애기 위해서는 똑같이 default와 static 메소드를 사용하여 없앨 수 있지만, 외부에서 접근이 가능하다. 이러한 점을 보완하기 위해 private 키워드를 사용하여 메소드를 정의할 수 있다.  

```
interface User {
  default void walk() {
    printMove(); //재사용
  }
  
  default void run() {
    printMove(); //재사용
  }
  
  default void stop() {
    System.out.println("멈춤!");
  }
  
  private void printMove() {
    System.out.println("움직임 시작!");
  }
}
```

[private 메소드 예제](https://github.com/jongnan/Java_Study_With_Whiteship/blob/master/week8/week8.md)  
[인터페이스 변화 히스토리](https://flyburi.com/605)







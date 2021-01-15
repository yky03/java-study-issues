# 목표  
자바의 예외 처리에 대해 학습하세요.  

# 학습할 것(필수)  
- 자바에서 예외 처리 방법 (try, catch, throw, throws, finally)  
- 자바가 제공하는 예외 계층 구조  
- Exception과 Error의 차이는?  
- RuntimeException과 RE가 아닌 것의 차이는?  
- 커스텀한 예외 만드는 방법  

# Today Keyword  
- Chained Exception : https://wisdom-and-record.tistory.com/46
- try - with - resoucres : https://sujl95.tistory.com/62
-

- - -


## 자바에서 예외 처리 방법 (try, catch, throw, throws, finally)   

```
try{

    예외 발생 가능성이 있는 문장들;

}catch(예외 타입1 매개변수명){

    예외타입1의 예외가 발생할 경우 처리 문장들;

}catch(예외 타입 n 매개변수명){

    예외타입 n의 예외가 발생할 경우 처리 문장들;

}finally{

    항상 수행할 필요가 있는 문장들; // 무조건 타는 로직

}

static void callDriver() throws ClassNotFoundException{
  예외(Exception)이 발생한 메소드를 호출 한 곳으로 예외 객체를 넘기는 방법 (throws)  
}

class 예외 클래스 이름 extends Exception
 사용자 정의 예외 생성 (throw)  // 기존의 예외 클래스로 처리할 수 없다면 사용자만의 예외 클래스를 작성하여 발생 시킬 수 있음, 예외 최상위 클래스인 java.lang.Exception 클래스를 상속
```

[예외처리 참고](https://hyeonstorage.tistory.com/203)  


## 자바가 제공하는 예외 계층 구조  

![21476F3E577E91080E](https://t1.daumcdn.net/cfile/tistory/21476F3E577E91080E)

| | Checked Exception | Unchecked Exception |
|------|---|---|
|클래스|Exception 클래스의 자손들 중 Runtime Exception을<br/> 제외한 모든 클래스|Runtime Exception 클래스와<br/> 자손 클래스|
|처리여부|반드시 예외 처리 해야함|명시적 처리 강제하지 않음|
|확인시점|컴파일단계|실행단계|
|예외발생시 트랜잭션처리|rollback 하지 않음|rollback함|
|대표예외|-IOException<br/> -SqlException|-NullPointerException<br/>-IllegalArgumentException<br/>-IndexOutOfBoundException<br/>-SystemException|


[계층구조, 예외발생 롤백](https://itmining.tistory.com/9)  
[자바 예외 구분 checkedException, UncheckedException](https://madplay.github.io/post/java-checked-unchecked-exceptions)  

## Exception과 Error의 차이는?  

- 오류 
: 에러, 예외 두가지로 구분할 수 있다.  

- Error  
: 컴파일 시 문법적인 오류와 런타임시 널포인트 참조와 같은 오류로 프로세스에 심각한 문제를 야기 시켜 프로세스를 종료 시킬 수 있다.  

- Exception  
: 컴퓨터 시스템의 동작 도중 예기치 않았던 이상 상태가 발생하여 수행 중인 프로그램이 영향을 받는 것.  


[에러와 예외 차이](https://drcarter.tistory.com/153)  

## RuntimeException과 RuntimeException이 아닌 것의 차이는?  

-RuntimeException에 해당하는 예외 클래스는 Unchecked Exception이 존재한다.   
Unchecked Exception은 실행 시점에서 확인이 가능하고 예외 처리를 강제하지 않기 때문에 컴파일 시점에서는 확인 할 수 없다.   
예외 발생 시 트랜잭션을 roll-back한다.  

-RuntimeException이 아닌 것에는 Checked Exception이 있다.  
Checked Exception에 경우 치명적인 예외 상황이 발생하기 때문에 반드시 예외를 처리해줘야 한다.  
컴파일 시점에서 확인 할 수 있다. 또한 예외 발생 시 트랜잭션을 roll-back하지 않는다.  


[RE 차이](https://hyeonic.tistory.com/57)  


## 커스텀한 예외 만드는 방법  

```
public class MyException extends Exception{
  MyException(String msg){
   super(msg);
  }
}
```
```
//실행부
new MyException("Custom Exception");
```

[커스텀 예외](https://i-am-clap.tistory.com/12)  

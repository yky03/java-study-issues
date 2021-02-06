
# 목표  
자바의 애노테이션에 대해 학습하세요.

# 학습할 것(필수)  
- 애노테이션 정의하는 방법  
- @retention  
- @target  
- @documented  
- 애노테이션 프로세서  

# Today Keyword  
-  


- - -


## 애노테이션 정의하는 방법  

- 애노테이션이란  
: 컴파일 과정과 실행 과정에서 코드를 어떻게 컴파일하고 처리할 것인지를 알려주는 정보입니다.  
@ + 어노테이션 명으로 사용할 수 있습니다.  

- 어노테이션 타입 정의  
```java
public @interface myanotation {
   //Element 라는 것을 멤버로 가질 수 있음
   String myname();
   int myage();
}

//사용부 예시
@myanotation(myName = “김석진” , myAge = 33)
```

- 어노테이션 유지정책  
: 사용 용도에 따라 해당 어노테이션을 어디까지 유지할 것인지 지정하는 것입니다.  
소스상에만 유지할것인지, 컴파일된 클래스까지 유지할 것이지, 런타임 시에도 유지할 것인지 정해야함.  
```
// java.lang.annotation.RetentionPolicy 열거 상수로 다음과 같이 정의되어 있습니다.
SOURCE : 소스상에서만 어노테이션을 유지하고 .class파일로 변경된 후에는 흔적이 남아 있지 않을 경우입니다. 주로 소스 코드를 분석할 때 사용되는 범위입니다. 
CLASS : 바이트 코드에도 어노테이션 정보를 유지하는 것입니다. 추후 다루겠지만 리플렉션을 이용해서 어노테이션 정보를 얻을 수 없습니다. 
RUNTIME : 리플렉션을 이용해서 런타임시에 어노테이션 정보를 얻을 수 있습니다.
// 리플렉션(Reflecion)이란 간단히 말해 Runtime시에 클래스의 메타 정보를 얻는 기능  
```

-  Runtime 시 어노테이션 정보 사용하기  
```
// java.lang.reflect 패키지의 Field, Constructor, Method 타입의 배열을 얻어야 합니다.
getFields() :  필드 정보를 Field배열인 Field[]로 리턴한다.
getConstructors() :  생성자 정보를 Constructor배열인 Constructor[]로 리턴한다. 
getDeclaredMethods() : 메서드 정보를 Method배열인 Method[]로 리턴한다. 

// 이후 Field, Constructor, Method 객체가 가지고 있는 다음 메서드를 통해 적용된 어노테이션 정보를 얻을 수 있습니다.
isAnnotationPresent( Class<? extends Anotation> annotationClass )
: 지정한 어노테이션이 적용되었는지 여부를 boolean타입으로 리턴합니다. Class에서 호출했을 때 상위 클래스에 적용된 경우도 true를 리턴합니다.
getAnnotation( Class<T> annotationClass )
: 지정한 어노테이션이 적용되어 있으면 해당 어노테이션을 리턴하고 없을 시 null을 리턴합니다. 마찬가지로 상위 클래스에 적용되어도 같습니다.
getAnnotations()
: 적용된 모든 어노테이션을 Annotation[] 배열로 받습니다. 상위클래스도 포함합니다. 
getDelaredAnnotations()
: 상위 클래스를 제외한 직접 적용된 어노테이션 배열을 리턴합니다.

```

[어노테이션 참고](https://honbabzone.com/java/java-anontation/)  

## @retention  

- Meta Annotations
: 커스텀 어노테이션을 만들 수 있음.  

```
**@Retention - 어노테이션의 범위라고 할 수 있겠습니다. 어떤 시점까지 어노테이션이 영향을 미치는지 결정합니다.**
@Documented - 문서에도 어노테이션의 정보가 표현됩니다.
@Target - 어노테이션이 적용할 위치를 결정합니다.
@Inherited - 이 어노테이션을 선언하면 자식클래스가 어노테이션을 상속 받을 수 있습니다.
@Repeatable - 반복적으로 어노테이션을 선언할 수 있게 합니다.
```
```
@Retention
어노테이션의 Life Time입니다.
Class
바이트 코드 파일까지 어노테이션 정보를 유지한다.
하지만 리플렉션을 이용해서 어노테이션 정보를 얻을 수는 없다.
Runtime
바이트 코드 파일까지 어노테이션 정보를 유지하면서 리플렉션을 이용해서 런타임시에 어노테이션 정보를 얻을 수 있다.
Source
Compile 이후로 삭제되는 형태
https://docs.oracle.com/javase/8/docs/api/java/lang/annotation/RetentionPolicy.html
```
```java
import java.lang.annotation.ElementType;
import java.lang.annotation.Retention;
import java.lang.annotation.RetentionPolicy;
import java.lang.annotation.Target;

/**
 * String 문자열을 주입하기 위해 선언하는 어노테이션입니다.
 * FIELD에만 선언가능하고 JVM이 어노테이션 정보를 참조합니다.
 */
@Target(ElementType.FIELD)
@Retention(RetentionPolicy.RUNTIME)
public @interface StringInjector {
    String value() default "This is StringInjector.";
}
```

[자바 어노테이션 retention](https://jdm.kr/blog/216)  

## @target  

: 해당 사용자가 만든 어노테이션이 부착될 수 있는 타입(클래스,생성자,메서드 등..)을 지정하는 것이다.  

- 어노테이션 적용 대상  
java.lang.annotation.**ElementType**에 열거 상수로 아래와 같은 값들이 있습니다.  
```
TYPE : 클래스, 인터페이스, 열거 타입에 적용합니다.
ANNOTATION_TYPE : 어노테이션에 적용합니다.
FIELD : 필드에 적용합니다. 
CONSTRUCTOR: 생성자에 적용합니다. 
METHOD: 메서드에 적용합니다.
LOCAL_VARIABLE: 로컬 변수에 사용합니다.
PACKAGE: 패키지에 사용합니다.
```
```java
// 어노테이션이 적용될 대상을 지정할 때 @Target 어노테이션을 사용합니다.
@Target(value = { ElementType.FIELD , ElementType.METHOD })
public @interface myanotation {
    String value();
}
```

[자바 어노테이션 target](https://seeminglyjs.tistory.com/249)  

## @documented  

: @Documented 어노테이션이 지정된 대상의 JavaDoc 에 이 어노테이션의 존재를 표기하도록 지정.

```java
java.lang.annotation.Documented 

@Documented 
public @interface MyAnnotation { 

}

@MyAnnotation public class MySuperClass { ... }
```

[자바 어노테이션 document](https://hamait.tistory.com/314)

## 애노테이션 프로세서  

- 어노테이션 프로세싱이란  
: 자바 컴파일러의 컴파일 단계에서, 유저가 정의한 어노테이션의 소스코드를 분석하고 처리하기 위해 사용되는 hook.  
컴파일 에러나 컴파일 경고를 만들어내거나, 소스코드(.java)와 바이트코드(.class)를 내보내기도 한다.  

- 어노테이션 프로세서란  
: 컴파일 단계에서 어노테이션을 분석하고 처리하기 위해 자바 컴파일러에 동본된 hook.  

[어노테이션 프로세서란](https://kkambi.tistory.com/84)  
[어노테이션 프로세서 만들기](https://better-dev.netlify.app/java/2020/09/08/thejava_17/)  


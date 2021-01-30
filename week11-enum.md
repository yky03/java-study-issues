# 목표  
자바의 열거형에 대해 학습하세요.  

# 학습할 것(필수)  
- enum 정의하는 방법  
- enum이 제공하는 메소드 (values()와 valueOf())  
- java.lang.Enum  
- EnumSet  

# Today Keyword  
- enum 클래스는 java.lang.Enum 클래스를 상속 받는다.  
- 타입세이프티(회사의 애플, 과일의 애플 비교?)  
- querydsl(type safety 문자열 작성보다는 )    
- @Enumerated(EnumType.ORDINAL)  -> - @Enumerated(EnumType.String)   
  jpa에서 ordinal 지양, Fruit fruit;  
- enum 순서 정의할때(1,2,3 이면 중간에 순서 추가 어려움)
```java
enum Fruit{
 Kiwi(10),
 Banana(20),
 Apple(30)
}
```

- - -


## enum 정의하는 방법  

-enum class 란
jdk 1.5 부터 추가되었으며, 열거형이라고 불립니다.  
서로 연관된 상수들의 집합을 의미합니다.  

enum 의 장점
: 코드단순, 가독성 향상, 타입안정성 보장 등.

```java
public enum DevType {
    MOBILE, WEB, SERVER
}
...
public class Developer {
     
    public String name;
    public int career;
    public enum DevType {
 
        MOBILE, WEB, SERVER
    }
 
}
...
Developer developer = new Developer();
System.out.println(developer.type);
```

[enum참고](https://limkydev.tistory.com/50)  


## enum이 제공하는 메소드 (values()와 valueOf())  

- values() : 열거된 모든 원소를 배열에 담아 순서대로 반환  
```java
enum Type {
    WALKING, RUNNING, TRACKING, HIKING
}
public class Shoes {
    public String name;
    public int size;
    public Type type;
     
    public static void main(String[] args) {
        for(Type type : Type.values()) {
            System.out.println(type);
        }
    }
}
# 결과
WALKING
UNNING
TRACKING
HIKING
```

- ordinal() : 원소에 열거된 순서를 정수 값으로 반환  
```java
enum Type {
    WALKING, RUNNING, TRACKING, HIKING
}
public class Shoes {
    public String name;
    public int size;
    public Type type;
     
    public static void main(String[] args) {
        Shoes shoes = new Shoes();
         
        shoes.name = "나이키";
        shoes.size = 230;
        shoes.type = Type.RUNNING;
         
        System.out.println(shoes.type.ordinal());
         
        Type tp = Type.HIKING;
         
        System.out.println(tp.ordinal());
    }
}
# 결과
1
3
```

- valueOf() : 매개변수로 주어진 String과 열거형에서 일치하는 이름을 갖는 원소를 반환  
(주어진 String과 일치하는 원소가 없는 경우 IllegalArgumentException 예외 발생)  
```java
enum Type {
    WALKING, RUNNING, TRACKING, HIKING
}
public class Shoes {
     
    public static void main(String[] args) {
        Type tp1 = Type.WALKING;
        Type tp2 = Type.valueOf("WALKING");
         
        System.out.println(tp1);
        System.out.println(tp2);
    }
}
 # 결과
WALKING
WALKING
```

*참고
- 클래스의 static final 이용해서 열거형 선언하기  
```java
class Type {
    static final String WALKING = "워킹화";
    static final String RUNNING = "러닝화";
    static final String TRACKING = "트래킹화";
    static final String HIKING = "등산화";
}
 
public class Shoes {
    public static void main(String[] args) {
        String w = Type.WALKING;
        System.out.println(w);
    }
}
# 결과
워킹화
```

[enum메소드 참고](https://www.opentutorials.org/module/1226/8025)  

## java.lang.Enum  

jdk7 : https://docs.oracle.com/javase/7/docs/api/java/lang/Enum.html  
jdk11 : https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/Enum.html

- enum Method 종류  
name  
ordinal  
toString  
equals  
hashCode  
clone  
compareTo   
getDeclaringClass     
valueOf  
finalize   

- enum 확장  
```java
public enum InvoiceStatus {
  DRAFT {
    @Override public void action(InputMessage inputMessage) {
      invoiceFileService.draft(inputMessage);
    }
  },
  VALID {
    @Override public void action(InputMessage inputMessage) {
      invoiceFileService.valid(eiInvoiceFileMessage);
    }
  },
  NOT_VALID {
    @Override public void action(InputMessage inputMessage) {
      invoiceFileService.notValid(eiInvoiceFileMessage);
    }
  };
  //+20 more values...
  @Autowired
  InvoiceFileService invoiceFileService;
  public abstract void action(InputMessage inputMessage);
}
```
```java
invoice.getStatus().action(inputMessage);
```

[enum뿌리를 찾아서](https://www.nextree.co.kr/p11686/)    
[우아한형제들 enum활용기](https://woowabros.github.io/tools/2017/07/10/java-enum-uses.html)  
[Spring을 위한 jdk11 enum확장](https://www.python2.net/questions-208712.htm)  

## EnumSet 
- 특수한 set을 구현으로써 enumset은 내부적으로 bit vector로 표현되서 매우 효율적.  
```java
EnumSet<Planet> planets = EnumSet.of(Planet.NEPTUNE, Planet.EARTH);
EnumSet<Planet> all = EnumSet.allOf(Planet.class);
EnumSet<Planet> none = EnumSet.noneOf(Planet.class);
EnumSet<Planet> inner = EnumSet.range(Planet.MERCURY, Planet.EARTH);
```
```java
//동기식으로 사용할때는 Collections.synchronizedSet 사용
Set<MyEnum> s = Collections.synchronizedSet(EnumSet.noneOf(MyEnum.class));
```
```
//HashMap 대신 EnumMap을 사용한다
EnumMap은 EnumSet처럼 HashMap보다 안정적이고 효율적이다
Map<Planet, String> enumMap = new EnumMap<>(Planet.class);
```
```java
E/enumMap을 동기적으로 사용할때는 Collections.synchronizedMap 사용
Map<EnumKey, V> m = Collections.synchronizedMap(new EnumMap<EnumKey, V>(...));
```

[enumset,enummap](https://johngrib.github.io/wiki/java-enum/)
[enum 활용](https://www.baeldung.com/a-guide-to-java-enums)

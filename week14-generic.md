
# 목표  
자바의 제네릭에 대해 학습하세요.  

# 학습할 것(필수)  
- 제네릭 사용법  
- 제네릭 주요 개념 (바운디드 타입, 와일드 카드)  
- 제네릭 메소드 만들기  
- Erasure  

# Today Keyword  
- 

- - -

## 제네릭 사용법  

- 제네릭이란  
- 클래스 내부에서 사용할 데이터 타입을 인스턴스로 생성할 때 확정해주고 타입 체크를 할 때 Generic을 사용한다.  
- 제너릭을 사용할려면 선언하려는 클래스 옆에 <>안에 데이터 타입을 사용하고 <>안에 지정된 데이터 타입으로 T의 데이터 타입이 결정된다.  
- java5 부터 사용할 수 있다.
- 컬렉션이 담을 수 있는 타입을 컴파일러에 미리 알려줄 수 있다.  
- 그래서 컴파일러는 알아서 형변환 코드를 추가할 수 있게 되고, 엉뚱한 타입의 객체를 넣으려는 시도를 컴파일 과정에서 차단하여 더 안전하고 명확한 프로그램을 만들어 준다.  

```java
class Person<T> {
    public T name;
    private String age;
    
    public String getAge() {
        return age;
    }
    
    public void setAge(String age) {
        this.age = age;
    }
    
    public T getName() {
        
        return name;
    }
    
    public void setName(T name) {
        this.name = name;
    }
}
```

```java
public class GenericTest {
    public static void main(String[] args) {
        Person<String> p1 = new Person<String>();
        p1.setName("String ktko");
        
        Person<StringBuilder> p2 = new Person<StringBuilder>();
        p2.setName(new StringBuilder("StringBuilder ktko"));
        
        System.out.println(p1.getName());
        System.out.println(p2.getName());
    }
}
```

[자바 제네릭 사용법](https://ktko.tistory.com/entry/%EC%9E%90%EB%B0%94-%EC%A0%9C%EB%84%A4%EB%A6%ADGeneric-%EA%B0%9C%EB%85%90%EA%B3%BC-%EC%82%AC%EC%9A%A9%EB%B2%95-1%ED%83%84)
[-제너릭의 종류,와일드카드 <T>, <?>, <? extends T>, <? super T>](https://blog.naver.com/ykycome00/222101321226)   

## 제네릭 주요 개념 (바운디드 타입, 와일드 카드)  

```java
public void drawAll(List< ? extends Shape > shapes)
{ ... }

// 위의 extends 부분이 바운디드 와일드카드라 한다.  
// drawAll()은 Shape, Circle, Rectangle 객체의 List만을 파라미터로 받게 된다. 그 이외에는 모두 컴파일 오류가 난다.  
// 위 경우처럼 바운디드 와일드카드를 사용하면, 단순히 와일드카드를 사용하는 것보다는 타입의 범위를 좀 더 명확히 할 수 있게 된다.  

// 그러나 주의할 점은 shapes가 정확히 어떤 타입의 객체를 담고 있는지에 대해서는 알 수가 없다는 것이다.  
// 만약 drawAll()에서 shapes.add(0, new Rectangle()); 을 넣는다고 할 때, 컴파일러는 오류를 내뱉는다.  
// -> 제네릭 메소드로 해결이 가능하다.  
```

[제너릭](http://qyleekr.blogspot.com/2010/05/java-generics.html)  

## 제네릭 메소드 만들기  

```java
// 1) 와일드 카드
static void fromArrayToCollection(
   Object[] a, Collection< ? > c) {
      for (Object o : a) {
         c.add(o); // comple time error
      }
}

// 2) 제네릭  
static < T > void fromArrayToCollection(
    T[] a, Collection< T > c) {
      for (T o : a) {
         c.add(o); // correct
   }
}

// 첫번째 예제는 콜렉션 c에 Object 배열인 a를 더하려는 코드이다. 그러나 콜렉션 c는 c가 담을 수 있는 타입이 언논이기 때문에, Object 타입의 o를 파라미터로 넘길 수가 없다.
// 반면, 두번째 예제는 제너릭 메소드라는 방법을 사용해서 첫번째 예제에서 발생한 문제를 해결한 경우이다.

// 그렇다면, 언제 제너릭 메소드를 사용하고, 언제  와일드카드를 사용해야 할까?
// 와일드카드는 타입 파라미터가 폴리모피즘을 지원하고자 할 때 사용한다. 반면, 제너릭 메소드는 타입 파라미터가 다른 파라미터의 타입이나 리턴 타입 사이의 종속성을 명시해야 할 때 사용한다.
```

## Erasure(소거)    

소거란 원소 타입을 컴파일 타입에만 검사하고 런타임에는 해당 타입 정보를 알 수 없는 것입니다.  
한마디로, 컴파일 타임에만 타입 제약 조건을 정의하고, 런타임에는 타입을 제거한다는 뜻입니다.  

배열 -> 공변,구체화타입(자신의 타입 정보를 런타임에도 알고 있는 것)  
제네릭 -> 불공변(자기와 타입이 같은 것만 같다고 인식하는 특징),비구체화타입(런타임에는 소거 되기 때문에 컴파일 타임보다 정보를 적게 가지는 것)    

[제네릭 Type Erasure](https://devlog-wjdrbs96.tistory.com/263)  

## Plus. [이펙티브 자바] 아이템 26 로 타입은 사용하지 말라.  

-용어 정리  
: 클래스와 인터페이스 선언에 타입 매개변수가 쓰이면, 이를 제네릭 클래스 혹은 제네릭 인터페이스라 한다.  
ex) List<E> -> List 라고도 자주 사용함.    

제네릭 타입 = 제네릭 클래스 + 제네릭 인터페이스.  
  
각각의 제네릭 타입은 일련의 매개변수화 타입을 정의한다.    
-> 먼저 클래스 이름이 나오고, 이어서 꺾쇠괄호 안에 실제 타입 매개변수들을 나열한다.    
-> 제네릭 타입을 하나 정의하면 그에 딸린 로 타입도 함께 정의된다.    
-> 로 타입이란 제네릭 타입에서 타입 매개변수를 전혀 사용하지 않을 때를 말한다.    

제네릭 지원 전에 컬렉션을 다음과 같이 사용했다.(따라하지 말것!)  
```java
// Stamp 인스턴스만 취급한다.
private final Collection stamps = ...;

// 실수로 동전을 넣는다.
stamps.add(new Coin(...)); // "unchecked call"경고를 내뱉는다.

// 컬렉션에서 이 동전을 다시 꺼내기 전에는 오류를 알아채지 못한다.
// 반복자의 로 타입 (따라 하지 말것! - 컴파일 시점이 아닌 런타임때 발견됨)
for (Iterator i = stamps.iterator(); i.hasNext(); ){
     // 인스턴스가 스탬프가아닌 코인이기 때문에 ClassCastException을 던진다.
     Stamp stamp = (Stamp) i.next(); 
     stamp.cancel();
}
```

```java
// 매개변수화된 컬렉션 타입으로 타입 안정성(type safety)을 확보하자!
// 코인을 넣을경우 컴파일 단계에서 체크 가능!
private final Collection<Stamp> stamps = ...;
```

```java
// 제네릭 타입을 쓰고 싶지만 실제 타입 매개변수가 무엇인지 신경 쓰고 싶지 않다면 물음표(?)를 사용하자.
// 비한정적 와일드 카드 타입을 사용할 경우 타입 안전하며 유연하다.
static int numElementsIncommon(Set<?> s1, Set<?> s2){ ... }
```

```
BUT 예외로 class 리터럴에는 로 타입을 써야 한다!
자바 명세는 class 리터럴에 매개변수화 타입을 사용하지 못하게 했다.

* 핵심 정리
로 타입을 사용하면 런타임에 예외가 일어날 수 있으니 사용하면 안 된다.  
로 타입은 제네릭이 도입되기 이전 코드와의 호환성을 위해 제공될 뿐이다.  
빠르게 훑어보자면, Set<Object>는 어떤 타입의 객체도 저장할 수 있는 매개변수화 타입이고,  
Set<?>는 모종의 타입 객체만 저장할 수 있는 와일드카드 타입이다. 그리고 이들의 로 타입인 Set은 제네릭  
타입 시스템에 속하지 않는다. Set<Object>와 Set<?>는 안전하지만, 로 타입인 Set은 안전하지 않다.  



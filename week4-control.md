# 목표
자바가 제공하는 제어문을 학습하세요.

# 학습할 것(필수)
- 선택문  
- 반복문  

# 과제(옵션)  

- 과제 0. JUnit 5 학습하세요.  
인텔리J, 이클립스, VS Code에서 JUnit 5로 테스트 코드 작성하는 방법에 익숙해 질 것.    
이미 JUnit 알고 계신분들은 다른 것 아무거나!    
더 자바, 테스트 강의도 있으니 참고하세요~    

- 과제 1. live-study 대시 보드를 만드는 코드를 작성하세요.  
깃헙 이슈 1번부터 18번까지 댓글을 순회하며 댓글을 남긴 사용자를 체크 할 것.  
참여율을 계산하세요. 총 18회에 중에 몇 %를 참여했는지 소숫점 두자리가지 보여줄 것.  
Github 자바 라이브러리를 사용하면 편리합니다.  
깃헙 API를 익명으로 호출하는데 제한이 있기 때문에 본인의 깃헙 프로젝트에 이슈를 만들고 테스트를 하시면 더 자주 테스트할 수 있습니다.  

- 과제 2. LinkedList를 구현하세요.  
LinkedList에 대해 공부하세요.  
정수를 저장하는 ListNode 클래스를 구현하세요.  
ListNode add(ListNode head, ListNode nodeToAdd, int position)를 구현하세요.  
ListNode remove(ListNode head, int positionToRemove)를 구현하세요.  
boolean contains(ListNode head, ListNode nodeTocheck)를 구현하세요.  

- 과제 3. Stack을 구현하세요.  
int 배열을 사용해서 정수를 저장하는 Stack을 구현하세요.  
void push(int data)를 구현하세요.  
int pop()을 구현하세요.  

- 과제 4. 앞서 만든 ListNode를 사용해서 Stack을 구현하세요.  
ListNode head를 가지고 있는 ListNodeStack 클래스를 구현하세요.  
void push(int data)를 구현하세요.  
int pop()을 구현하세요.  

- 과제 5. Queue를 구현하세요.
배열을 사용해서 한번  
ListNode를 사용해서 한번.  

- - -


## 선택문  
제어문 : 코드의 실행 흐름(순서)을 제어하는 구문.  
선택문: if 문, if ~ else 문, switch 문 

*Tip -> goto문  
```
loops:
for( int i = 0; i < MAX_I; i++ ) {
  //to do
  break loops;
}
```

if 구문은 사용자가 자주 사용하는 기능 순서대로 조건문을 써 주면 성능에 큰 도움이 될 것 같습니다.   
하지만 사용자가 여러 기능을 유사한 빈도로 사용한다면 switch를 이용하는 것이 더 좋을 듯합니다. 

[if vs switch speed](https://stackoverflow.com/questions/445067/if-vs-switch-speed)  
[if vs switch speed!](https://yeopbox.com/%EC%9E%90%EB%B0%94-%EC%B5%9C%EC%A0%81%ED%99%94-%EC%97%B0%EA%B5%AC-if%EC%99%80-switch-%EC%A1%B0%EA%B1%B4%EB%AC%B8-%EC%97%B0%EC%82%B0-%EC%86%8D%EB%8F%84-%EB%B9%84%EA%B5%90-int/)

## 반복문  
반복문: for문, while문  
java5부터 향상된 for문(foreach문 사용가능)

```
List<Integer> list = Arrays.asList(1, 2, 3, 4, 5);

for(Integer i : list){
    System.out.println(i);
}

```
```
int[] array = new int[10]; //int 형 배열

//좋지 못한 코드  
for(int i=0; i<array.length(); i++){
}
```
```
//리팩토링
int arrLength = array.length(); //length 함수를 반복문에서 계속 호출하지 않도록
for(int i=0; i<arrLength; i++){
}
or
//인덱스가 필요하지 않은 경우 아래 방법을 추천
for(int i : array){
}
```


[리스트돌릴땐 foreach를 쓰자](https://multifrontgarden.tistory.com/130?category=471239)

- - -

## 과제0 JUnit5 학습 

Junit : 어노테이션 사용, 단정문(Assertion)을 통해 수행 결과를 판별할 수 있는 java의 단위 테스팅 도구중의 하나.  
JUnit5 : 2017년부터 도입되었으며 JAVA8 이상일때 사용 가능.  
Spring Boot 2.2+ 버전의 프로젝트에서는 기본적으로 JUnit5 의존성 추가됨, 그 외의 경우는 pom.xml에 junit5 의존성 추가.  

- 기본 애노테이션  

@Test  
: 해당 메서드가 테스트 메소드임을 나타냄.  

@BeforeAll/@AfterAll  
: 현재 클래스의 어떤 테스트 메소드도 (시작하지 않은 상태/완료된 이후) 에서 해당 메소드를 실행해야함을 나타냄.  

@BeforeEach/@AfterEach  
: 현재 클래스에 속한 모든 테스트 메소드의 테스트 (수행 전/수행후) 마다 해당 메소드를 실행해야함을 나타냄.  

@Disabled  
: 이 테스트 클래스나 테스트 메소드를 사용하지 않음을 나타냄.  


- Assertion(단정문)  
: 테스트를 만약 성공하지 않으면 실패처리 하기 위해서 사용.  

- Assumtion(가정문)  
: 특정 상황에서만 테스트를 실행하고자 할때, 혹은 특정 상황에서 실행하지 않고자 할떄 사용하는 키워드.(local환경 등에서만 동작 등)  


[단정문 참고링크1](https://it-mesung.tistory.com/45)
[단정문 참고링크2](https://reiphiel.tistory.com/entry/junit5-features)
[단정문,가정문 참고링크](https://sabarada.tistory.com/80)
[애노테이션 참고링크](https://awayday.github.io/2017-11-11/junit5-03/)



## 과제1 live-study 대시 보드를 만드는 코드 작성
...

## 과제2 Linkedlist 구현

-연결리스트(링크드리스트)   

: 각 노드(마디,교점)가 데이터와 포인터를 가지고 한 줄로 연결되어 있는 방식으로 데이터를 저장하는 자료 구조이다.  
노드의 포인터가 다음이나 이전의 노드와의 연결을 담당하게 된다.  

![Singly_linked_list](https://upload.wikimedia.org/wikipedia/commons/3/37/Singly_linked_list.png)  


-역사  
: 1955~1956년 랜드 연구소에서 개발되었음.  

-종류  
1)단일 연결 리스트  
: 각 노드에 자료 공간과 한 개의 포인터 공간이 있고, 각 노드의 포인터는 다음 노드를 가리킨다.  

![400px-Single_linked_list](https://upload.wikimedia.org/wikipedia/commons/thumb/9/9c/Single_linked_list.png/400px-Single_linked_list.png)  


2)이중 연결 리스트  
: 단일 연결 리스트와 비슷하지만, 포인터 공간이 두 개가 있고 각각의 포인터는 앞의 노드와 뒤의 노드를 가리킨다.  

![400px-Doubly_linked_list](https://upload.wikimedia.org/wikipedia/commons/thumb/c/ca/Doubly_linked_list.png/400px-Doubly_linked_list.png)  

3)원형 연결 리스트  
: 일반적인 연결 리스트에 마지막 노드와 처음 노드를 연결시켜 원형으로 만든 구조이다.  

![400px-Circurlar_linked_list](https://upload.wikimedia.org/wikipedia/commons/thumb/9/98/Circurlar_linked_list.png/400px-Circurlar_linked_list.png)  


```

//LinkedList 구현


```













[위키백과 연결리스트란](https://ko.wikipedia.org/wiki/%EC%97%B0%EA%B2%B0_%EB%A6%AC%EC%8A%A4%ED%8A%B8)



# 목표
자바의 프리미티브 타입, 변수 그리고 배열을 사용하는 방법을 익힙니다.

# 학습할 것
- 프리미티브 타입 종류와 값의 범위 그리고 기본 값
- 프리미티브 타입과 레퍼런스 타입
- 리터럴
- 변수 선언 및 초기화하는 방법
- 변수의 스코프와 라이프타임
- 타입 변환, 캐스팅 그리고 타입 프로모션
- 1차 및 2차 배열 선언하기
- 타입 추론, var


- - -

## 프리미티브 타입 종류와 값의 범위 그리고 기본 값

- 프리미티브 타입(스택에 저장, 직접 데이터를 담는 타입)
논리형: boolean(1byte) | 기본값: false | 범위: true,false
정수형: byte(1byte) | 기본값: 0 | 범위: -128 ~ 127
정수형: short(2byte) | 기본값: 0 | 범위: -32,768 ~ 32,767
정수형: int(4byte) | 기본값: 0 | 범위: -2,147,483,648 ~ 2,147,483,647(21억대)
정수형: long(8byte) | 기본값: 0L | 범위: -9,223,372,036,854,775,808 ~ 9,223,372,036,854,775,807
실수형: float(4byte) | 기본값: 0.0F | 범위 : (3.4 * 10의-38승) - (3.4 * 10의38승)의 근사값
실수형: double(8byte) | 기본값: 0.0 | 범위 : (1.7 * 10의-308승) - (1.7 * 10의308승)의 근사값
문자형: char(2byte) 유니코드 | 기본값: '\u0000' | 범위 : 0 ~ 65,535

- 레퍼런스 타입(힙 메모리에 저장, 기본값 NULL, 객체의 주소값 4byte)
클래스타입(new 생성), 인터페이스타입, 배열타입(new 생성), 열거타입

[참고](https://gbsb.tistory.com/6)

## 프리미티브 타입과 레퍼런스 타입

- 프리미티브 타입과 레퍼런스 타입의 가장 큰 차이점은 메모리 참조 타입인가?(C언어에서는 포인터의 개념)
- 프리미티브 타입 : 실제 값을 저장
- 레퍼런스 타입 : 값이 아닌 객체를 참조하기 위한 어떤 특정한 참조 값을 저장(객체이름(id=xx))
- call by value and call by reference for java 
: 자바의 특성은 객체를 메소드로 넘길 때 객체를 참조하는 지역변수의 실제 주소를 넘기는 것이 아니라!
그 지역변수가 가리키고 있는 힙 영역의 객체를 가리키는 새로운 지역변수를 생성하여! 그 것을 통하여 같은 객체를 가리키도록 하는 방식


[참고1](https://m.blog.naver.com/PostView.nhn?blogId=highkrs&logNo=220242895539&proxyReferer=https:%2F%2Fwww.google.com%2F)
[참고2](https://blog.naver.com/PostView.nhn?blogId=chogahui05&logNo=221483768407&categoryNo=16&parentCategoryNo=14&viewDate=&currentPage=&postListTopCurrentPage=&isAfterWrite=true)
[참고3](https://hyoje420.tistory.com/6)

## 리터럴
상수 : 변하지 않는 변수
리터럴 : 데이터 그 자체로써 변하지 않는 변수에 넣는 데이터
ex) final int a =1; // 상수: a , 리터럴 : 1

[참고](https://mommoo.tistory.com/14)

## 변수 선언 및 초기화하는 방법
int a;
a=3;

*변수의 이름으로 예약어는 사용하지 않으며 카멜표기법 사용을 추천
*카멜표기법이란 : 낙타의 등모습을 닮았다고 해서 카넬표기법임 -> 시작은 소문자로 시작하지만 여러 단어가 이어지는 경우 첫 단어를 제외하고 각 단어의 첫 글자만 대문자로 지정하는 방식
ex) int colorFrame;

[참고](http://blog.naver.com/PostView.nhn?blogId=jhnyang&logNo=221574080889)

## 변수의 스코프와 라이프타임

-스코프란 : 변수 혹은 레퍼런스의 유효범위( java에서는 블록({}) 안의 범위 )
-전역 변수 : 클래스 내의 모든 장소에서 사용 가능
-지역 변수 : 메소드 내에서 선언하는 변수는 메소드 안에서만 사용 가능
-라이프타임 : 변수가 생성되고 소멸되는 시간
 ->인스턴스(전역) 변수 : 객체가 생성되고 객체가 메모리에 살아있는! 동안이 Lifetime
 ->클래스 변수 : 클래스가 초기화되고 프로그램이 끝날때!까지가 Lifetime
 ->로컬(지역) 변수 : 변수 선언 이후 부터 블록을 벗어날 때!까지가 Lifetime
  ->Example
    public class scope_and_lifetime {
        int num1, num2;   //Instance Variables
        static int result;  //Class Variable
        int add(int a, int b){  //Local Variables
            num1 = a;
            num2 = b;
            return a+b;
        }
        public static void main(String args[]){
            scope_and_lifetime ob = new scope_and_lifetime();
            result = ob.add(10, 20);
            System.out.println("Sum = " + result);
        }
    }

[참고1](https://velog.io/@dion/%EB%B0%B1%EA%B8%B0%EC%84%A0%EB%8B%98-%EC%98%A8%EB%9D%BC%EC%9D%B8-%EC%8A%A4%ED%84%B0%EB%94%94-2%EC%A3%BC%EC%B0%A8-%EC%9E%90%EB%B0%94-%EB%8D%B0%EC%9D%B4%ED%84%B0-%ED%83%80%EC%9E%85-%EB%B3%80%EC%88%98-%EA%B7%B8%EB%A6%AC%EA%B3%A0-%EB%B0%B0%EC%97%B4#%EB%B3%80%EC%88%98%EC%9D%98-%EC%8A%A4%EC%BD%94%ED%94%84%EC%99%80-%EB%9D%BC%EC%9D%B4%ED%94%84%ED%83%80%EC%9E%84)
[참고2](https://www.learningjournal.guru/article/programming-in-java/scope-and-lifetime-of-a-variable/)

## 타입 변환, 캐스팅 그리고 타입 프로모션

타입별 크기 순서(byte순) : byte(1) < short(2) < int(4) < long(8) < float(4) < double(8)
-> 작은타입은 큰 타입안에 들어갈 수 있음(프로모션)
but, 강제 타입 변환(캐스팅)을 통해 저장할 수 있음.
-> 작은 크기 타입 = (작은 크기 타입)큰 크기 타입

프로모션(자동 형 변환)이란 
: 크기가 더 작은 자료형을 더 큰 자료형에 대입할 때, 자동으로 작은 자료형이 큰 자료형으로 변환되는 현상

[참고1](https://kephilab.tistory.com/27)
[참고2](https://m.blog.naver.com/PostView.nhn?blogId=haejoon90&logNo=220781157092&proxyReferer=https:%2F%2Fwww.google.com%2F)

## 1차 및 2차 배열 선언하기

배열 : 선형 자료구조중 하나로 동일한 타입의 연관된 데이터를 메모리에 연속적으로 저장하여 하나의 변수에 묶어서 관리하기 위한 자료구조로써 인덱스를 통해 데이터에 접근.5

- 1차원 배열
int[] arr = new int[5]; //크기가 5인 int형 배열 생성
arr[0] = 1; arr[1] = 2; arr[2] = 3; arr[3] = 4; arr[4] = 5;
int[] arr = {1,2,3,4,5}; //크기가 5인 int형 배열 선언 및 값 초기화

- 2차원 배열 ( 2중 for문으로 주로 값 세팅)
int[][] array = new int[2][3]; //2행 3열
array[0][0] = 4; array[0][1] = 5; array[0][2] = 6; array[1][0] = 7; array[1][1] = 8; array[1][2] = 9;
int[][] array = {{4,5,6},{7,8,9}}; //2행 3열


## 타입 추론, var

타입추론이란 : 타입이 정해지지 않은 병수의 타입을 컴파일러가 유추하는 기능.(JAVA10 이상 문법)
장점 : 생산성 향상, 가독성 좋음, 인스턴스 객체의 타입이 바뀌어도 생성되는 클래스부분은 수정하지 않아도 됨, Object대안 가능,람다식,익명클래스 등에서 활용 가능.
단점 : IDE에따라 바로 타입 확인이 어려움, 해당 위치만 보고 어떤 타입의 데이터가 할당될지 알 수 없을수도 있음.(-> 변수명을 var checkList 등 의미있는 네이밍으로 어느정도 보완 가능)

[참고](https://dev.to/composite/java-10-var-3o67)






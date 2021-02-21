
# 목표  
자바의 Input과 Ontput에 대해 학습하세요.

# 학습할 것(필수)  
- 스트림 (Stream) / 버퍼 (Buffer) / 채널 (Channel) 기반의 I/O
- InputStream과 OutputStream
- Byte와 Character 스트림
- 표준 스트림 (System.in, System.out, System.err)
- 파일 읽고 쓰기 

# Today Keyword  
- 허건밀러 의자  
- 유닉스의 탄생 책  
- IO 데코레이터 패턴 예시  
- 직렬화  
- 바이트코드    

- - -


## 스트림 (Stream) / 버퍼 (Buffer) / 채널 (Channel) 기반의 I/O

- 입출력이란?  
I/O란 Input과 Output의 약자로 입력과 출력, 간단히 줄여서 입출력이라고 한다.   
입출력은 컴퓨터 내부 또는 외부의 장치와 프로그램간의 데이터를 주고받는 것을 의미한다.   
예를 들면 키보드로부터 데이터를 입력받는다든가 System.out.println()을 이용해서 화면에 출력한다던가 하는 것이 가장 기본적인 입출력의 예이다.  

- 스트림  
: 두 대상을 연결하고 데이터를 연결하는 것으로 바이트기반스트림과 보조스트림, 문자기반스트림 등이 있다.  

- 버퍼란?  
임시 저장공간을 의미한다.  
A와 B가 서로 입출력을 수행하는데 있어서 속도차이를 극복하기 위해 사용하는 임시 저장을 의미한다.  

- NIO  
New Input Output 패키지 java7부터 만들었음.  
-> 일관성 있는 클래스 설계를 바로 잡고 비동기 채널 등의 네트워크 지원.  
-> IO는 스트림 방식이지만, NIO는 채널방식이다.  
-> NIO의 Channel은 Buffer에 있는 내용을 다른 어디론가 보내거나 다른 어딘가에 있는 내용을 Buffer로 읽어들이기 위해 사용된다.  


[스트림,버퍼,채널 기반의 IO](https://velog.io/@ljs0429777/13%EC%A3%BC%EC%B0%A8-%EA%B3%BC%EC%A0%9C-IO)

## InputStream과 OutputStream
: 자바에서 데이터는 Stream 을 통해 입출력됨.  

데이터를 입력받을때 : InputStream  
-> 바이트 기반 입력 스트림의 최상위 클래스로 추상 클래스이다.  
모든 바이트 기반 입력 스트림은 이 클래스를 상속받아서 만들어짐.  
InputStream 클래스에는 바이트 기반 입력 스트림이 기본적으로 가져야 할 메소드들이 정의되어 있음.  

데이터를 출력할때 : OutputStream  
-> 바이트 기반 출력 스트림의 최상위 클래스로 추상 클래스이다.  
모든 바이트 기반 출력 스트림 클래스는 이 클래스를 상속받아서 만들어짐.  
OutputStream 클래스에는 모든 바이트 기반 출력 스트림이 기본적으로 가져야할 메소드가 정의되어 있음.  


[InputStream Outputstream 개념](https://develop-im.tistory.com/54)  

## Byte와 Character 스트림

Byte Stream은 데이터를 있는 그대로 송수신 하는 Stream.  
그리고 이 Byte Stream을 이용하여 문자를 파일에 저장하는 것도 가능하다.  
Byte Stream은 데이터를 Byte 단위로 주고받는 것을 말한다.  
```
Byte Stream들

- PrintStream
- InputStream, OutputStream
- ByteArrayInputStream, ByteArrayOutputStream
- FileInputStream, FileOutputStream
- FilterInputStream, FilterOutputStream
- ObjectInputStream, ObjectOutputStream
- PipedInputStream, PipedOutputStream
- BufferedInputStream, BufferedOutputStream
- DataInputStream, DataOutputStream
-  ... 기타 등등
```

Character Stream은 Reader와 Writer를 달고 있다.  
두 문자단위로 인코딩 처리를 하는 Stream들이다. Character Stream들은 다음과 같다.  
```
Character Stream들

- PrintWriter
- Reader, Writer
- BufferedReader, BufferedWriter
- CharArrayReader, CharArrayWriter
- FilterReader, FilterWriter
- InputStreamReader, OutputStreamWriter
- FileReader, FileWriter
- PipedReader, PipedWriter
- StringReader, StringWriter
- ... 기타 등등
```

[바이트 스트림과 문자 스트림](https://story.stevenlab.io/96)  

## 표준 스트림 (System.in, System.out, System.err)

-System.in  
: 표준 입출력 스트림은 미리 생성된 스트림이기 때문에 사용자가 직접 생성할 필요는 없다.  
PrintStream in은 키보드의 입력을 받아들이기 위해서 사용하는 입력 스트림이다.  

-System.out, System.err  
System.out 와 System.err은 둘 다 PrintStream이다.  
printStream은 출력을 편하게 하기 위해서 제공되는 출력 전용의 바이트 스트림이다.  

```
System.err.println("err 출력");
System.out.println("out 출력");
---
run:
err 출력    //단지 색이 다르다 //넷빈
out 출력
BUILD SUCCESSFUL (total time: 0 seconds)
---
-차이점  
1.err은 버퍼링을 지원하지 않는다. 이것은 err가 보다 정확하고 빠르게 출력되어야 하기 때문일것이다.   
버퍼링은 하던 도중 프로그램이 멈추면 버퍼링된 내용은 출력되지 않기 때문이다.  
(자바에서는 버퍼링을 둘다 지원하지만 내부에서 자동으로 버퍼비우기를 해 버림)  

2. err는 그냥 프로그램이 출력되는 콘솔창에만 출력된다.  
```

[표준스트림 system](https://m.blog.naver.com/PostView.nhn?blogId=force44&logNo=130096406237&proxyReferer=https:%2F%2Fwww.google.com%2F)  

## 파일 읽고 쓰기  

- FileWriter,FileReader  
: 자바 내장 클래스인 FileWriter,  BufferedWriter(파일읽기) , FileReader,BufferedReader(파일쓰기)를 사용가능.  


// File Write  
```java
package com.supercoding;


import java.io.*;

//파일 쓰고 읽기 테스트
public class FileMake {

    public static void main(String[] args) {

        /***********************FILE WRITE***********************/
        try( //요기서 객체를 생성하면 try종료 후 자동으로 close처리됨
                //true : 기존 파일에 이어서 작성 (default는 false임)
                FileWriter fw = new FileWriter( "coding532.txt" ,true);
                BufferedWriter bw = new BufferedWriter( fw );
                )
        {
            bw.write("손흥민"); //버퍼에 데이터 입력
            bw.newLine(); //버퍼에 개행 삽입
            bw.write("이강인");
            bw.newLine();
            bw.flush(); //버퍼의 내용을 파일에 쓰기
        }catch ( IOException e ) {
            System.out.println(e);
        }

        File f = new File("coding532.txt");
        // 파일 존재 여부 판단
        if (f.isFile()) {
            System.out.println("coding532.txt 파일이 있습니다.");
        }
    }

}
```

// File Read  
```java
package com.supercoding;


import java.io.*;

//파일 쓰고 읽기 테스트
public class FileMake {

    public static void main(String[] args) {

        /***********************FILE WRITE***********************/
        try( //요기서 객체를 생성하면 try종료 후 자동으로 close처리됨
                //true : 기존 파일에 이어서 작성 (default는 false임)
                FileWriter fw = new FileWriter( "coding532.txt" ,true);
                BufferedWriter bw = new BufferedWriter( fw );
                )
        {
            bw.write("손흥민"); //버퍼에 데이터 입력
            bw.newLine(); //버퍼에 개행 삽입
            bw.write("이강인");
            bw.newLine();
            bw.flush(); //버퍼의 내용을 파일에 쓰기
        }catch ( IOException e ) {
            System.out.println(e);
        }

        File f = new File("coding532.txt");
        // 파일 존재 여부 판단
        if (f.isFile()) {
            System.out.println("coding532.txt 파일이 있습니다.");
        }

        /***********************FILE READ***********************/
        try(
                FileReader rw = new FileReader("coding532.txt");
                BufferedReader br = new BufferedReader( rw );
                ){
            
            //읽을 라인이 없을 경우 br은 null을 리턴한다.
            String readLine = null ;
            while( ( readLine =  br.readLine()) != null ){
                System.out.println(readLine);
            }
        }catch ( IOException e ) {
            System.out.println(e);
        }

    }

}
```

[자바 파일 읽고 쓰기](https://vmpo.tistory.com/63)



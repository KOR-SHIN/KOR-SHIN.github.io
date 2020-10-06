---
title : File Encoding(파일 인코딩)
layout : posts
categories :
 - JAVA
tag :
 - JAVA
---

## __File Encoding__
---
이전 포스팅에서 Endiong문제로 파일작업이 제대로 이루어지지 않는 경우에 대한 예제를 살펴보았다.<br>
오늘은 보조스트림을 통해 Encoding까지 지정하는 방법을 알아보려고 한다.<br>

## __TextFile Encoding__
---
`.txt`파일을 가지고 예제를 살펴보기 전에 인코딩을 설정하는 법을 알아보려고 한다.<br>

- .txt File Encoding
    - 자신이 원하는 경로에 새로만들기로 TextFile을 생성한다.
    - 원하는 내용을 입력하고 `다른이름으로 저장`버튼을 누른다.
    - 저장하기 전에 하단에 `인코딩`부분에서 자신이 테스트할 인코딩 유형을 선택한다.

오늘 테스트해볼 유형은 대표적인 한글인코딩 타입인 `UTF-8, ANSI 계열` 인코딩이다.

## __UTF-8__
---
UTF는 `Unicode Transformation Format`의 줄임말로 전세계 모든 문자를 컴퓨터에서 표현하고 다룰 수 있도록 설계된 산업표준이다.<br>
따라서 한글도 당연하게 표현가능하다.<br>
`UTF-8`은 문자열 집합과 인코딩 형태를 `8bit`단위로 한다는 의미를 가진다.<br>
UTF-8은 한 글자를 표현하기 위해 `1~4byte`를 사용하는데 이를 가변길이 인코딩 방식이라고 한다.<br>

## __ANSI__
---
`ANSI`는 `ASCII`의 확장이라고 할 수 있다<br>
`ANSI`는 `8bit`로 이루어져 있어서 `256`개의 문자를 표현할 수 있다.<br>
하지만 ANSI로 모든 언어를 표현할 수 없어서 `Code Page`라는 개념이 도입되었다.<br>
각 언어별로 Code 값을 지정하고, Code마다 다른 문자열 표를 의미하도록 약속을 한 것이다.<br>
그러므로 안시는 아래와 같이 표현할 수 있다.<br>
> ANSI = ASCII(7bit) + CodePage(1bit)

## __CP949__
---
`CP949`는 `ANSI`계열의 한글 인코딩 방식이다.<br>
`CP949`는 `Code Page 949`의 줄임말이고, `949`는 한국을 의미한다.<br>
유닉스계열의 완성형 코드 조합 인코딩방식인 `EUC-KR`을 확장하여 만든것이다.<br>
`EUC-KR`로는 표현할 수 있는 문자에 한계가 있었기 때문이다.<br>
`CP949`는 윈도우즈 계열에서 사용나온것이고, 마이크로소프트가 `EUC-KR`을 확장하여 만든것이라서 `MS949`라고 부르기도 한다.
인코딩 방식에 대해 더 궁금한 사람은 <a href="https://onlywis.tistory.com/2">내가 참고했던 블로그</a>에서 더 많은 내용을 읽어보는 것도 좋을것 같다.

## __File Encoding__
---
Encoding에 대해 설명하다보니 글이 길어졌다.<br>
이제 보조 스트림을 사용하여 File Encoding을 지정하는 방법에 대해 알아보자.<br>

`Sample Code`
```java
public static void main(String[] args) throws IOException {
		
	FileInputStream fis_ANSI = new FileInputStream("d:/testDir/ansi.txt");
	FileInputStream fis_UTF8 = new FileInputStream("d:/testDir/utf-8.txt");
	
	InputStreamReader isr_ANSI = new InputStreamReader(fis_ANSI, "MS949");
	InputStreamReader isr_UTF8 = new InputStreamReader(fis_UTF8, "UTF-8");
		
	int data_ANSI;
		
	System.out.println("<< ANSI ENCODING >>");
	while( (data_ANSI = isr_ANSI.read()) != -1) {
		System.out.print((char)data_ANSI);
	}
	System.out.println();
	System.out.println("----------------------");
		
	int data_UTF8;
		
	System.out.println("<< UTF-8 ENCODING >>");
	while( (data_UTF8 = isr_UTF8.read()) != -1) {
		System.out.print((char)data_UTF8);
	}
	System.out.println();
	System.out.println("----------------------");
}
```
`출력결과`
```
<< ANSI ENCODING >>
ANSI ENCODING TEST
안시계열 인코딩 테스트
----------------------
<< UTF-8 ENCODING >>
UTF-8 ENCODING TEST
유티에프-8 인코딩 테스트
----------------------
```
출력결과에서 볼 수 있듯이 한글입력도 깨짐없이 잘 나오는 것을 알 수 있다.<br>
<hr>

```java
	FileInputStream fis_ANSI = new FileInputStream("d:/testDir/ansi.txt");
	FileInputStream fis_UTF8 = new FileInputStream("d:/testDir/utf-8.txt");
	
	InputStreamReader isr_ANSI = new InputStreamReader(fis_ANSI, "MS949");
	InputStreamReader isr_UTF8 = new InputStreamReader(fis_UTF8, "UTF-8");
```
위에서 `FileInputStream`은 파일을 읽어오는 기반스트림이고, `InputStreaReader`는 파일을 읽을 때 어떤 인코딩을 사용할지를 정해주는 보조스트림이다.<br>
이전 예제에서 InputStreamReader를 사용하여 콘솔의 입력을 읽어온 적이 있는데 그 때는 생성자의 매개변수로 `System.in`을 넘겨주었었다.<br>
오늘 사용한 InputStreamReader는 Character-set까지 지정할 수 있는 매개변수가 2개인 생성자를 사용하여 객체를 생성했다.<br>

## __SUMMARY__
---
- Stream
	- 자바에서는 바이트기반 스트림과 문자기반 스트림을 제공한다.
	- 두 스트림의 최상위 부모는 `InputStream`, `OutputStream`이고, ㅣ이것을 상속한 클래스는 `FileIOStream`, `ByteArrayIOStream`, `PipedIOStream`이 있다.
	- Stream은 `FIFO(First Input First Output)`구조로 이루어져 있다.

- ByteArrayIOStream
	- ByteArrayInputStream은 byte기반의 배열을 읽어와 내부 버퍼에 저장한다.
	- ByteArrayOutputStream은 inputStread의 내용을 읽어와 내부 버퍼에 저장하고, 출력할 때 사용한다.
	- read()메서드는 기본적으로 1byte씩 데이터를 읽어온다.

- FileIOStream
	- File을 읽어오거나 File내부에 내용을 작성할 때 사용된다.
	- 보조스트림과 함께 사용하면 부가적인 기능을 추가할 수 있다.
	- 보조스트림은 기반 스트림없이 단독으로 사용될 수 없다.

## __P.S__
---
File클래스에 대한 예제가 부족한 것 같아 Sample Code만 있는 포스트를 업로드 하려고 합니다.<br>
File클래스의 사용법이나 더 많은 Method를 알고싶으신 분들은 참고하시면 좋을 것 같습니다.<br>

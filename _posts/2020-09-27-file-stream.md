---
title : File Stream(파일 스트림)
layout : posts
categories :
 - JAVA
tag :
 - JAVA
---

## __File__
---
자바에서는 File 클래스는 사용해서 간단한 파일작업을 할 수 있다<br>
오늘 예제에서는 파일을 생성하고, 읽어오는 방법에 대해 알아보려고 한다<br>
File클래스는 이름은 File이지만 Directory까지 다루는 클래스이다<br>

## __FileIOStream__
---
이전 예제에서 Stream에 대해 간단히 알아보았는데<br>
기억이 안난다면 <a href="https://kor-shin.github.io/java/bais-baos" target="_blank">Stream</a>을 가볍게 읽어오는것을 추천한다<br>

`Sample Code`
```java
public class FileTest {
	public static void main(String[] args) throws IOException {
		
		FileInputStream fis = null;
		FileOutputStream fos = null;
		InputStreamReader isr = new InputStreamReader(System.in);
		
		File dir = new File("d:/testDir");
		
		if(dir.exists() && dir.isDirectory()) {
			System.out.println(dir + "은 이미 존재합니다.");
		} else {
			dir.mkdir();
		}
		
		File file = new File(dir+"/test.txt");
		if(file.exists()) {
			System.out.println(file + "은 이미 존재합니다.");
		} else {
			try {
				file.createNewFile();
			} catch (IOException e) {
				e.printStackTrace();
			}
		}
		
		fos = new FileOutputStream(file);
		
		System.out.println("파일내용을 입력하세요.");
		int input;
		while( (input = isr.read()) != -1) {
			fos.write(input);
		}
		System.out.println(" <<문서입력 종료>> ");
		System.out.println();
		fos.close();

		fis = new FileInputStream(file);
		
		System.out.println(" <<문서내용 출력 >>");
		int data;
		while( (data=fis.read()) != -1) {
			System.out.print((char)data);
		}
		System.out.println();
		System.out.println(" <<문서내용 출력종료 >>");
        fis.close();
	}
}
```
`출력결과`
```java
파일내용을 입력하세요.
FileIOStream Test
 <<문서입력 종료>> 

 <<문서내용 출력 >>
FileIOStream Test
 <<문서내용 출력종료 >>
```

`Stream 객체`
```java
	FileInputStream fis = null;
	FileOutputStream fos = null;
	InputStreamReader isr = new InputStreamReader(System.in);
```
위에 선언되어 있는것들은 Stream객체이다.<br>
`FileInputStream`은 외부문서를 읽어오기 위한 것이고, `FileOutputStream`은 생성한 문서를 외부에 저장하기 위한것이다.<br>
마지막으로 `InputStreamReader`는 바이트기반의 스트림을 문자기반 스트림으로 변환해주는 보조스트림이며, 콘솔창의 입력을 읽어오는데 사용된다.<br>
`보조 스트림`이기때문에 `기반 스트림`없이 단독으로 사용될 수 없다.<br>
<hr>

`File 객체`
```java
        File dir = new File("d:/textDir");
		if(dir.exists() && dir.isDirectory()) {
			System.out.println(dir + "은 이미 존재합니다.");
		} else {
			dir.mkdir();
		}
		
		File file = new File(dir+"/test.txt");
		if(file.exists()) {
			System.out.println(file + "은 이미 존재합니다.");
		} else {
			try {
				file.createNewFile();
			} catch (IOException e) {
				e.printStackTrace();
			}
		}
```
위에서 File은 `File과 Directory를 모두 다룬다`고 설명했다.
File의 생성자에 경로를 넣어줄 수 있는데, 보통 String으로 절대경로를 넣어주는것이 일반적이다.<br>
여기서 주의할 점은 File의 생성자에 매개변수로 넘겨준 절대경로는 참조의 대상일 뿐이고, 파일을 생성한다는 것은 아니다<br>

`Method`
 - exists()
    - 해당 File이 존재하는지 여부를 boolean으로 반환한다.
- isDirectory()
    - 해당 File객체가 Directory인지를 boolean으로 반환한다.
 - mkdir()
    - File객체의 경로에 Directory를 생성한다.
- createNewFile()
    - File객체의 경로에 File을 생성한다.
    - `IOException`이 발생할 수 있기 때문에 `try-catch`나 `thorws`를 통해 예외처리를 해야한다.

설명된 method를 보면 감이오겠지만, 내가 원하는 경로에 Directory가 있는지 확인하고 없다면 Directory를 생성한다.<br>
그 후 생성된 Directory안에 새로운 File을 생성한다.<br>
<hr>

`File 생성`
```java
        fos = new FileOutputStream(file);
		
		System.out.println("파일내용을 입력하세요.");
		int input;
		while( (input = isr.read()) != -1) {
			fos.write(input);
		}
		System.out.println(" <<문서입력 종료>> ");
		System.out.println();
		fos.close();
```
위에서 선언해놓았던 FileOutputStream의 매개변수로 File을 생성할 경로를 넘겨준다.<br>
while의 조건문을 보면 InputStreamReader의 참조변수를 사용하는 것을 볼 수 있다.<br>
`isr`은 사용자가 콘솔에 입력하는 내용을 읽어들여 문자기반 스트림으로 변환하여 input에 저장한다.<br>
그리고 읽어온 정보를 `write()`를 통해 입력한다.<br>
이 때, `isr`은 사용자의 입력을 읽어오기만 할 뿐이고 직접적인 입출력 작업을 하지않기 때문에 보조스트림이라고 하는 것이다.<br>
사용자가 콘솔에서 `crtl + z`를 누르면 `-1`이 반환되면서 문서입력이 종료된다.<br>
아래에 문서를 읽어오는 작업은 문서를 입력하는 작업과 유사하기 때문에 설명하지 않겠다<br>
하지만 여기서 생각해보아야 할 것은 `한글`입력이다.<br>
우선 결과를 보자

```java
d:\testDir은 이미 존재합니다.
d:\testDir\test.txt은 이미 존재합니다.
파일내용을 입력하세요.
한글입력 테스트
 <<문서입력 종료>> 

 <<문서내용 출력 >>
```
아까 테스트하면서 Directory와 File을 생성했기 때문에 이미 존재한다고 나온다.<br>
하지만 입력하는것과는 상관없다. 주의해야 할 것은 새롭게 입력한 내용은 기존에 입력된 내용뒤에 추가되는것이 아니라 파일자체가 덮어씌워 진다는 것이다.<br>
기존내용에 추가하는것은 다른 메서드를 사용하면 된다.<br><br>
결과적으로 한글입력은 제대로 되지 않았다.<br>
원인은 당연하게 `Encoding`이 맞지 않기때문이다.<br>
다음 포스팅에서는 보조스트림을 이용하여 Encoding까지 설정하여 파일작업을 해보려고 한다.


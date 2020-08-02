---
layout : posts
title : JVM 메모리 구조
comments : true
tag : 
    - JAVA
categories :
    - BASIC JAVA
---

## JVM (Java Virtual Machine)
---
자바 프로그램은 `JVM`을 통해 실행됩니다.<br>
자바 프로그램을 실행하면, `JVM`은 `운영체제`로부터 메모리를 할당받아 프로그램을 실행합니다.<br>
오늘은 자바 프로그램을 실행하면 `JVM`의 메모리 구조에 대해 알아보겠습니다.

## JVM Memory구조
---
![JVM 메모리 구조](https://user-images.githubusercontent.com/67519366/89014222-2df38580-d350-11ea-9985-c7896bed899c.png)
<br>
##### 출처 : [TCP School](http://tcpschool.com/java/java_array_memory)

- __메소드 영역(Method Area)__
    - 메소드 영역은 어떠한 클래스가 사용되었을 때 해당 클래스파일(*.class)을 읽어들여 클래스데이터를 저장하는 공간입니다.
    - 클래스 데이터의 소멸은 프로그램이 종료된 후 입니다.

- __힙 영역(Heap Area)__
    - 힙 영역은 `new`키워드를 통해 인스턴스 변수가 생성되면, 해당 인스턴스 변수를 저장하는 공간입니다.

- __스택 영역(Call Stack Area)__
    - 스택 영역은 자바 프로그램에서 메서드(Method)가 호출될 때 해당 메서드의 지역변수, 매개변수,  중간 계산결과 등을 저장하는 공간입니다.
    - 해당 메서드의 수행이 끝나면 스택 영역에 할당되었던 메모리는 반환됩니다.
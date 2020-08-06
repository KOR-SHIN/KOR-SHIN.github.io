---
layout : posts
title : 상속(Inheritance)
categories :
    - BASIC JAVA
tag :
    - JAVA
---

## __상속(Inheritance)__
---
자바에서 `상속`이라는 것은 내용이 작성되어 있는 클래스를 다른 클래스에서 사용할 수 있도록 만들어 주는 것입니다<br>
또한 `상속`을 사용하면 코드의 재사용을 통해 `코드의 중복`을 없앨 수 있고, 유지보수가 매우 용이해지는 장점이 있습니다.<br>
하나의 클래스만 잘 구현해 놓아도, 여기저기서 상속을 받아 사용가능한 것입니다.<br>
<br>
`[상속 예시]`
```java
public class Parent {

	public static void main(String[] args) {
		Child inheritance = new Child();
		
		inheritance.printX();
	}
	
	public void printX() {
		System.out.println("PrintX - Parent");
	}
		
}

class Child extends Parent {
	
}
```
위 코드에서 `Child 클래스`안에는 아무것도 정의되어 있지 않습니다.<br>
하지만 코드는 컴파일도 잘되고 실행도 잘 됩니다.<br>
그리고 출력결과는 `PrintX-Parent`라고 출력됩니다.<br>
이러한 결과가 나오는 이유는 `Child`클래스가 `Parent`클래스를 상속받았기 때문입니다.<br>
상속을 받으면 상속받은 클래스의 `변수와 메서드를 모두 사용할 수 있습니다.`<br>
`class Child extends Parent`에서 `Child`를 자식클래스, `Parent`를 부모클래스라고 부릅니다.<br>
그리고 상속을 받기위해서는 클래스 이름뒤에 `extends`라는 예약어를 사용하고 상속받고자 하는 클래스 이름을 쓰면 됩니다.<br>
여기서 조심해야 하는점은 `상속은 한 개의 클래스만 받을 수 있습니다`<br>
<br>
자식클래스의 경우, 자식클래스의 객체를 생성하면 `부모클래스의 기본생성자`가 실행되고 `자식클래스의 생성자`가 실행됩니다.<br>
예제를 통해 알아보겠습니다.

`[상속 예시 2]`
```java
public class Parent {
	
	Parent () {
		System.out.println("Constructor - Parents");
	}

	public static void main(String[] args) {
		Child inheritance = new Child();
		
		inheritance.printX();
	}
	
	public void printX() {
		System.out.println("PrintX - Parent");
	}
		
}

class Child extends Parent {
	
	Child () {
		System.out.println("Constructor - Child");
	}
}
```
`[출력]`
```java
Constructor - Parents
Constructor - Child
PrintX - Parent
```
위에서 말했듯이 `자식클래스의 객체`를 생성하면, `부모클래스`의 생성자가 먼저 호출됩니다.<br>
하지만 [상속 예시]([#상속-예시])에서 우리는 생성자를 만들지 않았지만 실행이 잘 됐습니다<br>
기억하시겠지만, 클래스 내에 생성자가 없는 경우에는 자바에서 `기본 생성자`를 자동으로 만들어 주기 때문입니다.<br>
그렇다면 부모 클래스에 `매개변수가 있는 생성자`가 있는 경우는 어떻게 될까요?<br>
이미 예상하시겠지만 그런 경우에는 반드시 부모 클래스에 `기본 생성자`를 만들어야 합니다.<br>

## __Super__
---
이전 포스팅에서 `this`에 대해서 알아본 적이 있습니다.<br>
`this`는 인스턴스 자기자신을 의미하고, `this`를 통해 매개변수와 인스턴스변수의 이름이 똑같은 경우 구분하는 방법에 대해 알아보았었습니다<br>
그렇다면 `super`는 무엇일까요?<br>
바로 `부모클래스`를 의미하는 것입니다.<br>
`super`를 사용하여 `부모 클래스`를 명시적으로 표현해 줄 수 있고, 부모 클래스의 매개변수가 있는 생성자를 이용하여 초기화 시 활용가능합니다.

`[super 예시]`
```java
public class Parent {
	String name;
	int age;
	
	Parent (String name, int age) {
		this.name = name;
		this.age = age;
	}

	public Parent() {
		
	}

	public static void main(String[] args) {
		Child inheritance = new Child();	
		System.out.println(inheritance.toString());
	}
	
	public String toString() {
		return this.name + "," + this.age;
	}
		
}

class Child extends Parent {
	
	Child () {
		super("abc", 40); //부모 클래스의 생성자 호출
		System.out.println("Constructor - Child");
	}
	
}
```

`[출력]`
```java
Constructor - Child
abc,40
```
이렇게 `super`를 명시적으로 사용하여 초기화 작업을 할 때 사용가능합니다.<br>
여기서 주의사항은 부모클래스를 의미하는 `super`는 반드시 `첫 줄`에 있어야 합니다.<br>
만약 Child의 기본생성자에서 `System.out.println("Constructor - Child");`가 첫 줄에 있었다면 오류가 발생했을 것입니다.<br>

### __P.S__
---
이후에 설명드릴 `오버라이딩(Overriding)`, `다형성(polymorphism)`은 매우 중요하고, 반드시 알아야 하는 개념입니다.<br>
분량이 너무 많다고 생각되서 상속은 2개로 나눠서 포스팅하겠습니다.<br>
이 글을 보시는 분들께 잘못된 지식을 전달하는 일이 없도록 열심히 공부해서 포스팅 하겠습니다!<br>
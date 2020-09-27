---
layout : posts
title : 추상클래스와 인터페이스 (Abstract Class and Interface)
categories :
    - JAVA
tag :
    - JAVA
---

## __추상클래스(Abstract Class)__
---
`추상클래스(Abstract Class)`는 말 그대로 추상적인 클래스입니다.<br>
하지만 추상적이라는 것은 너무 광범위한 단어입니다.<br>
자바에서는 `추상메소드`가 한 개라도 선언되어 있는 클래스는 반드시 `추상클래스`로 선언해야합니다.<br>
`추상메소드`란 `메소드의 선언부만 존재하고 구현부가 없는 메소드`입니다.<br>

`[추상클래스(Abstract Class) 예시]`
```java
public class Ex{

}

abstract class AbstractClass {
    final int FINAL_NUMBER = 10;
    static int staticNumber = 10;

    public abstract void printX();
    public void display() {
        System.out.println("display");
    }
}
```
위의 코드에서 `public abstract void printX();`는 추상메소드 입니다.<br>
추상 메소드를 가지고 있는 클래스이기 때문에 `abstract` 키워드를 사용해서 `추상클래스`로 선언하였습니다.<br>
<br>
위의 예제에서 추상클래스의 특징에 대해 알 수 있습니다.

- final, static 키워드 사용 가능
- 추상메소드, 일반메소드 선언 가능
- 추상 클래스를 상속받은 클래스는 추상메소드를 반드시 구현해야 한다

위의 특징을 통해 추상클래스는 반드시 추상메소드만 가지고 있어야 하는게 아닌것을 알 수 있습니다.<br><br>
`final`을 처음 보는 분들을 위해 `final`에 대해 간단히 알아보겠습니다.<br> (추후에 final관련해서 포스팅 하겠습니다)

- 변수에 `final`키워드를 사용하면 값을 변경 할 수 없다(상수로 만든다)
- 메소드에 `final`키워드를 사용하면 Overriding이 불가능하다
- 클래스에 `final`키워드를 사용하면 해당 클래스는 상속이 불가능하다.

`[추상클래스(Abstract Class) 구현 예시]`
```java
public class Ex extends AbstractClass{
    
    @Override
    public void printX() {
        System.out.println("PrintX");
    }
}

abstract class AbstractClass {
    final int FINAL_NUMBER = 10;
    static int staticNumber = 10;

    public abstract void printX();
    public void display() {
        System.out.println("display");
    }
}
```
위와 같이 추상클래스는 상속을 통해 구현됩니다.<br>
여기서 중요한 것은 추상클래스를 상속받은 클래스는 반드시 `추상클래스에 선언되어 있는 추상메소드`를 구현해야만 합니다.<br>
만약 추상메소드를 구현하지 않는다면 오류가 발생하게 됩니다.<br>
또한, 추상클래스의 인스턴스는 생성 불가능합니다.<br>

## __인터페이스(Interface)__
---
`인터페이스(Interface)`는 겉보기에는 `추상클래스(Abstract Class)`와 비슷합니다.<br>
하지만 인터페이스는 다음과 같은 특징을 가집니다.<br>

- 상수 및 추상메소드만을 멤버로 가진다.
- final, static 키워드 사용 가능
- 메소드의 구현부를 작성하면 안된다 (반드시 추상메소드만 가능하다)
- implemets를 통해 구현한다.
- abstract를 생략 가능하다 (interface는 abstract키워드가 없어도 추상 메소드로 인지)

`[인터페이스(interface) 예시]`
```java
public class Ex implements InterfaceEx{
	public static void main(String[] args) {

	}

	@Override
	public void printX() {
		// TODO Auto-generated method stub
		System.out.println("printX()");
	}

	@Override
	public void display() {
		// TODO Auto-generated method stub
		System.out.println("display()");
	}
}


interface InterfaceEx{
	final int a = 10;
	static int b = 20;
	
	public void printX();
	public void display();
}
```
위의 코드에서 보듯이 `인터페이스`는 `추상메소드`와 `상수`를 멤버로 가지고 있습니다.<br>
이러한 인터페이스를 구현하기 위해 `public class Ex implements InterfaceEx`처럼 `implemets`키워드를 사용하였습니다.<br>
추상메소드는 `extends`를 사용하여 상속으로 구현하고, 인터페이스는 `implemets`를 사용하여 구현합니다<br>
둘의 차이점은 `implemets`를 통해 구현하는 인터페이스는 `한 개의 클래스가 여러개의 인터페이스를 구현가능하다`는 점입니다.
반면에 상속은 `한 개의 클래스가 한 개의 클래스만 상속가능`합니다.

`[다중 인터페이스 구현예시]`
```java
public class Ex implements InterfaceEx, InterfaceEx2{
	public static void main(String[] args) {

	
	}

	@Override
	public void printX() {
		// TODO Auto-generated method stub
		System.out.println("printX");
	}

	@Override
	public void display() {
		// TODO Auto-generated method stub
		System.out.println("display");
	}

	@Override
	public void printX2() {
		// TODO Auto-generated method stub
		System.out.println("printX2");
	}

	@Override
	public void display2() {
		// TODO Auto-generated method stub
		System.out.println("display2");
	}
}


interface InterfaceEx{
	final int a = 10;
	static int b = 20;
	
	public void printX();
	public void display();
	
}

interface InterfaceEx2 {
	public void printX2();
	public void display2();
}
```
여러개의 인터페이스를 구현하는 것은 간단합니다.<br>
`public class Ex implements InterfaceEx, InterfaceEx2`처럼 뒤에 `,(Comma)`를 사용하여 인터페이스 이름을 구분해주면 됩니다.<br>

## __추상클래스와 인터페이스를 사용하는 이유__
---
추상메소드와 인터페이스를 사용하는 이유는 여러가지가 있습니다.<br>
여기서는 주관적인 의견만 써놓겠습니다.<br>

- 설계단계에서 활용하여 필요한 메소드를 미리 선언해놓으면 개발단계에서 구현에 집중할 수 있다.
- 통일성과 일관성을 지킬 수 있고, 유지보수에 용이하다
- 반드시 필요하다고 생각되는 메소드를 선언해놓으면 구현을 강제하기 때문에 실수를 방지 할 수 있다.


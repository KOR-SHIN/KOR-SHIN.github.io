---
layout : posts
title : 자바의 변수종류(Variables)
categories :
    - JAVA
tag :
    - JAVA
---

## 변수(Variable)
---
자바에서 변수는 값을 저장하기 위한 공간이라고 생각할 수 있습니다.<br>
그리고 변수들은 `데이터 타입(Data Type)`을 가지게 됩니다.<br>
우선 변수에 대해 알아보기 전에 자바의 데이터 타입에 대해 알아보겠습니다.<br>

- 기본형 타입(Primitive Type)
    - 기본형 타입에는 문자형, 논리형, 정수형, 실수형이 있다.
    - 기본형 타입은 총 8가지이고, 나머지는 모두 참조형 데이터 타입을 가진다.
    - 기본형 타입 값의 범위를 대략적으로 알아놓는것이 좋다.


		| Primitive Type | 1byte   | 2byte | 3byte | 4byte |
		| -------------- | -----   | ----- | ----- | ----- |
		|   논리형       | boolean |       |       |       |
		|   문자형       |         | char  |       |       |
		|   정수형       | byte    | short | int   | long  |
		|   실수형       |         |       | float | double|

- 참조형 타입(Reference Type)
    - 기본형을 제외한 모든것이 참조형 데이터 타입이다.
    - 가장 쉽게 접하는 것 중 하나가 `String`이다.

## 4가지 변수의 종류
---
자바에서 변수는 4가지가 있습니다.

- `클래스 변수`
- `인스턴스 변수`
- `지역변수`
- `매개변수`

이러한 변수들은 `선언위치`와 `예약어`로 구분합니다.

## __클래스 변수__
---
`클래스 변수`는 클래스 안에, 메서드 밖에 선언되고 `Static`이라는 예약어를 가집니다.<br>
`클래스 변수`는 클래스가 사용될 때 `메서드 영역(Method Area)`에 생성되고 프로그램이 끝날 때 사라집니다.

`[클래스 변수 선언 예시]`
```java
public class VariableTest {
	static int staticValue = 10; //클래스 변수 선언
	
	public static void main(String[] args) {
		System.out.println(staticValue);
	}
}

class Ex {
	
	public void print() {
		System.out.println(VariableTest.staticValue);
	}
}
```
클래스 변수를 선언할 때는 위에서 설명했듯이 `static`이라는 키워드를 붙이게 됩니다.<br>
또한 VariableTest 클래스에 선언된 클래스 변수를 다른 클래스(Ex 클래스)에서 접근하고 싶을때는 VariableTest 클래스의 인스턴스를 생성하지 않고 참조연산자를 활용하여 접근가능합니다.

## __인스턴스 변수__
---
`인스턴스 변수`는 클래스 변수와 선언위치는 같지만 `Static`이라는 키워드가 없습니다.
`인스턴스 변수`는 객체가 생성되는 시점에 `Heap`영역에 생성되고 그 객체를 참조하는 다른 객체가 없으면 사라집니다.

`[인스턴스 변수 선언 예시]`
```java
public class VariableTest {
	static int staticValue = 10; //클래스 변수 선언
	int instanceValue = 20; //인스턴스 변수 선언
	
	public static void main(String[] args) {
		System.out.println(staticValue);
		//System.out.println(instanceValue);
		//클래스 메소드에서 인스턴스 변수를 호출 불가능
	}
	
	public void display() {
		System.out.println(staticValue);
		System.out.println(instanceValue);
	}
}

class Ex {
	
	VariableTest test = new VariableTest();
	
	public void print() {
		System.out.println(VariableTest.staticValue);
		System.out.println(test.instanceValue);
	}

}
```
클래스 변수와 인스턴스 변수의 비교를 위해 두 변수를 모두 사용하는 예시를 만들어보았습니다<br>
위에서 보듯이 인스턴스 변수는 `static`이 없이 선언되어 있습니다.<br>
저희가 주목해야 하는곳은 `main`메서드에서 `인스턴스 변수`를 사용할 수 없다는 점입니다.<br>
이유는 `main`메서드가 `static`이 붙은 `클래스 메서드`이기 때문입니다.<br>
클래서 메서드와 인스턴스 메서드는 변수사용에서 차이를 가집니다.

- `클래스 메서드`에서는 인스턴스 메서드, 인스턴스 변수를 `사용할 수 없다.`
- `인스턴스 메서드`는 클래스 메서드, 클래스 변수를 `사용할 수 있다.`

이러한 규칙이 있는 이유는 `인스턴스 멤버`가 존재하는 시점에서 `클래스 멤버`는 항상 존재하지만, `클래스 멤버`가 존재하는 시점에서 `인스턴스 멤버`가 항상 존재한다는 보장이 없기 때문입니다.<br>
인스턴스 멤버는 반드시 `객체`를 생성한 후에 참조 또는 호출이 가능하지만, 클래스 멤버는 `객체`를 생성하지 않고 `참조연산자`를 통해 접근이 가능하기 때문입니다.<br>
지금 당장 이해가 되지 않아도 이러한 규칙이 있다는 것만 기억해두시면 됩니다.<br>

## 지역변수와 매개변수
---
`지역변수`는 `중괄호{} `안에 선언되어 있는 변수라고 생각하면 됩니다.<br>
`지역변수`들은 메서드가 호출될 때 `호출 스택(call stack)`영역 생성되었다가 메서드의 작업이 끝나면 반환됩니다<br><br>
`매개변수`는 메서드에 넘겨주는 변수라고 생각하시면 됩니다.<br>
다른이름으로는 `파라미터(Parameter)`라고 부르기도 합니다.


`[지역변수 선언 예시]`
```java
public class Local {
    public static void main(String[] args) {

        boolean x = true;

        local(x);
    }

    public static void local(boolean x) {
        if(x) {
            int localVariable = 10;
        }

        if(x) {
            int localVariable = 20;
        }
    }
}
```
위의 예시에서 `local(boolean x)`메서드는 boolean값을 `매개변수`로 가지는 메서드이다.<br>
`매개변수`라는것이 어려운 것은 단순히 `메서드에 넘겨주는 값`인 것이다.<br>
메서드 내부 내용을 살펴보면 2개의 이름이 같은 변수를 선언하고 있다.<br>
저런것이 가능한 이유는 `지역변수`는 `{}`속에서 생성되고 소멸되기 때문이다.<br>
하나의 `if`문이 끝나면 `localVariable`역시 사라지는 것이다.


## __변수 사용기준__
---
오늘은 자바의 변수 종류 4가지에 대해 알아보았습니다<br>
마지막으로 `클래스 변수`와 `인스턴스 변수`를 정하는 기준에 대해 알아보겠습니다<br>

- 클래스 변수
    - 모든 객체들이 동일한 값을 가져야 하는 속성은 클래스 변수로 선언한다.

- 인스턴스 변수
    - 모든 객체들이 고유의 값을 가져야 하는 속성은 클래스 변수로 선언한다.

이러한 기준의 근거는 `클래스 변수`는 하나의 저장공간을 공유하기 때문에 누군가 `클래스 변수`의 값을 바꾸면, 모든 객체들이 가진 `클래스 변수`값이 변하게 됩니다.
<br>하지만 `인스턴스 변수`는 `new`라는 키워드를 통해 생성되면서 독립된 저장공간을 가지게 됩니다.<br>
즉, 생성된 `객체`들의 인스턴스 변수 값은 `고유값`이지만, 클래스 변수 값은 `공통값`을 가지는 것입니다.

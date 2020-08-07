---
layout : posts
title : 오버라이딩과 다형성(Overriding and Polymorphism)
categories :
    - BASIC JAVA
tag : 
    - JAVA
---

## __오버라이딩(Overriding)__
---
`오버라이딩(Overriding)`이란 상위 클래스에 선언되어 있는 메소드를 하위 클래스에서 동일하게 선언하여 사용하는 것입니다.<br>
메소드의 이름, 시그니처가 동일하지만 하위 클래스에서 구현내용을 재정의 하여 사용할 수 있습니다.<br>

`[오버라이딩(Overriding) 예시]`
```java
public class Parent {
    public static void main(String[] agrs) {

        Parent p1 = new Parent();
        Parent p2 = new Child();
        Parent p3 = new ChildOther();

        p1.printX();
        p2.printX();
        p3.printX();
    }

    public void printX() {
        System.out.println("printX - Parent");
    }
}

class Child extends Parent {
    @Overriding
    public void printX() {
        System.out.println("printX - child");
    }
}

class ChildOther extends Parent {
    
}
```
`[출력]`
```java
System.out.println("printX - Parent");
System.out.println("printX - Child");
System.out.println("printX - Parent");
```

우선 코드와 출력결과를 살펴보기 전에 상속에서 부모클래스와 자식클래스의 형변환에 대해 알아보겠습니다.<br>

- 자식클래스의 객체는 부모클래스의 타입을 가질 수 있다.
- 부모클래스의 객체는 자식클래스의 타입을 가질 수 없다.
- 부모클래스의 객체가 자식클래스의 타입을 가지기 위해서는 `강제 형변환`이 필요하다.

이러한 규칙이 있는 이유는 자식클래스는 부모클래스의 모든 변수와 메소드를 사용가능합니다<br>
하지만, 자식클래스는 부모클래스에 없는 변수나 메소드를 추가하여 사용할 수 있습니다.<br>
그렇기 때문에 부모클래스에는 없지만 자식클래스에는 존재하는 변수나 메소드가 있을 수 있기 때문에 부모클래스의 객체는 자식클래스 타입을 가질 수 없습니다.<br>
<br>
```java
class Child extends Parent {
    @Overriding
    public void printX() {
        System.out.println("printX - child");
    }
}
```
위와 같이 `부모클래스(상위클래스)`에 있는 `printX()`라는 메소드를 `자식클래스(하위클래스)`에서 그대로 사용하면서 구현부를 재정의하여 사용하는것을 `오버라이딩(Overriding)`이라고 합니다.<br>
위에 보이는 `@Overriding`이라는 것은 `어노테이션(Annotation)`이라는 것인데, 시스템에게 `이것은 오버라이딩한 메소드니까 잘못 정의되어 있으면 경고해달라`고 알려주는 역할이라고 생각하시면 됩니다<br>
`어노테이션(Annotation)`에 관해서는 잘 모르기 때문에 간단히 설명드리겠습니다.<br>
혹시나 궁금하신 분들은 구글링으로 찾아보시면 많은 정보가 나올겁니다<br>

## __다형성(polymorphism)__
---
`다형성(polymorphism)`이란 하나의 객체가 여러가지 타입을 가질 수 있는 것이라고 생각하면 됩니다<br>
여러분은 이미 다형성의 예시를 `오버라이딩 예시`에서 보셨습니다.<br>

 ```java
 public class Parent {
    public static void main(String[] agrs) {

        Parent p1 = new Parent();
        Parent p2 = new Child();
        Parent p3 = new ChildOther();
```
바로 이부분입니다.<br>
세 개의 객체 모두 클래스 타입은 `Parent`입니다.<br>
하지만 각각 다른 클래스의 생성자를 호출하고 있습니다<br>
자바에는 `instanceOf`라는 메소드를 통해 객체의 클래스 타입을 알 수 있습니다<br>
위에서 다형성은 하나의 객체가 여러가지 타입을 가진다고 설명하였는데 사실인지 예제로 확인해보겠습니다.<br>

`[다형성(polymorphism) 예시]`
```java
public class Parent {
    public static void main(String[] agrs) {

        Parent p1 = new Parent();
        Parent p2 = new Child();
        Parent p3 = new ChildOther();

        Parent[] arr = {p1, p2, p3};
        
        for(Parent item : arr) {
        	System.out.println("---------------");
        	if(item instanceof Child) {
        		System.out.println("is Child Type");
        	} 
        	if(item instanceof ChildOther) {
        		System.out.println("is ChildOther Type");
        	} 
        	if(item instanceof Parent) {
        		System.out.println("is Parent Type");
        	}
        }
    }
}
```

`[출력]`
```java
---------------
is Parent Type
---------------
is Child Type
is Parent Type
---------------
is ChildOther Type
is Parent Type
```
부모클래스를 제외한 자식클래스들은 두 가지의 클래스 타입을 가진것을 볼 수 있습니다.<br>
이러한 것이 `다형성(ploymorphism)`입니다.<br>
`다형성`의 예시는 매우 많습니다.<br>
예를들어 `오버로딩(Overloading)`도 다형성을 구현하는 방법 중 하나입니다.<br>
`다형성`이라는것은 한마디로 정의하기 매우 어려운 개념이라고 생각합니다<br>
제가 작성한 예시말고도 많은 정보들이 있으니 꼭 여러사이트에서 `다형성`에 대해 찾아보시기 바랍니다.

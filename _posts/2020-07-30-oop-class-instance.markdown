---
layout : posts
title : 클래스와 인스턴스(Class and Instance)
tag :
    - JAVA
categories :
    - JAVA
---

## __객체지향 프로그래밍<br>(OOP - Oriented Object Programming)__
---

객체지향 프로그래밍은 프로그램을 여러개의 독립된 단위, `객체(Object)`로 보는 것입니다.<br>
이러한 객체지향 프로그래밍은 코드의 중복제거가 가능하고, 코드의 관리가 용이해서 유지보수 비용을 절감할 수 있습니다.<br>
객체지향 프로그래밍에서 객체를 만들기위해 `클래스(Class)`라는 것을 사용하고 클래스를 통해 만든 객체를 `인스턴스(Instance)`라고 합니다.

## __클래스(Class)__
---
자바에서 `클래스(Class)`는 객체를 정의하는 `설계도`와 같은 의미입니다.<br>
클래스를 가지고 객체를 생성하고, 한번 클래스를 정의해놓으면 여러개의 객체를 생성할 수 있습니다.<br><br>
이러한 클래스는 `상태(state)와 행동(behavior)`를 가집니다.
다른말로 `변수(Variable)와 메서드(Method)`라고 부릅니다.<br>
여기서 `메서드(Method)`는 특정한 작업을 수행하기 위한 명령문이라고 생각하면 됩니다.<br>

## __인스턴스(Instance)__
---
위에서 `인스턴스(Instance)`는 클래스를 통해 만들어진 `객체(Object)`라고 설명했습니다.<br>
비유하자면 `설계도(클래스)`에 정의된 대로 만들어진 `구체적인 제품(인스턴스)`입니다.<br>
이렇게 만들어진 인스턴스는 클래스가 가진 `상태`와 `행동`의 집합입니다.<br>
여기서 클래스를 통해 인스턴스를 만드는 과정을 `인스턴스화`라고 합니다.<br>

## __예시(Example)__
---
```java
public class Ex{
    public static void main(String[] args) {
        Tv ins1 = new Tv();
        // Tv클래스의 인스턴스 ins1을 생성
        // new라는 키워드를 반드시 써야한다.
    }
}

class Tv {
     int width = 200;
     int height = 50;

     void channelUp() { 
         channel++;
     }
}
```
`width`와 `height`는 우리가 만들 Tv의 크기(`속성`)을 정의하고 있고, `channelUp()`은 채널을 올려주는 작업을 수행하는 명령문(`행동`)을 정의하고 있습니다.
<br><br>
클래스를 한번 정의해놓으면 여러개의 객체를 만들 수 있습니다.<br>
위에서 처럼 Tv클래스의 인스턴스를 만들기 위해서는 `new`라는 키워드를 사용해야 합니다<br>
그리고 Tv클래스를 통해 만들어진 Tv(객체)들은 모두 같은 `속성과 행동`을 가집니다.
하지만 우리의 필요에 의해 `속성`, 즉 `변수값`을 바꿀수 있습니다. <br>

## __객체와 인스턴스__
---
글을 읽다보면 객체와 인스턴스라는 말이 자주 나옵니다.<br>
둘이 의미는 비슷한거같은데 어떨때는 객체고 어떨때는 인스턴스일까요?<br>
사실 엄격하게 둘을 구분해서 부를 필요는 없지만 그래도 약간은 다르게 사용됩니다.<br>
```java
public class Ex{
    public static void main(String[] args) {
        Tv ins1 = new Tv();
        Car ins2 = new Car();
    }
}

class Tv {

}

class Car{

}
```
`ins1`과 `ins2`는 모두 `객체`, `인스턴스`라고 부를 수 있습니다<br>
하지만 `ins1`은 `Tv클래스의 인스턴스`라고 부르고 `ins2`는 `Car클래스의 인스턴스`라고 부릅니다.<br>
인스턴스보다는 객체가 더 넓은 의미를 가지는 것이죠.<br>

 - ins1은 객체이다 ( O )
 - ins2는 객체이다 ( O )
 - ins1은 Tv의 인스턴스이다 ( O )
 - ins1은 Car의 인스턴스이다 ( X )
 - ins2는 Car의 인스턴스이다 ( O )
 - ins2는 Tv의 인스턴스이다 ( X )
## __메서드(Method)__
---
`메서드(Method)`는 `행동`, `특정한 작업을 수행하기 위한 명령문`이라고 위에서 설명했습니다.<br>
그렇다면 메서드는 어떻게 사용하고 어떻게 이루어져 있을까요?
<br>
```java
public class Ex {
    public static void main(String[] args){
        sum(10, 20);
    }

    public int sum(int x, int y) { // 선언부 (Header)
        return x+y; // 구현부 (body)
    }
}
```

위 코드에서 ```public int sum(int x, int y) { return x+y; }```이 바로 메서드입니다. <br>
예시에 써져있듯이 메서드는 선언부와 구현부로 나누어집니다.

- 선언부
    - 접근제어자 : 맨앞에 Public은 [접근제어자](https://opentutorials.org/course/1223/6061)입니다 
    - 반환타입 : 해당 메서드가 작업한 결과를 반환해주는 데이터 타입을 명시합니다.<br>
    여기서는 `int`이기 때문에 정수형 결과를 반환합니다.
    - 메서드 이름 : `sum`이라는 이름을 가지고 있습니다. <br> 메서드 이름을 보면 어떤 작업을 수행하는지 예상할 수 있도록 이름을 붙이는 것이 좋습니다.
    - 매개변수 : `(int x, int y)`처럼 메서드가 작업을 수행하는데 필요한 데이터를 명시하는 것입니다. 

- 구현부 
    - 구현부에는 메서드가 작업을 수행하는 로직을 작성합니다.








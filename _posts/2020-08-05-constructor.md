---
layout : posts
title : 생성자(Constructor)
categories :
    - JAVA
tag :
    - JAVA
---

## __생성자__
---
생성자란 객체 생성시 제공되는 초기화 기능이라고 생각하면 됩니다.<br>

`[기본 생성자 예시]`
```java
public class ConstructorEx{
    public static void main(String[] args){
        ConstructorEx constructorEx = new ConstructorEx();
    }
}
```
위의 예시에서 `new` 오른쪽에 있는 `ConstructorEx()`가 생성자입니다.<br>
생성자는 객체를 생성할 때 가장 먼저 실행되어 객체를 초기화합니다.<br>
하지만 `Constructor`클래스에서 아무리봐도 생성자가 정의된 부분을 찾을 수 없습니다.<br>
그 이유는 클래스를 작성할 때 사용자가 생성자를 만들지 않으면 자바에서 `기본 생성자`를 컴파일 할 때 자동으로 생성해주기 때문입니다.<br>
기본 생성자는 `매개변수가 없는`생성자입니다.

## __매개변수가 있는 생성자__
---
이제부터는 매개변수가 있는 생성자에 대해서 생각해 보겠습니다.<br>
우선 매개변수가 있는 생성자는 자바에서 제공해주지 않기때문에 우리가 직접 만들어야 합니다<br>
우리는 생성자를 정의해본 적이 없기때문에 몇 가지 생성자의 특징에 대해 알아보고 생성자를 만들어보겠습니다<br>

- 생성자의 특징
    - 생성자의 이름은 클래스 이름과 같아야 한다.
    - 리턴타입이 없다. `(생성자의 리턴타입은 해당클래스의 객체)`
    - Overloading이 가능하다.

오버로딩은 특징을 가집니다.

- 오버로딩(Overloading)
    - 메소드의 이름이 같아야 한다.
    - 리턴타입은 달라도 상관없다.
    - 매개변수의 타입 또는 개수가 달라야 한다.

`[매개변수가 있는 생성자 예시]`
```java
public class ConstructorEx{

    String name;

    public ConstructorEx() {
        //기본 생성자
    }

    public ConstructorEx(String name) {
        //매개변수가 있는 생성자
        this.name = name;
    }

    public static void main(String[] args){
        ConstructorEx constructorEx = new ConstructorEx("myName");
    }
}
```
기본생성자 예제와는 확실히 차이점이 보입니다.<br>
매개변수가 있는 생성자 예제를 보기로 했는데 기본 생성자가 선언되어 있는걸 보고 `기본 생성자는 자바에서 제공해주는 것 아닌가?`라는 생각을 할 수 있습니다.<br>
하지만 자바가 기본생성자를 자동으로 만들어주는 것은 `클래스안에 생성자가 없는 경우`입니다.<br>
만약 사용자가 클래스 안에 생성자를 하나라도 선언했다면, 기본 생성자가 제공되지 않으며 그 경우 기본 생성자가 없으면 `컴파일이 되지 않습니다`<br>
이처럼 우리는 매개변수를 다르게 가지는 여러개의 생성자를 이용해서 다양한 방법으로 객체를 초기화 할 수 있습니다.<br>

`[여러가지 생성자 활용 예시]`
```java
public class ConstructorEx{

    String name;
    int age;

    public ConstructorEx() {
        //기본 생성자
    }

    public ConstructorEx(String name) {
        //이름만 아는 경우
        this.name = name;
    }

    public ConstructorEx(int age) {
        //나이가 아는경우
        this.age = age;
    }

    public ConstructorEx(String name, int age) {
        //나이와 이름을 모두 아는 경우
        this.name = name;
        this.age = age;
    }

    public static void main(String[] args){
        ConstructorEx constructorEx = new ConstructorEx("myName");
        ConstructorEx constructorEx2 = new ConstructorEx(21);
        ConstructorEx constructorEx3 = new ConstructorEx("myName", 21);
    }
}
```
위의 예시처럼 여러가지 생성자를 만들어서 객체를 초기화 할 수 있습니다.<br>
`생성자를 몇 개 까지 만들수 있을까`라고 생각하시는 분도 계실거라고 생각합니다<br>
생성자에 정해진 개수는 없지만, 무분별하게 많이 만들경우 관리가 힘들어지고 혼란을 야기할 수 있기 때문에 꼭 필요한 생성자만 만드는 것을 추천합니다<br>

## __this__
---
위의 예시에서 `this`라는 키워드가 사용된 것을 보셨을 것입니다.<br>
`this`는 `인스턴스 자기자신`을 의미한다고 생각하시면 됩니다<br>
```java
public class ConstructorEx{

    String name;
    int age;

    public ConstructorEx(String name) {
        //이름만 아는 경우
        this.name = name;
    }
}
```
위의 생성자에서 매개변수로 받은 `name`과 인스턴스 변수 `name`의 이름이 같기때문에 `this`를 사용하지 않으면 두 개의 변수를 구분할 수 없습니다<br>
그렇다면 `매개변수 이름을 다르게 하면 되지 않나?`라고 생각 할 수 있습니다.<br>
물론 틀린말은 아니고, 그렇게 사용하는 것은 개인의 자유입니다.<br>
하지만 `this`를 이용해서 구분하는 것이 의미가 더 명확하다고 생각하기 때문에 저는 변수이름을 달리 사용하기 보다는 `this`를 이용하는 편이 더 좋다고 생각합니다.<br>

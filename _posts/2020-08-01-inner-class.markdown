---
layout : posts
title : 중첩 클래스(Nested Class)
categories :
    - JAVA
tag :
    - JAVA
---

## __중첩 클래스(Nested Class)__
---
중첩 클래스는 단어 그대로 클래스가 중첩되어있는 상태입니다.<br>
하나의 클래스안에 또 다른 클래스가 정의되어 있는 형태라고 생각하면 됩니다.<br>
이러한 중첩클래스 3가지 종류가 있습니다.

- 내부 클래스 (Inner Class)
- 정적 내부 클래스 (Static Inner Class)
- 지역 클래스 (Local Class)
- 익명 클래스 (Anonymous Class)

## __내부 클래스(Inner Class)__
---
내부 클래스는 하나의 클래스 안에 다른 클래스가 정의되어 있는 형태입니다.<br>
내부 클래스는 다음과 같은 특징을 가지고 있습니다.<br>

- 중첩되는 클래스는 한 개 이상 가능하다.
- Outer 클래스 멤버를 Inner 클래스에서 사용이 가능하다.
- Outer 클래스에서 Inner 클래스 멤버 사용이 불가능하다.
- 일반 중첩 클래스 내부에서는 static과 관련된 멤버를 선언할 수 없다.

`[내부 클래스 예시]`

```java
class Outer {
    int x = 10;
    static int y = 20;

    class Inner{ //내부 클래스
        int z = 30;

        public void print() {
            System.out.println(x);
            System.out.println(y);
            System.out.println(z);
        }

    }
}

public class Ex {
    public static void main(String[] args) {
        //내부 클래스 선언방법
        Outer out = new Outer();
        Outer.Inner inner = out.new Inner();

        inner.print();
    }
}
```
`main` 안에 있는 인스턴스 생성방법을 보면 우리가 알고있는 방법과 다르다는 것을 알 수 있습니다.<br>
내부 클래스의 인스턴스를 생성하기 위해서는 우선 바깥 클래스의 인스턴스를 먼저 생성해야 합니다.<br>
그 후 Outer클래스의 인스턴스를 참조하여 Inner클래스의 인스턴스를 생성할 수 있습니다<br>

## __정적 내부 클래스(Static Inner Class)__
---
정적 내부 클래스는 `static`과 관련된 멤버를 선언할 수 있는 내부 클래스 입니다.<br>
정적 내부 클래스는 다음과 같은 특징을 가집니다.<br>

- 클래스의 이름 앞에 `static` 키워드가 붙는다.
- 객체를 독립적으로 생성 가능하다.
- `static 멤버`, `static 메서드`도 만들어 사용할 수 있습니다.
- Outer 클래스의 static 멤버만 Inner 클래스에서 사용할 수 있습니다.

`[정적 내부 클래스 예시]`
```java
class Outer {

    int x = 10;
    static int y = 20;

    static class Inner{ //내부 클래스
        int z = 30;

        public void print() {
            // System.out.println(x); // outer클래스의 인스턴스 변수는 사용 불가능
            System.out.println(y);
            System.out.println(z);
        }

    }
}

public class Ex {
    public static void main(String[] args) {
        //정적 내부 클래스 선언방법
        Outer.Inner inner = new Outer.Inner();

        inner.print();
    }
}
```
`main` 문을 보면 기본 내부 클래스의 선언 벙법과는 조금 다른것을 알 수 있습니다.<br>
이전에 내부 클래스를 접근하기 위해서는 Outer클래스의 인스턴스를 생성하고, Outer클래스의 인스턴스를 참조하여 내부 클래스의 인스턴스를 생성해서 접근했습니다<br>
하지만 `static`이 붙은 정적 내부 클래스는 Outer클래스의 인스턴스 생성없이 곧바로 접근가능합니다.<br>

## __지역 중첩 클래스(Local Inner class)__
---
지역 중첩 클래스는 특정한 메서드에 한정적인 용도로 사용합니다.
지역 중첩 클래스는 다음과 같은 특징을 가집니다.

- 접근 제한자와 지정 예약어를 사용 할 수 없다.
- static 멤버를 선언하지 못한다.
- 객체 생성은 외부에서 불가능하고, 내부에서만 가능하다.

`[지역 중첩 클래스 예시]`
```java
public class Ex {
    public static void main(String[] args) {
        //정적 내부 클래스 선언방법

        int x = 10;

        class Inner{
            int y = 20;
        }

        Inner in = new Inner();

        System.out.println(x);
        System.out.println(in.y);
```
`main` 메서드 안에 내부 클래스를 선언해서 사용하는 예제입니다.<br>
이렇게 사용하는 방법 외에 많은 방법이 있지만 가장 간단한 예제로 사용해보았습니다.<br>

## __익명 클래스(Anonymous Class)__
---
익명 클래스는 기존에 있는 클래스의 특정 메서드를 `(오버라이딩)Overriding`하여 사용자가 재정의 하여 사용합니다. <br>
익명 클래스는 다음과 같은 특징을 가집니다.

- class 예약어와 클래스명이 없다.
- 익명 클래스에 사용되는 중첩 클래스는 기존에 존재하는 클래스이다.
- 생성자를 작성할 수 없다.
- 외부 멤버 중 final만 포함 가능하다.

`[익명 클래스 예시]`
```java
class Inner {
    int y = 20;

    public void print() {
        System.out.println("Anonymous class");
    }
}

public class Ex {
    public static void main(String[] args) {
        final int x = 10; //내부 클래스에서 사용하기 위해 final로 선언

        Inner in = new Inner() {
            public void print() {
                System.out.println("overriding");
                System.out.println(x);
                System.out.println(y);
            }

            public void printX() {
                //익명 클래스 안에서 메서드를 생성하여 사용 가능
                System.out.println("Method 추가");
            }
        };

        in.printX(); //익명클래스 안에서 생성된 메서드는 밖에서 사용 불가능      
    }
}
```

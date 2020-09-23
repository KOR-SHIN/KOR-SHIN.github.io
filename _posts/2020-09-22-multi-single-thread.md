---
title : Single-Thread VS Multi-Thread
layout : posts
categories :
 - JAVA
tag :
 - JAVA
---

## __Single Thread(단일 쓰레드)__
---
`Single Thread`는 말 그대로 하나의 Thread를 사용하는 것이다.<br>
단일 쓰레드를 사용하는 프로세스는 별도로 쓰레드를 관리하는 번거로움이 없어서 코딩은 용이하겠지만, 작업시간이 낭비되는 경우가 생긴다.

- `[Sample Code]`

    ```java
    public class T05_ThreadTest {
    	
    	public static void main(String[] args) {

    		Thread th1 = new Thread();
    		
    		String input = JOptionPane.showInputDialog("아무거나 입력하세요.");
    		
    		int i=10;
    		while(i != 0) {
    			System.out.println(i--);
    			try {
    				Thread.sleep(1000);
    			} catch(InterruptedException e) {
    				e.printStackTrace();
    			}
    		}
    		System.out.println("카운트가 종료되었습니다.");
    	}
    }
    ```

위의 코드에서는 사용자가 입력을 하지않으면, 카운트다운이 시작되지 않는다.<br>
사용자의 입력을 요구하는 Dialog가 생성되고, 사용자가 입력하기 전 까지 아무런 작업도 하지않는 버려지는 시간이 발생하는 것이다.<br>
하지만 `Multi Thread`를 사용하면 버려지는 시간을 효율적으로 사용 할 수 있다.

## __Multi Thread(다중 쓰레드)__
---
`Multi Thread`는 하나의 프로세스에 여러개의 쓰레드를 사용하여 작업을 처리하거나, 여러개의 프로세스에 여러개의 쓰레드를 사용하는 것을 의미한다.

다중 쓰레드의 장점은 이전 포스팅에 설명되어있다.

다중 쓰레드를 사용하면 단일 쓰레드보다 어떤점이 좋은지 예제를 통해서 살펴보려고 한다.

- `[Sample Code]`

    ```java
    public class T06_ThreadTest {

    	public static void main(String[] args) {

    		ThreadTest_1 th1 = new ThreadTest_1();
    		
    		th1.start();
    		
    		String input = JOptionPane.showInputDialog("아무거나 입력하세요");
    		System.out.println("입력값 : " + input);
    		th1.interrupt();
    	}
    }

    class ThreadTest_1 extends Thread {
    	@Override
    	public void run() {
    		int i = 10;
    		while(i!=0 && !isInterrupted()) {
    			System.out.println(i--);
    			try {
    				Thread.sleep(1000); 			
    			} catch(InterruptedException e) {
    				interrupt();
    			}
    		}
    		System.out.println("카운트가 종료되었습니다.");
    	}
    }
    ```

    위의 예제에서는 두 개의 쓰레드를 사용하여 작업을 동시에 처리하는 예제이다.<br>
    Thread를 상속한 클래스를 하나만 생성했기때문에 단일 쓰레드라고 오해할 수 있지만, Main Thread까지 사용하기 때문에 두 개의 쓰레드를 사용하는 것이다.<br>
    위에서 사용된 `interrupt`는 실행중인 쓰레드에게 작업중단을 요청하는 것이고 `Sleep`은 실행중인 쓰레드를 잠깐 멈추는 메서드이다.<br>
    `Sleep`은 단위가 `ms`이기 때문에 1초를 멈추려면 `1000`으로 값을 넣어야 한다. (1ms = 0.001초)
	<br>위의 코드에서는 사용자의 입력을 요청하는 Dialog가 생성되고, 사용자가 입력을 하지않아도 카운트다운이 시작된다.<br>
    그렇기때문에 단일 쓰레드를 사용하는 것보다 멀티쓰레드를 사용하는것이 작업시간을 더욱 효율적으로 사용할 수 있다.

## __Single Thread VS Multi Thread__
---
위에서 살펴본 예제를 보면 단일 쓰레드를 사용하는 이유를 모르겠다.

프로그램을 병렬적으로 처리하여 향상된 사용자 응답을 제공하고, 자원을 효율적으로 사용하는 다중 쓰레드를 놔두고 왜 단일 쓰레드를 사용할까?

여러가지 이유가 있겠지만 여기서는 3가지 정도의 이유를 들어보려고 한다 (개인적인 생각)

- 프로그래밍이 어렵다.
    - 말장난 하는것 같지만 다중 쓰레드를 사용하여 프로그래밍을 하는것은 여간 피곤한 일이 아닐것이다.<br>신경써야 하는부분이 많아지고 쓰레드의 실행순서도 완전히 예측할 수 없기 때문이다.<br> 이러한 근본적인 문제를 간과할 수 없다고 생각한다.
- 동기화 문제
    - 첫 번째 이유의 연장선이라고 볼 수 있다.<br> 이전 포스팅에서 설명했듯이 쓰레드 각각은 고유한 Call-Stack영역을 가지고 수행되기 때문에 문제가 발생할 수 있다.<br> 여기서 예시를 들진않겠지만 이러한 동기화문제로 인해 예상과 다른 결과를 얻는 상황이 발생할 수 있다 (synchronized로 해결가능하지만 최소화하여 사용하지 않으면 프로그램의 성능에 영향을 준다.)
- 환경의 영향
    - 멀티쓰레드는 단일쓰레드보다 항상 빠른것은 아니다.<br>우리가 사용하는 컴퓨터에는 Core가 있는데 요즘은 대부분 Multi-Core이기 때문에 멀티쓰레드가 빠를수 밖에없다. 하지만 단일코어에서 멀티쓰레드를 사용하면 오히려 단일쓰레드가 더 빠를 수 있다.
	- Core가 2개인 환경에서 쓰레드를 2개 사용하면 각각의 Core가 쓰레드를 하나씩 사용하기 때문에 Context-switching의 영향이 없겠지만 Single Core에서 쓰레드를 2개 사용하면 쓰레드간의 Context-switching시간때문에 오히려 더 느릴수도 있는것이다.
    - 쓰레드나 프로세스간의 정보를 교환하는 것을 Context-switching이라고 하는데 단일코어에서 멀티쓰레드를사용하면 Context-switching으로 인한 시간때문에 단일 쓰레드보다 작업속도가 느릴 수 있다.
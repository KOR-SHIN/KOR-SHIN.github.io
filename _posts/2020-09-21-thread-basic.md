---
title: Thread
layout: posts
categories:
 - JAVA
tag:
 - JAVA
---

## __Process__
---
- `Process`는 운영체제에서 실행중인 하나의 프로그램을 의미한다.
- `Multi-Process`는 두 개 이상의 프로세스가 실행되는 것을 의미한다.
- `Multi-Tasking`은 두 개 이상의 프로세스를 실행하여 일을 처리하는 것을 의미한다.

## __Thread__
---
- `Thread`는 프로그램의 실행 흐름을 의미한다.
- 프로세스 내에서 실행되는 세부 작업 단위이다.
- 하나의 프로세스 내에는 여러 개의 Thread가 존재할 수 있다.
- `경량화 프로세스(LWP : Low-weight Process)`라고도 부른다.
- 두 개 이상의 스레드를 `Multi-Thread`라고 부른다.

## __Thread의 특징__
---
- Thread는 프로세스에 비해 `문맥교환(Context Switching)`시간이 적게 걸린다.
- Thread는 동료 스레드와 사용메모리를 공유할 수 있다.
- Thread간의 통신은 프로세스간의 통신에 비해 시간이 적게 걸린다. (빠르다)
- Thread는 프로세스에 비해 생성 및 종료 시간이 적게 걸린다. (빠르다)

## __Thread 생성방법__
---
- Thread 클래스를 상속받은 클래스의 인스턴스를 생성한다.
    - Sample Code

        ```java
        public class T02_ThreadTest {

        	public static void main(String[] args) {
        		myThread t1 = new myThread();
        		t1.start();
        	}
        }

        class myThread extends Thread {
        	
        	@Override
        	public void run() {

        	}
        }
        ```

- Runnable 인터페이스를 구현한 클래스의 인스턴스를 생성 후, Thread클래스의 생성자를 이용한다.
    - Sample Code

        ```java
        public class T02_ThreadTest {

        	public static void main(String[] args) {
        		Thread t2 = new Thread(new myThread2());
        		t2.start();
        	}
        }

        class myThread2 implements Runnable {
        	
        	@Override
        	public void run() {

        	}
        }
        ```

## __Thread 실행원리__
---
![Thread%2097b9cd2a6b0145ba8f6e6735787f742b/callStack.png](Thread%2097b9cd2a6b0145ba8f6e6735787f742b/callStack.png)

- 이미지 설명

    사진에 표현된 것은 JVM에서 Call Stack영역에 속한다. 

    Method를 호출하게 되면, Main Method위에 스택이 쌓이고, 수행이 완료되면 반환되는것을 반복한다. 

    하지만 Thread는 생성되고, start() 메서드를 호출하면, 새로운 Call Stack영역을 만들어서 수행문을 처리한다.

    예상하듯이 Thread는 별도의 Call Stack영역을 필요로 한다.

    따라서 JVM은 모든 Thread의 수행이 끝나기 전까지 종료되지 않는다.

    또한, Thread의 수행은 순차적으로 이루어지는것이 아니라 운영체제의 스케줄링에 따라 코어를 번갈아가면서 사용한다.

    만약 Thread 2개, 코어가 2개라면, 한 Thread가 하나의 코어를 사용하여 병렬적으로 작업을 처리할 수 있다.

    Thread의 스케줄링은 Thread의 우선순위, 운영체제의 스케줄링, 코어의 개수, Thread 등 여러환경에 영향을 받기 때문에, Thread의 실행순서를 완벽히 예측하기는 어렵다.
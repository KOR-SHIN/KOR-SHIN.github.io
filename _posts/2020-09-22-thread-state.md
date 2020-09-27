---
title : Thread State(Thread 상태)
layout : posts
categories :
 - JAVA
tag :
 - JAVA
---

## __Thread State(Thread 상태)__
---

- Thread의 상태
	- NEW
		- Thread가 생성되었지만 아직 start()가 호출되지 않은 상태

	- RUNNABLE
		- Thread가 실행중이거나 실행대기중인 상태

	- BLOCKED
		- 동기화 블럭에 의해 일시정지된 상태 (Lock이 풀릴 때 까지 기다리는 상태)

	- WAITING
		- THREAD의 작업이 종료되지 않았지만 대기중인 상태, 즉 실행불가능(UNRUNNABLE)한 상태

	- TIMED-WAITING
		- WAITING상태와 동일한 상태, 하지만 대기시간이 정해져 있음

	- TERMINATED
		- Thread가 작업을 종료된 상태

- `[Sample Code]`

    ```java
    public class T10_ThreadStateTest {

    	public static void main(String[] args) {
    		statePrintThread spt = new statePrintThread(new TargetThread());
    		spt.start();
    	}
    	
    }

    class TargetThread extends Thread {
    	@Override
    	public void run() {
    		for(long i=1; i<10000000000L; i++) {
    			// 시간지연 loop
    			// RUNNABLE 
    		}
    		try {
    			Thread.sleep(1500); // TIMED_WAITING
    		} catch(InterruptedException e) {
    			e.printStackTrace();
    		}
    		for(long i=1; i<1000000000L; i++) {
    			// 시간지연 loop
    		}
    	}
    	
    }

    /**
     * Thread의 상태를 출력하기 위한 변수
     */
    class statePrintThread extends Thread {
    	private Thread targetThread; // 상태출력용 Thread를 저장할 변수
    	
    	public statePrintThread(Thread targetThread) {
    		this.targetThread = targetThread;
    	}
    	
    	@Override
    	public void run() {
    		while(true) {
    			Thread.State state = targetThread.getState();
    			System.out.println("Current Status : " + state);
    			
    			if(state == Thread.State.NEW) {
    				// State가 NEW이면 Thread를 실행함
    				targetThread.start();
    			}
    			
    			if(state == Thread.State.TERMINATED) {
    				// Thread가 소멸되면 반복문을 종료함
    				break;
    			}
    			
    			try {
    				Thread.sleep(500);
    			} catch(InterruptedException e) {
    				e.printStackTrace();
    			}
    		}
    	}
    }
    ```

    `출력결과`

    ```java
    Current Status : NEW
    Current Status : RUNNABLE
    Current Status : RUNNABLE
    Current Status : RUNNABLE
    Current Status : RUNNABLE
    Current Status : TIMED_WAITING
    Current Status : TIMED_WAITING
    Current Status : TIMED_WAITING
    Current Status : TERMINATED
    ```

`Thread state`, `Thread life Cycle`등으로 검색하면 Thread의 상태에 대해 더욱 자세히 알 수 있다.<br>
현재 예제에서는 BLOCKED과 WAITING이 나와있지 않은데, WAITING은 TIMED_WAITING에서 대기시간을 지정해주지 않으면 WAITING이 된다.<br>
BLOCKED는 추후에 동기화 블럭을 사용하는 예제에서 더욱 자세히 알아볼 예정이다.
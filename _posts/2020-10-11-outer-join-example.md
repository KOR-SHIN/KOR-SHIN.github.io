---
title : JOIN의 종류(외부조인)
layout : posts
categories :
 - ORACLE
 - DATABASE
tag :
 - ORACLE
 - DATABASE
---

## __외부조인(OUTER JOIN)__
---
<a href="https://kor-shin.github.io/oracle/database/join-example/" tager="_blank">이전 포스팅</a>에서는 `등가조인`, `비등가조인`, `자체조인`에 대해서 알아보았습니다.<br>
이번 포스팅에서는 `외부조인(outer join)`에 대해서 알아보려고 합니다.<br>
등가조인에서는 조인 조건의 데이터가 일치하는 정보만을 출력하였습니다.<br>
다시 말해서 조인 조건의 데이터 중 한쪽이 `NULL`이면 정보가 출력되지 않는다는 것이죠.<br>
하지만, 조인 조건의 데이터 중 한쪽이 `NULL`임에도 불구하고 결과에 출력되어야 하는 경우가 있습니다.<br>
이렇게 조인 조건의 한 쪽 데이터가 NULL이어도 강제로 결과를 출력하는 방식을 `외부조인(outer join)`이라고 합니다.<br>

외부조인은 아래와 같이 왼쪽과 오른쪽으로 나누어집니다.<br>

- 왼쪽 외부조인(Left Outer Join)
    - WHERE TABLE1.COL = TABLE2.COL(+)
- 오른쪽 외부조인(Right Outer Join)
    - WHERE TABLE1.COL(+) = TABLE2.COL

## __왼쪽 외부조인(Left Outer Join)__
---

`[왼쪽 외부조인(Left Outer Join) 예시]`
```java
SELECT E1.EMPNO, E1.ENAME, E1.MGR,
       E2.EMPNO, AS MGR_EMPNO,
       E2.ENAME AS MGR_NAME
  FROM EMP E1, EMP E2
 WHERE E1.MGR = E2.EMPNO(+)
ORDER BY E1.EMPNO
```
`[출력결과]`

<img src="https://user-images.githubusercontent.com/67519366/95675768-8bc80780-0bf4-11eb-9beb-2702690b54c8.png">

결과를 보면, `KING`의 데이터에 `NULL`값이 포함되어 있는걸 볼 수 있습니다.<br>
등가조인이었다면 출력되지 않는 데이터이지만, 외부조인이기 때문에 결과에 포함된 것입니다.<br>

```java
WHERE E1.MGR = E2.EMPNO(+)
```
부분을 살펴보면, `(+)`표시가 오른쪽에 포함되었습니다.<br>
`(+)`는 외부조인을 의미하는것이며, 오른쪽에 포함됐을경우 왼쪽 외부조인을 의미합니다.<br>
왼쪽 외부조인은 `WHERE절의 왼쪽열을 기준으로 오른쪽 열의 데이터가 없어도 결과로 출력한다`라고 생각하면 됩니다.
따라서 `E2.EMPNO`의 데이터가 존재하지 않아도, `E1.MGR`의 데이터가 존재한다면 모두 출력됩니다.

## __오른쪽 외부조인(Right Outer Join)__
---

`[오른쪽 외부조인(Right Outer Join) 예시]`
```java
SELECT E1.EMPNO, E1.ENAME, E1.MGR,
       E2.EMPNO AS MGR_EMPNO,
       E2.ENAME AS MGR_NAME
  FROM EMP E1, EMP E2
 WHERE E1.MGR(+) = E2.EMPNO
ORDER BY E1.EMPNO
```

`[출력결과]`

<img src="https://user-images.githubusercontent.com/67519366/95675869-435d1980-0bf5-11eb-86e5-de118378f024.png">

결과를 어느정도 예상하신 분도 계실거라고 생각합니다.<br>

```java
WHERE E1.MGR(+) = E2.EMPNO
```
이번에는 `(+)`표시가 왼쪽에 붙어있으니 오른쪽 외부조인(Right Outer Join)이고, 오른쪽 외부조인은 `WHERE절의 오른쪽열을 기준으로 왼쪽열의 데이터가 없어도 결과로 출력한다`라고 생각하면 됩니다.<br>
따라서 `E1.MGR`의 데이터가 존재하지 않아도, `E2.EMPNO`의 데이터가 존재한다면 모두 출력됩니다.<br>
일반적으로 외부조인을 사용할때는 `(null)`이라고 노출되지 않도록 `NVL`함수를 사용하여 NULL값을 처리합니다.<br>

## __조인 다이어그램(JOIN DIAGRAM)__
---

<div style="width:100%; text-align:center;" >
    <img src="https://user-images.githubusercontent.com/67519366/95676147-0eea5d00-0bf7-11eb-9c72-3a36ec555ea7.jpg" width="70%"> 
</div>
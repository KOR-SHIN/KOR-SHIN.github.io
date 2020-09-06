---
layout : posts
title : CHAR, VARCHAR2 (ORACLE)
categories :
 - ORACLE
 - DATEBASE
tag :
 - ORACLE
comments : true
toc : true
---

## __문자열__
---
오라클의 문자열 자료는 `' '(single quote)`로 묶어서 표현되며, 문자열 자료형은 `CHAR`, `VARCHAR`, `VARCHAR2`, `LONG`, `CLOB`, `NVARCHAR`, `NCLOB` 등이 있습니다.<BR>
`VARCHAR2`는 오라클에서만 사용하는 문자열 자료형입니다.<BR>
`VARCHAR`와 기능적인 차이는 거의 없지만 `ORACLE`에서는 `VARCHAR2`를 사용할 것을 권장하고 있습니다.<BR>
오늘 포스트에서는 가장 많이 사용되는 `CHAR`와 `VARCHAR2`에 대해서 알아보겠습니다.

## __CHAR__
---
`CHAR`는 고정길이 문자열이며 기본키 컬럼의 데이터 타입으로 자주 사용합니다.<BR>
문자열은 왼쪽부터 저장되고 남는 공간은 공백으로 채워집니다.
<BR>
- 사용형식
    - `COLUMN_NAME CHAR( SIZE [BYTE | CHAR] )`
    - `[BYTE | CHAR]는 생략가능 합니다.`
- BYTE
  - 2000BYTE 까지 사용가능하다.
  - `[BYTE | CHAR]`부분을 생략하면 기본타입은 BYTE로 설정된다.
  - CHAR를 사용하는 경우 `SIZE`는 글자수 자체를 의미한다.

BYTE를 사용하게 될 경우 주의해야 할 점이 있습니다.<BR>
한글은 한 글자에 `3 BYTE (ENCODING 종류에 따라 다를 수 있습니다)`크기를 가지기 때문에 한글 2000글자는 6000 BYTE의 크기입니다.
따라서 한글을 사용할 때는 `SIZE`를 얼마로 넣을지 생각하셔야 합니다.<BR>

`CHAR 예제`

```java

CREATE TABLE TEMP01 (
  COL1 CHAR(10),
  COL2 CHAR(10 BYTE),
  COL3 CHAR(10 CHAR));

INSERT INTO VALUES('대한민', '대한민', '대한민국');

SELECT LENGTHB(COL1), LENGTHB(COL2), LENGTHB(COL3)
  FROM TEMP01
```

COL1은 `[CHAR|BYTE]`를 생략했기 때문에 DEFAULT TYPE인 `BYTE`타입으로 설정되었고, COL2와 COL3는 타입을 지정해주었습니다.<BR>
위에서 설명했듯이 한글은 한 글자에 `3 BYTE`의 크기를 가집니다.<BR>
COL3에서 사용한 `CHAR`는 글자 수 자체를 의미합니다.<BR>
따라서 영어, 한글에 상관없이 `10글자`를 입력할 수 있습니다.<BR>
아래에 LENGTHB는 COLUMN의 기억공간을 BYTE단위로 반환해줍니다.
위 예제에서 반환값은 순서대로 `10, 10, 18`입니다.<BR>
입력한 글자수와 상관없이 처음에 지정해 준 기억공간만큼을 사용하고 있는것을 알 수 있습니다.

`CHAR 예제 2`

```java
UPDATE TEMP01
   SET COL1 = '대한민국'

UPDATE TEMP01
   SET COL2 = '대한민국'
```

위의 예제는 예상하신것처럼 제대로 실행되지 않습니다.<BR>
COL1, COL2는 10 BYTE의 크기를 가지지만, 우리는 12 BYTE크기를 입력했기 때문이죠<BR>
이런식으로 지정가능한 크기를 넘겼을 경우<BR> 
`ORA-12899: value too large for column` 오류가 출력됩니다.

## __VARCHAR2__
---
`VARCHAR2`는 가변길이 문자열을 저장하는데 사용되며 `4000 BYTE`까지 사용이 가능합니다.<BR>
위에서 설명한 `CHAR`는 고정된 길이를 가지기 때문에 입력가능한 범위보다 적게 입력해도 나머지 공간은 공백으로 채워진다고 설명했습니다<BR>
하지만 `VARCHAR2`는 입력가능한 범위보다 적게 입력하면 남는공간을 알아서 제거해줍니다.

- 사용형식
  - `COLUMN NAME VARCHAR2(SIZE [BYTE | CHAR])`

`VARCHAR2 예제`

```java
CREATE TABLE TEMP02 (
  COL1 VARCHAR2(4000),
  COL2 VARCHAR2(4000 BYTE),
  COL3 VARCHAR2(4000 CHAR));

INSERT INTO TEMP02
  VALUES ('대한민국대한민국대한민국', 'KOREAKOREAKOREA', 'IL POSITION')

SELECT LENGTHB(COL1), LENGTHB(COL2), LENGTHB(COL3)
  FROM TEMP02
```

`VARCHAR2`는 가변길이의 문자열이라고 설명했습니다.<BR>
위의 예제에서 LENGTHB의 반환값은 얼마일까요?<BR>
`CHAR`에서는 입력가능 범위보다 적게 입력해도 처음에 지정한 크기 그대로를 반환했습니다.<BR>
하지만 위의 예제에서 반환값은 `36, 15, 11`입니다.<BR>
`SIZE`를 아무리 크게 지정해도 입력한 만큼만 기억공간을 사용하는 것을 알 수 있습니다.<BR>

### P.S
---
현재 다니고 있는 개발원에서 8월 31일부터 초급 프로젝트를 진행하고 있습니다.<br>
프로젝트 진행중에도 가급적이면 끊기지 않게 블로그 포스팅을 이어나가고 싶었는데, 부족한 만큼 프로젝트에만 신경쓰기도 시간이 모자라고 저의 부족함을 더욱 절실히 느끼고 있습니다.<br>
프로젝트가 끝나면 고급자바와 html, css수업을 진행한다고 합니다.<br>
수업들으면서 제가 공부했던 내용을 꾸준히 포스팅하겠습니다.<br>







---
title: Apache tomcat install(아파치 톰캣 설치)
layout: posts
categories:
 - Jsp
 - Servlet
tag:
 - Jsp
 - Servlet
---

## __Apache Tomcat 설치__
---
<a href="http://tomcat.apache.org/" target="_blank">Apache Tomcat</a>를 클릭하여 다운로드 할 홈페이지로 접속합니다.<br>

<img src="https://user-images.githubusercontent.com/67519366/99554941-1aede980-2a03-11eb-95e4-f041c5fc5a34.png">

위와 같은 화면이 나왔다면 왼쪽에 `Download`에서 `tomcat 8`을 클릭합니다.<br><br>

<img src="https://user-images.githubusercontent.com/67519366/99555077-41138980-2a03-11eb-91b4-128a0181e892.png">

`tomcat 8`을 클릭하면 위와같은 화면이 나오는데 `Binary Distributions`하위에 `Core`아래에 있는 `zip`을 클릭하여 다운로드 받습니다.<br><br>

<img src="https://user-images.githubusercontent.com/67519366/99555647-df075400-2a03-11eb-960b-78bc4c0c1f0d.png">


저는 `d:/tomcat`경로에 다운로드받은 압축파일을 옮긴 후 압축을 풀어주었습니다.<br>
`apache-tomcat-8.5.60`폴더를 제외하고는 개인적으로 설치한것이기 때문에 무시하셔도 됩니다.<br>
이제 설치를 완료했으니, 환경변수에서 경로를 설정해주겠습니다.<br>
<br>

<img src="https://user-images.githubusercontent.com/67519366/99556468-e4b16980-2a04-11eb-9ecb-88d1cf111cea.png">

Window검색창에서 `sysdm.cpl`을 입력하고, 상단탭에서 고급을 클릭하여 환경변수로 들어갑니다.<br>
환경변수에서 하단의 시스템 변수쪽에서 새로만들기를 클릭하고 다음과 같이 입력합니다.<br>

`변수 이름 : CATALINA_HOME`<br>
`변수 값 : apache-tomcat-8.5.60 폴더 경로`

## __Tomcat 실행__
---
Apache Tomcat을 설치하고 경로설정까지 완료했으니 Terminal을 이용하여 서버를 실행시켜 보겠습니다.

`window + R`을 눌르고 `cmd`를 입력하여 터미널을 열어줍니다.<br>

<img src="https://user-images.githubusercontent.com/67519366/99558581-3bb83e00-2a07-11eb-8934-175465990286.png">
<br>

터미널에서 `cd %catalina_home%`이라고 입력하고 `d:`을 입력하면 시스템 환경변수에 설정해놓은 `catalina_home`경로로 이동됩니다.<br>
그리고 `cd bin`을 입력하여 `bin`디렉토리 안으로 이동합니다.<br>
여기서 `bin`디렉토리는 `binary file`들이 위치한 폴더입니다.<br>
내부에는 확장자가 `.bat` `.sh`등으로 된 파일들이 이루어져 있는데 이러한 파일들은 Terminal에서 명령어를 실행시켜주는 역할을 합니다.<br>
<br>
<img src="https://user-images.githubusercontent.com/67519366/99559176-d4e75480-2a07-11eb-8af7-867e3d27e5de.png">

이제 `startup.bat`를 입력하면 Terminal한 개 더 띄워질겁니다.<br><br>

<img src="https://user-images.githubusercontent.com/67519366/99559419-20016780-2a08-11eb-96df-024d7cd28c87.png">

아마 대부분의 분들에게 위와같은 에러메세지가 나올것입니다.<br>
한글이 깨져서 나오지만 중요한부분은 `org.apache.catalina.LifecycleException`과 `java.net.BindException: Address already in use: bind`부분입니다.<br>
Exception의 종류와 원인을 알려주는 부분입니다.<br>
Lifecycle Exception이고 원인은 Connector가 사용하는 주소를 이미 누군가가 사용하고 있어서 에러가 발생한것 같습니다.<br>
에러를 해결하기 위해서 tomcat디렉토리 안에있는 `conf`디렉토리에서 `server.xml`을 열어보겠습니다.<br>
`conf`디렉토리는 `configuration`의 줄임말로 환경설정 파일들이 위치하는 디렉토리입니다.<br><br>

<img src="https://user-images.githubusercontent.com/67519366/99560127-dd8c5a80-2a08-11eb-81d8-08ba815a10ec.png">

`server.xml`에서 `69 Line`쯤에 `<Connector>`라는 태그가 걸린 부분을 보면 `port=8080`이라고 적혀있습니다.<br>
아까 발생했던 에러는 이미 누군가가 8080번 포트를 사용하고 있기때문에 발생한 것입니다.<br>
따라서 우리는 `9090`번으로 포트번호를 변경해주고 다시 톰캣을 실행시켜보겠습니다.<br>
`server.xml`을 변경한 후 Terminal을 종료했다가 다시 켜서 실행해야 합니다.<br>
혹시나 포트번호를 변경했는데도 같은 에러가 발생한다면 포트번호를 다시 바꿔야합니다.<br><br>
만약 실행시 오류가 발생하지 않는다면 이제 브라우저를 열어서 구동중인 톰캣서버에 접속해보겠습니다.<br><br>

<img src="https://user-images.githubusercontent.com/67519366/99560957-cd28af80-2a09-11eb-8b52-2a9a991f0812.png">

주소창에 `localhost:portnumber(9090)`을 입력해서 위와같은 화면이 나온다면 정상적으로 톰캣서버가 실행중인 것입니다.<br>
만약 `server.xml`에서 `connector`의 port를 `80`으로 했다면 뒤에 portnumber는 생략하고 `localhost`만 입력해도 됩니다.<br>
또한 `localhost`와 같은 의미로 `127.0.0.1:9090`을 주소창에 입력해도 됩니다.<br>
`127.0.0.1`은 `loopback address`로써 `localhost`와 같다고 생각하시면 됩니다.<br>
이제 문제없이 서버를 동작시켜봤다면 다시 Terminal로 돌아가서 `shutdown.bat`을 입력하여 서버를 종료시켜줍니다.<br>







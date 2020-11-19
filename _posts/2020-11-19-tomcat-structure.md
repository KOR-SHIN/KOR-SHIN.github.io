---
title: Tomcat 구조
layout: posts
categories:
 - Jsp
 - Servlet
tag:
 - Jsp
 - Servlet
---

## __bin__
---
`bin`은 톰캣을 실행하고, 종료시키는 역할을 하는 스크립트(.bat, .sh) 파일이 위치하는 폴더입니다.

## __conf__
---
`conf`는 `configuration`으로써 단어 그대로 톰캣의 설정파일들이 위치하는 폴더입니다.<br>
`conf`폴더안에 `server.xml`을 열어보면 `connector`나 `Host` 태그에서 설정을 변경할 수 있습니다.<br>
`connector`태그 안에는 현재 사용하는 port번호, 프로토콜 등을 확인하거나 변경 할 수 있습니다.<br>
`Host`태그 안에는 hostName, appBase등을 확인할 수 있습니다.<br>

## __lib__
---
`lib`는 `library`로서 톰캣을 구동하는데 필요한 라이브러리(.jar)가 위치하는 폴더입니다.

## __temp__
---
`temp`는 `JVM`에 사용되는 임시 디렉토리입니다.

## __webapps__
---
`webapps`는 톰캣이 관리하는 애플리케이션들이 위치하는 폴더입니다.<br>
`webapps`안에 있는 폴더들의 이름은 `ContextName`이고 URL상에서 `ContextPath`로 사용됩니다.<br>
webapps안에 있는 애플리케이션들은 공통적으로 `WEB-INF`라는 폴더를 가지고 있습니다.<br>
`WEB-INF`는 `톰캣의 금고`라고 불리며, WEB-INF 내부에 있는 파일들은 URL로 접근할 수 없습니다.<br>
따라서 WEB-INF 안에 있는 파일들은 외부에 노출되면 안되는 파일들이 위치하게 됩니다.<br>
모든 WEB-INF안에는 `web.xml`이라는 설정 파일이 존재합니다.

## __work__
---
Jsp파일을 Servlet형태로 변환한 .java파일과 .class파일이 저장되는 디렉토리입니다.
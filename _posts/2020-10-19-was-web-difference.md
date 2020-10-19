---
title: Web Server와 WAS
layout: posts
categories:
 - NETWORK
tag:
 - NETWORK
---

## __Intro__
---
본 포스팅은 <a href="https://gmlwjd9405.github.io/2018/10/27/webserver-vs-was.html"> HeeJeong Kwon</a>님의 블로그를 참고하였습니다.

## __정적페이지와 동적페이지__
---
`정적페이지(Static pages)`는 반환결과가 항상 같은 페이지를 의미하며 가장 대표적인 정적콘텐츠는 html, css, image등이 있습니다.<br>
`동적페이지(Dynamic Pages)`는 전달되는 파라미터의 내용에 따라 반환결과가 달라지는 페이지를 의미하며, 반환결과는 웹 서버 위에서 동작하는 프로그램을 통해 생산된 결과물입니다.<br>
웹 서버 위에서 동작하는 대표적인 프로그램으로는 `Servlet(WAS 위에서 동작하는 Java Program)`이 있습니다.


## __Web Server__
---
`Web Server`는 HTTP 프로토콜을 기반으로 클라이언트(웹 브라우저)의 요청을 서비스 하는 기능을 담당합니다.<br>
이러한 Web Server는 하드웨어와 소프트웨어로 개념을 구분할 수 있습니다.<br>

- 하드웨어
    - Web Server가 설치된 컴퓨터
- 소프트웨어
    - 클라이언트(웹 브라우저)로부터 HTTP 요청을 받아 정적콘텐츠(Static Contents)를 제공하는 프로그램

이러한 Web Server의 동작은 두 가지로 분류할 수 있습니다.

- Static Contents를 요청받은 경우
    - WAS에 접근하지 않고 클라이언트가 요청한 Content를 반환
- Dynamic Contents를 요청받은 경우
    - WAS에게 클라이언트의 요청을 전달하고, WAS에게 처리결과를 받아서 클라이언트에게 반환

## __WAS(Web Application Server)__
---
`WAS(Web Application Server)`는 DB조회나 다양한 로직 처리를 요구하는 동적 콘텐츠를 제공하기 위해 만들어진 <a href="https://ko.wikipedia.org/wiki/%EB%AF%B8%EB%93%A4%EC%9B%A8%EC%96%B4" target="_blank">미들웨어(MiddleWare)</a>입니다.<br>
WAS는 `Web Sever + Web Container`의 역할을 수행하는데, Web Container는 JSP, Servlet을 실행시킬 수 있는 소프트웨어를 의미합니다.<br>
따라서 WAS는 JSP, Servlet의 구동 환경을 제공한다고 할 수 있습니다.<br>

- WAS의 주요기능
    - 프로그램 실행 환경과 DB접속 기능 제공
    - 여러개의 트랜잭션 관리
    - 업무를 처리하는 비즈니스 로직 수행

## __Server와 WAS__
---
WAS를 설명하면서 WAS는 Web Server + Web Container라고 설명했듯이, WAS단독으로도 정적데이터와 동적데이터를 모두 처리할 수 있습니다.<br>
하지만 WAS와 Web Server를 함께 사용하는것이 일반적이며 이렇게 사용하는 이유는 여러가지가 있습니다.<br>

- Web Server만 사용하는 경우
    - 웹 페이지에는 정적컨텐츠와 동적컨텐츠가 모두 존재하기 때문에 Web Server만을 사용하면 동적컨텐츠를 처리할 수 없습니다.
- WAS만 사용하는 경우
    - WAS는 단독으로 정적컨텐츠와 동적컨텐츠를 모두 처리할 수 있지만, WAS가 정적컨텐츠까지 처리하게 될 경우 정적컨텐츠 처리로 인한 부하가 커지고 그에따라 동적컨텐츠 수행속도가 느려지며 결과적으로 페이지 노출시간이 길어지는 문제가 발생합니다.
- Web Server와 WAS를 함께 사용하는 경우
    - Web Server는 주로 WAS의 앞단에 위치하여 사용자의 정적컨텐츠 요청을 WAS에게 전달하지 않고 빠르게 반환하기 때문에 정적컨텐츠에 대한 수행속도와 WAS의 부하를 줄여줍니다.
    - 결론적으로 Web Server를 WAS 앞단에 위치하여 WAS를 Web Server의 플러그인처럼 사용하면 효율적인 분산 처리가 가능합니다.

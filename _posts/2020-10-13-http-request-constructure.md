---
title: HTTP 개념 및 Request 구조
layout: posts
categories:
 - NETWORK
tag:
 - NETWORK
---
## **Intro**
---
본 게시물은 아래의 게시물을 참고하여 포스팅하였습니다.

[https://velog.io/@teddybearjung/HTTP-구조-및-핵심-요소](https://velog.io/@teddybearjung/HTTP-%EA%B5%AC%EC%A1%B0-%EB%B0%8F-%ED%95%B5%EC%8B%AC-%EC%9A%94%EC%86%8C)

[https://joshua1988.github.io/web-development/http-part1/#http-request--http-response](https://joshua1988.github.io/web-development/http-part1/#http-request--http-response)

[https://ko.wikipedia.org/wiki/HTTP_상태_코드](https://ko.wikipedia.org/wiki/HTTP_%EC%83%81%ED%83%9C_%EC%BD%94%EB%93%9C)

## **Protocol**
---
Protocol이란 서버와 클라이언트간의 약속된 통신규약입니다.

클라이언트가 서버에게 데이터를 요청할 때, 어떠한 프로토콜을 사용하여 요청할지 명시하고, 서버는 클라이언트의 요청을 받아 데이터를 제공할 때 클라이언트와 동일한 프로토콜을 사용합니다.

따라서 클라이언트와 서버는 약속된 방식으로 통신하게 되는것입니다.

## **HTTP**
---
HTTP는 HyperText Transfer Protocol의 약자로서 하이퍼텍스트(HTML)문서를 교환하기 위해 만들어진 프로토콜입니다.

기본적으로 웹에서는 브라우저와 서버간에 데이터를 주고받기 위한 방식으로 HTTP 프로토콜을 사용합니다.

이러한 HTTP 프로토콜은 일반적으로 TCP/IP 통신 위에서 동작하며 상태가 없는(Stateless)프로토콜이라고 합니다.

상태가 없다는 뜻은 데이터를 주고 받기 위한 각각의 데이터 요청이 서로 독립적으로 관리가 된다는 의미로써 요청과 응답이 서로 연결되어 있지 않다는 것입니다.

이러한 특징으로 서버는 세션과 같은 별도의 추가 정보를 관리하지 않아도 되고, 다수의 요청 처리 및 서버의 부하를 줄일 수 있는 이점이 생깁니다.

## **HTTP Request 구조**
---
HTTP Request 메세지는 크게 Start Line, headers, body로 구성된다.

## **Start Line**
---
이름 그대로 HTTP Request의 첫 라인입니다.

HTTP Request Start Line은 HTTP Method, Request target, HTTP Version 총 3부분로 이루어져 있습니다.

- HTTP Method
    - 해당 request가 서버에게 요청하는 동작을 정의하는 부분
    - GET과 POST가 가장 많이 사용된다.
- Request target
    - 해당 request가 전송되는 URI(Uniform Resourse Identifier)
- HTTP Version
    - 의미 그대로이며 1.0, 1.1 등이 있다.

> ex) GET /search HTTP/1.1

## **Header**
---
해당 request에 대한 추가 정보(additional information)을 담고 있는 부분입니다.

예를들어 request 메세지의 body 총 길이 등이 있습니다.

Header는 Key:Value 구조를 가지고 있으며 예를들어 HOST:google.com에서 Key는 HOST ,Value는 google.com입니다.

Header역시 Start Line과 동일하게 3부분으로 나누어 지지만 여기서 설명하지는 않습니다.

3부분은 General Headers, Request headers, entity입니다.

## **Body**
---
해당 Request의 실제 메세지, 내용을 담고 있는 부분입니다.

Body는 필수적인 부분은 아닙니다.

예를들어 GET 메서드의 같은경우는 서버에 요청한 정보를 읽어오기만 하기때문에 서버로 전송하는 메세지나 내용은 없습니다.

따라서 GET메서드의 경우에는 Body가 없습니다.

하지만 POST메서드는 서버에게 데이터의 생성, 수정, 삭제를 요구하기 때문에 서버로 전송하는 메세지나 내용이 있습니다.

따라서 POST메서드는 Body를 포함합니다.

## **HTTP Request Method**
---
HTTP Request Method는 주어진 리소스에 수행하길 원하는 행동을 나타냅니다.

주어진 리소스라는 것은 우리가 URL을 이용하여 서버에 요청한 특정한 데이터라고 생각하면 됩니다.

- GET
    - GET 메서드는 서버에게 데이터 검색을 요청합니다.
- HEAD
    - HEAD 메서드는 GET 메서드의 요청과 동일한 응답을 요구하지만, 응답 본문(body)을 포함하지 않습니다.
- POST
    - POST 메서드는 특정 리소스에 엔터티(entity)를 제출할 때 사용합니다. 종종 서버의 상태 변화나 부작용을 일으킬 수 있습니다.
    - 여기서 엔터티를 제출한다는 것은 서버에 새로운 데이터를 생성, 삭제, 수정을 요청한다는 것입니다.
- PUT
    - PUT 메서드는 서버에 데이터 저장(생성, 수정)을 요청합니다.
    - POST 메서드로 동일한 결과를 구현할 수 있기때문에 많이 사용되지는 않습니다.
- DELETE
    - 서버에 데이터 삭제를 요청합니다.
    - PUT 메서드와 같은 이유로 많이 사용되지 않습니다.
- TRACE
    - 최종 자원까지 경로를 따라 메세지 루프백 테스트를 수행합니다.

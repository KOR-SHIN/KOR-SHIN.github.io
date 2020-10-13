---
title: HTTP Response 구조
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

## **HTTP Response 구조**
---
Response도 Request와 마찬가지로 3부분으로 구성되며 각 부분은 Status Line, Header, Body입니다.

## **Status Line**
---
Response의 상태를 간략하게 나타내는 부분입니다.

Request의 Start Line처럼 3부분으로 구성되어 있습니다.

- HTTP Version
- Status Code
    - 대표적으로 200과 404가 있습니다.
    - 200은 요청을 성공적으로 처리했다는 의미이고, 404는 요청에 대한 결과를 찾을 수 없다는 의미입니다.
- Status Text
    - 응답 상태를 간략하게 설명해주는 부분입니다.
    - Status Code가 404라면 Status Text는 'Not Found'입니다.

> ex) HTTP/1.1 404 Not Found

## **Header**
---
Request의 headers와 동일한 구조입니다.

하지만 Response에서만 사용되는 header 값들이 있습니다.

예를들어 User-Agent대신에 Server헤더가 사용됩니다.

## **Body**
---
Request의 body와 보통 동일합니다.

Request와 마찬가지로 모든 Response가 body를 포함하지는 않습니다.

클라이언트측으로 전송할 데이터가 없다면 body는 비어있는 상태가 됩니다.

## HTTP Status Code
---
HTTP Request Method는 클라이언트가 설정하는 정보라면, HTTP Status Code는 서버에서 설정해주는 응답정보입니다.

 HTTP Status Code는 아래와 같은 분류를 가지고 있습니다.

 HTTP Status Code는 

- 100번대 (조건부 응답)
    - 100(계속)
        - 클라이언트는 요청을 지속해야한다. 서버가 이 코드를 제공하여 요청의 첫 번째 부분을 받았고 나머지 부분을 기다린다는 의미이다.
    - 101(프로토콜 전환)
        - 클라이언트가 서버에 프로토콜 전환을 요청했으며 서버가 승인중이라는 것을 의미한다.

- 200번대 (성공)
    - 200(성공)
        - 서버가 클라이언트의 요청을 제대로 수행했다는 의미로써 주로 요청한 페이지를 제공했다는 의미로 사용된다.
    - 204(콘텐츠 없음)
        - 서버가 요청을 성공적으로 처리햇지만 콘텐츠를 제공하지 않는다.
    - 205(콘텐츠 재설정)
        - 서버가 요청을 성공적으로 처리했지만 콘텐츠를 표시하지 않는다.
        - 204 응답과 달리 이 응답은 클라이언트가 문서 보기를 재설정 할 것을 요청한다 (예: 새입력을 위한 양식 비우기)
    - 206(일부 콘텐츠)
        - 서버가 GET 요청의 일부만 성공적으로 처리했는 의미이다.

- 300번대 (리다이렉션)
    - 301(영구이동)
        - 요청한 페이지를 새 위치로 영구적으로 이동했다는 의미이다.
        - GET 또는 HEAD 요청에 대한 응답으로 이 응답을 표시하면 클라이언트가 자동으로 새 위치로 전달된다.
    - 303(기타 위치 보기)
        - 클라이언트가 다른 위치에 별도의 GET 요청을 하여 응답을 검색할 경우 서버는 이 코드를 표시한다.
        - HEAD 요청 이외의 모든 요청을 다른 위치로 자동전달한다.
    - 304(수정되지 않음)
        - 마지막 요청 이후 요청한 페이지가 수정되지 않았다는 것을 의미한다.

- 400번대 (요청 오류)
    - 400(잘못된 요청)
        - 서버가 요청의 구문을 인식하지 못하는 경우이다.
    - 401(권한 없음)
        - 인증이 필요하다는 것을 의미한다.
        - 서버는 로그인이 필요한 페이지에 대해 이 요청을 제공할 수 있다.
        - 권한없음보다는 인증안됨과 더 가까운 의미를 가진다.
    - 404(Not Found, 찾을 수 없음)
        - 서버가 요청한 페이지(Resource)를 찾을 수 없다.
        - 예를 들어 서버에 존재하지 않는 페이지에 대한 요청이 있을 경우 이 코드를 제공한다.

- 500번대 (서버 오류)
    - 501(구현되지 않음)
        - 서버에 요청을 수행할 수 있는 기능이 없다.
        - 예를 들어 서버가 요청 메서드를 인식하지 못할 때 이 코드를 표시한다.
    - 503(서비스를 사용할 수 없음)
        - 서버가 오버로드되었거나 유지관리를 위해 다운되었기 때문에 현재 서버를 사용할 수 없다
        - 503코드가 제공되는 경우는 대부분 일시적인 상태이다.
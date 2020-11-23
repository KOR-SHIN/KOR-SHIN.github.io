---
title: URL과 URI
layout: posts
categories:
 - NETWORK
tag:
 - NETWORK
---

## __URL__
---
`URL`은 `Uniform Resource Locator`의 약자로써 리소스의 위치를 통해 식별하는 방법을 의미합니다.<br>

## __URN__
---
`URN`은 `Uniform Resource Name`의 약자로써 리소스의 이름을 통해 식별하는 방법을 의미합니다.<br>
하지만 이름으로 리소스를 식별하는 방법은 이름이 중복되는 문제, 관리의 불편성 때문에 현재는 거의 사용되지 않는 개념입니다<br>

## __URC__
---
`URC`는 `Uniform Resource Content`의 약자로써 리소스의 속성을 통해 식별하는 방법을 의미합니다.<br>
이 방법은 예를들어 서점에서 책을 검색할 때 책의 제목, 작가, 도서분류 등을 통해 검색하는 것과 같습니다.<br>
리소스의 속성으로 사용할 수 있는것이 매우 많기 때문에 식별자로서의 의미가 없어집니다.<br>
따라서 `URN`처럼 현재는 거의 사용되지 않는 개념입니다.<br>

## __URI__
---
`URI`는 `Uniform Resource Identifier`의 약자입니다.<br>
`URI`는 `URL`, `URN`, `URC`의 개념을 모두 포괄하고 있는 개념입니다.<br>

## __URL vs URI__
---
`URN`과 `URC`는 현재 거의 사용되지 않는 개념이기 때문에 많이 사용되는 `URL`과 `URI`에 대한 간단한 차이를 보려고 합니다.<br>
예를들어 `http://example.com/example.html?id=123`라는 주소가 있다고 한다면
`http://example.com/example.html`은 `URL`이면서 `URI`입니다.<br>
하지만 `http://example.com/example.html?id=123`는 queryString에 따라 결과가 달라지기 때문에 queryString이 식별자 역할을 하고 있다고 할 수 있습니다.<br>
따라서 `http://example.com/example.html?id=123`는 `URI`지만 `URL`은 아닌것입니다.<br>
`URL`은 `http://example.com/example.html`까지인 것이죠.<br>
만약 `http://example.com/example.html?id=123`과 `http://example.com/example.html?id=456`두 주소가 있다면, 두 주소는 같은 URL을 가지지만 다른 URI를 가진다고 할 수 있습니다.


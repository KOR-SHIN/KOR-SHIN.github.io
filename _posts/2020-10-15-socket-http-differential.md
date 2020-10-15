---
title: Socket통신과 HTTP통신
layout: posts
categories:
 - NETWORK
tag :
 - NETWORK
---

## Socket통신
---
`Socket`통신은 Server와 Client가 특정포트에 `실시간`으로 연결되어 있는 통신방식입니다.<br>
UDP를 사용하여 비연결지향 통신방식을 사용할 수 있지만, Socket통신의 경우 대부분이 TCP를 사용하여 연결지향형 통신방식을 사용합니다.<br>
연결지향형이기 때문에 Server와 Client가 양방향통신이 가능합니다.<br>
양방향통신이 가능하다는 것은 클라이언트와 Server와 서로 Request를 할 수 있다는 의미입니다.<br>
Socket통신은 실시간 스트리밍, 채팅 등에 많이 사용됩니다.

`[Socket 통신과정 예시]`

<img src="https://user-images.githubusercontent.com/67519366/96106130-ccd25b80-0f15-11eb-91ea-d7d7c1fee6a7.png">

사진출처 : <a href="https://12bme.tistory.com/297">https://12bme.tistory.com/297</a>

`[Java Socket 통신과정 예시]`

<img src="https://user-images.githubusercontent.com/67519366/96106287-01deae00-0f16-11eb-9601-513a89e75384.png">

사진출처 : <a href="https://12bme.tistory.com/297">https://12bme.tistory.com/297</a>

## HTTP 통신
---
`HTTP`통신은 <a href="https://kor-shin.github.io/network/http-request-constructure/" target="_blank">이전 포스팅</a>에서도 소개했지만, Client와 Server가 연결되어 있지 않습니다.<br>
또한 단방향 통신이기 때문에 Server는 Client에게 Request를 할 수 없습니다.<br>
HTTP통신에서 Server는 Client의 요청이 있으면 Client의 Request에 대한 응답만을 Response하고 연결을 끊습니다.<br>
따라서 Client가 Server에게 Request를 할때마다 지연시간이 발생합니다.<br>
이러한 HTTP통신은 필요한 경우에만 Server에 접근하는 컨텐츠 위주의 데이터를 사용할 때 많이 사용됩니다.<br>
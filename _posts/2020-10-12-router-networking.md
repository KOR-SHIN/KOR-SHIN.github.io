---
title : 서로 다른 네트워크의 통신
layout: posts
categories :
 - NETWORK
tag :
 - NETWORK
comments: true
---

## __Router__
---

`Router`는 패킷을 다음 경로로 전향시키는 장치입니다.

이 때, 최적의 경로는 일반적으로 가장 빠르게 통신이 가능한 경로입니다.

돌아가는 경로라도 고속의 전송로를 통하여 전달이 되는 경로가 될 수 있습니다.

간단히 말하면, 연결된 네트워크 간의 중계역할을 담당하는 것이 Router입니다.

가장 친숙한 예로 공유기를 생각할 수 있습니다.

## __공용주소와 사설주소__
---
<img src="https://user-images.githubusercontent.com/67519366/95746913-82ad6800-0cd2-11eb-8bb2-67f7c2332696.png">

위의 사진을보면 Public IP address와 private IP address가 다른것을 알 수 있습니다.

만약 외부에서 192.168.0.4라는 호스트에 접근하고 싶다면, public IP address로 접속요청을 하게됩니다.

그리고 공유기에서는 접속요청에 맞는 private IP address로 연결해주게 됩니다.

이렇게 라우터를 통해서 외부 인터넷과 통신이 가능한것은 NAT(Network Address Translation)이라는 기술때문에 가능한 것입니다.

## NAT(Network Address Translation)

`NAT`는 간단히 말해서 공용IP를 사설IP로 변경하거나 반대의 일을 수행합니다.

192.168.0.4의 사설IP에서 위키피디아로 접속하는 과정을 예로 들어보겠습니다.

<img src="https://user-images.githubusercontent.com/67519366/95747177-f3ed1b00-0cd2-11eb-93c6-ebc6f83f0997.png">

1. 192.168.0.4에서 위키피디아의 아이피로 접속을 요청한다.
2. 라우터에서 192.168.0.4를 저장해놓고 사설IP를 공용IP로 접속하여 위키피디아에게 접속 요청을 한다.
3. 위키피디아 서버에서 접속에 대한 응답을 보낸다.
4. 응답을 받은 라우터는 위키피디아에 접속을 요청한 아이피를 찾는다 (2번에서 저장해놓음)
5. 요청을 했던 사설 IP에게 위키피디아의 공용아이피로 접속하도록 한다.

위 예시에서 알 수 있듯이 NAT는 사설IP를 공용IP로 변경하고, 공용IP를 사설IP로 변경함으로써 서로다른 네트워크간의 접속을 할 수 있도록 도움을 주는 역할합니다.

## __Port__
---
위에서 NAT를 통해 서로다른 네트워크간의 접속이 어떻게 이루어지는지 알아보았습니다.

하지만 이것만으로는 충분하지 않습니다.

만약 사설IP의 요청이 없이 외부에서 192.168.0.4로 접속을 원한다면 어떤일이 벌어질까요?

외부에서는 사설IP를 모르기때문에 공용IP인 59.6.66.238로 접속을 요청할 것입니다.

하지만 같은 네트워크에 위치하고 있는 사설IP들은 모두 같은 공용IP를 가지고 있습니다.

그렇기때문에 외부의 요청을 받은 라우터는 어떤 사설IP로 접속을 시켜야 할지 모르게됩니다.

이 때 필요한것이 Port번호입니다.

## __Well-Known Port__
---
`well-known port`는 의미 그대로 잘 알려진 포트를 의미합니다.

well-known port는 `0번부터 1023번`까지의 포트번호이고, 이 포트번호들은 모두 예약된 포트이기 때문에 지정하여 사용할 수 없습니다.

대표적으로 `80번(Http)`, `22번(SSH)`가 있습니다.

만약 우리가 컴퓨터에 웹 서버를 구축한다면 기본적으로 80번 포트에 연결됩니다.

80번 포트와 연결됐다는 것을 보통 `Listen`한다고 표현합니다.

만약 한 컴퓨터에 웹 서버를 여러개 구축한다면, 포트번호를 지정해서 사용해야 합니다.

보통 8000번, 8080번 포트를 지정해서 사용합니다.

(다른 포트번호를 사용해도 전혀 상관없습니다.)

## __URL__
---

마지막으로 Port가 필요한 이유를 설명하기 전에 URL의 Format을 살펴보겠습니다.

> scheme:[//[user:password@]host[:port]][/]path[?query][#fragment]

우선 다른부분은 신경쓰지말고 host[:port]부분만 살펴보겠습니다.

[ ]기호안에 있는것은 생략가능하다는 의미입니다.

만약 우리가 <a href="http://kor-shin.github.io">http://kor-shin.github.io</a>로 host를 입력하면 http라는 통신규약을 사용하기 때문에 실제로는 http://kor-shin.github.io:80으로 입력되고 host에 해당하는 주소의 80번 포트와 연결되어 있는 서버에 접속하게 되는것입니다.

## __Port Forwarding__
---

<img src="https://user-images.githubusercontent.com/67519366/95747406-61994700-0cd3-11eb-8fd2-1426f5a520bf.png">
위의 예시를 보면 192.168.0.4와 192.168.0.3은 각각 웹 서버를 가지고 있습니다.

그리고 공유기에서는 59.6.66.238:8080으로 요청이 들어오면 192.168.0.3의 80번 포트로 연결하고 59.6.66.238:8081으로 요청이 들어오면 192.168.0.4의 80번 포트로 연결하게 설정해두었습니다.

이러한 설정을 공유기의 관리자에 접속하여 설정할 수 있는데 이렇게 접속을 요청하는 포트에 따라 연결해주는 사설IP를 다르게 하는것을 `Port Forwarding`이라고 합니다.

## __Dynamic IP Address vs Static IP Address__
---
마지막으로 동적IP와 정적IP에 대해서 알아보겠습니다.

지금까지의 내용은 서로다른 네트워크가 상호작용을 하기위해 어떠한 과정을 거치는지에 대해 알아보았습니다.

여기서 반드시 필요한 부분을 IP주소입니다.

하지만 IP주소는 불변이 아니기 때문에 변경되는 일이 일어날 수 있습니다.

<img src="https://user-images.githubusercontent.com/67519366/95747485-82fa3300-0cd3-11eb-8967-bd10b93eae79.png">

우리가 인터넷을 사용하기 위해서는 통신회선을 구매해야합니다.

우리가 구매한 통신회선을 구매하면 위의 사진처럼 ISP를 통해 IP를 할당받을 수 있습니다.

하지만 통신회사에서 제공할 수 있는 IP주소의 개수는 정해져있고, 가입자는 늘어납니다.

따라서 ISP는 DHCP(Dynamic host configuration Protocol)이라는 동적 IP할당방법을 사용하는데, 이것은 대여시간(Lease Time)이 지나면 해당 IP에게 인터넷을 사용하고 있는지 질의하고, 사용하고 있지않다면 다시 IP주소를 회수합니다.

그렇게 회수한 IP주소는 다른 가입자에게 할당됩니다.

따라서 우리가 사정이생겨서 대여시간이 지날동안 인터넷을 사용하지 않았다가 다시 인터넷에 연결되면 IP주소가 변경되는 일이 발생됩니다.
<br>

<img src="https://user-images.githubusercontent.com/67519366/95747532-94433f80-0cd3-11eb-87f0-b14857d229e7.png">

위 사진처럼 우리가 사용하던 IP주소는 다른 가입자에게 할당되고, 우리는 새로운 IP주소를 할당받는 것입니다.

그렇다면 59.6.66.238로 접속을 요청하던 클라이언트는 전혀다른 네트워크에 접속을 하게되는 일이 발생됩니다.

이러한 것을 방지하기 위한것이 정적IP(Static IP)입니다.

이 포스팅에서는 Static IP Address에 대해서는 다루지 않지만 꼭 찾아보기를 권장합니다.
<br><br>
포스팅내용, 이미지 출처 : <a href="https://opentutorials.org/course/3265" target="_blank">생활코딩 Home Server</a>
<br>
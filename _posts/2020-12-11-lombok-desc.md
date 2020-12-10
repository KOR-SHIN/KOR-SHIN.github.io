---
title : Lombok 설치 및 적용
layout: posts
categories :
 - API
tag :
 - API
---

## Lombok

---

Lombok은 Model Object의 boilerPlate Code를 줄이기 위해 사용되는 Annotation기반 라이브러리입니다.

Model Object(VO, DTO 등)을 만들때 보통 자바빈 규약에 의거하여 Object를 생성하게 되는데 여기서 boilerPlate Code가 많이 발생합니다.

Lombok을 사용하면 Annotation으로 이러한 문제점을 해결할 수 있습니다.

## Lombok 동작원리

---

Lombok은 `Annotation Processing`과 `Instrumentation`을 사용합니다.

Instrumentation은 이클립스는 별도의 컴파일러가 있기 때문에 이클립스 종속적인 bytecode 처리에 사용되고, Annotation Processor에서는 Annotation별로 코드를 생성하는데 사용됩니다.

간단히 요약하면, Lombok은 AnnotationProcessor를 이용하여 컴파일 시점에 코드를 생성해주는 기능을 하는것입니다.

## Lombok의 이점

---

Lombok을 사용하여 얻을 수 있는 이점은 위에서 언급한 `boilerPlate Code`를 줄일 수 있다는 것입니다.

또한 간단한 사용방법으로 Object Model을 생성할 수 있기때문에 생산성도 향상되며 개발자의 수고를 덜어주는 이점이 있습니다.

## Lombok의 단점

---

Lombok은 아주 강력한 API이기 때문에 그만큼 조심해서 사용해야 합니다.

Lombok에는 `@ToString, @EqualsAndHashCode, @Getter, @Setter, @RequiredArgsConstructor`를 한번에 생성해주는 `@Data`라는 Annotation이 있습니다.

Annotation을 여러개 선언하지않아도 한번에 모든것을 만들어주니 매우 편해보입니다.

하지만 이런 편리함으로 인해 문제가 발생될 수 있습니다.

예를들어 객체의 상태를 확인할 수 있는 @ToString을 생성하는데 VO안에 회원의 계좌정보, 비밀번호와 같은 민감정보를 포함하고 있는경우라면 ToString의 대상에서 제외하는것이 정상적입니다.

하지만 @Data하나만 선언하고 ToString을 Overriding하지 않는다면 문제가 발생합니다.

위처럼 단편적인 예를들었지만 Lombok의 편리함만을 이용하려고 하면 많은 문제점이 발생할 수 있으니 신중하게 사용해야 합니다.

## Lombok 적용 주의사항

---

현재 Maven Project를 사용하고 있기때문에 Maven을 기준으로 설명하겠습니다.

Maven에서 Lombok은 의존성주입만으로 사용할 수 없습니다.

projectLombok에서 jar파일을 다운로드하여 사용하고 있는 이클립스에 plugin을 설치해야 합니다.

## Lombok 설치 및 적용
---
![main](https://user-images.githubusercontent.com/67519366/101799331-62bde780-3b4f-11eb-803a-65469067226c.png)


Google에서 projectLombok을 검색하여 사이트로 접속합니다.

![down](https://user-images.githubusercontent.com/67519366/101799384-71a49a00-3b4f-11eb-93ab-5c5023f35cd7.png)

메인화면의 상단 네비게이션 바에서 Download를 클릭합니다.

![down2](https://user-images.githubusercontent.com/67519366/101799404-76694e00-3b4f-11eb-8e08-40ed2df52f7a.png)

화면에 나와있는 버전을 다운로드 합니다.

![lom](https://user-images.githubusercontent.com/67519366/101799458-841ed380-3b4f-11eb-9bca-a0f48896a626.png)

다운로드가 완료되면 파일이 저장되는 경로에 lombok.jar가 생성됩니다.

이 jar파일을 설치하기 위해 window console창을 열어 줍니다.

본인의 lombok.jar가 위치하고 있는 경로로 이동하여 아래에 명령을 입력합니다.

java -jar lombok.jar `(java -jar [path])`

![gocu](https://user-images.githubusercontent.com/67519366/101799455-83863d00-3b4f-11eb-8b53-d48b04b0c12c.png)

위의 명령어를 정상적으로 입력하였다면 위와같은 화면이 나올것입니다.

IDE의 위치를 자동으로 검색해주지만 혹시나 검색이 안되면 아래와 같은 에러가 발생합니다.

![error](https://user-images.githubusercontent.com/67519366/101799453-83863d00-3b4f-11eb-8475-db169a9f7599.png)

이러한 에러가 발생하면 확인버튼을 눌러 창을닫아주고

하단에 있는 Specify location..버튼을 클릭합니다.

![ecl](https://user-images.githubusercontent.com/67519366/101799451-82eda680-3b4f-11eb-866f-78e7f00e7bb5.png)

버튼을 클릭한 후 자신이 lombok을 설치하고 싶은 eclipse.exe파일이 위치하는 경로를 찾아가서 선택한 후 창을 닫고 install / update버튼을 클릭합니다.

![close](https://user-images.githubusercontent.com/67519366/101799448-82551000-3b4f-11eb-97f7-ea7429153beb.png)

성공적으로 설치되었다면 상단에 Install successful이라는 메세지가 나올것입니다.

그리고 선택했던 eclipse.exe파일이 위치하는 경로로 들어가서 lombok.jar가  생성되었다면 성공입니다.

![dep](https://user-images.githubusercontent.com/67519366/101799449-82eda680-3b4f-11eb-8f0c-a4ec6886fdc3.png)

이제 eclipse를 실행하고 maven project의 pom.xml로 들어가서 의존성을 주입합니다.

위의 태그를 사용해도 되고 dependencies에서 Add해도됩니다.

모두 완료되었다면 maven project를 업데이트하고 Model Object를 생성하여 테스트해보면 됩니다.

![vo](https://user-images.githubusercontent.com/67519366/101799437-8123e300-3b4f-11eb-8fff-dcc201324436.png)

테스트용으로 VO클래스를 생성하고 위와같이 Annotation을 적용해보았습니다.

Annotation을 사용하는것은 의존성 주입만 해도 가능하기 때문에 실제로 코드가 만들어지는지 확인해야 합니다.

![builder](https://user-images.githubusercontent.com/67519366/101799446-82551000-3b4f-11eb-9a1f-8f0de834f545.png)

실제로 코드가 만들어지는지 확인하는 작업은 project Explorer에서 lombok을 사용한 클래스를 확장해보면 알 수 있습니다.

만약 위와같이 보이지않거나 Annotation에 노란색줄이 그어져 있다면 설치가 제대로 안된것입니다.

## P.S
---
Lombok에 여러 글들을 읽으면서 느꼈지만 Lombok은 강력하고 매력적인 API입니다.

하지만 대충 사용하면 많은 사이드 이펙트가 발생할 수 있다는것을 알았습니다.

Lombok을 더욱 잘 사용하기 위해 더 많이 공부해야 할것같습니다
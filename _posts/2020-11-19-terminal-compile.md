---
title: 터미널에서 자바 컴파일과 실행
layout: posts
categories:
 - JAVA
tag:
 - JAVA
---

## __Terminal을 사용하는 이유__
---
`IDE`툴을 사용하면 소스코드를 알아서 컴파일해주고 실행해주기 때문에 어떻게 이러한 과정이 이루어지는지 생각하지 않게됩니다.<br>
특히 경로에 대한 개념이 무뎌지는것 같습니다.<br>
그래서 이번에는 `Eclipse`를 사용하지 않고 `Terminal`을 이용하여 직접 자바소스파일을 컴파일하고 실행시켜보면서
`IDE`툴이 우리에게 어떤 편리함을 제공하는지, 소스코드파일이 실행되는 과정은 어떻게 이루어져있는지를 살펴보려고 합니다.

## __java파일 생성하기__
---
`IDE`툴을 사용하지 않고, 메모장으로 간단한 소스코드를 작성한 후 확장자를 `.java`로 변경합니다.

<img src="https://user-images.githubusercontent.com/67519366/99544969-3d2e3a00-29f8-11eb-8f1c-265e2f077b49.png">


`classpathTest.java`파일 안에는 2개의 `class`가 정의되어 있습니다.<br>
`.java`을 컴파일하기 위해 `crtl + R`을 누르고 `cmd`를 입력하여 터미널을 열어줍니다.<br>
컴파일을 하기전에 해당 자바파일이 있는 디렉토리에 무엇이 있는지 살펴보겠습니다.<br>

## __디렉토리 살펴보기__
---
위에 쓰여진 방법을 통해 터미널을 열고 `java`파일이 위치하고 있는 경로를 입력합니다.

<img src="https://user-images.githubusercontent.com/67519366/99545386-aca42980-29f8-11eb-8465-9aace13830bb.png">

앞에 `cd`는 `change directory`로써 뒤에 쓰여진 경로로 이동한다는 의미이고, 뒤에 `c:/classpathExam`은 `c drive` 하위에 위치한 `classpathExam`디렉토리를 의미합니다.<br>
따라서 `cd`는 동일하지만 뒤에 경로는 본인의 자바파일이 위치한 경로를 적어주어야 합니다.<br><br>

<img src="https://user-images.githubusercontent.com/67519366/99545716-07d61c00-29f9-11eb-8d7f-075a766e2376.png">

자바파일이 위치한 경로로 이동하여 `dir`이라는 명령어를 입력하면 해당 경로안에 있는 `File`과 `Directory`가 보입니다.<br>
현재 위에서 만들어놓은 `classpathTest.java`가 보입니다.<br>
이제 만들어놓은 자바파일을 컴파일 해보겠습니다.

## __javac & compile__
---
`Javac`는 자바 개발 키트(JDK)에 포함된 `Java Compiler`입니다.<br>
자바 컴파일러는 `.java` 파일을 `.class`로 변경시키는데, 이것은 소스코드를 실행파일로 변환한 것입니다.<br>
`.class`파일은 `binary code`로 이루어져 있습니다.<br>
이제 `Javac`를 이용하여 터미널에서 자바파일을 컴파일 해보겠습니다.<br><br>

<img src="https://user-images.githubusercontent.com/67519366/99546916-48826500-29fa-11eb-9c1e-cbe058c1de1a.png">

위의 명령어는 `java compiler`로 `classpathTest.java`파일을 `complie`한다는 의미입니다.<br>
해당 자바파일에 오류가 없다면 정상적으로 컴파일되고 아무런 메세지가 출력되지 않을것입니다.<br>
그럼 컴파일된 상태에서 `dir`명령어를 통해 디렉토리 구조를 살펴보겠습니다.<br><br>

<img src="https://user-images.githubusercontent.com/67519366/99547153-8da69700-29fa-11eb-8342-5564dab6794a.png">

컴파일하기 전과는 다르게 `ClasspathTest.class`파일과 `Display.class`파일이 생성된것을 알 수 있습니다.<br>
우리는 `classpathTest.java`파일 하나만 컴파일했는데 실행결과로 2개의 파일이 생성되었습니다.<br>
그 이유는 우리가 컴파일한 자바소스코드 안에는 2개의 클래스가 정의되어 있었기 때문입니다.<br>
여기서 기억해야하는것은 하나의 자바소스파일을 컴파일했을때 생성되는 확장자가 .class인 파일은 한 개가 아닐수 있다는 것입니다.<br>

## __.class파일 실행__
---
위에서 `javac`를 이용하여 `.java`파일을 `.class`파일로 컴파일하는 과정까지 살펴보았습니다.<br>
이제 컴파일이 완료된 클래스 파일을 실행시켜보겠습니다.<br>

<img src="https://user-images.githubusercontent.com/67519366/99548280-d14dd080-29fb-11eb-97f5-910dc9f4b39a.png" height=80px>

`.class`파일을 실행할때는 뒤에 확장자를 제외한 파일명만을 써야합니다.<br>
현재는 에러가 발생하여 실행이 되지않았고, 이유는 `main method`가 없기때문입니다.<br>
실행이 제대로 될 수 있도록 메서드를 작성하고 다시 컴파일한 후 실행해보겠습니다.<br>

<img src="https://user-images.githubusercontent.com/67519366/99548854-6ea90480-29fc-11eb-9a31-20543f67baf3.png">

`classpathTest.java`파일의 내용은 위와 같습니다.<br><br>

<img src="https://user-images.githubusercontent.com/67519366/99549027-97c99500-29fc-11eb-92b7-59ca712117a3.png">

위의 과정과 똑같이 `javac`를 통해 컴파일하고, `java`를 통해 `ClasspathTest.class`파일을 실행한 결과입니다.<br>
결과로 `Hello Command`가 출력되는것을 볼 수 있습니다.<br>

## __classpath__
---
`classPath`는 말 그대로 클래스 파일의 경로를 의미합니다.<br>
컴파일하고 실행까지 잘 했지만 잘 생각해보면 `Eclipse`같은 `IDE`를 사용할 때 하나의 프로젝트 폴더안에 여러개의 폴더, 패키지를 구성하여 소스파일을 나누어 관리하는 경우가 많습니다.<br>
이번에는 `Display.class`파일과 `ClasspathTest.class`파일의 경로를 다르게 하여 실행해보려고 합니다.<br>
현재 디렉토리에서 `lib`라는 파일을 만들어 `Display.class`파일을 이동시키겠습니다.<br>
따라서 제 데스크탑에서 `Display.class`파일의 경로는 `c:/classpathExam/lib`입니다.<br>
파일을 옮겨놓은 상태로 실행해보겠습니다.<br>

<img src="https://user-images.githubusercontent.com/67519366/99549725-4f5ea700-29fd-11eb-94cf-82aeacdbfba5.png">

예상가능하듯이 에러가 발생합니다.<br>
이번에 발생한 에러메세지는 `NoClassDefFoundError: Display`입니다.<br>
위의 소스코드 내용을 보면 `ClasspathTest`클래스는 `Display`클래스를 인스턴스화 시킨 `dis`라는 참조변수를 이용하여 `display()`라는 메서드를 호출하고 있습니다.<br>
따라서 `ClasspathTest`클래스는 `Display`클래스를 참조하고 있는데 현재 디렉토리에서 `Display`클래스를 찾을수 없기때문에 에러가 발생한 것입니다<br>
이럴때 사용할 수 있는것이 `classpath`입니다.
`classpath`라는것은 클래스를 찾을때 시작점이 되는 위치를 의미합니다.
예를들어 Terminal에서 `set classpath="d:/webapps/classes`라고 하면 `javac`를 이용하여 컴파일을 하거나 `java`를 이용하여 `.class`파일을 실행할 때 `d:/webapps/classes`경로부터 대상 클래스 파일을 찾게되는 것입니다.

## __classpath 설정__
---
우선 터미널에서 `classpath`를 설정해주는 방법을 사용해보겠습니다.<br>

<img src="https://user-images.githubusercontent.com/67519366/99550444-1410a800-29fe-11eb-847e-c0eacb9e68d7.png">

기존의 실행명령어에서 `java`뒤에 `-classpath ".;lib"`를 추가하면됩니다.<br>
`-classpath`는 말 그대로 `classpath`를 지정하겠다는 것이고, 뒤에 큰 따옴표 안에 있는 내용에서 `'.'`은 현재 디렉토리를 의미하고, `';'`는 경로 구분자를 의미하며, `lib`는 디렉토리를 의미합니다.<br>
따라서 `현재 디렉토리에서 찾아보고 없다면 현재 디렉토리 안에 있는 lib라는 디렉토리에서 파일을 찾는다.`라고 명령해준것이라고 생각하면 됩니다.<br><br>
위의 방법을 사용하면 편리하지만 클래스파일이 여러곳에 위치한다면 비효율적인 방법이 될 수 있습니다.<br>
따라서 이번에는 환경변수로 설정하여 `classpath`를 사용하는 방법을 사용해보겠습니다.<br>

## __환경변수를 사용한 classpath__
---

<img src="https://user-images.githubusercontent.com/67519366/99551344-1293af80-29ff-11eb-9e5b-488802ca1d5a.png">

window검색창에서 sysdm.cpl을 입력하여 들어갑니다<br><br>

<img src="https://user-images.githubusercontent.com/67519366/99551435-322ad800-29ff-11eb-9e70-5055357ddf0f.png">

시스템 속성창이 나오면 상단 탭에서 `고급`으로 들어가서 `환경 변수`를 클릭합니다.<br><br>

<img src="https://user-images.githubusercontent.com/67519366/99551561-571f4b00-29ff-11eb-9096-7cde06998427.png">

상단에 `사용자 변수`와 하단에 `시스템 변수`가 있는데 잠깐 사용하고 지울것이기 때문에 `사용자 변수`에서 `새로 만들기`를 클릭하고 위와같이 입력하고 `확인`을 누릅니다.<br>
여기서 사용자 변수는 현재 계정만 사용가능한 변수이고 시스템 변수는 모든 계정에서 사용가능한 변수입니다.<br>

그럼 이제 다시 터미널을 열어서 클래스 파일을 실행해보겠습니다.<br>

<img src="https://user-images.githubusercontent.com/67519366/99551928-c6953a80-29ff-11eb-8bb6-6e404163d5dc.png">

`Display.class`파일은 여전히 `c:/classpathExam/lib`에 위치하고 있습니다.<br>
하지만 사용자 환경변수에 `CLASSPATH`를 설정해줌으로써 명령어에 `-classpath`를 생략해도 정상적으로 실행되는 것을 볼 수 있습니다.<br>

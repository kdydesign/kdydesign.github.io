---
title: "Mocha Tutorial - Step 08. IDE Edit Plug-in (IntelliJ)"
date: 2017-06-19 16:34:21
tags: 
- mocha
- javascript
- 단위 테스트
- intelliJ
- IDE
categories :
- javascript
- Mocha
keywords:
- javascript
- mocha
- chai
- unit test
- ide
- intellij
- jetbrain
- webstorm
- mocha intellij
- mocha plugin
disqusIdentifier: step08mochaide
clearReading: true
thumbnailImagePosition: left
autoThumbnailImage: yes
metaAlignment: center
coverMeta: out
coverSize: partial
comments: true
meta: true
actions: true
---

<!-- more -->
개발자들은 자기가 사용하는 IDE가 있을 것이다. IDE를 사용하는 이유는 더 편리하기 때문이다. 당연하다. bash, nodepad 보다는 훨씬 편하니까. 나 역시 `IntelliJ`를 사용하고 있다. 이 `IntelliJ`에서는 Mocha를 좀 더 다루기 쉽게 Plug-in을 지원하고 있다. `IntelliJ`뿐만 아니라 `Webstorm` 등의 `JETBRAIN` 제품군에서 지원하고있다.
이번 Tutorial은 `IntelliJ`에서 Mocha를 손쉽게 사용하는 방법을 배워보도록 하겠다. `JETBRAINS` 제품군을 사용하지 않는다면 해당 Tutorial은 건너 뛰도록하자.
<!-- more -->

<!-- excerpt -->
<!-- excerpt -->

![cover](cover.png)

개발자들은 자기가 사용하는 IDE가 있을 것이다. IDE를 사용하는 이유는 더 편리하기 때문이다. 당연하다. bash, nodepad 보다는 훨씬 편하니까. 나 역시 `IntelliJ`를 사용하고 있다. 이 `IntelliJ`에서는 Mocha를 좀 더 다루기 쉽게 Plug-in을 지원하고 있다. `IntelliJ`뿐만 아니라 `Webstorm` 등의 `JETBRAIN` 제품군에서 지원하고있다.
이번 Tutorial은 `IntelliJ`에서 Mocha를 손쉽게 사용하는 방법을 배워보도록 하겠다. `JETBRAINS` 제품군을 사용하지 않는다면 해당 Tutorial은 건너 뛰도록하자.

- - -

## Node.js 및 Plug-in 설치

Mocha를 사용해보기에 앞서 먼저 `Node.js` 와 `IntelliJ NodeJs Plug-in`을 설치하자. 먼저 [여기서](https://nodejs.org/ko/) Node.js를 설치한다. 기본적으로 `IntelliJ`를 설치할 때 별도의 설치 여부가 나오지만 설치가 되어있지 않다면 설치하도록 하자.
`ctrl + shift + a` 또는 `IntelliJ`설정 창에서 `plugins`를 검색하여 해당 창을 실행 후 `nodejs`를 검색하였을 때 설치가 되어있지 않으면 `Browser Repositories`에서 `nodejs`를 설치하도록 하자. 

## Mocha Configurations

`Node.js`가 설치되었다면 `Mocha` runner 또는 compiler를 추가하자. `run/debug configurations` 창에서 `+`버튼을 눌러 `Mocha`를 선택한다. 이후 출력되는 설정 창에서 수정해야 할 부분은 아래를 참고하자.

|Option|Description|
|---|---|
|Node interpreter|node.exe 경로|
|Working directory|mocha 프로젝트 경로|
|Mocha package|mocha 패키지 경로(ex. npm\node_modules\mocha|
|User Interface|사용자 인터페이스 설정|
|Test directory|테스트 파일 경로(ex. test.js)|

![image01](image01.png)

설정이 완료되면 실행해 보도록 하자. 실행을 해보면 테스트 스위트와 테스트 케이스별로 성공, 실패 여부를 확인할 수 있다. 여기서 **`IntelliJ`에서 실행하면 좋은 점 두 가지**가 있다.

{% alert info %}
1. Break Point를 통한 Debugging
2. HTML 출력
{% endalert %}

![image02](image02.png)

이전 Tutorial [Step 06: 브라우저에서의 Mocha 지원](https://kdydesign.github.io/2017/06/16/Mocha-step-06/)에서 Mocha를 브라우저에서 구동하는 방법을 배웠었는데 `IntelliJ`를 사용하면 별도의 HTML파일을 출력할 수가 있다. 그리고 불편하기만하던 Mocha의 `--debug` 옵션을 `IntelliJ`에서는 Break Point를 통해서 쉽게 Debugging이 가능하다.
  
- - -

IDE Tool을 사용하면 어떤 개발 프레임워크이든 쉽게 이용할 수가 있다. 그만큼 개발 속도 역시 빠르다 할 수 있다. 이번 Tutorial을 통해 우리는 이제 Mocha를 사용하여 단위 테스트를 할 수 있는 최적화된 환경을 만들 수 있다.
이제 마지막으로 `Mocha를 활용하여 실제 TDD`를 어떻게 하는지 알아볼 차례이다.


[Step 09: Mocha로 실제 TDD 해보기](https://kdydesign.github.io/2017/06/21/Mocha-step-09/)
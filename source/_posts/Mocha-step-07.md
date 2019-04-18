---
title: "Mocha Tutorial - Step 07. Mocha Options"
date: 2017-06-19 12:39:36
tags: 
- mocha
- javascript
- 단위 테스트
categories :
- javascript
- Mocha
keywords:
- javascript
- mocha
- chai
- unit test
- mocha test
- mocha option
- option
- javascript mocha
- mocha tutorial
disqusIdentifier: step07mochaoptions
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
이제 Mocha의 기본적인 사용법을 모두 터득하였다. 지금까지 배운 것만으로도 어느 정도의 Test가 가능하다. 하지만 우리가 항상 개발할 떄에 Framework를 찾는 이유는 무엇인가 개발을 할 때 손쉽게 개발하기 위해서이다. Mocha 역시 옵션을 조정하여 좀 더 편리하게 사용할 수 있는데 이번 Tutorial에서는 이 옵션에 대해서 알아보겠다.
<!-- more -->

<!-- excerpt -->
<!-- excerpt -->

![cover](cover.png)

이제 Mocha의 기본적인 사용법을 모두 터득하였다. 지금까지 배운 것만으로도 어느 정도의 Test가 가능하다. 하지만 우리가 항상 개발할 떄에 Framework를 찾는 이유는 무엇인가 개발을 할 때 손쉽게 개발하기 위해서이다. Mocha 역시 옵션을 조정하여 좀 더 편리하게 사용할 수 있는데 이번 Tutorial에서는 이 옵션에 대해서 알아보겠다.

- - -

## 기본 옵션

Mocha의 기본 옵션 먼저 확인해 보도록 하자.

```bash
$ mocha -h
```

꽤 많은 옵션이 출력된다. 하나하나 설명하기는 양이 많기에 일부 가장 자주 쓰이는 것으로 알아보자.

|Option|Description|
|---|---|
|-reporters|테스트 결과를 출력할 수 있는 레포트 형식 목록을 출력|
|-R, --reporter <name>|테스트 결과를 출력할 레포트 형식을 지정|
|-d, --debug|Node늬 Debug 모드 활성화|
|-g, --grep <pettern>|정규식 패턴에 일치하는 특정 테스트 실행|
|-f, --fgrep <string>|특정 문자열이 포함된 테스트 실행|
|-r, --require <name>|require 할 모듈 명을 미리 지정하여 미리 특정 모듈을 포함|
|-t, --timeout <ms>|timeout을 지정(default : 2000ms)|
|-u, --ui <name>|사용자 인터페이스 지정(tdd, bdd, qunit, exports)|
|-w, --watch|테스트 파일 수정 시 자동 반영|

이 외에 다른 옵션은 `$ mocha -h`를 통해 확인할 수 있다.

## mocha.opts

위처럼 기본 옵션을 `Command`를 통해 지정할 수 있겠지만 다른 방법으로 더욱 편리하게 사용할 수 있다. 그 방법으로는 `mocha.opts`파일에 필요한 옵션들을 지정해 놓는 것이다. 대부분의 `test` 파일들은 `test` 또는 `tests` 폴더에 모아두는 것이 관례이다. 이 `test` 또는 `tests` 폴더 안에 미리 옵션들을 정의 해둔 `mocha.opts`를 넣어두면 테스트 시에 자동으로 파일에 정의된 옵션들을 사용하여 테스트하게 된다.

먼저 프로젝트 안에 `tests`라는 폴더를 만들고 그 안에 `mocha.opts`파일을 만들자.

```bash
$ mkdir tests
$ cd tests
$ touch mocha.opts
```

이제 `mocha.opts`에 원하는 옵션을 지정해주면 된다.

```
--require should
--reporter dot
--ui bdd
```

위 옵션은 `should` 라이브러리를 포함하고 `reporter`는 `dot`로 사용하며, `사용자 인터페이스`는 `bdd`를 사용한다는 옵션이다.

## package.json에 Options 지정

`mocha.opts`로 사용하면 편리하지만 이 밖에도 `package.json`에도 옵션을 명시할 수 있다. `package.json`에서 `script`항목에 위와 동일하게 옵션을 추가하여 수정한다.

```json
/*...*/

"scripts" : {
    "test": "mocha test --reporter spec --ui bdd",
  },
  
/*...*/
```
  
- - -

Mocha는 옵션뿐만 아니라 IDE Tools에서도 편리하게 사용할 수 있다. 다음 편에서는 `JETBRAINS`제품 군(`IntelliJ`,`WebStorm` 등)에서 Mocha를 쉽게 사용하는 방법을 알아보겠다.


[Step 08: IDE Edit Plug-in (IntelliJ)](https://kdydesign.github.io/2017/06/19/Mocha-step-08/)
---
title: JavaScript 단위 테스트 프레임워크 - Mocha
date: 2017-06-08 00:56:13
tags: 
- mocha
- javascript
categories :
- javascript
- Mocha
keywords:
- javascript
- mocha
- 단위테스트
- unit test
- javascript mocha
- tutorial
- mocha tutorial
disqusIdentifier: step00mocha
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
기술이 나날히 발전함에 따라 Web Front-End에도 테스트 방법론들을 적용하여 보다 효율적이고 효과적으로 프로젝트를 진행할 수 있다. JavaScript기반의 테스트 프레임워크는 무수히 많다. 그 중 대표적으로 `Mocha`와 `jasmine`을 말 할수 있다. 이 두 프레임워크 중 어떤 프레임워크가 더욱 뛰어난지 비교할 수 없다. 그저 어떤 프레임워크를 사용하느냐는 진행하고자하는 프로젝트와 주변 환경의 요소에 따라 다르다. 이번 포스팅에서는 `Mocha`를 먼저 말하고 싶다.
<!-- more -->

<!-- excerpt -->
<!-- excerpt -->

![cover](cover.png)

## Mocha
기술이 나날히 발전함에 따라 Web Front-End에도 테스트 방법론들을 적용하여 보다 효율적이고 효과적으로 프로젝트를 진행할 수 있다. JavaScript기반의 테스트 프레임워크는 무수히 많다. 그 중 대표적으로 `Mocha`와 `jasmine`을 말 할수 있다. 이 두 프레임워크 중 어떤 프레임워크가 더욱 뛰어난지 비교할 수 없다. 그저 어떤 프레임워크를 사용하느냐는 진행하고자하는 프로젝트와 주변 환경의 요소에 따라 다르다. 이번 포스팅에서는 `Mocha`를 먼저 말하고 싶다.

`Mocha`는 Node.js 기반의 Javascript 테스트 프레임워크이다. `Mocha` 공식 페이지에서는 `Mocha`를 세 단어로 설명하도 있다.

> 

{% alert info %}
***Simple(간단하고), Flexible(유연하며), Fun(재미있는)***
{% endalert %}

정말 그런지 확인해보자.

## Mocha 설치하기
**Mocha**를 설치하기 위해서는 먼저 Node.js와 npm이 설치되어 있어야 한다. Node.js와 npm 설치 방법과 개념은 npm과 node.js에 대해서는 [빠르게 배우는 Node.js와 NPM 설치부터 개념잡기](https://kdydesign.github.io/2017/07/15/nodejs-npm-tutorial/)포스트를 참고하자.
Node.js와 npm을 설치하였다면 적당한 프로젝트 폴더를 생성한다. 여기서는 `Mocha_test`라고 하겠다.

``` bash
$ C:\Mocha_test
```

생성된 경로에 npm 명령어를 통해 `package.json`을 생성한다.

```bash
$ npm init
```

이제 `package.json`이 생성되었으니 본격적으로 `mocha`를 설치해 보자. `mocha`를 설치 할 때에는 `-g` 옵션을 붙혀서 global하게 설치해도 무방하다.

```bash
$ npm install mocha --save-dev 또는 npm i -g mocha
```

`--save-dev` 옵션을 주었기에 `package.json`에 `devDependencies`에서 `mocha`가 추가된 것을 볼 수 있다.
`mocha`가 정상적으로 설치가 되어 있는지 확인하기 위해 다음과 같이 실행해 보자.

```
$ mocha --version 또는 mocha -V
```

`mocha`와 관련된 옵션은 `mocha -h`를 통해 확인 할 수 있다. 이제 `mocha` 설치까지 끝났으니 본격적으로 `mocha`를 사용할 때이다. 비교적 Learning Curve가 적어 Tutorial이 적지만 단계별로 진행해 보자.


[Step 01: Hello World!](https://kdydesign.github.io/2017/06/15/Mocha-step-01/)



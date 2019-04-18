---
title: "Mocha Tutorial - Step 03. Hooks"
date: 2017-06-16 00:03:49
tags: 
- mocha
- javascript
- hooks
- 단위 테스트
- BDD
- TDD
categories :
- javascript
- Mocha
keywords:
- javascript
- mocha
- chai
- TDD
- BDD
- mocha hooks
- unit test
- mocha test
- javascript mocha
- mocha tutorial
disqusIdentifier: step03mochhook
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
이번 Tutorial에서는 Mocha의 `Hooks`를 알아보겠다. **Mocha에서는 테스트들의 전제 조건과 후 조건을 미리 설정할 수 있는 `Hooks`를 지원**한다. Mocha에서는 기본적으로 `BDD` 스타일을 지원하지만 `TDD` 스타일도 역시 지원하기 때문에 이 두 스타일에 대한 `Hooks`도 정의할 수 있다.
<!-- more -->

<!-- excerpt -->
<!-- excerpt -->

![cover](cover.png)

이번 Tutorial에서는 Mocha의 `Hooks`를 알아보겠다. **Mocha에서는 테스트들의 전제 조건과 후 조건을 미리 설정할 수 있는 `Hooks`를 지원**한다. Mocha에서는 기본적으로 `BDD` 스타일을 지원하지만 `TDD` 스타일도 역시 지원하기 때문에 이 두 스타일에 대한 `Hooks`도 정의할 수 있다.

먼저 `Hooks`를 살펴보겠다.

- - -

## 기본 Hooks
Mocha의 기본 `BDD` 스타일의 `Hooks`는 다음과 같이 정의할 수 있다.

```javascript
describe('#Hooks', function(){
   before(function(){
        // runs before all tests in this block            
   });
   
   after(function(){
        // runs after all tests in this block
   });
   
   beforeEach(function() {
        // runs before each test in this block
   });
   
   afterEach(function() {
        // runs after each test in this block
   });
   
   it('test', function(){
        // test case 
   });
});
```

간단하다!!. 
주석을 보면 알겠지만 Mocha에서는 `before()`, `after()`, `beforeEach()`, `afterEach()` 4가지의 `Hooks`를 지원한다. 여기서 `before()`, `after()`는 테스트 스위트 단위(`describe`)로 실행된다. `before()`는 각 테스트 스위트가 실행되기 전에 실행하고 `after()`는 각 테스트 스위트가 종료되고 실행된다.
`beforeEach()`, `afterEach()`는 어떨까? 이 두개의 `Hooks`는 테스트 스위트가 아닌 테스트 케이스 단위(`it`)로 실행된다. `beforeEach()`는 각 테스트 케이스가 실행하기 전에 실행되고  `afterEach()` 반대로 테스트 케이스가 종료 후에 실행된다.
 
## Hooks 실행 순서

이 `Hooks`들은 적절하게 정의 된 순서대로 실행된다.
모든 `before()` Hooks가 한 번 실행한 후 모든 `beforeEach()` Hooks와 테스트 케이스(`it`)가 실행된다. 이후 모든 `afterEach()` Hooks를 실행하고 마지막으로 `after()` Hooks를 한 번 실행하게 된다.

아래 코드를 보자.

```javascript
describe('#Hooks', function () {
    before(function () {
        console.log('before');
    });

    after(function () {
        console.log('after');
    });

    beforeEach(function () {
        console.log('beforeEach');
    });

    afterEach(function () {
        console.log('afterEach');
    });

    it('test case #1', function () {
        console.log('test case #1');
    });

    it('test case #2', function () {
        console.log('test case #2');
    })
});
```

해당 코드를 실행하게 되면 초기에 `before()`이 실행이 되고 이후 `beforeEach()` 그리고 테스트 케이스(`it`)이 실행된다. 그리고 테스트 케이스(`it`)이 종료되면 `afterEach()`가 실행되고 또 다시 테스트 케이스(`it`)을 위해 반복적으로 `beforeEach()`와 `afterEach()`가 실행되며, 마지막으로 `after()`가 실행되는 것을 볼 수 있다.

![result01](result_thumbnail_01.png)

## Hooks 설명

어떤 `Hooks`는 특정 설명과 함께 호출 할 수 있으므로 테스트에서 오류를 쉽게 찾아 낼 수 있다. 또한 `Hooks`에 특정 명칭을 가진 함수가 주어지면 그 명칭을 사용하게 된다.

```javascript
describe('#Describing Hooks', function () {
    beforeEach(function() {
        // beforeEach hook
    });

    beforeEach(function namedFun() {
        // beforeEach:namedFun
    });

    beforeEach('some description', function() {
        // beforeEach:some description
    });
});
```

## Hooks로 보는 BDD와 TDD

[Step 01: Hello World!](https://kdydesign.github.io/2017/06/15/Mocha-step-01/)부터 강조했던 점은 Mocha는 `TDD`와 `BDD` 스타일을 각각 지원한다고 하였다. 그 차이가 무엇인지 `Hooks`를 통해 알아보겠다.

단순히 `TDD`와 `BDD`는 코딩의 스타일이 아닌 하나의 애자일 소프트웨어 개발 방법론에서 가장 널리 쓰이는 테스트 방법론이다. `TDD`는 테스트 주도 개발(`Test-Driven-Devenlopment`)이며, `BDD`는 `TDD`를 근간으로 파생된 행위 주도 개발(`Befavior-Driven-Development`)이다. 이런 복잡하고 학습 곡선이 긴 내용은 이 Tutorial에서는 넘어가도록 하겠다.

{% alert warning %}
오직 이 Tutorial에서는 다루는 내용은 Mocha에서의 TDD와 BDD스타일 입니다.
{% endalert %}

우리가 이 Tutorial에서 배운 것은 Mocha는 기본적으로 `BDD` 스타일을 우선순위로 지원한다고 하였다. 그리고 4가지의 `Hooks`인 `before()`, `after()`, `beforeEach()`, `afterEach()` 이다. `TDD`는 4가지의 `Hooks`의 명칭이 다릅니다. `suiteSetup()`, `suiteTeardown()`, `setup()`, `teardown()` 이렇게 된다. 또한 `BDD`에서의 `describe()`는 `suite()`로, `it()`은 `test()`로 표현한다.

`TDD` 스타일을 직접 코드로 살펴보자.

```javascript
suite('#Hooks', function(){
   suiteSetup(function(){
        // runs before all tests in this block            
   });
   
   suiteTeardown(function(){
        // runs after all tests in this block
   });
   
   setup(function() {
        // runs before each test in this block
   });
   
   teardown(function() {
        // runs after each test in this block
   });
   
   test('test', function(){
        // test case 
   });
});
```

우리가 처음 `Hooks`를 시작할 때 작성했던 코드와 비교하면 어떤 부분이 다른지 알 수 있다. 그저 관점의 차이라고 볼 수 있겠다. 여기서 중요한 건 코딩의 스타일도 있겠지만 `TDD` 스타일을 사용하기 위해서는 Mocha의 옵션을 지정을 해줘야 한다.

```
$ mocha test --ui tdd 또는 -u tdd
```

`--ui` 또는 `-u`의 옵션을 통해 우리가 Mocha의 어떤 스타일을 사용할 것인지 명시를 해줘야 한다.

[예제 코드](https://github.com/kdydesign/Mocha-Tutorial/tree/master/step03-Hooks)

- - - 

`Hooks`는 용이하게 사용할 수 있다. 예를 들어 테스트 케이스 필요한 `Book`이라는 객체를 생성한다고 하였을 때 우리는 `var book = new Book()`을 테스트 케이스마다 만들 것이다. 하지만 우리는 지금까지 배운 `Hooks`를 통해 한 번에 객체를 만들고 `destroy`까지 완벽하게 끝낼 수 있다.
이제 `Hooks`를 배웠으니 다음 Tutorial에서는 `비동기 처리`에 대한 방법을 배워보고 `Hooks`에도 `비동기 처리`를 적용하는 방법을 배워보겠다.


[Step 04: 비동기 처리](https://kdydesign.github.io/2017/06/16/Mocha-step-04/)
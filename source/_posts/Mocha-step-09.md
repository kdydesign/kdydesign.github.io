---
title: "Mocha Tutorial - Step 09. Mocha로 실제 TDD 해보기"
date: 2017-06-21 22:56:03
tags: 
- mocha
- javascript
- 단위 테스트
- TDD
categories :
- javascript
- Mocha
keywords:
- javascript
- mocha
- chai
- unit test
- TDD
- mocha tdd
- javascript mocha tdd
disqusIdentifier: step09mochatdd
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
지금까지의 Tutorial을 통해 Mocha에 대해서 어느 정도 인지하고 습득하였다. 아직도 Mocha에 대해 애매모호한 기분이 들거나 뭔가 아쉬움이 남는다면 다시 돌아가 [JavaScript 단위 테스트 프레임워크 - Mocha](https://kdydesign.github.io/2017/06/08/Mocha/)부터 살펴보도록 하자.
이제 지금까지 배운 내용을 토대로 실제로 Mocha를 가지고 TDD를 진행해 보자. 이 Tutorial을 추가한 이유는 두 가지로 분류하였다.
<!-- more -->

<!-- excerpt -->
<!-- excerpt -->

![cover](cover.png)

지금까지의 Tutorial을 통해 Mocha에 대해서 어느 정도 인지하고 습득하였다. 아직도 Mocha에 대해 애매모호한 기분이 들거나 뭔가 아쉬움이 남는다면 다시 돌아가 [JavaScript 단위 테스트 프레임워크 - Mocha](https://kdydesign.github.io/2017/06/08/Mocha/)부터 살펴보도록 하자.

이제 지금까지 배운 내용을 토대로 실제로 Mocha를 가지고 TDD를 진행해 보자. 이 Tutorial을 추가한 이유는 두 가지로 분류하였다.

> 1. TDD를 이해하기 위함이며,
> 2. Mocha를 실전에 사용해 보기 위함이다.

이 두 가지를 생각하며 Tutorial을 시작해보자.

- - -

## TDD(Test-Driven-Development) Cycle

TDD는 [Step 03: Hooks](https://kdydesign.github.io/2017/06/16/Mocha-step-03/)에서 살짝 설명한 바가 있다. TDD는 짧은 Cycle을 반복적으로 테스트하는 개발 프로세스로 테스트 코드를 먼저 작성하고 작성된 테스트 코드를 패스할 수 있도록 비즈니스 로직을 개발하는 방법이다. 자세한 TDD가 무엇인지는 구글링을 통해 알아보자. 

시작하기에 앞서 TDD의 프로세스를 생각해두자. 위에서 말했듯이 하나의 짧은 Cycle을 반복적으로 수행하는 것이다. 이 Cycle의 대략적인 순서는 이렇다.

{% alert info %}
1. 개발 **명세 작성**
2. 개발 명세에 따른 **테스트 코드 작성**
3. 테스트 실행
4. 테스트가 성공하도록 **최소한의 비스니스 로직 작성**
5. 테스트 실행
6. **테스트 케이스 추가**
7. 테스트 실행
8. 테스트 코드 및 테스트 케이스 **Refactoring**
9. 테스트 실행
{% endalert %}

위의 순서대로 우리는 간략하게 **Validation Check Plug-in**을 만들어 보면서 TDD와 Mocha를 동시에 파악할 것이다.

## 1. 명세 작성

프로세스 순서에 따라 명세를 작성한다. 명세를 작성하기 위해서는 우리가 무엇을 개발해야 하는지 목표를 정확하게 파악하는 것이 좋다. 우리는 **Validation Check Plug-in** 만드는 것을 목표로 필요한 사항을 명세에 적어볼 수 있겠다. 

{% alert info %}
* 이메일의 형식을 검증한다.
* 전화번호의 형식을 검증한다.
* 이름의 형식을 검증한다.
{% endalert %}

간략하게 3가지의 명세를 적어보았다. Validation Check를 진행하는데 필요한 몇 가지의 기능을 나열한 것이다.

## 2. 개발 명세에 따른 테스트 코드 작성

개발 명세를 작성하였으니 테스트 코드를 작성해 보자. 첫 번째로 `이메일의 형식을 검증한다.`는 것에 대해 테스트 코드를 작성해 볼 것이다. `Assertions`는 `Chai`를 사용할 것이다. `Chai`에 대해서는 [Step 02: Assertion-chai](https://kdydesign.github.io/2017/06/15/Mocha-step-02/)를 참고하자.

해당 파일은 `test.js`와 같은 테스트 파일이 될 것이다.

```javascript
var chai = require('chai');
var expect = chai.expect;

suite('#Validation Check', function () {
    test('이메일의 형식을 검증한다.', function () {
        var validate = new Validate();
        var result = validate.email('test@naver.com');

        expect(result).to.be.true;
    });
});
```

우리는 TDD를 진행할 것이니 테스트 스위트의 스타일을 `describe`, `it`이 아닌 `suite`, `test`를 사용했다. 물론 Mocha의 옵션 역시 `--ui tdd`로 주어야 한다. [Step 03: Hooks](https://kdydesign.github.io/2017/06/16/Mocha-step-03/)을 참고하자.

## 3. 테스트 실행

위에 테스트 코드를 실행해보자. 당연히 **비즈니스 코드**가 없기 때문에 오류가 발생 될 것이다. 여기까지만 보아도 왜 TDD가 `테스트 주도 개발`인지 알 수 있다. 테스트 코드를 먼저 작성 후 이후에 비즈니스 코드를 작성한다.

## 4. 테스트가 성공하도록 최소한의 비즈니스 로직 작성

이제 작성한 테스트 코드가 통과될 수 있도록 최소한으로써 비즈니스 코드를 작성해보자. 해당 파일은 `validate.js`와 같은 적당한 파일이 될 것이다.

```javascript
function Validate() {

}

Validate.prototype = {
    email: function (email) {
        var regex = /^[0-9a-zA-Z]([-_\.]?[0-9a-zA-Z])*@[0-9a-zA-Z]([-_\.]?[0-9a-zA-Z])*\.[a-zA-Z]{2,3}$/i;

        return regex.test(email);
    }
};

module.exports = Validate;
```

`validate.js`를 만들었으니 이미 만든 테스트 코드가 있는 `test.js`에 해당 모듈을 불러오자.

```javascript
//...
var Validate = require('./validate');
//...
```

여기서 언급할 내용은 코드의 설명이 아닌 TDD에 대한 내용이다. 처음 TDD를 접하게 되면 다소 난감한 상황에 부딪힌다. 그 부분은 첫 테스트 코드를 작성할 때이다. 막막하기 그지없다. 무엇을 시작해야 할지 모르기 때문이다. 이때 기억해야 할 것은 이것이다.

{% alert info %}
* **given** - 어떤 조건이 필요한가.
* **when** - 어떻게 동작이 진행되는가.
* **then** - 동작에 대한 결과가 어떠한가.
{% endalert %}

?????... 무슨 말이지.. 
이 내용을 위에 작성한 코드에 대입해보자.

```javascript
var chai = require('chai');
var expect = chai.expect;

suite('#Validation Check', function () {
    test('이메일의 형식을 검증한다.', function () {
        //given
        var validate = new Validate();
        
        //when
        var result = validate.email('test@naver.com');

        //then
        expect(result).to.be.true;
    });
});
```

주석을 적어놓으니 이해가 되는 듯하다. TDD에 익숙하지 않다면 `given`, `when`, `then` 패턴을 기억하고 주석을 먼저 적고 시작하자.

## 5. 테스트 실행

이제 테스트 코드를 실행해보자. 적당하게 비즈니스 코드를 작성하였다. 테스트 코드가 실패한다면 비즈니스 코드를 수정하자.
 
## 6. 테스트 케이스 추가

5번에서 테스트가 성공하였다면 바로 변칙적인 다른 테스트 케이스를 추가하자.

```javascript
var chai = require('chai');
var Validate = require('./validate');
var expect = chai.expect;

suite('#Validation Check', function () {
    test('이메일의 형식을 검증한다.', function () {
        //given
        var validate = new Validate();

        //when
        var result1 = validate.email('test@naver.com');
        var result2 = validate.email('test_1234@naver.com');
        var result3 = validate.email('!@test@naver.com');
        var result4 = validate.email('test#naver.com');
        var result5 = validate.email('test');
        var result6 = validate.email('naver.com');

        //then
        expect(result1).to.be.true;
        expect(result2).to.be.true;
        expect(result3).to.be.false;
        expect(result4).to.be.false;
        expect(result5).to.be.false;
        expect(result6).to.be.false;
    });
});
```

## 7. 테스트 실행

테스트를 실행해보자. 여기서 테스트 실패가 나온다면 비즈니스코드가 잘못된 것이니 테스트가 성공하도록 비즈니스 코드를 수정하면 된다.

## 8. 테스트 코드 및 테스트 케이스 Refactoring

테스트 케이스를 추가하고도 완료되었다면 테스트 코드 및 비즈니스 코드를 `Refactoring`을 진행하면 된다. 테스트 코드를 `Refactoring`하는 이유는 당연히 유지관리를 위해서이다. 테스트 코드는 일회성이 아닌 유지관리 포인트에 포함되는 사항이기 때문이다.
6번에서 작성한 코드가 반복적인 부분이 많다. result1, 2, 3, 4....라니... 수정하도록 하자.

```javascript
var chai = require('chai');
var Validate = require('./validate');
var expect = chai.expect;

suite('#Validation Check', function () {
    test('이메일의 형식을 검증한다.', function () {
        //given
        var successTestCase = [
            'test@naver.com', 'test_1234@naver.com'
        ];

        var failTestCase = [
            '!@test@naver.com', 'test#naver.com', 'test', 'naver.com'
        ];

        var validate = new Validate();

        successTestCase.forEach(function (testCase) {
            //when
            var result = validate.email(testCase);

            //then
            expect(result).to.be.true;
        });

        failTestCase.forEach(function (testCase) {
            //when
            var result = validate.email(testCase);

            //then
            expect(result).to.be.false;
        });
    });
});
```

가독성을 위해 `success`와 `fail`로 나눠 보았다. 자세히 보니 명세에 적힌 기능을 구현해본다면 `Validate` 객체를 테스트 케스트마다 생성할 테니 미리 `Refactoring`을 하자.

```javascript
var chai = require('chai');
var Validate = require('./validate');
var expect = chai.expect;

suite('#Validation Check', function () {
    var validate = null;
    var successTestCase = [];
    var failTestCase = [];

    suiteSetup(function () {
        validate = new Validate();
    });

    suiteTeardown(function () {
        validate = null;
        successTestCase = [];
        failTestCase = [];
    });

    test('이메일의 형식을 검증한다.', function () {
        //given
        successTestCase = [
            'test@naver.com', 'test_1234@naver.com'
        ];

        failTestCase = [
            '!@test@naver.com', 'test#naver.com', 'test', 'naver.com'
        ];

        successTestCase.forEach(function (testCase) {
            //when
            var result = validate.email(testCase);

            //then
            expect(result).to.be.true;
        });

        failTestCase.forEach(function (testCase) {
            //when
            var result = validate.email(testCase);

            //then
            expect(result).to.be.false;
        });
    });
});
```
## 9. 테스트 실행

실행해보자. 테스트가 실패한다면 비즈니스 코드 수정 후 7번으로 돌아가 반복적으로 테스트를 진행하면 된다.

- - -

여기까지가 Mocha의 마지막 지점이다. 물론 명세에 있는 내용을 다 포스팅하진 않았지만, 처음에 말했듯이 `하나의 짧은 Cycle을 반복적으로 수행하는 것`이다. 물론 테스트함에 있어서 특수한 케이스가 나올 수 있지만, TDD를 사용하는 목적을 다시 생각해 보면 어느 부분부터 다시 시작해야 하는지 알 수 있을 것이다. 


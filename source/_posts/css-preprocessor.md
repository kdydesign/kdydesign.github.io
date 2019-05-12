---
title: "CSS 전처리기(Pre-Processor) 배우기!"
date: 2019-05-12 15:21:40
tags: 
- css
- css pre-processor
- sass
- less
- stylus
categories :
- css
- css pre-processor
- sass
- less
- stylus
keywords:
- css
- css3
- css 전처리기 배우기
- css 전처리기 튜토리얼
- css 전처리기 tutorial
- sass 배우기
- less 배우기
- stylus 배우기
- sass 기초
- css 전처리기
- css preprocessor
- sass
- less
- stylus
- scss
- sass 장점
- sass 단점
- 전처리기 단점
- 전처리기 장점
disqusIdentifier: css-pre-processor
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
이번 포스트에서는 Sass, Less, Stylus와 같은 CSS 전처리기(CSS Pre-Processor)에 대해 알아보자. CSS 전처리기(CSS Preprocessor)는 CSS 작성 모듈별로 특별한 Syntax를 가지고 있고 여기에 믹스인(mixin), 중첩 셀렉터(nesting selector), 상속 셀렉터(inheritance selector) 등 Programmatically 한 요소를 접목해 방대해지는 CSS 문서의 양을 효율적으로 처리하고 관리해 주는 통합적인 단어를 말한다.
<!-- more -->

<!-- excerpt -->
<!-- excerpt -->

이번 포스트에서는 `Sass`, `Less`, `Stylus`와 같은 `CSS 전처리기(CSS Preprocessor)`에 대해 알아보자.

CSS 전처리기(CSS Preprocessor)는 모듈별로 특별한 `Syntax`를 가지고 있고 여기에 `믹스인(mixin)`, `중첩 셀렉터(nesting selector)`, `상속 셀렉터(inheritance selector)` 등 Programmatically 한 요소를 접목해 방대해지는 CSS 문서의 양을 효율적으로 처리하고 관리해 주는 통합적인 단어를 말한다. 이 CSS 전처리기(CSS Preprocessor) 자체만으로는 웹 서버가 인지하지 못하기 때문에 각 CSS 전처리기에 맞는 `Compiler`를 사용해야 하고 컴파일을 하게 되면 실제로 우리가 사용하는 CSS 문서로 변환이 된다.

이번 포스트에서는 이 세 가지의 CSS 전처리기를 비교해보고 동향을 알아보며, Sass, Less, Stylus를 직접 설치 및 사용하는 방법을 배워보자.

***- 해당 포스트에서는 세 가지의 전처리기 문법을 다루지는 않습니다. -***


# CSS 전처리기(CSS Preprocessor)
위에 설명한 바와 같이 `CSS 전처리기(CSS Preprocessor)`는 CSS 문서의 작성에 도움을 주는 도구이다. 우리가 흔히 CSS 문서 작성할 때는 많은 반복적인 작업을 요구하고 Color 값을 찾는 일, tag를 닫는 일 등 번거로운 작업 역시 포함되어있다. 그뿐만 아니라 클래스의 상속과 같은 사항으로 점점 CSS 문서는 양이 많아지고 이로 인해서 이후 유지관리에 많은 영향을 준다. 이런 CSS의 문제점들을 Programmatically 한 방식. 즉 변수, 함수, 상속 등 일반적인 프로그래밍 개념을 사용하여 해결해 나갈 수 있다.

CSS 전처리기(CSS Preprocessor)에는 다양한 모듈이 존재하고 가장 많이 사용되는 전처리기에는 `Sass`, `Less`, `Stylus`가 있으며, 서로의 특징에 맞게 약간의 Syntax만 다를 뿐 개념 자체는 동일하기 때문에 Learning curve가 낮은 편이다.


## 장점
CSS 전처리기(CSS Preprocessor) 역시 하나의 기술이기 때문에 장단점이 존재할 수밖에 없다. 장점이라 하면 위에서도 설명했지만 정리하자면 이렇다.

* 재사용성 - 공통 요소 또는 반복적인 항목을 변수 또는 함수로 대체
* 시간적 비용 감소 - 임의 함수 및 Built-in 함수로 인해 개발 시간적 비용 절약
* 유지 관리 - 중첩, 상속과 같은 요소로 인해 구조화된 코드로 유지 및 관리가 용이

**재사용성**의 장점을 가장 쉽게 파악하는 방법은 `CSS에서 color를 지정`하는 방법을 생각해보자. 우리가 특정 클래스에 color 속성을 주고 값을 지정할 때 `hex code` 또는 `RGB`로 지정을 한다. 하지만 특정 색상이 반복된다면 우리는 주기적으로 색상 코드를 찾고 반영을 해줘야 한다. 하지만 CSS 전처리기(CSS Preprocessor)에서는 이런 반복되는 부분을 변수로 처리할 수 있다. 대부분 실무에서는 하나의 파일 안에 `color-set`을 모두 정의하여 사용된다.


```css
$primary-color: #fff

.class-A {
    background-color: $primary-color
}

.class-B {
    background-color: $primary-color
}
```

**시간적 비용 감소**에 대해서 보자. 각 CSS 전처리기(CSS Preprocessor)에는 `내장함수(Built-in Functions)`가 존재한다. 이 내장 함수는 이미 전처리기 내에 포함된 함수로 우리는 필요한 값들만 전달하면 이에 대한 결과를 생성해 준다. 예를 들어 `darken(color, amount)`이라는 내장 함수는 색상과 퍼센티지를 지정해 주면 거기에 알맞은 값을 출력해 준다.

```css
$color: #2ecc71
$buttonDark: darken($buttonColor, 10%)

button {
    background: $color;
    box-shadow: 0px 5px 0px $buttonDark
}
```


**유지 관리**는 가장 중요하고 눈에 띄는 장점 중의 하나이다. 클래스를 정의하다 보면 상속과 공통 속성을 지정하기 위해서 무지막지하게 길게 정의를 한다. 이런 이유로 CSS 문서가 가독성이 매우 떨어지는 이유 중 하나이다. 이런 내용을 CSS 전처리기(CSS Preprocessor)에서는 `중첩(Nesting)`과 `상속(Extend)`을 통해 구조화 할 수 있다.

`중첩(Nesting)`은 아래처럼 정의한다.

```css
.class-A {
    width: 100%

    .A-child-1 {
        color: red
    }

    .A-child-2 {
        color: blue
    }
}
```

위 내용을 컴파일하게 되면 아래와 같다.

```css
.class-A {
    width: 100%
}

.class-A .A-child-1 {
    color: red
}

.class-A .A-child-2 {
    color: blue
}
```

`상속(Extend)`은 아래처럼 정의한다.

```css
.class-A {
    color: red
    padding: 10px
}

.class-B {
    @extend: .class-A
    border: 1px solid red
}
```

위 내용을 컴파일하게 되면 아래와 같다.

```css
.class-A, .class-B {
    color: red
    padding: 10px
}

.class-B {
    border: 1px solid red
}
```

## 단점
성능, 사용성 등 단점을 찾고 있겠지만 가장 중요한 것 중 하나가 실무에서의 사용이다. 그리고 이 내용이 곧 단점이 되기도 하다. 실무에서는 대부분 `CSS의 작업(Publishing)`은 `퍼블리셔(Publisher)` 또는 `디자이너(Designer)`가 진행하게 된다. 물론 Front-End 개발자가 진행하는 경우도 있지만 좀 더 체계가 필요한 회사나 프로젝트에서는 퍼블리셔나 디자이너가 퍼블리싱 작업을 하는 경우가 있는데 퍼블리셔나 디자이너가 개발에 대한 역량과 요소를 알아야 한다는 것이 문제이다. 지금까지 말했지만, CSS 전처리기(CSS Preprocessor)는 Programmatically 한 요소를 접목했기 때문에 분기문 처리, 변수의 이해, mixin의 이해 등 개발적인 요소를 알아야 하기 때문이다. Learning curve가 낮다는 장점은 순전히 개발자에 한해서이다.

여기까지 해서 CSS 전처리기(CSS Preprocessor)의 장점과 이에 따른 간단한 예제를 보았다.


# Sass, Less, Stylus 비교
`Sass`, `Less`, `Stylus`는 가장 대표적인 전처리기이다. 만약 전처리기 도입을 고민한다면 사실상 이 세 개의 전처리기 차이가 크지 않기 때문에 어느 것을 선택해도 문제는 되지 않지만 그래도 선택이 어렵다면 이 섹션을 보고 조금이나마 도움이 되었으면 한다.

먼저 `Trend`를 보자.

<script type="text/javascript" src="https://ssl.gstatic.com/trends_nrtr/1754_RC01/embed_loader.js"></script> <script type="text/javascript"> trends.embed.renderExploreWidget("TIMESERIES", {"comparisonItem":[{"keyword":"Sass","geo":"","time":"today 5-y"},{"keyword":"Less","geo":"","time":"today 5-y"},{"keyword":"Stylus","geo":"","time":"today 5-y"}],"category":733,"property":""}, {"exploreQuery":"cat=733&date=today%205-y&q=Sass,Less,Stylus","guestPath":"https://trends.google.co.kr:443/trends/embed/"}); </script> 


<script type="text/javascript" src="https://ssl.gstatic.com/trends_nrtr/1754_RC01/embed_loader.js"></script> <script type="text/javascript"> trends.embed.renderExploreWidget("GEO_MAP", {"comparisonItem":[{"keyword":"Sass","geo":"","time":"today 5-y"},{"keyword":"Less","geo":"","time":"today 5-y"},{"keyword":"Stylus","geo":"","time":"today 5-y"}],"category":733,"property":""}, {"exploreQuery":"cat=733&date=today%205-y&q=Sass,Less,Stylus","guestPath":"https://trends.google.co.kr:443/trends/embed/"}); </script> 


Trend에서는 검색어를 통한 관심도를 볼 수 있다. 정확하게 CSS 전처리기에 대해 검색을 하지 않았고 포함된 관심도이지만 `Sass`를 가장 많이 사용하는 것을 볼 수 있다. 그럼 Github의 Start 수와 Fork 수를 확인해 보자.

![css-github](github.png)

NPM 기준으로 확인해보자.

![npmcompare](npmcompare.png)

수치상으로만 볼 때는 무엇이 높고 낮음은 판가름이 되지만 그게 정확한 척도는 되지 않는다.

위 세 전처리기 모두 사용해보는 것이 좋을 것이지만 무엇을 사용할지의 판단은 본인의 몫이고 필자로서는 무엇을 써도 무방하다고 생각된다.

이제 이 세 개의 CSS 전처리기에 대해서 간략하게 알아보도록 하자.

# Sass vs Less vs Stylus
초기에는 JavaScript로 작성된 `Less`가 가장 선호되었다. `node-sass`가 나오고 나서부터는 `Sass`가 선호되고 있다. `Stylus`는 가장 늦게 나온 전처리기로 최근 들어서 `open-project`에 많이 사용되고 있다.

## Sass
`Sass`는 전처리기 중 가장 먼저 나온 전처리기이다. 최초에는 `Ruby` 언어를 기반으로 구동되었지만 `Ruby` 언어가 지닌 한계로 컴파일이 다소 느렸기 때문에 `Less`를 더 선호하였다. 하지만 `node-sass`라는 `Node.js`기반의 라이브러리가 나오면서 이후 `Sass`를 많이 사용하고 있다. 최근에는 `sass` 자체가 NPM에 등록되어있다. 다른 전처리기에 비해 상대적으로 다양한 기능이 제공되고 지속적인 업데이트가 진행되고

### Sass 설치
npm을 통한 설치 방법이다.

```
$ npm install -g sass
```

### Sass 컴파일
기본적인 컴파일은 아래처럼 사용하고 더 자세한 커맨드 라인은 [Sass Command-Line Interface](https://sass-lang.com/documentation/cli)를 참고하자.

```
$ sass styls.scss styls.css
```

## Less
`Less`는 `Twitter의 Bootstrap`에서 사용되면서 전파되기 시작했고 Client(브라우저)에서 자바스크립트 Parser를 통해 실행된다. `Sass`와는 다르게 초창기부터 `Node.js`기반으로 구동되었고 `Sass`에 비해 컴파일 속도가 빠른 것이 장점이었으나 `Sass`가 캐쉬를 적용한 뒤로부터는 큰 차이가 없어졌다.

### Less 설치
NPM을 통한 설치 방법이다.

```
$ npm install -g less
```

### Less 컴파일
기본적인 컴파일은 아래처럼 사용하고 더 자세한 커맨드 라인은 [Using Less.js](http://lesscss.org/usage/)를 참고하자.

```
$ lessc style.less style.css
```

## Stylus
`Stylus`는 가증 나중에 나온 전처리기로 `Less`와 동일하게 `Node.js`기반으로 구동된다. 가장 늦게 발표된 전처리기이지만 많은 기능이 구현되어있다. 몇 년 전만 해도 다른 전처리기에 비해 완성도가 낮고 여러 잔존 버그가 존재하였지만, 시간이 지남에 따라 많은 부분이 해결되어 최근에는 많은 `open-project`에서 사용되고 있다.

### Stylus 설치
NPM을 통한 설치 방법이다.

```
$ npm install -g stylus
```

### Stylus 컴파일
기본적인 컴파일은 아래처럼 사용하고 더 자세한 커맨드 라인은 [Stylus Executable](http://stylus-lang.com/docs/executable.html)을 참고하자.

```
$ stylus style.styl style.css
```

- - -


지금까지 CSS 전처리기(CSS Preprocessor)에 대해서와 `Sass`, `Less`, `Stylus`를 알아보았다. 확실히 CSS 전처리기를 사용하면 많은 도움이 된다. 다만 단점 섹션에서도 말했듯이 실제로 기술을 습득하고 반영해야 하는 사람은 개발자가 아닐 수 있다는 것이다.

해당 포트스에 각 전처리기에 대한 문법에 대해서 언급하지 않은 이유는 세 전처리기에 대한 문법이 비슷하기 때문에 오히려 어떤 전처리기를 사용할지 결정에 있어서 혼동을 줄 수 있을 것 같아서이다. 위 섹션에서 설치 방법과 컴파일하는 명령어만 보아도 비슷한 것을 알 수 있을 것이다. 각 세 전처리기의 Document는 모두 잘 되어있기 때문에 문법에 대해서는 각 API를 참고하기 바란다.

* [Sass](https://sass-lang.com/)
* [Less](http://lesscss.org/#)
* [Stylus](http://stylus-lang.com/)

---

더 알아보기
> [빠르게 배우는 Node.js와 NPM 설치부터 개념잡기](https://kdydesign.github.io/2017/07/15/nodejs-npm-tutorial/)

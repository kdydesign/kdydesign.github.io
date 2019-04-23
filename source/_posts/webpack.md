---
title: "Webpack 개념잡기"
date: 2017-07-27 15:17:51
tags: 
- nodejs
- javscript
- webpack
- build tool
- gulp
- webpack
categories :
- javascript
- nodejs
- build tool
- webpack
keywords:
- javascript
- nodejs
- webpack
- gulp
- javascript build tool
- webpack build
- webpack 설치
- 웹팩 설치
- webpack tutorial
- webpack 강좌
- webpack 튜토리얼
- webpack 배우기
- webpack 사용법
disqusIdentifier: webpackOrg
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
Web front-end build tool에는 여러 가지가 있다. 이러한 build tool은 단순히 소스를 묶고 컴파일하고 압축하는 단순한 형태에서 벗어나 하나의 기술로 자리잡혔다. 이 build tool들을 활용함으로써 우리가 진행하는 프로젝트에 엄청난 시너지를 안겨 줄 수 있다. 수많은 build tool 중 이 포스트에서는 떠오르는 build tool인 webpack에 대해 소개하겠다.
<!-- more -->

<!-- excerpt -->
<!-- excerpt -->

![cover](cover.png)

`Web front-end build tool`에는 여러 가지가 있다. 이러한 `build tool`은 단순히 소스를 묶고 컴파일하고 압축하는 단순한 형태에서 벗어나 하나의 기술로 자리잡혔다. 이 `build tool`들을 활용함으로써 우리가 진행하는 프로젝트에 엄청난 시너지를 안겨 줄 수 있다. 수많은 `build tool` 중 이 포스트에서는 **떠오르는 build tool인 `webpack`**에 대한 소개와 프로젝트를 진행하면서 왜 `Build Tool`이 필요한지 포스팅하겠다.

## Build Tools

`Build`는 서버 사이드에서만 사용하는 것이 아닌 `Web Front-End`에서도 필수이다. JavScript와 CSS를 축소하고 단위 테스트도 수행하며 프로젝트에 필요한 자산들(Image, Font)을 효율적으로 관리할 수 있을 뿐만 아니라 패키지화까지 진행할 수 있다. 이러한 사항들로 인해 결국 해당 프로젝트의 성능과 개발의 편의, 그리고 개발 속도가 향상될 수 있다. 물론 build를 실행하지 않고 직접적으로 시스템 파일을 `Linking`하여 사용할 수도 있겠지만 우리는 언제나 `Performance` 대립하게 되어있다. 그럼 이 `Front-End`의 `build tool`에는 어떤 것이 있을까?

> Jake
> Brunch
> Grunt
> Gulp
> Webpack
> Brocolli
> Cha

너무 많다. 그냥 "이런 게 있구나.."라고 기억만 하자. 

그럼 왜 저 많은 `build tool` 중에서 `Webpack`을 포스팅하는 것일까? 저 `build tool` 중 가장 많이 사용하는 tool은 {% hl_text orange %}Gulp{% endhl_text %}와 {% hl_text orange %}Grunt{% endhl_text %} 그리고 {% hl_text danger %}Webpack{% endhl_text %}이다. 이 세 가지를 비교해 볼 수는 없다. 셋 모두 훌륭한 시스템이다. 단지 [NPMCOMPARE](https://npmcompare.com/compare/grunt,gulp)에서 `Gulp`와 `Grunt`를 비교해 보았을 때 `Gulp`가 좀 더 활성화되어 있는 것을 볼 수 있다. 그렇다면 `Webpack`은??

## Webpack VS Gulp

사실 `Webpack`와 `Gulp`은 다르게 볼 수 있다. `Webpack`은 `Package Bundler`이며, `Gulp`는 `Task Runner`이다. 크게 다르다고는 할 수 없지만, 이 이유가 `Webpack`을 포스팅하는 이유이다. 그럼 `Task Runner`와 `Package Bundler`는 무슨 차이일까.

{% alert info no-icon %}
**Package Bundler** - 종속성을 가진 애플리케이션 모듈을 정적인 소스로 재생산
**Task Runner** - 반복 가능한 특정 작업을 자동화
{% endalert %}

쉽게 말하면 `Task Runner`는 그저 미리 정의해 놓은 어떠한 작업을 실행하는 것이고 `Package Bundler`는 말 그대로 어떤 소스들을 하나의 패키지화 하는 것이다. 

구글 트렌드를 통해 `Gulp`와 `Webpack`의 검색 추이를 보게 되면 처음에는 `Gulp`가 우세한 면을 보이지만 최근 들어 `Webpack`이 `Gulp`를 넘어서 더 우세한 것을 볼 수 있다. 

<script type="text/javascript" src="https://ssl.gstatic.com/trends_nrtr/1101_RC01/embed_loader.js"></script> <script type="text/javascript"> trends.embed.renderExploreWidget("TIMESERIES", {"comparisonItem":[{"keyword":"Webpack","geo":"","time":"today 5-y"},{"keyword":"Gulp","geo":"","time":"today 5-y"}],"category":31,"property":""}, {"exploreQuery":"cat=31&date=today 5-y&q=Webpack,Gulp","guestPath":"https://trends.google.co.kr:443/trends/embed/"}); </script>

이는 프로젝트 규모와 그리고 `Task Runner`로는 진행할 수 없는 `Webpack`만의 중요한 종속성 관리에 따라 변화된 것으로 보인다. 이러한 종속성 관리는 프로젝트 규모가 클수록 더 빛을 발하며 그리고 날이 갈수록 `단일 웹 애플리케이션(SPA)`의 확산에 따라 중요한 자리를 차지하고 있다. 이 그래프에서 우리가 유추해 볼 수 있는 또 다른 하나는 `Webpack`과 `Gulp`의 교차 지점이다. 이 기간에서는 `Webpack`과 `Gulp`를 같이 사용했다고 볼 수 있다. 물론 지금도 그렇게 사용하는 개발자도 있다. `jsHint`나 `jsLint`등의 코드 검사 도구 또는 `mocha`나 `jasmine`과 같은 테스트 도구를 `Gulp`를 통해 실행하고 이 후 프로젝트의 패키징은 `Webpack`으로 사용하는 것처럼 말이다. 하지만 `Webpack`에서도 `Gulp`와 마찬가지로 전처리 작업을 지원하면서 `Webpack`이 더욱 상승세를 보인다. 

`Webpack`과 `Gulp`의 [NPM COMPARE](https://npmcompare.com/compare/gulp,webpack)를 보게 되면 `Gulp`가 종속된 모듈수가 적고 발생 이슈가 낮지만, 전체적인 면에서 보면 현재로서는 `Webpack`이 좀 더 활성화가 된 것을 볼 수 있다. 그럼 먼저 간단하게 `Webpack`와 `Gulp`의 특징을 알아보도록 하겠다.

### Webpack

위에서 말했듯이 `Webpack`은 JavaScript 애플리케이션을 위한 `Package Bundler`이고 목적은 종속성을 가진 애플리케이션 모듈을 정적인 소스들로 생산하는 것이다. 애플리케이션을 처리할 때 필요한 모든 모듈을 종속성 그래프로 반복적으로 작성한 다음 모든 모듈을 브라우저에서 로드 할 수 있는 하나의 Bundle로 패키지화한다. 이 외의 특징은 다음과 같다. 

{% alert info no-icon %}
* Loader를 통해 Javascript, Image file, Font, CSS, SCSS 등과 같은 자산을 하나의 모듈로 취급
* Entry 별로 Bundle 생성 가능
* Bundle에 대한 압축 및 난독화, 소스 맵에 대한 옵션을 제공
* Plug-In 사용을 통한 사용자 정의 기능 수행
* 비동기 I/O와 다중 캐시 레벨을 사용하기 때문에 컴파일 속도가 매우 빠름
* CommonJS(nodejs)와 AMD(requires) 스펙 지원
{% endalert %}


`Webpack`은 크게 `Entry`, `Output`, `Loader`, `Plug-In` 이 4가지로 나눌 수 있다. 

{% alert danger no-icon %}
**Entry** - Webpack은 모든 애플리케이션에 대한 종속성 그래프를 작성하고 이 그래프의 시작점을 Entry Point라고 한다. 이 Entry Point를 통해 모듈이 어디서부터 시작하는지를 명세하는 애플리케이션을 시작하는 첫 번째 파일로 나타낼 수 있다.
**Output** - Output은 모든 애플리케이션의 자산(resources 또는 assets)을 하나의 Bundle로 묶었으면 해당 Bundle을 처리하는 방법을 명세한다.
**Loader** - Loader는 사전에 처리할 작업을 나타내며 css, html, jpg, scss 등의 자산을 하나의 모듈로 취급하며 이러한 파일들을 종속성 그래프에 추가할 때 모듈로 변환한다.
**Plug-In** - Plug-In은 일반적인 Compile 또는 모듈 처리에 필요한 작업 및 사용자 정의 기능을 수행하는데 사용한다.
{% endalert %}

`Webpack`의 장점은 이렇게 많지만 단점이라 하면 초기 구축에 대한 시간적인 비용이 많이 투자되며 Learning Curve가 길다는 점이다.

### Gulp

`Gulp`는 `Task Runner`이며, `Work Flow`를 자동화 및 향상할 수 있는 도구이다. 개발 `Work Flow`에서 번거로운 작업들이나 시간적인 소모가 많이 들어가는 작업을 자동화하여 쉽게 처리할 수 있다. `Gulp`의 특징을 보자.

{% alert info no-icon %}
* 반복 가능한 작업을 자동화
* JavaScript 테스트 실행 및 파일 병합
* js, css, html등의 자산 파일을 압축
* Node stream 기반으로 빠른 빌드 속도를 제공
* 작업을 정의하고 실행하는 것이 수월
{% endalert %}

`Gulp`는 `Webpack`에 비하여 `Learning Curve`가 낮기 때문에 사용하기 쉬운 편이며, 코드에 대한 가독성이 좋다. 대신 `Webpack`과 같이 모든 모듈에 대한 종속성 관리가 이루어지지 않기에 규모가 큰 프로젝트에서 패키지화하기가 쉽지 않다. 나도 `Gulp`를 사용하지만 개인 오픈 소스 프로젝트를 진행하는데에는 이만한 Tool도 없다.

- - -

지금까지 우리는 `Webpack`과 `Gulp`를 알아 보았다. 전체적으로 본다면 `Build Tools`를 알아 본 것이다. 이번 포스팅에서는 `Webpack`이 기준이기 때문에 `Webpack`에 대해 좀 더 자세히 알아보았지만, 명심해야 할 것은 무조건 `Webpack`이 좋다는 것이 아니다. `Gulp`, `Grunt` 역시 훌륭한 `Build Tool`이다. 우리가 진행해야 할 프로젝트에 어떤 것이 더 효과적이고 필요한지를 되새김하고 그에 걸 맞는 `Build Tool`을 선정해야 할 것이다.

다음 포스팅에서는 실제로 `Webpack`을 어떻게 사용하지. `Webpack` 설치부터 응용까지 해 보기로 하자.

---

더 알아보기
> [Webpack 완전정복하기!!](https://kdydesign.github.io/2017/11/04/webpack-tutorial/)


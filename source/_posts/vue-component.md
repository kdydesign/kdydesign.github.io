---
title: "Vue.js Component 개념을 익히고 만들어보자!!"
date: 2019-04-27 16:05:38
tags: 
- javascript
- framework
- vue.js
categories :
- javascript
- framework
- vue.js
keywords:
- javascript
- vue.js
- vue 튜토리얼
- vuejs 튜토리얼
- vuejs 강좌
- vuejs 설치
- vue 기초
- store
- vuex
- vue.js tutorial
- vue 배우기
- vuejs 배우기
- vue-cli 3
- vue-cli 3 배우기
- vue-cli 3 tutorial
- vue-cli
- vue-cli 3 개념
- vue-cli 3 설치
- vue.js component 만들기
- vuejs 컴포넌트
- vue 컴포넌트 만들기
- vuejs 컴포넌트 만들기
- vuejs component 만들기
disqusIdentifier: vueComponent01
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
Vue.js의 기본 개념을 익히고 기본적인 Vue.js Component를 생성해 보자. Vue.js의 Component 개념은 Vue.js Framework에서도 중요한 부분을 차지하고 어떻게 Vue.js Component를 생성하느냐에 따라 Vue.js의 개발속도와 코드의 가독성, 그리고 효율성이 현저히 차이가 난다.
우리는 이번 포스트에서 Vue.js의 Component 생성 방법에 대해 알아보고 실제로 Vue.js의 Component를 직접 만들어보기로 하자. 이번 포스트는 공식 문서에 나와있는 컴포넌트 생성 방법의 여러가지 방법 중에 어떤 것이 실무에서 효율적인 것인지를 파악하는 Vue.js Tutorial이다.
<!-- more -->

<!-- excerpt -->
<!-- excerpt -->

![cover](cover.png)

이번 포스트에서는 Vue.js의 기본 개념을 익혔다는 가정 하에 Vue.js의 강력한 기능 중인 하나인 `Component`에 대해서 알아보자. 먼저 포스팅을 하기 전에 앞써서 기본 `Vue.js`에 대한 개념과 추세를 모르거나 알고 싶다면 [빠르게 배우는 Vue.js](https://kdydesign.github.io/2017/11/15/vuejs-tutorial/) 포스트를 먼저 확인하자.

`Vue.js Component`에 대해서 포스팅 할 내용들은 많지는 않다. 개념부터 사용법까지 본다면 분량은 얼마되지는 않지만 가장 중요하기 때문에 깊게 봐야할 필요성이 있다. 실무에서 특정 프로젝트에 Vue.js를 도입을 한다면 더욱이 깊게 봐야한다. Vue.js Component는 API 문서대로 **전역 등록**을 통한 Component 생성과 **지역 등록**을 통한 컴포넌트 등록이 있고 이 두 형태를 가지고 문법대로 생성하면 끝이다. 하지만 중요한 것은 컴포넌트의 생성 범위이다. 어떤 컴포넌트를 `전역/지역`으로 등록을 할 지, 그리고 어떤 특정 부분을 컴포넌트로 만들어야 할 지가 중요하다. 즉, 쉽게 말한다면 **`설계`** 가 가장 중요하다고 볼 수 있다.

Vue.js Component를 배우고 만들기 앞서 가장 중요한 Component의 설계를 먼저 보자.

# Vue.js Component 설계의 중요성

위에서 언급했듯이 **Component를 생성할 때에는 설계가 가장 중요**하다. Component를 만드는 방법이야 [Vue.js 공식](https://kr.vuejs.org/v2/guide/components.html) API를 보고 문법을 익혀 만들면 그만이다. 하지만 Component를 어느 곳에 사용하고 어느 부분이 Component 화 해야할지에 대해 정확한 설계가 없다면 이 후 전반적으로 문제를 야기한다. 물론 Application을 개발 할 때 모든 항목들 Component 단위로 잘게 쪼개도 Application 성능에 크게 영향을 주지는 않지만 규모가 크거나 또는 점점 규모가 커지는(고도화) 프로젝트에서는 해당 프로젝트의 유지관리와 개발 진행 단계에 영향을 준다는 말이다.

설계를 무시하고 `Vue.js Component`를 생성했을 때 아래와 같은 문제점들이 있다. 

> 1. 무분별한 Component의 생성은 코드의 가독성과 유지보수를 현저하게 떨어뜨린다.
> 2. 복잡한 구조를 가진 Component의 사용은 Component의 순환과 참조를 어렵게 만든다.
> 3. 독립적인 컴포넌트로 작성되는 경우가 존재한다.


## 1. 무분별한 Component의 생성은 코드의 가독성과 유지보수를 현저하게 떨어뜨린다.

무분별한 Component의 생성은 코드의 가독성과 유지보수 시 개발 능력를 현저하게 떨어뜨린다. 대부분 특정 부분을 Component화를 한다고 했을때 굳이 Component를 안해도 되는 부분까지 나눠서 Component화 하는 경우가 많다. 아주 간단하게 로그인 페이지를 만든다고 했을 때 ID, Password 입력 폼을 각각의 Component로 만드는 것이다. 이렇게 되면 메인이 되는 App은 매우 심플해 지겠지만 우리는 ID, Password 폼을 각각 찾아 다니며 분석하고 수정해야한다.
딱 보아도 `로그인 페이지 하나 만드는데 무슨 컴포넌트를 쓰고 가독성과 복잡성을 논하는가` 라고 생각하는가? 그렇다면 이미 설계의 중요성을 알고 있는 것이다. 하지만 당신 로그인 페이지가 아니라 수십개의 페이지가 존재하는 Application을 구현할 때 이미 알고 있고 느끼는 부분을 망각하고 개발을 한다. Application의 전반적인 내용을 알고 있다 하더라도 설계를 무시하고 한다면 당연시하게 되는 일이다. 그만큼 특정 부분을 Component로 나누고 생성한다는 것은 어려운 일이다.


## 2. 복잡한 구조를 가진 Component의 사용은 Component의 순환과 참조를 어렵게 만든다.

뒤에서도 배우겠지만 대부분 Comnponent의 작성은 Template과 Script 그리고 Style Sheet를 하나의 파일에 작성하는 `단일 파일 컴포넌트(Single File Component)`로 작성하게 된다. 이런 Component에서 `props`, `watch`, `methods` 등의 속성이 무수히 많고 정확한 설계없이 동작만을 목적으로하고 작성한다면 이미 이 컴포넌트 복잡한 구조를 가진 컴포넌트이다. 뿐만아니라 부모-자식의 참조 역시 어려워지게 된다.

가장 중요한 `props`와 `watch`에 대한 이유를 확인해보자.


### props

`props`가 많다는 것은 이미 부모 컴포넌트(Parent Component)에서 많은 속성들을 전달하고 있다는 것이다. 이렇게 된다면 이미 이 컴포넌트는 부모 컴포넌트에 종속된 것이나 다름없는 것이다. 물론 다른 페이지 또는 컴포넌트에서 해당 컴포넌트를 가져가 사용할 수 있겠지만 알겠는가? 여러 페이지에 바인딩 된 컴포넌트에서 실제로 전달된 `props`가 무엇이고 유지 보수 시에 무엇이 필요한지 아닌지를 말이다. 
뿐만 아니라 `props`는 해당 컴포넌트에서 직접적으로 변경이 불가능하기 때문에 이미 넘어온 `props`를 변경하기 위해서는 바인딩 되어 있는 `props`를 `data`에 재 바인딩해야하는 경우가 많다. 이렇게 되면 자연적으로 `watch`와 같은 감시자와 상위 컴포넌트로 이벤트를 전달하는 `$emit`이 많아지게 된다. 


### watch

`watch`가 많다는 것은 이미 해당 컴포넌트에서 반 강제적으로 반응적인 모델이 필요하다는 경우이다. 이런 `watch`가 많아지게 되면 해당 컴포넌트를 다른 곳에 반인딩하였을 때 의도치 않은 동작을 야기할 수 있다. 특히 이런 경우엔 유지보수가 매우 어렵다. 이미 이 `watch`에 종속되어 있는 기능이 거미줄커럼 엉켜있기 때문이다.  


이러한 문제를 해결하기 위해서는 

> props는 해당 컴포넌트에서 절대적으로 필요한 요소로 생성하고 
> watch의 사용을 최소화하고 
> 공통적인 methods와 같은 Script들은 javaScript 파일로 별로 분리하는 것이 좋다.


## 3. 독립적인 컴포넌트로 작성되는 경우가 존재한다

이렇게 무분별하게 컴포넌트를 생성하고 하나의 컴포넌트가 복잡한 구조를 가진 컴포넌트 생성하다보면 결국 해당 컴포넌트는 어느 순간부터 특정 페이지 또는 컴포넌트에 종속되어 버리고 단 하나의 독립적인 컴포넌트가 생성된다. 이렇게 독립적인 컴포넌트가 작성되면 Vue.js 컴포넌트의 목적에 어긋나고 특성을 활용하지 못한 방치되는 컴포넌트가 되고 만다. 


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

이번 포스트에서는 Vue.js의 기본 개념을 익혔다는 가정 하에 Vue.js의 강력한 기능 중인 하나인 `컴포넌트(Component)`에 대해서 알아보자. 먼저 포스팅을 하기 전에 앞써서 기본 `Vue.js`에 대한 개념과 추세를 모르거나 알고 싶다면 [빠르게 배우는 Vue.js](https://kdydesign.github.io/2017/11/15/vuejs-tutorial/) 포스트를 먼저 확인하자.

`Vue.js Component`에 대해서 포스팅 할 내용들은 많지는 않다. 개념부터 사용법까지 본다면 분량은 얼마되지는 않지만 가장 중요하기 때문에 깊게 봐야할 필요성이 있다. 실무에서 특정 프로젝트에 Vue.js를 도입을 한다면 더욱이 깊게 봐야한다. Vue.js Component는 API 문서대로 **전역 등록**을 통한 Component 생성과 **지역 등록**을 통한 컴포넌트 등록이 있고 이 두 형태를 가지고 문법대로 생성하면 끝이다. 하지만 중요한 것은 컴포넌트의 생성 범위이다. 어떤 컴포넌트를 `전역/지역`으로 등록을 할 지, 그리고 어떤 특정 부분을 컴포넌트로 만들어야 할 지가 중요하다. 즉, 쉽게 말한다면 **`설계`** 가 가장 중요하다고 볼 수 있다.

Vue.js Component를 배우고 만들기 앞서 가장 중요한 컴포넌트의 설계를 먼저 보자.

# Vue.js Component 설계의 중요성

위에서 언급했듯이 **컴포넌트를 생성할 때에는 설계가 가장 중요**하다. 컴포넌트를 만드는 방법이야 [Vue.js 공식](https://kr.vuejs.org/v2/guide/components.html) API를 보고 문법을 익혀 만들면 그만이다. 하지만 컴포넌트를 어느 곳에 사용하고 어느 부분이 컴포넌트 화 해야할지에 대해 정확한 설계가 없다면 이 후 전반적으로 문제를 야기한다. 물론 Application을 개발 할 때 모든 항목들을 컴포넌트 단위로 잘게 쪼개도 Application 성능에 크게 영향을 주지는 않지만 규모가 크거나 또는 점점 규모가 커지는(고도화) 프로젝트에서는 해당 프로젝트의 유지관리와 개발 진행 단계에 영향을 준다.

명확한 설계를 무시하고 `Vue.js Component`를 생성했을 때 아래와 같은 문제점들이 있다. 


{% alert danger no-icon %}
1. 전반적인 코드의 가독성과 유지관리 효율성 저하
2. 컴포넌트 구조의 복잡성 증가
3. 독립적인 컴포넌트로의 변이
{% endalert %}


## 1. 전반적인 코드의 가독성과 유지관리 효율성 저하

무분별한 컴포넌트의 생성은 코드의 가독성과 앞으로 있을 유지관리에 대한 효율성을 현저히 저하시킨다. 대부분 특정 부분을 컴포넌트 화를 한다고 했을때 굳이 컴포넌트를 안해도 되는 부분까지 나눠서 컴포넌트 화 하는 경우가 많다. 

아주 간단하게 로그인 페이지를 만든다고 했을 때 ID, Password 입력 폼을 각각의 컴포넌트로 만들었다고 가정하자. 이렇게 되면 메인이 되는 App은 매우 심플해 지겠지만 유지관리시에 우리는 ID, Password 폼을 각각 찾아 다니며 분석하고 수정해야한다.

`로그인 페이지 하나 만드는데 무슨 컴포넌트를 쓰고 가독성과 복잡성을 논하는가` 라고 생각하는가? 그렇다면 이미 설계의 중요성을 알고 있는 것이다. 하지만 당신은 로그인 페이지가 아니라 수십개의 페이지가 존재하는 Application을 구현할 때 이미 알고 있고 느끼는 부분을 망각하고 개발하게 될 수 있다. Application의 전반적인 내용을 알고 있다 하더라도 설계를 무시하고 한다면 당연시하게 되는 일이다. 그만큼 특정 부분을 컴포넌트로 나누고 생성한다는 것은 어려운 일이다.

그렇다면 어떻게해야 가독성이 높은 컴포넌트와 효율성을 올릴 수 있을까? 
먼저 **컴포넌트 화 해야하는 부분을 명확하게 나눠야한다.** A라는 부분이 N개의 페이지에서 사용하는 공통적인 항목이라면 컴포넌트로 분리해야하는 것이 바람직하다. 그리고 **컴포넌트 화 해야하는 덩어리(chunk)를 굳이 세분화해서 나눌 필요는 없다.** 우리는 컴포너트를 작성할 때 과감하게 큰 `덩어리(chunk)` 단위로 나눌 필요도 있다.


## 2. 컴포넌트 구조의 복잡성 증가

뒤에서도 배우겠지만 대부분 컴포넌트의 작성은 `Template`과 `Script` 그리고 `Style Sheet`를 하나의 파일에 작성하는 `단일 파일 컴포넌트(Single File Component)`로 작성하게 된다. 이런 컴포넌트에서 `props`, `watch`, `methods` 등의 속성이 무수히 많고 정확한 설계없이 동작만을 목적으로하고 작성한다면 이미 이 컴포넌트 복잡한 구조를 가진 컴포넌트이다. 뿐만아니라 부모-자식의 참조 역시 어려워지게 된다.

가장 중요한 `props`와 `watch`에 대한 이유를 확인해보자.


### props

`props`가 많다는 것은 이미 부모 컴포넌트(Parent Component)에서 많은 속성들을 전달하고 있다는 것이다. 이렇게 된다면 이미 이 컴포넌트는 특정한 부모 컴포넌트에 종속된 것이나 다름없는 것이다. 물론 다른 페이지 또는 컴포넌트에서 해당 컴포넌트를 가져가 사용할 수 있겠지만 알겠는가? 여러 페이지에 바인딩 된 컴포넌트에서 실제로 전달된 `props`가 무엇이고 유지 보수 시에 무엇이 필요한지 아닌지를 말이다. 
뿐만 아니라 `props`는 해당 컴포넌트에서 직접적으로 변경이 불가능하기 때문에 이미 넘어온 `props`를 변경하기 위해서는 바인딩 되어 있는 `props`를 `data`에 재 바인딩해야하는 경우가 많다. 이렇게 되면 자연적으로 `watch`와 같은 감시자와 상위 컴포넌트로 이벤트를 전달하는 `$emit`이 많아지게 된다. 


### watch

`watch`가 많다는 것은 이미 해당 컴포넌트에서 반 강제적으로 반응적인 모델이 필요하다는 경우이다. 이런 `watch`가 많아지게 되면 해당 컴포넌트를 다른 곳에 반인딩하였을 때 의도치 않은 동작을 야기할 수 있다. 특히 이런 경우엔 유지보수가 매우 어렵다. 이미 이 `watch`에 종속되어 있는 기능이 거미줄럼 엉켜있기 때문이다. 특히나 Vue.js의 반응적모델은 Application의 성능에 직접적인 연관을 주기도하기 때문에 **watch를 최소화**하는 것이 좋다.
Vue.js의 성능 처리에 관련해서 [Vue.js 대용량 데이터의 처리 방법과 성능 최적화 방법 (Vue.js Performance)](https://kdydesign.github.io/2019/04/10/vuejs-performance/)를 참고하자.


위와 같은 컴포넌트의 복잡성 증가를 해결하기 위해서는 

{% alert info no-icon %}
* props는 해당 컴포넌트에서 절대적으로 필요한 요소로 생성하고 
* watch의 사용을 최소화하고 
* 공통적인 methods와 같은 Script들은 javaScript 파일로 별로 분리하는 것이 좋으며
* 컴포넌트 간의 깊은 바인딩(deep)은 자제해야한다.
{% endalert %}


## 3. 독립적인 컴포넌트로의 변이

이렇게 무분별하게 컴포넌트를 생성하고 하나의 컴포넌트가 복잡한 구조를 가진 컴포넌트 생성하다보면 결국 해당 컴포넌트는 어느 순간부터 특정 페이지 또는 컴포넌트에 종속되어 버리고 단 하나의 독립적인 컴포넌트가 생성된다. 이렇게 독립적인 컴포넌트가 작성되면 Vue.js 컴포넌트의 목적에 어긋나고 특성을 활용하지 못한 방치되는 컴포넌트가 되고 만다.


- - -

컴포넌트를 개발하기 전 컴포넌트에서의 설게가 왜 중요한지 알아보았다.
개발에 있어서 설계가 중요하다는 것은 누구나 아는 것이다. 하지만 설계가 Application에 대한 전반적인 설계라고 한다면 나는 **컴포넌트 간의 설계만 별도로 작성하는 것을 추천**한다. 시간이 난다면 컴포넌트 간의 다이어그램도 한번 그려보기 바란다. 많은 도움이 될 것이다. 이 밖에도 설계가 부족할 경우 야기되는 문제들이 많지만 모두 나열할 수는 없어도 분명한 것은 단 하나의 판단 미스로 나비효과를 일으킬 수 있다는 것을 명심하자.

이제 본격적으로 `Vue.js Component` 대해 알아보자.


# Vue.js Component

`Vue.js Component`은 HTML Element를 확장하고 재사용 가능한 형태로 구현하는 것을 말한다. Vue.js에서 사용된 모든 컴포넌트는 하나하나가 Vue.js의 인스턴스이기도 하다. 컴포넌트의 생성 과정은 단순히 **등록 -> 사용** 패턴으로만 이루어 진다.


## 테스트 프로젝트 생성

먼저 테스트 할 프로젝트를 생성하자.

Vue 프로젝트 생성은 `Vue-CLI 3`를 이용하여 생성 할 것이다. `Vue-CLI 3`에 대해서 [Vue-CLI 3 시작하기](https://kdydesign.github.io/2019/04/22/vue-cli3-tutorial/)에서 배워볼 수 있다. `Vue-CLI 3`를 배웠다는 가정하에 진행하겠다.


```
$ vue create vue-component
$ cd vue-component
```

프로젝트가 생성되었으면 기본으로 생성되는 코드들을 정리하자.
`HelloWorld.vue` 파일은 삭제를 하고 `App.vue`는 아래와 같이 초기상태로 돌려놓자.

{% codeblock App.vue lang:html%}
<template>
  <div id="app">
  </div>
</template>

<script>
  export default {
    name: 'app',
    components: {}
  }
</script>
{% endcodeblock %}


## 컴포넌트의 등록과 사용

컴포넌트의 등록에는 `전역등록(Global Registration)`과 `지역등록(Local Registration)`으로 나눌 수 있다.


### 전역등록 (Global Registration)

컴포넌트 전역등록은 프로그래밍에서 전역 변수와 같은 의미이다. 인스턴스 생성 후 어느 페이지 또는 컴포넌트에서 사용할 수 있게 Global 하게 등록 할 수 있다. 

테스트로 생성한 프로젝트에서 `component` 경로에 `global-component.vue` 파일을 만들고 생성하자.

{% codeblock global-component.vue lang:html%}
<template>
  <div>
    <button @click="showTitle">Click</button>
    <span>{{ title }}</span>
  </div>
</template>

<script>
  export default {
    name: 'global-component',
    data () {
      return {
        title: void 0
      }
    },
    methods: {
      showTitle () {
        this.title = 'Global Component!!'
      }
    }
  }
</script>

<style scoped>
  div {
    padding: 20px
  }

  div span {
    margin: 20px
  }
</style>
{% endcodeblock %}

이렇게 전역등록할 컴포넌트를 만들었다. 이제 생성한 컴포넌트를 전역적으로 등록하자. `main.js`를 열어 아래와 같이 작성하자.

{% codeblock main.js lang:javascript%}
import Vue from 'vue'
import App from './App.vue'

Vue.config.productionTip = false

import GlobalComponent from './components/global-component'

Vue.component(GlobalComponent.name, GlobalComponent)

new Vue({
  render: h => h(App),
}).$mount('#app')

{% endcodeblock %}

`Vue.component()`를 통해서 우리는 앞에서 생성한 컴포넌트를 Vue 인스턴스에 바인딩시켰다. 이로써 이제 우리는 템플릿에서 **Custom Element**를 사용할 수 있게 되었다.

`App.vue`에 직접 삽입하고 http://localhost:8080/를 확인해보자.

{% codeblock App.vue lang:html%}
<template>
  <div id="app">
    <global-component></global-component>
  </div>
</template>

<script>
  export default {
    name: 'app'
  }
</script>
{% endcodeblock %}


## 지역등록 (Local Registration)

사실 상 컴포넌트 등록에 있어서 `전역등록` 보다는 `지역등록`을 가장 많이 쓰고 보편적으로 사용한다. 웹팩같은 빌드 시스템을 사용하면 `전역등록` 된 사용되지 않는 모든 컴포넌트가 빌드에 포함되기 떄문이다. 

component 경로에 `local-component.vue` 파일을 생성하자.

{% codeblock local-component.vue lang:html%}
<template>
  <div>
    <button @click="showTitle">Click</button>
    <span>`{`{` title `}`}`</span>
  </div>
</template>

<script>
  export default {
    name: 'local-component',
    data () {
      return {
        title: void 0
      }
    },
    methods: {
      showTitle () {
        this.title = 'Local Component!!'
      }
    }
  }
</script>

<style scoped>
  div {
    padding: 20px
  }

  div span {
    margin: 20px
  }
</style>
{% endcodeblock %}

`전역등록`과는 다르게 생성된 컴포넌트는 사용될 곳에 바로 삽입하여 사용하면 된다. `App.vue`를 아래와 같이 수정 후 삽입하고 http://localhost:8080/를 확인해보자.

{% codeblock App.vue lang:html%}
<template>
  <div id="app">
    <global-component></global-component>
    <local-component></local-component>
  </div>
</template>

<script>
  import LocalComponent from './components/local-component'

  export default {
    name: 'app',
    components: { LocalComponent }
  }
</script>
{% endcodeblock %}

여기까지해서 컴포넌트의 등록 방법과 등록 유형별로 등록된 컴포넌트를 사용하는 방법을 배워봤다. 간단한 예제였지만 사실 여기에는 `컴포넌트의 모듈 시스템`까지 배운 것이다. 모듈 단위의 `단일 파일 컴포넌트 (Single File Component)`를 작성하고 모듈 형태로 삽입까지 했기 때문이다.



---
title: "[Vue.JS] Vuex 개념부터 실무에서의 사용까지 배우기!!"
date: 2019-05-09 23:16:35
tags: 
- vue.js
- vuex
categories :
- javascript
- vue.js
- vuex
- vuex tutorial
- vue.js tutorial
keywords:
- vue.js
- vuex 튜토리얼
- vuex 배우기
- vuex 강좌
- vuex 설치
- vuex 기초
- store
- vuex
- vuex tutorial
- vuex 기초
- state
- mutation
- action
- getter
disqusIdentifier: vuex-initialized-state
clearReading: true
thumbnailImagePosition: left
autoThumbnailImage: yes
metaAlignment: center
coverMeta: out
coverSize: partial
comments: true
meta: true
action: true
---

<!-- more -->
이번 포스팅에서는 Vuex의 개념을 살펴보고 간단한 예제를 통하여 실무에 어떻게 적용을 하는지 알아보도록 하자. Vuex 설치부터 사용까지 한방에 배우기!!
<!-- more -->

<!-- excerpt -->
<!-- excerpt -->

![vuex](cover.png)

이번 포스팅에서는 Vuex의 개념을 살펴보고 설치부터 실무에서의 사용 방법까지 예제를 통하여 알아보도록 하자. Vuex는 작성 방법에 따라 형태가 조금씩 다르며 [공식 API](https://vuex.vuejs.org/) 를 통해서만은 실무에 반영하기가 어렵다.

당신이 처음 Vuex를 사용한다면 도움이 되기를 바란다.


# Vuex 개념

`Vuex`는 **Vue.js의 상태관리 라이브러리**로 애플리케이션의 모든 컴포넌트에 대한 중앙 집중식 저장소 역할을 하며 의도적인 방법으로 상태를 변경 및 관리할 수 있다. Vuex는 기존 **Flux의 아키텍처**를 따라가고 있고 React로 본다면 `Redux`와 비교 대상으로 볼 수 있다. Vue.js에서도 Redux를 사용할 수 있지만 Vue.js는 Vuex와의 호환이 좋을 뿐만 아니라 더 직관적으로 개발할 수 있다.

[[Vue.JS] Component 개념을 익히고 만들어보자!!](https://kdydesign.github.io/2019/04/27/vue-component/) 에서 언급하였듯이 컴포넌트는 일반적으로 `부모-자식`의 관계를 가지고 `props`와 `event`를 통해 서로의 데이터를 주고받는다고 하였다. 하지만 Vuex는 말 그대로 **중앙 집중식 저장소** 이기 때문에 `props`와 `event`에 얽매이지 않아도 된다. 그렇기 때문에 컴포넌트의 구조가 복잡한 경우에는 `props`와 `event`를 통한 데이터 전달보다는 Vuex를 통해 별도의 저장소에서 데이터를 관리하는 것이 올바르다.

대부분 Vuex의 채택은 필수로 보고 있지만, 규모가 작은 애플리케이션의 경우 **Event Bus**를 사용해도 무방하다. 하지만 Event Bus의 규모가 커지면 관리 포인트가 매우 어려워지므로 Vuex를 사용하는 것을 추천한다.

Vuex를 이해하고 바로 도입하기에는 비용이 많이 드는 편이다. 또한 [[Vue.JS] Component 개념을 익히고 만들어보자!!](https://kdydesign.github.io/2019/04/27/vue-component/) 에서 언급한 **컴포넌트 설계의 중요성보다 더욱 설계가 중요시된다.** 컴포넌트와는 다르게 Vuex는 어느 한 곳에 종속되지 않고 중앙에서 관리 되므로 모든 컴포넌트가 읽기/쓰기가 가능하기 때문이다.


# Vuex 구조

Vuex는 `state`, `mutations`, `action`, `getters` 4가지 형태로 관리가 되며, 이때 이 관리 포인트는 **store 패턴**을 사용하고 통상 **store**라고 불린다. 이 4가지는 서로간의 간접적으로 영향이 있으며 단방향 데이터 흐름으로 볼수 있다.


## State

State는 Vue 컴포넌트에서 data로 볼 수 있다. **원본 소스의 역할을 하며, View와 직접적으로 연결되어있는 Model이다.** 이 state는 직접적인 변경은 불가능하고 mutation을 통해서만 변경이 가능하다. mutation을 통해 state가 변경이 일어나면 반응적으로 View가 업데이트된다.


## Mutations

Mutation은 **state를 변경하는 유일한 방법이고 이벤트와 유사하다.** mutation은 함수로 구현되며 첫 번째 인자는 `state`를 받을 수 있으며, 두 번째 인자는 `payload`를 받을 수 있다. 여기서 payload는 여러 필드를 포함할 수 있는 객체형태도 가능하다. 이 mutation은 일반적으로(Helper를 쓰지 않는 경우)는 직접 호출을 할 수 없으며, **commit**을 통해서만 호출할 수 있다.

*대부분 실무에서는 mutations에서는 API를 통해 전달받은 데이터의 가공하여 state를 설정하는 데 많이 사용된다.*

{% codeblock Mutations lang:javascript %}
store.commit('setData', payload)
{% endcodeblock %}


## Actions

Action은 mutation과 비슷하지만 mutation과는 달리 **비동기 작업이 가능하다.** 또한 mutation에 대한 `commit`이 가능하여 action에서도 mutation을 통해 state를 변경할 수 있다. action에서는 첫 번째 인자를 `context` 인자로 받을 수 있으며 이 context에는 `state`, `commit`, `dispatch`, `rootstate`와 같은 속성들을 포함한다. 두 번째 인자는 mutation과 동일하게 payload로 받을 수 있다.

commit을 통해 mutation을 호출했다면 Action은 `dispatch`를 통해서 호출한다. context의 속성을 보면 dispatch가 있는 것으로 보아 action에서는 서로 다른 action을 호출할 수 있다는 것을 볼 수 있다.

*실무에서 action은 Axios를 통한 API 호출과 그 결과에 대해서 반환(return)을 하거나 mutation으로 commit하여 상태를 변경하는 용도로 사용된다.*

{% codeblock Actions lang:javascript %}
store.dispatch('setData', payload)
{% endcodeblock %}


## Getters

Getters는 쉽게 **Vue 컴포넌트에서 Computed로 볼 수 있다.** 말로 풀자면 계산된 속성인데 getter의 결과는 종속성에 따라 캐시 되고 일부 종속성이 변경된 경우에만 다시 재계산된다. 즉, 특정 state에 대해 어떠한 연산을 하고 그 결과를 View에 바인딩할 수 있으며, state의 변경 여부에 따라 getter는 재계산이 되고 View 역시 업데이트를 일으킨다. 이때 state는 원본 데이터로서 변경이 일어나지 않는다.

*실무에서도 state의 연산 처리가 필요한 내용에 대해 getter를 사용하지만 getters의 경우 대용량 처리 시에 퍼포먼스와 연관이 되어있으므로 조심해야 한다. 대용량 처리에 관련해서는
[[Vue.JS] 대용량 데이터의 처리 방법과 성능 최적화 방법 (Vue.js Performance)](https://kdydesign.github.io/2019/04/10/vuejs-performance/) 를 참고하자.*

- - -

여기까지 해서 Vuex에 대한 개념을 알아보았다. Vuex의 주요 핵심은 **중앙 집중식 저장소**이며 이에 따라 `state`, `action`, `mutations`, `getters`의 개념과 흐름만 파악하면 무리 없이 진행할 수 있을 것이다.


# Vuex 설치

이제 Vuex를 설치해 보고 `state`, `mutations`, `actions`, `getters` 4가지의 형태별로 사용하는 방법을 알아보도록 하자.

이미 테스트용 프로젝트가 준비되어 있다면 **NPM을 통해 바로 설치**를 할 수 있고 아직 준비가 안되었다면 **Vue-CLI 3를 통한 Vuex 설치법**을 보자.

## NPM을 통한 Vuex 설치
Vuex의 설치는 npm으로 진행하도록 하자. npm에 대해서는 [빠르게 배우는 Node.js와 NPM 설치부터 개념 잡기](https://kdydesign.github.io/2017/07/15/nodejs-npm-tutorial/)를 참고하자.

```
$ npm i vuex --save
```

{% codeblock main.js lang:javascript %}
import Vue from 'vue'
import Vuex from 'vuex'

Vue.use(Vuex)
{% endcodeblock %}

개념을 설명 할 때 action이 비동기 처리가 가능하다고 하였다. Promise를 IE 브라우저에서 사용하기 위해서는 Vuex는 **polyfill 라이브러리**가 필요하기 때문에 IE 브라우저를 사용한다면 `es6-promise` polyfill을 설치하도록 하자.

```
$ npm i es6-promise --save
```

{% codeblock main.js lang:javascript %}
import 'es6-promise/auto'
{% endcodeblock %}


## Vue-CLI 3를 통한 Vuex 설치

Vue에 대한 프로젝트가 이미 설치되어있다면 NPM 설치와 같이 Vuex만 개별로 설치할 수 있지만 우리는 **Vue-CLI를 통해 한 번에 해결**할 수 있다. `Vue-CLI 3`에 대해서는 [[Vue.JS] Vue-CLI 3 시작하기](https://kdydesign.github.io/2019/04/22/vue-cli3-tutorial/)를 참고하자.

Vue-CLI가 설치되었다는 가정하에 설명하자면.

```
$ vue create vuex-poject
```

CLI를 통해 Vue 프로젝트를 생성할 때 `Manually select features`를 통해서 Vuex를 설치하자. 설치 후 `package.json`과 `main.js`를 확인해 보면 이미 Vuex가 설치와 바인딩 된 것을 확인할 수 있고 `store.js`가 생성된 것을 확인할 수 있다.

이제 실행해보자.

```
$ npm run serve
```

기본 페이지가 http://localhost:8080으로 실행이 될 것이다. 세부 내용을 시작하기 전에 간단하게 Vuex를 사용해 보자.


# Vuex 전체적인 Flow 예제

먼저 App.vue 파일과 store.js 파일을 아래와 같이 수정하자.


{% codeblock App.vue lang:html %}
<template>
  <div id="app">
    <div>
      <label>{{getMsg}}</label>

      <br/>

      <button @click="onChangedMsg">Click</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'app',
  computed: {
    getMsg () {
      return this.$store.getters.getMsg
    }
  },
  methods: {
    onChangedMsg () {
      this.$store.dispatch('callMutation', { newMsg: 'World !!' })
    }
  }
}
</script>
{% endcodeblock %}

{% codeblock store.js lang:javascript %}
import Vue from 'vue'
import Vuex from 'vuex'

Vue.use(Vuex)

export default new Vuex.Store({
  state: {
    message: 'Hello'
  },
  mutations: {
    changeMessage (state, newMsg) {
      state.message = newMsg
    }

  },
  actions: {
    callMutation ({ state, commit }, { newMsg }) {
      commit('changeMessage', newMsg)
    }
  },
  getters: {
    getMsg (state) {
      return `${state.message} => Length : ${state.message.length}`
    }
  }
})
{% endcodeblock %}

결과는 최초 Hello라는 단어와 해당 단어의 길이를 나타낸다. 그리고 버튼을 클릭 시 단어가 바뀌고 바뀐 단어에 대한 길이가 나온다.

먼저 `store.js`를 보자. 

**state**에는 `message`라는 상태를 저장할 모델을 생성하고 기본값으로 Hello라는 단어를 지정하였다. 하지만 이 state를 View에 바인딩하진 않았다. 만약 바인딩하였다면 문자의 길이는 나오지 않았을 것이다.

**getters**를 보자. `getMsg`라는 getter를 생성하고 state와 추가로 단어의 길이를 나타내는 문장을 더해서 반환해주고 있다. 반환된 값은 `App.vue`에서 `getMsg()`의 computed로 바인딩 되어있다. 이 코드를 보게 되면 컴포넌트에서 **this.$store.getters.getMsg**를 통해 getter를 바인딩하는 것을 볼 수 있다. 여기서 state의 message가 변경되면 View 역시 업데이트가 된다.

**actions**를 보자. action에는 `callMutation()`이라는 함수가 정의되어 있고 newMsg라는 payload를 받고 있다. 최초 이 `callMutation()`은 `App.vue`에서 Click Event가 수행되고 실행되는 `onChangedMsg()`에서 **this.$store.dispatch('callMutation', { newMsg: 'World !!' })**를 통해 호출하고 있다. actions를 호출하게 되면 `callMutation()`에서는 받은 payload와 함께 바로 `commit`을 통해서 mutations의 `changeMessage()`를 호출하고 있다.

**mutations**에서는 전달받은 payload를 state인 `message`에 설정하고 있다. 이렇게 message가 설정되면 다시 getter가 이를 감지하고 수행하게 되고 View가 업데이트되는 과정을 거친다.

- - - 

Vue와 Vuex의 한 싸이클을 간략하게 예제로 보았다. 대부분의 패턴은 위처럼 사용하며 가장 기본이 되는 방식이다.


# Store의 모듈화

지금의 예제는 `store.js`라는 store를 하나만 사용하고 있지만 실상 **실무에서는 단 하나의 store를 사용할 수는 없다.** 기능별 또는 페이지별로 store를 분리해야 하고 관리해야 한다. 이렇게 관리하기 위해서는 store를 모듈별로 분리를 해야 한다.

모듈별로 분리하는 형태는 두 가지로 분리된다.

{% alert info no-icon %}
* state, mutations, actions, getters를 script 파일 단위로 분리
* 기능/페이지별로 store를 분리하고, 하나의 store에는 state, mutations, actions, getters를 포함
{% endalert %}


어느 형태로 분리할지는 프로젝트의 규모와 구조에 따라 다르기 때문에 본인이 판단하길 바란다. 여기서는 store 별로 분리하는 방법으로 설명을 하겠다.

먼저 현재 샘플 프로젝트의 src 경로에 `store`라는 폴더를 생성하자. 그리고 그 하위에 `book` 폴더를 생성하자. 그다음 'user' 폴더 하위에 'book.js'와 'bookList.js'를 생성하자.

여기까지 진행한다면 store의 모듈 구조를 생성한 것이다. **폴더 트리의 path가 이후 store 모듈을 불러올 경로가 된다.** 

이제 기존에 있던 store.js는 삭제를 하고 store 폴더 안에 `index.js`를 생성하자.

{% codeblock store/index.js lang:javascript %}
import Vue from 'vue'
import Vuex from 'vuex'

import BookStore from './book'

Vue.use(Vuex)

export default new Vuex.Store({
    modules: {
        book: BookStore
    }
})
{% endcodeblock %}

위 코드는 기존에 존재하던 store.js에서 하는 역할을 한다. 다른 게 있다면 `book`이라는 모듈을 불러와 store에 바인딩하고 있다는 것이다.

이제 실제로 store가 될 파일 수정하자. `book.js`를 열어 아래와 같이 정의하자.

{% codeblock store/book/book.js lang:javascript %}
// state
const state = {
    message: 'Hello'
}

// mutations
const mutations = {
     changeMessage (state, newMsg) {
      state.message = newMsg
    }
}

// actions
const actions = {
    callMutation ({ state, commit }, { newMsg }) {
      commit('changeMessage', newMsg)
    }
}

// getters
const getters = {
    getMsg (state) {
      return `${state.message} => Length : ${state.message.length}`
    }
}

export default {
  state,
  mutations,
  actions,
  getters
}
{% endcodeblock %}

코드는 초기에 만들었던 `store.js`에 있는 내용이다. 이렇게 정의를 하면 `book`이라는 하나의 모듈이 생성되었다.


# Vuex Binding Helper

위처럼 모듈을 생성하고 컴포넌트에 바인딩을 하기 위해서는 아래와 같이 사용해야 한다.

{% codeblock state binding lang:javascript %}
this.$store.state.book.message
{% endcodeblock %}

모듈을 생성하고 Vuex.Store에 바인딩할 때 우리는 `book`이라는 명칭을 주었기 때문에 `book`에 있는 state에 접근하기 위해서는 그에 맞는 속성값을 명시해줘야 한다. 하지만 만약 store의 구조가 깊고 복잡한 구조라면 state 하나를 바인딩하기 위해서는 길고도 긴 값을 코딩해야한다. 이런 이유로 인해서 **Vuex에는 Helper라는 Util이 존재한다.**

Helper는 `state`, `mutations`, `actions`, `getters` 별로 각각 `mapState`, `mapActions`, `mapMutations`, `mapGetters`가 존재하고 아래처럼 바인딩할 수 있다.

{% codeblock Sample.vue lang:javascript %}
import { mapState, mapActions, mapMutations, mapGetters } from 'vuex'

export default {
  name: 'Sample',
  computed: {
    ...mapState('book', {
        message: state => state.message     // -> this.message
    }),
    ...mapGetters('book', [
       'getMsg'       // -> this.getMsg
    ])
  },
  methods: {
    ...mapMutations('book', [
        'changeMessage'     // -> this.changeMessage()
    ]),
    ...mapActions('book', [
        'callMutation'      // -> this.callMutation()
    ])
  }
}
{% endcodeblock %}

Helper를 사용하게 되면 코드의 가독성이 훨씬 좋아진다. 하지만 우리가 최종적으로 배울 것은 이러한 방법이 아니다.


## Vuex createNamespacedHelpers

충분히 위에서 배운 `mapHelper`를 통해 개발이 가능하지만 좀 더 편리하고 효율적으로 하기 위해서는 **createNamespacedHelpers**를 사용하는 것이 좋다. 어떻게 보면 결과적으로나 사용되는 Util은 동일하다.

아래 코드를 보자.


{% codeblock Sample.vue lang:javascript %}
import { createNamespacedHelpers } from 'vuex'

const bookHelper = createNamespacedHelpers('book')

export default {
  name: 'Sample',
  computed: {
    ...bookHelper.mapState({
        message: state => state.message     // -> this.message
    }),
    ...bookHelper.mapGetters([
       'getMsg'       // -> this.getMsg
    ])
  },
  methods: {
    ...bookHelper.mapMutations([
        'changeMessage'     // -> this.changeMessage()
    ]),
    ...bookHelper.mapActions([
        'callMutation'      // -> this.callMutation()
    ])
  }
}
{% endcodeblock %}

처음에 설명한 Helper와 다른 것은 `createNamespacedHelpers`를 통해서 모듈의 경로를 미리 지정했다는 것이다. 코드의 차이는 별것이 없겠지만 실제로 하나의 컴포넌트에 여러 개의 모듈을 바인딩하면 `createNamespacedHelpers`를 사용하는 것이 효율적으로 볼 수 있다.

{% codeblock Sample.vue lang:javascript %}
import { createNamespacedHelpers } from 'vuex'

const 
    bookHelper = createNamespacedHelpers('book'),
    bookListHelper = createNamespacedHelpers('bookList')

export default {
  name: 'Sample',
  computed: {
    ...bookHelper.mapState({
        message: state => state.message     // -> this.message
    }),
    ...bookHelper.mapGetters([
       'getMsg'       // -> this.getMsg
    ]),
    ..bookListHelper.mapState({
        messageList: state => state.messageList     // -> this.messageList
    }),
    ...bookListHelper.mapGetters([
       'getMsgList'       // -> this.getMsgList
    ])
  },
  methods: {
    ...bookHelper.mapMutations([
        'changeMessage'     // -> this.changeMessage()
    ]),
    ...bookHelper.mapActions([
        'callMutation'      // -> this.callMutation()
    ]),
    ...bookListHelper.mapMutations([
        'changeMessageList'     // -> this.changeMessageList()
    ]),
    ...bookListHelper.mapActions([
        'callMutationList'      // -> this.callMutationList()
    ]),
  }
}
{% endcodeblock %}

지금까지 언급한 방법이 최고의 방법은 아니다. store를 바인딩하는 방법은 개발자의 스타일이 많이 반영된다. 여러 가지의 형태로 개발을 해보고 본인의 스타일에 맞는 방법을 찾는 게 좋다. Vuex Sotre의 바인딩의 다양한 방법은 [[Vue.JS] Vuex Store를 바인딩하는 4가지 방법!!](https://kdydesign.github.io/2019/04/06/vuejs-vuex-helper/)을 참고하자.

- - -

여기까지 해서 우리는 Vuex의 개념과 설치 그리고 실무에서 사용하는 방법을 알아보았다.
Vuex의 Store 패턴은 한번 잡아 놓으면 변경할 일이 별로 없기 때문에 처음에 진입장벽만 넘어선다면 수월한 부분이 많다. 다만 모듈의 구조화, 그리고 store의 설계가 잘못된다면 오히려 Vuex는 독이 될 수 있다. 이 부분만 조심하면 컴포넌트 간의 데이터 흐름은 확실하게 제어할 수 있을 것이다.


- - -

더 알아보기
> [빠르게 배우는 Vue.js](https://kdydesign.github.io/2017/11/15/vuejs-tutorial/)
> [Vue-CLI 3 시작하기](https://kdydesign.github.io/2019/04/22/vue-cli3-tutorial/)
> [Vue.js 대용량 데이터의 처리 방법과 성능 최적화 방법 (Vue.js Performance)](https://kdydesign.github.io/2019/04/10/vuejs-performance/)
> [Vue.js의 Vuex Store를 바인딩하는 4가지 방법!!](https://kdydesign.github.io/2019/04/06/vuejs-vuex-helper/)
> [Vuex Store의 state를 효율적으로 초기화하기](http://localhost:4000/2019/05/09/vue-store-state/)
> [[Vue.JS] Component 개념을 익히고 만들어보자!!](http://localhost:4000/2019/04/27/vue-component/)
> [Nuxt.js 개념부터 설치까지 빠르게 배우기](https://kdydesign.github.io/2019/04/10/nuxtjs-tutorial/)

---
title: "[Vue.JS] Vuex Store의 state를 효율적으로 초기화하기"
tags: 
- vue.js
- vuex
categories :
- javascript
- vue.js
- nuxt.js
- vuex
- vuex tutorial
- vue.js tutorial
- nuxt.js tutorial
keywords:
- javascript
- nuxt.js
- vue.js
- vue 튜토리얼
- vuejs 튜토리얼
- vuejs 강좌
- vuejs 설치
- nuxtjs
- vue 기초
- store
- vuex
- vue.js tutorial
- nuxt.js tutorial
- vue 배우기
- vuejs 배우기
- vuex 배우기
- vuex 기초
- vuex state
- store state 초기화
- state 초기화
disqusIdentifier: vuex-initialized-state
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
Vue.js의 상태 관리 패턴인 Vuex에서 Store의 state를 초기화하는 방법에 대해 알아보자. Vuex Store에서 state는 원본 데이터 즉, 모델의 역할을 하며 mutation에 의해 변경이 가능하다. state는 최초에 명시되어 있어야 하며, 때로는 기본값을 가지고 있다. 이때 state를 초기화하는 방법이 있어야만 좀 더 효율적인 상태 관리를 진행할 수 있다.
<!-- more -->

<!-- excerpt -->
<!-- excerpt -->

![vue-tutorial](cover.png)

Vue.js의 상태 관리 패턴인 Vuex에서 Store의 state를 초기화하는 방법에 대해 알아보자. Vuex Store에서 state는 원본 데이터 즉, 모델의 역할을 하며 `mutation`에 의해 변경이 가능하다. state는 최초에 명시되어 있어야 하며, 때로는 기본값을 가지고 있다. 이러한 state를 mutation에 의해 변경을 하고 이후 어떠한 작업을 하더라도 초기화되지 않는다. 그렇기 때문에 해당 stat를 다시 사용한다면 이전 값이 남아있다. 그렇기 때문에 state의 초기화는 필수적이다. 

이번 포스트에서는 **state를 초기화하는 효율적인 방법**에 대해 알아보자.


# state의 효율적인 선언과 초기화 
당연한 말이지만 state의 초기화는 mutation에 의해서 초기값을 지정해주면 끝이다. 물론 이러한 방법을 공유하려는 것은 아니다. 더욱 효율적이고 가독성이 좋은 코드 스타일을 설명을 하려 한다. 

먼저 아래 코드를 보자.

{% codeblock lang:javascript%}
// state
const state = {
  userList: [],
  isFlag: false,
  userData: {
    id: void 0,
    password: void 0,
    name: void 0,
    age: 30,
    job: 'programmer'
  },
  companyData: {
    name: 'company',
    address: void 0,
    job: void 0
  }
}

// mutations
const mutations = {
  initData (state) {
    state.userList = []
    state.isFlag = false
    state.userData = {
      id: void 0,
      password: void 0,
      name: void 0,
      age: 30,
      job: 'programmer'
    }
    state.companyData =  {
      name: 'company',
      address: void 0,
      job: void 0
    }
  }
}

export {
  state,
  mutations
}
{% endcodeblock %}

별다를 것 없는 기본적인 state이고 이 state를 초기화하는 `initData`이라는 mutataion이다. 이러한 방법은 가장 기본적이고 이렇게 밖에 할 수 없을 것이다. 하지만 여기서 `userData`와 `companyData`를 보자. 다른 state와는 다르게 `object`형태를 가지고 있다. 보통 이런 state는 단일로 설정하고 사용하는 경우가 많다. 예를 들면 아래와 같다.

{% codeblock lang:javascript %}
// mutations
const mutations = {
  setUserData (state, payload) {
    state.userData.id = payload.id
    state.userData.password = payload.password
    state.userData.name = payload.name
    state.userData.age = payload.age
    state.userData.job = payload.job

    // or
    // state.userData = {...payload}
  },

  setCompanyData (state, payload) {
    state.companyData.name = payload.name
    state.companyData.address = payload.address
    state.companyData.job = payload.job

    // or
    // state.companyData = {...payload}
  }
}
{% endcodeblock %}

이렇게 같은 레벨의 state지만 독립적으로 별도로 사용되는 경우가 많은데 이런 경우엔 별개로 초기화해야 하는 경우가 생긴다. 초기화 시에 `initData`와 같은 방식으로 해도 무방하지만 `userData`와 `companyData`의 속성들이 수십 개라면 수없이 초기화 코드가 길어진다. 그렇게 되면 초기화 mutation 하나로 store의 코드 가독성이 현저히 떨어지게 된다. 특히 `userData`와 `companyData` 같은 state는 주기적으로 초기화해야 하기 때문에 효율적인 코드가 필요하다. 

이런 경우를 대비하여 `userData`와 `companyData`는 애초부터 state에 명시를 할 경우 별도의 **함수로 분리**해 주는 것이 좋다. 

아래 코드를 보자.

{% codeblock lang:javascript %}
// initialized userData
const USER_DATA = () => {
  return {
    id: void 0,
    password: void 0,
    name: void 0,
    age: 30,
    job: 'programmer'
  }
} 

// initialized companyData
const COMPANY_DATA = () => {
  return {
    name: 'company',
    address: void 0,
    job: void 0
  }
} 

// state
const state = {
  userList: [],
  isFlag: false,
  userData: USER_DATA(),
  companyData: COMPANY_DATA()
}

// mutations
const mutations = {
  initData (state) {
    state.userList = []
    state.isFlag = false
    state.userData = USER_DATA()
    state.companyData = COMPANY_DATA()
  }
}

export {
  state,
  mutations
}
{% endcodeblock %}

위 코드를 보면 `userData`와 `companyData`는 객체 상수 형태의 함수로 미리 선언을 하고 state에 해당 함수를 대입하여 초기화하고 있다. 물론 `initData`에서 다시 초기화 시에 이미 선언된 함수를 통해 초기화를 한다. 앞으로 `userData`와 `companyData`를 초기화할 땐 이미 정의된 함수를 쓰면 그만인 것이다. 이런 구조는 특히나 객체 안에 객체를 가진 복잡한 형태의 state를 정의하거나 초기화할 때 효율적이고 가독성도 좋아진다. 우리는 초기화 코드에 신경을 쓸 필요가 없다. 또한 특정 조건에 따른 초기화라면 이미 정의해 놓은 초기화 코드는 함수로 선언되어있기 때문에 인자를 받아 처리할 수 도 있다. 

- - - 

state를 초기화하는 것은 사실 중요한 부분은 아니다. 초기화하는 것에 문제가 될게 무엇인가. 하지만 대부분 vuex의 store는 모듈별로 선언하게 되고 그 안에는 무수히 많은 state, mutations, actions가 포함된다.(물론 state, mutation, action을 분리할 수도 있다.) 이런 상황에서 작은 단위 하나하나를 지나치지 않고 효율적으로 처리한다면 더 나은 Application을 개발할 수 있을 것이다.

---

더 알아보기
> [빠르게 배우는 Vue.js](https://kdydesign.github.io/2017/11/15/vuejs-tutorial/)
> [Vue-CLI 3 시작하기](https://kdydesign.github.io/2019/04/22/vue-cli3-tutorial/)
> [Vue.js 대용량 데이터의 처리 방법과 성능 최적화 방법 (Vue.js Performance)](https://kdydesign.github.io/2019/04/10/vuejs-performance/)
> [Vue.js의 Vuex Store를 바인딩하는 4가지 방법!!](https://kdydesign.github.io/2019/04/06/vuejs-vuex-helper/)
> [Nuxt.js 개념부터 설치까지 빠르게 배우기](https://kdydesign.github.io/2019/04/10/nuxtjs-tutorial/)

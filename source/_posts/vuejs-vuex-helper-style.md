---
title: "[Vue.js Tutorial] Vuex Store를 바인딩하는 4가지 방법!!"
date: 2019-04-06 17:09:57
tags: 
- vue.js
- vuex
- vuex component binding
- store
- vue.js tutorial
categories :
- javascript
- vue.js
- vue.js tutorial
- vuex tutorial
- vuex helper
keywords:
- javascript
- nuxt.js
- vue.js
- vue.js tutorial
- nuxt.js tutorial
- vuex
disqusIdentifier: vuex-helper-style
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
Vuex Store 패턴에서 컴포넌트에 Store를 바인딩 시키는 여러가지 방법을 알아보자.
<!-- more -->

<!-- excerpt -->
<!-- excerpt -->


![cover](cover.png)

해당 포스트에서는 Vuex의 설명과 사용법에 대해서는 언급하지 않았으며, 오로지 Vuex Store를 컴포넌트에 바인딩하는 방법을 설명한다.

프로젝트의 규모가 크거나 작든 `Vuex를 사용할 때는 Store를 Module 별로 분리`하는 것이 바람직하다. 그렇지 않으면 각 컴포넌트마다 바인딩 된 Store의 state들이 다른 컴포넌트의 루틴에 의해 오염될 가능성과 코드의 복잡성이 높아지게 되어 있다. 

이번 포스트에서는 모듈별로 분리된 Store를 각 컴포넌트에서 효율적으로 바인딩시키는 여러 가지 방법들과 코드 스타일을 알아보자.


# Basic

Vue 공식 API에서는 명시된 기본 Store 바인딩 방법이다.

```javascript
import {mapState} from 'vuex'

new Vue({
    computed: mapState({
        count: state => state.count,
        countAlias: 'count'
    })
})
```

위 내용은 `mapState`라는 Helper를 이용하여 객체의 형태로 `count`를 바인딩 한 형태이고 아래처럼 state의 이름을 그대로 상속받아 정의할 수도 있다.

```javascript
import {mapState} from 'vuex'

new Vue({
    computed: mapState([
        'count'
    ])
})
```

기본적인 바인딩 방법은 가장 단순한 구조를 가진 Store를 바인딩하였을 때이다. 하지만 Store가 여러 모듈별로 분리되어 있고 하나의 컴포넌트에서는 여러 Store 모듈을 바인딩해야 한다면 매우 복잡해질 것이다.

아래 가정을 가지고 각 바인딩 Style을 살펴보자.

{% alert danger no-icon %}
각각 **User**, **Book** 이라는 Store 모듈이 존재하고, **User**는 `A/B` 경로에 있으며, **Book**은 `A/B/C` 경로에 위치한다.
{% endalert %}

프로젝트 구조는 다음과 같다.

{% alert info no-icon %}
A
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|- B
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|- user
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|- C
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;|- Book
{% endalert %}


# Style 1 - Vuex Helper

```javascript
import {mapState, mapActions} from 'vuex'

new Vue({
    computed: {
        ... mapState({
            bookList: state => state.A.B.C.Book.list
        })
    },
    methods: {
        ...mapActions([
            'A/B/C/Book/setList'
        ])
    }
})
```

또는

```javascript
import {mapState} from 'vuex'

new Vue({
    computed: {
        ... mapState('A/B/C/Book', {
            bookList: state => state.list
        })
    },
     methods: {
        ...mapActions('A/B/C/Book', [
            'setList'
        ])
    }
})
```

특정 경로에 포함된 Store 모듈을 사용하기 위해서는 해당 경로를 모두 명시해줘야 한다. 이렇게 사용을 한다면 어느 경로에 있든 서로 다른 Store 모듈을 하나의 컴포넌트 또는 여러 컴포넌트에서 바인딩하여 사용이 가능하다. 하지만 위 예제에서 A/B/C의 단순하고 짧은 명칭이지만 폴더나 Store 모듈의 명칭이 꽤나 길다면 역시나 가독성이 좀 떨어질 것이다. 그래서 우리는 Vuex에서 제공하는 Namespace Helper를 생성할 수 있는 `createNamespacedHelpers` 이용하여 바인딩하는 것을 가장 인상적으로 볼 수 있다.


# Style 2 - createNamespacedHelpers 1

```javascript
import {createNamespacedHelpers} from 'vuex'

const {mapState} = createNamespacedHelpers('A/B/C/Book')

new Vue({
    computed: {
        ... mapState({
            bookList: state => state.list
        })
    }
})
```

또는

```javascript
import {createNamespacedHelpers} from 'vuex'

const {mapState} = createNamespacedHelpers('A/B/C/Book')

new Vue({
    computed: {
        ... mapState([
            'list'
        ])
    }
})
```

모듈의 이름이 길고 구조가 복잡하다면 `createNamespacedHelpers`를 사용하여 바인딩한다면 computed 또는 methods가 간결하고 뛰어난 가독성을 보이는 것을 알 수 있다.

Store 모듈들의 경로를 computed와 methods에 정의를 안 했을 뿐이지 무엇이 다르겠냐고 한다면 생각해보자. 우리는 개발을 하면서 코드를 살펴볼 때나 구현을 할 때 가장 상단에 삽입하거나 명시해 놓은 구현체는 자주 보지 않는다. 오히려 data, computed, methods를 가장 많이 볼 것이다. 이러한 상황에서 수많은 모듈의 경로가 명시되어 있다면 state나 mutation, action의 개체들을 찾기 어려울 것이다.


# Style 3 - createNamespacedHelpers 2

그러면 여기서 좀 더 깊이 한번 보자.

만약 `createNamespacedHelpers를` 사용을 한다고 하지만 만약 하나의 컴포넌트에 서로 다른 경로에 있는 Store 모듈을 여러 개 바인딩할 경우에는 어떻게 해야 할까? 
지금까지 `Book`이라는 모듈만을 가지고 예제를 보았지만, 여기에서 `User` 모듈을 추가해보자.

```javascript
import {createNamespacedHelpers} from 'vuex'

const
    {mapState: userMapState, mapActions: userMapActions} = createNamespacedHelpers('A/B/User'),
    {mapState: bookMapState, mapActions: bookMapActions} = createNamespacedHelpers('A/B/C/Book')

new Vue({
    computed: {
        ... userMapState({
            userList: state => state.user.userList
        }),
        ... bookMapState([
            'list'
        ])
    },
    methods: {
        ...userMapActions({
            setUserList: 'setUserList'
        }),
        ...bookMapActions([
            'setBookList'
        ])
    }
})
```

아래처럼 정의도 가능하다.

```javascript
import {createNamespacedHelpers} from 'vuex'

const
    userListHelper = createNamespacedHelpers('A/B/User'),
    bookListHelper = createNamespacedHelpers('A/B/C/Book')

new Vue({
    computed: {
        ... userListHelper.mapState({
            userList: state => state.user.userList
        }),
        ... bookListHelper.mapState([
            'list'
        ])
    },
    methods: {
        ...userListHelper.mapActions({
            setUserList: 'setUserList'
        }),
        ...bookListHelper.mapActions([
            'setBookList'
        ])
    }
})
```

이렇게 한다면 하나의 컴포넌트에서도 많은 모듈을 바인딩하기가 쉬우며, 코드의 가독성 역시 좋아진다.

- - -

각 개발자마다 코드 스타일은 모두 다르고 해당 포스트에 언급한 내용 이외에 더 좋은 방법이 있을 수 있다. 다만 중요한 것은 개발하기 전 또는 하면서 어느 방법이 가장 좋은지 몸소 느끼며 차근차근 수정해 나아가는 것이 중요하다고 본다. 어느 스타일이든 결과는 같겠지만 업무/개발의 속도는 확연히 차이가 날 것이다.

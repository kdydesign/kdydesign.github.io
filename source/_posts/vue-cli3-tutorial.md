---
title: "Vue-CLI 3 배우기"
date: 2019-04-22 12:22:06
tags: 
- npm
- nodejs
- javscript
- electron
- nuxt.js
- vue.js
- vue cli
categories :
- javascript
- nodejs
- npm
- vue.js
- vue cli
keywords:
- javascript
- nodejs
- npm
- npm tutorial
- nodejs tutorial
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
disqusIdentifier: vueCli3Tutorial
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
Vue CLI 3는 Vue.js 개발을 위한 시스템으로 Vue.js Core에서 공식으로 제공하는 CLI이다. Vue CLI는 애플리케이션 개발에 집중할 수 있도록 프로젝트의 구성을 도와주는 역할을 하며, Vue 생태계에서 표준 툴 기준을 목표로 하고 있다. 이번 포스트에서는 Vue CLI의 개념부터 설치 그리고 Vue-CLI의 사용 방법까지 알아보도록 하자.
<!-- more -->

<!-- excerpt -->
<!-- excerpt -->

![cover](cover.png)

Vue CLI 3는 Vue.js 개발을 위한 시스템으로 Vue.js Core에서 공식으로 제공하는 CLI이다. Vue CLI는 애플리케이션 개발에 집중할 수 있도록 프로젝트의 구성을 도와주는 역할을 하며, Vue 생태계에서 표준 툴 기준을 목표로 하고 있다.

Vue CLI의 사용은 선택사항이다. Vue 애플리케이션을 개발하기 전에 Vue CLI를 통해 프로젝트를 구성하고 구축하지 않는다 하더라도 애플리케이션에 영향을 주지는 않는다. 그저 Vue CLI는 앞에서 말했듯이 툴의 역할을 하고 스캐폴딩에 도움을 주는 역할만 한다.
Vue CLI를 사용하지 않아도 무방하지만 Vue.js와 관련된 오픈 소스들은 대부분 Vue CLI를 통해 구성이 가능하도록 구현되어 있고 굳이 Git으로 clone하지 않아도 Vue CLI를 통해 더욱더 손쉽게 설치가 가능하기 때문에 Vue CLI의 사용을 추천하는 바이다.

그럼 이제 Vue CLI에 대해서 알아보자. 해당 포스트에서는 Vue CLI 3.x에 관해서 설명을 하며 Vue CLI 2.x에 대한 내용은 [Vue CLI 2](https://github.com/vuejs/vue-cli/tree/v2#vue-cli--)를 참고하자.


# Vue-CLI 3
Vue CLI는 애플리케이션에 필요한 요소들을 대화형 커맨드로 쉽게 설치하도록 도와준다. 현재 Vue CLI는 3.x까지 릴리즈된 상태이며, Vue CLI의 시스템은 3가지 요소로 구분할 수 있다.

## CLI
CLI(@vue/cli)는 전역적으로 설치된 npm 패키지이며, Vue.js 프로젝트를 생성하는 `vue create`, UI를 통해 프로젝트를 관리할 수 있는 `vue ui` 등 터미널에서 `vue`를 사용한 명령을 제공한다.

## CLI Service
CLI Service는 `webpack`, `webpack-dev-server` 위에 구축이 되며 CLI PlugIn을 실행하는 핵심 서비스와 webpack에 대한 설정을 포함하고 있다. 즉, webpack을 통해 애플리케이션의 개발 서버 실행, 빌드 등을 처리한다.

## CLI PlugIn
CLI PlugIn은 Babel/TypeScript, ESLint, e2e Test, 단위 테스트와 같은 선택적으로 설치가 필요한 PlugIn을 말하며, 프로젝트 생성 과정에서 포함하거나 이후에 포함 시킬 수 있다.


# Vue-CLI 3 설치
이제 Vue CLI를 설치해 보자. 기본적으로 Vue CLI를 설치하기 위해서는 8.9 버전 이상의 Node.js가 필요하다. Node.js 설치와 설명은 [빠르게 배우는 Node.js와 NPM 설치부터 개념 잡기](https://kdydesign.github.io/2017/07/15/nodejs-npm-tutorial/)를 참고하자.

Node.js를 설치하였다면 Vue-CLI를 설치하자.

```
$ npm i -g @vue/cli
$ vue --version
```

Vue CLI를 설치 후 버전을 확인해 보면 3.x이 설치된 것을 확인할 수 있다. 그리고 하나 더 설치하자.

```
$ npm i -g @vue/cli-init
```

`@vue/cli-init`은 2.x Template을 가져오기 위한 `vue init`기능을 제공한다.
예를 들면.

```
$ vue init webpack my-project
```

위와 같이 [vue-webpack-boilerplate](https://github.com/vuejs-templates/webpack)를 구성할 수 있다.


# Vue-CLI 3를 통한 프로젝트 생성
대부분 프로젝트를 시작할 때 또는 프로토타입 프로젝트를 만들 때 잘되어있는 Bolierplate를 가져다가 쓸 것이다. 그럴 때는 위에 설명했듯이 `vue init`만 사용하면 되지만 직접 프로젝트를 생성할 때에는 `vue create`를 사용한다.

vue 프로젝트를 생성해 보자.

```
$ vue create <project-name>
```

위와 같이 실행하면 대화형 커맨드로 프로젝트 구성에 필요한 요소들을 선택하여 설치할 수 있다. `default`를 선택하여 생성하게 되면 표시된 대로 `babel`과 `eslint`가 설치된다.
`Manually select features`를 선택하게 되면 `vuex`, `vue-router` 등과 같은 몇 가지 더 선택적으로 설치할 수 있다. 우리는 `Manually select features`를 선택하도록 하자.

![vue-cli-sample1](img1.png)

무엇을 설치할지는 본인의 몫이지만 해당 포스트에서는 ** `Babel`, `Router`, `Vuex`, `CSS pre-processors`, `Linter / Formatter` **를 선택하여 설치해 보자. `Unit Testing`에 대해서는 [JavaScript 단위 테스트 프레임워크 - Mocha Tutorial](https://kdydesign.github.io/2017/06/08/Mocha/)을 참고하자.

필요한 모듈들을 선택하고 다음 단계로 넘어가면 vue-router의 `history` 기능을 사용할지 여부를 확인한다. 기본 설치이므로 엔터를 치고 넘어가자.

![vue-cli-sample2](img2.png)

다음 단계에서는 `CSS 전처리기(CSS pre-processors)`에 대해서 어떤 모듈을 사용하지 선택하는 항목이 나온다. 본 포스트에서는 `Stylus`를 선택하였다.

![vue-cli-sample3](img3.png)

그다음으로는 `ESLint`에 관련된 항목이 나온다. 어떤 항목을 선택하더라도 ESLint는 기본적으로 설치가 되며 여기서는 ESLint에 대해 어떤 룰을 적용할지를 선택한다. 본 포스트에서는 `Standard config`를 선택하도록 하겠다.

![vue-cli-sample4](img4.png)

다음으로는 `Lint on save`를 선택하고 그다음 단계에서는 `In package.json` 선택하고 넘어가게 되면 선택된 모듈들이 설치됨으로써 프로젝트 구성은 끝이 난다.

생성된 디렉토리를 보게 되면 우리가 애플리케이션을 구성하는데 필요한 요소들이 이미 준비가 되어있다.


# Vue-CLI 3 UI
이제 이렇게 구성된 프로젝트를 `Vue-CLI 3 UI`를 통해 프로젝트 관리를 알아보자.
위에서 생성된 프로젝트에서 `vue ui`를 실행하자.

```
$ vue ui
```

위와 같이 실행하면 `Vue 프로젝트 매니저`가 `locahost:8000`으로 자동으로 브라우저가 실행된다. 이 Vue 프로젝트 매니저에서 위에서 생성한 프로젝트를 생성 할 수도 있으며 이미 생성된 프로젝트를 불러와서 관리 포인트로 둘 수도 있다. 우리는 프로젝트를 이미 생성하였으므로 `가져오기` 버튼을 클릭하여 해당 프로젝트를 가져오자.

![vue-ui](vue-ui.png)

Vue 프로젝트 매니저를 훑어보면 대번 어떤 형태인지 알 수 있다. 우리가 커맨드로 처리하던 행동들을 UI를 통해서 처리할 수 있다고 볼 수 있다.


# 프로젝트 실행
`Vue 프로젝트 매니저`의 `작업 목록`에서 `serve`를 통해 구동할 수도 있으며, npm 커맨드를 통해서도 구동할 수 있다.

```
$ npm run serve
```

![run-serve](run-serve.png)


# Vue CLI 3 PlugIn 설치
Vue CLI를 통해 PlugIn을 설치하기 위해서는 `vue add` 커맨드를 사용하면 된다. 또는 `Vue 프로젝트 매니저`에서 PlugIn의 목록을 검색할 수도 있고 설치까지 할 수 있으니 한번 확인해보기 바란다.

여기서는 `vue-cli-plugin-axios`를 설치해보자.

```
$ vue add axios // or vue add vue-cli-plugin-axios
```

PlugIn이 설치되었으면 확인해보자.
먼저 `src > plugins` 폴더를 보게 되면 `axios.js`를 확인해 볼 수 있다. 해당 파일의 내용을 보면 이런 내용이 있다.

{% codeblock axios.js lang:javascript%}
Plugin.install = function(Vue, options) {
  Vue.axios = _axios;
  window.axios = _axios;
  Object.defineProperties(Vue.prototype, {
    axios: {
      get() {
        return _axios;
      }
    },
    $axios: {
      get() {
        return _axios;
      }
    },
  });
};

Vue.use(Plugin)
{% endcodeblock %}

우리가 Vue CLI를 사용하지 않고 Vue.js 애플리케이션을 만들었다면 `axios`를 npm으로 설치하고 main.js 또는 app.js에 수동적으로 추가해주었을 `Vue.use()`가 자동으로
생성되어있다.

그럼 `axios.js`는 어디에 삽입된 것일까? `src > main.js`를 열어보자.

{% codeblock main.js lang:javascript%}
import './plugins/axios'
{% endcodeblock %}

상단에 보면 이미 `axios.js`가 `main.js`에 import 된 것을 볼 수 있다.




- - -
여기까지 해서 우리는 `Vue CLI 3`를 통해 프로젝트를 구성하고 실행했으며, `Vue 프로젝트 매니저`를 통해 프로젝트를 관리할 수 있다는 것을 알게 되었다. 물론 `package.json`에도 종속성이 관리되어 설치된 것도 확인이 가능하다.

Vue CLI 3 PlugIn에 대해서는 [Vue CLI 3 플러그인 및 프리셋](https://cli.vuejs.org/guide/plugins-and-presets.html#plugins)을 참고하자.

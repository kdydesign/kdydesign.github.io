---
title: "Lerna를 활용한 Mono-Repo 구축 완벽 가이드 - 예제를 통한 완벽 파악"
date: 2020-08-27 08:37:12
tags:
- lerna
- mono-repo
- multi-repo
- poly-repo
- git
- repository
- lerna tutorial
- lerna example
categories :
- javascript
- nodejs
- git
- repository
- mono-repo
keywords:
- javascript
- lerna
- mono-repo
- multi-repo
- poly-repo
- lerna tutorial
- mono-repo tutorial
- multi-repo tutorial
- git repository
- git
- lerna example
- lerna sample
disqusIdentifier: mono-repo-lerna-example
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
[Lerna를 활용한 Mono-Repo 구축 완벽 가이드 - 개념 정리](https://kdydesign.github.io/2020/08/25/mono-repo-lerna/) 에서 `Lerna`와 `Mono-Repo`에 대한 개념을 잡았다면 이번 포스팅에서는 `Lerna`를 설치하고 주요 명령어 및 실제로 패키지를 만들고 배포까지 따라 하면서 완벽하게 `Lerna`와 `Mono-Repo`를 파악하자
<!-- more -->

<!-- excerpt -->
<!-- excerpt -->

![cover](cover.png)

[Lerna를 활용한 Mono-Repo 구축 완벽 가이드 - 개념 정리](https://kdydesign.github.io/2020/08/25/mono-repo-lerna/) 에서 `Lerna`와 `Mono-Repo`에 대한 개념을 잡았다면 이번 포스팅에서는 `Lerna`를 설치하고 주요 명령어 및 실제로 패키지를 만들고 배포까지 따라 하면서 완벽하게 `Lerna`와 `Mono-Repo`를 파악하자

예제는 **`CLI를 통해 간단한 로그를 출력하는 패키지`**로 `Lerna`를 활용한 `Mono-Repo` 구조로 구축, 개발, 배포까지 진행할 것이다.

lerna의 독립 모드의 경우 패키지의 버전을 독립적으로 가져가며 좀 더 까다로운 면이 있기 때문에 해당 예제에서는 lerna의 **`고정모드(Fixed Mode)`**가 아닌 **`독립 모드(Independent Mode)`**로 구축할 것이다.
또한 `npm`보다는 `yarn`을 추구하고 lerna와 좋은 궁합을 보이고 `Yarn Workspace`를 사용할 것이기 때문에 `yarn`을 사용할 것이다.

{% alert info no-icon%}
 - CLI를 통한 간단한 로그 출력 패키지
 - 독립 모드(Independent Mode)
 - Yarn
 - Yarn Workspace
{% endalert %}


# CLI를 통하여 간단한 로그를 출력하는 패키지를 만들어 보자.

## 1. lerna 설치
먼저 이전 포스팅에서 개념을 익혔으니 실제로 lerna를 설치해보자.

```sh
$ npm install -g lerna
```

위처럼 lerna를 설치하기가 싫다면 아래처럼 `npx`를 통하여 바로 사용하자.

```sh
$ npx lerna init
```

## 2. Git 초기화
lerna의 `publish` 명령어는 변경된 패키지를 일괄적으로 Git Remote Repository에 Push를 하므로 Git을 사용해야 한다.

Github Repository를 미리 구축해 놓자. Repository 구축에 관한 내용은 아래를 참고하자.

{% alert info no-icon%}
* [Github에 내 Repostiory(저장소) 생성과 연동하기]()
{% endalert %}

Git을 통해 초기화 및 폴더까지 생성하자.

```sh
$ git init [DIR_NAME]
$ cd [DIR_NAME]
```


## 3. Lerna Repository로 변경
폴더를 생성하고 Git을 초기화하였다면 해당 Repository를 lerna로 구성하자.

```sh
$ lerna init --independent // or -i
```


### lerna.json
`lerna.json`은 lerna를 구성하는 설정 파일이다.

패키지로 배포와 관리된 `packages`를 명시해 주며 version 정책을 어떻게 가져갈 것인지며 npmClint는 npm을 사용하지 yarn을 사용할지 지정해 줄 수 있다.


아래와 같이 수정하자.

{% codeblock lerna.json lang:json %}
{
  "version": "independent",
  "npmClient": "yarn",
  "useWorkspaces": true,
  "packages": [
    "packages/*"
  ]
}
{% endcodeblock %}

우리는 version 정책을 독립 모드로 가져가기 때문에 `version: "independent"`로 지정한 것이고,
yarn을 사용할 것이기 때문에 `npmClient: "yarn"` 그리고 yarn workspace 사용을 위해 `useWorkspaces: true`로 지정하였다.


### package.json
Root 경로에 있는 `package.json`의 역할은 `공통된 node module들의 devDependencies`와 `최상위에서 실행될 script`들을 명시해준다.


아래와 같이 수정하자. 

{% codeblock package.json lang:json %}
{
  "private": true,
  "workspaces": [
    "packages/*"
  ],
  "devDependencies": {
    "lerna": "^3.20.2"
  }
}
{% endcodeblock %}

lerna.json에서 yarn workspace를 사용하였기 때문에 실제로 workspace에 어떤 패키지가 담길 것인지 지정해준다. 보통 `lerna.json의 packages의 경로와 일치`한다. 그리고 `private: true`로 지정함으로써 Root가 NPM Repository로 배포되는 것을 막아준다.
 

## 4. 패키지 생성
이제 실제로 사용될 패키지를 만들어보자.


패키지는 `packages` 경로에 포함되어있어야 하며, 모든 패키지는 `lerna.json의 packages 속성에 따른다.` 수동으로 직접 폴더를 생성할 수도 있지만 lerna의 `create` 명령을 통해서도 기본 패키지의 구조를 Scaffolding 할 수 있다.

```sh
$ lerna create [PACKAGE_NAME]
```

우리는 **CLI를 통한 Log 출력 패키지**를 예시로 들고 있어서 **`log-cli`**와 **`log-core`**라는 두 패키지를 생성하자.

 
```sh
$ lerna create log-cli
```

```sh
$ lerna create log-core
```

`log-cli`는 우리가 CLI command를 입력하여 그 값을 받아 처리하는 패키지이고, `log-core`는 입력받은 command를 통해 실제로 로그를 출력하는 패키지이다.


## 5. 공통 종속성 설치
Root 경로에 모든 패키지가 공통으로 사용될 모듈을 설치하자. `lerna add`라는 명령어를 사용할 수도 있지만 `lerna add`는 패키지 간 종속성 설치 시 사용하는 걸 추천한다.
그냥 사용한다 하더라고 Root 경로에 모듈은 설치되겠지만 각 패키지에 dependencies가 걸리게 되어있다. 그렇기 때문에 Root 경로의 공통 모듈을 `npm`또는 `yarn`을 통하여 설치하자.


공통으로 사용될 모듈로 `eslint`를 설치해보자 

```sh
$ yarn add eslint --dev --ignore-worksapce-root-check

```

```sh
$ npm install eslint --dev
```

{% alert danger no-icon %}
`yarn`을 통해 eslint를 설치하기 위해서는 workspace를 지정하였기 때문에 일반 `add`를 통해서는 설치가 불가능하다. 그렇기 때문에 `--ignore-worksapce-root-check` 옵션을 지정하도록 하자. 
{% endalert %}

설치 후 Root 경로의 `package.json`을 보면 `devDependencies`에 `eslint`가 설치된 것을 확인 할 수 있다.


## 6. 각 패키지에 모듈 설치
이제 각 패키지에 필요한 모듈을 설치해보자.


### log-cli 모듈 설치
command를 입력받아야 하는 log-cli에 [commander](https://github.com/tj/commander.js#readme)를 설치하자.

각 패키지에 모듈을 설치할 때에는 공통 모듈을 설치하는 것과는 다르게 `lerna add`를 통해서 각 패키지에 설치 할 수 있다. 이 과정에서 `hoisting`이 일어나고 종속성을 최적화시킨다.

`lerna add`를 사용할 때는 `--scope` 옵션을 통해서 어느 패키지에 설치할 것인가를 명시해준다. `--scope`를 주지 않을 경우 모든 패키지에 설치된다.

```sh
$ lerna add commander --scope=log-cli
```

위 명령어 실행 후 파일 주로를 보면 log-cli 경로에 `node_modules` 폴더가 생성되지 않았다. 하지만 `package.json`을 보게 되면 commander 모듈이 추가되어있는 것을 볼 수 있다. 이는 종속성 최적화로 인해 Root 경로에 추가된 것이다.


### log-core 모듈 설치
log-core에서는 console.log를 출력하는 모듈을 만들 것이다.

패키지 설치 방법을 익히기 위해 임의로 로그 문구에 색상을 입힐 수 있는 [chalk](https://www.npmjs.com/package/chalk) 모듈을 설치해보자.

```sh
$ lerna add chalk --scope=log-core
```

설치 방법은 log-cli에서 설치한 방법과 동일하다. 다만 다른 게 있다면 log-cli와는 다르게 `log-core에는 node_modules 경로가 생성`되었다. 이 역시 `hoisting` 과정에서 일어난 사항이니 그게 염두에 두지 않아도 된다.


## 7. 각 패키지에 기능 추가
필요한 모듈은 설치가 되었기 때문에 이제 각 패키지에서 기능이 동작되도록 구현하자.

### log-core 수정
`log-core.js`를 수정하자.

{% codeblock log-core.js lang:javascript%}
const { red } = require('chalk')

function core () {
  console.log(red('❤  Running Core !!!!!'))
}

module.exports = core
{% endcodeblock %}

`log-core`에서는 `chalk`를 사용하여 `console.log`를 출력해 주는 코드를 작성하였다.


### log-cli 수정
`log-cli.js`와 `log-cli/package.json`을 수정하자 
 
{% codeblock log-cli.js lang:javascript%}
#!/usr/bin/env node

const { program } = require('commander')
const LogCore = require('log-core')

// action
program.action(cmd => LogCore())

program.parse(process.argv)
{% endcodeblock %}

{% codeblock log-cli/package.json lang:json%}
{
  "name": "log-cli",
  "version": "1.0.0",
  "description": "log-cli-example",
  "author": "Your name",
  "license": "MIT",
  "bin": {
    "log-cli": "lib/log-cli.js"
  },
  "files": [
    "lib"
  ],
  "dependencies": {
    "commander": "^6.0.0"
  }
}
{% endcodeblock %}


`log-cli.js`에서는 `commander`와 `log-core`를 추가하고 `commander`를 통해 command를 입력받으면 `log-core`를 수행되게 되어있다.

`package.json`에서는 기본적으로 추가되어있던 `main`속성 대신 `bin` 속성을 추가하여 CLI가 가능하게 수정한다.


## 8. 로컬에서 CLI 테스트 수행
기능까지 완성이 되었으니 로컬에서 만든 모듈들을 실행해보자.

최초 실행은 `log-cli`를 실행하는 것이기 때문에 `log-cli`를 설치 후 실행해 보자. 여기서는 `npm link`를 통하여 global로 `symbolic link`를 생성하였다.

```sh
$ npm link packages/log-cli
```

```sh
$ log-cli
```

`log-cli`를 입력하면 결과가 출력되는 것을 확인할 수 있다.


## 9. 패키지 내 참조 및 설치
위처럼 로컬에서 실행하면 정상적으로 동작된다. 로컬에서는 `log-cli`와 `log-core` 연관 관계를 인지하고 있기 때문이다. 그렇기 때문에 실제로 패키지를 배포 후 배포된 패키지를 설치하여 실행한다면 아래와 같은 오류가 출력될 것이다.

![run-error](error-capture.png)

이 오류는 `log-cli`에서 `log-core`를 삽입하였는데 실제로 `log-cli`에는 `log-core`가 종속되지 않았기 때문에 발생한다. 이를 해결하기 위해서는 `lerna add`를 통해서 `log-cli`에 `log-core`를 설치해 해줘야 한다.

```sh
$ lerna add log-core --scope=log-cli
```


## 10. Git Commit과 Push
이제 모든 변경 사항을 연동된 Git Remote Repository에 반영하자. 그 전에 불필요한 리소스들이 반영되지 않도록 Root 경로에 **`.gitignore`** 작성하는 것을 잊지 말자.


아래는 `.gitignore` 예시이다.

{% codeblock .gitignore lang:text%}
.idea
node_modules
*.lock
*lock.json
{% endcodeblock %}


```sh
$ git add .
$ git commit -m "deploy" 
$ git push -u origin master
```

## 11. 패키지 배포
이제 패키지 배포 이전의 모든 작업이 끝이 났다. 실제로 지금까지 만든 `log-cli`와 `log-core`를 `NPM Repository`에 배포해 보자. NPM Repository에 대해서는 [NPM 패키지 - 가입부터 생성 및 배포까지 배워보기!]() 을 참고하자.

NPM 설정이 준비되었다면 `lerna publish`를 통해서 모든 패키지를 배포하자.

{% alert danger no-icon %}
NPM Repository에 배포하기 전 **log-cli와 log-core의 package.json에서 `name` 속성을 변경**하자. 해당 명칭은 이미 배포된 다른 모듈과 충돌이 나므로 변경해야 한다. 
{% endalert %}

```sh
$ lerna publish
```

위 명령어를 입력하면 `log-cli`와 `log-core`가 동시에 NPM Repository로 배포된 것을 확인할 수 있다.


![lerna-publish-example](lerna-publish-example.png)

{% alert danger no-icon %}
NPM Repository에 배포된 패키지는 **72시간**이 지나면 직접 지울 수 없어서 불필요하다면 즉시 삭제하기 바란다.

```
$ npm unpublish log-core -f
$ npm unpublish log-cli -f
```

`log-cli`에서 `log-core`가 종속되어있기 때문에 `log-cli`먼저 삭제해야 한다.
{% endalert %}


## 12. 릴리즈 패키지 설치 및 실행
이제 실제로 배포된 패키지를 설치하여 사용해 보자.

```sh
$ npm install -g log-cli // or PACKAGE_NAME
```

- - -

## 릴리즈 노트 생성
lerna에서 독립 모드(Independent)로 사용하게 되면 릴리즈 노트가 걸릴 것이다. 릴리즈 노트는 보통 `CHANGELOG.md`로 남게 되는데 이를 위해서는 `lerna.json`을 아래와 같이 설정해 주면 기본적인 `CHANGELOG`를 사용할 수 있다.

{% codeblock lerna.json lang:json %}
{
  "version": "independent",
  "npmClient": "yarn",
  "useWorkspaces": true,
  "packages": [
    "packages/*"
  ],
  "command": {
    "publish": {
      "conventionalCommits": true
    }
  }
}
{% endcodeblock %}

lerna의 `publish` 명령어를 실행하면 `conventiaonalCommit`이 실행되도록 `conventionalCommits` 옵션을 지정해 주었다. [Conventional commits](https://www.conventionalcommits.org/en/v1.0.0/)는 이곳에서 참고하자.


`conventionalCommits` 옵션을 지정하면 `semver`에 따른 버전이 결정되고 `commit message`의 기록에 따라 `CHANGELOG.md`가 각 패키지 별로 생성된다.
기본적인 옵션 이외에 [lerna-changelog](https://github.com/lerna/lerna-changelog)를 사용하면 더 적합한 릴리즈 노트를 작성할 수 있다.


- - -


여기까지 해서 [Lerna를 활용한 Mono-Repo 구축 완벽 가이드 - 개념 정리](https://kdydesign.github.io/2020/08/25/mono-repo-lerna/)부터 예제를 통하여 `Lerna`와 `Mono-Repo`에 대해 알아보았다.


여기서 집고 넘어갈 것은 `Lerna`는 단순히 `Mono-Repo`를 구축하는 데 도움을 주는 도구에 불과하다. 귀찮고 오래 걸리겠지만 `Mono-Repo`의 구조에서 수동으로 생성, 배포, 설치 모두 할 수 있는 것이다. `Mono-Repo`의 구조로 간다면 패키지의 관리와 배포가 쉬워지니 반영해 볼 기회가 있다면 적극적으로 추천한다.

---

더 알아보기
> [Lerna를 활용한 Mono-Repo 구축 완벽 가이드 - 개념 정리](https://kdydesign.github.io/2020/08/25/mono-repo-lerna/)

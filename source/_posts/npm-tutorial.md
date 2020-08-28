---
title: "빠르게 배우는 NPM 패키지 생성부터 배포까지 완벽 가이드"
date: 2020-08-28 14:31:36
tags: 
- npm
- nodejs
- javscript
categories :
- javascript
- nodejs
- npm
keywords:
- javascript
- nodejs
- npm
- npm tutorial
- nodejs tutorial
- npm 설치
- npm
- npm 패키지
- npm 모듈
- node module 배포
- npm 배포
- npm 만들기
- node module 만들기
- node module
disqusIdentifier: npmtutorialdepoly
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
예제를 통하여 `npm` 패키지를 생성하고 생성된 `npm` 패키지를 NPM Repostory에 배포까지 배움으로 인해 오픈소스로서 NPM 생태계에 기여하는 방법을 배워보자.
<!-- more -->

<!-- excerpt -->
<!-- excerpt -->

![cover](cover.png)

이번 포스팅에서는 `npm` 모듈 혹은 `npm` 패키지를 생성하여 실제로 NPM Registry에 업로드까지 하여 오픈소스로서 NPM 생태계에 기여하는 방법을 배워보자.

해당 섹션을 읽기 전에 `npm`에 관하여 알고 싶다면 [빠르게 배우는 Node.js와 NPM 설치부터 개념 잡기](https://kdydesign.github.io/2017/07/15/nodejs-npm-tutorial/)에서 `node.js`와 `npm`에 대하여 파악 먼저 하자.


우리가 오픈 소스를 만들고 싶거나 관리를 하고 싶다면 `git hub`에 오픈소스를 올리는 것에는 한계가 있다. 우리가 오픈 소스를 만드는 목적은 `공유`와 `제공`이라 생각한다. 내가 만든 것을 남에게 공유하고 이런 오픈 소스가 필요한 사람에게는 쉽게 접해서 사용할 수 있게끔 하는 것이다. 그렇기 때문에 `git hub`에 올리는 것을 넘어서 `npm` 패키지로 모듈화하여 `NPM Registry`에 올리는 것이 필요하다. 지금부터 `npm` 패키지를 만들고 배포하는 방법을 배워보자.


# NPM (Node Package Manager)
시작하기에 앞서 간단하게 `npm`에 대해 알아보자.


## NPM 개념
`npm`은 `Node Package Manager`로 이름의 유래는 npm이 Node.js용 패키지 관리자로 처음 생성되었을 때이다.

`npm`의 역할은 소프트웨어의 라이브러리 또는 레지스트리이다. 소프트웨어를 관리하고 설치를 지원하며 이 레지스트리에는 약 800,000개 이상의 npm 패키지가 포함되어있다. 오픈 소스 개발자는 이 npm을 이용하여 소프트웨어를 공유하고 관리한다.


## NPM 설치
`npm`은 `Node.js`와 함께 설치된다. 그렇기 때문에 `Node.js`를 설치하면 `npm` 역시 같이 설치가 된다.

설치가 되어있지 않았다면 [Node.js](https://nodejs.org)에서 설치하도록 하자. 

## Package.json
`npm`의 패키지는 `package.json`에 정의된다. `npm init` 명령어를 통하면 최초에 이 파일이 만들어지고 `npm` 패키지를 설치하게 되면 이 `package.json`에 명시된다. 이 외에도 이 패키지가 이름이 무엇인지, 라이센스가 어떻게 되는지, NPM Repostory에 배포될 파일들이 무엇인지 등 패키지에 대한 정보를 명시한다. 보통 `package.json`을 가볍게 여기는 경우가 있는데 이 정보들은 단순하게 제공하는 것이 아닌 배포에 필요하고 패키지의 사용처를 남기는 등의 역할을 하므로 **신중하게 작성**할 필요가 있다.

## Package-lock.json
`package-lock.json`은 최초 `npm init`을 실행 시 생성되지는 않는다. 이 `package-lock.json`은 `npm` 패키지를 설치하거나 수정, 삭제 등의 작업을 진행할 때 생성되며 핵심 역할은 **각 패키지에 대한 의존성 관리**이다.

각 패키지는 서로 엉켜있는 실타래와 같다. 하나의 패키지를 여러 패키지에서 사용할 수 있고 하나의 패키지는 여러 개의 버전을 가지며 또 이 여러 버전을 다른 패키지에서 사용할 수 있다. 이렇게 되면 패키지 버전 간의 충돌과 호환이 되지 않는 경우가 있는데 이를 미연에 방지하기 위한 것이다.

실제로 `package-lock.json`을 살펴보면 하나의 패키지에 `dependencies(종속)`가 어떤 패키지인지 버전 정보와 이름이 나열되어 있고 `dependencies`에 명시된 특정 패키지를 다시 검색 및 추적하다 보면 여러 패키지에서 사용하는 것을 볼 수 있다.

간혹 **내가 설치한 npm 패키지의 버전을 업데이트하기 위해 `npm install`을 하였는데 최신 버전이 업데이트되지 않는 경우에는 이 `package-lock.json`을 삭제하고 재 설치**하자.


## 패키지 공유
`npm` 패키지는 [NPM Registry](https://www.npmjs.com)에 배포하여 공유할 수 있다. 가입과 사용은 **무료**이고 일부 개인적인 권한을 확장하기 위해서는 요금을 부과해야 하지만 해당 포스팅을 따라 하는 데에는 불필요하다.


아래에 요금을 지불하고 업그레이드 시 사용 가능한 기능이니 참고만 하자.

{% alert info no-icon%}
**NPM 권한 업그레이드($7)**

✓ 비공개 패키지 게시
✓ 개인 패키지 설치
{% endalert %}

- - - 

여기까지 간략하게나마 `npm`에 대하여 알아보았다.

이제 실제로 `npm` 패키지를 만들고 `NPM Registry`에 배포하는 방법을 배워보겠다.


# NPM 가입
`NPM Registry` 가입은 [NPM 공식 페이지](https://www.npmjs.com)에서 가입할 수 있다. 이름과 email, 비밀번호 입력 후 **email 인증을 필수로 진행**해야 한다. **email 인증을 하지 않으면 배포가 불가능**하다.

가입 후 로그인을 하고 우측 상단의 아이콘을 눌러 `Package`로 가보자. 앞으로 패키지를 배포하게 되면 이곳에 올라가게 된다.


# 패키지 만들기
패키지가 올라갈 곳을 마련해 두었다. 이제 패키지를 만들어보자. 패키지는 간단한 예제용으로 **`cli` 커맨드를 입력하여 로그를 출력하는 패키지**를 만들어보겠다.

## 1. NPM 초기화
`npm-deploy-sample`이라는 폴더를 생성하고 내부에서 커맨드 창을 연 후 아래와 같이 명령어를 입력하여 NPM 초기 설정을 진행하자.

```
$ npm init -y
```

위와 같이 명령어를 입력하면 `package.json`이 생성된 것을 확인 할 수 있다.

{% alert info no-icon%}
`-y`를 입력하지 않으면 `package.json`에 들어가 값들을 직접 입력하면서 `package.json`을 생성할 수 있으며 `-y`를 입력할 경우 기본값으로 설정된다.
{% endalert %}


## 2. Dependencies 설치
우리가 해당 예제를 만들면서 필요한 패키지는 [commander](https://github.com/tj/commander.js#readme)이다. 이 패키지는 `Node.js`의 CLI 인터페이스를 위한 패키지이다. 즉, 우리가 CLI를 입력하여 로그를 출력할 때 CLI를 입력하게끔 해주는 도구이다.

바로 설치하자.

```
$ npm i commander
```

{% alert info no-icon%}
`i`는 `install`의 축약형이다.
{% endalert %}

`commander`를 설치하게 되면 `package.json`의 `dependencies`에 추가되므로 확인해 보도록 하자. `commander`는 패키지가 배포 후에도 사용할 패키지이기 때문에 `devDependencies`가 아님을 참고하자.


{% alert warning no-icon%}
* **dependencies** - 런타임에도 계속 사용되며 실제로 필요한 기술 스펙
* **devDependencies** - 개발, 컴파일 시에만 필요하며 Production Mode에는 필요하지 않은 스펙
{% endalert %}


## 3. 기능 개발
이제 CLI를 구현해보자. 

먼저 `bin`라는 폴더를 생성하자. **폴더명에 있어서 지금 만드는 폴더명은 앞으로 `package.json`에 명시가 필요하니 대충 만들지는 말자.**

`bin` 폴더를 만든 후 안에 `cli.js` 파일을 생성하고 아래와 같이 적용하자. 

{% codeblock cli.js lang:javascript %}
#!/usr/bin/env node

const { program } = require('commander')

// action
program.action(cmd => console.log('✓ Running!!'))

program.parse(process.argv)
{% endcodeblock %}

`commander`를 통해 CLI를 입력하면 문구를 출력하는 단순한 기능이다.


## 4. Package.json 수정
이 부분에서 `package.json`을 수정하는 이유는 위에서 개발된 파일을 배포 대상으로 삼고 CLI를 통해 실행될 파일을 지정해줘야 하기 때문이다.

우선 아래와 같이 `package.json`을 수정하자.

{% codeblock package.json lang:json %}
{
  "name": "npm-deploy-sample",
  "version": "1.0.0",
  "description": "npm deploy sample project",
  "author": "",
  "bin": {
    "log-run": "bin/cli.js"
  },
  "license": "MIT",
  "keywords": [
    "sample"
  ],
  "files": [
    "cli"
  ],
  "dependencies": {
    "commander": "^6.1.0"
  }
}
{% endcodeblock %}

이 수정 내용에서 중요한 점은 `bin` 속성이다. `bin` 속성은 실행 할 수 있는 패키지를 만들기 위해서는 정의가 필요하며, 이 패키지를 설치 시에 npm은 `bin` 속성에 정의된 파일(`bin/cli`)의 Symlink를 생성하게 된다. 여기서 `log-run`은 CLI의 명령어가 된다.

`files`는 패키지를 `npm`에 배포할 경우 실제로 패키지에 포함될 파일들이며, 폴더 이름을 지정하면 폴더 안의 파일을 포함한다. 

`keyword`는 문자열 배열로 `npm` 패키지 검색 시 리스트에 표시되도록 도와준다. 이 외의 속성은 참고만 하자.


## 5. Local 테스트
패키지를 다 만들고 설정까지 끝냈으니 잘 동작하는지 Local에서 테스트해보자.

해당 패키지 디렉토리 내 커맨드 창에서 아래와 같이 입력하자.

```
$ npm link
```

이제 커맨드 창에 CLI를 입력하여 실행해 보자. `CLI 명령어`는 우리가 `package.json`의 `bin` 속성에 명시한 key 값이다.

```
$ log-run
```

위와 같이 실행하면 로그가 출력되는 것을 확인 할 수 있다.

`npm link`는 명령을 수행한 위치의 패키지를 `global` 한 상태로 심볼링 링크로 연결된다. 심볼릭 링크로 생성되었기 때문에 `bin/cli.js`를 수정하고 바로 실행을 하더라도 수정된 내용이 반영된다.

아래 명령을 통해 `global` 하게 링크가 걸려있는 것을 확인 할 수 있다.

```
$ npm ls -g --depth=0
```

## 6. .npmignore
이제 `NPM Registry`에 배포하는 일만 남았지만, 그전에 개발 도구의 설정 파일과 같은 불필요한 파일이 배포되지 않게 `.npmignore` 파일을 최상위 경로에 작성해주자. `.npmignore`파일은 `.gitignore`파일로도 대체가 가능하다.

{% codeblock .npmignore lang:text %}
.idea
node_modules
{% endcodeblock %}


## 7. 배포
기능이 우리가 원하는 대로 동작하는 것을 확인하였으면 이제 `NPM Registry`에 배포를 하자.

먼저 커맨드 창에서 명령어를 통해 `NPM Registry`에 로그인을 하자. 로그인 정보는 위에서 `NPM Registry`에 가입한 이름과 패스워드 그리고 메일이다.

```
$ npm login
```

로그인이 정상적으로 되었는지 확인은 아래 명령어로 확인 할 수 있다.

```
$ npm whoami
```

로그인이 정상적으로 되었다면 이제 배포하자.

```
$ npm publish
```

정상적으로 배포가 된다면 `NPM Registry`에는 아래와 같이 패키지가 업로드되었을 것이다.

![success-deploy](success-deploy.png)


만약 배포 중 오류가 출력되면 현재로는 보통 **세 가지 경우**이다.

{% alert warning no-icon%}
**1. `NPM Registry` 가입 후 E-Mail 인증을 하지 않은 경우**
 - E-Mail 인증을 시도하자.

**2. 패키지의 이름이 이미 다른 패키지와 중복이 된 경우**
 - `package.json`의 `name` 속성을 바꿔주자.

**3. 이미 같은 버전으로 배포가 된 경우**
 - `$ npm version [major, minor, path, x.x.x]` 명령어로 버전을 올려 배포하자.
{% endalert %}


위 내용대로 하면 정상적으로 패키지가 배포되는 것을 확인할 수 있다. 

{% alert danger no-icon %}
**참고**

배포된 패키지는 **72시간**이 지나면 삭제할 수 없어서 불필요한 패키지라면 미리 삭제하자.
`$ npm unpublish PACKAGE_NAME -f`
{% endalert %}


## 8. 릴리즈 버전 설치 후 실행
`NPM Registry`에 등록된 패키지를 설치하여 사용해 보자.

```
$ npm i -g PACKAGE_NAME
$ log-run
```

- - - 
 
사실 `Git`도 연동을 하면 좋지만, 이번 포스팅에서는 `npm` 배포 방법만 설명해 보았다. `npm` 패키지 배포에 있어서 한 두 번만 하면 크게 어려울 것이 없지만 `@`와 같은 `scope` 개념도 있기 때문에 다음 포스팅에서는 `NPM 패키지의 Scope에 대하여` 알아보도록 하겠다.

또한 이 포스팅에서 더 나아가 `하나의 Git Repository에 N개의 패키지가 존재`하는 `Mono-Repo`와 이 `Mono-Repo` 구조에서 `npm publish`를 어떻게 동시에 진행 할 수 있는지는 아래 **더 알아보기**에서 확인할 수 있다.

더 알아보기
> [빠르게 배우는 Node.js와 NPM 설치부터 개념잡기](https://kdydesign.github.io/2017/07/15/nodejs-npm-tutorial/)
> [Lerna를 활용한 Mono-Repo 구축 완벽 가이드 - 개념 정리](https://kdydesign.github.io/2020/08/25/mono-repo-lerna/)
> [Lerna를 활용한 Mono-Repo 구축 완벽 가이드 - 예제를 통한 완벽 파악](https://kdydesign.github.io/2020/08/27/mono-repo-lerna-example/)

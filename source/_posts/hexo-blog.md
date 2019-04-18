---
title: "Hexo와 Github page로 시작하는 블로그 만들기"
date: 2017-06-23 22:18:15
tags: 
- hexo
- git
- github
- 블로그
categories :
- javascript
- nodejs
- hexo
- github
keywords:
- javascript
- nodejs
- hexo
- git
- github
- githubio
- blog
- hexo blog
- hexo 블로그
- hexo 테마
- hexo 블로그 만들기
- hexo github
- github page
- 블로그
- 블로그 만들기
- hexo 테마 추천
- github 블로그
- github 블로그 hexo
- hexo page
- hexo new post
- jekyll
disqusIdentifier: starthexoblog01
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
 Jekyll보다 쉬운 hexo와 github page를 이용하여 블로그를 쉽고 빠르게 만들어보자.  `github page`는 `Jekyll`과 많이 사용되지만 hexo가 `Jekyll`보다 더욱 쉽고 빠르게 블로그를 만들 수 있다.
<!-- more -->

<!-- excerpt -->
<!-- excerpt -->

![cover](cover.png)

블로그를 호스팅해주는 포털 사이트는 많지만 이번 포스팅에서는 **hexo**와 **github page**를 이용하여 블로그를 만드는 방법을 적어보겠다. `github page`는 `Jekyll`과 많이 사용되지만 hexo가 `Jekyll`보다 더욱 쉽고 빠르게 블로그를 만들 수 있다.

자세한 설명은 건너뛰고  **`Hexo와 Github io로 시작하는 블로그 만들기`**  바로 시작하자.

## Git과 Github

개발자들이라면 `github`가 무엇인지는 알 것이다. (몰라도 상관없다.) 이 `github`에 대해 주야장천 떠들기만 하면 이 포스트의 목적을 이룰 수 없다. 그리고 이 포스트는 **일반인이 보고 따라하는 것도 목적이 있기에** 간단하게 설명하고 바로 시작한다.

먼저 `git`을 대충 설명하면 `버전 관리 도구`이다. `subversion` 같은 거.. (아.. 뭔가 점점 깊게 설명하게 될 것 같은..) 그냥 이 포스트에서는 이렇게 이해하자.

{% alert info %}
**git** - 내 포스트를 웹에 올리기 위해 필요한 도구
{% endalert %}

`hexo`와 `github page`를 통해 만드는 블로그는 일반 블로그처럼 웹에서 직접 작성하지 않는다. 내 컴퓨터에서 먼저 글을 쓰고 그걸 웹으로 보내서 브라우저에서 볼 수 있도록 하는 것이다.

그럼 `github`와 `github page`는 무엇인가?
 
{% alert info %}
**github** - 내 포스트를 웹에 저장하는 저장 공간
**github page** - 저장된 내 포스트를 브라우저에 출력하는 페이지
{% endalert %}

`github`는 어떤 저장소라 생각하자. 그리고 `github page`는 저장소에 올린 글을 브라우저에서 보여주는 페이지라고 생각하면 된다. (실제 정의와 차이가 있다.)

### Git 설치

**내 포스트를 웹에 올리기 위해** `git`을 설치하자. 
[Git 공식 사이트](https://git-scm.com/)에 접속해서 우측에 Download를 진행한 후 그저 Next를 통해 빠르게 설치한다. `git`이 설치가 잘 되었다면 바탕화면에서 `마우스 우클릭`을 눌러보자. `Git GUI Here`과 `Git Bash Here`라는 Context가 생겼을 것이다. `Git Bash Here`을 눌러 Bash를 실행한 후에 아래처럼 입력하자.
 
```bash
$ git --version
```

버전이 출력되는 것이 보이는가? 그럼 설치가 끝난 것이다.


### Github 가입 및 생성

**내 포스트를 웹에 저장하기 위해** `github`에 가입하고 저장소를 생성하자.
설치는 필요 없고 웹에서 가입하고 저장소를 만들 수 있다. [Github 공식 사이트](https://github.com/) 에 접속하여 적당하게 회원가입을 한다. 그리고 로그인을 하게 되면 `New Repository`가 보일 것이다. 클릭하자.

![thumb01](thumb01.png)

`New Repository`를 누르면 저장소를 생성하는 화면이 나온다. 여기서 `Repository Name`와 `Description`을 적어주는데 `Repository Name`은 아래와 같은 형식으로 적어준다.

{% alert danger no-icon %}
Repository Name - **계정이름.github.io**
{% endalert %}

위와 같이 생성하면 블로그를 접속할 도메인은 **`https://계정이름.github.io`**이 될 것이다. 왜 이렇게 생성해야하는 이유는 넘어가도록하겠지만 추후에 도메인 이름을 변경하는 방법을 포스팅하겠다.

## Git 설정
`git`을 설치 후 최초에 한번 기본 설정을 진행하면 된다. 설정은 `이름`과 `email`을 등록하는 것이다. `github`를 가입하고 `git` 설정을 넣은 이유는 설정 시에 복잡하게 생각할 것 없이 `github`로 생성한 아이디나 이메일로 등록하자라는 취지에서 순서를 좀 섞었다. `git`설치 시에 열었던 `git bash`창을 다시 열어 설정을 진행하자.

```bash
$ git config --global user.name 사용자 명
$ git config --global user.email 사용자 이메일
```

## Node.js와 NPM 설치

여기까지 해서 블로그를 저장할 공간과 그 공간에 업로드할 수 있는 도구까지 설치하였다. 이제 우리가 할 일은 저장될 블로그를 만드는 것이다. 블로그는 이 포스트의 타이틀 대로 `hexo`를 이용하여 블로그를 만들 것이다. `hexo`를 사용하기 위해서는 먼저 `node.js`를 설치하여야 한다. [Node.js 공식 사이트](https://nodejs.org/ko/)에서 `6.x` 버전을 다운받은 후 설치하도록 하자.

설치가 완료되었으면 Command( *window 키 + R 후에 cmd 입력*)창에 명령어를 입력해 보자. `node.js`와 `npm`에 대해서는 [빠르게 배우는 Node.js와 NPM 설치부터 개념잡기](https://kdydesign.github.io/2017/07/15/nodejs-npm-tutorial/)를 참고하자.

```bash
$ node -v
```

```bash
$ npm -v
```

위 두 명령어를 입력하여 정상적으로 version이 출력된다면 설치가 완료된 것이다. 

`node.js`는 javascript 런타임으로 생각하고 `npm`은 `node.js`의 오픈 소스 모듈들의 집합 저장소라고 생각하자. 우리는 이 **npm을 통해 hexo를 설치**할 것이다.

## Hexo 설치
이제 hexo를 설치하자. 위에서 `npm`을 통해 hexo를 설치한다고 하였다. 그대로 실행해 보자.

```bash
$ npm install -g hexo-cli
```

명령어 `npm`을 통해 `hexo-cli` 모듈을 `global`하게 설치한다는 명령어이다. 우리는 이 `Hexo`를 통해 여러 가지를 진행할 것이다.

{% alert success no-icon %}
1. 기본 블로그 구조 생성
2. 새로운 포스트 생성
3. github page에 올리기 위해 markdown을 html로 변환
4. local(내 컴퓨터)에서 실행 테스트
5. github에 업로드
{% endalert %}

- - - 

여기까지 해서 필요한 프로그램들을 모두 설치를 완료하였다. 이제 블로그를 만들고 포스팅을 하기만 하면 된다. 블로그를 생성 및 운영하면서 부가적으로 필요한 모듈들은 모두 `npm`을 통해 설치하면 된다. 필요한 모듈은 그때그때 필요할 때 설치하도록 하겠다.

## Hexo 블로그 생성

블로그와 관련된 모든 행동은 hexo명령어로 시작된다. 이는 hexo를 설치할 때 `-g` 옵션을 통해 global로 설치하였기에 가능한 것이다.

이제 블로그를 생성해 보겠다. 먼저 적당하게 폴더를 하나 만든 후에 그 폴더에 접근 후 `Shift + 마우스 우클릭`을 통해 `여기서 명령 창 열기`를 실행하자. 그리고 명령어를 입력하자.

```bash
$ hexo init myBlog
$ cd myBlog
$ npm install
```

`hexo init`명령어를 입력하게 되면 지정된 블로그 명으로 hexo가 알아서 기본적인 블로그를 만들어 준다. 그리고 생성된 블로그 경로로 이동하여 `npm install`명령어를 통해 필요한 모듈을 설치한다. 모듈은 `package.json`에 명시되어 있다.  

만들어진 블로그 폴더를 열어 내용을 확인해보자.

{% alert info no-icon %}
* **node_modules** - hexo 블로그 사용에 필요한 기본적인 node.js 모듈
* **scaffolds** - hexo 페이지를 구성할 기본적인 markdown파일
* **source** - 실제로 포스트를 작성한 파일(markdown)과 이미지 등의 리소스가 저장되는 경로
* **theme** -  테마 파일이 저장되는 경로로 처음 hexo를 설치하게 되면 `landscape` 테마가 설치
* **.gitignore** - git을 통해 github에 블로그를 업로드할 때 업로드를 제외할 파일의 목록을 정의하는 파일
* **_config.yml** - hexo 블로그의 옵션을 지정하는 설정 파일
{% endalert %}

### Hexo 블로그 Github에 연동하기

hexo로 생성한 블로그는 `github`에 업로드해야지만 블로그에 접속하여 확인할 수 있다. 이미 생성한 블로그를 `github`에 업로드하기 위해서는 `git 명령어(add, commit, push)`를 통해서 업로드할 수 있겠지만 **hexo를 사용하면 별도의 git 명령어가 없이도 알아서 github에 업로드**를 해준다. 그러기 위해서는 `hexo`와 `github`간의 연결고리가 있어야 하는데 이 연결고리는 `_config.yml`을 통해 지정할 수 있다.

`_config.yml`을 열어보자.  여러 설정이 있지만 일단 넘어가고 마지막에 있는 `#Depolyment`를 보자. 여기에 `deploy`에 처음에 만든 `github repository`를 적어주면 `github`와 연동되게 된다. 

아래처럼 수정하자.

```yaml
# Deployment
## Docs: https://hexo.io/docs/deployment.html
deploy:
  type: git
  repo: https://github.com/계정이름/계정이름.github.io.git
```

그리고 hexo에서 `github`에 업로드하기 위해 필요한 `npm`모듈을 설치하자. 생성한 블로그 폴더 경로로 이동하여 명령 창을 실행하여 `npm`명령어를 입력하자.

```bash
$ npm install hexo-deployer-git --save
```

위와 같이 설정하고 `hexo deploy` 명령어를 실행하게 되면 `_config.yml`에 작성해둔 주소로 소스를 업로드하게 된다.

`_config.yml`에서는 블로그의 공통적인 속성을 설정할 수 있다. 예를들면 `title`은 블로그의 타이틀을 나타낸다. 자세한 내용은 [HEXO DOCUMENT](https://hexo.io/ko/docs/)에서 확인하고 수정하도록 하자.
### 포스트 생성하기
이제 포스트를 작성해보도록 하자. 모든 것은 hexo를 통해 이루어진다. 생성한 블로그 폴더 경로로 이동하여 명령 창을 실행하여 아래처럼 입력하자.

```bash
$ hexo new post first-post
```

hexo의 `new post [포스트 파일명]`명령어를 입력하게 되면 포스팅이 가능한 파일을 만들어 준다. `Jekyll`과 비교했을 때 `hexo`가 편리하고 좋은 점이 이 부분이다. **단 하나의 명령어 하나로 포스트 파일을 아주 쉽게 만들 수가 있다.**

`블로그명/source/_posts`경로로 가보면 `first-post.md`파일이 생성된 것을 볼 수 있다. `github page`를 사용하기 위해서는 `markdown`언어를 사용하여 글을 작성해야 한다. `markdown`언어는 `md 확장자`를 가지며 [WIKI](https://ko.wikipedia.org/wiki/%EB%A7%88%ED%81%AC%EB%8B%A4%EC%9A%B4)를 참고하면 그리 어려운 언어가 아니다. 모든 포스트는 `markdown`언어로 이루어진다.

생성한 파일을 열어보자. 참고로 `markdown`을 지원하는 에디터는 다양하다. 웹으로도 지원하는 에디터를 참고하여 작성하자. 나는 [StackEdit](https://stackedit.io/)를 사용한다.

```yaml
---
title: first-post
date: 2017-06-30 13:53:51
tags:
---
```

기본 옵션에 대한 설명은 아래와 같다.

{% alert info no-icon %}
**title** - 실제 페이지에 출력될 포스트의 제목
**date** - 포스트를 생성한 날짜(*hexo 빌드 시 date 날짜별로 폴더가 생성*)
**tags** - hexo 블로그에서 관리 될 tag 목록
{% endalert %}

글을 작성해 보자.

```markdown
---
title: first-post
date: 2017-06-30 13:53:51
tags:
---

## 제목
나의 첫번째 포스트입니다.
...
...
```

### Hexo 빌드
우리는 포스트 작성을 `markdown`으로 작성하였다. hexo로 이 `markdown`으로 구성된 파일을 빌드하게 되면 `github page`에 적합한 구조로 재 생성하고 `md`파일들은 `html`파일로 변경해준다.

```bash
$ hexo generate 또는 hexo g
```

빌드 후에 블로그 경로로 들어가보면 `public` 폴더가 생겼을 것이다. 이 안에는 테마에 맞게 css 파일도 생겼고 `first-post.md`파일도 `index.html`로 변경된 것을 볼 수 있다. 포스트는 날짜 별로 폴더가 생성되고 그 안에 생성된다.  `hexo`를 통해 `github`에 파일을 업로드하게 되면 실제로 업로드되는 파일은 이 `public` 폴더가 업로드된다.

### 로컬에서 확인하기

포스트를 작성하고 `generate`까지 하였다면 로컬에서 먼저 확인해보자.

```bash
$ hexo server
```

hexo의 내장 서버 구동하고 브라우저를 실행하여 **http://localhost:4000**으로 접속하자. 그러면 실제로 서비스 될 블로그를 로컬에서 확인할 수 있다.

### Github에 업로드하기

로컬에서 확인하고 수정할 곳이 없다고 판단되면 블로그 소스들을 `github`에 업로드하여 실제 블로그 페이지 띄워 서비스해보자.

```bash
$ hexo deploy 또는 hexo d
```
위의 명령어를 통해  `github`에 업로드를 하며, `generate 명령어`와 동시에 작성할 수도 있다.

```bash
$ hexo g --d
```  

`deploy`가 되었다면 `github`에 접속하여 `계정명.github.io`의 `Repository`를 보자. 파일이 업로드가 되었는가? 그렇다면 브라우저 주소창에 **https://계정명.github.io**를 입력해보자. 우리가 지금까지 해온 결과물이 출력 될 것이다.

- - -

## 요약

`git`, `github page`, `npm`, `node.js`, `hexo` 같은 단어들이 많이 나왔다. 그리고 설명도 복잡해졌다. 하지만 우리는 아무것도 몰라도 된다. ***목적은 포스트를 만들기***이기 때문이다. 간단하게 요약하면 이렇게 된다.

{% alert success no-icon %}
1.  git 설치
2.  github 가입 및 Repository 생성
3.  node.js 설치
4.  npm으로 hexo 설치
5.  hexo로 블로그 생성
6.  hexo와 github 연동
7.  hexo로 새로운 포스트 생성
8.  hexo로 빌드
9.  로컬에서 확인
10. github에 업로드
{% endalert %}

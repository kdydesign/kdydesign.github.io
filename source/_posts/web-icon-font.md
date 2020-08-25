---
title: "Web Icon Font 제작 방법을 배워보자!"
date: 2020-08-25 10:20:57
tags:
- icon-font
- svg
- font
- web font
- web icon font
- fontagon
- material icon
- ionic icon
- fontawesome
categories :
- javascript
- nodejs
- fontagon
- icon font generate
keywords:
- icon font
- web font
- fontagon
- web icon font
- icon font 생성
- icon font 제작
- web font 만들기
- fontagon
- svg
- icon 생성
- vector icon 만들기
- icon font tutorial
disqusIdentifier: web-icon-font
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
흔히 아는 material-icon, font-awesome, ionic-icon은 SVG를 토대로 font 형식으로 생성하여 사용되는 web icon font이다.
보통 위 icon set을 가져다가 쓰겠지만 프로젝트를 하면서 내가 원하는 아이콘이 없다면 어떡할까? 대부분 아이콘은 png로 제작되고 icon font를 생성하여 만들지 않는다.

이번 포스트에서는 매일 가져다가 쓰지 않으며 Image Sprite를 통해서 Image Icon을 사용하지 않는 직접 web icon font를 만들어서 사용하는 방법에 대해 알아보자.
<!-- more -->

<!-- excerpt -->
<!-- excerpt -->

흔히 아는 material-icon, font-awesome, ionic-icon은 SVG를 토대로 font 형식으로 생성하여 사용되는 web icon font이다.
보통 위 icon set을 가져다가 쓰겠지만 프로젝트를 하면서 내가 원하는 아이콘이 없다면 어떡할까? 대부분 아이콘은 png로 제작되고 icon font를 생성하여 만들지 않는다.

이번 포스트에서는 매일 가져다가 쓰지 않으며 Image Sprite를 통해서 Image Icon을 사용하지 않는 직접 web icon font를 만들어서 사용하는 방법에 대해 알아보자.

# Icon Font
`Icon Font`는 SVG 기반의 Vector 그래픽을 Font 파일 화 하여 CSS를 통해서 Icon을 사용하는 방식이다.
수많은 이미지 아이콘을 관리해야 하는 방법과 다르게 단순히 Font 파일과 CSS만 관리하면 된다.
대표적으로는 [Material-Icon](https://material.io/resources/icons/?style=baseline), [FontAwesome](https://fontawesome.com/) 이 있으며, 이 외에 여러 프레임워크에서 자체 Icon Font를 지원하기도 한다.


# 과거와 현재

## Image Sprite

Icon을 표현하고 작업하는 데 있어서 이전에도 그렇고 현재도 동일하게 사용하는 방식은 Image Sprite 방식이다.
Image Sprite는 여러 아이콘을 하나의 큰 이미지에 모두 포함해 CSS의 Position을 이용하여 해당 위치에 있는 아이콘만 보여주는 방식이다.

Image Sprite의 장점은 최소화된 HTTP 요청을 통해 문서에 삽입한다. 하지만 스마트 폰의 활성화와 다양한 DPI를 제공하는 기기들이 늘어나면서 이미지가 강제로 DPI에 맞게 늘어나 뿌옇게 보이거나 깨지는 현상이 발생한다.
이러한 이유로 Sprite 된 이미지의 크기를 변경해야 하거나 수정해야 하는데 이럴 때 불편함을 보인다.

이러한 단점에도 불구하고 장점이 더욱더 많기 때문에 현재까지도 많이 사용되는 방식이다.


## Web Font

현재에 와서 이렇게 다양한 디스플레이 크기에 픽셀 기반의 이미지는 대응하지 못하기 때문에 온전한 이미지를 대체하기 위해 초기에는 SVG를 사용했지만, 구형 브라우저 및 모던 브라우저들이 당시에는 SVG를 지원하지 못했다.
이를 극복하기 위해 Vector 형식의 아이콘을 Web Font로 만들어서 사용하였는데 이러한 방식이 많이 애용되면서 `FontAwesome`이란 Vector 기반의 Web Font가 무료로 제공되기 시작했다.
이 `FontAwesome`을 시작으로 다양한 `Web Icon Font`가 개발되기 시작했다.


# 추이

10년간의 `FontAwesome`과 `Material-Icon`의 추세를 보면 계속 증가하는 추세로 보이며, Icon Font의 선두주자답게 `FontAwesome`에 대한 관심도가 가장 높은 것으로 보인다.

<script type="text/javascript" src="https://ssl.gstatic.com/trends_nrtr/2213_RC01/embed_loader.js"></script> <script type="text/javascript"> trends.embed.renderExploreWidget("TIMESERIES", {"comparisonItem":[{"keyword":"fontawesome","geo":"","time":"2010-01-01 2020-08-05"},{"keyword":"material icon","geo":"","time":"2010-01-01 2020-08-05"}],"category":0,"property":""}, {"exploreQuery":"date=2010-01-01%202020-08-05&q=fontawesome,material%20icon","guestPath":"https://trends.google.co.kr:443/trends/embed/"}); </script>


# Icon Font 장점

**1. 하나의 글꼴 파일에 다양한 아이콘을 넣어두고 사용**

Image Sprite와 비슷하게 Icon Font도 모든 Icon을 Font 파일 하나에 넣어서 사용이 가능하다.
Image Sprite는 모든 Icon을 담기에는 무리가 있기에 형태 별, 종류별로 분리를 하지만 Icon Font는 구분 없이 모든 아이콘을 하나로 관리할 수 있다. 그렇기 때문에 HTTP 요청 역시 단 한 번만 진행된다.


**2. CSS로 확장하여 모든 작업이 가능**

Image Icon과 동일하게 CSS를 통해서 크기, 변형, 회전 등 모든 작업이 가능하다. 특히 `color`를 사용한다면 하나의 아이콘으로도 여러 가지 색을 가진 Icon을 표현할 수 있다.


**3. Vector Graphic이기 때문에 크기 변형에 제한이 없음**

픽셀 기반의 Image는 기본 크기에 비례하여 확대할 경우 이미지가 깨지는 현상을 볼 수 있는데 Icon Font는 Vector 기반으로 연산 된 그래픽 이기 때문에 제한 없이 확대를 한다 하더라도 Icon 형태 그대로 유지 할 수 있다.


**4. Unicode 또는 Ligature 사용**

Image Icon의 경우 CSS로 class를 정의하여 해당 class만을 사용하지만, Icon Font의 경우 Unicode 및 Ligature를 사용할 수 있다.
Ligature는 Icon Font로 생성된 CSS의 class를 사용하지 않고 Text 형식으로 사용할 수 있다.

아래 코드를 보자.
 
{% codeblock Ligature lang:html%}
<span class="icon-class sub-class">arrow_up</span>
{% endcodeblock %}


해당 코드에서 arrow_up은 Icon Font에서 Ligature이다. CSS class를 통한 사용이 아닌 Text 형식으로 삽입하게 되면 Icon이 출력되게 되어 있다.
만약 CSS를 통한 사용이 된다면 아래와 같을 것이다.

{% codeblock Ligature - CSS lang:html%}
<span class="icon-class sub-class icon-arrow_up"></span>
{% endcodeblock %}

Unicode 및 Ligature의 key는 SVG를 Font 파일로 변환 시 지정할 수 있으며, 수많은 아이콘 중 Unicode를 사용하면 특정 아이콘만 사용이 가능하다.

{% alert info no-icon %}
Locale 별 서로 다른 아이콘이 Font 파일에 있을 경우 모두 사용될 필요는 없다. 이럴 경우에 Unicode를 사용하여 해당 지역에서 사용되는 Icon만 사용할 수 있다.
{% endalert %}


**5. 전체 서체보다 적은 문자를 포함하여 파일의 크기가 작음**

Icon Font 역시 Font 파일이지만 일반 서체용 Font 파일보다는 단순하게 아이콘만 저장되어 있기 때문에 일반 Font보다 파일의 용량이 적다.
Image Icon으로 비교해 보자면 약 1,000개의 Image Icon이 1.3MB라고 할 경우 동일하게 1,000개의 Icon을 Icon Font로 만들 경우 5KB밖에 되지 않는다.


# Icon Font 단점

이렇게 장점이 많지만 단 하나의 단점이 있다. 이 단점으로 인해 모든 Icon을 Icon Font로 만들지 못하는 이유이다.


**다양한 색상의 Icon 표현 불가**

Icon Font 자체만 놓고 보았을 때는 Font 파일이다. Font 파일의 글꼴은 색상 정보가 포함되어 있지 않기 때문에 여러 색상을 가진 Icon Font는 생성할 수 없다.
굳이 하자면 여러 글리프를 색상별로 분리해 놓고 하나로 겹쳐 하나의 폰트처럼 보일 수 있지만 이렇게 하면 아이콘 제작에 많은 시간을 투자하게 되기 때문에 효율 적이지 않다.

{% alert info no-icon %}
여러 글리프를 겹쳐 하나의 글꼴을 만드는 것을 [크로마 틱](https://www.myfonts.com/search/chromatic/) 글꼴이라고 한다.
{% endalert %}


# Icon Font 생성 도구

Icon Font를 가장 쉽게 만들 방법은 도구를 사용하는 것이다. 이미 상용화된 소스들이 많을뿐더러 SVG만 있다면 누구나 SVG를 통하여 Icon Font로 제작할 수 있다.
대표적인 도구로는 [IcoMoon](https://icomoon.io/), [Glyphter](https://glyphter.com/), [Fontello](http://fontello.com/)가 있으며 웹 페이지에 SVG를 업로드하면 Font 파일로 변환하여 다운로드할 수 있다.
이 과정에서 대부분 위에서 언급한 `Unicode` 및 `Ligature`를 설정하거나 볼 수 있다.


# Icon Font 제작 도구

Icon Font 제작을 위해서는 SVG를 생성하고 이 SVG를 Font 파일 및 CSS로 변환해야 한다. 이러한 과정을 도와주는 여러 가지 도구가 있어서 소개하고 간략하게 집고 넘어가자.

## SVG 생성 도구

Icon Font로 생성하기 SVG는 보통 일러스트를 통해서 제작한다. 어떤 방법이든 SVG를 만들면 되지만 일러스트의 경우 유료라이센스이며 [inkscape](https://inkscape.org/ko/)는 무료 라이센스이기 때문에 선택에 따라서 사용하면 된다.

## Fontagon

Icon Font 변환 도구를 통해서 Icon Font를 제작할 수 있지만, 자체 내 Build System 구축을 하고 싶다면, [Fontagon](https://github.com/kdydesign/fontagon)을 보자.
`Fontagon`은 [Webfonts-Generator](https://www.npmjs.com/package/webfonts-generator)를 기반으로 재구축한 오픈 소스이며, Build System을 지원할 뿐만 아니라 CLI를 통하여 간단하고 빠르게 SVG를 Font로 변환할 수 있다.

Fontagon을 사용하면 SVG를 모든 형식의 폰트 파일로 생성할 수 있으며, 이 폰트를 사용이 가능하도록 CSS를 구성해 준다. 사용자는 만들어져 있는 CSS의 class만을 사용하면 된다.

Fontagon의 기능은 다음과 같다.

* WOFF2, WOFF, TTF, EOT, TTF, SVG를 지원
* CSS, Sass, Less 모두 지원 및 생성
* 사용자 정의 CSS Template 생성 가능
* ligature 지원


{% alert info no-icon %}
**Font 종류 및 특징**

* **eot**: IE 전용, 기본적으로 압축되지 않음
* **ttf**: 부분적인 IE 지원, 기본적으로 압축되지 않음
* **woff**: 지원 범위가 가장 넓지만 몇몇 이전 브라우저에서는 사용 불가, 압축이 기본적으로 지원
* **woff2**: 현재 많은 브라우저에서 지원, 맞춤형 처리 및 압축 알고리즘을 사용하여 다른 폰트 형식보다 30% 파일 크기 절감
{% endalert %}

### Fontagon 설치
Fontagon-CLI는 Global로 설치하여 사용 할 수 있다.
   
```sh
$ npm install fontagon
$ npm install -g fontagon-cli  // cli 
```

### Fontagon을 사용한 Build Script 생성
Fontagon의 옵션은 [Document](https://github.com/kdydesign/fontagon/tree/master/packages/fontagon)에서 확인해보자.

{% codeblock index.js lang:javascript%}
const Fontagon = require('fontagon')

Fontagon({
  files: [
    'path/**/*.svg'
  ],
  dist: 'dist/',
  fontName: 'fontagon-icons',
  style: 'all',
  classOptions: {
    baseClass: 'fontagon-icons',
    classPrefix: 'ft'
  }
}).then((opts) => {
  console.log('done! ' ,opts)
}).catch((err) => {
  console.log('fail! ', err)
})
{% endcodeblock %}


### Fontagon 사용
Fontagon을 통해서 Build가 진행되면 CSS 파일이 추출된다. 이 CSS 파일에는 같이 추출된 Font 파일들을 Import하고 있으며 해당 CSS를 삽입하여 사용하면 된다.

```html
<link rel="stylesheet" type="text/css" href="dist/fontagon-icons.css">
```

```javascript
import '../dist/fontagon-icons.css'
```

```html
<i class="fontagon-icons ft-icon">SVG FILE NAME</i>
<i class="fontagon-icons ft-icon ft-SVG FILE NAME"></i>
```

- - -

단점에서 설명했듯이 Icon Font 하나만으로는 사용이 불가능하기 때문에 Image Icon 역시 같이 사용해야 한다.
하지만 같이 사용한다 하더라도 많은 양의 리소스를 줄일 수 있으며, Icon Font를 사용하면 확실히 이점을 남길 수 있다.

이전부터 Material-Icon과 FontAwesome을 대다수가 사용하면서 목적과 디자인이 다른 웹 페이지 및 애플리케이션들이 어딘가 모르게 비슷한 느낌을 준다. 본인이 어떤 프로젝트를 하고 있고 차별화된 느낌을 주면서 효율성도 챙기고 싶다면 회사, 디자이너, 퍼블리셔에서 Icon Font 제작을 권해보자.
  

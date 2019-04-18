---
title: "Webpack 완전정복하기!!"
date: 2017-11-04 20:08:50
tags: 
- nodejs
- javscript
- webpack
- build tool
- gulp
- webpack
categories :
- javascript
- nodejs
- build tool
- webpack
keywords:
- javascript
- nodejs
- webpack
- gulp
- javscript build tool
disqusIdentifier: webpacktutorial
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
지금까지 우리는 webpack에 대한 개념을 먼저 살펴보았다. 이제 실제로 webpack을 설치해보고 사용해 보면서 하나하나 짚어나가 보자. 왜 webpack이 많이 사용되는지와 `Gulp`와의 차이점을 알았다면 이제 실제로 webpack을 설치해보고 사용해 보면서 하나하나 짚어나가 보자. 
<!-- more -->

<!-- excerpt -->
<!-- excerpt -->

![cover](cover.png)

지금까지 우리는 [Webpack 개념잡기](https://kdydesign.github.io/2017/07/27/webpack/) 포스트에서 webpack에 대한 기본 개념을 먼저 살펴보았다. 왜 webpack이 많이 사용되는지와 `Gulp`와의 차이점을 알았다면 이제 실제로 webpack을 설치해보고 사용해 보면서 하나하나 짚어나가 보자. **이 포스트에 올린 예제들은 [webpack 공식 사이트](https://webpack.js.org/)들의 예제를 포함하고 있다.**


# Webpack 설치 및 Build

webpack은 npm으로 쉽게 설치할 수 있다. 만약 이 포스트를 보는 당신은 npm이 무엇인지 모른다면 [빠르게 배우는 Node.js와 NPM 설치부터 개념잡기](https://kdydesign.github.io/2017/07/15/nodejs-npm-tutorial/) 포스트를 참고하자. 자! 이제 설치를 해보자. 먼저 적당한 경로에 `Webpack_Project`라는 이름의 프로젝트 폴더를 생성하고 해당 폴더에서 명령 프롬프트를 실행하여 `webpack`을 설치하자.

```sh
$ npm init -y
$ npm install webpack --save-dev
```

먼저 `npm init -y`를 통해 package.json을 생성하고 `npm install webpack --save-dev`명령을 통해 webpack을 설치하면서 동시에 package.json에 적용하였다. 실제로 webpack의 설치는 이것으로 끝이다. 우리는 항상 설치가 정상적으로 됐는지 확인은 버전으로 확인을 한다. 확인해보자.

```sh
$ .\node_modules\.bin\webpack -v
```

버전이 출력된다면 정상적으로 설치가 완료된 것이다.


## CLI를 사용한 Build

가장 기초적인 방법으로 `webpack cli`명령어를 통해 javascript를 build 해 보자. 테스트에 필요한 파일은 `index.js`와 `index.html`이다.

```javascript
//index.js

function component() {
	var element = document.createElement('div');
	element.innerHTML = 'Hello Webpack!!';

	return element;
}

document.body.appendChild(component());
```

```html
<!-- index.html -->

<!-- ... -->
<body>
	<script type="text/javascript" src="bundle.js"></script>
</body>
<!-- ... -->
```

코드는 간단하다. `Hello Webpack!!`이라는 문구를 출력할 뿐이다. 그런데 html에서는 조금 다르다. 먼저 .js파일을 불러오는 것은 이해가 되지만 우리가 만든 파일은 `index.js`인데 왠 `bundle.js`라는 파일을 호출하였을까. 일단 궁금증은 접어두고 webpack을 통해 build를 해보자.

```sh
$ .\node_modules\.bin\webpack index.js bundle.js
```

여기서 `bundle.js`가 나왔다. 대강 이해가 가는가? 우리는 위에 있는 cli를 통해 `index.js`를 `bundle.js`로 build 한 것이다. 그렇기 때문에 `index.html`에서는 처음에는 존재하지는 않지만, build 후에 생성 될 `bundle.js`를 호출한 것이다. 비록 지금은 코드나 그 프로젝트 구조가 복잡하지 않기 때문에 별 느낌이 없을지 모르겠지만 이 포스트를 끝까지 읽는다면 어느 정도 감이 올 것이다.


## config를 사용한 Build

cli를 통한 build는 단순한 구조의 파일을 build 하기에는 편하지만 실제로 우리가 어떤 프로젝트에 임하면 그 프로젝트는 `절.대.로` 간단한 구조로 되어 있지 않다. build 시에 더욱 부가적인 요소들을 요구하며 이 요소들을 통하여 build를 하게 된다. 이렇게 복잡한 build의 경우 webpack에서는 어떤 특정한 설정 파일에 build에 필요한 요소들을 나열하고 해당 설정 파일을 통해 build를 진행하게끔 지원한다.

먼저 `Webpack_Project` 경로에 `webpack.config.js`라는 javascript 설정 파일을 만들고 간단한 설정부터 진행하자.

```javascript
//webpack.config.js

var path = require('path');

module.exports = {
	entry: './index.js',
	output: {
        filename: 'bundle.js',
        path: path.resolve(__dirname, 'dist')
    }
};
```

이렇게 작성된 설정 파일은 webpack 명령어를 통해 실행할 수 있다. (물론 실행 시에는 해당 디렉토리 경로에서 실행하자.)

```sh
$ .\node_modules\.bin\webpack
```

결과는 `webpack cli`명령어를 통하여 build 한 내용과 동일하지만 `bundle.js`의 생성 위치가 다르다. 하나씩 살펴보자. 

{% alert danger no-icon %}
* **path** - 파일의 경로를 다루고 변경하는 유틸리티
* **output** - build 결과를 저장할 경로
* **entry** - build의 대상이 될 파일 
{% endalert %}

처음 우리가 webpack cli를 통해 build 할 때는 build 될 대상과 build 된 파일을 명시해줬지만 여기서는 그저 webpack 이라는 단순한 명령어를 사용하였다. 그 이유는 우리가 webpack의 설정을 정의한 `webpack.config.js`를 생성하였고 이 파일은 webpack 명령어의 기본 파일이기 때문이다. 만약 우리가 설정파일이 `webpack.config.js`가 아닌 `webpack.build.js`와 같은 다른 파일로 정의를 하였다면 아래와 같은 명령어를 통해 실행 할 수 있다.

```sh
$ .\node_modules\.bin\webpack --config webpack.build.js
```

# Loader 사용하기

우리는 이전 포스트인 [Webpack 개념잡기](https://kdydesign.github.io/2017/07/27/webpack/)에서 `webpack은 크게 Entry, Output, Loader, Plug-In 이 4가지로 나눌 수 있다.` 라고 하였다. 이미 앞서 webpack을 설치하고 build 해 보면서 `entry`와 `output`이 무엇인지 대강 감을 잡았으니 이제 파일을 사전 처리하여 정적인 리소스들을 javascript와 같이 하나의 bundle로 만들 수 있는 `Loader`를 알아보자.


## style-loader, css-Loader

`style-loader`와 `css-loader`는 같이 사용되며 `style-loader`는 `<style>`태그를 삽입하여 CSS를 추가해주는 역할을 한다. 모든 설치는 npm을 통해 설치를 진행한다.

```sh
$ npm install style-loader css-loader --save-dev
```

설치가 완료되었으면 `webpack.config.js`에 `style-loader`와 `css-loader`를 정의하자.

```javascript
//webpack.config.js

var path = require('path');

module.exports = {
	entry: './index.js',
	output: {
        filename: 'bundle.js',
        path: path.resolve(__dirname, 'dist')
    },
    module: {
	    rules: [
	     	{
	        	test: /\.css$/,
	        	use: [
	         		'style-loader',
	          		'css-loader'
	        	]
	      	}
	    ]
  	}
};

```

loader는 `module`에 추가해주며, 정규식(test)을 통해 loader가 인식될 파일을 잡아준다. 그리고 어떤(use) loader를 사용하는지 정의해 주면 된다. 이제 `style.css`파일을 추가하고 `index.js`파일을 수정하자.

```css
/* style.css */

.hello {
	color: red;
}
```

```javascript
//index.js

import './style.css';

function component() {
	var element = document.createElement('div');
	element.innerHTML = 'Hello Webpack!!';
	element.classList.add('hello');

	return element;
}

document.body.appendChild(component());
```

우선 추가된 코드는 `hello`클래스와 이 클래스를 element에 추가하는 코드이다. 코드는 어렵지 않다. 그런데 왜 `style.css`를 `index.html`에 `<link>` 태그나 `<style>`태그를 통해 삽입하지 않고 `index.js`에 삽입을 하였을까? 이유는 처음에 설명한 style-loader의 역할 때문이다. 이렇게 `index.js`에 `style.css`를 명시하고 이 `index.js`를 build하게 되면 `loader`를 통해 `style.css`의 클래스는 `<script>`태그로 CSS가 추가되도록 되어 있다.

위 코드를 build하여 실행하고 결과를 확인해 보도록 하자.


## file-loader

`file-loader`를 사용하면 시스템에 존재하는 파일. 즉 이미지나 폰트와 같은 자산들을 하나로 통합할 수 있다. 사용 방식은 위에서 설명한 css-loader와 style-loader와 동일하다. `file-loader`를 먼저 설치하고 `webpkac.config.js`를 열어 loader를 추가하자.

```sh
npm install file-loader --save-dev
```

```javascript
//webpack.config.js

var path = require('path');

module.exports = {
	entry: './index.js',
	output: {
        filename: 'bundle.js',
        path: path.resolve(__dirname, 'dist')
    },
    module: {
	    rules: [
	     	{
	        	test: /\.(png|svg|jpe?g|gif)$/,
	        	loader:'file-loader'
	      	}
	    ]
  	}
};
```

여기서 loader를 보면 `css-loader`와 `style-loader`에서 사용한 `user:[]`가 사용되지 않고 `loader`로 사용되었다. 둘 다 적용이 가능한 옵션이며, `use:[]`경우 여러 `loader`를 지정할 때 사용되며 `loader`는 단일로 사용이 된다. 또한 각 `loader`는 각각의 특성에 따라 옵션을 지정할 있으며 아래와 같이 정의 할 수 있다.

```javascript
//example...

 module: {
	    rules: [
	     	{
	        	test: /\.(png|svg|jpe?g|gif)$/,
	        	loader:'file-loader',
	        	option: {
	        		name: '[hash].[ext]'
	        	}
	      	}
	    ]
  	}
//...
```

이어서 가자. file-loader를 정의 하였으니 `Webpack_Project`안에 `asset`폴더를 하나 만들고 `image.png`파일과 같은 이미지 파일을 넣어놓자. 이렇게 넣어 놓은 이미지 파일을 `index.js`에서 불러 올 것이다.

```javascript
//index.js

import './style.css';
import './asset/image.png';

function component() {
	var element = document.createElement('div');
	element.innerHTML = 'Hello Webpack!!';
	element.classList.add('hello');

	var myIcon = new Image();
    myIcon.src = Icon;

    element.appendChild(myIcon);

	return element;
}

document.body.appendChild(component());
```

이제 다시 build 하고 확인해 보자.

해당 예제는 이미지로 진행하였지만 폰트 역시 동일하다. 다른게 있다면 폰트의 확장자를 통해 걸러내는 정규식이 다를 뿐이다.

```javascript
//example...

 module: {
	    rules: [
	     	{
	        	test: /\.(woff|woff2|eot|ttf|otf)$/,
	        	loader:'file-loader'
	      	}
	    ]
  	}
//...
```

## url-loader

`file-loader`를 사용해 보았다면 한 번쯤 생각해 볼 것이다. 웹을 표한하는데 있어서 리소스를 가장 많이 잡아먹는 것 중 하나가 이 이미지 파일들인데 이 파일을 더 효율적으로 관리 할 수 없을지 말이다. webpack에서는 이 단계 이후에 진행될 논리적 단계는 `이미지를 축소하고 최적화하는 것이다.` 라고 말한다. `url-loader`는 이 이미지 로딩 프로세스를 향상 시킬 수 있는 하나의 방법이며, 특정 파일을 `base64`로 인코딩된 URL를 로드해주는 역할을 한다.

`url-loader`를 설치하고 `webpack.config.js`를 열어 `url-loader`를 추가해 주자.

```sh
npm install url-loader --save-dev
```

```javascript
//webpack.config.js

var path = require('path');

module.exports = {
	entry: './index.js',
	output: {
        filename: 'bundle.js',
        path: path.resolve(__dirname, 'dist')
    },
    module: {
	    rules: [
	     	{
	        	test: /\.(png|svg|jpe?g|gif)$/,
	        	loader:'url-loader',
	        	options: {
	              limit: 10000
	            }
	      	}
	    ]
  	}
};
```

`url-loader`는 `file-loader`와 같이 작동한다. 그렇기에 정규식 역시 동일하지만 다른 점은 `limit`이라는 옵션을 준 것이다. `options`에 `limit`는 파일의 크기를 말하는데 현재 예제에서 10KB 미만은 `url-loader`로 처리가 되고 그 이상의 파일은 `file-loder`와 같이 처리가 된다.

다시 build를 하고 `dist`폴더를 확인해 보자. 해당 이미지 파일이 존재하지 않는 것을 확인할 수 있다. 만약 파일이 존재한다면 파일의 용량을 확인해 보고 그 용량 이상의 값을 `limit`에 적용해보다. 그리고 브라우저를 열어 실제로 파일이 `base64`로 인코딩이 되었는지 확인해 보자.

- - - 

지금까지 `Loader`를 알아 보았는데 여기서 언급한 `Loader`이외에도 `xml-loader`, `babel-loader`, `i18n-loader` 등과 같이 효율적인 `Loader`들이 무수히 존재한다. 해당 `Loader`들은 [Webpack - Loader](https://webpack.js.org/loaders/)에서 확인해 보자.


# Plug-In

webpack은 풍부한 Plug-In이 있으며 webpack 자체의 대부분의 기능은 이 Plug-In을 사용한다. Plug-In 을 통해 우리가 할 수 있는 일들은 build 된 bundle 파일을 동적으로 특정 html 페이지에 추가 할 수 있으며 build 시에 javscript, css, html 등의 파일을 난독화 및 압축을 진행할 수 있다. 이 외에도 많은 기능을 지원하며 필수 적으로 사용한다 해도 무방하다. 그럼 몇 가지 Plug-In을 살펴보겠다.

## html-webpack-plugin

엔트리 포인트 중 하나의 모듈의 이름을 변경하거나 새로운 것을 추가하는 경우 생성된 번들은 빌드에서 이름이 변경되지만 `index.html`에 script는 여전히 이전의 이름을 참조한다. 그렇게 때문에 우리는 주기적으로 번들링 된 파일을 `index.html`에 삽입을 시켜야하는 번거로움이 있다. 이런 불편함을 `html-webpack-plugin`이 해결해 준다. `html-webpack-plugin`은 정의되어있는 기본 template을 기준으로 번들링 시에 새로운 html 파일을 생성해 준다. 이때 파일을 생성할 때 번들링된 javascript 파일을 삽입해준다. 

`html-webpack-plugin`을 설치하고 `webpack.config.js`에 추가해 주자.

```sh
npm install html-webpack-plugin
```

```javascript
//webpack.config.js

var path = require('path');
const HtmlWebpackPlugin = require('html-webpack-plugin');

module.exports = {
	entry: './index.js',
	output: {
        filename: 'bundle.js',
        path: path.resolve(__dirname, 'dist')
    },
    plugins: [
        new HtmlWebpackPlugin({
            favicon: './static/asset/favicon.ico',
            template: './static/index.html',
            chunks: ['css', 'index', 'app', 'system', 'monitor']
        })
    ]
};
```

## commonChunk
`commonChunk` Plug-In은 여러 개의 엔트리 포인트 사이에서 공유되는 공통 모듈로 구성된 파일(Chunk)을 별도의 엔트리로 분리함으로써 종속성을 관리 할 수 있다. 예를 들면 어떤 프로젝트에서 jquery를 사용하고 jquery를 필요로 하는 모든 모듈에 jquery를 참조한다고 했을 때 이후 build를 하게 되면 jquery 모듈이 중복되는데 이렇게 common하게 사용되는 모듈을 여러 모듈이 참조를 한다고 하더라도 `commonChunk`를 사용하여 build 시에 하나의 별도의 vendor 모듈로 분리 할 수 있다.

`commonChunk`는 webpack의 내장 모듈이기 때문에 별도의 설치는 필요하지 않다. 대신에 webpack을 참조해야 한다.

```javascript
//webpack.config.js

var path = require('path');
var webpack = require('webpack');
const HtmlWebpackPlugin = require('html-webpack-plugin');

module.exports = {
	entry: './index.js',
	output: {
        filename: 'bundle.js',
        path: path.resolve(__dirname, 'dist')
    },
    plugins: [
        new HtmlWebpackPlugin({
            favicon: './static/asset/favicon.ico',
            template: './static/index.html',
            chunks: ['css', 'index', 'app', 'system', 'monitor']
        }),
        new webpack.optimize.CommonsChunkPlugin({
           name: 'common' 
        })
    ]
};
```

## clean-webpack-plugin
우리는 `webpack.config.js`에 build 시 output을 통해 어디로 가는지 지정을 해줬다. `clean-webpack-plugin`은 이 output 디렉토리를 build를 할때마다 삭제를 해주는 Plug-In이다.

```sh
npm install clean-webpack-plugin
```

```javascript
//webpack.config.js

var path = require('path');
var webpack = require('webpack');
const HtmlWebpackPlugin = require('html-webpack-plugin');
var CleanWebpackPlugin = require('clean-webpack-plugin');

module.exports = {
	entry: './index.js',
	output: {
        filename: 'bundle.js',
        path: path.resolve(__dirname, 'dist')
    },
    plugins: [
        new CleanWebpackPlugin(['dist']),
        new HtmlWebpackPlugin({
            favicon: './static/asset/favicon.ico',
            template: './static/index.html',
            chunks: ['css', 'index', 'app', 'system', 'monitor']
        }),
        new webpack.optimize.CommonsChunkPlugin({
           name: 'common' 
        })
    ]
};
```


## uglify

javascript 소스를 보게 되면 `xxx.min.js` 라는 파일과 그 안의 코드는 알아볼 수 없는 형태로 되어있는 것을 봤을 것이다. 이는 난독화와 압축을 진행했기 때문인데 javascript를 build 할 때 다른 중요한 부분은 난독화와 압축이다. 이 프로세스를 걸침으로 인해 내부 코드의 내용을 쉽게 파악하지 못하게 함과 파일의 용량을 줄일 수 있다. 압축하는 방법이야 여러 가지가 있지만 `uglify`는 간단하게 난독화와 압축을 진행할 수 있는 Plug-In이다.


```sh
npm install uglifyjs-webpack-plugin
```

```javascript
//webpack.config.js

var path = require('path');
var webpack = require('webpack');
const HtmlWebpackPlugin = require('html-webpack-plugin');
const UglifyWebpackPlugin = require('uglifyjs-webpack-plugin');

module.exports = {
	entry: './index.js',
	output: {
        filename: 'bundle.js',
        path: path.resolve(__dirname, 'dist')
    },
    plugins: [
        new HtmlWebpackPlugin({
            favicon: './static/asset/favicon.ico',
            template: './static/index.html',
            chunks: ['css', 'index', 'app', 'system', 'monitor']
        }),
        new webpack.optimize.CommonsChunkPlugin({
           name: 'common' 
        }),
        new UglifyWebpackPlugin()
    ]
};
```

## provider

`webpack.ProvidePlugin`을 통해 등록된 모듈을 자유 변수로 사용이 가능하다.

```javascript
//webpack.config.js

var path = require('path');
var webpack = require('webpack');
const HtmlWebpackPlugin = require('html-webpack-plugin');
const UglifyWebpackPlugin = require('uglifyjs-webpack-plugin');

module.exports = {
	entry: './index.js',
	output: {
        filename: 'bundle.js',
        path: path.resolve(__dirname, 'dist')
    },
    plugins: [
        new HtmlWebpackPlugin({
            favicon: './static/asset/favicon.ico',
            template: './static/index.html',
            chunks: ['css', 'index', 'app', 'system', 'monitor']
        }),
        new webpack.optimize.CommonsChunkPlugin({
           name: 'common' 
        }),
        new UglifyWebpackPlugin(),
        new webpack.ProvidePlugin({
		  $: 'jquery',
		  jQuery: 'jquery',
		  _:'underscore'
		})
    ]
};
```

```javascript
//modual A

$('<div>');
jQuery('<div>');
var array = _.map([1, 2, 3], function(num){
	 return num * 3; 
	});

```

- - - 

`Loader`에 이어 `Plug-in`을 알아보았다. 이밖에 `Plug-in`은 [WEbpack Plugin-IN](https://webpack.js.org/plugins/)을 참고하자.


# DevServer && HMR

`DevServer`는 webpack의 주요 기능 중 하나이다. 실제로 우리는 자산들을 bundling 후에도 테스트가 필요하다. 또한 자산의 추가, 수정, 삭제에 따라 반영 작업이 필요한데 webpack의 DevServer를 이용한다면 매우 편리하게 개발에 임할 수 있다. DevServer는 말 그대로 개발 서버이며 이와 관련된 또 하나의 webpack 주요 기능인 `HMR(Hot Module Replacement)`가 있다. 이 `핫 모듈 교체(한국어 풀이)`는 특정 모듈이 변경되더라도 새로고침 할 필요없이 런타임에 모든 종류의 모듈을 업데이트해 주는 기능이다. 이 기능을 사용하기 위해서는 DevServer의 설정을 추가하고 webpack에 내장된 HMR 플러그 인을 사용하는 것 뿐이다. 그렇기에 DevServer와 같이 설명하려 한다. HMR의 자세한 내용은 [webpack hmr](https://webpack.js.org/guides/hot-module-replacement/)을 참고하자.

살을 덧붙여 요약을 하자면.

{% alert success no-icon %}
* webpack-dev-server는 빠른 실시간 리로드 기능을 갖춘 개발 서버
* webpack-dev-serve는 디스크에 저장되지 않는 메모리 컴파일을 사용하기 때문에 컴파일 속도가 빨라짐
* webpack.config.js에도 devServer 옵션을 통해 옵션을 지정하여 사용이 가능
{% endalert %}

`webpack-dev-server`의 간략한 프로세스는 이렇다.

{% alert success no-icon %}
1. 서버 실행 시 소스 파일들을 번들링하여 메모리에 저장
2. 소스 파일을 감시하고 있다가 소스 파일이 변경되면 변경된 모듈만 새로 번들링
3. 변경된 모듈 정보를 브라우저에 전송
4. 브라우저는 변경을 인지하고 새로고침되어 변경사항이 반영된 페이지를 로드
{% endalert %}


이제 `webpack-dev-server`를 설치하고 설정을 적용해보자.

```sh
npm install webpack-dev-server --save-dev
```

```javascript
//webpack.config.js

var path = require('path');
var webpack = require('webpack');
const HtmlWebpackPlugin = require('html-webpack-plugin');
const UglifyWebpackPlugin = require('uglifyjs-webpack-plugin');

module.exports = {
	entry: './index.js',
	output: {
        filename: 'bundle.js',
        path: path.resolve(__dirname, 'dist')
    },
    plugins: [
        new HtmlWebpackPlugin({
            favicon: './static/asset/favicon.ico',
            template: './static/index.html',
            chunks: ['css', 'index', 'app', 'system', 'monitor']
        }),
        new webpack.optimize.CommonsChunkPlugin({
           name: 'common' 
        }),
        new UglifyWebpackPlugin(),
        new webpack.ProvidePlugin({
		  $: 'jquery',
		  jQuery: 'jquery',
		  _:'underscore'
		})
    ],
    devServer: {
      host : '127.0.0.1',
	  contentBase: path.join(__dirname, "dist"),
	  compress: true,
	  hot : true,
	  inline: true,
	  port: 9000,
	  open : true
	}
};
```

devServer의 설정을 보면 감이 올 것으로 생각된다. 간단한 설명으로 넘어가겠다.

|option      | description                                            | CLI 사용                                                 |
|------------|--------------------------------------------------------|---------------------------------------------------------|
|host        | 사용될 호스트 지정                                       | webpack-dev-server --host 127.0.0.1                      |
|contentBase | 콘텐츠를 제공할 경로지정(정적파일을 제공하려는 경우에만 필요) | webpack-dev-server --content-base /path/to/content/dir   |
|compress    | 모든 항목에 대해 gzip압축 사용                            | webpack-dev-server --compress                            |
|hot         | webpack의 HMR 기능 활성화                                | -                                                        |
|inline      | inline 모드 활성화                                       |webpack-dev-server --inline=true                          |
|port        | 접속 포트 설정                                           | webpack-dev-server --port 9000                           |
|open        | dev server 구동 후 브라우저 열기                          | webpack-dev-server --open                                |


`webpack-dev-server`의 구동은 CLI로 실행을 하고 이 CLI를 npm script에 등록하여 할 수 있다.

```sh
$ ./node_modules/.bin/webpack-dev-server --config webpack.config.js
```

open 옵션으로 인해 서버가 구동 후 브라우저가 열리는 것을 볼 수 있다. 여기서 F12를 통해 개발자 콘솔을 열고 모듈을 변경, 수정하면서 console 창을 확인해 보자. 당신은 지금 `HMR`이라는 훌륭한 기능을 보고 있는 것이다.

- - -

여기까지 해서 webpack의 핵심적인 사용법을 알아보았다. webpack에 대한 디테일한 가이드는 [webpack guides](https://webpack.js.org/guides/)를 참고하면서 하나씩 따라 해보자. 

webpack은 초기 설정이 까다롭게 느껴질 수 있다. 당연한 것이다. webpack 자체의 configulation과 Loader, plug-in 제각기 옵션이 존재하기 때문이다. 하지만 초기 설정만 끝난다면 webpack이 왜 떠오르고 많이 사용하는지 몸소 느낄 것이다. 현재 내가 진행하고 있는 프로젝트에도 webpack을 도입하기로 하였기에 Test하고 Prototype을 만들고 실제로 프로젝트에 적용해 보면서 매번 정말 훌륭하다고 느껴진다. Web Front-End의 Bundling tool을 고민하는 당신에게 적극적으로 추천한다.
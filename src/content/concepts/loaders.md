---
title: Loaders
sort: 4
contributors:
  - manekinekko
  - ev1stensberg
  - SpaceK33z
  - gangachris
  - TheLarkInn
  - simon04
  - jhnns
---

<!--Loaders are transformations that are applied on the source code of a module. They allow you to pre-process files as you `import` or “load” them. Thus, loaders are kind of like “tasks” in other build tools, and provide a powerful way to handle front-end build steps. Loaders can transform files from a different language (like TypeScript) to JavaScript, or inline images as data URLs. Loaders even allow you to do things like `import` CSS files directly from your JavaScript modules!
-->
로더는 모듈의 소스코드에 적용 가능한 변경사항들입니다. 파일들을 `import`하거나 로드할 때에 선처리 과정을 추가할 수 있게 해 주는 것입니다. 즉, 다른 툴들에서 흔히 볼 수 있는 태스크(task)의 역할을 하며, 프론트엔드 빌드 과정을 제어할 수 있는 강력한 도구입니다. 로더는 다른 언어(타입스크립트 등)로 작성된 파일들을 자바스크립트로 바꾸거나, 인라인 이미지들을 데이터 url 로 바꾸는 것 외에도 CSS 파일을 자바스크립트 모듈에서 직접 `import`하는 등의 기능도 지원합니다.

<!--Example-->
## 예시

<!--For example, you can use loaders to tell webpack to load a CSS file or to convert TypeScript to JavaScript. To do this, you would start by installing the loaders you need:-->
예를 들면, 로더를 이용해서 웹팩에게 CSS 파일을 불러오거나 타입스크립트를 자바스크립트로 변환하도록 명령할 수 있습니다. 이를 위해 필요한 로더를 설치하는 것으로 시작해 봅시다.

``` bash
npm install --save-dev css-loader
npm install --save-dev ts-loader
```

<!--And then instruct webpack to use the [`css-loader`](/loaders/css-loader) for every `.css` file and the [`ts-loader`](https://github.com/TypeStrong/ts-loader) for all `.ts` files:-->
그 후 웹팩에게 모든 `.css` 파일에 대하여 [`css-loader`](/loaders/css-loader)를 사용하게 하고, 마찬가지로 모든 `.ts`파일에 대해서 [`ts-loader`](https://github.com/TypeStrong/ts-loader)를 사용하도록 지시합니다:

**webpack.config.js**

``` js
module.exports = {
  module: {
    rules: [
      { test: /\.css$/, use: 'css-loader' },
      { test: /\.ts$/, use: 'ts-loader' }
    ]
  }
};
```

<!--Using Loaders-->
## 로더 사용하기

<!--There are three ways to use loaders in your application:-->
로더를 애플리케이션에서 사용하는 방법에는 세가지가 있습니다:

<!--
* Configuration (recommended): Specify them in your __webpack.config.js__ file.
* Inline: Specify them explicitly in each `import` statement.
* CLI: Specify them within a shell command.
-->
* 설정(추천): __webpack.config.js__ 파일에 지정하기.
* 인라인: 각 `import` 선언 안에 로더들을 지정하기.
* CLI: 셸 명령어를 이용해서 지정하기.


<!--Configuration-->
### 설정

<!--[`module.rules`](/configuration/module/#module-rules) allows you to specify several loaders within your webpack configuration.
This is a concise way to display loaders, and helps to maintain clean code. It also offers you a full overview of each respective loader:-->
[`module.rules`](/configuration/module/#module-rules) 를 이용하면 여러개의 로더를 웹팩 설정에 지정할 수 있습니다.
이렇게 하면 간단하게 로더를 표시하고, 코드를 깔끔하게 유지할 수 있습니다. 더불어 순서대로 전체 항목들을 리뷰할 수 있습니다:

```js-with-links-with-details
  module: {
    rules: [
      {
        test: /\.css$/,
        use: [
          { loader: ['style-loader'](/loaders/style-loader) },
          {
            loader: ['css-loader'](/loaders/css-loader),
            options: {
              modules: true
            }
          }
        ]
      }
    ]
  }
```

<!--Inline-->
### 인라인

<!--It's possible to specify loaders in an `import` statement, or any [equivalent "importing" method](/api/module-methods). Separate loaders from the resource with `!`. Each part is resolved relative to the current directory.-->
`import` 키워드 선언, 혹은 [equivalent "importing" method](/api/module-methods)를 통해서 로더를 지정할 수 있습니다. 로더와 리소스의 구분은 `!`를 이용해서 지정합니다. 지정되는 각 항목은 현재 경로를 기준으로 파악됩니다.

```js
import Styles from 'style-loader!css-loader?modules!./styles.css';
```

<!--
It's possible to overwrite any loaders in the configuration by prefixing the entire rule with `!`.

Options can be passed with a query parameter, e.g. `?key=value&foo=bar`, or a JSON object, e.g. `?{"key":"value","foo":"bar"}`.

T> Use `module.rules` whenever possible, as this will reduce boilerplate in your source code and allow you to debug or locate a loader faster if something goes south.
-->
전체 항목 앞에 `!`를 붙이면 설정 파일에서 지정한 어떤 로더라도 덮어쓰는 것이 가능합니다.

옵션을 추가하고 싶다면 쿼리 파라미터를 이용하여 추가할 수 있습니다. 예)`?key=value&foo=bar` / JSON 개체의 예)  `?{"key":"value","foo":"bar"}`.

T> `module.rules`가 사용 가능한 곳이라면 사용하는 것을 추천합니다. 이렇게 하면 기존 소스 코드상의 보일러플레이트를 줄일 수 있고, 무언가가 잘못되었을 때 디버깅이나 문제가 발생한 로더를 신속하게 찾을 수 있게 해 줍니다.


### CLI

<!--You can also use loaders through the CLI:-->
로더는 CLI를 통해서도 사용 가능합니다:

```sh
webpack --module-bind jade-loader --module-bind 'css=style-loader!css-loader'
```

<!--This uses the `jade-loader` for `.jade` files, and the [`style-loader`](/loaders/style-loader) and [`css-loader`](/loaders/css-loader) for `.css` files.-->
이 예시에서는 `.jade` 파일들을 위해 `jade-loader`를, `.css`파일들을 위해 [`style-loader`](/loaders/style-loader)와 [`css-loader`](/loaders/css-loader)를 이용합니다.


<!--Loader Features-->
## 로더의 기능

<!--
* Loaders can be chained. They are applied in a pipeline to the resource. A chain of loaders are compiled chronologically. The first loader in a chain of loaders returns a value to the next. At the end loader, webpack expects JavaScript to be returned.
* Loaders can be synchronous or asynchronous.
* Loaders run in Node.js and can do everything that’s possible there.
* Loaders accept query parameters. This can be used to pass configuration to the loader.
* Loaders can also be configured with an `options` object.
* Normal modules can export a loader in addition to the normal `main` via `package.json` with the `loader` field.
* Plugins can give loaders more features.
* Loaders can emit additional arbitrary files.
-->
* 로더는 연계(chain)해서 사용할 수 있습니다. 이는 리소스에 파이프라인으로서 적용되며, 연계된 로더들은 순서대로 컴파일됩니다. 연계된 로더들 중 첫번째 로더는 반환값을 그 다음 로더에게 넘겨줍니다. 웹팩은 마지막 로더에서는 자바스크립트가 반환되는 것을 대기합니다.
* 로더는 동기식 / 비동기식 모두 지원합니다.
* 로더는 Node.js 상에서 실행되므로, 그 안에서 가능한 모든 것들을 할 수 있습니다.
* 로더는 쿼리 파라미터를 수용합니다. 이를 통해 설정을 로더에게 넘겨줄 수 있습니다.
* 로더는 `options` 객체를 통해 세부 설정을 지정할 수 있습니다.
* 일반 모듈들은 보통의 `main` 로더 이외에도 `package.json` 의 `loader` 필드를 통해 추가 로더들을 불러올(export) 수 있습니다.
* 플러그인은 로더에 더 많은 기능을 추가할 수 있습니다.
* 로더는 부가적인 임의의(arbitrary) 파일들을 생성할 수 있습니다.

<!--Loaders allow more power in the JavaScript ecosystem through preprocessing
functions (loaders). Users now have more flexibility to include fine-grained logic such as compression, packaging, language translations and [more](/loaders).
-->
로더들은 함수들(loaders)을 선처리하므로써 자바스크립트 생태계에 더 많은 가능성을 제공합니다. 유저들은 이를 통해 압축, 패키징, 언어 번역 외에도 [다양한](/loaders) 전문적 기능들을 추가할 수 있게 됩니다.


<!--Resolving Loaders-->
## 로더의 위치 지정(Resolving)

<!--Loaders follow the standard [module resolution](/concepts/module-resolution/). In most cases it will be loaders from the [module path](/concepts/module-resolution/#module-paths) (think `npm install`, `node_modules`).

A loader module is expected to export a function and be written in Node.js compatible JavaScript. They are most commonly managed with npm, but you can also have custom loaders as files within your application. By convention, loaders are usually named `xxx-loader` (e.g. `json-loader`). See ["How to Write a Loader?"](/development/how-to-write-a-loader) for more information.
-->
로더는 일반적인 [모듈 리졸빙](/concepts/module-resolution/) 법칙을 따릅니다. 대부분의 경우 [module path](/concepts/module-resolution/#module-paths)에서 로더를 불러오게 될 것입니다. (`npm install`, `node_modules` 등의 경우를 떠올리시면 됩니다).

로더 모듈은 Node.js 기반의 자바스크립트에서 함수를 불러오도록(export) 되어있습니다. 보통 npm을 통해서 관리하지만, 커스텀 로더도 추가할 수 있습니다. 일반적으로 로더들은 `xxx-loader` (e.g. `json-loader`)와 같은 형식(convention)으로 네이밍합니다. 더 알고 싶다면 ["로더 작성하기"](/development/how-to-write-a-loader) 항목을 확인하세요.

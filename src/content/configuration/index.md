---
title: 설정
sort: 1
contributors:
  - sokra
  - skipjack
  - grgur
  - bondz
  - sricc
  - terinjokes
  - mattce
  - kbariotis
  - sterlingvix
---

<!--webpack is fed via a configuration object. It is passed in one of two ways depending on how you are using webpack: through the terminal or via Node.js. All the available configuration options are specified below.-->
웹팩은 설정 객체를 기반으로 실행됩니다. 설정 객체는 어떤 식으로 웹팩을 사용하느냐에 따라 두가지 방법: 터미널 혹은 Node.js 중 하나를 택하여 넘길 수 있습니다. 설정 가능한 옵션들은 아래와 같습니다.

<!--New to webpack? Check out our guide to some of webpack's [core concepts](/concepts) to get started!-->
T> 웹팩은 처음이신가요? 웹팩의 [코어 개념](/concepts)에 대한 가이드로 먼저 시작해 보세요!


<!--Notice that throughout the configuration we use Node's built-in [path module](https://nodejs.org/api/path.html) and prefix it with the [__dirname](https://nodejs.org/docs/latest/api/globals.html#globals_dirname) global. This prevents file path issues between operating systems and allows relative paths to work as expected. See [this section](https://nodejs.org/api/path.html#path_windows_vs_posix) for more info on POSIX vs. Windows paths.-->
T> 설정 전반에 Node의 내장 [path 모듈](https://nodejs.org/api/path.html)에 글로벌 prefix [__dirname](https://nodejs.org/docs/latest/api/globals.html#globals_dirname) 을 붙여서 사용하고 있음을 아실 수 있습니다. 이렇게 하여 OS 간에 있을 수 있는 파일 경로 이슈를 방지하고, 상대 경로들이 제대로 작동하도록 하고 있습니다. POSIX와 윈도우즈의 차이에 대해서는 [여기](https://nodejs.org/api/path.html#path_windows_vs_posix)를 참조하세요.


## 옵션

<!--Click on the name of each option in the configuration code below to jump to the detailed documentation. Also note that the items with arrows can be expanded to show more examples and, in some cases, more advanced configuration.-->
각 옵션에 대한 더 자세항 문서를 읽고 싶으시다면 다음 코드에서 각 옵션명을 클릭하세요. 화살표가 있는 항목들은 더 많은 예제를 펼쳐 볼 수 있으며, 몇몇 항목은 더 자세한 설정 항목을 보실 수 있습니다.

``` js-with-links-with-details
const path = require('path');

module.exports = {
  <details><summary>[entry](/configuration/entry-context#entry): "./app/entry", // string | object | array</summary>
  [entry](/configuration/entry-context#entry): ["./app/entry1", "./app/entry2"],
  [entry](/configuration/entry-context#entry): {
    a: "./app/entry-a",
    b: ["./app/entry-b1", "./app/entry-b2"]
  },
  </details>
  // 여기서 애플리케이션이 실행되고
  // 웹팩이 번들링을 시작

  [output](/configuration/output): {
    // 웹팩이 어떻게 결과를 만들어낼 것인지에 대한 옵션들

    [path](/configuration/output#output-path): path.resolve(__dirname, "dist"), // string
    // 모든 아웃풋 파일에 대한 타겟 경로는
    // 절대 경로로 (Node.js의 path 모듈 사용)

    <details><summary>[filename](/configuration/output#output-filename): "bundle.js", // string</summary>
    [filename](/configuration/output#output-filename): "[name].js", // 엔트리 포인트가 여러개인 경우
    [filename](/configuration/output#output-filename): "[chunkhash].js", // [long term caching](/guides/caching) 용
    </details>
    // 초기 청크들의 파일명 형식

    <details><summary>[publicPath](/configuration/output#output-publicpath): "/assets/", // string</summary>
    [publicPath](/configuration/output#output-publicpath): "",
    [publicPath](/configuration/output#output-publicpath): "https://cdn.example.com/",
    </details>
    // HTML페이지를 기준으로 한 아웃풋 디렉토리의 상대 경로

    [library](/configuration/output#output-library): "MyLibrary", // string,
    // export된 라이브러리명

    <details><summary>[libraryTarget](/configuration/output#output-librarytarget): "umd", // universal module definition</summary>
        [libraryTarget](/configuration/output#output-librarytarget): "umd2", // universal module definition
        [libraryTarget](/configuration/output#output-librarytarget): "commonjs2", // exported with module.exports
        [libraryTarget](/configuration/output#output-librarytarget): "commonjs", // exported as properties to exports
        [libraryTarget](/configuration/output#output-librarytarget): "amd", // defined with AMD defined method
        [libraryTarget](/configuration/output#output-librarytarget): "this", // property set on this
        [libraryTarget](/configuration/output#output-librarytarget): "var", // variable defined in root scope
        [libraryTarget](/configuration/output#output-librarytarget): "assign", // blind assignment
        [libraryTarget](/configuration/output#output-librarytarget): "window", // property set to window object
        [libraryTarget](/configuration/output#output-librarytarget): "global", // property set to global object
        [libraryTarget](/configuration/output#output-librarytarget): "jsonp", // jsonp wrapper
    </details>
    // export된 라이브러리들의 종류

    <details><summary>/* 아웃풋 추가 설정 (클릭해서 보기) */</summary>

    [pathinfo](/configuration/output#output-pathinfo): true, // boolean
    // 생성될 코드에 모듈, export, request 등에 관련된 path 정보 포함 여부

    [chunkFilename](/configuration/output#output-chunkfilename): "[id].js",
    [chunkFilename](/configuration/output#output-chunkfilename): "[chunkhash].js", // for [long term caching](/guides/caching)
    // 추가 청크(chunk)들을 위한 파일명 형식

    [jsonpFunction](/configuration/output#output-jsonpfunction): "myWebpackJsonp", // string
    // 청크들을 불러올 때 사용할 JSONP 함수명

    [sourceMapFilename](/configuration/output#output-sourcemapfilename): "[file].map", // string
    [sourceMapFilename](/configuration/output#output-sourcemapfilename): "sourcemaps/[file].map", // string
    // 소스 맵 위치에 대한 파일명 형식

    [devtoolModuleFilenameTemplate](/configuration/output#output-devtoolmodulefilenametemplate): "webpack:///[resource-path]", // string
    // 개발툴 모듈들에 대한 형식

    [devtoolFallbackModuleFilenameTemplate](/configuration/output#output-devtoolfallbackmodulefilenametemplate): "webpack:///[resource-path]?[hash]", // string
    // 개발툴 모듈들에 대한 형식l (충돌시 사용)

    [umdNamedDefine](/configuration/output#output-umdnameddefine): true, // boolean
    // 지정된 AMD 모듈을 UMD 라이브러리 내에서 사용

    [crossOriginLoading](/configuration/output#output-crossoriginloading): "use-credentials", // enum
    [crossOriginLoading](/configuration/output#output-crossoriginloading): "anonymous",
    [crossOriginLoading](/configuration/output#output-crossoriginloading): false,
    // 런타임중 cross origin 요청을 어떻게 할 것인가를 지정

    <details><summary>/* 전문가용 아웃풋 설정 (위험 본인 부담) */</summary>

    [devtoolLineToLine](/configuration/output#output-devtoollinetoline): {
      test: /\.jsx$/
    },
    // 이 모듈들에 대해서는 간단한 1:1 맵핑의 소스맵을 이용 (더 빠름)

    [hotUpdateMainFilename](/configuration/output#output-hotupdatemainfilename): "[hash].hot-update.json", // string
    // HMR manifest 의 파일명 형식

    [hotUpdateChunkFilename](/configuration/output#output-hotupdatechunkfilename): "[id].[hash].hot-update.js", // string
    // HMR 청크들의 파일명 형식

    [sourcePrefix](/configuration/output#output-sourceprefix): "\t", // string
    // 더 나은 가독성을 위해 번들 내 모듈 소스에 추가하는 prefix
    </details>
    </details>
  },

  [module](/configuration/module): {
    // 모듈 관련 설정

    [rules](/configuration/module#module-rules): [
      // 모듈들에 대한 규칙 (로더 설정, 파저 옵션, 등등.)

      {
        [test](/configuration/module#rule-test): /\.jsx?$/,
        [include](/configuration/module#rule-include): [
          path.resolve(__dirname, "app")
        ],
        [exclude](/configuration/module#rule-exclude): [
          path.resolve(__dirname, "app/demo-files")
        ],
        // matching condition - 정규표현식 혹은 string test로 설정 가능
        // include: 위와 같으나, 두 인자가 모두 만족될 떄 포함
        // exclude: test와 include 보다 더 우선순위로, 제외할 항목
        // 베스트 프랙티스:
        // - test와 filename에 대해서는 정규표현식만 사용
        // - include와 exclude에 대해서는 절대경로의 배열들만 사용
        // - exclude 보다는 include를 사용하도록 함

        [issuer](/configuration/module#rule-issuer): { test, include, exclude },
        // issuer에 대한 조건 (import의 원 소스)

        [enforce](/configuration/module#rule-enforce): "pre",
        [enforce](/configuration/module#rule-enforce): "post",
        // 오버라이딩 됬다 하더라도 위의 규칙들을 적요할지 여부 (고급 옵션)

        [loader](/configuration/module#rule-loader): "babel-loader",
        // 어느 로더를 사용할지 지정. context에 따라 경로 선언.
        // -loader suffix는 웹팩2에서는 명확성을 위해 필수 조건임.
        // [웹팩 1 업그레이드 가이드](/guides/migrating) 참조

        [options](/configuration/module#rule-options-rule-query): {
          presets: ["es2015"]
        },
        // 로더의 옵션들
      },

      {
        [test](/configuration/module#rule-test): /\.html$/,

        [use](/configuration/module#rule-use): [
          // 다수 로더 및 옵션 적용
          "htmllint-loader",
          {
            loader: "html-loader",
            options: {
              /* ... */
            }
          }
        ]
      },

      { [oneOf](/configuration/module#rule-oneof): [ /* rules */ ] },
      // 다중 규칙중 하나만 이용하도록 설정

      { [rules](/configuration/module#rule-rules): [ /* rules */ ] },
      // 다중 규칙 모두 이용 (조건들과 조합하여 사용하면 유용)

      { [resource](/configuration/module#rule-resource): { [and](/configuration/module#condition): [ /* conditions */ ] } },
      // 모든 조건이 만족될 때에 한해 매치됨

      { [resource](/configuration/module#rule-resource): { [or](/configuration/module#condition): [ /* conditions */ ] } },
      { [resource](/configuration/module#rule-resource): [ /* conditions */ ] },
      // 조건 중 하나만 만족해도 매치됨 (배열에 대해서 기본 설정)

      { [resource](/configuration/module#rule-resource): { [not](/configuration/module#condition): /* condition */ } }
      // 조건이 만족되지 않았을 떄 매치됨
    ],

    <details><summary>/* 고급 모듈 설정 (클릭해서 보기) */</summary>

    [noParse](/configuration/module#module-noparse): [
      /special-library\.js$/
    ],
    // 이 모듈은 파싱 금지

    unknownContextRequest: ".",
    unknownContextRecursive: true,
    unknownContextRegExp: /^\.\/.*$/,
    unknownContextCritical: true,
    exprContextRequest: ".",
    exprContextRegExp: /^\.\/.*$/,
    exprContextRecursive: true,
    exprContextCritical: true,
    wrappedContextRegExp: /.*/,
    wrappedContextRecursive: true,
    wrappedContextCritical: false,
    // 동적 요청(request)에 대한 기본 행동 설정
    </details>
  },

  [resolve](/configuration/resolve): {
    // 모듈 요청의 resolve(경로 처리)에 대한 옵션
    // (로더 resolve에 대해서는 적용되지 않음)

    [modules](/configuration/resolve#resolve-modules): [
      "node_modules",
      path.resolve(__dirname, "app")
    ],
    // 모듈을 검색할 디렉토리들

    [extensions](/configuration/resolve#resolve-extensions): [".js", ".json", ".jsx", ".css"],
    // 사용될 extention

    [alias](/configuration/resolve#resolve-alias): {
      // 모듈명 별명(aliases)들에 대한 설정

      "module": "new-module",
      // "module" -> "new-module" 그리고 "module/path/file" -> "new-module/path/file"로 alias 설정

      "only-module$": "new-module",
      // "only-module" -> "new-module"로 alias 설정. 하지만 "module/path/file" -> "new-module/path/file"으로는 적용되지 않음

      "module": path.resolve(__dirname, "app/third/module.js"),
      // "module" -> "./app/third/module.js" 와 "module/file" 의 alias 설정시 에러 발생
      // 현재 위치에 따라 모듈 alias가 import 됨
    },
    <details><summary>/* 대체 alias 문법 (클릭해서 보기) */</summary>
    [alias](/configuration/resolve#resolve-alias): [
      {
        name: "module",
        // 예전 요청

        alias: "new-module",
        // 새로운 요청

        onlyModule: true
        // true일 경우 "module" 만 alias화 됨
        // false일 경우 "module/inner/path" 도 alias화 됨
      }
    ],
    </details>

    <details><summary>/* 고급 resolve 설정 (클릭해서 보기) */</summary>

    [symlinks](/configuration/resolve#resolve-symlinks): true,
    // symlinks를 새로운 경로로 따라가기

    [descriptionFiles](/configuration/resolve#resolve-descriptionfiles): ["package.json"],
    // 패키지 설명이 기록되는 파일

    [mainFields](/configuration/resolve#resolve-mainfields): ["main"],
    // 폴더가 요청되었을 때 설명 파일을 통해 인식된 속성들

    [aliasFields](/configuration/resolve#resolve-aliasfields): ["browser"],
    // 패키지에 대한 
    // alias 요청으로 description 파일에서 인식된 속성들

    [enforceExtension](/configuration/resolve#resolve-enforceextension): false,
    // true일 경우 요청이 extentions를 포함하지 않아야함
    // false일 경우 요청이 이미 extension을 포함하고 있음

    [moduleExtensions](/configuration/resolve#resolveloader-moduleextensions): ["-module"],
    [enforceModuleExtension](/configuration/resolve#resolve-enforcemoduleextension): false,
    // extensions/enforceExtension과 흡사하나 파일명이 아닌 모듈명에 대한 항목

    [unsafeCache](/configuration/resolve#resolve-unsafecache): true,
    [unsafeCache](/configuration/resolve#resolve-unsafecache): {},
    // resolved 요청에 대해 캐싱 사용
    // 폴더 형태를 바꿀 수 있으므로 안전하지 않음
    // 대신, 퍼포먼스를 크게 높힐 수 있음

    [cachePredicate](/configuration/resolve#resolve-cachepredicate): (path, request) => true,
    // 캐싱 요청을 선택할 근거 함수

    [plugins](/configuration/resolve#resolve-plugins): [
      // ...
    ]
    // resolver에 대해 적용된 추가 플러그인들
    </details>
  },

  [performance](/configuration/performance): {
    <details><summary>[hints](/configuration/performance#performance-hints): "warning", // enum </summary>
    [hints](/configuration/performance#performance-hints): "error", // emit errors for perf hints
    [hints](/configuration/performance#performance-hints): false, // turn off perf hints
    </details>
    [maxAssetSize](/configuration/performance#performance-maxassetsize): 200000, // int (in bytes),
    [maxEntrypointSize](/configuration/performance#performance-maxentrypointsize): 400000, // int (in bytes)
    [assetFilter](/configuration/performance#performance-assetfilter): function(assetFilename) {
      // 파일명들을 제공하는 함수 predicate
      return assetFilename.endsWith('.css') || assetFilename.endsWith('.js');
    }
  },

  <details><summary>[devtool](/configuration/devtool): "source-map", // enum </summary>
  [devtool](/configuration/devtool): "inline-source-map", // 원본 파일에 SourceMap을 inline함
  [devtool](/configuration/devtool): "eval-source-map", // 각 모듈에 SourceMap을 inline함
  [devtool](/configuration/devtool): "hidden-source-map", // 원본 파일에 대한 리퍼런스 없이 SourceMap
  [devtool](/configuration/devtool): "cheap-source-map", // 모듈 맵핑이 없는 SourceMap의 저비용 버전
  [devtool](/configuration/devtool): "cheap-module-source-map", // 모듈 맵핑이 있는 SourceMap의 저비용 버전
  [devtool](/configuration/devtool): "eval", // SourceMap 대신 이름을 붙인 모듈 사용. 디테일을 생략한 대신 속도가 빠름.
  </details>
  // 브라우저 개발자도구를 위해 메타 정보를 추가하여 더 강력한 디버깅 기능 추가
  // 빌드 스피드를 낮추는 대신 가장 디테일한 source-map 설정

  [context](/configuration/entry-context#context): __dirname, // string (absolute path!)
  // 웹팩의 홈 디렉토리
  // [entry](/configuration/entry-context) and [module.rules.loader](/configuration/module#rule-loader) 옵션은
  // 이 경로를 기준으로 결정(reolved)됨

  <details><summary>[target](/configuration/target): "web", // enum</summary>
  [target](/configuration/target): "webworker", // WebWorker
  [target](/configuration/target): "node", // Node.js via require
  [target](/configuration/target): "async-node", // Node.js via fs and vm
  [target](/configuration/target): "node-webkit", // nw.js
  [target](/configuration/target): "electron-main", // electron, main process
  [target](/configuration/target): "electron-renderer", // electron, renderer process
  [target](/configuration/target): (compiler) => { /* ... */ }, // custom
  </details>
  // 번들이 실행될 환경
  // 청크 로딩 방법(behavior)와 가능한 모듈들을 변경함

  <details><summary>[externals](/configuration/externals): ["react", /^@angular\//],</summary>
  [externals](/configuration/externals): "react", // string (exact match)
  [externals](/configuration/externals): /^[a-z\-]+($|\/)/, // Regex
  [externals](/configuration/externals): { // object
    angular: "this angular", // this["angular"]
    react: { // UMD
      commonjs: "react",
      commonjs2: "react",
      amd: "react",
      root: "React"
    }
  },
  [externals](/configuration/externals): (request) => { /* ... */ return "commonjs " + request }
  </details>
  // 이 모듈들을 follow하거나 묶지(bundle) 말고, 런타임 도중에 호출

  <details><summary>[stats](/configuration/stats): "errors-only",</summary>
  [stats](/configuration/stats): { //object
    assets: true,
    colors: true,
    errors: true,
    errorDetails: true,
    hash: true,
    // ...
  },
  </details>
  // 보여주는 번들 정보를 제어 가능

  [devServer](/configuration/dev-server): {
    proxy: { // proxy URLs to backend development server
      '/api': 'http://localhost:3000'
    },
    contentBase: path.join(__dirname, 'public'), // boolean | string | array, static file location
    compress: true, // enable gzip compression
    historyApiFallback: true, // 404시에 index.html에 대해 실행, 다수 경로에 대한 오브젝트
    hot: true, // hot 모듈 교체. HotModuleReplacementPlugin에 따라 결정
    https: false, // self-signed 와 cert authority 객체 생성을 위해서는 true로 설정
    noInfo: true, // hot reload의 경우 에러와 경고만 표시
    // ...
  },

  [plugins](plugins): [
    // ...
  ],
  // 추가 플러그인 리스트


  <details><summary>/* 고급 설정 (클릭해서 보기) */</summary>

  [resolveLoader](/configuration/resolve#resolveloader): { /* same as resolve */ }
  // 로더에 대한 resolve 옵션 분리
  
  [parallelism](other-options#parallelism): 1, // number
  // 병렬 프로세스 모듈의 숫자 제한

  [profile](other-options#profile): true, // boolean
  // 시간 정보 수집

  [bail](other-options#bail): true, //boolean
  // 첫번째 에러에서 용인 없이 fail 하도록 유도

  [cache](other-options#cache): false, // boolean
  // 캐싱 사용/비사용

  [watch](watch#watch): true, // boolean
  // watching 사용

  [watchOptions](watch#watchoptions): {
    [aggregateTimeout](watch#watchoptions-aggregatetimeout): 1000, // in ms
    // 한번 재빌드 할 떄마다 다중 변경 사항을 aggregate

    [poll](watch#watchoptions-poll): true,
    [poll](watch#watchoptions-poll): 500, // intervall in ms
    // watch에 대해 polling 모드 자용
    // 변경이 일어나도 알림이 없는 파일 시스템에 사용할것
    // 예) nfs shares
  },

  [node](node): {
    // Node.js 실행을 위한 임시 설정 /폴리필
    // 비Node 환경에 대한 환경 코드.
    
    [console](node#node-console): false, // boolean | "mock"
    [global](node#node-global): true, // boolean | "mock"
    [process](node#node-process): true, // boolean
    [__filename](node#node-__filename): "mock", // boolean | "mock"
    [__dirname](node#node-__dirname): "mock", // boolean | "mock"
    [Buffer](node#node-buffer): true, // boolean | "mock"
    [setImmediate](node#node-setimmediate): true // boolean | "mock" | "empty"
  },

  [recordsPath](other-options#recordspath): path.resolve(__dirname, "build/records.json"),
  [recordsInputPath](other-options#recordsinputpath): path.resolve(__dirname, "build/records.json"),
  [recordsOutputPath](other-options#recordsoutputpath): path.resolve(__dirname, "build/records.json"),
  // TODO

  </details>
}
```

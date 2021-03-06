[![Build Status](https://api.travis-ci.org/brunoosilva/webpack-import-glob.svg)](https://travis-ci.org/brunoosilva/webpack-import-glob)
[![npm version](https://badge.fury.io/js/webpack-import-glob.svg)](https://badge.fury.io/js/webpack-import-glob)
# webpack-import-glob
ES6 import with glob patterns (preloader for Webpack)

Expands globbing patterns for ES6 `import` statements.

// Forked of https://github.com/terpiljenya/import-glob

---
```js
import modules from "./foo/**/*.js";
```
Expands into
```js
import * as module0 from "./foo/1.js";
import * as module1 from "./foo/bar/2.js";
import * as module2 from "./foo/bar/3.js";

modules = [module0, module1, module2]
```
---
__For side effects:__

```js
import "./foo/**/*.scss";
```
Expands into
```js
import "./foo/1.scss";
import "./foo/bar/2.scss";
```
---
__For sass:__

```scss
@import "./foo/**/*.scss";
```
Expands into
```scss
@import "./foo/1.scss";
@import "./foo/bar/2.scss";
```

---

## Install
```sh
yarn add webpack-import-glob -D
```

## Usage
You can use it one of two ways, the recommended way is to use it as a preloader

```js
{
  module: {
    preloaders: [{
      test: /\.js/,
      loader: 'webpack-import-glob'
    },
    {
      test: /\.scss/,
      loader: 'webpack-import-glob'
    }
    ]
  }
}

// or

{
  test: /\.js$/,
  enforce: 'pre',
  loader: 'webpack-import-glob',
}
```

Alternatively you can use it as a chained loader
```js
require('!webpack-import-glob!foo/bar.js')
```

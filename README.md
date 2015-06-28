# is-kindof [![npmjs.com][npmjs-img]][npmjs-url] [![The MIT License][license-img]][license-url] 

> Check type of given javascript value. Support promises, generators, streams, and native types. Thin wrapper around `kind-of` module.

[![code climate][codeclimate-img]][codeclimate-url] [![standard code style][standard-img]][standard-url] [![travis build status][travis-img]][travis-url] [![coverage status][coveralls-img]][coveralls-url] [![dependency status][david-img]][david-url]


## Install
```
npm i is-kindof --save
npm test
```


## Features
- multiple check types - e.g. check value is `string` or `number`
- multiple APIs - `is(val, type)`, `is(val).type()`, `is.type(val)` or `is().type(val)`
- have support for es6 features like WeakMap, Symbol, Promises, Generators and etc
- all methods also exists prefixed with `is` like `isNumber`, `isRegexp`
- performance, because is on top of `kind-of` which is the fastest
- [see below supported methods](https://github.com/tunnckoCore/is-kindof#supported-methods-and-types) and types that you can use to check values


## Usage
> For more use-cases see the [tests](./test.js)

```js
var kindof = require('is-kindof')

kindof(123456789, 'number')   //=> true
kindof([1, 2, 3], 'array')    //=> true 
kindof(/^[a-f]$/, 'regexp')   //=> true 
kindof({a: 'bc'}, 'object')   //=> true 
kindof('foo bar', 'array')    //=> false 
kindof('foo bar', 'string')   //=> true

kindof(123, ['number', 'string'])   //=> true
kindof('foo', ['number', 'array'])  //=> false
```

**Example for numbers**
> Here below we use all available APIs to check that given `value` is number.

```js
var is = require('is-kindof')

is.number()         //=> false
is.isNumber()       //=> false
is.number(123)      //=> true
is.isNumber(123)    //=> true
is().number()       //=> false
is().isNumber()     //=> false
is().number(123)    //=> true
is().isNumber(123)  //=> true
is(123).number()    //=> true
is(123).isNumber()  //=> true
is(123, 'number')   //=> true
```

> **Note:** We also have support for promises, hybrids, generators, streams and other es6  
features like Set, WeakMap, Symbol and etc.

**Generators**
> We have [few aliases](./index.js#L123-L133) for the `generator function` type

- generatorFunction
- generator function
- generatorFn
- generator Fn
- generator fn
- gen fn
- genfn

> All of them you can use in `is(val, type)` way.  
Otherwise only `generatorFn` and `generatorFunction` are exposed as methods.

**Example**

```js
var gen = (function * () {yield 42})()
var genfn = function * () {yield 42}

is.generator(gen) //=> true
is().generator(gen) //=> true
is(gen).generator() //=> true

is.generatorFunction(genfn) //=> true
is().generatorFunction(genfn) //=> true
is(genfn).generatorFunction() //=> true

is.generatorFn(genfn) //=> true
is().generatorFn(genfn) //=> true
is(genfn).generatorFn() //=> true

is(gen, 'generatorFunction') //=> false
is(gen, 'generator function') //=> false
is(gen, 'generator Fn') //=> false
is(gen, 'generatorFn') //=> false

is(genfn, 'generatorFunction') //=> true
is(genfn, 'generator function') //=> true
is(genfn, 'generator Fn') //=> true
is(genfn, 'generatorFn') //=> true

is(genfn, ['generator', 'string']) //=> false
is(gen, ['generator', 'string']) //=> true
```


## Supported methods and types
> All of them also exist prefixed with `is`, like `isNumber`, `isFunction` and etc.

- `null`
- `set`
- `map`
- `date`
- `array`
- `string`
- `object`
- `number`
- `regexp`
- `boolean`
- `function`
- `undefined`
- `generator`
- `generatorFunction`
- `weakmap`
- `weakset`
- `symbol`
- `promise`
- `hybrid`
- `stream`
- `error`


## Checking for errors
> You may think it is interesting case, yea. We just cast given value to string and then  
check that this string have `Error` in it. It is the easiest and guaranteed way to do that,
because error extending and inheriting is little bit tricky in Javascript world.

**Example**

```js
var is = require('is-kindof')
var PluginErr = require('plugin-error')

is.error(new Error('foo bar baz!')) //=> true
is.error(new TypeError('type err')) //=> true

is.error(new PluginErr('foo', 'msg'))
//=> true, because it's internal name is `Error`

is.error(new PluginErr('foo', 'msg', {name: 'MyErr'}))
//=> false, because we change it's name to `MyErr`
```


## Contributing

Pull requests and stars are always welcome. For bugs and feature requests, [please create an issue](https://github.com/tunnckoCore/is-kindof/issues/new).  
But before doing anything, please read the [CONTRIBUTING.md](./CONTRIBUTING.md) guidelines.


## [Charlike Make Reagent](http://j.mp/1stW47C) [![new message to charlike][new-message-img]][new-message-url] [![freenode #charlike][freenode-img]][freenode-url]

[![tunnckocore.tk][author-www-img]][author-www-url] [![keybase tunnckocore][keybase-img]][keybase-url] [![tunnckoCore npm][author-npm-img]][author-npm-url] [![tunnckoCore twitter][author-twitter-img]][author-twitter-url] [![tunnckoCore github][author-github-img]][author-github-url]


[npmjs-url]: https://www.npmjs.com/package/is-kindof
[npmjs-img]: https://img.shields.io/npm/v/is-kindof.svg?label=is-kindof

[license-url]: https://github.com/tunnckoCore/is-kindof/blob/master/LICENSE.md
[license-img]: https://img.shields.io/badge/license-MIT-blue.svg


[codeclimate-url]: https://codeclimate.com/github/tunnckoCore/is-kindof
[codeclimate-img]: https://img.shields.io/codeclimate/github/tunnckoCore/is-kindof.svg

[travis-url]: https://travis-ci.org/tunnckoCore/is-kindof
[travis-img]: https://img.shields.io/travis/tunnckoCore/is-kindof.svg

[coveralls-url]: https://coveralls.io/r/tunnckoCore/is-kindof
[coveralls-img]: https://img.shields.io/coveralls/tunnckoCore/is-kindof.svg

[david-url]: https://david-dm.org/tunnckoCore/is-kindof
[david-img]: https://img.shields.io/david/tunnckoCore/is-kindof.svg

[standard-url]: https://github.com/feross/standard
[standard-img]: https://img.shields.io/badge/code%20style-standard-brightgreen.svg


[author-www-url]: http://www.tunnckocore.tk
[author-www-img]: https://img.shields.io/badge/www-tunnckocore.tk-fe7d37.svg

[keybase-url]: https://keybase.io/tunnckocore
[keybase-img]: https://img.shields.io/badge/keybase-tunnckocore-8a7967.svg

[author-npm-url]: https://www.npmjs.com/~tunnckocore
[author-npm-img]: https://img.shields.io/badge/npm-~tunnckocore-cb3837.svg

[author-twitter-url]: https://twitter.com/tunnckoCore
[author-twitter-img]: https://img.shields.io/badge/twitter-@tunnckoCore-55acee.svg

[author-github-url]: https://github.com/tunnckoCore
[author-github-img]: https://img.shields.io/badge/github-@tunnckoCore-4183c4.svg

[freenode-url]: http://webchat.freenode.net/?channels=charlike
[freenode-img]: https://img.shields.io/badge/freenode-%23charlike-5654a4.svg

[new-message-url]: https://github.com/tunnckoCore/messages
[new-message-img]: https://img.shields.io/badge/send%20me-message-green.svg

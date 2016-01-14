# http-node
This module is a standalone package of http from Node.js v5.4.0. Unlike
[http-browserify](https://www.npmjs.com/package/http-browserify), this is not
a shim but the original code of Node, so it requires the `net` module. This is
useful for having the Node core APIs on JS platforms other than Node, where
TCP socket APIs are available (which can be wrapped in a `net` module),
such as [Chrome Apps](https://developer.chrome.com/apps/sockets_tcp).

## install / usage with browserify

```bash
npm install http-node
```

To use it with browserify, you have to use the js API of browserify;
the command line API does not support changing builtins.

Example:

```js
const browserify = require('browserify');

const builtins = require('browserify/lib/builtins.js');
var customBuiltins = Object.assign({}, builtins);
customBuiltins.http = require.resolve('http-node');

var b = browserify({builtins: customBuiltins});

b.add(...
```

## differences to original Node.js code

- `require` calls of `_http_*` modules prefixed with `./`
- `require('internal/util').deprecate` replaced by `require('util').deprecate`
- uses [http-parser-js](https://github.com/creationix/http-parser-js)
- commented out calls to `DTRACE_HTTP_*`, `LTTNG_HTTP_*` and `COUNTER_HTTP_*`
- does not presume that sockets have a `_handle`

## credit

The code is taken from the [Node.js](http://nodejs.org) project:
Copyright Node.js contributors. All rights reserved.

## license

MIT

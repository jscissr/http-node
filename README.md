# http-node
This module is a standalone package of Nodes http, Node.js v0.12.0. Unlike
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
var browserify = require('browserify');

var builtins = require('browserify/lib/builtins.js');
builtins.http = require.resolve('http-node');

var b = browserify();

b.add(...
```

The above example will use http-node for all browserify builds.
If you only want it for a specific build of a larger build script:

```js
var browserify = require('browserify');

var builtins = require('browserify/lib/builtins.js');
var myBuiltins = {};
Object.keys(builtins).forEach(function(key) {
  myBuiltins[key] = builtins[key];
});

myBuiltins.http = require.resolve('http-node')

var b = browserify({builtins: myBuiltins});

b.add(...
```

## differences to original Node.js code

- `require` calls of `_http_*` modules prefixed with `./`
- uses [http-parser-js](https://www.npmjs.com/package/http-parser-js)
- commented out calls to `DTRACE_HTTP_*` and `COUNTER_HTTP_*`
- in older versions of stream module, `cork` was not available, fix for that in
  `_http_outgoing.js`

## credit

The code is taken from the [Node.js](http://nodejs.org) project:
Copyright Joyent, Inc. and other Node contributors.

Node.js is a registered trademark of Joyent, Inc. in the United states and other countries. This
package is not formally related to or endorsed by the official Joyent Node.js project.

## license

MIT

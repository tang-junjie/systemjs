SystemJS
========

[![Build Status][travis-image]][travis-url]
[![Gitter](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/systemjs/systemjs?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)
[![Support](https://supporterhq.com/api/b/33df4abbec4d39260f49015d2457eafe/SystemJS)](https://supporterhq.com/support/33df4abbec4d39260f49015d2457eafe/SystemJS)

_SystemJS 0.20.0-alpha.1 is now available with performance improvements and Web Assembly support. [Try it out here](https://github.com/systemjs/systemjs/releases/tag/0.20.0-alpha.1)._

Universal dynamic module loader - loads ES6 modules, AMD, CommonJS and global scripts in the browser and NodeJS.

* [Loads any module format](docs/module-formats.md) with [exact circular reference and binding support](https://github.com/ModuleLoader/es6-module-loader/blob/v0.17.0/docs/circular-references-bindings.md).
* Loads [ES6 modules compiled into the `System.register` bundle format for production](docs/production-workflows.md), maintaining circular references support.
* Supports RequireJS-style [map](docs/overview.md#map-config), [paths](https://github.com/ModuleLoader/es6-module-loader/blob/master/docs/loader-config.md#paths-implementation), [bundles](docs/production-workflows.md#bundle-extension) and [global shims](docs/module-formats.md#shim-dependencies).
* [Loader plugins](docs/overview.md#plugin-loaders) allow production resource loading and custom transpilation dev workflows.

Built with the [ES Module Loader project](https://github.com/ModuleLoader/es-module-loader), based on principles and APIs from the WhatWG Loader
specification, modules in HTML and NodeJS.

~14KB minified and gzipped, runs in IE9+ and NodeJS.

For discussion, join the [Gitter Room](https://gitter.im/systemjs/systemjs).

Documentation
---

* [ES6 Modules Overview](docs/es6-modules-overview.md)
* [SystemJS Overview](docs/overview.md)
* [Config API](docs/config-api.md)
* [Module Formats](docs/module-formats.md)
* [Production Workflows](docs/production-workflows.md)
* [System API](docs/system-api.md)
* [Creating Plugins](docs/creating-plugins.md)

Basic Use
---

### Browser

```html
<script src="system.js"></script>
<script>
  SystemJS.import('/js/main.js');
</script>
```

The above will support loading all module formats, including ES Modules transpiled into the System.register format.

**To load ES6 code with in-browser transpilation, ne of the following transpiler plugins must be configured**:

* [Babel](https://github.com/systemjs/plugin-babel)
* [TypeScript](https://github.com/frankwallis/plugin-typescript)
* [Traceur](http://github.com/systemjs/plugin-traceur)

### NodeJS

To load modules in NodeJS, install SystemJS with:

```
  npm install systemjs
```

If transpiling ES6, also install the transpiler plugin, following the instructions from the transpiler project page.

We can then load modules equivalently in NodeJS as we do in the browser:

```javascript
var SystemJS = require('systemjs');

// loads './app.js' from the current directory
SystemJS.import('./app.js').then(function(m) {
  console.log(m);
});
```

If you are using jspm as a package manager you will also need to load the generated configuration.
The best way to do this in node is to get your `System` instance through jspm, which will automatically load your config correctly for you:

```js
var Loader = require('jspm').Loader;
var SystemJS = new Loader();

SystemJS.import('lodash').then(function (_) {
 console.log(_);
});
```

### Promise Polyfill

SystemJS relies on `Promise` being present in the environment.

For the best performance in IE and older browsers, it is advisable to load a polyfill like [Bluebird](https://github.com/petkaantonov/bluebird) or [es6-promise](https://github.com/stefanpenner/es6-promise) before SystemJS.

### Plugins

Supported loader plugins:

* [CSS](https://github.com/systemjs/plugin-css)
* [LESS](https://github.com/systemjs/plugin-less)
* [Image](https://github.com/systemjs/plugin-image)
* [JSON](https://github.com/systemjs/plugin-json)
* [Text](https://github.com/systemjs/plugin-text)
* [Node Binary](https://github.com/systemjs/plugin-node-binary)

Additional Plugins:

* [Audio](https://github.com/ozsay/plugin-audio)
* [CoffeeScript](https://github.com/forresto/plugin-coffee)
* [Ember Handlebars](https://github.com/n-fuse/plugin-ember-hbs)
* [Handlebars](https://github.com/davis/plugin-hbs)
* [HTML](https://github.com/Hypercubed/systemjs-plugin-html/)
* [Image (lazy)](https://github.com/laurentgoudet/plugin-lazyimage)
* [Jade](https://github.com/johnsoftek/plugin-jade)
* [Jade VirtualDOM](https://github.com/WorldMaker/system-jade-virtualdom)
* [jst](https://github.com/podio/plugin-jst)
* [JSX](https://github.com/floatdrop/plugin-jsx)
* [Markdown](https://github.com/guybedford/plugin-md)
* [raw](https://github.com/matthewbauer/plugin-raw)
* [SASS](https://github.com/screendriver/plugin-sass)
* [SCSS](https://github.com/kevcjones/plugin-scss)
* [sofe](https://github.com/CanopyTax/sofe)
* [svelte](https://github.com/CanopyTax/system-svelte)
* [SVG](https://github.com/vuzonp/systemjs-plugin-svg)
* [WebFont](https://github.com/guybedford/plugin-font)
* [WebWorkers](https://github.com/casperlamboo/plugin-worker)
* [YAML](https://github.com/tb/plugin-yaml)

Guides:

* [Using plugins](docs/overview.md#plugin-loaders)
* [Creating plugins](docs/creating-plugins.md)

#### Running the tests

```
  npm run build && npm run test
```

License
---

MIT

[travis-url]: https://travis-ci.org/systemjs/systemjs
[travis-image]: https://travis-ci.org/systemjs/systemjs.svg?branch=master

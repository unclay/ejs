koa-ejs
=========

[![Build Status](https://secure.travis-ci.org/koajs/ejs.svg)](http://travis-ci.org/koajs/ejs)

Koa ejs view render middleware. support all feature of [ejs](https://github.com/mde/ejs).

[![NPM](https://nodei.co/npm/koa-ejs.png?downloads=true)](https://nodei.co/npm/koa-ejs/)

## Usage

### Example

```js
var koa = require('koa');
var render = require('koa-ejs');

var app = koa();
render(app, {
  root: path.join(__dirname, 'view'),
  layout: 'template',
  viewExt: 'html',
  cache: false,
  debug: true,
  context: {}
});

app.use(function *() {
  yield this.render('user');
});

app.listen(7001);
```

Or you can checkout the [example](https://github.com/dead-horse/koa-ejs/tree/master/example).

### Wokraround for Koa 2

```sh
npm install co --save
```
```javascript
import co from 'co';
import render from 'koa-ejs';

render(app, options);
app.context.render = co.wrap(app.context.render);

app.use(async (ctx, next) => {
    await ctx.render(view, locals);
});
```

### settings

* root: view root directory.
* layout: global layout file, default is `layout`, set `false` to disable layout.
* viewExt: view file extension (default `html`).
* cache: cache compiled templates (default `true`).
* debug: debug flag (default `false`).
* delimiter: character to use with angle brackets for open / close (default `%`).
* context: global template context

### Layouts

`koa-ejs` supports layouts. The default layout file is `layout`. If you want to change default layout file, use `settings.layout`. Also you can specify layout by `options.layout` in `yield this.render`.
Also you can set `layout = false` to disable the layout.

```
<html>
  <head>
    <title>koa ejs</title>
  </head>
  <h3>koa ejs</h3>
  <body>
    <%- body %>
  </body>
</html>
```

### Inlcude

Supports ejs includes.

```
<div>
  <% include user.html %>
</div>
```

### State

Support [`ctx.state` in koa](https://github.com/koajs/koa/blob/master/docs/api/context.md#ctxstate).

## Licences
(The MIT License)

Copyright (c) 2014 dead-horse and other contributors

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the 'Software'), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED 'AS IS', WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

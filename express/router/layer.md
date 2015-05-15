# layer.js

### 1. 模块依赖及变量定义

```javascript
/**
 * Module dependencies.
 */

var pathRegexp = require('path-to-regexp');
var debug = require('debug')('express:router:layer');

/**
 * Module variables.
 */

var hasOwnProperty = Object.prototype.hasOwnProperty;
```

# 2. 导出对象

该模块的导出对象为`Layer`类，源码如下：

```javascript
/**
 * Expose `Layer`.
 */

module.exports = Layer;

function Layer(path, options, fn) {
  if (!(this instanceof Layer)) {
    return new Layer(path, options, fn);
  }

  debug('new %s', path);
  options = options || {};

  this.handle = fn;
  this.name = fn.name || '<anonymous>';
  this.params = undefined;
  this.path = undefined;
  this.regexp = pathRegexp(path, this.keys = [], options);

  if (path === '/' && options.end === false) {
    this.regexp.fast_slash = true;
  }
}
```

其中主要是对一些实例属性的设置，主要包括：

- `handle`
- `name`
- `params`
- `path`
- `keys`
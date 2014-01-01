# Sublime UMD Snippets

JavaScript snippets for the [Universal Module Definition](https://github.com/umdjs/umd).

## Installation

Use [Package Control](https://sublime.wbond.net/installation). Search for "UMD Snippets."

Alternatively, clone this repository into your `Packages` folder.

## Usage

Each snippet is described below, with a title that you can search for in the Command Palette (prefixed by "UMD—") and with a tab trigger.

The snippets mirror (with a couple tiny differences) the templates provided in the [UMD repo](https://github.com/umdjs/umd), with fields for making it easier to configure module names and dependencies. For detailed explanations of each UMD variant, see the corresponding template in the UMD repo.

### AMD or browser global

```javascript
(function (root, factory) {
    if (typeof define === 'function' && define.amd) {
        // AMD. Register as an anonymous module.
        define(['b'], factory);
    } else {
        // Browser globals
        root.amdWeb = factory(root.b);
    }
}(this, function (b) {

    function amdWeb () {
        
    }

    return amdWeb;
}));
```

Tab trigger: **umda**

Fields:  

1. module name
2. factory dependencies
3. module parameters
4. module code

Reference: [amdWeb](https://github.com/umdjs/umd/blob/master/amdWeb.js)

### AMD with global export

```javascript
(function (root, factory) {
    if (typeof define === 'function' && define.amd) {
        // AMD. Register as an anonymous module.
        define(['b'], function (b) {
            // Also create a global in case some scripts
            // that are loaded still are looking for
            // a global even when an AMD loader is in use.
            return (root.amdWebGlobal = factory(b));
        });
    } else {
        // Browser globals
        root.amdWebGlobal = factory(root.b);
    }
}(this, function (b) {

    function amdWebGlobal () {
        
    }

    return amdWebGlobal;
}));
```

Tab trigger: **umdag**

Fields:  

1. module name
2. factory dependencies
3. module parameters
4. module code

Reference: [amdWebGlobal](https://github.com/umdjs/umd/blob/master/amdWebGlobal.js)

### CommonJS adapter

```javascript
// Help Node out by setting up define.
if (typeof exports === 'object' && typeof define !== 'function') {
    define = function (factory) {
        factory(require, exports, module);
    };
}

define(function (require, exports, module) {
    var b = require('b');

    // Only attach properties to the exports object to define
    // the module's properties.
    exports.action = function () {
        
    };
});
```

Tab trigger: **umdca**

Fields:

1. name of property on the `exports` object
2. optional dependency
3. module parameters
4. module code

Reference: [commonjsAdapter](https://github.com/umdjs/umd/blob/master/commonjsAdapter.js)

### CommonJS strict

```javascript
(function (root, factory) {
    if (typeof define === 'function' && define.amd) {
        // AMD. Register as an anonymous module.
        define(['exports', 'b'], factory);
    } else if (typeof exports === 'object') {
        // CommonJS
        factory(exports, require('b'));
    } else {
        // Browser globals
        factory((root.commonJsStrict = {}), root.b);
    }
}(this, function (exports, b) {

    // attach properties to the exports object to define
    // the exported module properties.
    exports.action = function () {
        
    };
}));
```

Tab trigger: **umdcs**

Fields:

1. global module name
2. name of property on `exports` object
3. factory dependencies
4. module parameters
5. module code

Reference: [commonjsStrict](https://github.com/umdjs/umd/blob/master/commonjsStrict.js)

### CommonJS strict with global

```javascript
(function (root, factory) {
    if (typeof define === 'function' && define.amd) {
        // AMD. Register as an anonymous module.
        define(['exports', 'b'], function (exports, b) {
            factory((root.commonJsStrictGlobal = exports), b);
        });
    } else if (typeof exports === 'object') {
        // CommonJS
        factory(exports, require('b'));
    } else {
        // Browser globals
        factory((root.commonJsStrictGlobal = {}), root.b);
    }
}(this, function (exports, b) {

    // attach properties to the exports object to define
    // the exported module properties.
    exports.action = function () {
        
    };
}));
```

Tab trigger: **umdcg**

Fields:

1. global module name
2. name of property on `exports` object
3. factory dependencies
4. module parameters
5. module code

Reference: [commonjsStrictGlobal](https://github.com/umdjs/umd/blob/master/commonjsStrictGlobal.js)

### jQuery plugin

```javascript
(function (factory) {
    if (typeof define === 'function' && define.amd) {
        // AMD. Register as an anonymous module.
        define(['jquery'], factory);
    } else {
        // Browser globals
        factory(jQuery);
    }
}(function ($) {
    $.fn.jqueryPlugin = function () {
        
    };
}));
```

Tab trigger: **umdj**

Fields:

1. plugin name
2. factory dependencies
3. plugin parameters
4. plugin code

Reference: [jqueryPlugin](https://github.com/umdjs/umd/blob/master/jqueryPlugin.js)

### jQuery plugin with CommonJS

```javascript
(function (factory) {
    if (typeof define === 'function' && define.amd) {
        // AMD. Register as an anonymous module.
        define(['jquery'], factory);
    } else {
        // Browser globals
        factory(jQuery);
    }
}(function ($) {
    $.fn.jqueryPlugin = function () {
        
    };
}));
```

Tab trigger: **umdjc**

Fields:

1. plugin name
2. factory dependencies
3. plugin parameters
4. plugin code

Reference: [jqueryPluginCommonjs](https://github.com/umdjs/umd/blob/master/jqueryPluginCommonjs.js)

### Node adapter

```javascript
// Help Node out by setting up define.
if (typeof module === 'object' && typeof define !== 'function') {
    var define = function (factory) {
        module.exports = factory(require, exports, module);
    };
}

define(function (require, exports, module) {
    var b = require('b');

    return function () {
        
    };
});
```

Tab trigger: **umdn**

Fields:

1. optional dependency
2. module parameters
3. module code

Reference: [nodeAdapter](https://github.com/umdjs/umd/blob/master/nodeAdapter.js)

### AMD, Node, or browser global

```javascript
(function (root, factory) {
    if (typeof define === 'function' && define.amd) {
        // AMD. Register as an anonymous module.
        define(['b'], factory);
    } else if (typeof exports === 'object') {
        // Node. Does not work with strict CommonJS, but
        // only CommonJS-like enviroments that support module.exports,
        // like Node.
        module.exports = factory(require('b'));
    } else {
        // Browser globals (root is window)
        root.returnExports = factory(root.b);
    }
}(this, function (b) {

    function returnExports () {
        
    }

    return returnExports;
}));
```

Tab trigger: **umdr**

Fields:

1. module name
2. factory dependencies
3. module parameters
4. module code

Reference: [returnExports](https://github.com/umdjs/umd/blob/master/returnExports.js)

### AMD with global, Node, or global

```javascript
(function (root, factory) {
    if (typeof define === 'function' && define.amd) {
        // AMD. Register as an anonymous module.
        define(['b'], function (b) {
            // Also create a global in case some scripts
            // that are loaded still are looking for
            // a global even when an AMD loader is in use.
            return (root.returnExportsGlobal = factory(b));
        });
    } else if (typeof exports === 'object') {
        // Node. Does not work with strict CommonJS, but
        // only CommonJS-like enviroments that support module.exports,
        // like Node.
        module.exports = factory(require('b'));
    } else {
        // Browser globals (root is window)
        root.returnExportsGlobal = factory(root.b);
    }
}(this, function (b) {

    function returnExportsGlobal () {
        
    }

    return returnExportsGlobal;
}));
```

Tab trigger: **umdrg**

Fields:

1. module name
2. factory dependencies
3. module parameters
3. module code

Reference: [returnExports](https://github.com/umdjs/umd/blob/master/returnExports.js)

## License

The Sublime UMD Snippets package is released under the MIT License. See [LICENSE.txt](https://github.com/garrettn/sublime-umd-snippets/blob/master/LICENSE.txt) for details.



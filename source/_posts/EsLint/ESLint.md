---
title: ESLint 配置
date: 2017-05-17 20:08:03
tags: 
    - ESLint
---

### 配置方式

1. 注释配置-使用 `JavaScript` 注释直接嵌入配置信息到文件。
2. 配置文件-可以使用 `JavaScript`， `JSON`， `YAML`文件来指定，`.eslintrc.*`

### 指定解释器选项
默认情况为 `ECMAScript 5` 语法。可以选择其他 `ECMAScript` 版本以及 `JSX` 语法。

但是支持 `JSX` 并不能支持 `React`，如果想使用 `React` 应该使用 [eslint-plugin-react](https://github.com/yannickcr/eslint-plugin-react)

分析器选项 `.eslintrc.*` 文件中使用`parserOptions`属性。可用的选项有：
* `ecmaVersion` ECMAScript语法的版本，默认为3,5
* `sourceType` 设置"script"（默认值）或者"module"如果你的代码是在ECMAScript中的模块。
* `ecmaFeatures` 指示哪些额外的语言特性的对象
	* `globalReturn`  允许在全局范围 `return`
	* `impliedStrict` 使用全局严格模式
	* `jsx` 使用JSX
	* `experimentalObjectRestSpread` 启用对实验性支持对象静止/扩展性

```
{
    "parserOptions": {
        "ecmaVersion": 6,
        "sourceType": "module",
        "ecmaFeatures": {
            "jsx": true
        }
    },
}
```

### 指定解释器
默认情况下，`ESLint` 使用 `Espree`作为解释器

也可以使用以下解释器：
* `Esprima`
* `Babel-ESLin`

```
{
    "parser": "esprima",
    "rules": {
        "semi": "error"
    }
}
```

### 指定环境

可用的有：
* `browser` - 浏览器全局变量。
* `node` - `Node.js`加载全局变量和Node.js的作用域。
* `commonjs` - CommonJS的全局变量和CommonJS的作用域（用这个使用Browserify /只的WebPack浏览器的代码）。
* `shared-node-browser` - 全局常见的两种节点和浏览器。
* `es6`-使除了模块的所有的 `ECMAScript 6` 的特性（这自动地将设置ecmaVersion解析器选项〜6）。
* `worker` - 网络工作者全局变量。
* `amd`-定义 `require()` 和 `define()` 全局变量为每AMD规范。
* `mocha` - 将所有的 `mocha` 全局变量。
* `jasmine` - 将所有的`jasmine`的1.3和2.0版本测试全局变量。
* `jest` - `jest` 全局变量。
* `phantomjs` - `PhantomJS` 全局变量。
* `protractor` - `protractor` 全局变量。
* `qunit` - `QUnit` 全局变量。
* `jquery` - `jQuery` 的全局变量。
* `prototypejs` - `Prototype.js` 全局变量。
* `shelljs` - `ShellJS`全局变量。
* `meteor` - `meteor`全局变量。
* `mongo` - `MongoDB` 的全局变量。
* `applescript` -` AppleScript` 的全局变量。
* `nashorn` - `Java 8 Nashorn` 全局变量。
* `serviceworker` - `serviceworker` 的全局变量。
* `atomtest` - `atomtest` 全局变量。
* `embertest` -  `embertest` 全局变量。
* `webextensions` -  `webextensions` 全局变量
* `greasemonkey` - `GreaseMonkey` 全局变量。

这些环境不是相互排斥的，所以你可以定义一个超过一次。

环境可以文件的内部被指定，在配置文件或使用--env 命令行标志，例如：
```javascipt
/* eslint-env node, mocha */
```
要在配置文件中指定的环境中，使用env键，并指定要由每设置要启用的环境true
```
{
    "env": {
        "browser": true,
        "node": true
    }
}
```
或在一个package.json文件
```
{
    "name": "mypackage",
    "version": "0.0.1",
    "eslintConfig": {
        "env": {
            "browser": true,
            "node": true
        }
    }
}
```
### 全局说明
使用没有声明的变量会被警告，但如果使用的是文件里的全局变量使 `ESLint` 不会发出警告。

##### JavaScript 注释方式：
```
/* global var1, var2 */
```
如果你想选择指定这些全局变量不应该被写入（只读），那么你可以设置每一个false标志：

```
/* global var1:false, var2:false */
```
##### 配置文件方式：
```
{
    "globals": {
        "var1": true,
        "var2": false
    }
}
```

### 配置插件
`ESLint` 支持使用第三方插件。使用插件之前，你必须使用 `npm` 来安装它。
要配置一个配置文件内的插件，使用的 `plugins` 键，其中包含插件名称的列表。该 `eslint-plugin-` 前缀可以从插件名称被省略。

例如：
```
{
    "plugins": [
        "plugin1",
        "eslint-plugin-plugin2"
    ]
}
```
### 配置规则

##### 注释方式：
```
/* eslint eqeqeq: "off", curly: "error" */
```
在该示例中，`eqeqeq` 关闭，`curly` 为错误。也可以使用数字相当于该规则的严重性：
```
/* eslint eqeqeq: 0, curly: 2 */
```
如果规则有更多的选项，你可以使用数组文本语法，如指定它们：
```
/* eslint quotes: ["error", "double"], curly: 2 */
```
##### 配置文件方式：
```
{
    "rules": {
        "eqeqeq": "off",
        "curly": "error",
        "quotes": ["error", "double"]
    }
}
```

**注意**：当从插件指定的规则，一定要忽略 `eslint-plugin-` 。`ESLint` 只使用前缀的名称在内部找到规则。

### 文件中暂时禁用 `ESLint`
例如：
```
/* eslint-disable */
alert('foo');
/* eslint-enable */
```
还可以禁用或启用特定规则的警告：
```
/* eslint-disable no-alert, no-console */
alert('foo');
console.log('bar');
/* eslint-enable no-alert, no-console */
```
要禁用特定行上的规则：
```
alert('foo'); // eslint-disable-line

// eslint-disable-next-line
alert('foo');
```

### 使用配置文件
```
eslint -c myconfig.json myfiletotest.js
```

### 规则
详细规则参考[官方文档](http://eslint.org/docs/rules/#stylistic-issues)


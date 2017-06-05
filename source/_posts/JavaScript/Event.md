---
title: JavaScript 事件捕获和冒泡
date: 2016-09-04 13:30:44
tags: 
    - JavaScript
---

## 规范
在最新的 DOM 规范中，事件的捕获与冒泡是通过 `addEventListener(...arg)` 的第三个参数的 `capture`来指定的。默认为 `false`,也就是默认冒泡。
```
addEventListener(type, listener, {
    capture: false,
    passive: false,
    once: false
})
```

## 触发规则

在多个嵌套情况下，捕获的触发是从外到内的，冒泡则相反。先进行捕获，然后是冒泡。

** 这里要注意一点，在最后的一层中，先触发冒泡或捕获决定于代码中出现的先后，先出现的先执行。 **
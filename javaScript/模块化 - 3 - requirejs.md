# require.js
## 产生原因
```js
    <script src="1.js"></script>
　　 <script src="2.js"></script>
　 　<script src="3.js"></script>
　　 <script src="4.js"></script>
　　 <script src="5.js"></script>
　　 <script src="6.js"></script>
```
文件很多，会依次加载，加载的时候，浏览器会停止渲染。
如果文件之间存在依赖，必须要保证顺序。

解决问题：
1. 实现 js 文件的异步加载，避免网页失去响应。
2. 管理模块之间的依赖性，便于代码编写和维护。


### requirejs 引用文件时路径问题

requirejs 引用时的路径是根据入口 html 的相对路径，不是模块文件之间的相对路径
```
    - js
        - a.js
        - b.js
        - c.js
        - index.js
    - index.html
    在 index.js 中引用 a.js 时，不能根据 a.js 相对于 index.js 的相对路径，
    而要根据 a.js 相对于 index.html 的相对路径 
```


#### 只有在前边的模块都加在成功后，回调才会运行
解决了依赖性问题 
并且三个模块都是异步加载，所以不会阻塞浏览器，不会导致浏览器失去响应

```js
require.config({
    baseUrl: './js',
    paths  : {
        'a'     : 'a',
        'b'     : 'b',
        'c'     : 'c',
        'jQuery': 'https://cdn.bootcss.com/jquery/3.3.1/jquery.min'
    }
});
// require 的 baseUrl 对各模块中的 define 都有效
require(['a', 'b', 'c', 'jQuery'], function(a, b, c, $ = jQuery) {
    console.log($, 'jQuery');
    console.log(123);
});
```
这样 a.js，b.js，c.js，jQuery 每个模块都会单独发一次 HTTP 请求，会影响页面的加载速度。
requirejs 有提供[工具](http://requirejs.org/docs/optimization.html)来进行优化，
合并请求。

#### 模块定义，AMD 写法
模块必须采用特定的 define 函数来定义。
如果一个模块不依赖其他模块，可以直接定义在 define 函数中。
```js
// a.js
define(function() {
    let a = 5;
    return a;
})

```
如果一个模块依赖其他模块，第一个参数必须是一个数组，并指明该模块的依赖性。
```js
// b.js
define(['a'],function(a) {
    let b = 6;
    let add = () => a + b;
    return {add}
})
```
#### 加载非 AMD 标准模块
使用 require.config
```js
require.config({
    shim: {
        'underscore': {
            exports: '_'
        },
        'backbone': {
            deps: ['underscore', 'jquery'],
            exports: 'Backbone'
        }
    }
})
```
1. exports 表明模块外部调用时的名称。
2. deps 表明该模块的依赖。



## 参考文档
- [Javascript模块化编程（三）：require.js的用法](http://www.ruanyifeng.com/blog/2012/11/require_js.html)

## Demo
- [requirejs](https://github.com/luoyin1994/test/tree/master/module-pattern/requirejs) 
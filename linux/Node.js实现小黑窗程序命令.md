# Node.js 实现小黑窗程序命令

## 小黑窗可执行 node 文件 hello 
```
    echo "#!/usr/bin/env node" > hello.bash  # 创建文件 hello.bash ，并写入“#!/usr/bin/env node”让node可执行js
    > hello.js 创建 hello.js
```
```js
    // hello.js
    console.log('hello world');
```
```
    cat hello.bash hello.js > hello  # 创建文件 hello 
    chmod 755 hello  # 修改权限让 hello 文件可执行
    ./hello  # 打印出 hello world 
```
去掉 ./hello 的前缀路径，在该目录下创建 package.json 。
```json
    {
        "name": "hello",
        "bin": {
            "hello": "hello"
        }
    }
```
```
    npm link  # 相当于全局安装了该执行文件 hello （npm i -g hello），并且在“hello”所在目录下会出现同 hello 文件同级的 node_modules/.bin 
```
## 系统变量 [process.argv](http://nodejs.cn/api/process.html#process_process_argv)

process.argv属性返回一个数组，由命令行执行脚本时的各个参数组成。它的第一个成员总是node，第二个成员是脚本文件名，其余成员是脚本文件的参数。
```js
    // hello.js
    console.log('hello', process.argv[2]);
```
```
    cat hello.bash hello.js > hello
    hello node  # 打印出 hello node
```
## child_process 新建子进程，执行 Unix 命令
```js
    // hello.js
    var name = process.argv[2];
    var exec = require('child_process').exec;
    var child = exec('echo hello ' + name, function(err, stdout, stderr) {
      if (err) throw err;
      console.log(stdout);
    });
    
```
```
    cat hello.bash hello.js > hello
    hello child  # 打印出 hello child
```

## 封装了 child_precess 的 shelljs

### 安装
```
    npm i --save shelljs
```

### 本地模式
```js
    // hello.js
    var name = process.argv[2];
    var shell = require("shelljs");

    shell.exec("echo hello " + name);
```
```
    cat hello.bash hello.js > hello
    hello shelljs  # 打印出 hello shelljs
```

### 全局模式
```js
    // hello.js
    var name = process.argv[2];
    var shell = require("shelljs/global");

    exec("echo hello global");
    exec("echo hello " + name);
```
```
    cat hello.bash hello.js > hello
    hello shelljs  # 打印出 hello global; hello shelljs
```

## yargs 处理参数

### 安装
```
    npm install --save yargs
```
```js
    var argv = require('yargs').argv;

    console.log('hello ', argv.name);
```
```
    cat hello.bash hello.js > hello
    hello --name=yargs  # 打印出 hello yargs
    hello --name yargs  # 打印出 hello yargs
```
### 别名
短参数可以使用 -x 的形式，长参数使用 -xxx 会显示 true， --xxx才会显示真实参数。
```js
    var argv = require('yargs')
        .alias('n', 'name')
        .argv;
    
        console.log('hello ', argv.n);
```
```
    cat hello.bash hello.js > hello
    hello -n=yargs  # 打印出 hello yargs
    hello -n=yargs  # 打印出 hello yargs
    hello --n yargs  # 打印出 hello yargs
    hello --n yargs  # 打印出 hello yargs
    hello --name=yargs  # 打印出 hello yargs
    hello --name yargs  # 打印出 hello yargs  
```
### 方法
```
    alias：别名
    demand：是否必选
    default：默认值
    describe：提示
    options：允许将所有这些配置写进一个对象
```

## 参考文档
* [阮一峰 - Node.js 命令行程序开发教程](http://www.ruanyifeng.com/blog/2015/05/command-line-with-node.html)
* [阮一峰 JavaScript 标准参考教程（alpha） - process对象](http://javascript.ruanyifeng.com/nodejs/process.html#toc4)
* [node - process.argv(中)](http://nodejs.cn/api/process.html#process_process_argv)
* [node - process.argv(英)](https://nodejs.org/docs/latest/api/process.html#process_process_argv)




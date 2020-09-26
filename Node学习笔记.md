







# Node介绍

## 为什么要学习Node.js

- 企业需求
  - 具有服务端开发经验更改
  - front-end
  - back-end
  - 全栈开发工程师
  - 基本的网站开发能力
    - 服务端
    - 前端
    - 运维部署
  - 多人社区

![image-20200317114503403](C:\Users\A\AppData\Roaming\Typora\typora-user-images\image-20200317114503403.png)

## Node.js是什么

- Node.js是JavaScript 运行时
- 通俗易懂的讲，Node.js是JavaScript的运行平台
- Node.js既不是语言，也不是框架，它是一个平台
- 浏览器中的JavaScript
  - EcmaScript
    - 基本语法
    - if
    - var
    - function
    - Object
    - Array
  - Bom
  - Dom
- Node.js中的JavaScript
  - 没有Bom，Dom
  - EcmaScript
  - 在Node中这个JavaScript执行环境为JavaScript提供了一些服务器级别的API
    - 例如文件的读写
    - 网络服务的构建
    - 网络通信
    - http服务器
- 构建与Chrome的V8引擎之上
  - 代码只是具有特定格式的字符串
  - 引擎可以认识它，帮你解析和执行
  - Google Chrome的V8引擎是目前公认的解析执行JavaScript代码最快的
  - Node.js的作者把Google Chrome中的V8引擎移植出来，开发了一个独立的JavaScript运行时环境
- Node.js uses an envent-driven,non-blocking I/O mode that makes it lightweight and efficent.
  -  envent-driven	事件驱动
  - non-blocking I/O mode   非阻塞I/O模型（异步）
  - ightweight and efficent.   轻量和高效
- Node.js package ecosystem,npm,is the larget scosystem of open sourcr libraries in the world
  - npm 是世界上最大的开源生态系统
  - 绝大多数JavaScript相关的包都存放在npm上，这样做的目的是为了让开发人员更方便的去下载使用
  - npm install jquery

## Node能做什么

- web服务器后台
- 命令行工具
  - npm(node)
  - git(c语言)
  - hexo（node）
  - ...
- 对于前端工程师来讲，接触最多的是它的命令行工具
  - 自己写的很少，主要是用别人第三方的
  - webpack
  - gulp
  - npm

# 起步

## 安装Node环境

- 查看Node环境的版本号
- 下载：https://nodejs.org/en/
- 安装：
  - 傻瓜式安装，一路`next`
  - 安装过再次安装会升级
- 确认Node环境是否安装成功
  - 查看node的版本号：`node --version`
  - 或者`node -v`
- 配置环境变量

## 解析执行JavaScript

1. 创建编写JavaScript脚本文件
2. 打开终端，定位脚本文件的所属目录
3. 输入`node  文件名`执行对应的文件

注意：文件名不要用`node.js`来命名，也就是说除了`node`这个名字随便起，最好不要使用中文。

## 文件的读写

文件读取:

```javascript
//浏览器中的JavaScript是没有文件操作能力的
//但是Node中的JavaScript具有文件操作能力
//fs是file-system的简写，就是文件系统的意思
//在Node中如果想要进行文件的操作就必须引用fs这个核心模块
//在fs这个和兴模块中，就提供了人所有文件操作相关的API
//例如 fs.readFile就是用来读取文件的

//  1.使用fs核心模块
var fs = require('fs');

// 2.读取文件
fs.readFile('./data/a.txt',function(err,data){
   if(err){
        console.log('文件读取失败');
   }
    else{
         console.log(data.toString());
    }
})
```

文件写入：

```javascript
//  1.使用fs核心模块
var fs = require('fs');

// 2.将数据写入文件
fs.writeFile('./data/a.txt','我是文件写入的信息',function(err,data){
   if(err){
        console.log('文件写入失败');
   }
    else{
         console.log(data.toString());
    }
})
```

## http

服务器：

```javascript
// 1.加载http核心模块
var http = require('http');

// 2.使用http.createServer()创建一个web服务器
var server = http.createServer();

// 3.服务器要做的事儿
// 提供服务：对数据服务
// 发请求
//	接收请求
//	处理请求
//	反馈（发送响应）
//	当客户端请求过来，就会自动触发服务器的request请求事件，然后执行第二个参数：回调处理函数
server.on('request',function(){
    console.log('收到客户的请求了')
})

// 4.绑定端口号，启动服务
server.listen(3000,function(){
    console.log('runing...')
})

```

# Node中的模块系统

使用Node编写应用程序主要就是在使用：

- EcmaScript语言
  - 和浏览器一样，在Node中没有Bom和Dom

- 核心模块
  - 文件操作的fs
  - http服务操作的http
  - url路径操作模块
  - path路径处理模块
  - os操作系统信息
- 第三方模块
  - art-template
  - 必须通过npm来下载才可以使用
- 自己写的模块
  - 自己创建的文件



## 什么是模块化

- 文件作用域(模块是独立的，在不同的文件使用必须要重新引用)【在node中没有全局作用域，它是文件模块作用域】
- 通信规则
  - 加载require
  - 导出exports

## CommonJS模块规范

在Node中的JavaScript还有一个重要的概念，模块系统。

- 模块作用域

- 使用require方法来加载模块

- 使用exports接口对象来导出模板中的成员

  ### 加载`require`

  语法：

  ~~~java
  var 自定义变量名 = require('模块')
  ~~~

  作用：

  - 执行被加载模块中的代码
  - 得到被加载模块中的`exports`导出接口对象

  ### 导出`exports`

  - Node中是模块作用域，默认文件中所有的成员只在当前模块有效

  - 对于希望可以被其他模块访问到的成员，我们需要把这些公开的成员都挂载到`exports`接口对象中就可以了

    导出多个成员（必须在对象中）：

    ```javascript
    exports.a = 123;
    exports.b = function(){
        console.log('bbb')
    };
    exports.c = {
        foo:"bar"
    };
    exports.d = 'hello';
    ```

    

    导出单个成员（拿到的就是函数，字符串）：

    ```javascript
    module.exports = 'hello';
    ```

    以下情况会覆盖：

    ```javascript
    module.exports = 'hello';
    //后者会覆盖前者
    module.exports = function add(x,y) {
        return x+y;
    }
    ```

    也可以通过以下方法来导出多个成员：

    ```javascript
    module.exports = {
        foo = 'hello',
        add:function(){
            return x+y;
        }
    };
    ```

## 模块原理

exports和`module.exports`的一个引用：

```javascript
console.log(exports === module.exports);	//true

exports.foo = 'bar';

//等价于
module.exports.foo = 'bar';
```

`当给exports重新赋值后，exports！= module.exports.`

`最终return的是module.exports,无论exports中的成员是什么都没用。`

```javascript
真正去使用的时候：
	导出单个成员：exports.xxx = xxx;
	导出多个成员：module.exports 或者 modeule.exports = {};
```

## 总结

```javascript
// 引用服务
var http = require('http');
var fs = require('fs');
// 引用模板
var template = require('art-template');
// 创建服务
var server = http.createServer();
// 公共路径
var wwwDir = 'D:/app/www';
server.on('request', function (req, res) {
    var url = req.url;
    // 读取文件
    fs.readFile('./template-apche.html', function (err, data) {
        if (err) {
            return res.end('404 Not Found');
        }
        fs.readdir(wwwDir, function (err, files) {
            if (err) {
                return res.end('Can not find www Dir.')
            }
            // 使用模板引擎解析替换data中的模板字符串
            // 去xmpTempleteList.html中编写模板语法
            var htmlStr = template.render(data.toString(), { 
                title: 'D:/app/www/ 的索引',
                files:files 
            });
            // 发送响应数据
            res.end(htmlStr);
        })
    })
});
server.listen(3000, function () {
    console.log('running....');
})
```

```javascript
1.jQuery中的each 和 原生JavaScript方法forEach的区别：
	提供源头：
    	原生js是es5提供的（不兼容IE8）,
        jQuery的each是jQuery第三方库提供的（如果要使用需要用2以下的版本也就是1.版本）,它的each方法主要用来遍历jQuery实例对象（伪数组）,同时也可以做低版本forEach的替代品,jQuery的实例对象不能使用forEach方法，如果想要使用必须转为数组（[].slice.call(jQuery实例对象)）才能使用
2.模块中导出多个成员和导出单个成员
3.301和302的区别：
	301永久重定向,浏览器会记住
    302临时重定向
4.exports和module.exports的区别:
	每个模块中都有一个module对象
    module对象中有一个exports对象
    我们可以把需要导出的成员都挂载到module.exports接口对象中
	也就是`module.exports.xxx = xxx`的方式
    但是每次写太多了就很麻烦，所以Node为了简化代码，就在每一个模块中都提供了一个成员叫`exports`
    `exports === module.exports`结果为true,所以完全可以`exports.xxx = xxx`
    当一个模块需要导出单个成员的时候必须使用`module.exports = xxx`的方式，=,使用`exports = xxx`不管用,因为每个模块最终return的是module.exports,而exports只是module.exports的一个引用,所以`exports`即使重新赋值,也不会影响`module.exports`。
    有一种赋值方式比较特殊：`exports = module.exports`这个用来新建立引用关系的。
    
```

# require的加载规则

- 核心模块

  - 模块名

- 第三方模块

  - 模块名

- 用户自己写的

  - 路径




## require的加载规则：

- 优先从缓存加载

- 判断模块标识符

  - 核心模块
  - 自己写的模块（路径形式的模块）
  - 第三方模块（node_modules）
    - 第三方模块的标识就是第三方模块的名称（不可能有第三方模块和核心模块的名字一致）
    - npm
      - 开发人员可以把写好的框架库发布到npm上
      - 使用者通过npm命令来下载
    - 使用方式：`var 名称 = require('npm install【下载包】 的包名')`
      - node_modules/express/package.json main
      - 如果package.json或者main不成立，则查找被选择项：index.js
      - 如果以上条件都不满足，则继续进入上一级目录中的node_modules按照上面的规则依次查找，直到当前文件所属此盘根目录都找不到最后报错



```javascript
// 如果非路径形式的标识
// 路径形式的标识：
    // ./  当前目录 不可省略
    // ../  上一级目录  不可省略
    //  /xxx也就是D:/xxx
    // 带有绝对路径几乎不用（D:/a/foo.js）
// 首位表示的是当前文件模块所属磁盘根目录
// require('./a'); 


// 核心模块
// 核心模块本质也是文件，核心模块文件已经被编译到了二进制文件中了，我们只需要按照名字来加载就可以了
require('fs'); 

// 第三方模块
// 凡是第三方模块都必须通过npm下载（npm i node_modules），使用的时候就可以通过require('包名')来加载才可以使用
// 第三方包的名字不可能和核心模块的名字是一样的
// 既不是核心模块，也不是路径形式的模块
//      先找到当前文所述目录的node_modules
//      然后找node_modules/art-template目录
//      node_modules/art-template/package.json
//      node_modules/art-template/package.json中的main属性
//      main属性记录了art-template的入口模块
//      然后加载使用这个第三方包
//      实际上最终加载的还是文件

//      如果package.json不存在或者mian指定的入口模块不存在
//      则node会自动找该目录下的index.js
//      也就是说index.js是一个备选项，如果main没有指定，则加载index.js文件
//      
        // 如果条件都不满足则会进入上一级目录进行查找
// 注意：一个项目只有一个node_modules，放在项目根目录中，子目录可以直接调用根目录的文件
var template = require('art-template');

```

## 模块标识符中的`/`和文件操作路径中的`/`

文件操作路径：

```javascript
// 咱们所使用的所有文件操作的API都是异步的
// 就像ajax请求一样
// 读取文件
// 文件操作中 ./ 相当于当前模块所处磁盘根目录
// ./index.txt    相对于当前目录
// /index.txt    相对于当前目录
// /index.txt   绝对路径,当前文件模块所处根目录
// d:express/index.txt   绝对路径
fs.readFile('./index.txt',function(err,data){
    if(err){
       return  console.log('读取失败');
    }
    console.log(data.toString());
})
```

模块操作路径：

```javascript
// 在模块加载中，相对路径中的./不能省略
// 这里省略了.也是磁盘根目录
require('./index')('hello')
```



# npm

- node package manage(node包管理器)
- 通过npm命令安装jQuery包（npm install --save jquery），在安装时加上--save会主动生成说明书文件信息（将安装文件的信息添加到package.json里面）

### npm网站

> ​	npmjs.com	网站   是用来搜索npm包的

### npm命令行工具

npm是一个命令行工具，只要安装了node就已经安装了npm。

npm也有版本概念，可以通过`npm --version`来查看npm的版本

升级npm(自己升级自己)：

```javascript
npm install --global npm
```

### 常用命令

- npm init(生成package.json说明书文件)
  - npm init -y(可以跳过向导，快速生成)
- npm install
  - 一次性把dependencies选项中的依赖项全部安装
  - 简写（npm i）
- npm install 包名
  - 只下载
  - 简写（npm i 包名）
- npm install --save 包名
  - 下载并且保存依赖项（package.json文件中的dependencies选项）
  - 简写（npm i  包名）
- npm uninstall 包名
  - 只删除，如果有依赖项会依然保存
  - 简写（npm un 包名）
- npm uninstall --save 包名
  - 删除的同时也会把依赖信息全部删除
  - 简写（npm un 包名）
- npm help
  - 查看使用帮助
- npm 命令 --help
  - 查看具体命令的使用帮助（npm uninstall --help）

### 解决npm被墙问题

npm存储包文件的服务器在国外，有时候会被墙，速度很慢，所以需要解决这个问题。

> https://developer.aliyun.com/mirror/NPM?from=tnpm淘宝的开发团队把npm在国内做了一个镜像（也就是一个备份）。
>

安装淘宝的cnpm：

```javascript
npm install -g cnpm --registry=https://registry.npm.taobao.org;
```



```shell
#在任意目录执行都可以
#--global表示安装到全局，而非当前目录
#--global不能省略，否则不管用
npm install --global cnpm
```

安装包的时候把以前的`npm`替换成`cnpm`。

```shell
#走国外的npm服务器下载jQuery包，速度比较慢
npm install jQuery;

#使用cnpm就会通过淘宝的服务器来下载jQuery
cnpm install jQuery;
```

如果不想安装`cnpm`又想使用淘宝的服务器来下载：

```shell
npm install jquery --registry=https://npm.taobao.org;
```

但是每次手动加参数就很麻烦，所以我们可以把这个选项加入到配置文件中：

```shell
npm config set registry https://npm.taobao.org;

#查看npm配置信息
npm config list;
```

只要经过上面的配置命令，则以后所有的`npm install`都会通过淘宝的服务器来下载

# package.json

每一个项目都要有一个`package.json`文件（包描述文件，就像产品的说明书一样）

这个文件可以通过`npm init`自动初始化出来

```javascript

D:\code\node中的模块系统>npm init
This utility will walk you through creating a package.json file.
It only covers the most common items, and tries to guess sensible defaults.

See `npm help json` for definitive documentation on these fields
and exactly what they do.

Use `npm install <pkg>` afterwards to install a package and
save it as a dependency in the package.json file.

Press ^C at any time to quit.
package name: (node中的模块系统)
Sorry, name can only contain URL-friendly characters.
package name: (node中的模块系统) cls
version: (1.0.0)
description: 这是一个测试项目
entry point: (main.js)
test command:
git repository:
keywords:
author: xiaochen
license: (ISC)
About to write to D:\code\node中的模块系统\package.json:

{
  "name": "cls",
  "version": "1.0.0",
  "description": "这是一个测试项目",
  "main": "main.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "xiaochen",
  "license": "ISC"
}


Is this OK? (yes) yes
```

对于目前来讲，最有用的是`dependencies`选项，可以用来帮助我们保存第三方包的依赖信息。

如果`node_modules`删除了也不用担心，只需要在控制面板中`npm install`就会自动把`package.json`中的`dependencies`中所有的依赖项全部都下载回来。

- 建议每个项目的根目录下都有一个`package.json`文件
- 建议执行`npm install 包名`的时候都加上`--save`选项，目的是用来保存依赖信息

## package.json和package-lock.json

npm 5以前是不会有`package-lock.json`这个文件

npm5以后才加入这个文件

当你安装包的时候，npm都会生成或者更新`package-lock.json`这个文件

- npm5以后的版本安装都不要加`--save`参数，它会自动保存依赖信息
- 当你安装包的时候，会自动创建或者更新`package-lock.json`文件
- `package-lock.json`这个文件会包含`node_modules`中所有包的信息（版本，下载地址。。。）
  - 这样的话重新`npm install`的时候速度就可以提升
- 从文件来看，有一个`lock`称之为锁
  - 这个`lock`使用来锁版本的
  - 如果项目依赖了`1.1.1`版本
  - 如果你重新install其实会下载最细版本，而不是`1.1.1`
  - ``package-lock.json``的另外一个作用就是锁定版本号，防止自动升级

## path路径操作模块

> 参考文档：https://nodejs.org/docs/latest-v13.x/api/path.html

- path.basename：获取路径的文件名，默认包含扩展名
- path.dirname：获取路径中的目录部分
- path.extname：获取一个路径中的扩展名部分
- path.parse：把路径转换为对象
  - root：根路径
  - dir：目录
  - base：包含后缀名的文件名
  - ext：后缀名
  - name：不包含后缀名的文件名
- path.join：拼接路径
- path.isAbsolute：判断一个路径是否为绝对路径![image-20200315150610001](C:\Users\A\AppData\Roaming\Typora\typora-user-images\image-20200315150610001.png)

# Node中的其它成员(__
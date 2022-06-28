# node.js介绍

### 为什么学习node.js

###### 企业需求

1.具有服务端开发经验更好

2.不仅仅会做前端，还要会做后端

3.做全栈开发工程师

4.基本的网站开发能力

  - 服务端
  - 前端
  - 运维部署

### node.js是什么

###### node.js是一个js的运行环境

1. node不是一门语言也不是库不是框架，简单来说就是node.js课解析和执行js代码
2. 以前只有浏览器可以执行js代码，现在js完全可以脱离浏览器运行

###### 浏览器中的js

1. EomaScript(基本的语法)
2. BOM
3. DOM

###### node中的js

1. 没有BOM和DOM，只有EomaScript，服务器不操作页面

2. 在node这个运行环境中为js提供了一些服务器级别的aip

     - 例如文件的读写
     - 网络服务的构建
     - 网络通信
     - http服务器
     - ...
     - 学node就是在学web服务器开发

   3.构建于chrome的v8引擎之上

   - 代码只是具有特定意义的字符串
   - 引擎可以识别代码并解析执行
   - Goole Chorme V8引擎是现在公认解析js代码最快的
   - Node.js的作者把chrome v8引擎移植出来，开发了一个独立的js运行环境

### node.js的特性

- 事件驱动
- 非阻塞I/O模型(异步) 
	- node 绝大部分操作都支持回调(callback)，也就是异步
	- 异步会带来更好的性能
- 轻量高效
- npm是node.js开发的包管理工具
- npm是世界上最大的开源库生态系统
- 绝大多数js相关的包都放在了npm上，这样做的目的是方便开发人员下载
- node中的全局对象是global

### node.js能做什么

###### web服务器后台

###### 命令行工具

- npm (node)
- git(c语言)
- ...

- 对于前端开发工程师来说，接触node最多的是它的命令行工具
  - webpack
  - npm
  - ...

### 学习内容

###### B/S编程模型

- Browser-Server 浏览器服务器之间的编程模型
- back-end 服务器开发
- 任何服务端技术的B/S编程模型都是一样的，只是语言不通
- node只是作为我们学习BS编程模型的工具

###### 模块化编程

- RequireJS
- SeaJS
- 以前认知的js只能通过script来加载执行别的文件
- 在node中可以使用import来加载js脚本文件

###### node常用aip

###### 异步编程

- 回调函数
- Promise
- async
- generator

###### express Web开发框架



# 依赖管理工具(npm,yarn)

###### npm

- 查询镜像：npm get registry
- 配置淘宝镜像：npm config set registry http://registry.npm.taobao.org/
- 配置原镜像：npm config set registry https://registry.npmjs.org/
###### yarn
- 查询镜像：yarn config get registry
- 配置淘宝镜像：yarn config set registry http://registry.npm.taobao.org/
- 配置原镜像：yarn config set registry http://registry.npmjs.org/

# 核心模块

- `node` 为 `js` 提供了很多服务器级别的 `api` ，这些 `api` 绝大多数都被包装到了一个具名的核心模块中。例如文件操作的 `fs` 核心模块，`http` 服务构建的 `http` 模块，`path`路径操作模块，`os` 操作系统模块。加载模块需要使用 `require()` 方法。

```js
const fs = require('fs')
const http = require('http')
const path = require('path')
```

## fs模块

### 功能

fs是file-system的缩写，就是文件系统的意思，在node中如果想要进行文件操作，就必须引入fs模块，fs模块提供了所有文件操作相关的API

### 加载模块

```js
const fs = require('fs')
```

### 读取文件

```js
 fs.readFile('path', (error, data) => {
     if (error) {
         console.log(error)
     }
     console.log(data) 
     //16进制数据，可使用toString()转化成字符串
 })
```
- 第一个参数是读取的文件路径
- 第二个参数是一个回调函数，它接受两个参数
    - error
    - data
    - 文件读取成功：data是数据；error为null
    - 文件读取失败：data为null；error是错误对象
- **注意：**文件中默认存储的是二进制数据；电脑会转成16进制，使用 `toString` 方法可以转化成字符串

### 写入文件

```js
fs.writeFile('path', '写入内容', (error) => {
    console.log('文件写入成功')
})
```
- 参数1：文件路径
- 参数2：写入内容
- 参数3：回调函数，该回调函数只接受一个参数error
    - 成功：文件写入成功；error为null
    - 失败：文件写入失败；error是错误对象
- 如果当前路径下没有该文件，`fs.writeFile` 会创建这个文件
- 电脑系统不支持文件名中含有特殊符号，比如 `* > <` 等等，如果文件名中含有这些符号就会出现写入失败的情况

### 5. 其他操作
#### 读取目录
- 读取一个目录下的所有内容（无论目录下是文件还是文件夹） `fs.readdir()`
  ```js
  fs.readdir('path', (err, files) => {
    if (err) {
      console.log(err);
    } else {
      console.log(files);
    }
  })
  //读取path文件，结果是一个数组，数组的每项都是该目录下的子目录
```
## http模块

### 功能
- `http` 模块的职责就是帮我们创建编写服务器的

### 加载模块
```js
const http = require('http')
```
### 创建web服务器
- `http` 模块提供了 `http.createServer()` 方法来创建 `web` 服务器
```js
const server = http.createServer()
```
### 提供服务
- 提供对数据的服务：浏览器发送请求，服务器接受请求并处理，给出反馈(发送响应)
```js
const server = http.createServer()
server.on('request', (request, response) => {
    conslole.log('收到客户端请求，路径是' + request.url)
    response.write('hello node.js')
    response.write('hello')
    response.end('404 Not Found')
})
```
- 可以在 `server.on` 中配置路由，这里使用 `swith` 分支来配置路由，也可以使用 `if else`

```js
server.on('request', (request, response) => {
  response.setHeader('Content-Type', 'text/plain; charset=utf-8')
  switch (request.url) {
    case '/index':
      response.write('index')
      break
    case '/page':
      response.setHeader('Content-Type', 'text/html; charset=utf-8')
      response.write('<h1>page</h1>')
      break
    case '/data':
      response.write(JSON.stringify(data))
      break
    default:
      response.write('空空如也')
      break
  }
  response.end()
})

```
- 第二种配置路由的方式，路由名由文件路径决定，初始路由设置为 `fileUrl = index.html`，当 `req.url` 不为 `index.html` 时，将其赋值给 `fileUrl` ，这样就可以直接根据文件地址来读取到文件，不用再写繁杂的分支语句来判断读取哪个文件

```js
const http = require('http')
const path = require('path')
const server = http.createServer()
const fs = require('fs')

server.on('request', (req, res) => {
  let fileUrl = 'index.html'
  if (req.url !== '/') {
    fileUrl = req.url
  }
  fs.readFile(path.join(__dirname, fileUrl), (err, data) => {
    if (err) {
      res.setHeader('Content-Type', 'text/plain; charset=utf-8')
      res.end('404 Not Found')
    } else {
      res.end(data)
    }
  })
})

server.listen(3000, () => {
  console.log('3000端口已启动');
})
```

### url

- `url` 叫做统一资源定位符，一个 `url` 最终要对应到一个资源
- `server.on` 有两个参数：
    - 参数一：`request`，注册 `request` 请求事件
    - 参数二：回调函数，该回调函数接受两个对象参数
      - `request`：请求对象
      - `response`：响应对象，`response` 对象提供了 `write` 方法给客户端发送响应数据，`write` 可以使用多次，但最后一定要用 `end` 来结束响应，否则客户端会一直等待
      - 注意：发送响应的数据只能是二进制或者 `string`，`number,array,object()` 都不行，此时就可以使用 `json` 中的 `JSON.parse()` 和 `JSON.stringfy()` 方法进行转换
      - `JSON.parse()`：字符串转化成数据类型，例如 `JSON.parse('[]') --> []`
      - `JSON.stringfy()`：数据类型转化成字符串，例如 `JSON.stringfy([]) --> '[]'`

当客户端发请求过来，就会自动触发服务器的request请求事件，然后执行回调函数

### 监听端口
- 监听端口号，启动服务器
```js
server.listen(3000, () => {
  console.log('3000端口已启动');
})
```
- 访问监听的端口号服务器就能接收到请求

## os模块

### 功能
- 提供了一些操作系统相关的实用方法

### 加载模块
```js
const os = require('os')
```
### 常见操作
```js
os.cpus() //返回一个对象数组，包含每个逻辑cpu内核的信息
os.totalmem() //获取当前操作系统内存大小，单位为字节
```
## path模块
### 功能
- `path` 模块提供了一些工具函数，用于处理文件与目录的路径
### 引用模块
```js
const path = require('path')
```
### 常见操作
```js
path.join('foo','bar','baz/asdf') //拼接给定的路径片段，并规范化生成的路径
path.join(__dirname, './index.html') // 拼接生成index.html文件的绝对路径
path.extname('index.html') // 返回该文件的扩展名
```
- `dirname`：`dirname`是 `path` 模块中的一个全局变量，用来获取当前文件所在目录从盘符开始的全路径，也就是绝对路径。使用dirname可以规避一些错误的的发生，相对路径在某些情况下有可能会有错误
- `path.extname`：扩展名是最后一部分中的 . 到字符串节数，如果最后一部分没有或者文件名是 `.pathname` 则返回一个空字符串

## util模块
- 实用工具模块，主要用于支持 `Node.js` 内部 `API` 的需求。 大部分实用工具也可用于应用程序与模块开发者
### API
- `util.isDeepStrictEqual`：用于测试实际值(`value1`)和预期值(`value2`)之间的两个值的深度相等性。深度相等是一种通过一些规则来递归评估子对象的可枚举 `own` 属性的方法。
# 模块系统

## 三种模块

- 核心模块：核心模块就是 `fs、http` 等模块
- 用户文件模块：用户自己编写的文件也是模块
- 第三方模块
## 模块引入
- 所有的模块引入都使用 `require` 或者 `import` 方法引入，可以省略后缀名，相对路径的 `./` 或者 `../` 是不能省略的
### require
```js
const fs = require('fs') // require引入
```
### import
```js
import Header from './Header'
```
### require和import的区别

- 原生浏览器不支持 `require/exports`，可使用支持 `CommonJS` 模块规范的 `Browsersify、webpack` 等打包工具，它们会将` require/exports` 转换成能在浏览器使用的代码。`import/export` 在浏览器中无法直接使用，我们需要在引入模块的 `<script>` 元素上添加 `type="module"` 属性。
- `require/exports` 是运行时动态加载，`import/export` 是静态编译
- `require/exports` 输出的是一个**值的拷贝**，一旦输出一个值，模块内部的变化就影响不到这个值 `import/export` 模块输出的是**值的引用**，`JS` 引擎对脚本静态分析的时候，遇到模块加载命令 `import`，就会生成一个只读引用。等到脚本真正执行时，再根据这个只读引用，到被加载的那个模块里面去取值。若文件引用的模块值改变，`require` 引入的模块值不会改变，而 `import` 引入的模块值会改变。

- `import/export` 不能对引入模块重新赋值/定义

- `import/export` 只能在模块顶层使用，不能在函数、判断语句等代码块之中引用，`require/exports` 可以。

- 如果想使用 `import` 来导入模块，需要先把项目初始化为 `node` 项目,`npm init -y`，写入`"type":module`。

## 模块导出

### 模块作用域
- 在 `node` 中，每个模块都是一个作用域，模块的内部访问不到外部，外部也访问不到内部
### 导出模块
- 有时候，加载文件模块的目的不是简单地执行里面的代码，而是为了使用里面的某个成员，每个文件中都提供了一个对象 `exports`，默认是一个空对象，每个文件中的 `require` 都是导入这个 `exports` 对象，`node.js` 中导出模块的方法有两种：

- 将要导出的内容挂载到 `exports` 对象上，这样做可以给挂载的属性取任意名称
```js
const name = 'yzx'
const age = 18
export.name = name
export.age = age
```

- 使用 `module.exports`
```js
const name = 'yzx'
const age = 18
module.exports = {
    name,
    age
}
```

**注意：**

`exports` 只是对 `module.exports` 的一个引用，因此不能使用 `exports={}` 的做法来导出模块，这样会切断 `exports` 与 `module.exports` 的引用关系

### 导入模块
- `require` 导入模块都是导入了模块文件中的 `exports` 对象

```js
const person = require('./exports')
console.log(person.name) //打印挂载在exports上的name属性
console.log(person.age)  //打印挂载在exports上的age属性
```

### commonjs
- `CommonJS` 是一个项目，其目标是为 `JavaScript` 在网页浏览器之外创建模块约定。创建这个项目的主要原因是当时缺乏普遍可接受形式的 `JavaScript` 脚本模块单元，模块在与运行`JavaScript` 脚本的常规网页浏览器所提供的不同的环境下可以重复使用。

### js模块化规范
- CJS(commonjs)
- AMD
- CMD
- UMD
- ESM

# 流(stream)
#### 流是什么
- 流（stream）在 Node.js 中是处理流数据的抽象接口（abstract interface）
- 总之它是会冒数据（以 Buffer 为单位），或者能够吸收数据的东西，它的本质就是让数据流动起来。
- stream 模块提供了基础的 API 。使用这些 API 可以很容易地来构建实现流接口的对象。
#### 缓冲(Buffer)
- Writable 和 Readable 流都将数据存储在内部缓冲器(Buffer)中，这些缓冲器可以通过相应的方法来获取
	- writable._writableState.getBuffer()
	- readable._readableState.buffer
- 缓冲器的大小取决于传递给流构造函数的 highWaterMark 选项。 对于普通的流， highWaterMark 选项指定总的字节数。对于工作在对象模式的流， highWaterMark 指定了对象的总数。
- 更多详情见 http://nodejs.cn/api/stream.html#stream
# ip地址&端口号

##### ip地址

ip地址用来定位计算机

所有联网的程序都需要进行网络通信，计算机只有一个物理网卡，而在同一个局域网中，网卡的地址必须是唯一的，网卡是通过唯一的ip来进行定位的

域名--->DNS解析-->ip地址

###### 获取ip地址

node.js中提供了一个socket.remoteAddress方法来获取当前向本服务器发送请求的客户端的远程ip地址

```js
const server  = require('server')
server.on('request', (req, res) =>{
    console.log('请求我的客户端远程ip地址是', req.socket.remoteAddress)
})
```



##### 端口号

- 端口号用来定位应用程序
- 所有具有联网通信的软件都必须具有端口号
- 端口号的范围是0~65536
- 计算机中有一些默认的端口号，最好不要去使用，例如http服务的80，网站上线后浏览器默认配置80端口号，如果手动配置了别的端口号，用户输入地址时就需要手动输入端口号
- 在开发过程中使用一些简单好记没有意义的就好，例如3000, 5000
- 可以同时开启多个服务，但一定要确保不同服务占用不同的端口号，在同一台计算机中，同一个端口号同一时间只能被一个程序占用

###### 获取端口号

node.js中提供了一个socket.remotePort方法来获取当前向本服务器发送请求的客户端的端口号，socket.remoteAddress获取当前向本服务器发送请求的客户端远程ip地址，如下：

```js
const server  = require('server')
server.on('request', (req, res) =>{
    console.log('请求我的客户端的端口号是', req.socket.remotePort)
})
```

# 乱码问题

###### 原因

- 在服务器默认发送的数据是utf-8编码(国际通用编码)的内容
- 浏览器不知道接收到的数据时utf-8编码的内容
- 浏览器在不知道服务器相应内容编码的情况下会按照当前操作系统的默认编码去解析
- 中文操作系统默认是gbk

###### 解决方法

1.正确地告诉浏览器发送的内容是什么编码的

在server.on中使用res.setHeader('Content-Type', 'text/plain; charset=utf-8')给浏览器指定编码信息是utf-8

```js
server.on('request', (request, response) => {
  response.setHeader('Content-Type', 'text/plain; charset=utf-8')
  response.end('中文乱码问题')
})
```

- 在http协议中，Content-Type就是用来告诉对方我给你发送的数据内容是什么类型的
- text/plain用于指定文本类型，plain指定普通文本类型，text/html指定html文本类型，'image/jpeg'代表图片资源
- 图片不需要指定编码格式，编码说的是字符编码，一般只为字符数据指定编码

2.在html文档的head标签中可以使用

```js
<meta charset="UTF-8">
```

指定编码格式

###### 查询文档网址

http://tool.oschina.net/

# 分号问题



当采用了没有分号的代码风格时，只需要注意以下情况就不会出问题

当一行代码是以：

​	( 

​	[

​	{

​	开头的时候，在前面补上一个 ; 就可以避免一些语法解析错误

# api收录

###### replace

`replace` 可以在一段字符串中精确替换掉某一个字符串

```js
str = ste.replace('a','b')
//把str中的a替换为b
```

# 第三方工具收录

##### art-template

art-template是一个简约、超快的模板引擎。它不关心你的字符串内容，只关心自己能识别的模板标记语法

它采用作用域预声明的技术来优化模板渲染速度，从而获得接近 JavaScript 极限的运行性能，并且同时支持 NodeJS 和浏览器。

###### 特性

1. 拥有接近 JavaScript 渲染极限的的性能
2. 调试友好：语法、运行时错误日志精确到模板所在行；支持在模板文件上打断点（Webpack Loader）
3. 支持 Express、Koa、Webpack
4. 支持模板继承与子模板
5. 浏览器版本仅 6KB 大小

###### 安装

```js
npm install art-template --save
```

###### 地址

https://aui.github.io/art-template/zh-cn/docs/index.html

###### html语法

```html
<script src="node_modules/art-template/lib/template-web.js"></script> // 加载模块
  <script type="text/template" id='tpl'>
    hello{{name}}
    age:{{age}}
    爱好:{{each hobbies}} {{$value}} {{/each}}  //循环遍历hobbies
  </script>
  <script>
    let ret = template('tpl', {
      name: 'Join',
      age: 18,
      hobbies: [
        '敲代码',
        '阅读',
        '学习'
      ]
    })
    console.log(ret);
  </script>
```

###### js语法

```js
const template = require('art-template')
```
# Koa
### 中间件收录
##### koa-router
koa路由中间件，用于配置后端路由
详见：https://www.jianshu.com/p/f169c342b4d5
##### koa-views
koa模板中间件，可以用于启用`ejs`等模板引擎
详见：https://www.jianshu.com/p/33e55974a32f 

##### koa-bodyparser
这个中间件可以将post请求的参数转为json格式返回
koa接收到的post请求参数并不是json格式，我们需要将其转换为json
详见：https://www.jianshu.com/p/6f4bc9c77c9e
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
- 轻量高效
- npm是node.js开发的包管理工具
- npm是世界上最大的开源库生态系统
- 绝大多数js相关的包都放在了npm上，这样做的目的是方便开发人员下载

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

# 核心模块

###### 概念

node为js提供了很多服务器级别的api，这些api绝大多数都被包装到了一个具名的核心模块中。例如文件操作的fs核心模块，http服务构建的http模块，path路径操作模块，os操作系统模块。加载模块需要使用require这个方法。

```js
const fs = require('fs')
const http = require('http')
const path = require('path')
```



##### fs模块

###### 1.功能

fs是file-system的缩写，就是文件系统的意思，f在node中如果想要进行文件操作，就必须引入fs模块，fs模块提供了所有文件操作相关的API

###### 2.加载模块

```js
const fs = require('fs')
```

###### 3.读取文件

```js
 fs.readFile('path', (error, data) => {
     if (error) {
         console.log(error)
     }
     console.log(data) 
     //16进制数据，可使用toString()转化成字符串
 })
```

第一个参数是读取的文件路径

第二个参数是一个回调函数，它接受两个参数

- error
- data
- 文件读取成功：data是数据；error为null
- 文件读取失败：data为null；error是错误对象



文件中默认存储的是二进制数据；电脑会转成16进制，使用toString方法可以转化成字符串

###### 4.写入文件

```js
fs.writeFile('path', 'str', (error) => {
    console.log('文件写入成功')
})
```

参数1：文件路径

参数2：写入内容

参数3：回调函数，该回调函数只接受一个参数error

- 成功：文件写入成功；error为null
- 失败：文件写入失败；error是错误对象

如果当前路径下没有该文件，fs.writeFile会创建这个文件

电脑系统是不支持文件名中含有特殊符号的，比如* > <等等，如果文件名中含有这些符号就会出现写入失败的情况

##### http模块

###### 1.功能

http模块的职责就是帮我们创建编写服务器的

###### 2.加载模块

```js
const http = require('http')
```



###### 3.创建web服务器

http模块提供了http.createServer()方法来创建web服务器

```js
let server = http.createServer()
```

###### 4.提供服务

提供对数据的服务：浏览器发送请求，服务器接受请求并处理，给出反馈(发送响应)

```js
server.on('request', (request, response) => {
    conslole.log('收到客户端请求，路径是' + request.url)
    response.write('hello node.js')
    response.write('hello')
    response.end('404 Not Found')
})
```

server.on有两个参数：

- 参数一：'request'，注册request请求事件
- 参数二：回调函数，该回调函数接受两个对象参数
  - request
  - response：response对象提供了write方法给客户端发送响应数据，write可以使用多次，但最后一定要用end来结束响应，否则客户端会一直等待
  - 注意：发送响应的数据只能是二进制或者string，number,array,object都不行，此时就可以使用json中的JSON.parse()和JSON.stringfy()方法进行转换
  - JSON.parse()：字符串转化成数据类型，例如JSON.parse('[]') --> []
  - JSON.stringfy()：数据类型转化成字符串，例如JSON.stringfy([]) --> '[]'

当客户端发请求过来，就会自动触发服务器的request请求事件，然后执行回调函数

###### 5.监听端口

监听端口号，启动服务器

```js
server.listen(3000, () => {
  console.log('3000端口已启动');
})
```

访问监听的端口号服务器就能接收到请求

##### os模块

###### 1.功能

提供了一些操作系统相关的实用方法

###### 2.加载模块

```js
const os = require('os')
```

###### 3.常见操作

```js
os.cpus() //返回一个对象数组，包含每个逻辑cpu内核的信息
os.totalmem() //获取当前操作系统内存大小，单位为字节
```

##### pat模块

###### 1.功能

path模块提供了一些工具函数，用于处理文件与目录的路径

###### 2.引用模块

```js
const path = require('path')
```

###### 3.常见操作

```js
path.join('foo','bar','baz/asdf') //拼接给定的路径片段，并规范化生成的路径
path.join(__dirname, './index.html') // 拼接生成index.html文件的绝对路径
path.extname('index.html') // 返回该文件的扩展名
```

- dirname：dirname是path模块中的一个全局变量，用来获取当前文件所在目录从盘符开始的全路径，也就是绝对路径。使用dirname可以规避一些错误的的发生，相对路径在某些情况下有可能会有错误

- path.extname：扩展名是最后一部分中的 . 到字符串节数，如果最后一部分没有或者文件名是 .pathname则返回一个空字符串

# 模块系统

##### 三种模块

###### 1.核心模块

核心模块就是fs,http等模块

###### 2.用户文件模块

用户自己编写的文件也是模块

###### 3.第三方模块

##### 模块引入

所有的模块引入都使用require或者import方法引入,可以省略后缀名，相对路径的./或者../是不能省略的

###### 1.require

```js
const fs = require('fs') // require引入
```

###### 2.import

```js
import Header from './Header'
```

###### 3.require和import的区别：

- **原生浏览器不支持 require/exports**，可使用支持 CommonJS 模块规范的 Browsersify、webpack 等打包工具，它们会将 require/exports 转换成能在浏览器使用的代码。**import/export 在浏览器中无法直接使用**，我们需要在引入模块的 <script> 元素上添加type="module" 属性。

- **require/exports 是运行时动态加载，import/export 是静态编译**

- **require/exports 输出的是一个值的拷贝**，一旦输出一个值，模块内部的变化就影响不到这个值。**import/export 模块输出的是值的引用**,JS 引擎对脚本静态分析的时候，遇到模块加载命令import，就会生成一个只读引用。等到脚本真正执行时，再根据这个只读引用，到被加载的那个模块里面去取值。若文件引用的模块值改变，require 引入的模块值不会改变，而 import 引入的模块值会改变。

- **import/export 不能对引入模块重新赋值/定义**

- **import/export 只能在模块顶层使用**，不能在函数、判断语句等代码块之中引用；require/exports 可以。

- 如果想使用import来导入模块，需要先把项目初始化为node项目,`npm init -y`，写入`"type":module`。

  

##### 模块导出

###### 1.模块作用域

在node中，每个模块都是一个作用域，模块的内部访问不到外部，外部也访问不到内部

###### 2.导出模块

有时候，加载文件模块的目的不是简单地执行里面的代码，而是为了使用里面的某个成员，每个文件中都提供了一个对象:exports，默认是一个空对象，每个文件中的require都是导入这个exports对象

##### commonjs:

CommonJS 是一个项目，其目标是为 JavaScript 在网页浏览器之外创建模块约定。创建这个项目的主要原因是当时缺乏普遍可接受形式的 JavaScript 脚本模块单元，模块在与运行JavaScript 脚本的常规网页浏览器所提供的不同的环境下可以重复使用。

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
- 计算机中有一些默认的端口号，最好不要去使用，例如http服务的80
- 在开发过程中使用一些简单好记没有意义的就好，例如3000, 5000

###### 获取端口号

node.js中提供了一个socket.remotePort方法来获取当前向本服务器发送请求的客户端的端口号，socket.remoteAddress获取当前向本服务器发送请求的客户端远程ip地址，如下：

```js
const server  = require('server')
server.on('request', (req, res) =>{
    console.log('请求我的客户端的端口号是', req.socket.remotePort)
})
```


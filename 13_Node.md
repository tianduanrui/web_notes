## 1,Node.js简介

浏览器通过**js解析引擎**来解析js代码调用的**浏览器内置的Web API函数**,来操作DOM和BOM

内置API是由运行环境提供的特殊接口,只能在所属的运行环境中被调用

Node.js是一个基于Chrome V8引擎的JS后端运行环境.

Node.js中无法调用DOM和BOM或Ajax等浏览器内置API

## 2,fs文件系统模块

Node.js官方提供用来操作文件的模块.用之前需要导入fs模块

```javascript
const fs = require('fs')
```

### fs的方法和属性

#### fs.readFile()方法,用来读取指定文件中的内容:

参数1:字符串,表示i文件路径.参数2:可选参数,以什么编码格式来读取文件 3,必选参数,文件读取完成后,通过回调函数拿到读取结果

```javascript
const fs = require('fs')
fs.readFile(path,[options],callbck)
```

#### fs.writeFile()方法,用来向指定的文件中写入文件:

参数1:必选,指定一个文件路径的字符串,表示文件的存放路径.参数2:必选,表示要写入的内容  参数3:可选,以什么样的格式写入文件内容,默认utf-8.   参数4:必选,文件写入完成后的回调函数.

```javascript
const fs = require('fs')
fs.writeFile(path,data,[options],callbck)
```

注:1,该方法只能创建文件,不能创建路径

​     2,重复使用该方法写入同一个文件,新写入的内容会覆盖之前的旧内容

#### fs模块路径拼接错误问题:

fs模块操作文件时,如果提供的操作路径是以./或../开头的相对路径,容易出现路径动态拼接错误的问题

代码在运行时,会以执行node命令时所处的目录,动态拼接出操作文件的完整路径

解决这个问题使用绝对路径:js代码中\表示转义字符,所以路径中使用\\\代表\. 使用绝对路径移植性非常差,不利于维护

##### __dirname表示当前文件所处的目录:不会跟随执行node命令时所处文件的变化而变化,来解决路径动态拼接问题

```
fs.readFile(__dirname + '/files/1.txt',[options],callbck)
```

## 3,path路径模块

用来处理路径的模块,

```
const path = require('path')
```

### path模块的属性和方法:

#### path.join()方法,用来将多个路径片段拼接成一个完整的路径字符串.

...[paths] <string>路径片段的序列   路径参数中若有'../',则会抵消前面一层路径   返回值:<string>  

```
path.join('path1','path2',[...paths])
```

涉及到路径拼接操作,都是用path.join()方法

#### path.basename()方法,用来从路径字符串中,将文件名解析出来

使用path.basename()方法,可以获取路径的最后一部分,通常获取路径中的文件名

参数1:path 必选,表示一个路径的字符串   参数2:可选,表示文件扩展名 如果传入此参数,返回值中就不带扩展名了

 返回值:string类型,表示路径中的最后一部分

```
path.nasename(path,[ext])
```

#### path.extname()方法:获取路径中的扩展名部分

```
path.extname(path)
```

## 4,http模块

用来创建web服务器的模块,可以通过http.createServer()方法,将一台奠奈编程一台Web服务器,从而对外提供Web资源服务.

```javascript
const http = require('http')
```

### http基本概念回顾

服务器和普通电脑的区别,就是 服务器上安装了web服务器软件,如IIS,Apache等

在node.js中不需要第三方web服务器软件,可以通过http模块,手写一个服务器软件.

互联网中的每台web服务器,都有自己的ip地址.自己电脑服务器的ip地址为 127.0.0.1 即 localhost

ip地址和域名是一一对应的关系,存在域名服务器的电脑中.域名服务器就是提供ip地址和域名之间的转换服务的服务器

每台电脑可以运行很多web服务,每个服务对应一个唯一的端口号,客户端发送来的请求,通过端口号准确交给对应的web服务处理.,URL中的80端口可以被省略.

### 创建最基本的web服务器:

1,导入http模块

```javascript
const http = require('http')
```

2,创建web服务器实例

```javascript
const server = http.createServer()j
```

3,为服务器实例绑定request事件,监听客户端的请求

```javascript
server.on('request',(req,res)=>{
       console.log('有请求到服务器')
})
```

4,启动服务器:调用服务器实例的.listen(端口号,callback)方法,即可启动当前web服务器

```javascript
server.linsen(80,()=>{
console.log('http server running at http://127.0.0.1 ')
})
```

#### req请求对象:包含了客户端相关的数据和属性

**req.url** 是客户端请求的URL地址

**req.method** 是客户端的method请求类型

#### res响应对象:服务器相关的数据或属性

**res.end()**:向客户端发送指定的内容,并结束这次请求的处理过程

当调用res.end()方法,向客户端发送中文内容时,会出现乱码问题,需要手动设置内容的编码格式

设置响应头Content-Type的值为: text/html; charset=utf-8

```
res.setHeader('Content-Type','text/html; charset=utf-8')
```

### 根据不同的url相应不同的html内容:动态响应页面

1获取请求的url地址

2,设置默认的响应内容为404 Not Found

3,判断用户请求的是否为/或/index.html首页

4,判断用户请求的是否为/about.html关于页面

5,设置Content-Type 响应头,防止中文乱码

6,使用res.end()把内容响应给客户端

```javascript
server.on('request',(req,res)=>{
    const url = req.url                       //1获取请求的url地址
    let content = '<h1>404 Not found</h1>'    //2,设置默认的响应内容为404 Not Found
    if(url==='/'||url==='/index.html'){       //3,判断用户请求的是否为/或/index.html首页
        content = '<h1>首页</h1>' 
    }else if(url==='/about.html'){            //4,判断用户请求的是否为/about.html关于页面
        content = '<h1>关于页面</h1>'
    }
    res.setHeader('Content-Type','text/html; charset=utf-8')//5,设置Content-Type 响应头,防止中文乱码
    res.end(content)                          //6,使用res.end()把内容响应给客户端
})
```






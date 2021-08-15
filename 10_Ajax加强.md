## 一,XMLHttpRequest的基本使用

### 1,什么是XMLHttpRequest?

浏览器提供的js对象,通过它,可以请求服务器上的数据资源,jQuery中的Ajax函数,就是基于 xhr对象封装出来的.

### 2,使用xhr发起GET请求

#### 步骤:

##### 1,创建xhr对象

```javascript
   var xhr = new XMLHttpRequest()
```

##### 2,调用xhr.open()函数 :指定请求方式 与 URL地址

```javascript
   xhr.open('GET','http://www.xxx.top:3006/api/getbooks')
```

##### 3,调用xhr.send()函数: 发起Ajax请求

```javascript
   xhr.send()
```

##### 4,监听xhr.onreadystatechange事件

```javascript
    xhr.onreadystatechange = function(){
        //监听xhr对象的请求状态 readyState; 与服务器响应的状态 status
    if(xhr.readyState === 4 && xhr.status === 200){
        //打印服务器响应回来的数据
     console.log(xhr.responseText
    }
   }
```

### 3,xhr对象的readyState属性 :

用来表示当前Ajax请求所处的状态,每个Ajax请求必然处于下面状态中的一个.

|  值  |       状态       |                      描述                       |
| :--: | :--------------: | :---------------------------------------------: |
|  0   |      UNSENT      |  XMLHttpRequest对象已被创建,但未调用open()方法  |
|  1   |      OPENED      |              open()方法已经被调用               |
|  2   | HEADERS_RECEIVED |     send()方法已经被调用,响应头也已经被接受     |
|  3   |     LOADING      | 数据接收中,此时的response属性中已经包含部分数据 |
|  4   |       DONE       | Ajax请求完成,这意味着数据传输已经彻底完成或失败 |

### 4.使用xhr发起带参数的GET请求

在调用xhr.open期间,为URL地址指定参数即可.

```javascript
   xhr.open('GET','http://www.xxx.top:3006/api/getbooks?id=1&password=123')
```

### 5,查询字符串:

   在URL地址后面拼接的参数,用于向服务器发送信息的字符串叫做查询字符串

   格式:在URL末尾 ? 加上 参数=值,多个参数用&分隔

##### GET请求携带的参数的本质:

jquery中的get()函数或ajax()函数,需要携带参数时,本质上都是将参数直接以查询字符串的形式,追加到URL地址后面,发送给服务器的.

### 6,URL编码及解码

URL地址中,只允许出现英文相关的字母,标点符号,数字,不允许出现中文字符

若需要包含中文,则必须对中文字符进行编码(转义)

编码原则:使用英文字符表示非英文字符

##### 如何对URL进行编码与解码:

encodeURL() 编码的函数

decodeURL()  解码的函数

浏览器会自动对URL地址及进行编码操作

### 7,使用xhr发起POST请求

步骤:

1,创建xhr对象

```javascript
var xhr = new XMLHttpRequest()
```

2,调用xhr.open()函数:指定请求的方式和请求的URL地址

```javascript
xhr.open('POST','http://www.xxx.top:3006/api/add/book')
```

3,设置Content-Type属性(固定写法)

```javascript
xhr.setReuestHeader('Content-Type','application/x-www-form-urlencoded')
```

4,调用xhr.send()函数 同时指定要发送的数据   将数据以查询字符串的形式,提交给服务器.

```
xhr.send('bookname=水浒传&author=施耐庵&publisher=天津图书出版社')
```

5,监听xhr.onreadychange事件

```javascript
xhr.onreadystatechange = function(){
        //监听xhr对象的请求状态 readyState; 与服务器响应的状态 status
    if(xhr.readyState === 4 && xhr.status === 200){
        //打印服务器响应回来的数据
     console.log(xhr.responseText)
    }
   }
```

## 二,数据交换格式

数据交换格式:就是服务器端和客户端之间的数据传输和交换的格式

主要要是XML和JSON. 其中XML用的非常少,多数用的JSON

### 1.XML: 可扩展标记语言,和HTML类似,但是两者之间没有关系

```XML
<note>
 <to>ls</to>
 <from>zs</from>
 <heading>通知</heading>
 <body>晚上开会</body>
</note>
```

XML被设计用来传输和存储数据.是数据的载体.

##### XML缺点:

1,XML格式臃肿,和数据无关的代码多,体积大,传输效率低

2,在js中解析XML比较麻烦

### 2.JOSN: JS对象表示法

JSON就是js对象和数组的字符串表示法,本质是用字符串表示js对象数据或数组结构.

作用:JSON是一种轻量级的文本数据交换格式,专门用于在计算机和网络之间存储和传输数据,但是JSON比XML更小,更快,更易解析

#### 2.1 JSON的两种结构

JSON中包含**对象**和**数组**两种结构,这两种结构相互嵌套,可以表示各种复杂的数据结构

**1,对象结构:**

表示为{}括起来的内容.数据结构为{key : value}的键值对结构.

key必须是使用英文的双引号包裹的字符串,value的数据类型可以使**数字,字符串,布尔值,null,数组,对象**六种类型.

**2,数组结构:**

表示为[]括起来的结构,数据结构为    ["java","JavaScript",30,true...]

数组种数据的类型可以是**数字,字符串,布尔值,null,数组,对象**6种类型.

#### 2.2 JSON语法注意事项:

1,属性名必须使用双引号包裹

2,字符串类型的值必须使用双引号包裹

3,JSON中不允许使用单引号表示字符串

4,JSON中不能写注释

5,JSON的最外层必须是对象或数组格式

6,不能使用undefined或函数作为JSON的值.

#### 2.3 JSON和js对象的关系

JSON是js对象的字符串表示法,它使用文本表示一个js对象的信息,本质是一个字符串

#### 2.4 JSON和JS对象的互转

从JSON转化为JS对象: **JSON.parse('JSON对象').**

从JS对象转化为JSON字符串: **JSON.stringify(js对象)**

#### 2.5序列化和反序列化

把数据对象转换为字符串的过程,叫做序列化.如 JSON.stringify()函数,叫做 JSON序列化

把字符串转化为数据对象的过程,叫做反序列化,如 JSON.parse()函数,叫做JSON反序列化

## 三,封装自己的Ajax函数

#### 1,定义options参数选项

tdr()自定义的Ajax函数,接受一个配置对象作为参数,配置对象中可以配置如下属性:

method  请求的类型

url            请求的URL地址

data          请求携带的数据

success    请求成功之后的回调函数

#### 2,处理data参数

需要把data对象,转化为查询字符串的格式,从而提交给服务器,提前定义**resolveData函数**:

```javascript
 //处理data参数  data是需要发送到服务器的数据
function resolveData(data){
  var arr = []
  for(let k in data){
    arr.push(k+'='+data[k])
  }
 //返回拼接好的查询字符串
  return arr.join('&')
}
```

#### 3.定义tdr函数

在tdr()函数中,需要创建xhr对象,并监听onreadystatechange事件

```javascript
function tdr(options){
    var xhr = new XMLHttpRequest()
    //拼接字符串
    var qs = resloveData(options.data)
    //监听请求状态改变的事件
    xhr.onreadystatechange = function(){
        if(xhr.readystate === 4 && xhr.status === 200){
            var result = JSON.parse(xhr.responseText)
            options.success(result)
        }
    }
}

```

#### 4,判断请求的类型

不同的请求类型,对应xhr对象的不同操作,因此需要对请求类型进行if...else...的判断

```javascript
if(options.method.toUpperCase()==='GET'){
    xhr.open(optins.method,options.url+'?'+qs)
    xhr.send()
}else if(options.method.toUpperCase()==='POST'){
    xhr.open(optins.method,options.url)
    xhr.setRequestHeader('Content-Type','application/x-www-form-urlencoded')
    xhr.send(qs)
}
```

#### 5封装好的函数

```javascript
function tdr(options){
    var xhr = new XMLHttpRequest()
    //拼接字符串
    var qs = resloveData(options.data)
    //判断请求类型                     
    if(options.method.toUpperCase()==='GET'){
    xhr.open(optins.method,options.url+'?'+qs)
    xhr.send()
    }else if(options.method.toUpperCase()==='POST'){
    xhr.open(optins.method,options.url)
    xhr.setRequestHeader('Content-Type','application/x-www-form-urlencoded')
    xhr.send(qs)
}                     
    //监听请求状态改变的事件
    xhr.onreadystatechange = function(){
        if(xhr.readystate === 4 && xhr.status === 200){
            var result = JSON.parse(xhr.responseText)
            options.success(result)
        }
    }
}
```

## 四,XMLHttpRequest Level2的新特性

### 1,对比

#### 旧版XMLHttpRequest的缺点

1,只支持文本数据的传输,无法用来读取和上传文件

2,传送和接收数据时,没有进度信息,只能提示有没有完成

#### XMLHttpRequest Level2的新特性

1,可以设置HTTP请求的时限

2,可以使用FormData对象管理表单数据

3,可以上传文件

4,可以获得数据传输的进度信息

### 2,设置HTTP请求时限 : timeout属性

请求的最长时间,过了时限,就自动停止HTTP请求

xhr.timeout = 3000   //单位是毫秒

请求停止后的回调函数

xhr.ontimeout = function(event){

  alert('请求超时')

}

### 3,使用FormData对象管理表单数据

Ajax操作往往用来提交表单数据.HTML5新增了一个FormData对象,可以用来模拟表单操作

```javascript
//新建一个FormData对象
var fd =  new FormData()
//为FormData对象添加表单项
fd.append('uname','zs')
fd.append('upwd','123')
//创建xhr对象
var xhr = new XMLHttpRequest()
//指定请求类型和URL地址
xhr.open('POST','http://www.xxx.top:3006/api/add/book')
//直接提交FormData对象,这和提交网页表单的效果一样
xhr.send(fd)
```

#### FormData对象也可以用来获取网页表单的值

```javascript
//获取表单元素
var form = document.querySelector('#form1')
//监听表单元素的submit事件
form.addEventListener('submit',function(e){
    e.preventDefault()
    //根据form表单创建FormData对象,会自动将表单内容 数据填充到FormData对象中
    var fd = new FormData(form)
    var xhr = new XMLHttpRequest()
    xhr.open('POST','http://www.xxx.top:3006/api/add/book')
    xhr.send(fd)
    xhr.onreadystatechange = function(){}
})
```

### 4,上传文件

步骤:

1,定义UI结构

```html
//文件选择框
<input type="file" id="file1"/>
//上传文件按钮
<button id="btnUpload">上传文件</button>
//img标签,显示上传成功后的图片
<img src="" alt="" id="img">
```

2,验证是否选择了文件

```javascript
//获取上传文件的按钮
var btnUpload = document.querySelector('#btnUpload')
//为按钮添加点击事件监听
btnUpload.addEventListener('click',function(){
    //获取到选择的文件列表
    var files = document.querySelector('#file1').files
    if(files,length<=0){
        return alert('请选择想要上传的文件')
    }   
    //后续业务逻辑
})

```

3,向FormData中追加文件

```javascript
var fd = new FormData
//向FormData中追加文件
fd.append('avatar',files[0])
```

4,使用xhr发起上传文件的请求

```javascript
    var xhr = new XMLHttpRequest()
    xhr.open('POST','http://www.xxx.top:3006/api/add/book')
    xhr.send(fd)
```

5监听on事件

```javascript
xhr.onreadystatechange = function(){
        if(xhr.readystate === 4 && xhr.status === 200){
            var result = JSON.parse(xhr.responseText)
            if(result.status===200){
                document.querySelector('#img').src = 'http://www.xxx:3006' + result.url
            }else{
                console.log(result.message)
            }
        }
    }
```

**上传文件完整步骤:**

```html

<input type="file" id="file1"/>

<button id="btnUpload">上传文件</button>

<img src="" alt="" id="img">
```



```javascript
//获取上传文件的按钮
var btnUpload = document.querySelector('#btnUpload')
//为按钮添加点击事件监听
    btnUpload.addEventListener('click',function(){
    //获取到选择的文件列表
    var files = document.querySelector('#file1').files
    if(files,length<=0){
        return alert('请选择想要上传的文件')
    }   
    var fd = new FormData
    //向FormData中追加文件
    fd.append('avatar',files[0])

    var xhr = new XMLHttpRequest()
    xhr.open('POST','http://www.xxx.top:3006/api/add/book')
    xhr.send(fd)

    xhr.onreadystatechange = function(){
        if(xhr.readystate === 4 && xhr.status === 200){
            var result = JSON.parse(xhr.responseText)
            if(result.status===200){
                document.querySelector('#img').src = 'http://www.xxx:3006' + result.url
            }else{
                console.log('图片上传失败' + result.message)
            }
        }
    }
})
```

### 5,显示文件上传进度

可以通过监听xhr.upload.onprogress事件,来获取到文件的上传进度

```javascript
var xhr = new XMLHttpRequest()
//监听 xhr.load的onprogress事件
xhr,onload.onprogress = function(e){
    //e.lengthComputable 是一个布尔值,表示当前上传的资源是否具有可计算的长度
    if(e.lengthComputable){
        //e.loaded 已传输的字节  e.total  要传输的总字节
        var percentComplete = Math.ceil((e.loaded/e.total)*100)
    }
}
```

监听上传完成的事件

```javascript
xhr.upload.onload = function(){
    
}
```

## 五,jQuery高级用法

#### 使用jQuery上传文件过程:

```javascript
//为按钮添加点击事件监听
$(btnUpload).on('click',function(){
    //将获取的jQuery对象转换为DOM对象,并获取选中的文件列表
    var files = $('#file1')[0].files
    if(files,length<=0){
        return alert('请选择想要上传的文件')
    }   
    
})
    var fd = new FormData
    //向FormData中追加文件
    fd.append('avatar',files[0])
    $.ajax({
        method:'POST',
        url:'http://www.xxx:3006/api/upload',
        data:fd,
        //不修改Content-Type 属性,使用FormData默认的Content-Type值
        contentType:false,
        //不对FormData中的数据进行url编码,而是将FormData数据鸳鸯发送到服务器
        progressData:false,
        success:function(res){
            console.log(res)
        }        
    })
```

#### 用ajax实现loading效果

1, ajaxStart(callback) : Ajax请求开始时,执行AjaxStart函数,可以在ajaxStart的callback中显示loading效果

```
$(document).ajaxStart(function(){
    $('#loading').show()
})
```

注意:$(document).ajaxStart()函数会监听当前文档内所有的Ajax请求.

2,ajaxStop(callback):Ajax请求结束时,执行ajaxStop函数,可以在ajaxStop的callback

```
$(document).ajaxStop(function(){
    $('#loading').hide()
})
```

## 六,axios

### 1,介绍

axios是专注于网络数据请求的库

相比于原生的xhr对象,axios简单易用

相比于jQuery,axios更加轻量化,只专注于网络数据请求

### 2,axios发起GET请求

axios.get('url',{params:{参数}}).then(callback)

```javascript
//请求的URL地址
var url - 'http://www.xxx:3006/api/get'
//请求的参数对象
var paramsObj = {name : 'zs', age:20}
//调用axios.get()发起GET请求
axios.get(url,{params:paramsObj}).then(function(res){
    //res是axios为我们包装的返回对象,res中的data属性才是服务器的返回值
    var result = res.data
    console.log(result)
})
```

### 3,axios发起POST请求

axios.post('url',{参数}).then(callback)

```javascript
//请求的URL地址
var url - 'http://www.xxx:3006/api/get'
//要提交到服务器的数据
var dataObj = {name : 'zs', age:20}
//调用axios.post()发起POST请求
axios.post(url,dataObj).then(function(res){
    //res是axios为我们包装的返回对象,res中的data属性才是服务器的返回数据
    var result = res.data
    console.log(result)
})
```

### 4,直接使用axios发起请求

axios也提供了类似jQery中$.ajax()的函数

```javascript
axios({
    method:'请求类型'
    url:'请求的URL地址'
    data:{/* POST数据*/}
    params:{/* GET参数*/}
}).then(callback)
```


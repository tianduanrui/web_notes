xml:可扩展标记语言,被设计进行数据的传输和保存.已被josn代替.

# Ajax : 

## 1,介绍:

异步JavaScript和XML

在网页中利用XMLHttpRequest对象和服务器及逆行数据交互的方式,就是Ajax.

实现网页和服务器之间的数据交互.

经典使用场景: 用户名检测,用户名是否被注册.

​           输入搜索关键字时,动态加载提示框

​           数据分页.根据页码值动态刷新表格数据

​           数据的增删改查

### 优缺点:

#### 优点:

 1可以无需刷新进行数据通讯

 2根据事件可以进行页面的更新

#### 缺点:

1:没有浏览历史,不能回退

2,存在跨域问题(同源)

3,SEO不友好 搜索引擎优化

## 2,jQuery中的Ajax:

#### 2-1,$.get(); 用来发起get请求,将服务器上的资源请求到客户端

​       $.get (url.[data],[callback]);

​         url  要请求的资源地址,String类型

​         data 要求资源期间要携带的参数 Object类型

​         callback 请求成功时的回调函数 function类型

#### 2-2,$.post(); 用来发起post请求,从而向服务器提交数据

​     $.post (url.[data],[callback]);

​     url  要请求的资源地址,String类型

​     data  要提交的数据 Object类型

​     callback 数据提交成功时的回调函数 function类型

####  2-3,$.ajax();

​    $.ajax( {

​     type:'', //请求的方式 GET或POST

​      url:''  //请求的URL地址

​      data:{}   //请求要携带的数据

​      success: function(res){}  //请求成功后的回调函数

})

#### 接口概念:

使用AAjax请求数据时,被请求的URL地址,就叫做数据接口,每个接口必须有请求方式.

## 3,form表单:

表单在网页中主要负责数据采集功能   <form>

### 3-1组成部分:

表单标签 <form>

表单域: 包含文本框,密码框,隐藏域,复选框,下拉框,文件上传框等.

表单按钮:

### 3-2form标签属性:

用来规定如何让把采集到的数据发送到服务器

#### 1,action:向何处发送表单数据

属性值是后端提供的一个URL地址,来接受表单提交的数据

form表单若未指定action属性值的情况下,action的默认值为当前页面的URL地址.

提交表单后,页面会立即跳转到action属性指定的URL地址

#### 2,target:规定在何处打开action URL

可选值有五个:

_blank  在新窗口中打开

_self     默认,在相同的框架中打开

_parent  在父框架中打开 很少用

_top     在整个窗口中打开   很少用

framename  在指定的框架中打开  很少用

####  3,method:以何种方式把表单数据提交到 action URL

可选值: get (默认) 和 post

get:以URL地址的形式来提交数据  数据会在地址栏看到

post:数据以 form data 形式提交,数据在地址栏看不到.

get方式适合用来提交少量的,简单的数据 很少用到get.

post方式适合用来提交大量的,复杂的,或包含文件上传的数据

#### 4,enctype:规定在发送数据之前如何让随数据进行编码

可选值:

application/x-www-form-urlencoded    默认值,在发送前编码所有字符

multipar/form-data     不对字符编码.在使用包含文件上传控件的表单时,必须使用该值

text/plain     空格转换为 "+" 加号,但不对特殊字符编码

### 3-3表单的同步提交及缺点:

同步提交:点击submit按钮,触发表单提交的操作,从而使页面跳转到 action URL的行为,叫做表单的同步提交

#### 缺点:

1,提交之后,整个页面会发生跳转,到 action URL所指向的地址,用户体验差

2,同步提交后,页面之前的状态和数据会丢失

#### 如何解决?

表单只负责采集数据, Ajax负责将数据提交到服务器

## 4,通过Ajax来提交表单数据

### 4-1,监听表单提交事件:

`$(#form).submit(function(){`

`})`

`$(#form).on('submit', funtion(){`

`})`

### 4-2,阻止表单默认提交行为:

调用事件的 event.preventDefault()函数,来阻止表单的提交和页面的跳转

```javascript
$(#form).submit(function(e){`

   `e.preventDefault()`

`})`

`$(#form).on('submit', funtion(e){`

   `e.preventDefault()`

`})
```



### 4-3,快速获取表单中的数据:

#### 1,serialize()函数:可以一次性获取到表单中的所有数据

$(slector).serialize()

使用此函数快速获得表单数据时**,每个表单元素必须添加name属性**

#### 2,快速重置表单:清空表单中的内容

$(选择器)[0].reset()

## 5,模板引擎:

为了解决字符串拼接遇到的问题.

模板引擎可以根据程序员指定的**模板结构 和 数据**,自动生成一个完整的HTML页面.

### 5-1 优点

1,减少了字符串的拼接操作

2,使代码结构更加清晰

3,使代码更易于阅读和维护

### 5-2: art-template

#### 5-2-1:步骤

1.导入art-tempalte,在window全局多了一个函数,叫做template('模板id',需要渲染的数据对象)

2,定义数据:

3,定义模板:  模板的HTML结构,必须定义到script标签中 ,script标签的type类型需要改成  text/html  模板id定义到script标签上.

​                     {{data.属性名}}作为占位符,来表示要将数据渲染到此处.

4,调用art-template函数:  var htmlstr = art-template('模板id',data); 返回一个字符串

5,渲染HTML函数  $(选择器).html('htmlstr')

#### 5-2-2:art-template标准语法

{{}}语法格式,在{{}}内可以进行变量输出,或循环数组等操作.这种语法被称为标准语法

##### 1,标准语法-输出:

{{输出的值}}   可以进行变量的输出,对象属性的输出,三元表达式的输出,逻辑或输出,加减乘除表达式的输出

##### 2,标准语法-原文输出:

**{{@ value}}**;   若要输出的value值中,包含了HTML标签结构,则需要使用原文输出语法,才能保证HTML标签的正常渲染

##### 3,标准语法-条件输出:

在{{}}中使用if...elseif.../if的方式进行按需输出

**{{if value}}** 按需输出的内容**{{/if}}**

**{{if v1}}**按需输出的内容**{{else if v2}}**按需输出的内容 **{{/if}}**

##### 4,标准语法-循环输出:

在{{}}}内,通过each语法循环数组,当前循环的索引使用**$index**及进行访问,当前的循环项使用**$value**访问.

{{each arr}}

​        {{$index}}{{$value}}

{{/each}}

##### 5,标准语法-过滤器:本质是一个function处理函数

{{value | filterName}}   过滤器语法类似管道操作符,他的上一个输出作为下一个输入.

**定义过滤器语法:**

 template.defaults.imports.filterName = function(value){ /* return 处理的结果*/  }

### 5-3模板引擎的实现原理:

#### 5-3-1:正则与字符串操作

**1,exec()**函数用于 检索字符串 中的正则表达式的匹配.字符串中有匹配的值,返回该匹配值,否则返回null.

**2,分组**:正则表达式中()包起来的内容表示一个分组,可以通过分组来提取自己想要的内容

**3,replace()**函数:用于字符串中用一些字符替换另一些字符   字符串.replace('str1','str2');

**4,多次replace():**

**5,使用while()循环进行字符串的repalace()**

 

```javascript
     var pattResult = null
     while(pattResult = pattern.exec(str){
           str = tsr.replace(pattResult[0],pattResult[1])
     }
```

**6,replace替换为真值**

```javascript
     var pattResult = null
     while(pattResult = pattern.exec(str){
           str = tsr.replace(pattResult[0],data[pattResult[1]])
     }
```

#### 5-3-2:实现简易的模板引擎

##### 步骤

1,定义模板结构

2,预调用模板引擎

3,封装template函数

```javascript
 function template(id,data){
     var str = document.getElementById(id).innerHTML
     var pattern = /{{\s*([a-zA-Z]+)\s*}}/
     var pattResult = null
     while(pattResult = pattern.exec(str){
           str = tsr.replace(pattResult[0],data[pattResult[1]])
           }
     return str;
 }
```

4,导入并使用自定义的模板引擎


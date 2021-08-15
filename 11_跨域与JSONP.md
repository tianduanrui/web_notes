## 1,同源策略和跨域

**同源:**如果两个页面的协议,域名和端口号都相同,则两个页面具有相同的源

**同源策略:**是浏览器提供的一个安全功能.限制了从同一个源加载的文档或脚本如何与来自另一个源的资源进行交互,这是一个用于隔离潜在恶意文件的重要安全机制.

简单讲就是:A网站的 Javascript ,**不允许和非同源的网站C之间进行资源的交互**

1,无法读取非同源网站的Cookie,LocalStorage 和 IndexedDB

2,无法接触非同源网站的DOM对象

3,无法向非同源地址发送Ajax请求

**跨域:**两个URL中的协议,域名,端口号中有任何一项不一致,就是跨域.  不是同源既是跨域

**浏览器对跨域请求的拦截:**浏览器允许发起跨域请求,也能接收到跨域响应的数据,但是跨域请求响应回来的数据,会被浏览器的同源策略拦截,无法被页面获取到.

**如何让实现跨域数据请求:**

主要两种解决方案: JSONP和CORS.**

**JSONP:** 出现的早,兼容性好.只支持GET请求,不支持POST请求  是一种临时解决方法.

**CORS:** W3C标准,属于跨域Ajax请求的根本解决方案,支持GET和POST请求,兼容性较差.

## 2,JSONP: JSON with Padding

JSONP是JSON的一种"使用模式",可以用于解决主流浏览器的跨域数据访问的问题

### JSONP的实现原理:

浏览器的同源策略限制,使网页中无法通过Ajax请求非同源的接口数据.

但是,<script>标签不受浏览器同源策略影响,可以通过src属性,请求非同源的js脚本

因此,JSONP的实行原理就是: 通过<script>标签的src属性,请求跨域的数据接口,并通过函数调用的形式,接受跨域接口响应回来的数据.

```html
<script src="./js/getdata.js?callback=success"></script>
```

### 实现JSONP

定义一个success回调函数

```html
<script>
function success(data){
    console.log('获取到了data数据')
    console.log(data)
}
</script>
```

通过<script>标签,请求接口数据

```html
<script src="http://ajax.frontend.net:3006/api/jsonp?callback=success&name=zs&age=20"></script>
```

JSONP缺点:

只支持GET请求,不支持POST请求

注意:JSONP和Ajax之间没有任何关系,不能把JSONP请求数据的方式叫做Ajax,因为JSONP没有用到xhr对象.

### jQuery中的JSONP:

jQuery提供的$.ajax()函数,除了可以发起真正的Ajax数据请求之外,还能发起JSONP数据请求

```javascript
$.ajax({
    url:'http://ajax.frontend.net:3006/api/jsonp?callback=success&name=zs&age=20'
    //若要使用$.ajax()发起JSONP请求,必须指定dataType为jsonp
    dataType:'jsonp'
    success:function(res){
    console.log(res)
    } 
})
```

默认情况下,使用jQuery发起JSONP请求,会自动携带一个callback=jQueryxxx的参数,jQueryxxx是随即生成的一个回调函数名称. 

#### 自定义参数及回调函数名称:

```javascript
$.ajax({
    url:'http://ajax.frontend.net:3006/api/jsonp?callback=success&name=zs&age=20'
    //若要使用$.ajax()发起JSONP请求,必须指定dataType为jsonp
    dataType:'jsonp'
    //发送到服务器端的参数名称,默认值为callback
    jsonp:'callback'
    //自定义的回调函数名称,默认值为jQueryxxx格式
    jsonpCallback: 'abc'
    success:function(res){
    console.log(res)
    } 
})
```

#### jQuery中的JSONP实现过程:

jQuery中的JSONP,也是通过<script>标签的src属性实现跨域数据访问的,只不过,jQuery采用的是动态创建和移除<script>标签的方式,来发起JSONP数据请求的.

在发起JSONP请求时,动态向<header>中append一个<script>标签

在JSONP请求成功以后,动态从<header>中移除刚才append进去的<script>标签

## 3,防抖和节流

### 1,防抖: 

防抖策略(debounce):当事件被触发时,延迟n秒后在执行回调,如果这n秒内事件又被触发,则重新计时

#### 应用场景:输入框的防抖

用户在输入框连续输入一串字符时,可以通过防抖策略,在输入完成之后,才执行查询的请求,这样可以有效减少请求次数,节约请求资源

#### 实现输入框的防抖:

```javascript
//定义防抖动的timer
var timer = null
//定义防抖动函数
function debounceSearch(keywords){
    timer = settimeout(function(){
        //发起JSONP请求
        getSuggestList(keywords)
     },500)
  }
     $('#ipt').on('keyup',function(){
         clearTimeout(timer)
         debouceSearch(keyword)
     })
```

#### 缓存搜索的建议记录:

##### 1,定义缓存对象

```
var cacheObj = {}
```

##### 2,将搜索结果保存到缓存对象中

```javascript
//渲染建议列表
renderSuggesList(res){

 //将搜索的结果,添加到缓存对象中
  var k = $('#ipt').val().trim()
  cacheObj[k] = res
}
```

##### 3,优先从缓存中获取搜索建议

```javascript
//监听文本框的keyup事件
$('#ipt').on('keyup',function(){
  //优先从缓存中获取搜索建议
  if(cacheObj[keywords]){
  return renderSuggestList(cacheObj[keywords])
  }
  debounceSearch(keywords)
})
```

### 2,节流:

节流策略:减少一段时间内事件的触发频率.事件被触发时,一段时间内再次触发无效,等待时间过去才会再次触发

#### 节流应用场景

1,鼠标连续不断的触发某事件,只在单位时间内触发一次

2,懒加载时要监听计算滚动条的位置,但不必每次滑动都触发,可以降低i计算的频率,而不必去浪费CPU资源.

#### 节流阀:

节流阀为空,表示可以执行下一次操作,不为空,表示不能执行下一次操作.

当前操作执行完,必须将节流阀重置为空,表示可以执行下次操作了

每次执行操作前,必须先判断节流阀是否为空.

```javascript
$(fuction{
  var angel = $('#angel')
  var timer = null   //预定义一个timer节流阀
  $(document).on('mousemove',function(e){   //监听时间触发
  if(timer){return}  //判断节流阀是否为空,如果不为空,则证明距离上次执行间隔不足
  timer = setTimeout(fuction(){
  //业务代码
  timer = null  //执行完事件之hi偶,清空节流阀,方便下次开启延时器
  }, 16)
 })
})
```

### 3,节流和防抖区别

防抖:若事件被频繁触发,防抖能保证只有最后一次触发生效,前面N多次的触发都会被忽略

节流:若事件被频繁触发,节流能够减少事件触发的频率,因此节流是有选择性的执行一部分事务
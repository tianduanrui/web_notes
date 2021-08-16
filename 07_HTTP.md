# HTTP:

#### 请求报文:

行 POST / s?ie=utf-8 HTTP/1.1

头  Host: 

​     Cookie: name=guigu

​     Content-type: application/

​     User-Agent: chrome 83

空行

体 username=admin&password=admin

GET请求请求体可以为空,POST请求请求体可以不为空.

#### 响应报文:

行  HTTP1.1 200 OK  协议版本 响应状态码 响应字符串

头  Content-Type: text/

​      Content-length: 2048

空行

体  <html>

​     <head>

​    </head>

​    </html>

#### URL:

统一资源定位符

1,客户端与服务器之间的通信协议

2,存有资源的服务器名称

3,资源在服务器上具体的存放位置



#### 客户端与服务器中间的通信过程:

请求-处理-响应

 

要在网页中请求服务器上的数据资源,需要用到XMLHttpRequest对象.简称xhr

时浏览器提供的js成员,通过他,可以请求服务器上的数据资源.

cost xhr = new XMLHttpRequest;

 

#### GET和POST

get请求通常用于获取服务器资源

post请求通常用于向服务器提交数据. 如登录时向服务器提交登录信息

 
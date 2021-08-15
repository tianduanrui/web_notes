$(function(){

  此处是页面DOM加载完成的入口

})

等着DOM结构渲染完毕即可执行内部代码,不必等到所有外部资源加载完成

相当于原生js中的DOMContentLoaded

 

$是jQuery的别称,也是jQuery的顶级对象.相当于原生js中的window,将元素通

过$包装成jQuery对象.

jQuery对象:用jQUery方法获取过来的对象 本质:通过$把DOM元素进行了包装.

$('div')

jQuery对象的本质:利用$对DOM对象包装后产生的对象(伪数组形式存储)

jQuery对象只能使用jQuery方法.DOM对象只能使用原生js属性方法

 

DOM对象转换为jQuery对象:$(DOM对象)

jQuery对象转换为DOM对象:$('div')[index]   $('div').get(index) 

## jQuery常用API:

### 一,jQuery选择器:

$("选择器"):选择器伪css选择器. 

子代选择器 使用> ,获取亲儿子层级的元素

后代选择器 使用空格,代表后代选择器

jQuery设置样式:$('div').css('属性','值')

#### 隐式迭代:

遍历内部DOM元素(伪数组形式存储)的过程就叫做隐式迭代.

给匹配到的所有元素进行循环遍历,执行相应的方法.

得到当前元素索引号:$(this).index();

#### jQuery筛选选择器:

:first   $('li:first') 获取第一个li元素

:last    $('li:last')  获取最后一个li元素

:eq(index) $("li:eq(2)") 获取到的li元素中,选择索引值为2的元素 索引号从0开始

:odd   $("li:odd")  获取到的li元素中,选择索引号为奇数的元素

:even  $("li:even") 获取到的li元素中,选择索引号为偶数的元素

#### jQuery筛选方法:

$("li").parent(); 查找父级

$("ul").children("li"); 相当于$("ul>li"),子代选择器

$("ul").find("li");相当于$("ul li") 后代选择器

$(".first").siblings("li"); 查找兄弟节点,不包括自己本身

$(".first").nextAll(); 查找当前元素之后的所有同辈元素

$(".last").prevAll(); 查找当前元素之前的所有同辈元素

$('div').hasClass("protected") 检查当前的元素是否含有某个特定的类 返回布尔值

$('li').eq(2);相当于$("li:eq(2)")

jQuery的排他思想: 主要利用了隐式迭代和选择兄弟节点的方法

$(this).css();

$(this).siblings("").css();

### 二,jQuery样式操作:

可以使用CSS方法来修改简单元素样式,也可以操作类,修改多个样式.

1,参数只写属性名,则是返回属性值.

2,参数是属性名,属性值,逗号分隔,时设置一组样式.属性必须加引号,值如果是数字可以不用加单位和引号.

3,参数可以使对象,方便设置多组样式,属性名和属性值用:隔开,属性可以不用加引号.

设置类样式方法:

1,添加类:$('div').addClass("类名");

2,删除类:removeClass("类名")

3,切换类:toggleClass("") 有就删除,没有就添加

 

原生js中的className会覆盖元素原先里面的类名.

jQuery里面类操作相对于追加类名,不会影响原先的类名.

 

### 三,jQuery效果:

#### 显示隐藏:

show([speed],[easing],[fn]) 参数可以省略

hide([speed],[easing],[fn])

toggle([speed],[easing],[fn])

#### 滑动:

slideDown([speed],[easing],[fn])

slideUp([speed],[easing],[fn])

SlideToggle([speed],[easing],[fn])

#### 事件切换:

hover([over],out) over相当于mouseenter out相当于mouseleave

当参数只写一个函数时,鼠标经过和离开都会触发

动画队列:动画多次触发时,会产生排队

动画停止:stop() 此方法必须写在动画的前面.

#### 淡入淡出:

fadeIn()

fadeOut()

fadeTo([speed],opacity,[easing],[fn]) 修改透明度

fadeToggle()

#### 自定义动画:

animate(params,[speed],[easing],[fn])

params:想要更改的样式属性,以对象的形式传递,必须写

### 四,jQuery属性操作

#### 1,设置或获取元素固有属性值 

元素.prop("属性名");

元素.prop("属性名","属性值");

2,设置或获取元素自定义属性

元素.attr("属性名"); 类似原生中的getAttribute();

元素.attr("属性名","属性值"); 类似原生中的setAttribute();

该方法也可以获取H5自定义属性.

3,数据缓存data(): 相当于把元素看作一个变量

data()方法可以在指定的元素上存取数据,并不会修改DOM元素结构,一旦页面刷新,之前存放的数据都会被移除.

### 五,jQuery内容文本值

#### 1普通内容html() 相当于原生中的innerHTML

html() 获取元素的内容

html("内容") 设置元素的内容

#### 2,普通元素文本内容 text() 相当于原生的innerText

text() 获取文本内容

text("内容") 设置文本内容

#### 3,获取设置表单值 val() 相当于原生中的value

val()

val("内容")

获取指定祖先元素:

parents("选择器")

数字计算结果保留小数位数

toFixed(位数)

### 六,jQuery元素操作 :遍历,创建,添加,删除

#### 1,遍历元素

隐式迭代时对同一种元素做相同操作,若想对同一元素做不同操作,需要遍历

$("div").each( function(index, domEle) {...}) 

index是每个元素的索引号,demEle是每个DOM对象,不是jQuery对象.若想要使用jQuery方法需要$(domEle)

$.each()方法遍历,主要用与遍历数据,处理数据.

$.each($("div"),function(i,ele){...})

#### 2,创建元素

$("<li></li>"); 将标签名用$括起来.

添加元素: 内部添加:$("ul").append() 放到内容的最后面,相当于appendchild

​                $("ul").prepend() 内部添加到最前面

​        外部添加:$("").after() 外部添加到后面

​                $("").before() 外部添加到前面

删除元素: $().remove(); 删除匹配的元素本身

​        $().empty() 删除匹配的元素集合中的所有子节点

​        $().html("") 清空匹配的元素内容

### jQuery事件:

#### 事件注册:

元素.事件(function(){...}) 如 $("div").click(function(){...})

#### 事件处理on绑定事件:

元素.on(events,[selector],fn) evnets:一个或多个用空格分隔的事件类型  selector:元素的子元素选择器 fn:回调函数

on可以事件委派操作

on()可以给动态生成的元素绑定事件.

#### 事件解绑: off()可以移除通过on()方法添加的事件

元素.off():解除元素上的所有事件

元素.off("事件")解除元素上的特定事件.

元素.off("事件","子元素") 解除元素上的事件委托

元素.one("事件" fn) 给元素绑定的事件只触发一次

自动触发事件: trigger()

元素.事件(); 

元素.trigger("事件");

元素.triggerHandler("事件"); 不会触发元素的默认行为. 

### 事件对象:

阻止默认行为:事件.prevebtDefault(); 或者return false;

组织冒泡:事件.stopPropagation()

#### 其他方法:

对象拷贝:$.extend();

$.extend([deep],target,object1,[objectN]) 

deep若为true为深拷贝,否则为浅拷贝.

target为要拷贝的目标对象.

object1为待拷贝到第一个对象的对象.

浅拷贝吧原来对象里面的复杂数据类型地址拷贝给目标对象

深拷贝把里面的数据完全复制一份给目标对象,如果里面有不冲突的属性,会合并到一起.

#### 多库共存:

1,把里面的$同一改为JQuery

2,jQuery规定新的名称:    var 新名称 = $.noConflict()



#### jQuery尺寸:

width()/height():只算width/height

innerWidth()/innerHeight() 包含padding

outerWidth/outerHeight() 包含padding,border

outerWidth(true)/outerHeight(true) 包含padding border margin

#### 位置:

offset(): 设置获取元素偏移 相对于文档的,跟父元素没有关系 有两个属性 left,top

position() 获取相对于带有定位的父级元素偏移位置 只能获取不能设置

scollTop() 设置或返回备选元素被卷去的头部

scollLeft()
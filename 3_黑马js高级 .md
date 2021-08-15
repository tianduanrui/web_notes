使用insertjacentHTML()可以直接把字符串格式元素添加到父元素中

insertjacentHTML(position,html)

#### call方法:

fn.call(); 1.可以调用函数

​      2,可以改变这个函数的this指向

1 :借用父构造函数继承属性:

father.call(this,name,age); 

2:

可以使子构造函数的原型对象指向父构造函数的实例,来继承父构造方法中的方法,然后再将父构造函数的实例中的constructor属性指向子构造函数 

#### es5中新增方法:

数组方法:迭代遍历方法 : foreach(); map(), filter();some();every()

  array.foreach(function(currentValue,index,arr))

  array.filter(function(currentValue,index,arr){ return 条件}) 创建一个新数组,数组中的元素使通过检查指定数组中符合条件的所有元素.主要用于筛选数组.返回值是一个数组.

  array.some(function(currentValue,index,arr){return 条件}) 查找数组中是否有满足条件的元素,返回值为布尔类型.找到第一个符合的就不再继续.

map()和foreach()相似 every()和some()类似.

#### 字符串方法:

trim() 取出字符串两侧空格.

对象方法:

Object.keys(obj):用于获取对象自身所有的属性 类似于for..in 返回一个有属性名组成的数组

Object.defineProperty(obj,prop,descriptor)定义对象中新属性或修改原有的属性. 第三个参数descriptor说明:以对象形式{}书写 属性有:value:属性值,默认undefined  writable:值是否可以重写,默认false enumerable:目标属性是否可以被枚举 默认false  configurable:目标属性是否可以被删除或是否可以再次修改特性. 默认false

### 函数进阶:

函数定义: new Function('参数','参数','函数体'); 参数必须是字符串格式

所有函数都是Function的实例对象

#### 改变函数内this的指向:

1,call方法:

fn.call(thisarg, arg1, arg2); 1.可以调用函数

​      2,可以改变这个函数的this指向

2,apply()方法

fun.apply(thisArg,[argsArray]) 参数必须是数组形式的. 也可以改变this指向.

应用:借助数学内置对象进行操作.

Math.max.apply(thisarg,arr);

3bind()方法:不会调用函数,能改变内部this指向

fun.bind(thisarg,arg1,arg2);

返回由指定的this和初始化参数改造的原函数拷贝,常用于改变定时器内部的this指向. 

#### 严格模式:

1,变量必须先声明,再使用

2,严禁删除已经声明的变量

3,全局作用域函数中的this是undefined

4,构造函数不通过new调用,this指向undefined,入宫给它赋值,会报错.普通模式指向window

5,定时器下this还是执行window

6,事件,对象还是指向调用者

#### 函数变化:

1,函数不能有重名参数.

2,函数必须在顶层声明,不允许在非函数的代码块中声明函数

#### 浅拷贝和深拷贝:

浅拷贝知识拷贝一层,更深层次对象级别的只靠用引用.

深拷贝拷贝多层,每一级别的数据都会拷贝

es6浅拷贝语法:

Object.assign(o,obj); 将obj拷贝到o中.

深度拷贝靠的是函数的递归

### 正则表达式:

匹配字符串中字符组合 验证表单,替换,提取

1,利用RegExp对象来创建正则表达式

var regexp = new RegExp(/222/);

2,利用字面量创建正则表达式

var regexp = / 22/;

3,测试正则表达式方法 test();

正则表达式对象.test(str); 

### ES6:

#### let: 

1,let'声明的变量旨在所处于的块级有效 块级作用域 使用var声明的变量不具备块级作用域特性. 块级作用域能够防止循环变量变成全局变量

2,使用let声明的变量,不存在变量提升.

3,暂时性死区.在块级作用域中定义的变量,不会被外部变量影响.

const:声明常量,具有块级作用域. 声明时必须赋值.常量赋值后,值不能更改.指的是内存地址无法更改,但是若用const赋值一个复杂数据类型如数组,复杂数据类型不能重新 赋值,但是内部的数据可以更改如数组内的元素值可以更改.

解构赋值:从组中提取值,按照对应位置,赋值给变量

let[a,b,c]=[1,2,3]; 

结构失败时,变量为undefined.

对象解构:从对象中提取属性,按照变量的名字匹配对象的属性,赋值给变量.

let person = {name:'张三',age:20};

let{name,age} = person;

另一种写法:

let{name:myName,age:myAge} =person; 左边为跟对象中匹配的属性名,右侧为变量名.

#### 箭头函数: (参数)=>{函数体}

const fn = (参数)=>{函数体};

若函数体中只有一句代码,且代码的执行结果就是返回值,可以省略大括号.

若形参只有一个,那么小括号可以省略.

箭头函数中不绑定this关键字,箭头函数中的this,指向的时函数定义位置的上下文this.

 

剩余参数:剩余参数允许我们将一个不定数量的参数表示为一个数组.

function fun(first,...args){ }; fun(1,2,3,4)

 

剩余参数可以和解构对象结合使用,变量使用剩余参数表示,可以接收对象中没有匹配到的剩余属性.

 

#### 扩展运算符(展开语法)

1,扩展运算符可以将数组或者对象转为用逗号分隔的参数序列. 

2,扩展运算符可以应用于合并数组.

let ary3 = [...ary1,...ary2];

或者 ary1.push(...ary2);

3,将类数组或可遍历对象转换为真正的数组: [...ary]

也可以用构造函数方法:Array.from(类数组 函数); 函数的作用是对数组进行加工处理. 

#### Array的扩展方法:

find(item=>item>1):找出第一个符合条件的数组成员,没有找到则返回undefined.

findIndex(item=>item>1)找出第一个符合条件的数组成员的位置,没有找到返回-1

includes()表示某个数组是否包含给定的值,返回的是布尔值.

#### String的扩展方法:

模板字符串:``

可以解析变量:`****${变量名}`

模板字符串中可以换行

模板字符串中可以调用函数,.`&{函数}`

原字符串.startwith(参数字符串)和endwith() 表示参数字符串是否在原字符串的头部或者尾部,返回布尔值.

repeat():表示将原字符串重复n次,返回一个一个新字符串.

#### Set数据结构

类似于数组,但是成员的值是唯一的,没有重复的值.

本身是一个构造函数,可以接收一个数组作为参数,用来初始化

set可以进行数组去重.

Set实例方法:

add(value),添加某个值,返回Set结构本身

delete(value):删除某个值,返回一个布尔值,表示删除是否成功

has(value):判断该值是否为set成员,返回布尔值

clear();清除所有成员,没有返回值.

forEach(函数)遍历,没有返回值
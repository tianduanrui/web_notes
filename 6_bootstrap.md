### 列排序: 元素位置浮动,可以被覆盖,不影响其他列元素

col-md-pull 向左,

col-md-push 向右

### 列偏移: 元素间空隙,影响其他列元素.

col-md-offset

### 列嵌套:

### 常用样式:

#### 标题:

bootstrap对h1-h6进行了覆盖,并提供了对应类名来为其他元素设置标题样式 .h1-.h6

副标题 saml标签 或.small类名.

#### 段落:

通过.lead来突出强调内容作用(作用就是增大文本字号,加粗文字,对行高和margin也做出相应处理)

<small>:小字号 <b><strong>加粗  <i><em>斜体

#### 强调:

.text-muted:提示 浅灰色

.text-primary 主要 蓝色

.text-success 成功 浅绿色

.text=info 通知信息 浅蓝色

.text-warning 警告 黄色

.text-danger 危险 褐色

#### 对齐效果:

text-left 左对齐

text-right右对齐

text-justify 两端对齐

text-center 居中对齐

#### 列表:

去点列表: .list-unstyled

内联列表:.list-inline  把垂直列表换成水平列表 制作水平导航

定义列表:.dl-horizontal 制作水平定义列表,当标题宽度超过160px时,将会显示三个省略号.

#### 代码:

<code>:显示单行内联代码

<pre>:显示多行代码  样式:pre-scrollable(height,max-height高度固定,为340px.超过存在滚动条)

显示html代码需要使用字符实体来防止当作标签 如<>要使用 &1t &gt代替

<kbd>:显示用户输入代码,如快捷键

#### 表格:

1,基础表格 .table

附加样式:

table-bordered:边框:

table-striped :斑马隔行换色:

table-hover :鼠标悬停高亮

table-condensed :紧凑型表格单元格没内距或内据较其他表格小

tr,td,th样式:

不同类名控制行的不同背景颜色

.active

.success

.info

.warning

.danger 

#### 表单:

文本框

.form-control 表单元素的样式 

 input-lg input-sm 表单控件的大小

下拉选择框select: 多行选择设置 : multiple = "multiple"

复选框:.checkbox 垂直显示  .checkbox-inline 水平显示

单选框:.radio

单选框和复选框的类都写在div上,然后将表单写进div里

#### 按钮:

基础样式:.btn 

复杂样式: .btn btn-danger

btn-default

btn-success

btn-info

btn-warning

btn-danger

btn-link

a标签,span标签等也可以通过按钮样式设置为按钮效果

按钮大小:

btn-sm

btn-xs

btn-lg

按钮禁用: disable 样式禁用但是还可以点击

disable="disable" 真正禁用 

#### 表单布局:

向父元素添加 role="form"

把标签和控件放在一个带有class.form-group的div中

所有的文本元素input,textarea和select添加calss="form-control"

水平表单" form-horizontal

内联表单:form-inline

#### 缩略图:

thumbnail

#### 面板:.panel

.panel-default:默认样式

.panel-heading:面板头

.panel-body:面板主体内容

bootstrap:插件
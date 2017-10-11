#说明
- 本文是css基础学习和了解，按照下面的部分学习，部分内容不完整。
- 简单dome查看css如何使用
- 选择器的学习和了解，样式基层
- 字体和文本，颜色和背景
- 基本视觉格式、浮动和定位
- 盒子模型
- 布局


#css初探

##css使用

通过下面dome学习css的使用位置
代码：
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>css位置</title>
    <link href="a.css" rel="stylesheet" type="text/css" />
</head>
    <style>
        /* @import "a.css"; */
        h2 {
            color: #a1020a;
        }
    </style>
<body>
    <h1 style="color: #77b823;">hello world</h1>
    <h2>我是p标签内容</h2>
    <h3>我是p标签内容</h3>
</body>
</html>
```
```
h3 {
    color: #959595;
}
```
效果如下：
![图片](http://bos.nj.bpc.baidu.com/v1/agroup/256623ae3e4b69f6eac8215e8e5b8f0db12ad165)

可以看到，即便是不写任何css代码，只有html，页面也会有一些默认的样式，这是浏览器默认样式起作用了。此处先不深究，了解即可（但是大部分初学者忽略了这一步）

###三种方式使用css

1. 行内样式
行内样式是所有样式方法中最为直接的一种，它直接对HTML的标记的style属性，然后将CSS代码直接写在其中。
2. 嵌入式
嵌入式又称内嵌式样式表，她是指在`<head></head>`标记之间，用`<style></style>`标记对声明，利用选择器指定需要控制的标记，将样式的声明写在选择器的{}大括号之间，对上诉实例采用内嵌式的效果完全相同，嵌入式的方法依旧麻烦，维护成本也不低，代码还是存在一定的冗余，因此适用于对特殊页面设置单独的样式风格
3. css的外部链接形式
外部链接式CSS样式又称链接式，使用频率最高，也是最实用的的方法，它将HTML页面本身的CSS样式风格分离为两个或者多个单独的css文件，实现了页面框架HTML代码与样式的CSS代码的完全分离。多个页面引用一个css文件。
一般引用样式的`<link>`标签都会写在`<head>`标签里面。

###说明&思考

1. 未定义标签样式，会有默认样式
2. 选择器，属性，值 `h1{color:red;}`。其中`color:red`是声明，多个说明之间`;`分割
3. 第一次访问，内部css渲染效果快。重复访问，link方式效果较好

##css位置对优先级影响

优先级权重相同，就近原则，离标签越近的style优先级越高

## 浏览器渲染过程

学习和使用html、css等web前端知识，了解浏览器的工作原理是非常重要的，推荐扩展阅读的文章 http://www.w3ctech.com/topic/48 

此处不再详细看这个过程（其实我也只是了解皮毛），通过一张图简单看一下html和css这两个的结合过程。

![图片](http://bos.nj.bpc.baidu.com/v1/agroup/beca7545475db93005d3eaf19070fcd629f56b1a)

上图大体的意思是：获取html之后，生成了DOM树，获取css之后，生成样式规则，然后两者结合成功一个Render Tree，即常说的『渲染树』，然后再通过渲染树来绘制页面并显示。

这里的『渲染树』大致的样子，其实是可以通过chrome浏览器看到的，例如

![图片](http://bos.nj.bpc.baidu.com/v1/agroup/adab47c88c878705216b4a18ca3a6913e1e9dc49)

上图中左侧是一个DOM树（即根据HTML结构生成的树），然后每个节点上又挂着了计算之后得出来的样式值。因为你可以看到右侧样式的计算结果，有些优先级低的样式已经被优先级高的覆盖了。这样的一个数据结构，就是浏览器渲染页面需要的。

#选择器

## 选择器类型

css选择器概括将来一共以下几种：
- 标签选择器，如上面的代码，再如`* {margin:0;}`
- ID选择器，如`#p1 {color:blue;}`
- class选择器，如`.content {width:100px;}`
- 属性选择器，如`a[href] {color:#ff0;}`，再如`input[type="text"] {border:0}`
- 上下文选择器，如 `div p {font-size:10px;}`，再如`div .content {padding:0;}`
- 伪类，如 `a:hover {color:red}`
- 伪元素，如 `a::after {content：''; display: table; clear: both}`

##选择器说明

- 标签选择器
标签选择器很简单，用哪个标签，就写哪个即可，例如上文的 `h1 {...} p {....}`
`*`标识通配表达式 ，匹配全部标签元素

### ID选择器

html的body标签内的所有标签，每个标签都可以设置一个`id`属性，这个属性具有唯一性，不能与其他标签重复。
```html
	<style>
	    #div1 {
	        background-color: #004444;
	        width: 100px;
	        height: 100px;
	    }
	</style>
    <div id="div1"></div>
```

### class选择器

在html的标签中，可以设置一个特殊的`class`属性，例如`<div class="div1"></div>`，设置之后，浏览器会去css代码中寻找`.div1`这个选择器，这就是class选择器，（如果class属性值有多个，可用空格隔开）。完整代码如下：
```html
	<style>
	    .div1 {
	        background-color: #004444;
	        width: 100px;
	        height: 100px;
	    }
	</style>
    <div class="div1"></div>
    <div class="div1"></div>
```

### 属性选择器

html即xml的一个特殊类型，每个标签都会有属性。上文讲到的ID和class按理说也是标签的属性，但是它们写法比较特殊，用于优先级计算（下文讲到）时也比较特殊，就单独拿出来讲。但是如果针对不是ID和class的属性，可是可以作为选择器的。
```html
	<style>
	   a[href] {
	        color: darkred;
	    }
	</style>
	<!--我的颜色是默认颜色-->
	<a>我没有href属性</a>
	<!--我的颜色是css定义的-->
	<a href="www.baidu.com">我是连接，有href属性</a>
```

###上下文选择器

- `div p {...}`后代选择器，`div`与`p`要符合祖先子孙关系
- `div > p {...}`选择子元素，`div`与`p`要符合父子关系
- `div + p {...}`选择相邻兄弟元素，`div`之后紧接着是`p`，而且有相同的父元素
- `div ~ p {...}`  选择兄弟元素，`div`之后是`p`，不一定相连
结合下面代码理解
```html
	<style>
	    div p {
	        color: red;
	    }
	    div > span {
	        color: green;
	    }
	    span + span {
	        color: blue;
	    }
	    a ~ a {
	        color: yellow;
	    }
	</style>

	<div>
	    <p>第一个p标签</p>
	    <span>我是第一个span</span>
	    <p>第二个p
	        <span>第二个span</span>
	    </p>
	    <span>
	        我是第三个span
	    </span>
	    <span>
	        我是第四个span
	    </span>
	    <a>我是第一个a</a>
	    <a>我是第二个a</a>
	    <a>我是第三个a</a>
	</div>
```

### 伪类

- 链接的交互样式。即一个链接点击之前、鼠标放上时、点击过程中、点击之后等这些样式的定义
```html
<style>
    a:link {
        color: blue;
    }
    a:visited {
        color: red;
    }
    a:hover {
        color: orange;
    }
    a:active {
        color: green;
    }
</style>
<a href="http://www.baidu.com">测试伪类</a>
```

-  输入框在focus时的样式，这个比较好理解。代码如 `input:focus {...}`

- 命中url锚点时的样式。例如，html和css如下定义
```
<style>
#div1:target {..自定义样式..}
</style>

<div id="div1">
	....
</div>
```
此时css定义的样式不会起作用，但是当url中有`#div1`的锚点时，就会起作用。

- 用伪类选中集合中的第几个元素。例如针对如下html代码
```
<ul>
	<li>a</li>
	<li>b</li>
	<li>c</li>
	<li>d</li>
	<li>e</li>
	<li>f</li>
</ul>
```
这是一个无序列表，`li:first-child{...}`将命中第一个元素，`li:last-child`将命中最后一个元素，`li:nth-child(2)`将命中第三个元素（从0开始计数），`li:nth-child(odd)li:nth-child(2n)`和`li:nth-child(even)li:nth-child(2n+1)`可命中偶数元素和奇数元素

### 伪元素

伪元素这个概念比较重要，其中最常用的就是`:after`和`:before`这两个
```
<style>
    .span1:before {
        content: 'hello';
        color: red;
    }
    .span1:after {
        content: '!!!!!';
        color: blue;
    }
</style>
<span class="span1">world</span>
```
![图片](http://bos.nj.bpc.baidu.com/v1/agroup/db75fd7fe721c5d1a27cce363cbc84fd3c117a36)

##权重说明

从CSS代码存放位置看权重优先级：内嵌样式 > 内部样式表 > 外联样式表。其实这个基本可以忽视之，大部分情况下CSS代码都是使用外联样式表。

从样式选择器看权重优先级：important > 内嵌样式 > ID > 类 > 标签 | 伪类 | 属性选择 > 伪对象 > 继承 > 通配符。

- 代表内联样式，如: style=””，权值为1000。
- important的权重为1,0,0,0
- ID的权重为0,1,0,0
- 类的权重为0,0,1,0
- 标签的权重为0,0,0,1
- 属性的权重为0,0,1,0
- 伪类的权重为0,0,1,0
- 伪对象的权重为0,0,0,1
- 通配符的权重为0,0,0,0
示例：
![图片](http://bos.nj.bpc.baidu.com/v1/agroup/9816180810c90c75bef1d22a65c48cf16dfe9926)

##样式继承

针对某些css样式（特别是文字相关的，例如颜色、字体、字号、间距等），是可以从祖先元素中继承过来的。例如,通常会设置`body {color:#333}`使页面所有文字的颜色都是`#333`，因为浏览器默认样式中`color:#000`。
然而有些属性是不可以被继承的，因为继承这些没有意义甚至会导致页面混乱。这些属性主要涉及到元素的尺寸、定位、边框、内外边距等。
最主要的是记得，与文字相关的属性，经常使用继承来设置。

#字体与文本

##字体属性

CSS 字体属性定义文本的字体系列、大小、加粗、风格（如斜体）和变形（如小型大写字母）。

- `font-family` 字体类型系列
- `font-weight` 字体加粗
- `font-size` 字体大小。可以使用px，em，rem，百分比等单位。也可以使用相对大小
- `font-style` 字体风格，例如斜体等
- `font` 字体设置。包括font-style | font-variant | font-weight | font-size | line-height | font-family 等。例子：
```
body {
　　 font-family: Arial, Helvetica, sans-serif;
    font-size: 13px;
    font-weight: normal;
    font-variant: small-caps;
    font-style: italic;
    line-height: 150%;
}
body {
    font: italic small-caps normal 13px/150% Arial, Helvetica, sans-serif;
}
```

##文本属性

- `text-indent` 文本缩进 
- `text-align` 水平对其
- `line-height` 行高。可用于当行垂直居中
- `vertical-align` 垂直对其文本。文本相对于极限的垂直距离
- `word-spacing` 字间隔，letter-spacing字母间隔。需分清楚。
- `text-decoration` 文本装饰，下划线等装饰
- `text-shadow` 文本阴影
- `white-space` 对文档中空格，换行和tab字符的处理
- `text-overflow` 属性规定当文本溢出包含元素时发生的事情。
```
/*单行文本超出显示'...'*/
    white-space: nowrap;
    text-overflow: ellipsis;
    overflow: hidden;
```

#颜色和背景

##颜色命名

颜色命名可以使用，命名颜色、RGB（RGBA）、十六进制RGB
转换示例：
|颜色 | 百分数 | 数值 | 十六进制 | 简写十六进制 | 
|---|---|---|---|---|
|blue | rgb(0%,0%,100%) | rgb(0,0,255) | #0000ff | #00f |
|white | rgb(100%,100%,100%) | rgb(255,255,255) | #ffffff | #fff |
|black | rgb(0%,0%,0%) | rgb(0,0,0) | #000000 | #000 |
|red | rgb(100%,0%,0%) | rgb(255,0,0) | #ff0000 | #f00 |
|orange | rgb(100%,40%,100%) | rgb(255,102,0) | #ff6600 | #0f60 |
|green | rgb(0%,50%,0%) | rgb(0,128,0) | #008000 |  | 

##前景色

`color`  字体颜色，边框颜色（未规定边框颜色，显示前景色）

##背景

- `background-color` 背景颜色
- `background-image` 背景图片（不可继承）。
   `background-repeat` 重复方向
   `background-position` 背景定位
   `background-attachment` 属性设置背景图像是否固定或者随着页面的其余部分滚动。
- background 简写属性在一个声明中设置所有的背景属性。
可以设置如下属性：background-color、background-position、background-size、background-repeat、background-origin、background-clip、background-attachment、background-image
```
div {
    background-image: url('http://yunyuan.baidu.com/static/img/logo.png');
    background-color: #ddd;
    background-repeat: repeat-y;
    background-position: 50% 50%;
}
div {
    background: url('http://yunyuan.baidu.com/static/img/logo.png') #ddd repeat-y 50% 50%;
}
```

#基本视觉样式

##基础框

css假定每个元素都会生成一个或者多个矩形框，这称为元素框。各元素框中心有一个内容区，这个内容区有可选的内边距、边框、外边距。

- 正常流  从左向右、从上到下显示
- 非替换元素  元素内容包含在文档中
- 替换元素  用作为其他内容占位符的一个元素
- 块级元素  段落、标题或div之类的元素。或者`display:block`
- 行内元素  指`strong`或`span`之类的元素。或者`display:inline`

##块级元素

段落、标题或div之类的元素。或者`display:block`
以block模式存在于文本流中，可以通过属性调节实现水平格式化，垂直格式化

###注意事项：

1. 合并外边框
在常规文档流中，2个或以上的块级盒模型相邻的垂直margin会被折叠。最终的margin值计算方法如下：
a、全部都为正值，取最大者；
b、不全是正值，则都取绝对值，然后用正值减去最大值；
c、没有正值，则都取绝对值，然后用0减去最大值。
注意：相邻的盒模型可能由DOM元素动态产生并没有相邻或继承关系。
2. div塌陷
a、在父级加入`overflow：hidden`；
b、在父级用`padding-top`
c、在父级加`position：absolute`；
d、在父级加`border`；

##行内元素

可以设置行布局，行内格式化等

###注意事项

1. 基线与行高
2. 字形和内容区
3. 非替换元素的呈现展示形式

##改变元素显示 display

可以通过设置`display`来改变元素框的属性，使之成为块元素或者行内元素

###注意事项

**display visibility 隐藏元素区别**

- `display`
`display:none`隐藏（元素消失），可恢复inline,block显示
1. display被设置为block(块)时，容器中所有的元素将会被当作一个单独的块，就像div元素一样，它会在那个点被放入到页面中。(实际上你可以设置span的display:block，使其可以像div一样工作。
2. display设置为inline，将使其行为和元素inline一样---即使它是普通的块元素如div，它也将会被组合成像span那样的输出流。最后是display被设置：none,这时元素实际上就从页面中被移走，它下面所在的元素就会被自动跟上填充。
-` visibility`
visibility属性用来确定元素是显示还是隐藏，visible表示显示，hidden表示（仅）隐藏，不可恢复。当visibility被设置为"hidden"的时候，元素虽然被隐藏了，
1. 仍然占据它原来所在的位置。visibility会保留元素的位置.
2. 元素被隐藏之后，就不能再接收到其它事件了，当其被设为"hidden"的时候，就不能再接收响应到事件了，因此也就无法通过JS令其显示出来。

##列表与生成内容

列表形式例如
```html
<div>
    <ul>
        <li>我是无需列表</li>
        <li>我是无需列表</li>
    </ul>
    <ol>
        <li>我是有序列表</li>
        <li>我是有序列表</li>
    </ol>
</div>
```
1. `list-style-type` 标识类型
2. `list-style-image` 使用图片作为标志（可以继承）
3. `list-style-position` 列表标志位置
4. `list-style` 以上样式的汇总

#盒子模型

当在浏览器中查看一个元素的样式的时候，每个元素都可以看到右侧的这个正方形，如下图。这就是所谓的『盒子模型』，即一个『块』的尺寸，都有width（宽度）、height（高度）、padding（内边距）、border（边框）、margin（外边距）组成。

![图片](http://bos.nj.bpc.baidu.com/v1/agroup/7ecdfb386002e5c115c7c3ec9e72c47bd3551742)

早期的IE6浏览器在处理盒子模型的时候，与当前W3C标准有些兼容性问题，但是由于我们主要针对移动端高级浏览器，就不考虑IE6的兼容性问题了。

下面实现一个简单的盒子模型的demo，盒子模型的css代码可参见截图右侧，如下图。注意看到左侧的宽度（370px）和右侧css样式中的宽度（300px），说明最终盒子的总宽度和总高度，是由css中规定的宽度或高度，加内边距、加边框、加外边距的宽度。

![图片](http://bos.nj.bpc.baidu.com/v1/agroup/5bf99f36f21fd21699317990dd0a21f3325f78e2)

涉及到盒子模型的css属性值有以下情况，比较容易理解，就不一一演示了

- `width` 设置宽度
- `height` 设置高度
- `border` 设置边框 参见 http://www.w3school.com.cn/cssref/pr_border.asp
- `padding` 设置内边距 参见 http://www.w3school.com.cn/cssref/pr_padding.asp
- `margin` 设置外边距 参见 http://www.w3school.com.cn/cssref/pr_margin.asp

以上是盒子模型的最基本的情况，其实它还可能遇到其他一些意外情况，例如宽度是手动设置的、宽度是充满父容器的等，这些可参见 http://www.cnblogs.com/wangfupeng1988/p/4287292.html

###注意事项

1. `body`设置margin后背景颜色问题，原因是`html`未被激活，背景颜色和`body`一样。
2. `margin`可以为负数，`padding`、`border`负数不起作用
3. 百分数值定义为相对于父元素的width，这不仅用于左右外边距，也应用于上下外边距
4. 负外边距和合并外边距问题
5. margin,padding,width,height中auto设置产生的效果
水平居中，垂直居中
```
<style>
.div {
    background: #DE5F5F;
    border: 10px solid #ccc;
    margin: 20px;
    padding: 10px;
    position: relative;
}
.div-1 {
    width: 50px;
    height: 50px;
    background: #fff;
    position: absolute;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    margin: auto auto;
}
</style>
<div class="div">
    <div class="div-1" style="">水平垂直居中</div>
</div>
```

#浮动和定位

##浮动

属性`float`值
- `left` 向左浮动
- `right`  向右浮动
- `none` 防止元素浮动

###注意事项

1. 会以某种方式将浮动元素从文档的正常流中删除，但是还是会影响布局
2. 浮动元素的外边距不会合并
3. 浮动元素会生成一个块级元素
4. 浮动元素的左（或右）外边界不能超出其包含块的左（或右）内边界。
5. float 造成父元素塌陷，解决方法如下，使用clear，清除浮动
```html
<style>
	.clearfix { 
	    *zoom: 1; 
	} 
	.clearfix:before, 
	.clearfix:after { 
	    display: table; 
	    line-height: 0; 
	    content: ""; 
	}
	.clearfix:after { 
	    clear: both; 
	} 
</style>
```

##定位

- `top`、`right`、`bottom`、`left` 偏移属性
- `position:static` 元素框正常生成，块级元素生成一个矩形框，座位文档流的一部分，行内元素则会创建一个或者多个行框，置于其父元素中。
- `position:relative` 元素框偏移某个距离，元素仍保持其未定位前的形状，它原来所占的空间仍保留![图片](http://bos.nj.bpc.baidu.com/v1/agroup/bb787dc3370961d46a7750ce24333e8f76abaa82)
可以通过一个Demo来看一下效果
![图片](http://bos.nj.bpc.baidu.com/v1/agroup/0855d52f4dc2965b97249dbf7dfb151f6658da3f)
- `position:absolute` 元素框从文档流完全删除。相对于最近的`position`不是`static`的祖先元素（可以是任何类型）定位
- `position:fix` 元素框表现类似于position:absolute，不过其包含块是视窗本身。
`absolute`和`fixed`原理差不多，唯一区别就是——`fixed`是完全根据浏览器边界定位，而`absolute`是根据最近的一个定位上下文元素来定位。这里的『定位上下文』下文会解释，此处我们就当`absolute`也是根据浏览器定位。即可用下图标识，横向、竖向的剪头，分别标识`left`和`top`的值。
![图片](http://bos.nj.bpc.baidu.com/v1/agroup/8f2cfc664ab65bdc0f3196a56fd5419ea150c6f5)
代码可以这样表示
```
.class1 {
	position:fixed;
	top: 30px; 
	left: 30px;
}
.class2 {
	position:absolute;
	top: 30px; 
	left: 30px;
}
```
另外，除了以上的定位规则之外，两者还有一个『脱离文档流』的特性（记得`float:left / right` 也会导致脱离文档流，但是有解决方法），但是这里`absolute/fixed`脱离文档流，就没有办法解决了，特性就是这样的。具体表现可以看如下例子

![图片](http://bos.nj.bpc.baidu.com/v1/agroup/417aa15e2830a9bacd7bdbf74832e1c0e89e4604)

**层叠规则**
`pisition: absolute/fixed/relative`定位时，如果多个元素出现在同一个位置，可能会导致重叠，那么谁在上谁在下？

默认来说，同意个属性值的元素，是『后来者居上』，但是可以通过`z-index`来设置，`z-index`的值越大，就越靠上。例如设置`z-index:99999`。

#布局

浏览器得到HTML之后只能生成DOM树，仅仅是一个树，而我们看到的却是一个页面。将DOM树形成页面的过程中，就是由css设计的，即css的最终作用就是做页面排版。那么一个页面的排版，到底需要做哪些事情，我们来拿一个页面分析一下。
![图片](http://bos.nj.bpc.baidu.com/v1/agroup/e3dd2553d2df034db9d363c5f5f2f8fa4b18ea85)
如上图。按照html+css的布局思想，页面的布局就是块的定位（左、中、右、上）、尺寸（大小、边距）和嵌套（父子关系），以及块中内容区域的样式设置（如字体、颜色、行间距等）。因此，重点在于搞清楚这些功能。
下面按照这个顺序，依次来看看css是如何完成这些功能的。

## 布局 - table

现在看来，使用table做布局是最low的方式，除了浏览器兼容比较好（兼容IE6、7）之外，其他地方几乎一无是处。因此，从早期就已经摒弃了这种布局方式。不过发现[新闻的webapp](http://m.news.baidu.com/news)的导航部分，还是用着table布局，正好可以体验一下这种布局方式

![图片](http://bos.nj.bpc.baidu.com/v1/agroup/c0b4728cbb9977525aec77e4b04117c4080f46dc)

## 布局 - float

float——一个非常纠结的属性，因为它本来设计出来的用意是为了做图文混排，如下图。但是却因为它可以实现布局（比table布局要好），而硬生生的被当做一个布局的方法。虽然你需要做很多工作来协助它完成布局。这也是为何css3中要重新设计flex布局的原因。

![图片](http://bos.nj.bpc.baidu.com/v1/agroup/956acc0d474d438dbf5d894505f9de9fe8fd2193)

目前已经有成熟的使用float布局的案例，例如前期经典的[圣杯布局 & 双飞翼布局](http://www.jianshu.com/p/c3f33f4aed02/comments/1072948)，都是为了实现『左、中、右』布局（主要用于PC端），如下效果
![图片](http://bos.nj.bpc.baidu.com/v1/agroup/d25bd02c8eecc24834ccdd52810eca9cccb45b4d)

后来twitter开源[bootstrap](https://github.com/twbs/bootstrap)，里面非常牛X的栅格布局，也是使用了float。可见float在布局中的重要地位。

![图片](http://bos.nj.bpc.baidu.com/v1/agroup/56112fce47a1bbd71f3edb965a3e352fcc459e20)

具体如何使用float实现一个复杂的，可以参见以上的那些介绍和链接，下面会简单介绍一下float的使用。*PS：主要用于移动端的系统，不建议再使用float来布局，而是用css3中的flex，React Native也支持flex布局，此处建议做一个了解即可。*

float的属性值有两个`float:left` `float:right`，这两个其实是一个意思，一个向左浮动，一个向右浮动。下面以`float:left`为例来讲解。

```
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>css test</title>
    <style>
        .float-left {
            width:100px;
            height: 100px;
            float: left;
        }
        .clear-both {
            clear:both;
            height: 0;
        }
    </style>
</head>
<body>
    
    <div style="border:1px solid #333;">
        <div class="float-left" style="background-color:red">item1</div>
        <div class="float-left" style="background-color:yellow">item1</div>
        <div class="float-left" style="background-color:blue">item1</div>

        <!--清除浮动-->
        <div class="clear-both"></div>
    </div>

</body>
</html>
```

运行的效果如下

![图片](http://bos.nj.bpc.baidu.com/v1/agroup/b3b822399557fa7568879386b838a4347ade7045)

这样就形成了一个简单的排列效果。其实再复杂的排列样式，也是在这个基础上再增加一些例如宽度计算的工作来完成的。

注意代码里面有一段 `clear:both`，这个的意思是清除浮动，其实这就是用float做布局的一个后遗症。因为元素被`float:left`之后，会出现一个现象叫做**脱离文档结构**（下文的`postion:absolute`也会有这个问题），必须用`clear:both`来解决这个问题。而**脱离文档结构**的细节，我们此处就不再深究了，总之是一个不好的情况、但被已有解决方案能彻底解决。


## 布局 - flex

css3 新增内容，完全为布局而生（不像float那么纠结），目前移动端的浏览器基本都支持，因此也被React Native采用。接下来会有专门的介绍，此处就不深入了。扩展阅读 http://www.runoob.com/cssref/css3-pr-flex.html
http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html


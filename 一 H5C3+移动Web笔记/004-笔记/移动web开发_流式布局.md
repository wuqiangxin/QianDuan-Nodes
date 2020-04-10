# 移动web开发流式布局

### 1. 移动端基础

#### 1.1 浏览器现状

![](images\broswer.jpg)

国内的UC和QQ，百度等手机浏览器都是根据Webkit修改过来的内核，国内尚无自主研发的内核，就像国内的手机操作系统都是基于Android修改开发的一样。

**总结：兼容移动端主流浏览器，处理Webkit内核浏览器即可。**

#### 1.2 手机屏幕的现状

+ 移动端设备屏幕尺寸非常多，碎片化严重。
+ Android设备有多种分辨率：480x800, 480x854, 540x960, 720x1280，1080x1920等，还有传说中的2K，4k屏。
+ 近年来iPhone的碎片化也加剧了，其设备的主要分辨率有：640x960, 640x1136, 750x1334, 1242x2208等。
+ 作为开发者无需关注这些分辨率，因为我们常用的尺寸单位是 px 。

#### 1.3 常见移动端屏幕尺寸

<img src="images/1.png">

​	注：以上数据均参考自 https://material.io/devices/ 。  	

​	注：作为前端开发，不建议大家去纠结dp，dpi，pt，ppi等单位，这些单位是Android和IOS开发人员需要熟悉的，前端开发不常用这些单位。

#### 1.4 移动端调试方法

我们在开发移动端网页的时候，需要调试看效果是否正确，如何调试呢？

有以下三种：

+ Chrome DevTools（谷歌浏览器）的模拟手机调试
+ 搭建本地web服务器，手机和服务器一个局域网内，通过手机访问服务器
+ 使用外网服务器，直接IP或域名访问

目前，我们使用第一种即可，服务器属于后边课程介绍的内容。

**模拟手机调试如下**：

![](images\debug.jpg)

**切换手机型号如下**：

![](images\debug-change-mobile.jpg)

**调整缩放比例**：（如果调整为分辨率比较大的手机型号，但是显示的竟然变小了，这是因为缩放比例问题，改为百分比即可）

![](images\debug-change-scale.jpg)

**添加手机型号**：

**首先先编辑**：

![](images\debug-edit.jpg)

**再添加**：

![](images\debug-add.jpg)



#### 1.5 移动端开发：

我们以在浏览器通过模拟手机形式，去访问jd.com，自动跳转到了m.jd.com（手机端的京东界面，m：moblie）。这是因为京东可以知道你是以手机的形式访问过去的，自动给你做了跳转。

![](images\mobile-ym.jpg)



总结：

- 移动端开发，就是编写移动端的网页
- 移动端浏览器我们主要对webkit内核进行兼容
- 我们现在开发的移动端主要针对手机端开发（pad屏幕较大，可以使用PC端界面）
- 现在移动端碎片化比较严重，分辨率和屏幕尺寸大小不一
- 学会用谷歌浏览器模拟手机界面以及调试

### 2. 视口

视口（viewport）就是浏览器显示页面内容的屏幕区域。 视口可以分为布局视口、视觉视口和理想视口。

#### 2.1 布局视口 layout viewport

一般移动设备的浏览器都默认设置了一个布局视口，用于解决早期的PC端页面在手机上显示的问题。

iOS, Android基本都将这个视口分辨率设置为 980px，所以PC上的网页大多都能在手机上呈现，只不过元素看上去很小，一般默认可以通过手动缩放网页。

<img src="/images/2.png">





**总结**：

- 布局视口为啥设置为980px？因为我们PC端的网页一般就是1000左右，所以差不多能显示完。
- 布局视口的缺点，就是现实的pc的网页的内容会比较小。
- 下图是以前处理过的PC端的网页，我们通过模拟手机查看一下，发现非常小：

![](images\viewport.jpg)

####2.2 视觉视口 visual viewport

字面意思，它是用户正在看到的网站的区域。注意：是网站的区域。

visual：[ˈvɪʒuəl]，视觉的，看得见的

我们可以通过缩放去操作视觉视口，但不会影响布局视口，布局视口仍保持原来的宽度。

<img src="images/3.png">

一个比较大的布局视口，想要在一个比较小的视觉视口中显示完整，并且大小还合适，那怎么办呢？

使用理想视口。

#### 2.3 理想视口 ideal viewport

- ideal： [aɪˈdi:əl] ，理想的
- 为了使网站在移动端有最理想的浏览和阅读宽度而设定

- 理想视口，对设备来讲，是最理想的视口尺寸

- 需要手动添写meta视口标签通知浏览器操作

- meta视口标签的主要目的：布局视口的宽度应该与理想视口的宽度一致，简单理解就是设备有多宽，我们布局的视口就多宽

- **总结：我们开发最终会用理想视口，而理想视口就是将布局视口的宽度修改为视觉视口**
  - 其实之前为啥显示的不合适，就是因为布局的宽度设置的太宽了（980），而我们手机的屏幕太窄了，两者不相匹配。
  - 大家肯定在想，我有多大的区域可以显示，你的布局就用多大区域不就行了
  - 哎，对了，那么就将布局视口的宽度修改为视觉视口的宽度即可
  - 说人话：将布局的宽度与手机屏幕宽度保持一致

#### 2.4 meta标签

语法：

```html
<meta name="viewport" content="width=device-width, user-scalable=no, 
 	initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
```

最标准的viewport设置

+ 视口宽度和设备保持一致
+ 视口的默认缩放比例1.0
+ 不允许用户自行缩放
+ 最大允许的缩放比例1.0
+ 最小允许的缩放比例1.0
  

**代码**：

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0,maximum-scale=1.0, minimum-scale=1.0, user-scalable=no">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>

<body>
    黑马程序员
</body>

</html>
```

**效果**：

**添加之前的效果**：

![](images\meta-before.jpg)

**添加之后的效果**：

![](images\meta-after.jpg)

### 3. 二倍图

我们在学习移动开发的时候，还需要普及一些知识点：物理像素，物理像素比

####3.1 物理像素&物理像素比

- 物理像素点指的是屏幕显示的最小颗粒，是物理真实存在的。这是厂商在出厂时就设置好了,比如苹果6 是  750* 1334
- **物理像素其实就是我们的分辨率，分辨率为750*1344，那么一行可以放750个像素点**
- 我们开发时候的1px 不是一定等于1个物理像素的
- PC端页面，1个px 等于1个物理像素的，但是移动端就不尽相同
- **一个px的能显示的物理像素点的个数，称为物理像素比或屏幕像素比**

- 如果把1张100*100的图片放到手机里面会按照物理像素比给我们缩放

我们来验证一下上述的结论：

代码：

```html
    <style>
        * {
            margin: 0;
            padding: 0;
        }
        
        div {
            width: 300px;
            height: 300px;
            background-color: pink;
        }
        /* 1. 物理像素 就是我们说的分辨率  iPhone8的物理像素是 750 */
        /* 2. 在 iPhone8里面  1px 开发像素  =  2个物理像素  */
    </style>
</head>

<body>
    <div></div>
</body>
```

效果：

![](images\px01.png)



上图结果：

- 发现在pc端1px就是一个像素点
- 但是在手机端，发现300px他应该占用iphone678宽度750物理像素点差不多一半呀。
- 但是现在的现象是大于一半，将近占满了，这是怎么回事呢？
- 还有一个问题，就是哎，iphone678的分辨率不是750*1334么？那么上图顶端为啥显示的是375\*667呀？好像缩小了一半，为啥？

手动修改一下width：

![](images\px02.jpg)

上图结论：

- 手动改为375px，发现正好填满，375px正好填满750的物理像素点。
- 那么在iphone678中，1px=2倍物理像素点 （物理像素比为2）
- 刚刚的问题，上图顶端显示的375\*667是啥呀？其实是iphone678 物理像素点转换后的px单位，这个称之为开发尺寸

各个手机的开发尺寸，以及物理像素比，如下图：

![](images\1.png)

#### 3.2 二倍图

- 那么为啥手机端不能像PC端那样，1px就等于1个物理像素点呢？
  - PC端 和 早前的手机屏幕 / 普通手机屏幕，他们的像素比是 1CSS像素  =  1 物理像素
  - 但是大家想想一下，电脑屏幕多大，手机屏幕多大，差距有点大对吧。
  - 屏幕电脑能容纳下的物理像素点比如是1000*700，那么他要是物理像素比为1:1，那么电脑能显示1000px\*700px的网页
  - 手机屏幕比较小，他只能容纳下500*350个物理像素点，那么他要是物理像素比也为1:1，那么他是显示不了与电脑屏幕相同大小的网页的
  - 那怎么办呢？手机屏幕大小是有限的，那么我们可以在有限的空间内，压缩出更多的物理像素点。这就是Retina
- Retina（视网膜屏幕）是一种显示技术，可以将把更多的物理像素点压缩至一块屏幕里，从而达到更高的分辨率，并提高屏幕显示的细腻程度。

![](images\retina.jpg)

- 那么问题就来了，文字是矢量的，放大是不会变模糊的，但是图片放大就会模糊了
- 对于一张 50px * 50px 的图片,在手机或 Retina 屏中打开，按照刚才的物理像素比会放大倍数，这样会造成图片模糊
- 在标准的viewport设置中，使用**倍图**来提高图片质量，解决在高清设备中的模糊问题
- 通常使用**二倍图**， 因为iPhone 6\7\8 的影响·。
- 但是现在还存在3倍图4倍图的情况，这个看实际开发公司需求
- 背景图片 注意缩放问题

**二倍图案例代码：**

```html
    <style>
        /* 我们需要一个50*50像素（css像素）的图片 直接放到我们的iphone8 里面会放大2倍  100* 100 就会模糊 */
        /* 我们采取的是 放一个 100* 100 图片  然后手动的把这个图片 缩小为 50* 50 （css像素） */
        /* 我们准备的图片 比我们实际需要的大小 大2倍，这就方式就是 2倍图 */
        
        img:nth-child(2) {
            width: 50px;
            height: 50px;
        }
    </style>
</head>

<body>
    <!-- 模糊的 -->
    <img src="images/apple50.jpg" alt="">
    <!-- 我们采取2倍图 -->
    <img src="images/apple100.jpg" alt="">
</body>
```

效果：这个需要放到真实手机上查看，通过谷歌模拟手机不行：

![](images\2scalepic.jpg)

#### 3.3 背景缩放background-size

background-size 属性规定背景图像的尺寸

```
background-size: 背景图片宽度 背景图片高度;
```

单位： 长度|百分比|cover|contain;

cover把背景图像扩展至足够大，以使背景图像完全覆盖背景区域。（**等比例拉伸，完全覆盖，会有一边超出**）

![](images\bgi-cover.jpg)



contain把图像图像扩展至最大尺寸，以使其宽度或高度完全适应内容区域。（**等比例拉伸，任意一边先与盒子重合即可**）

![](images\bgi-contain.jpg)

![](images\bgi-contain2.jpg)

代码：

```html
    <style>
        div {
            width: 500px;
            height: 500px;
            border: 2px solid red;
            background: url(images/dog.jpg) no-repeat;
            /* background-size: 图片的宽度 图片的高度; */
            /* background-size: 500px 200px; */
            /* 1.只写一个参数 肯定是宽度 高度省略了  会等比例缩放 */
            /* background-size: 500px; */
            /* 2. 里面的单位可以跟%  相对于父盒子来说的 */
            /* background-size: 50%; */
            /* 3. cover 等比例拉伸 要完全覆盖div盒子  可能有部分背景图片显示不全 */
            /* background-size: cover; */
            /* 4. contain 高度和宽度等比例拉伸 当宽度 或者高度 铺满div盒子就不再进行拉伸了 可能有部分空白区域 */
            background-size: contain;
        }
    </style>
</head>

<body>
    <div></div>
</body>
```

#### 3.4  背景二倍图

插入图需要使用二倍图，而背景图也需要。

原理一样。

代码：

```html
    <style>
        /* 1. 我们有一个 50 * 50的盒子需要一个背景图片，但是根据分析这个图片还是要准备2倍， 100*100 */
        /* 2. 我们需要把这个图片缩放一半，也就是 50*50  background-size*/
        
        div {
            width: 50px;
            height: 50px;
            border: 1px solid red;
            background: url(images/apple100.jpg) no-repeat;
            background-size: 50px 50px;
        }
    </style>
</head>

<body>
    <div></div>
</body>
```

#### 3.5 多倍切图

我们在移动端开发，需要原图，2倍图，有时候还需要3倍图，那如何快速处理呢？

cutterman，可以帮助我们快速的切出不同倍数的图片。

![](images\cutterman.jpg)

**使用**：

![](images\cutterman-use.jpg)

**结果**：

![](images\cutterman-result.jpg)



### 4. 移动开发选择和技术解决方案

####4.1 移动端主流方案

##### 1.单独制作移动端页面（主流）

- 通常情况下，网址域名前面加 m(mobile)可以打开移动端。
- 通过判断设备，如果是移动设备打开，则跳到移动端页面。  
- 也就是说，**PC端和移动端为两套网站，pc端是pc断的样式，移动端在写一套，专门针对移动端适配的一套网站**


京东pc端：

<img src="images/5.png">



京东移动端：

<img src="images/6.jpg">



##### 2.响应式页面兼容移动端（其次）

响应式网站：即pc和移动端共用一套网站，只不过在不同屏幕下，样式会自动适配

三星电子官网： www.samsung.com/cn/ ，通过判断屏幕宽度来改变样式，以适应不同终端。

缺点：制作**麻烦**， 需要花很大精力去调**兼容性问题**

<img src="images/7.jpg">



#### 4.2 移动端技术解决方案

1.移动端浏览器兼容问题

移动端浏览器基本以 webkit 内核为主，因此我们就考虑webkit兼容性问题。

我们可以放心使用 H5 标签和 CSS3 样式。

同时我们浏览器的私有前缀我们只需要考虑添加 webkit 即可

2.移动端公共样式

移动端 CSS 初始化推荐使用 normalize.css/

Normalize.css：保护了有价值的默认值

Normalize.css：修复了浏览器的bug

Normalize.css：是模块化的

Normalize.css：拥有详细的文档

官网地址： <http://necolas.github.io/normalize.css/>

#### 4.3 移动端大量使用 CSS3盒子模型box-sizing

- 传统模式宽度计算：盒子的宽度 = CSS中设置的width + border + padding 

- CSS3盒子模型：     盒子的宽度=  CSS中设置的宽度width 里面包含了 border 和 padding 

- 也就是说，我们的CSS3中的盒子模型， padding 和 border 不会撑大盒子了
- 代码：

```
/*CSS3盒子模型：border-box，边框盒子，理解：从边框开始计算盒子的大小（包括边框内部所有内容，边框，内边距，内容）*/
box-sizing: border-box;
/*传统盒子模型：content-box，内容盒子，理解：从内容开始计算盒子大小（只包括内容）*/
box-sizing: content-box;

```

- 移动端可以全部CSS3 盒子模型

- PC端如果完全需要兼容，我们就用传统模式，如果不考虑兼容性，我们就选择 CSS3 盒子模型


#### 4.4 移动端特殊样式

```
    /*CSS3盒子模型*/
    box-sizing: border-box;
    -webkit-box-sizing: border-box;
    /*点击高亮我们需要清除清除  设置为transparent 完成透明*/
    -webkit-tap-highlight-color: transparent;
    /*在移动端浏览器默认的外观在iOS上加上这个属性才能给按钮和输入框自定义样式*/
    -webkit-appearance: none;
    /*禁用长按页面时的弹出菜单*/
    img,a { -webkit-touch-callout: none; }

```

点击高亮效果（上），以及添加transparent效果（下）：

![](images\tap-highlight.jpg)

按钮默认样式（上），添加appearance：none效果（下）：

![](images\normal.jpg)

长按右键菜单：

![](images\rightmenu.jpg)

### 5. 移动端常见布局

#### 1. 移动端单独制作

+ 流式布局（百分比布局）
+ flex 弹性布局（强烈推荐）
+ less+rem+媒体查询布局
+ 混合布局

#### 2. 响应式

+ 媒体查询
+ bootstarp

#### 3. 流式布局：

流式布局，就是百分比布局，也称非固定像素布局。

通过盒子的宽度设置成百分比来根据屏幕的宽度来进行伸缩，不受固定像素的限制，内容向两侧填充。

流式布局方式是移动web开发使用的比较常见的布局方式。

代码：

```html
   <style>
        * {
            margin: 0;
            padding: 0;
        }
        
        section {
            width: 100%;
            max-width: 980px;
            min-width: 320px;
            margin: 0 auto;
        }
        
        section div {
            float: left;
            width: 50%;
            height: 400px;
        }
        
        section div:nth-child(1) {
            background-color: pink;
        }
        
        section div:nth-child(2) {
            background-color: purple;
        }
    </style>
</head>

<body>
    <section>
        <div></div>
        <div></div>
    </section>
</body>
```

效果：

![](images\liushi.gif)



### 6. 京东移动端首页

#### 6.1准备工作

1. 技术选型

   方案：我们采取单独制作移动页面

   方案技术：布局采取流式布局

2. 搭建相关文件夹结构

   ![](images\construc.png)

3. 设置视口标签以及引入初始化样式

   ```html
   <meta name="viewport" content="width=device-width, user-scalable=no,        
      initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
     <link rel="stylesheet" href="css/normalize.css"> <!-- 引入我们的css初始化文件 -->
     <link rel="stylesheet" href="css/index.css"><!-- 引入我们首页的css -->
   ```

   css中新建normalize.css

   css中新建index.css

#### 6.2 body设置

接下来我们先来处理一下body的整体设置。

代码：

```css
body {
    width:100%; /* body的宽度与浏览器保持一致*/
    margin: 0 auto; /* 页面最大宽度是640px，如果在比较大的手机上显示，显示不完全，居中显示 */
    min-width: 320px;  /* 目前市面上最小手机分辨率为320 */
    max-width: 640px;  /*经过测量*/
    background: #fff;
    font-size: 14px;
    font-family: -apple-system, Helvetica, sans-serif;
    line-height: 1.5;
    color: #666;
}
```

总结：流式布局，百分比布局，只能处理宽度百分比：width：xx%。 

​	    高度没有办法确定，所以只能固定，height：xxpx；

#### 6.3 顶部app设置

效果：

![](images\jd01.jpg)

结构代码：

```
<body>
    <!-- 顶部 -->
    <header class="app">
        <ul>
            <li>8
            </li>
            <li>10
            </li>
            <li>57</li>
            <li>25</li>
        </ul>
    </header>
 </body>
```

样式代码：

```css
ul {
    margin: 0;
    padding: 0;
    list-style: none;
}
.app {
    height: 45px;
}

.app ul li {
    float: left;
    height: 45px;
    line-height: 45px;
    background-color: #333333;
}

.app ul li:nth-child(1) {
    width: 8%;
}
.app ul li:nth-child(2) {
    width: 10%;
}
.app ul li:nth-child(3) {
    width: 57%;
}
.app ul li:nth-child(4) {
    width: 25%;
    background-color: #F63515;
}
```

#### 6.4 app内容填充

结构代码：

```html
<!-- 顶部 -->
    <header class="app">
        <ul>
            <li>
                <img src="images/close.png" alt="">
            </li>
            <li>
                <img src="images/logo.png" alt="">
            </li>
            <li>打开京东App，购物更轻松</li>
            <li>立即打开</li>
        </ul>
    </header>
```

css样式：

```css
.app ul li:nth-child(1) img {
    width: 10px; /*图片大小固定死*/
}
.app ul li:nth-child(2) img {
    width: 30px;
    vertical-align: middle; /*文字和图片默认基线对齐，需要改为middle*/
}

.app ul li {
    float: left;
    height: 45px;
    line-height: 45px; /* 垂直居中 */
    background-color: #333333;
    text-align: center; /* 水平居中 */
    color: #fff;/* 颜色 */
}
```

#### 6.5 搜索模块

搜索模块效果：

![](images\jd02.jpg)

说明： 中间search模块是随着浏览器宽度变化，两边的内容是固定的。

结构代码：

```
    <!-- 搜索 -->
    <div class="search-wrap">
        <div class="search-btn"></div>
        <div class="search"> </div>
        <div class="search-login"> </div>
    </div>
```

样式代码：

```css
/* 搜索 */

.search-wrap {
    position: fixed;
    overflow: hidden;
    height: 44px;
}

.search-btn {
    position: absolute;
    top: 0;
    left: 0;
    background-color:pink;
    width: 40px;
    height: 44px;
}
.search-login {
    position: absolute;
    right: 0;
    top: 0;
    width: 40px;
    height: 44px;
    background-color:purple;
}

.search {
    height: 30px;
    background-color: #fff;
    margin: 0 50px;
    border-radius: 15px;
    margin-top:7px;
}
body{
   	backround-color:#ccc; /*临时给的*/ 
}
```

最终效果：

![](images\jd03.jpg)

**问题**：

搜索模块是固定定位，那么固定应该脱离标准流，以浏览器左上角为参照进行定位，那么搜索模块为啥不会盖住app模块？

这里跟固定定位的一个特点有关系：

如果固定定位的top不是0px，那么就以浏览器左上角为参照开始偏移。

如果固定定位的top是0px，那么他会在当前位置脱离标准流，并不会覆盖前边的盒子，而后边的盒子会顶上来。

#### 6.6 搜索模块内容填充

结构：

```html
    <!-- 搜索 -->
    <div class="search-wrap">
        <div class="search-btn"></div>
        <div class="search">
            <div class="jd-icon"></div>
        </div>
        <div class="search-login">登陆</div>
    </div>
```

样式：

```css
.search-btn::before {
    content: "";
    display: block;
    width: 20px;
    height: 18px;
    background: url(../images/s-btn.png) no-repeat;
    background-size: 20px 18px;
    margin: 14px 0 0 15px;
}
.search-login { 
    color: #fff;
    line-height: 44px;
    background-color:purple；/*去掉*/
}
.search-btn {
    background-color:pink; /*去掉*/
}

.jd-icon {
    width: 20px;
    height: 15px;
    position: absolute;
    top: 8px;
    left: 13px;
    background: url(../images/jd.png) no-repeat;
    background-size: 20px 15px;
}

.jd-icon::after {
    content: "";
    position: absolute;
    right: -8px;
    top: 0;
    display: block;
    width: 1px;
    height: 15px;
    background-color: #ccc;
}
```

最终效果：

![](images\jd04.jpg)

#### 6.7 二倍精灵图的做法

做法：

- 在firework里面把精灵图等比例缩放为原来的一半
- 之后根据大小 测量坐标
-  注意代码里面background-size也要写： 精灵图原来宽度的一半

结构：

```html
    <!-- 搜索 -->
    <div class="search-wrap">
        <div class="search-btn"></div>
        <div class="search">
            <div class="jd-icon"></div>
            <div class="sou"></div>     <!-- 增加 -->
        </div>
        <div class="search-login">登陆</div>
    </div>
```

样式：

```css
.sou {
    position: absolute;
    top: 8px;
    left: 50px;
    width: 18px;
    height: 15px;
    background: url(../images/jd-sprites.png) no-repeat -81px 0;
    background-size: 200px auto;
}

```

#### 6.8 焦点图制作

结构：

```html
    <!-- 主体内容部分 -->
    <div class="main-content">
        <!-- 滑动图 -->
        <div class="slider">
            <img src="upload/banner.dpg" alt="">
        </div>
	</div>
```

样式：

```css
.slider img {
    width: 100%;/*图片本身比较大，所以需要设置一下*/
}

.search-wrap {
    position: fixed;  /*相对定位改为固定定位*/
    overflow: hidden;
    width: 100%;   /*增加宽度，加了固定定位的盒子必须要有宽度*/
    height: 44px;
    min-width: 320px; /*增加最大宽度，最小宽度*/
    max-width: 640px;
}
```

效果：

![](images\jd06.jpg)

轮播图我们暂时只能处理一张图片，因为想处理多张并且能够自动轮播，这是需要使用js的。

#### 6.9 品牌日

品牌日如下图：

![](images\jd07.jpg)

分析如下：

![](images\jd08.jpg)

这里不是一张图片，而是三张，因为每个图片点击之后，跳转链接不一致。

结构：

```html
        <!-- 蔡康永品牌日 -->
        <div class="brand">
            <div>
                <a href="#">
                    <img src="upload/pic1.dpg" alt="">
                </a>
            </div>
            <div>
                <a href="#">
                    <img src="upload/pic2.dpg" alt="">
                </a>

            </div>
            <div>
                <a href="#">
                    <img src="upload/pic3.dpg" alt="">
                </a>

            </div>
        </div>
```

样式：

```css
/* 品牌日 */

.brand {
    overflow: hidden;
    border-radius: 10px 10px 0 0;
}

.brand div {
    float: left;
    width: 33.33%;
}

.brand div img {
    width: 100%;
}
img {
    vertical-align: top; /*去除图片之间垂直的空隙*/
}
```

效果：

![](images\jd09.jpg)



#### 6.10 导航栏nav

##### 1. 品牌日修改

先调整一下品牌日的图片：

结构：修改一下图片即可，样式不需要修改

```html
        <!-- 小家电品牌日 -->
        <div class="brand">
            <div>
                <a href="#">
                    <img src="upload/pic11.dpg" alt="">
                </a>
            </div>
            <div>
                <a href="#">
                    <img src="upload/pic22.dpg" alt="">
                </a>

            </div>
            <div>
                <a href="#">
                    <img src="upload/pic33.dpg" alt="">
                </a>

            </div>
        </div>
```

效果：调整之后的图片颜色风格与即将要处理的内容风格一致。

![](images\jd10.jpg)

##### 2. 导航栏nav

效果如下：

![](images\jd11.jpg)

京东采用的图片技术：

![](images\jd12.jpg)

结构：

```html
 <!-- nav部分 -->
        <nav class="clearfix">
            <a href="">
                <img src="upload/nav1.webp" alt="">
                <span>京东超市</span>
            </a>

            <a href="">
                <img src="upload/nav2.webp" alt="">
                <span>京东超市</span>
            </a>

            <a href="">
                <img src="upload/nav1.webp" alt="">
                <span>京东超市</span>
            </a>

            <a href="">
                <img src="upload/nav1.webp" alt="">
                <span>京东超市</span>
            </a>

            <a href="">
                <img src="upload/nav1.webp" alt="">
                <span>京东超市</span>
            </a>

            <a href="">
                <img src="upload/nav3.webp" alt="">
                <span>京东超市</span>
            </a>

            <a href="">
                <img src="upload/nav1.webp" alt="">
                <span>京东超市</span>
            </a>

            <a href="">
                <img src="upload/nav1.webp" alt="">
                <span>京东超市</span>
            </a>

            <a href="">
                <img src="upload/nav1.webp" alt="">
                <span>京东超市</span>
            </a>

            <a href="">
                <img src="upload/nav1.webp" alt="">
                <span>京东超市</span>
            </a>

        </nav>
```

样式：

```css
/* nav */

nav {
    padding-top: 5px;
}

nav a {
    float: left;
    width: 20%;
    text-align: center;
}

nav a img {
    width: 40px;
    margin: 10px 0;
}

nav a span {
    display: block;
}

a {
    color: #666;
    text-decoration: none;
}
body{
    height:2000px;/*这个body的高度临时给的，为了看导航方便*/
}

```

效果：

![](images\jd13.jpg)

#### 6.11 新闻快报

分析如下：京东快报，我们不处理右侧的文字了，只处理下方的图片

![](images\jd14.jpg)

结构：

```html
        <!-- 新闻模块 -->
        <div class="news">
            <a href="#">
                <img src="upload/new1.dpg" alt="">
            </a>
            <a href="#">
                <img src="upload/new2.dpg" alt="">

            </a>
            <a href="#">
                <img src="upload/new3.dpg" alt="">

            </a>
        </div>
```

样式：

```css
/* news */

.news {
    margin-top: 20px;
}

.news img {
    width: 100%;
}

.news a {
    float: left;
    box-sizing: border-box;
}

.news a:nth-child(1) {
    width: 50%;
}


/* .news a:nth-child(2),
.news a:nth-child(3),
{
    width: 25%;
} */
/* .news a:nth-child(3) {
    width: 25%;
} */


/* n+2 就是从从2个往后面选 */

.news a:nth-child(n+2) {
    width: 25%;
    border-left: 1px solid #ccc; /*图片之间有竖线*/
}



```

效果：

![](images\jd15.jpg)











#### 6.12 最终

1. 问题1：左上角的小叉号的问题

![](images\jd-went-01.jpg)

修复代码：

```css
img {
    vertical-align: middle; /*改为中间*/
}

```

2. body测试样式删除，删除一下两条样式：

```
body{
    background-color:#ccc;
    height:2000px;
    
}
```

3. 移动端特殊样式：

```css
/*点击高亮我们需要清除清除  设置为transparent 完成透明*/

* {
    -webkit-tap-highlight-color: transparent;
}


/*在移动端浏览器默认的外观在iOS上加上这个属性才能给按钮和输入框自定义样式*/

input {
    -webkit-appearance: none;
}


/*禁用长按页面时的弹出菜单*/

img,
a {
    -webkit-touch-callout: none;
}
```

4. 最终效果：

![](images\jd16.jpg)




























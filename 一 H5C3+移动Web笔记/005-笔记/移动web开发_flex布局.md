# 移动web开发——flex布局

## 1. 传统布局和flex布局对比

### 1.1传统布局

+ 兼容性好
+ 布局繁琐
+ 局限性，不能再移动端很好的布局

### 1.2 flex布局

+ 操作方便，布局极其简单，移动端使用比较广泛
+ pc端浏览器支持情况比较差
+ IE11或更低版本不支持flex或仅支持部分

### 1.3 建议

+  如果是pc端页面布局，还是采用传统方式
+  如果是移动端或者是不考虑兼容的pc则采用flex

### 1.4 初体验

效果：

![](images\flex01.jpg)

代码： 有很多代码看不懂，没关系，接下来我们会慢慢学习。

```html
   <style>
        div {
            display: flex; /*flex布局，使得span可以添加大小，等等*/
            width: 80%;
            height: 300px;
            background-color: pink;
            justify-content: space-around; /*水平平均分布显示*/
        }
        
        div span {
            /* width: 150px; */
            height: 100px;
            background-color: purple;
            margin-right: 5px;
            flex: 1;/*三等份 ,根据屏幕自适应*/
        }
    </style>
</head>

<body>
    <div>
        <span>1</span>
        <span>2</span>
        <span>3</span>
    </div>
</body>
```

代码效果：

![](images\flex02.jpg)

## 2. flex布局原理

+ flex 是 flexible Box 的缩写，意为"弹性布局"，用来为盒状模型提供最大的灵活性，任何一个容器都可以指定为 flex 布局。
+ 当我们为父盒子设为 flex 布局以后，子元素的 float、clear 和 vertical-align 属性将失效。
  + 因为flex布局可以让子元素一行显示，不需要浮动，所以就不需要清除浮动
  + flex布局还可以设置盒子垂直居中，之前只能设置水平居中。
+ flex布局又叫伸缩布局 、弹性布局 、伸缩盒布局 、弹性盒布局 
+ 采用 Flex 布局的元素，称为 Flex 容器（flex container），简称"容器"。
+ 它的所有子元素自动成为容器成员，称为 Flex 项目（flex item），简称"项目"。

- **总结**：**就是通过给父盒子添加display:flex属性，来控制子盒子的位置和排列方式** 


## **3. 父项常见属性**

### 3.0 介绍

+ flex-direction：设置主轴的方向 （direction：方向）
+ justify-content：设置主轴上的子元素排列方式 （justify： [ˈdʒʌstɪfaɪ] ，证明..有理。content：内容）
+ flex-wrap：设置子元素是否换行  
+ align-content：设置侧轴上的子元素的排列方式（多行）
+ align-items：设置侧轴上的子元素排列方式（单行）
+ flex-flow：复合属性，相当于同时设置了 flex-direction 和 flex-wrap

### 3.1 flex-direction设置主轴的方向

+ 在 flex 布局中，是分为主轴和侧轴两个方向，同样的叫法有 ： 行和列、x 轴和y 轴
+ 默认主轴方向就是 x 轴方向，水平向右
+ 默认侧轴方向就是 y 轴方向，水平向下

<img src="images/1.jpg">

+ 注意： 主轴和侧轴是会变化的，就看 flex-direction 设置谁为主轴，剩下的就是侧轴。而我们的子元素是跟着主轴来排列的

+ flex-direction可以设置的值：

  <img src="images/2.jpg">

  ​

代码：

```html
    <style>
        div {
            /* 给父级添加flex属性 */
            display: flex;
            width: 800px;
            height: 300px;
            background-color: pink;
            /* 默认的主轴是 x 轴 行 row  那么y轴就是侧轴喽 */
            /* 我们的元素是跟着主轴来排列的 */
            /* flex-direction: row; */
            /* 简单了解 翻转 */
            /* flex-direction: row-reverse; */
            /* 我们可以把我们的主轴设置为 y轴 那么 x 轴就成了侧轴 */
            flex-direction: column;
        }
        
        div span {
            width: 150px;
            height: 100px;
            background-color: purple;
        }
    </style>
</head>

<body>
    <div>
        <span>1</span>
        <span>2</span>
        <span>3</span>
    </div>
</body>
```

效果：

主轴为x-正方向：row

![](images\flex04.jpg)

主轴为x-反方向：row-reverse

![](images\flex03.jpg)

主轴为y-正方向：column

![](images\flex05.jpg)



### 3.2 justify-content 设置主轴上的子元素排列方式

#### 1. 介绍

- justify-content 属性定义了**项目在主轴上的对齐方式**（项目就是子元素）
- 注意： 使用这个属性之前一定要确定好主轴是哪个

- 属性值如下：

| 属性值                                               | 说明                                         |
| ---------------------------------------------------- | -------------------------------------------- |
| **flex-start** （start：开始）                       | 默认值 从头部开始  如果主轴是x轴，则从左到右 |
| flex-end （end：结束）                               | 从尾部开始排列                               |
| **center** （center：中间）                          | 在主轴居中对齐（如果主轴是x轴则 水平居中）   |
| **space-around** （空间-周围：周围空间一致（平分）） | 平分剩余空间                                 |
| **space-between**（空间-中间）                       | 先两边贴边 再平分剩余空间（**重要**）        |

#### 2. x主轴-例子

代码：

```html
    <style>
        div {
            display: flex;
            width: 800px;
            height: 300px;
            background-color: pink;
            /* 默认的主轴是 x 轴 row */
            flex-direction: row;
            /* justify-content: 是设置主轴上子元素的排列方式 */
            /* justify-content: flex-start; */
            /* justify-content: flex-end; */
            /* 让我们子元素居中对齐 */
            /* justify-content: center; */
            /* 平分剩余空间 */
            /* justify-content: space-around; */
            /* 先两边贴边， 在分配剩余的空间 */
            justify-content: space-between;
        }
        
        div span {
            width: 150px;
            height: 100px;
            background-color: purple;
        }
    </style>
</head>

<body>
    <div>
        <span>1</span>
        <span>2</span>
        <span>3</span>
        <span>4</span>
    </div>
</body>

```

效果：

justify-content: flex-start：

![](images\flex06.jpg)

justify-content: flex-end：

![](images\flex07.jpg)

**总结**：

flex-direction：row；justify-content: flex-start： ----  左1234（开始位置1234）

flex-direction：row；justify-content: flex-end： ----右1234（结束位置1234）

flex-start和flex-end，只是改变起始位置，排列的顺序不变



flex-direction：row-reverse；justify-content: flex-start： ---- 右4321（ 与 第一个翻转）

flex-direction：row-reverse；justify-content: flex-end： ---- 左4321 （与 第二个翻转）

row-reverse 与 row ， 正好相反，位置相反，顺序相反



justify-content: center：

![](images\flex08.jpg)

justify-content: space-around：

![](images\flex09.jpg)

![](images\flex10.jpg)

 justify-content: space-between：

![](images\flex11.jpg)

#### 3. y主轴-例子

代码：我们直分析两个，其他自己看一下即可。

```html
  <style>
        div {
            display: flex;
            width: 800px;
            height: 400px;
            background-color: pink;
            /* 我们现在的主轴是y轴 */
            flex-direction: column;
            /* justify-content: center; */
            justify-content: space-between;
        }
        
        div span {
            width: 150px;
            height: 100px;
            background-color: purple;
        }
    </style>
</head>

<body>
    <div>
        <span>1</span>
        <span>2</span>
        <span>3</span>
    </div>
</body>
```

效果：

justify-content: center：

![](images\flex12.jpg)

justify-content: space-between：

![](images\flex13.jpg)



### 3.3 flex-wrap设置是否换行

+ 默认情况下，项目都排在一条线（又称”轴线”）上。flex-wrap属性定义，flex布局中默认是不换行的。
+ nowrap 不换行
+ wrap 换行

代码：

```html
    <style>
        div {
            display: flex;
            width: 600px;
            height: 400px;
            background-color: pink;
            /* flex布局中，默认的子元素是不换行的， 如果装不开，会缩小子元素的宽度，放到父元素里面  */
            /* flex-wrap: nowrap; */
            flex-wrap: wrap;
        }
        
        div span {
            width: 150px;
            height: 100px;
            background-color: purple;
            color: #fff;
            margin: 10px;
        }
    </style>
</head>

<body>
    <div>
        <span>1</span>
        <span>2</span>
        <span>3</span>
        <span>4</span>
        <span>5</span>
    </div>
</body>
```

效果：

flex-wrap: nowrap：不换行效果：如果装不开，会缩小子元素的宽度，放到父元素里面

![](images\flex14.jpg)

 flex-wrap: wrap：换行效果：

![](images\flex15.jpg)

### 3.4 align-items 设置侧轴上的子元素排列方式（单行 ）

+ 该属性是控制子项在侧轴（默认是y轴）上的排列方式  在**子项为单项（单行）的时候使用**

+ 该属性在控制盒子水平居中和垂直居中时使用

  ![](images\flex16.jpg)

+ flex-start 从头部开始

+ flex-end 从尾部开始

+ center 居中显示

+ stretch 拉伸   （[stretʃ ] : 拉伸)

代码：

```html
   <style>
        div {
            display: flex;
            width: 800px;
            height: 400px;
            background-color: pink;
            /* 默认的主轴是 x 轴 row */
            /* flex-direction: column; */
            justify-content: center;
            /* 我们需要一个侧轴居中 */
            /* 拉伸，但是子盒子不要给高度 */
            /* align-items: stretch; */
            align-items: center;
        }
        
        div span {
            width: 150px;
            height: 100px;
            background-color: purple;
            color: #fff;
            margin: 10px;
        }
    </style>
</head>

<body>
    <div>
        <span>1</span>
        <span>2</span>
        <span>3</span>
    </div>
</body>
```

效果：

默认x主轴时 -居中：justify-content: center; align-items: center;

![](images\flex17.jpg)

y主轴时 - 居中：flex-direction: column;justify-content: center; align-items: center;

![](images\flex19.jpg)

x主轴时-侧轴拉伸：justify-content: center; align-items: stretch ;

![](images\flex18.jpg)



### 3.5 align-content  设置侧轴上的子元素的排列方式（多行）

设置子项在侧轴上的排列方式 并且只能用于**子项出现 换行 的情况（多行）**，在单行下是没有效果的。

<img src="images/4.jpg">

代码：

注意：

我们需要多添加几个元素，然后换行： flex-wrap: wrap; *

 因为有了换行，此时我们侧轴上控制子元素的对齐方式我们用 align-content 

```html
  <style>
        div {
            display: flex;
            width: 800px;
            height: 400px;
            background-color: pink;
            /* 换行 */
            flex-wrap: wrap;
            /* 因为有了换行，此时我们侧轴上控制子元素的对齐方式我们用 align-content */
            /* align-content: flex-start; */
            /* align-content: center; */
            /* align-content: space-between; */
            align-content: space-around;
        }
        
        div span {
            width: 150px;
            height: 100px;
            background-color: purple;
            color: #fff;
            margin: 10px;
        }
    </style>
</head>

<body>
    <div>
        <span>1</span>
        <span>2</span>
        <span>3</span>
        <span>4</span>
        <span>5</span>
        <span>6</span>
    </div>
</body>
```

效果：

 flex-wrap: wrap;

![](images\align-content01.jpg)

 flex-wrap: wrap; align-content: flex-start;

![](images\align-content02.jpg)

 flex-wrap: wrap; align-content: center;

![](images\align-content03.jpg)

 flex-wrap: wrap; align-content: space-between; 在侧轴先分布两头，再平均

![](images\align-content04.jpg)

 flex-wrap: wrap; align-content: space-around; 在侧轴平分

![](images\align-content05.jpg)

### 3.6 align-content 和align-items区别

+ align-items  适用于单行情况下， 只有上对齐、下对齐、居中和 拉伸
+ align-content适应于换行（多行）的情况下（单行情况下无效）， 可以设置 上对齐、下对齐、居中、拉伸以及平均分配剩余空间等属性值。 
+ 总结：**单行找align-items  多行找 align-content**

### 3.7 flex-flow 属性是 flex-direction 和 flex-wrap 属性的复合属性

```css
flex-flow:row wrap; /*x主轴，换行 */
```

### 3.8 复习：

- flex-direction：设置主轴的方向
- justify-content：设置主轴上的子元素排列方式
- flex-wrap：设置子元素是否换行  
- align-content：设置侧轴上的子元素的排列方式（多行）
- align-items：设置侧轴上的子元素排列方式（单行）
- flex-flow：复合属性，相当于同时设置了 flex-direction 和 flex-wrap

## 4. flex布局子项常见属性

+ flex子项目占的份数
+ align-self控制子项自己在侧轴的排列方式
+ order属性定义子项的排列顺序（前后顺序）

### 4.1  flex 属性

flex 属性定义子项目分配剩余空间，用flex来表示占多少份数。

```
.item {
    flex: <number>; /* 默认值 0 */
}

```

分配剩余空间-例子：

```
  <style>
      section {
            display: flex;
            width: 60%;
            height: 150px;
            background-color: pink;
            margin: 0 auto;
        }
        
        section div:nth-child(1) {
            width: 100px;
            flex:1;
            height: 150px;
            background-color: red;
        }
        
        section div:nth-child(2) {
            flex: 1;
            background-color: green;
        }
        
        section div:nth-child(3) {
            width: 100px;
            height: 150px;
            background-color: blue;
        }
</style>
<body>
    <section>
        <div></div>
        <div></div>
        <div></div>
    </section>
</body>
```

效果：

![](images\flex20.jpg)

占多少份代码：

```
 <style>
 	  p {
            display: flex;
            width: 60%;
            height: 150px;
            background-color: pink;
            margin: 100px auto;
        }
        
        p span {
            flex: 1;
        }
        
        p span:nth-child(2) {
            flex: 2;
            background-color: purple;
        }
    </style>
    <body>
    <p>
        <span>1</span>
        <span>2</span>
        <span>3</span>
    </p>
</body>
```

效果：

![](images\flex21.jpg)

### 4.2 align-self控制子项自己在侧轴上的排列方式

align-self 属性允许单个项目有与其他项目不一样的对齐方式，可覆盖 align-items 属性。

默认值为 auto，表示继承父元素的 align-items 属性，如果没有父元素，则等同于 stretch。

````
span:nth-child(2) {
      /* 设置自己在侧轴上的排列方式 */
      align-self: flex-end;
}

````

总结：align-items是控制素有的子项，而align-self是控制单个子项

代码：

```html
   <style>
        div {
            display: flex;
            width: 80%;
            height: 300px;
            background-color: pink;
            /* 让三个子盒子沿着侧轴底侧对齐 */
            /* align-items: flex-end; */
           
        }
        
        div span {
            width: 150px;
            height: 100px;
            background-color: purple;
            margin-right: 5px;
        }
        
        div span:nth-child(3) {
             /* 我们想只让3号盒子下来底侧 */
            align-self: flex-end;
        }
    </style>
</head>

<body>
    <div>
        <span>1</span>
        <span>2</span>
        <span>3</span>
    </div>
</body>
```

效果：

![](images\flex31.jpg)

### 4.3 order 属性定义项目的排列顺序

数值越小，排列越靠前，默认为0。

注意：和 z-index 不一样。

```
.item {
    order: <number>;
}
```

代码：

```
    <style>
        div {
            display: flex;
            width: 80%;
            height: 300px;
            background-color: pink;
        }
        
        div span {
            width: 150px;
            height: 100px;
            background-color: purple;
            margin-right: 5px;
        }
            
        div span:nth-child(2) {
            /* 默认是0   -1比0小所以在前面 */
            order: -1;
        }
        div span:nth-child(3) {
            align-self: flex-end;
        }
    </style>
</head>

<body>
    <div>
        <span>1</span>
        <span>2</span>
        <span>3</span>
    </div>
</body>
```

效果：

![](images\flex32.jpg)

## 5. 携程网首页案例制作

### 5.0准备工作

携程网链接：http://m.ctrip.com

效果：

![](images\xc01.jpg)

1.技术选型

- 方案：我们采取单独制作移动页面方案

- 技术：布局采取flex布局


2.搭建相关文件夹

<img src="images/5.jpg">

3.设置视口标签以及引入初始化样式

```html
<meta name="viewport" content="width=device-width, user-scalable=no,initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">

<link rel="stylesheet" href="css/normalize.css">
<link rel="stylesheet" href="css/index.css">
```

4.常用初始化样式

```css
body {
  max-width: 540px; /*经过测量*/
  min-width: 320px; /*移动端一般最小宽度都是320*/
  margin: 0 auto;
  font: normal 14px/1.5 Tahoma,"Lucida Grande",Verdana,"Microsoft Yahei",STXihei,hei;
  color: #000;
  background: #f2f2f2;
  overflow-x: hidden;
  -webkit-tap-highlight-color: transparent;
}

```

给body暂时添加123，看效果：

![](images\xc02.jpg)

### 5.1 首页布局分析&搜索模块

#### 1. 模块名字划分

<img src="images/6.jpg">

每一个模块的宽度是自适应的，但是高度都是固定的

#### 2. 搜索模块

结构：

```html
<!-- 顶部搜索 -->
<div class="search-index">
</div>
```

样式：

```css
/* 搜索模块 */
.search-index {
    /* 固定定位跟父级没有关系 它以屏幕为准 */
    position: fixed;
    top: 0;
    left: 50%;
    -webkit-transform: translateX(-50%);
    transform: translateX(-50%);
 	/* 固定的盒子应该有宽度 */
    width: 100%;
    min-width: 320px;
    max-width: 540px;
    height: 44px;
    background-color: pink; 
}
```

效果：

![](images\xc03.jpg)

### 5.2  搜索模块 - user

分析： 右侧的我的模块的宽高是固定的（经过拖拽发现宽高都是44）

![](images\xc04.jpg)



结构：

```html
<!-- 顶部搜索 -->
<div class="search-index">
    <div class="search">搜索:目的地/酒店/景点/航班号</div>
    <a href="#" class="user">我 的</a>
</div>
```

样式：

```css
.search {
    flex: 1;
}
.user {
    width: 44px;
    height: 44px;
    background-color: purple; 
    font-size: 12px;
    text-align: center;
    color: #2eaae0;
}
.user::before {
    content: "";
    display: block;
    width: 23px;
    height: 23px;
    background: url(../images/sprite.png) no-repeat -59px -194px;
    background-size: 104px auto;
    margin: 4px auto -2px;
}
.search-index{
    display:flex;/*增加*/
}

a {
    text-decoration: none;
}
```

效果：

![](images\xc05.jpg)

### 5.3 搜索模块 - search

结构：

```html
<!-- 顶部搜索 -->
<div class="search-index">
    <div class="search">搜索:目的地/酒店/景点/航班号</div>
    <a href="#" class="user">我 的</a>
</div>
```

样式：

```css
div { /*我们界面会有大量的div，增加padding和border，所以直接使用box-sizing自动处理*/
    box-sizing: border-box;
}
.search-index { /*修改*/
    /* background-color: pink; */
    background-color: #F6F6F6;
    border-top: 1px solid #ccc;
    border-bottom: 1px solid #ccc;
}
.search {
    position: relative;
    height: 26px;
    line-height: 24px; /*因为css3中的盒子模型是包含了边框，26px不是我们想要的行高，应该减去边框*/
    border: 1px solid #ccc;
    flex: 1;
    font-size: 12px;
    color: #666;
    margin: 7px 10px;
    padding-left: 25px;
    border-radius: 5px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, .2);
}

.search::before {
    content: "";
    position: absolute;
    top: 5px;
    left: 5px;
    width: 15px;
    height: 15px;
    background: url(../images/sprite.png) no-repeat -59px -279px;
    background-size: 104px auto;
}
.user::before {
    margin: 4px auto -2px; /*修改*/
}
```

效果：

![](images\xc07.jpg)

### 5.4 焦点图focus模块制作

结构：

```html
<!-- 焦点图模块 -->
<div class="focus">
    <img src="upload/focus.jpg" alt="">
</div>
```

样式：

```css
/* focus */

.focus {
    padding-top: 44px;
}
.focus img {
    width: 100%;
}
```

效果：

![](images\xc08.jpg)

###  5.5 local-nav布局

local-nav，本地导航，如下：

![](images\xc09.jpg)

结构：

```html
<!-- 局部导航栏 -->
<ul class="local-nav">
    <li>1</li>
    <li>2</li>
    <li>3</li>
    <li>4</li>
    <li>5</li>
</ul>
```

样式：

```css
/* local-nav */

.local-nav {
    display: flex;
    height: 64px;
    margin: 3px 4px;
    background-color: #fff;
    border-radius: 8px;
}

.local-nav li {
    flex: 1;
}
ul {
    list-style: none;
    margin: 0;
    padding: 0;
}
```

效果：

![](images\xc10.jpg)



### 5.6 local-nav内容制作

导航内容如下：

![](images\xc09.jpg)

结构：

```html
 <!-- 局部导航栏 -->
    <ul class="local-nav">
        <li>
            <a href="#" title="景点·玩乐">
                <span class="local-nav-icon"></span>
                <span>景点·玩乐</span>
            </a>
        </li>
        <li>
            <a href="#" title="景点·玩乐">
                <span class="local-nav-icon"></span>
                <span>景点·玩乐</span>
            </a>
        </li>
        <li>
            <a href="#" title="景点·玩乐">
                <span class="local-nav-icon"></span>
                <span>景点·玩乐</span>
            </a>
        </li>
        <li>
            <a href="#" title="景点·玩乐">
                <span class="local-nav-icon"></span>
                <span>景点·玩乐</span>
            </a>
        </li>
        <li>
            <a href="#" title="景点·玩乐">
                <span class="local-nav-icon"></span>
                <span>景点·玩乐</span>
            </a>
        </li>

    </ul>
```

样式：

```css
.local-nav a {
    display: flex;
    flex-direction: column;
    /* 侧轴居中对齐 因为是单行 */
    align-items: center;
    font-size: 12px;
}
.local-nav-icon {
    width: 32px;
    height: 32px;
    background-color: pink;
    margin-top: 8px;
    background: url(../images/localnav_bg.png) no-repeat 0 0;
    background-size: 32px auto;
}
a {
    text-decoration: none;
    color: #222; /*增加*/
}
```

效果：

![](images\xc11.jpg)

### 5.7 利用属性选择器更换背景图片

我们来处理 local-nav 导航图片切换。

结构： 将第一个span的样式，修改一下，增加不同的后缀

```html
 <!-- 局部导航栏 -->
    <ul class="local-nav">
        <li>
            <a href="#" title="景点·玩乐">
                <span class="local-nav-icon-icon1"></span>
                <span>景点·玩乐</span>
            </a>
        </li>
        <li>
            <a href="#" title="景点·玩乐">
                <span class="local-nav-icon-icon2"></span>
                <span>景点·玩乐</span>
            </a>
        </li>
        <li>
            <a href="#" title="景点·玩乐">
                <span class="local-nav-icon-icon3"></span>
                <span>景点·玩乐</span>
            </a>
        </li>
        <li>
            <a href="#" title="景点·玩乐">
                <span class="local-nav-icon-icon4"></span>
                <span>景点·玩乐</span>
            </a>
        </li>
        <li>
            <a href="#" title="景点·玩乐">
                <span class="local-nav-icon-icon5"></span>
                <span>景点·玩乐</span>
            </a>
        </li>

    </ul>
```

样式： 我们处理图片的时候，采用属性选择器先统一设置一下相同的样式，然后在单独设置背景位置

```css
.local-nav li [class^="local-nav-icon"] {
    width: 32px;
    height: 32px;
    background-color: pink;
    margin-top: 8px;
    background: url(../images/localnav_bg.png) no-repeat 0 0;
    background-size: 32px auto;
}

.local-nav li .local-nav-icon-icon2 {
    background-position: 0 -32px;
}

.local-nav li .local-nav-icon-icon3 {
    background-position: 0 -64px;
}

.local-nav li .local-nav-icon-icon4 {
    background-position: 0 -96px;
}

.local-nav li .local-nav-icon-icon5 {
    background-position: 0 -128px;
}
```

效果：

![](images\xc12.jpg)

### 5.8 nav外观布局

分析：

![](images\xc13.jpg)

结构：

```html
 <!-- 主导航栏 -->
    <nav>
        <div class="nav-common">
            <div class="nav-items">a</div>
            <div class="nav-items">b</div>
            <div class="nav-items">c</div>
        </div>
        <div class="nav-common">2</div>
        <div class="nav-common">3</div>

    </nav>
```

样式：

```css
/* nav */
nav {
    overflow: hidden;
    border-radius: 8px;
    margin: 0 4px 3px;
}
.nav-common {
    display: flex;
    height: 88px;
    background-color: pink;
}
.nav-common:nth-child(2) {
    margin: 3px 0;
}
.nav-items {
    flex: 1;
}
/* -n+2就是选择前面两个元素 
不能写成：2-n: - 不是减号，而是负号。
注意： n ， -n 写前边，-负号，代表反方向
*/
.nav-items:nth-child(-n+2) {
    border-right: 1px solid #fff;
}
```

效果：

![](images\xc14.jpg)

### 5.9 nav内容制作

结构：

```html
 <!-- 主导航栏 -->
    <nav>
        <div class="nav-common">
            <div class="nav-items">
                <a href="#">海外酒店</a>
            </div>
            <div class="nav-items">
                <a href="#">海外酒店</a>
                <a href="#">特价酒店</a>
            </div>
            <div class="nav-items">
                <a href="#">海外酒店</a>
                <a href="#">特价酒店</a>
            </div>
        </div>
        <div class="nav-common">
            <div class="nav-items">
                <a href="#">海外酒店</a>
            </div>
            <div class="nav-items">
                <a href="#">海外酒店</a>
                <a href="#">特价酒店</a>
            </div>
            <div class="nav-items">
                <a href="#">海外酒店</a>
                <a href="#">特价酒店</a>
            </div>
        </div>
        <div class="nav-common">
            <div class="nav-items">
                <a href="#">海外酒店</a>
            </div>
            <div class="nav-items">
                <a href="#">海外酒店</a>
                <a href="#">特价酒店</a>
            </div>
            <div class="nav-items">
                <a href="#">海外酒店</a>
                <a href="#">特价酒店</a>
            </div>
        </div>

    </nav>
```

样式：

```css
.nav-items {
    /* 不冲突的：自己可以作为flex布局的儿子，本身也可以是flex布局 */
    flex: 1;
    display: flex;
    flex-direction: column;
}

.nav-items a {
    flex: 1;
    text-align: center;
    line-height: 44px;
    color: #fff;
    font-size: 14px;
    /* 文字阴影 */
    text-shadow: 1px 1px rgba(0, 0, 0, .2);
}

.nav-items a:nth-child(1) {
    border-bottom: 1px solid #fff;
}

.nav-items:nth-child(1) a {
    border: 0;
    background: url(../images/hotel.png) no-repeat bottom center;
    background-size: 121px auto;
}

```

效果：

![](images\xc15.jpg)

### 5.10 背景渐变

#### 1.  介绍如下：

![](images\gb.jpg)

语法：

```css
background: linear-gradient(起始方向, 颜色1, 颜色2, ...);
background: -webkit-linear-gradient(left, red , blue);
background: -webkit-linear-gradient(left top, red , blue);
/* linear:线性，gradient： [ˈgreɪdiənt] 变化率，理解为渐变*/
```

注意：

- 背景渐变必须添加浏览器私有前缀
- 起始方向可以是： 方位名词  或者 度数 ， 如果省略默认就是 top

#### 2. 案例

代码：

```html
    <style>
        div {
            width: 600px;
            height: 200px;
            /* 背景渐变必须添加浏览器私有前缀 */
            /* background: -webkit-linear-gradient(left, red, blue); */
            /* background: -webkit-linear-gradient(red, blue); */
            background: -webkit-linear-gradient(top left, red, blue);
        }
    </style>
</head>

<body>
    <div></div>
</body>
```

效果：

![](images\gb02.jpg)

### 5.10 subnav-entry 侧导航入口

侧导航入口如下：

![](images\xc17.jpg)

结构：

```html
 <!-- 侧导航栏 -->
    <ul class="subnav-entry">
        <li>
            <a href="#">
                <span class="subnav-entry-icon"></span>
                <span>电话费</span>
            </a>
        </li>
        <li>
            <a href="#">
                <span class="subnav-entry-icon"></span>
                <span>电话费</span>
            </a>
        </li>
        <li>
            <a href="#">
                <span class="subnav-entry-icon"></span>
                <span>电话费</span>
            </a>
        </li>
        <li>
            <a href="#">
                <span class="subnav-entry-icon"></span>
                <span>电话费</span>
            </a>
        </li>
        <li>
            <a href="#">
                <span class="subnav-entry-icon"></span>
                <span>电话费</span>
            </a>
        </li>
        <li>
            <a href="#">
                <span class="subnav-entry-icon"></span>
                <span>电话费</span>
            </a>
        </li>
        <li>
            <a href="#">
                <span class="subnav-entry-icon"></span>
                <span>电话费</span>
            </a>
        </li>
        <li>
            <a href="#">
                <span class="subnav-entry-icon"></span>
                <span>电话费</span>
            </a>
        </li>
        <li>
            <a href="#">
                <span class="subnav-entry-icon"></span>
                <span>电话费</span>
            </a>
        </li>
        <li>
            <a href="#">
                <span class="subnav-entry-icon"></span>
                <span>电话费</span>
            </a>
        </li>

    </ul>
```

样式：

```css
/* subnav-entry */

.subnav-entry {
    display: flex;
    border-radius: 8px;
    background-color: #fff;
    margin: 0 4px;
    flex-wrap: wrap;
    padding: 5px 0;
}

.subnav-entry li {
    /* 里面的子盒子可以写 % 相对于父级来说的  注意：flex除了写数字，还可以写百分比 */
    flex: 20%;
}

.subnav-entry a {
    display: flex;
    flex-direction: column;
    align-items: center;
}

.subnav-entry-icon {
    width: 28px;
    height: 28px;
    background-color: pink;
    margin-top: 4px;
    background: url(../images/subnav-bg.png) no-repeat;
    background-size: 28px auto;
}
/*注意：这个subnav-bg图片的宽度为48，所以这里的28不是缩小了2倍，但是并不会影响太多
	   当然这里大家也可以修改为24px，但是前提是width和height也得是24px。
	   老师是直接参照携程的大小28来处理的。
*/
```

效果：

![](images\xc18.jpg)

### 5.11 热门活动模块制作

分析：

![](images\xc19.jpg)

结构：

```html
<!-- 销售模块 -->
    <div class="sales-box">
        <div class="sales-hd">
            <h2>热门活动</h2>
            <a href="#" >更多</a>
        </div>
    </div>
```

样式：

```css
/* sales-box */

.sales-box {
    border-top: 1px solid #bbb;
    background-color: #fff;
    margin: 4px;
}

.sales-hd {
    height: 44px;
    border-bottom: 1px solid #ccc;
}

.sales-hd h2 {
    position: relative;
    text-indent: -999px;
    overflow: hidden;
}

.sales-hd h2::after {
    position: absolute;
    top: 5px;
    left: 8px;
    content: "";
    width: 79px;
    height: 15px;
    background: url(../images/hot.png) no-repeat 0 -20px;
    background-size: 79px auto;
}
body{
    height:2000px;/*测试用*/
}
```

效果：

![](images\xc20.jpg)



### 5.12 更多福利模块

结构：

```html
    <!-- 销售模块 -->
    <div class="sales-box">
        <div class="sales-hd">
            <h2>热门活动</h2>
            <a href="#" class="more">获取更多福利</a>  <!-- 修改 -->
        </div>
	</div>
```

样式：

```css
.more {
    position: absolute;
    right: 5px;
    top: 0px;
    background: -webkit-linear-gradient(left, #FF506C, #FF6BC6);
    border-radius: 15px;
    padding: 3px 20px 3px 10px;
    color: #fff;
}

.more::after {
    content: "";
    position: absolute;
    top: 9px;
    right: 9px;
    width: 7px;
    height: 7px;
    border-top: 2px solid #fff;
    border-right: 2px solid #fff;
    transform: rotate(45deg);
}
```

效果：

![](images\xc21.jpg)

### 5.13 sales-bd模块

结构：

```html
<div class="sales-bd">
            <div class="row">
                <a href="#">
                    <img src="upload/pic1.jpg" alt="">
                </a>
                <a href="#">
                    <img src="upload/pic2.jpg" alt="">

                </a>
            </div>
            <div class="row">
                <a href="#">
                    <img src="upload/pic3.jpg" alt="">
                </a>
                <a href="#">
                    <img src="upload/pic4.jpg" alt="">

                </a>
            </div>
            <div class="row">
                <a href="#">
                    <img src="upload/pic5.jpg" alt="">
                </a>
                <a href="#">
                    <img src="upload/pic6.jpg" alt="">

                </a>
            </div>

        </div>
```

样式：

```css
.row {
    display: flex;
}

.row a {
    flex: 1;
    border-bottom: 1px solid #eee;
}

.row a:nth-child(1) {
    border-right: 1px solid #eee;
}

.row a img {
    width: 100%;
}
body去掉height:2000px;
```

效果：

![](images\xc23.jpg)




























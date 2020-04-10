# 移动web开发之rem布局

### 1. rem基础

#### 1.0 思考问题

- 页面布局文字能否随着屏幕大小变化而变化？
- 流式布局和flex布局主要针对于宽度布局，那高度如何设置？（之前的案例都是写死的高度）
- 怎么样让屏幕发生变化的时候元素高度和宽度等比例缩放？（rem）

#### 1.1 rem单位

rem (**root** em)是一个相对单位，类似于em，em是**父元素字体大小**。

不同的是rem的基准是相对于**html元素的字体大小**。

**em案例**：

```html
   <style>
        div {
            font-size: 12px;
        }
        
        p {
            /* 1. em相对于父元素 的字体大小来说的 */
            width: 10em;
            height: 10em; 
            /* 理解：em是父元素字体大小，那么10em就是10倍的父元素字体大小，所以p的大小是120px*120px*/
        }
    </style>
</head>

<body>
    <div>
        <p></p>
    </div>

</body>
```

**rem使用**：

比如，根元素（html）设置font-size=12px; 非根元素设置width:2rem; 则换成px表示就是24px。

```
/* 根html 为 12px */
html {
   font-size: 12px;
}
/* 此时 div 的字体大小就是 24px */       
div {
    font-size: 2rem;
}
```



**rem案例**：

```html
   <style>
        html {
            font-size: 12px;
        }
        
        div {
            font-size: 12px;
            width: 15rem;
            height: 15rem;
            background-color: purple;
        }
        
        p {
            /* 1. em相对于父元素 的字体大小来说的 */
            /* width: 10em;
            height: 10em; */
            /* 2. rem 相对于 html元素 字体大小来说的 */
            width: 10rem;
            height: 10rem;
            background-color: pink;
            /* 3.rem的优点就是可以通过修改html里面的文字大小来改变页面中元素的大小可以整体控制 */
        }
    </style>
</head>

<body>
    <div>
        <p></p>
    </div>

</body>
```

**总结**：

上述代码的结果是：

div的宽高为：15*12=180px

p的宽高为：10*12 = 120px

rem的优势：父元素文字大小可能不一致， 但是整个页面只有一个html，可以很好来控制整个页面的元素大小。

### 2. 媒体查询

#### 2.0 思考问题

之前的代码中，我们说了根据界面的大小，调整html的字体大小，从而可以改变使用rem为单位的元素的大小。

但是我们的代码中html的font-size是写死了，那么怎么根据界面大小，改变font-size呢？

我们来看媒体查询。

#### 2.1 什么是媒体查询

媒体查询（Media Query）是CSS3新语法。

+ 使用 @media查询，可以针对不同的媒体类型定义不同的样式
+ **@media 可以针对不同的屏幕尺寸设置不同的样式**
+ 当你重置浏览器大小的过程中，页面也会根据浏览器的宽度和高度重新渲染页面 
+ 目前针对很多苹果手机、Android手机，平板等设备都用得到多媒体查询

#### 2.2 媒体查询语法规范

**语法如下**：

```
@media mediatype and|not|only (media feature) {
    CSS-Code;
}
```

**注意**：

- 用 **@media**开头 注意@符号
- mediatype  媒体类型
- 关键字 and  not  only
- media feature 媒体特性必须有小括号包含

**关键字详细说明**：

1. mediatype 查询类型

​       将不同的终端设备划分成不同的类型，称为媒体类型  （理解为设备类型，非屏幕，屏幕）

<img src="images/1.jpg">

2. 关键字

​       **关键字将媒体类型或多个媒体特性连接到一起做为媒体查询的条件**。

+ and：可以将多个媒体特性连接到一起，相当于“且”的意思。
+ not：排除某个媒体类型，相当于“非”的意思，可以省略。
+ only：指定某个特定的媒体类型，可以省略。    

3. 媒体特性

   **每种媒体类型都具有各自不同的特性，根据不同媒体类型的媒体特性设置不同的展示风格**

   我们暂且了解三个：（注意他们要加小括号包含）

   <img src="images/2.jpg">

4. 示例代码：

   ```html
      <style>
           /* 这句话的意思就是： 在我们屏幕上 并且 最大的宽度是 800像素 设置我们想要的样式 */
           /* max-width 小于等于800 */
           /* 媒体查询可以根据不同的屏幕尺寸在改变不同的样式 */
           
           @media screen and (max-width: 800px) {
               body {
                   background-color: pink;
               }
           }
          /* 总结：媒体查询， 检测媒体（手机，电脑），的特征变化*/
           
           @media screen and (max-width: 500px) {
               body {
                   background-color: purple;
               }
           }
       </style>
   </head>
   
   <body>
   
   </body>
   ```

   

#### 2.3 媒体查询案例 

效果如下：

![](images\media-demo.gif)

**代码**：

```html
  <style>
        /* 1. 媒体查询一般按照从大到小或者 从小到大的顺序来 */
        /* 2. 小于540px 页面的背景颜色变为蓝色 */
        
        @media screen and (max-width: 539px) {
            body {
                background-color: blue;
            }
        }
        /* 3. 540 ~ 970 我们的页面颜色改为 绿色 */
        /* @media screen and (min-width: 540px) and (max-width: 969px) {
            body {
                background-color: green;
            }
        } */
        
        @media screen and (min-width: 540px) {
            body {
                background-color: green;
            }
        }
        /* 4. 大于等于970 我们页面的颜色改为 红色 */
        
        @media screen and (min-width: 970px) {
            body {
                background-color: red;
            }
        }
        /* 5. screen 还有 and 必须带上不能省略的 */
        /* 6. 我们的数字后面必须跟单位  970px   这个 px 不能省略的 */
    </style>
</head>

<body>

</body>
```

**总结：媒体查询书写规则**

注意： 

为了防止混乱，媒体查询我们要按照从小到大或者从大到小的顺序来写

但是我们最喜欢的还是**从小到大**来写，这样代码更简洁

![](images\3.png)

#### 2.4 媒体查询+rem案例 ***

**效果**： 屏幕大小变化时，购物车的字体，以及所在盒子的高度也在变化：

![](images\media+rem.gif)

**代码**：

```html
  <style>
        * {
            margin: 0;
            padding: 0;
        }
        /* html {
            font-size: 100px;
        } */
        /* 从小到大的顺序 */
        
        @media screen and (min-width: 320px) {
            html {
                font-size: 50px;
            }
        }
        
        @media screen and (min-width: 640px) {
            html {
                font-size: 100px;
            }
        }
        
        .top {
            /* 高度，字体大小，都设置为rem单位，即可根据html的font-size的改变而改变*/
            height: 1rem;
            font-size: .5rem;
            background-color: green;
            color: #fff;
            text-align: center;
            line-height: 1rem;
        }
    </style>
</head>

<body>
    <div class="top">购物车</div>
</body>

```

**注意**：这里的字体大小设置的比较大，一般我们是不会设置这么大的字的。

​	     这里设置的font-size为100px，那么div的高度就是1rem，也是100px

​	     那么真实情况可能是font-size为14px，那么div的高度为10rem，为140px。

**总结**：

​	rem+媒体查询，实现屏幕大小改变，界面元素跟着一起改变的原理，实现顺序：

- 媒体查询作用，根据屏幕尺寸的范围，来切换html的font-size （界面元素的参照物跟着屏幕改变）
- 界面元素的大小都以rem为单位（rem代表参照物html的font-size）



#### 2.5 媒体查询引入资源

- 当界面大小变化时，整个界面的结构有较大的变化时，我们会使用媒体查询引入资源。
- 针对不同大小的界面，准备不同的css样式文件，当界面大小变化时，直接改变引入的css样式文件，这就是媒体查询引入资源。

**效果**：

![](images\media+link.gif)

**代码**：

```html
    <style>
        /* 当我们屏幕大于等于 640px以上的，我们让div 一行显示2个 */
        /* 当我们屏幕小于640 我们让div一行显示一个 */
        /* 一个建议： 我们媒体查询最好的方法是从小到大 */
        /* 引入资源就是 针对于不同的屏幕尺寸 调用不同的css文件 */
    </style>
    <link rel="stylesheet" href="style320.css" media="screen and (min-width: 320px)">
    <link rel="stylesheet" href="style640.css" media="screen and (min-width: 640px)">
</head>

<body>
    <div>1</div>
    <div>2</div>
</body>

```

**总结**：link标签+media属性，就是媒体引入资源

### 3. less 基础

为啥要学习less，这是因为css有很多弊端。

#### 3.1 css弊端

CSS 是一门非程序式语言，没有变量、函数、SCOPE（作用域）等概念。

+ CSS 需要书写大量看似没有逻辑的代码，CSS 冗余度是比较高的。
+ 不方便维护及扩展，不利于复用。
+ CSS 没有很好的计算能力
+ 非前端开发工程师来讲，往往会因为缺少 CSS 编写经验而很难写出组织良好且易于维护的 CSS 代码项目。 

演示代码：

```html
  <style>
        html {
            font-size: 50px;
        }
        
        img {
            /* width: 82px;
            height: 82px; */
            /* width: 1.64rem;
            height: 1.64rem; */
            /* width: 82 / 50; */ /* 这里如果能直接写计算的公式，那就简单了：没有很好的计算能力*/
        }
        /* 如下的div，p，span的背景颜色都是pink，如果想改，得一个一个修改，维护不方便 */
        div {
            background-color: pink;
        }
        
        p {
            background-color: pink;
        }
        
        span {
            background-color: pink;
        }
    </style>
</head>

<body>

</body>
```



#### 3.2 Less 介绍 

- Less（LeanerStyle Sheets 的缩写）是一门 **CSS扩展语言**，也成为CSS预处理器。

- 做为 CSS的一种形式的扩展，它并没有减少CSS的功能，而是在现有的CSS语法上，**为CSS加入程序式语言**的特性。

- 它在CSS 的语法基础之上，**引入了变量，Mixin（混入），运算以及函数等功能**，大大简化了 CSS 的编写，并且降低了 CSS的维护成本，就像它的名称所说的那样，Less可以让我们用更少的代码做更多的事情。

- Less中文网址：[http://](http://lesscss.cn/)[less](http://lesscss.cn/)[css.cn/](http://lesscss.cn/)

- 常见的CSS预处理器：Sass、Less、Stylus

- 一句话：Less是一门 CSS 预处理语言，它扩展了CSS的动态特性。


#### 3.3 Less安装

①安装nodejs，可选择版本(8.0)，网址：<http://nodejs.cn/download/>

②检查是否安装成功，使用cmd命令（win10是window+r 打开运行输入cmd）  ---输入“node –v”查看版本即可

③基于nodejs在线安装Less，使用cmd命令“npm install -g less”即可

​	npm：node package manager，node包管理工具

​	less是作为node中的一个工具包存在的，所以通过npm安装

④检查是否安装成功，使用cmd命令“ lessc -v ”查看版本即可

![](images\node+less.jpg)

问题：node是啥？

![](images\nodejs.jpg)

**总结**：node作为一个软件进行安装，安装完成之后就作为一个环境存在，**一个可以运行js代码的环境**。

问题：-g啥意思？全局安装

![](images\-g.jpg)

**总结**：全局安装之后，在哪个目录都可以使用。

#### 3.4 Less使用

##### 1. Less 使用之变量

变量是指没有固定的值，可以改变的。

**理解**：变化的量，变化的内容，变化的值。

**语法**：

```
@变量名:值;
如：
@color: pink;
```

**注意**：

+ 必须有@为前缀
+ 不能包含特殊字符
+ 不能以数字开头
+ 大小写敏感

**代码**：

```less
// 定义一个粉色的变量
@color: pink;  
// 错误的变量名  @1color   @color~@#
// 变量名区分大小写  @color  和  @Color 是两个不同的变量
// 定义了一个 字体为14像素的变量
@font14: 14px;
body {
    background-color: @color;
}
div {
    color: @color;
    font-size: @font14;
}
a {
    font-size: @font14;
}
```

**总结**：

- 定义了一个粉色的变量，body和div都使用了这个变量。那么我们如果想要将body和div的颜色一起修改为另一个颜色，只需要修改变量的值即可，简单方便

- 一般将使用次数比较多的内容，定义为变量，然后通过使用变量，来使用到变量的值

  

##### 2. Less 编译 - vocode Less 插件

- 问题：html文件，是没有办法直接使用less文件的。html只能使用css文件，那么能不能将less转换为css，然后html文件去使用呢？

- 介绍：
  - 本质上，**Less 包含一套自定义的语法及一个解析器/翻译器，用户根据这些语法定义自己的样式规则，这些规则最终会通过解析器，编译生成对应的 CSS 文件**。
  - 所以，我们需要把我们的 less文件，编译生成为css文件，这样我们的html页面才能使用。
  - Easy LESS 插件用来把less文件编译为css文件
  - **Easy Less插件会使用less中的解析器/翻译器，将less翻译为css**
  - 安装完毕插件，重新加载下 vscode
  - 只要保存一下Less文件，会自动生成CSS文件
  - **less 编译： less翻译，将less翻译为css**
- 插件安装：

<img src="images/4.png">

效果：

![](images\less编译.png)

##### 3. Less 嵌套

less嵌套写法如下：

```css
/*我们经常用到选择器的嵌套 (选择器组合使用：后代选择器)*/
#header .logo {
  width: 300px;
}
/* less中的选择器嵌套写法 */
#header {
    .logo {
       width: 300px;
    }
}

```

如果遇见 （交集|伪类|伪元素选择器） ，利用&进行连接

```
a:hover{
    color:red;
}
a{
  &:hover{
      color:red;
  }
}
```

案例分析图：

![](images\less嵌套.png)

##### 4. Less 运算

任何数字、颜色或者变量都可以参与运算。就是Less提供了加（+）、减（-）、乘（*）、除（/）算术运算。

```
/*Less 里面写*/
@witdh: 10px + 5;
div {
    border: @witdh solid red;
}
/*生成的css*/
div {
  border: 15px solid red;
}
/*Less 甚至还可以这样 */
width: (@width + 5) * 2;

```

+ 乘号（*）和除号（/）的写法  
+ 运算符中间左右有个空格隔开 1px + 5
+ 对于两个不同的单位的值之间的运算，运算结果的值取第一个值的单位 
+ 如果两个值之间只有一个值有单位，则运算结果就取该单位

**案例分析图**：

![](images\less运算.png)

### 4. rem适配方案

#### 4.1 介绍

**先来思考问题**：

![](images\rem-适配.png)

**实际开发技术方案**：

- 按照设计稿与设备宽度的比例，动态计算并设置 html 根标签的 font-size 大小；（媒体查询）
- CSS 中，设计稿元素的宽、高、相对位置等取值，按照同等比例换算为 rem 为单位的值；
- 实现后的效果：根据屏幕大小，所有内容都可以实现适配

![](images\等比缩放效果.jpg)

**技术方案**：

1.less+rem+媒体查询

2.flexible.js+rem

**总结**： 

两种方案现在都存在。

方案2 更简单，现阶段大家无需了解里面的js代码。

#### 4.2 rem实际开发适配方案1---less+rem+媒体查询

##### 1.设计稿常见尺寸宽度

| 设备        | 常见宽度                                                     |
| ----------- | ------------------------------------------------------------ |
| iphone  4.5 | 640px                                                        |
| iphone 678  | 750px                                                        |
| Android     | 常见320px、360px、375px、384px、400px、414px、500px、720px大部分4.7~5寸的安卓设备为720px |

- 一般情况下，我们以一套或两套效果图适应大部分的屏幕，放弃极端屏或对其优雅降级，牺牲一些效果 
- 现在基本以750为准

##### 2. 动态设置 html 标签 font-size 大小 

①假设设计稿是750px

②假设我们把整个屏幕划分为15等份（划分标准不一可以是20份也可以是10等份）

③每一份作为html字体大小，这里就是50px

④那么在320px设备的时候，字体大小为320/15就是  21.33px

⑤用我们页面元素的大小除以不同的 html字体大小会发现他们比例还是相同的

⑥比如我们以750为标准设计稿

⑦一个100\*100像素的页面元素在  750屏幕下，  就是 100/ 50  转换为rem  是  2rem*2rem  比例是1比1

⑧320屏幕下，  html字体大小为21.33   则 2rem=  42.66px  此时宽和高都是 42.66  但是宽和高的比例还是 1比1

⑨但是已经能实现不同屏幕下  页面元素盒子等比例缩放的效果

**代码如下**：

```html
   <style>
        @media screen and (min-width: 320px) { /* 2/15   ----  42.66  */
            html {
                font-size: 21.33px;  /* 1rem就是21.33，是屏幕的 1/15  ,1rem屏幕等分之后的一份*/
            }
        }
        
        @media screen and (min-width: 750px) {   /*2/15   ---- 100px   */
            html {
                font-size: 50px;/* 1rem就是50px，是屏幕的 1/15 */
            }
        }
        
        div {
            width: 2rem; /* 设计稿为750px的100px的大小的盒子，转换为rem。   100/50 = 2rem  --- 2/15 */
            height: 2rem;
            background-color: pink;
        }
        /* 1. 首先我们选一套标准尺寸 750为准 
        2. 我们用屏幕尺寸 除以 我们划分的份数 得到了 html 里面的文字大小 但是我们知道不同屏幕下得到的文字大小是不一样的 */
        /* 3. 页面元素的rem值 =  页面元素在 750像素的下px值 / html 里面的文字大小 */
    </style>
</head>

<body>
    <div></div>
</body>
```

##### 3. 元素大小取值方法 ：

①最后的公式：页面元素的rem值 =  页面元素值（px） /  （屏幕宽度  /  划分的份数）

②屏幕宽度/划分的份数，就是每一份的大小，而每一份大小就是 htmlfont-size 的大小

③或者：页面元素的rem值 =  页面元素值（px） /  html font-size 字体大小

##### 4. 问题---为啥要将屏幕划分几等份，比如15等份？

这样做我们可以根据不同的屏幕分辨率，计算出html的font-size。（屏幕划分出的每一份就是font-size）

而我们界面上的元素都使用rem为单位，rem就是html的font-size。

这样的话，不同分辨率下的所有元素的大小，都会有等比例的缩放效果。

比如一个元素的宽度为2rem：

​	那么在320px屏幕下，这个元素的大小为2*21.33px = 42.66px

​	那么在750px屏幕下，这个元素的大小为2*50px = 100px

​	这两个结果，都是占自己屏幕的15分之2，但是在变大，所以是等比例缩放。



##### 5. 总结

rem方案1：less+rem+媒体查询方案的流程如下：

- 根据设计稿宽度，确定要分多少份，计算出一份多少px
- 比如设计稿750px，要分15份，一份50px，那么html的font-size就为50px，也就是1rem是50px
- 通过，媒体查询，计算出不同分辨率下的font-size
- 页面元素大小通过less的除法运算算出占多少rem：设计稿大小 / font-size = xx rem



rem+媒体查询，实现屏幕大小改变，界面元素跟着一起改变的原理，实现顺序：

- 媒体查询作用，根据屏幕尺寸的范围，来切换html的font-size （界面元素的参照物跟着屏幕改变）
- 界面元素的大小都以rem为单位（rem代表参照物html的font-size）



### 5. 苏宁首页

#### 5.1 15-苏宁首页common.less制作

苏宁首页地址 ：[苏宁首页](m.suning.com)

![](images\suning.jpg)

1、 技术选型

方案：我们采取单独制作移动页面方案

技术：布局采取rem适配布局（less + rem  + 媒体查询）

设计图： 本设计图采用 750px 设计尺寸（苏宁的就是750px）

2、搭建文件结构

<img src="images/5.jpg">

3、设置视口标签以及引入初始化样式

```css
<meta name="viewport" content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">

<link rel="stylesheet" href="css/normalize.css">
```

4、设置公共common.less文件

+ 新建common.less    设置好最常见的屏幕尺寸，利用媒体查询设置不同的html字体大小，因为除了首页其他页面也需要
+ 我们关心的尺寸有 320px、360px、375px、384px、400px、414px、424px、480px、540px、720px、750px
+ 划分的份数我们定为 15等份
+ 因为我们pc端也可以打开我们苏宁移动端首页，我们默认html字体大小为 50px，注意这句话写到最上面
+ 因为这套方案，是一套比较通用的方案，所以我直接处理成一个公共的文件：common.less

代码如下：

```less
// 设置常见的屏幕尺寸 修改里面的html文字大小
// 一定要写到最上面 ,老师的本意是，如果在pc端打开我们的界面，那么就是用这个写死的font-size:50px;
//但是这个压根不会生效，如果pc界面打开，走的是最后一个min-witdh:750px，其实也是font-size:50px;
html {
    font-size: 50px;
}
// 我们此次定义的划分的份数 为 15
@no: 15; //no ：number数字，老师写错了，一般我们会写成num
// 320
@media screen and (min-width: 320px) {
    html {
        font-size: 320px / @no;
    }
}
// 360
@media screen and (min-width: 360px) {
    html {
        font-size: 360px / @no;
    }
}
// 375 iphone 678
@media screen and (min-width: 375px) {
    html {
        font-size: 375px / @no;
    }
}

// 384
@media screen and (min-width: 384px) {
    html {
        font-size: 384px / @no;
    }
}

// 400
@media screen and (min-width: 400px) {
    html {
        font-size: 400px / @no;
    }
}
// 414
@media screen and (min-width: 414px) {
    html {
        font-size: 414px / @no;
    }
}
// 424
@media screen and (min-width: 424px) {
    html {
        font-size: 424px / @no;
    }
}

// 480
@media screen and (min-width: 480px) {
    html {
        font-size: 480px / @no;
    }
}

// 540
@media screen and (min-width: 540px) {
    html {
        font-size: 540px / @no;
    }
}
// 720
@media screen and (min-width: 720px) {
    html {
        font-size: 720px / @no;
    }
}

// 750
@media screen and (min-width: 750px) {
    html {
        font-size: 750px / @no;
    }
}
```

#### 5.2 16-苏宁首页import导入样式

- 新建index.less    这里面写首页的样式

- 将刚才设置好的 common.less 引入到index.less里面  

  语法如下：

```less
@import  “文件名”  

import:导入。引号里边的是导入的文件，可以不写后缀less
```

​	具体代码：

```less
index.less中：
// 首页的样式less文件
@import "common";
// @import 导入的意思 可以把一个样式文件导入到另外一个样式文件里面
// link 是把一个 样式文件引入到 html页面里面
//总结：link和import，一个引入，一个导入，其实以上都一样，我中包含你
//	   只不过使用场景不一样：
//	   	   import是less语法，用于less文件导入less文件
//	   	   link是html语法，用于html引入css文件
```

- 生成index.css  引入到 index.html 里面

具体代码：

```html
<link rel="stylesheet" href="css/index.css">
```



#### 5.3 17-苏宁首页body样式设置

```less
body {
    min-width: 320px;
    width: 15rem;
    margin: 0 auto;
    line-height: 1.5;
    font-family: Arial,Helvetica;
    background: #F2F2F2;
}
```

**问题**：

- width：为啥是15rem？

rem是html的font-size，而我们的设计稿是750px，那么750px对应设置的html的font-size是50px，所以就是750/50px=15rem。

- 为啥不用写max-width？

因为有媒体查询：

```less
// 750
@media screen and (min-width: 750px) {
    html {
        font-size: 750px / @no; //(750px/15份=50px)
    }
}
// 这里写的是min-width:750px,那么意味着他匹配的屏幕大小范围是：750-无限大
// 那么意思就是在比如1024px大小的屏幕下，html的font-size依然是50px，那么咱们的body的width：15rem依然是750px。
// 所以使用媒体查询之后，就不用在限制max-width了，只需要指定min-width即可。
```

最终效果：

![](images\sn01.jpg)

#### 5.4 18-苏宁首页search-content模块布局

搜索模块：

![](images\sn02.jpg)

结构：

```html
   <!-- 顶部搜索框 -->
    <div class="search-content">
    </div>
```

样式：

```less
// 页面元素rem计算公式： 页面元素的px / html 字体大小 50
// search-content 
@baseFont: 50;  //font-size的大小为50，为啥是50呢？因为我们的设计稿是750px，而750对应的font-size就是50
.search-content {
    position: fixed;
    top: 0;
    left: 50%;
    transform: translateX(-50%);
    width: 15rem;  // 固定定位必须有宽度，而搜索栏的宽度与设计稿一样是750px，所以是750/50=15rem
    height: 88rem / @baseFont; //经过测量是88px，但是我们需要经过计算得到以rem为单位的值
    //height: 88rem / 50;  //可以将50变为一个变量再使用，也可以直接写50
    background-color:#FFC001;
 }
// 计算的写法是88rem/50，为啥是rem呢？因为我们需要最终的单位是rem。
```

效果：

![](images\sn03.jpg)

#### 5.5 19-苏宁首页search-content内容布局

分析：左右固定，中间剩余空间给搜索框。采用flex布局。

![](images\sn04.jpg)



结构：

```html
    <div class="search-content">
        <a href="#" class="classify">1</a>
        <div class="search">2</div>
        <a href="#" class="login">3</a>
    </div>
```

样式：

```less
.search-content {
    display: flex;
    .classify {
        width: 44rem / @baseFont;
        height: 70rem / @baseFont;
        margin: 11rem / @baseFont 25rem / @baseFont 7rem / @baseFont 24rem / @baseFont;
    }
    .search {
        flex: 1;
        background-color:purple;
    }
    .login {
        width: 75rem / @baseFont;
        height: 70rem / @baseFont;
        background-color:blue;
        margin: 10rem / @baseFont;

    }
}
```

效果：

![](images\sn05.jpg)

#### 5.6 20-苏宁首页search模块制作

结构：

```html
    <div class="search-content">
        <a href="#" class="classify"></a>
        <div class="search">
            <form action="">
                <!--注意：这里必须是search，如果使用text，添加padding值之后，会超出。因为search默认有border-box -->
                <input type="search" value="厨卫保暖季 哒哒哒"> 
            </form>
        </div>
        <a href="#" class="login">登录</a>
    </div>
```

样式：

```less
 .classify {
        width: 44rem / @baseFont;
        height: 70rem / @baseFont;
        margin: 11rem / @baseFont 25rem / @baseFont 7rem / @baseFont 24rem / @baseFont;
        background: url(../images/classify.png) no-repeat;  /*增加*/
        // 背景缩放
        background-size: 44rem / @baseFont 70rem / @baseFont; /*增加*/
    }
    .search {
        flex: 1;
        background-color:purple; /*去掉*/
        input { /*增加*/
            outline: none;
            width: 100%;
            border: 0;
            height: 66rem / @baseFont;
            border-radius: 33rem / @baseFont;
            background-color:#FFF2CC;
            margin-top: 12rem / @baseFont;
            font-size: 25rem / @baseFont;
            padding-left: 55rem / @baseFont;
            color: #757575;
        }
    }
    .login {
        width: 75rem / @baseFont;
        height: 70rem / @baseFont;
        line-height: 70rem / @baseFont; /*增加*/
        margin: 10rem / @baseFont;
        font-size: 25rem / @baseFont; /*增加*/
        text-align: center; /*增加*/
        color: #fff; /*增加*/
        background-color:blue; /*去掉*/

    }
    common.less：增加
    a {
        text-decoration: none;
    }
```

效果：

![](images\sn06.jpg)

#### 5.7 21-苏宁首页banner和广告模块制作5.8

banner和广告：

![](images\sn07.jpg)

结构：

```html
 <!-- banner部分 -->
    <div class="banner">
        <img src="upload/banner.gif" alt="">
    </div>
    <!-- 广告部分 -->
    <div class="ad">
        <a href="#"><img src="upload/ad1.gif" alt=""></a>
        <a href="#"><img src="upload/ad2.gif" alt=""></a>
        <a href="#"><img src="upload/ad3.gif" alt=""></a>
    </div>
```

样式：

```less
// banner
.banner {
    width: 750rem / @baseFont;
    height: 368rem / @baseFont;
    img {
        width: 100%;
        height: 100%;
    }
}
// ad
.ad {
    display: flex;
    a {
        flex: 1;
        img {
            width: 100%;
        }
    }
}
```

效果：

![](images\sn08.jpg)

#### 5.8 22-苏宁首页nav部分制作

nav部分：

![](images\sn09.jpg)

结构：

```html
 <!-- nav模块 -->
    <nav>
        <a href="#">
            <img src="upload/nav1.png" alt="">
            <span>爆款手机</span>
        </a>
        <a href="#">
            <img src="upload/nav1.png" alt="">
            <span>爆款手机</span>
        </a>
        <a href="#">
            <img src="upload/nav1.png" alt="">
            <span>爆款手机</span>
        </a>
        <a href="#">
            <img src="upload/nav1.png" alt="">
            <span>爆款手机</span>
        </a>
        <a href="#">
            <img src="upload/nav1.png" alt="">
            <span>爆款手机</span>
        </a>
        <a href="#">
            <img src="upload/nav1.png" alt="">
            <span>爆款手机</span>
        </a>
        <a href="#">
            <img src="upload/nav1.png" alt="">
            <span>爆款手机</span>
        </a>
        <a href="#">
            <img src="upload/nav1.png" alt="">
            <span>爆款手机</span>
        </a>
        <a href="#">
            <img src="upload/nav1.png" alt="">
            <span>爆款手机</span>
        </a>
        <a href="#">
            <img src="upload/nav1.png" alt="">
            <span>爆款手机</span>
        </a>

    </nav>
```

样式：

```less
// nav
nav {
    width: 750rem / @baseFont;
    a {
        float: left;
        width: 150rem / @baseFont;
        height: 140rem / @baseFont;
        text-align: center;
        img {
            display: block;
            width: 82rem / @baseFont;
            height: 82rem / @baseFont;
            margin: 10rem / @baseFont auto 0;
        }
        span {
            font-size: 25rem / @baseFont;
            color: #333;
        }
    }
}
```

效果：

![](images\sn10.jpg)



### 6. rem 适配方案2---flexible.js+rem

#### 6.1. rem适配2

简洁高效的rem适配方案flexible.js：

![](images\rem2.jpg)

#### 6.2. flexible.js介绍

手机淘宝团队出的简洁高效 移动端适配库

我们再也不需要在写不同屏幕的媒体查询，因为里面js做了处理

它的**原理是把当前设备划分为10等份**，但是不同设备下，比例还是一致的。

我们要做的，就是**确定**好我们当前设备的**html 文字大小**就可以了

比如当前设计稿是 750px， 那么我们只需要把 **html 文字大小设置为 75px(750px / 10)** 就可以

里面页面元素rem值： **页面元素的px 值 /  75**  

剩余的，让flexible.js来去算

github地址：[https://github.com/amfe/lib-flexible](https://link.jianshu.com/?t=https://github.com/amfe/lib-flexible)

**flexible的代码分析**：

```js
  // set 1rem = viewWidth / 10 ： 设置1rem为设备的宽度/10
  function setRemUnit () {
    var rem = docEl.clientWidth / 10  // 当前屏幕宽度 / 10 
    docEl.style.fontSize = rem + 'px' // html.fontsie = rem
  }

```

#### 6.3 总结

rem方案2：flexible+rem流程如下：

- 根据设计稿宽度，确定要分多少份，计算出一份多少px （**flexible帮助我们做了**）
- 比如设计稿750px，flexible会分10份，一份75px，那么html的font-size就为75px，也就是1rem是75px
- 通过，媒体查询，计算出不同分辨率下的font-size (**flexible帮助我们做了：setRemUnit**)
- 页面元素大小通过**插件**帮助我们做除法运算算出占多少rem：设计稿大小 / font-size = xx rem

#### 6.4 方案对比

方案1：

rem方案1：less+rem+媒体查询方案的流程如下：

- 根据设计稿宽度，确定要分多少份，计算出一份多少px
- 比如设计稿750px，要分15份，一份50px，那么html的font-size就为50px，也就是1rem是50px
- 通过，媒体查询，计算出不同分辨率下的font-size
- 页面元素大小通过less的除法运算算出占多少rem：设计稿大小 / font-size = xx rem

方案2：

rem方案2：flexible+rem流程如下：

- 根据设计稿宽度，确定要分多少份，计算出一份多少px （**flexible帮助我们做了固定10份**）

- 比如设计稿750px，flexible会分10份，一份75px，那么html的font-size就为75px，也就是1rem是75px

- 通过，js，计算出不同分辨率下的font-size (**flexible帮助我们做了：setRemUnit**)

- 页面元素大小通过**插件**帮助我们做除法运算算出占多少rem：设计稿大小 / font-size = xx rem

- 为了防止屏幕过大，自己添加了一个媒体查询，限制如果大于750，font-size：75px

  ```css
  @media screen and (min-width: 750px) { /*超过750，就设置font-size为75px。意思就是我们最大的font-size为75px，也以为这屏幕最大为750px，因为屏幕再变大，界面不跟着变了（我们设置的body宽度为10rem）*/
      html {
          font-size: 75px!important;
      }
  }
  ```

  

**优势**：屏幕变化的过程中，界面跟着一起缩放的效果比较细腻。因为只要屏幕改变一点点，font-size就改变了。

方案1：都是某个范围之内一个效果，超过这个范围，才会有效果变化。



### 7. 方案2制作苏宁首页

#### 7.1准备工作

1. 技术选型

- 方案：我们采取单独制作移动页面方案
- 技术：布局采取rem适配布局2（flexible.js +  rem）
- 设计图： 本设计图采用 750px 设计尺寸

2. 搭建目录结构

![](images\html5.png)

​	这里需要引入flexible的js，所以需要有一个js文件夹。

​	将flexible.js放入js中。

3. 设置视口标签以及引入初始化样式还有js文件

   ```html
   <meta name="viewport" content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
   
   <link rel="stylesheet" href="css/normalize.css">
   <link rel="stylesheet" href="css/index.css">
   ```

   我们页面需要引入 这个js文件：

   ```html
   //在 index.html 中 引入 flexible.js 这个文件
   <script src=“js/flexible.js”> </script>
   ```

4. body样式

   ```css
   body {
   min-width: 320px;
   width:15rem;
   margin: 0 auto;
   line-height: 1.5;
   font-family: Arial,Helvetica;
   background: #F2F2F2;
   }
   ```



#### 7.3 25-rem适配方案2body样式修改

flexible与我们第一种方案不太一样，那么body的样式也会不一样：

```css
body {
    min-width: 320px;
    max-width: 750px; /*增加*/
    /* flexible 给我们划分了 10 等份 */
    width: 10rem; /*修改*/
    margin: 0 auto;
    line-height: 1.5;
    font-family: Arial, Helvetica;
    background: #f2f2f2;
}
```

**问题**：

- 这里为啥需要max-width:750px？

  因为我们使用的是flexible来处理的，他跟第一种方案不一样，并没有通过媒体查询来限制条件，所以需要自己设置max-width。

- width为啥是10rem？

  因为设计稿是750px，而分成10等份，每一份是75px，font-size就是75px，所以750/75=10rem。

**效果**：

添加过flexible，设置过body之后，没有添加max-width之前，我们测试了一下flexible的功能：

打开index.html，F12观察，发现html的font-size是136.6。这是因为分辨率为1366/10等份 = 136.6

![](images\sn21.jpg)



**总结**：

**发现flexible，会根据屏幕分辨率，自动将屏幕分成10等份，而html的font-size等于1等份的值**

**而我们需要将最大宽度限定在自己的设计稿宽度。max-width:750px。**

#### 7.4 26-一个神奇的vscode插件cssrem

- 刚刚的body的width是我们自己计算出来的，那么界面的元素大小还是需要自己计算么？
- 之前是有less，可以直接使用除法。
- 现在呢？
- 可以使用一个插件：cssrem，可以将px转换为rem
- 插件效果如下：

![](images\cssrem.gif)

设置html字体大小基准值

1. 插件默认的html字体大小为16px

![](images\sn24.jpg)

2. 而我们的字体大小为75px

3. 打开 设置 快捷键是 ctrl + 逗号

   点击首选项按钮，再点击设置

![](images\sn23.jpg)

4. 进入设置界面：点击三个点，再点击打开settings.json  （**如果进入此界面，没有三个点，则直接搜索cssrem**）

   ![](images\sn25.jpg)

   

5. 修改

![](images\sn26.jpg)

点击编辑之后，再点击复制到设置，这个设置项就跑到右侧了，然后修改为75。最后重启vscode。

![](images\sn27.jpg)

重启之后，测试： 82/75就是等于1.0933

![](images\sn28.jpg)



#### 7.5 27-修改flexible默认html字体大小

都配置好了之后，我们再来实现苏宁搜索框：

搜索框：

![](images\sn31.jpg)

结构：

```html
<div class="search-content">
</div>
```

样式：

```css
/* search-content */

.search-content {
    display: flex;
    position: fixed;
    top: 0;
    left: 50%;
    transform: translateX(-50%);
    width: 10rem;
    height: 1.173333rem;
    background-color: #FFC001;
}
```

问题：

![](images\sn29.jpg)

发现设置的宽度为10rem，但是宽度为啥是1366呢，一看html的font-size，原来是136.6px。为啥是这样的效果呢？

flexible，他就是将屏幕平分为10分，每一份就是136.6px。他并没有限制屏幕最大尺寸。

那怎么办呢？我们自己限制一下：index.css中，增加如下代码：

```css
/* 如果我们的屏幕超过了 750px  那么我们就按照 750设计稿来走 不会让我们页面超过750px */

@media screen and (min-width: 750px) { /*超过750，就设置font-size为75px。意思就是我们最大的font-size为75px，也以为这屏幕最大为750px，因为屏幕再变大，界面不跟着变了（我们设置的body宽度为10rem）*/
    html {
        font-size: 75px!important;
    }
}
```

**效果**：

![](images\sn30.jpg)

**效果描述**：只要屏幕变化一点，我们的body就会跟着一起变化，这是flexible的优势，界面时刻跟着屏幕一起变化，这样的话，效果也会更加细腻。

不像之前的处理方式，都是某个范围之内一个效果，超过这个范围，才会有效果变化。

**总结**：

因为flexible是默认将屏幕分为10等分

但是当屏幕大于750的时候希望不要再去重置html字体了

所以要自己通过媒体查询设置一下

并且要把权重提到最高

#### 7.6 28-rem适配方案2search-content内容制作1

 结构：

```html
  <div class="search-content">
        <a href="#" class="classify"></a>
        <div class="search"></div>
        <a href="#" class="login">登录</a>
    </div>
```

样式：

```css
.search-content {
    display: flex;/*增加*/
}
.classify {
    width: .586667rem;
    height: .933333rem;
    margin: .146667rem .333333rem .133333rem;
    background: url(../images/classify.png) no-repeat;
    background-size: .586667rem .933333rem;
}

.search {
    flex: 1;
    background-color:purple;
}

.login {
    width: 1rem;
    height: .933333rem;
    margin: .133333rem;
    background-color:pink;
    color: #fff;
    text-align: center;
    line-height: .933333rem;
    font-size: .333333rem;
}
a {
    text-decoration: none;
    font-size: .333333rem;
}

```

效果：

![](images\sn32.jpg)



#### 7.7 29-rem适配方案2search-content内容制作2

结构：

```html
  <div class="search-content">
        <a href="#" class="classify"></a>
        <div class="search">
            <form action=""> //增加
                <input type="search" value="rem适配方案2很开心哦">
            </form>
        </div>
        <a href="#" class="login">登录</a>
    </div>
```

样式：

```css
.search input {
    outline: none;
    border: 0;
    width: 100%;
    height: .88rem;
    font-size: .333333rem;
    background-color: #FFF2CC;
    margin-top: .133333rem;
    border-radius: .44rem;
    color: #757575;
    padding-left: .733333rem;
}
.login {
    background-color:pink; /*去掉*/
} 
.search {
    background-color:purple;/*去掉*/
}
```

效果：

![](images\sn33.jpg)
















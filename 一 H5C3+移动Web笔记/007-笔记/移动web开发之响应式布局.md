# 移动端WEB开发之响应式布局

### 1. 响应式开发原理 

#### 1.1 响应式开发原理

就是**使用媒体查询针对不同宽度的设备进行布局和样式的设置，从而适配不同设备的目的**。

响应式开发可以实现，一套界面在不同终端进行正常显示。

移动端设备的屏幕分辨率太多，响应式将这些进行了归类：

| 设备划分                 | 尺寸区间             |
| ------------------------ | -------------------- |
| 超小屏幕（手机）         | < 768px              |
| 小屏设备（平板）         | >= 768px  ~  < 992px |
| 中等屏幕（桌面显示器）   | >= 992px  ~  <1200px |
| 宽屏设备（大桌面显示器） | >= 1200px            |

#### 1.2 响应式布局容器

- 问题：
  - 响应式要适配各种大小屏幕，那么我们通过媒体查询，来控制界面中的每个元素的大小么？
  - 这样太麻烦了，可以使用响应式。
- 响应式介绍：
  - 响应式需要一个**父级做为布局容器**，**来配合子级元素来实现变化效果**。
  - 原理就是在不同屏幕下，**通过媒体查询来改变这个布局容器的大小**，**再改变里面子元素的排列方式和大小**，从而实现不同屏幕下，看到不同的页面布局和样式变化。
- 问题：
  - 父容器的大小如何确定呢？
  - 响应式进行了父容器尺寸的划分
- 父容器版心的尺寸划分
  - 超小屏幕（手机，小于 768px）：设置宽度为 100% （屏幕小的，我们让界面跟屏幕一般大）
  - 小屏幕（平板，大于等于 768px）：设置宽度为 750px
  - 中等屏幕（桌面显示器，大于等于 992px）：宽度设置为 970px
  - 大屏幕（大桌面显示器，大于等于 1200px）：宽度设置为 1170px 
  - 规律：父容器的宽度总是比屏幕小一点，这是因为我们在处理的时候，让父容器居中，两边有些许空白，这样更好看，所以父容器，也可以叫做版心。
  - 但是我们也可以根据实际情况自己定义划分

案例代码：

```html
  <style>
        .container {
            height: 150px;
            background-color: pink;
            margin: 0 auto;
        }
        /* 1. 超小屏幕下  小于 768  布局容器的宽度为 100% */
        
        @media screen and (max-width: 767px) {
            .container {
                width: 100%;
            }
        }
        /* 2. 小屏幕下  大于等于768  布局容器改为 750px */
        
        @media screen and (min-width: 768px) {
            .container {
                width: 750px;
            }
        }
        /* 3. 中等屏幕下 大于等于 992px   布局容器修改为 970px */
        
        @media screen and (min-width: 992px) {
            .container {
                width: 970px;
            }
        }
        /* 4. 大屏幕下 大于等于1200 布局容器修改为 1170 */
        
        @media screen and (min-width: 1200px) {
            .container {
                width: 1170px;
            }
        }
    </style>
</head>

<body>
    <!-- 响应式开发里面，首先需要一个布局容器 -->
    <div class="container"></div>
</body>
```

**总结**：其实都是一样的：

​	之前的rem布局，我们是根据媒体查询来控制html的font-size的大小，界面的元素尺寸都以font-size为单位，屏幕变化，font-size变化，进而影响界面的每个元素。

​	现在的响应式布局，我们是根据媒体查询控制父布局容器的宽度，界面的元素尺寸都以父布局容器为参考，以父布局容器的百分比来设置元素大小。这样的话，屏幕变化，父布局容器宽度变化，进而影响界面的每个元素。

#### 1.3响应式案例-导航栏

代码：

```html
 <style>
        * {
            margin: 0;
            padding: 0;
        }
        
        ul {
            list-style: none;
        }
        
        .container {
            width: 750px;
            margin: 0 auto;
        }
        
        .container ul li {
            float: left;
            width: 93.75px;
            height: 30px;
            background-color: green;
        }
        
        @media screen and (max-width: 767px) {
            .container {
                width: 100%;
            }
            .container ul li {
                width: 33.33%;/*布局中的元素，都以父容器的宽度百分比设置大小*/
            }
        }
    </style>
</head>

<body>
    <div class="container">
        <ul>
            <li>导航栏</li>
            <li>导航栏</li>
            <li>导航栏</li>
            <li>导航栏</li>
            <li>导航栏</li>
            <li>导航栏</li>
            <li>导航栏</li>
            <li>导航栏</li>
        </ul>
    </div>
</body>
```

**总结**：

此案例，只处理了两种范围的屏幕： 小屏幕pad，超小屏幕（手机）

在范围切换时，界面布局发生了改变，由1/8，变为1/3  (如果范围切换时，布局可能发生变化)  ***

在某一个范围内，屏幕继续变化，界面元素依然是等比例缩放

###  2. bootstrap的介绍

#### 2.1 Bootstrap简介

Bootstrap 来自 Twitter（推特），是目前最受欢迎的前端**框架**。Bootstrap 是基于HTML、CSS 和 JAVASCRIPT 的，它简洁灵活，使得 Web 开发更加快捷。

[中文网](lhttp://www.bootcss.com/)  [官网](lhttp://getbootstrap.com/)  [推荐网站](http://bootstrap.css88.com/)

Bootstrap：是用于开发响应式布局，移动设备优先的web项目。

框架：顾名思义就是一套架构，它有一套比较完整的网页功能解决方案，而且控制权在框架本身，有预制样式库、组件和插件。使用者要按照框架所规定的某种规范进行开发。

组件：很多样式的下拉菜单，导航栏，按钮等等组件。（**这些带样式的，界面常用的效果，称之为组件**）

插件：**js代码写出来的效果**（会自动轮播的轮播图等），**称之为插件**。

**框架**：**其实就是一个成规模的工具**。**有很多现成的样式（css代码），和功能（js代码）**。

#### 2.2 bootstrap优点

+ 标准化的html+css编码规范
+ 提供了一套简洁、直观、强悍的组件
+ 有自己的生态圈，不断的更新迭代
+ 让开发更简单，提高了开发的效率

#### 2.3 版本简介

2.x.x：停止维护,兼容性好,代码不够简洁，功能不够完善。

3.x.x：目前使用最多,稳定,但是放弃了IE6-IE7。对 IE8 支持但是界面效果不好,偏向用于开发响应式布局、移动设备优先的WEB 项目。

4.x.x：最新版，目前还不是很流行

#### 2.4 bootstrap基本使用

在现阶段我们还没有接触JS相关课程，所以我们只考虑使用它的样式库。

那么我们接下来就需要看一下如何使用bootstrap框架的样式库：

框架的控制权在框架制作者，而开发者(使用者)要按照框架所规定的某种规范进行开发。

Bootstrap 使用四步曲： 

1. 创建文件夹结构  

   ![](images/1.png)

   将bootstrap中的三个文件夹（右侧），复制到自己创建的bootstrap文件夹（左侧）中。

2. 创建 html 骨架结构 （下面是最简单的一个Bootstrap的一个例子）

   ```html
   <!DOCTYPE html>
   <html lang="zh-CN">
    <head>
       <meta charset="utf-8">
       <!--要求当前网页使用IE浏览器最高版本edge的内核来渲染 -->
       <meta http-equiv="X-UA-Compatible" content="IE=edge">
       <!-- 视口标签：视口的宽度和设备一致，默认的缩放比例和PC端一致，用户不能自行缩放 -->
       <meta name="viewport" content="width=device-width, initial-scale=1">
       <!-- 上述3个meta标签*必须*放在最前面，任何其他内容都*必须*跟随其后！ -->
   
       <title>Bootstrap 101 Template</title>
   
       <!-- 条件注释，如果小于id9，就添加如下两个文件  （if 如果，lt 小于 less then）-->
       <!--第一句： 解决ie9以下浏览器对html5新增标签的不识别，并导致CSS不起作用的问题 -->
       <!--第二句： 解决ie9以下浏览器对 css3 Media Query 的不识别 -->
       <!--[if lt IE 9]> 
       <script src="//cdn.bootcss.com/html5shiv/3.7.2/html5shiv.min.js"></script>
       <script src="//cdn.bootcss.com/respond.js/1.4.2/respond.min.js"></script>
       <![endif]-->
   </head>
   
   <body>
   </body>
   
   </html>
   ```

   

3. 引入相关样式文件  

   ```
   <!-- Bootstrap 核心样式-->
   <link rel="stylesheet" href="bootstrap/css/bootstrap.min.css">
   ```

   ​

4. 书写内容 

   这里我们直接在body中添加123即可：

   **效果**：123没了边距，就说明我们引入bootstrap样式库成功了。

   ![](images\bootstrap-demo.jpg)

5. 直接使用bootstrap提供的样式

   

   **代码**：在刚刚的index.html中添加如下代码

   ```html
       <style>
           /*利用我们自己写的样式覆盖原先的样式*/
           
           .login {
               width: 80px;
               height: 45px;
           }
       </style>
   </head>
   
   <body>
       <!-- 123 -->
       <button type="button" class="btn btn-success">Success </button>
       <div class="btn btn-success login">登陆</div>
       <div class="btn btn-danger">未成功</div>
   </body>
   ```

   **效果**：

   ![](images\bootstrap-demo2.jpg)

   **总结**：

   直接拿Bootstrap 预先定义好的样式来使用

   修改Bootstrap 原来的样式，注意权重问题

   学好Bootstrap 的关键在于**知道它定义了哪些样式，以及这些样式能实现什么样的效果**

   **其实这些样式，大家是没必要记的，只需要知道网站，能够自己上去查找，找到自己想要的效果即可**：

   收藏网站：http://bootstrap.css88.com/

#### 2.5 bootstrap布局容器

Bootstrap 需要为页面内容和栅格系统包裹一个容器，**Bootstrap预先定义好了两个容器样式类**：

.container

+ `.container` 类用于固定宽度并支持响应式布局的容器。 
+ `.container` 类，已经通过媒体查询处理了屏幕范围：
+ 大屏 ( >=1200px)  宽度定为 1170px
+ 中屏 ( >=992px)   宽度定为  970px
+ 小屏 ( >=768px)   宽度定为  750px
+ 超小屏  (100%) 

.container-fluid

+ 用于流式布局的容器，宽度为百分百，占据全部视口（viewport）的容器
+ 适合于单独移动端开发

**两者区别**：

（1）**container-fluid的width是100％**，**而container的width是用媒体查询获得的动态尺寸**。两者样式肯定是不一样的。并且由于padding的原因两者不可用嵌套，他们就是提供两种视觉风格。

（2）container-fluid和container 全部都是响应式的布局。只是container有1个98px的margin 存在 Container-fluid 没有。

**代码**：

```html
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <!--[if lt IE 9]>
      <script src="https://oss.maxcdn.com/html5shiv/3.7.2/html5shiv.min.js"></script>
      <script src="https://oss.maxcdn.com/respond/1.4.2/respond.min.js"></script>
    <![endif]-->
    <!-- 一定不要忘记引入bootstrap 的样式文件 -->
    <link rel="stylesheet" href="bootstrap/css/bootstrap.min.css">
    <title>Document</title>
</head>

<body>
    <div class="container">123</div>
    <div class="container-fluid">123</div>
</body>
```

**效果**：

![](images\container.jpg)

**总结**：

意思就是我们想要使用boostrap进行布局，就必须包裹一个容器，而且这个容器使用的类必须是.container和.contianer-fluid。





#### 2.6 bootstrap栅格系统

##### 1. 介绍

- Bootstrap提供了一套响应式、移动设备优先的流式栅格系统，随着屏幕或视口（viewport）尺寸的增加，系统会自动分为最多12列。

- 栅格系统用于通过一系列的行（row）与列（column）的组合来创建页面布局，你的内容就可以放入这些创建好的布局中。
- Bootstrap里边的container的宽度是固定的，但是不同屏幕下，container的宽度不同，Bootstrap是将container进行12等份划分。
- 那么屏幕变化，container变化，12等份的每一份变化，我们的界面元素的大小依据每一等份来设置，那么也就实现了屏幕适配。
- **栅格系统**：其实就是网格布局，有行有列。栅格系统用于通过一系列的行（row）与列（column）的组合来创建页面布局，你的内容就可以放入这些创建好的布局中 

![](images\shange.png)



##### 2. 使用

Bootstrap针对不同的屏幕大小，设置了对应的类样式的前缀：

|                     | 超小屏幕（手机）< 768px | 小屏设备（平板）>=768px | 中等屏幕（桌面显示器）>=992px | 宽屏设备（大桌面显示器）>=1200px |
| ------------------- | ----------------------- | ----------------------- | ----------------------------- | -------------------------------- |
| .container 最大宽度 | 自动(100%)              | 750px                   | 970px                         | 1170px                           |
| 类前缀              | .col-xs-                | .col-sm-                | .col-md-                      | .col-lg-                         |
| 列（column）数      | 12                      | 12                      | 12                            | 12                               |

+ 按照不同屏幕划分为1~12 等份 （一般都是划分为2等份）
+ **我们实现列的平均划分  需要给列添加  类前缀** 
+ **这样bootstrap才知道你是在哪个屏幕下，划分成几等份**
+ xs：extra small--超小； sm：small--小；  md：medium--中等； lg：large--大；
+ 列（column）大于 12，多余的“列（column）”所在的元素将被作为一个整体另起一行排列
+ 每一列默认有左右15像素的 padding

**代码**：

```html
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <!--[if lt IE 9]>
      <script src="https://oss.maxcdn.com/html5shiv/3.7.2/html5shiv.min.js"></script>
      <script src="https://oss.maxcdn.com/respond/1.4.2/respond.min.js"></script>
    <![endif]-->
    <!-- 一定不要忘记引入bootstrap 的样式文件 -->
    <link rel="stylesheet" href="bootstrap/css/bootstrap.min.css">
    <title>Document</title>
    <style>
        [class^="col"] {
            border: 1px solid #ccc;
        }
    </style>
</head>

<body>
    <div class="container">
        <div class="row">
            <div class="col-lg-3">1</div>
            <div class="col-lg-3">2</div>
            <div class="col-lg-3">3</div>
            <div class="col-lg-3">4</div>
        </div>
        <!-- 如果孩子的份数相加等于12 则孩子能占满整个 的container 的宽度 -->
        <div class="row">
            <div class="col-lg-6">1</div>
            <div class="col-lg-2">2</div>
            <div class="col-lg-2">3</div>
            <div class="col-lg-2">4</div>
        </div>
        <!-- 如果孩子的份数相加 小于 12 则会？ 则占不满整个container 的宽度 会有空白 -->
        <div class="row">
            <div class="col-lg-6">1</div>
            <div class="col-lg-2">2</div>
            <div class="col-lg-2">3</div>
            <div class="col-lg-1">4</div>
        </div>
        <!-- 如果孩子的份数相加 大于 12 则会？多于的那一列会 另起一行显示  -->

        <div class="row">
            <div class="col-lg-6">1</div>
            <div class="col-lg-2">2</div>
            <div class="col-lg-2">3</div>
            <div class="col-lg-3">4</div>
        </div>


    </div>
</body>
```

**效果**：

![](images\01.jpg)

##### 3. 同时指定不同屏幕的类名

- 在屏幕不断变化的情况下，我们的界面布局可能会发生比较大的改变，比如大屏幕一行显示4列，小屏幕一行显示3列，这种效果应该如何处理呢？
- 可以同时为一列指定多个设备的类名，以便划分不同份数  例如 class="col-md-4 col-sm-6"

代码：

```html
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <!--[if lt IE 9]>
      <script src="https://oss.maxcdn.com/html5shiv/3.7.2/html5shiv.min.js"></script>
      <script src="https://oss.maxcdn.com/respond/1.4.2/respond.min.js"></script>
    <![endif]-->
    <!-- 一定不要忘记引入bootstrap 的样式文件 -->
    <link rel="stylesheet" href="bootstrap/css/bootstrap.min.css">
    <title>Document</title>
    <style>
        [class^="col"] {
            border: 1px solid #ccc;
        }
        
        .row:nth-child(1) {
            background-color: pink;
        }
    </style>
</head>

<body>
    <div class="container">
        <div class="row">
            <div class="col-lg-3 col-md-4 col-sm-6 col-xs-12">1</div>
            <div class="col-lg-3 col-md-4 col-sm-6 col-xs-12">2</div>
            <div class="col-lg-3 col-md-4 col-sm-6 col-xs-12">3</div>
            <div class="col-lg-3 col-md-4 col-sm-6 col-xs-12">4</div>
        </div>
    </div>
</body>
```

效果：

超小屏幕：

![](images\04.jpg)

小屏幕：

![](images\03.jpg)

中屏幕：

![](images\05.jpg)

大屏幕：

![](images\02.jpg)



##### 4. 栅格嵌套-列嵌套

- 栅格系统内置的栅格系统将内容再次嵌套
- 简单理解就是一个列内再分成若干份小列
- 我们可以通过添加一个新的 .row 元素和一系列 .col-sm-* 元素到已经存在的 .col-sm-*元素内
- 也就是将一个row+col添加到一个col中

**嵌套效果如下**：

![](images\06.jpg)

**嵌套语法如下**：

```
<!-- 列嵌套 -->
 <div class="col-sm-4">
    <div class="row">
         <div class="col-sm-6">小列</div>
         <div class="col-sm-6">小列</div>
    </div>
</div>

```

**代码**：

```html
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <!--[if lt IE 9]>
      <script src="https://oss.maxcdn.com/html5shiv/3.7.2/html5shiv.min.js"></script>
      <script src="https://oss.maxcdn.com/respond/1.4.2/respond.min.js"></script>
    <![endif]-->
    <!-- 一定不要忘记引入bootstrap 的样式文件 -->
    <link rel="stylesheet" href="bootstrap/css/bootstrap.min.css">
    <title>Document</title>
    <style>
        .row>div {
            height: 50px;
            background-color: pink;
            /* margin: 0 10px; */
        }
    </style>
</head>

<body>
    <div class="container">
        <div class="row">
            <div class="col-md-4">
                <!-- 我们列嵌套最好加1个行 row 这样可以取消父元素的padding值 而且高度自动和父级一样高 -->
                <div class="row">
                    <div class="col-md-4">a</div>
                    <div class="col-md-8">b</div>
                </div>
            </div>
            <div class="col-md-4">2</div>
            <div class="col-md-4">3</div>
        </div>
    </div>
</body>
```

**效果**：

![](images\07.jpg)

##### 5. 列偏移

- 使用 .col-md-offset-* 类可以将列向右侧偏移。
- 这些类实际是通过使用 * 选择器为当前元素增加了左侧的边距（margin）。

**列偏移效果如下**：

![](images\08.jpg)

**列偏移语法如下**：

```html
 <!-- 列偏移 -->
  <div class="row">
      <div class="col-lg-4">1</div>
      <!-- 占4份，并且向右偏移4份 -->
      <div class="col-lg-4 col-lg-offset-4">2</div>
  </div>

```

**代码**：

```html
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <!--[if lt IE 9]>
      <script src="https://oss.maxcdn.com/html5shiv/3.7.2/html5shiv.min.js"></script>
      <script src="https://oss.maxcdn.com/respond/1.4.2/respond.min.js"></script>
    <![endif]-->
    <!-- 一定不要忘记引入bootstrap 的样式文件 -->
    <link rel="stylesheet" href="bootstrap/css/bootstrap.min.css">
    <title>Document</title>
    <style>
        .row div {
            height: 50px;
            background-color: pink;
        }
    </style>
</head>

<body>
    <div class="container">
        <div class="row">
            <div class="col-md-3">左侧</div>
            <!-- 如果有俩盒子，想左右排列：偏移的份数就是： 12 - 两个盒子的份数 = 6 -->
            <div class="col-md-3 col-md-offset-6">右侧</div>
        </div>
        <div class="row">
            <!-- 如果只有一个盒子想居中 ：偏移的份数 = (12 - 8) /2 -->
            <div class="col-md-8 col-md-offset-2">中间盒子</div>
        </div>

    </div>
</body>
```

**效果**：

![](images\09.jpg)

##### 6. 列排序

- 有时候，我们希望左侧盒子与右侧盒子的顺序进行颠倒，那么这时候就需要用到列排序了
- 但是它这个排序不是添加序号，而是使用push和pull，推和拉来改变
- 通过使用 .col-md-push-* 和 .col-md-pull-* 类就可以很容易的改变列（column）的顺序

**列排序效果**：

![](images\10.jpg)

**列排序语法**：

```html
 <!-- 列排序 -->
  <div class="row">
  	  <!-- 将左侧4份盒子，向右推8份的距离-->
      <div class="col-lg-4 col-lg-push-8">左侧</div>
      <!-- 将右侧8份盒子，向左拉4份的距离-->
      <div class="col-lg-8 col-lg-pull-4">右侧</div>
  </div>
<!-- 怎么理解推和拉的方向？
	假设，人站在界面左侧：
		想将元素向右移动，那就是推，推过去。
		想将元素向左移动，那就是拉，拉过来。
-->

```

**代码**：

```html
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <!--[if lt IE 9]>
      <script src="https://oss.maxcdn.com/html5shiv/3.7.2/html5shiv.min.js"></script>
      <script src="https://oss.maxcdn.com/respond/1.4.2/respond.min.js"></script>
    <![endif]-->
    <!-- 一定不要忘记引入bootstrap 的样式文件 -->
    <link rel="stylesheet" href="bootstrap/css/bootstrap.min.css">
    <title>Document</title>
    <style>
        .row div {
            height: 50px;
            background-color: pink;
        }
    </style>
</head>

<body>
    <div class="container">
        <div class="row">
            <div class="col-md-4 col-md-push-8">左侧</div>
            <div class="col-md-8 col-md-pull-4">右侧</div>
        </div>
    </div>
</body>
```

**效果**：

![](images\11.jpg)





##### 7. 响应式工具

- 为了加快对移动设备友好的页面开发工作，
- 利用媒体查询功能，
- 并使用这些工具类可以方便的针对不同设备展示或隐藏页面内容。

比如：

在大屏下，淘宝的第三列是显示的：

![](images\t01.jpg)

但是在小屏下，隐藏：

![](images\t2.jpg)

**语法**：

![](./images/2.jpg)

**代码**：

```html
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <!--[if lt IE 9]>
      <script src="https://oss.maxcdn.com/html5shiv/3.7.2/html5shiv.min.js"></script>
      <script src="https://oss.maxcdn.com/respond/1.4.2/respond.min.js"></script>
    <![endif]-->
    <!-- 一定不要忘记引入bootstrap 的样式文件 -->
    <link rel="stylesheet" href="bootstrap/css/bootstrap.min.css">
    <title>Document</title>
    <style>
        .row div {
            height: 300px;
            background-color: purple;
        }
        
        .row div:nth-child(3) {
            background-color: pink;
        }
        
        span {
            font-size: 50px;
            color: #fff;
        }
    </style>
</head>

<body>
    <div class="container">
        <div class="row">
            <div class="col-xs-3">
                <!--只有在超大屏幕显示-->
                <span class="visible-lg">我会显示哦</span>
            </div>
            <div class="col-xs-3">2</div>
            <!-- 中屏幕，超小屏幕隐藏 -->
            <div class="col-xs-3 hidden-md hidden-xs">我会变魔术哦</div>
            <div class="col-xs-3">4</div>
        </div>

    </div>
```

**效果**：

大屏幕：

![](images\h01.jpg)

中屏幕：

![](images\h02.jpg)

小屏幕：

![](images\h03.jpg)

超小屏幕：

![](images\h04.jpg)

### 3. 阿里百秀案例制作

![](images\a02.png)

#### 3.1 技术选型

方案：我们采取响应式页面开发方案

技术：bootstrap框架

设计图： 本设计图采用 1280px 设计尺寸

#### 3.2 案例分析

##### 1. **界面布局分析**：

![](images\a01.png)

##### 2. 屏幕划分分析

- 屏幕缩放发现 中屏幕 和 大屏幕布局 是一致的。 因此我们列 定义为 col-md- 就可以了， md 是大于等于 970 以上的
- 屏幕缩放发现  小屏幕 布局发生变化，因此我们需要为 小屏幕根据需求改变布局
- 屏幕缩放发现  超小屏幕布局又发生变化，因此我们需要为 超小屏幕根据需求改变布局
- 策略：  我们先布局  md以上的 pc端布局，最后根据实际需求在修改 小屏幕 和 超小屏幕的 特殊布局样式

中屏幕：

![](images\a-m.jpg)

小屏幕：

![](images\a-sm.jpg)

超小屏幕：

![](images\a-xs.jpg)

#### 3.2 项目结构搭建

Bootstrap 使用四步曲： 

1. 创建文件夹结构  

   ![](images\a03.jpg)

2. 创建 html 骨架结构  

3. 引入相关样式文件  ，新建index.css

4. 书写内容 

上三步代码：

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <!--[if lt IE 9]>
      <script src="https://oss.maxcdn.com/html5shiv/3.7.2/html5shiv.min.js"></script>
      <script src="https://oss.maxcdn.com/respond/1.4.2/respond.min.js"></script>
    <![endif]-->
    <!-- 引入bootstrap 样式文件 -->
    <link rel="stylesheet" href="bootstrap/css/bootstrap.min.css">
    <!-- 引入我们自己的首页样式文件 -->
    <link rel="stylesheet" href="css/index.css">
    <title>Document</title>
</head>

<body>
    123
</body>

</html>
```

#### 3.3 container宽度修改

因为本效果图采取 1280的宽度， 而Bootstrap 里面 container宽度 最大为 1170px，因此我们需要手动改下container宽度。

在index.css中添加，如下代码：

```css
/* 修改container的最大宽度为 1280 根据设计稿来走的 */

@media screen and (min-width: 1280px) {
    .container {
        width: 1280px;
    }
}

```

#### 3.4 19-阿里百秀logo制作

**logo效果**：

![](images\a04.jpg)

**结构**：

```html
<body>
    <div class="container">
        <div class="row">
            <header class="col-md-2">
                <div class="logo">
                    <a href="#">
                        <img src="images/logo.png" alt="" >
                    </a>
                </div>
                <div class="nav"></div>
            </header>
            <article class="col-md-7">
			中间
            </article>
            <aside class="col-md-3">右侧
            </aside>
        </div>
    </div>
</body>
```

**样式**：

```css
/* header */

header {
    padding-left: 0!important;
}

.logo {
    background-color: #429ad9;
}

.logo img {
     width: 100%; 
}
```

**效果**：

![](images\a05.jpg)



#### 3.5 20-阿里百秀nav制作引入字体图标

**导航效果**：

![](images\a06.jpg)

**结构**：

```html
    <div class="nav">
      <ul>
          <li><a href="#" class="glyphicon glyphicon-camera">生活馆</a></li>
          <li><a href="#" class="glyphicon glyphicon-picture">自然汇</a></li>
          <li><a href="#" class="glyphicon glyphicon-phone">科技湖</a></li>
          <li><a href="#" class="glyphicon glyphicon-gift">奇趣事</a></li>
          <li><a href="#" class="glyphicon glyphicon-glass">美食杰</a></li>
      </ul>
   </div>
```

**样式**：

```css
.nav {
    background-color: #eee;
    border-bottom: 1px solid #ccc;
}

.nav a {
    display: block;
    height: 50px;
    line-height: 50px;
    padding-left: 30px;
    font-size: 16px;
}

.nav a:hover {
    background-color: #fff;
    color: #333;
}

.nav a::before {
    vertical-align: middle;
    padding-right: 5px;
}
ul {
    list-style-type: none;
    margin: 0;
    padding: 0;
}

a {
    color: #666;
    text-decoration: none;
}

a:hover {
    text-decoration: none;
}

```

**效果**：

![](images\a07.jpg)

#### 3.6 21-阿里百秀news制作（上）

**中间新闻模块**：

![](images\a08.jpg)

**结构**：

```html
 <article class="col-md-7">
   	<!-- 新闻 -->
   	<div class="news">
   	    <ul>
   	        <li>
   	            <a href="#">
   	                <img src="upload/lg.png" alt="">
   	                <p>阿里百秀</p>
   	            </a>
   	        </li>
   	       <li>2</li>
   	       <li>3</li>
   	       <li>4</li>
   	       <li>5</li>
   	    </ul>
   	</div>
   	<!-- 发表 -->
   	<div class="publish"><div>
 </article>
```

**样式**：

```css
.news li {
    float: left;
    width: 25%;
    height: 128px;
    padding-right: 10px;
}
.news li a {
    position: relative;
    display: block;
    width: 100%;
    height: 100%;
}

.news li:nth-child(1) {
    width: 50%;
    height: 266px;
}

.news li:nth-child(1) p {
    line-height: 41px;
    font-size: 20px;
}

.news li a img {
    width: 100%;
    height: 100%;
}

.news li a p {
    position: absolute;
    bottom: 0;
    left: 0;
    width: 100%;
    height: 41px;
    padding: 0px 10px;
    margin-bottom: 0;
    background: rgba(0, 0, 0, .5);
    font-size: 12px;
    color: #fff;
}
```

**效果**：

![](images\a09.jpg)

#### 3.7 22-阿里百秀news制作（下）

结构：

```html
 <!-- 新闻 -->
 <div class="news">
     <ul>
         <li>
             <a href="#">
                 <img src="upload/lg.png" alt="">
                 <p>阿里百秀</p>
             </a>
         </li>
         <li>
             <a href="#">
                 <img src="upload/1.jpg" alt="">
                 <p>奇了 成都一小区护卫长得像马云 市民纷纷求合影</p>
             </a>
         </li>

         <li>
             <a href="#">
                 <img src="upload/2.jpg" alt="">
                 <p>奇了 成都一小区护卫长得像马云 市民纷纷求合影</p>
             </a>
         </li>

         <li>
             <a href="#">
                 <img src="upload/3.jpg" alt="">
                 <p>奇了 成都一小区护卫长得像马云 市民纷纷求合影</p>
             </a>
         </li>

         <li>
             <a href="#">
                 <img src="upload/4.jpg" alt="">
                 <p>奇了 成都一小区护卫长得像马云 市民纷纷求合影</p>
             </a>
         </li>

     </ul>
 </div>
```

样式：

```css
.news li a p {
    padding: 5px 10px; /*修改*/
}
.news li:nth-child(1) p {
    padding: 0 10px; /*增加*/
}
.news li {
    margin-bottom: 10px;/*增加*/
}
```

效果：

![](images\a10.jpg)

#### 3.8 23-阿里百秀publish模块制作

发布模块：

![](images\a11.jpg)

在超小屏幕下发现布局改变了：

![](images\a11-xs.jpg)

结构：

```html
//news清除浮动：
 <!-- 新闻 -->
 <div class="news clearfix">
 </div>
 <!-- 发表  这个模块里用到了大量的bootstrap的样式 
	分12份的时候，用的类前缀为啥是col-sm-？
	是因为我们发现只有在超小屏幕下有变化，大于小屏sm都一样
-->
<div class="publish">
    <div class="row">
        <div class="col-sm-9">
            <h3>生活馆 关于指甲的10个健康知识 你知道几个？</h3>
            <p class="text-muted">alibaixiu 发布于 2015-11-23</p>
            <p >指甲是经常容易被人们忽略的身体部位， 事实上从指甲的健康状况可以看出一个人的身体健康状况， 快来看看10个暗藏在指甲里知识吧！</p>
            <p class="text-muted">阅读(2417)评论(1)赞 (18) 标签：健康 / 感染 / 指甲 / 疾病 / 皮肤 / 营养 / 趣味生活
            </p>
        </div>
        <div class="col-sm-3">
            <img src="upload/3.jpg" alt="">
        </div>
    </div>
    <!--总共五行，再复制4个div即可-->
</div>
```

样式：

```css
.publish {
    border-top: 1px solid #ccc;
}
.publish .row {
    border-bottom: 1px solid #ccc;
    padding: 10px 0;
}
.pic {
    margin-top: 10px;
}
.pic img {
    width: 100%;
}
```

效果：

![](images\a12.jpg)

#### 3.10 24-阿里百秀aside模块制作

右侧模块：

![](images\a13.jpg)

结构：

```html
<aside class="col-md-3">
     <a href="#" class="banner">
         <img src="upload/zgboke.jpg" alt="">
     </a>
     <a href="#" class="hot">
         <span class="btn btn-primary">热搜</span>
         <h4 class="text-primary">欢迎加入中国博客联盟</h4>
         <p>这里收录国内各个领域的优秀博客，是一个全人工编辑的开放式博客联盟交流和展示平台......</p>
     </a>
 </aside>
```

样式：

```css
.banner img {
    width: 100%;
}

.hot {
    display: block;
    margin-top: 20px;
    padding: 0 20px 20px;
    border: 1px solid #ccc;
}

.hot span {
    border-radius: 0;
    margin-bottom: 20px;
}

.hot p {
    font-size: 12px;
}
```

效果：

![](images\a14.jpg)

#### 3.11 25-阿里百秀logo响应式制作

我们要做的是响应式界面，那么在不同分辨率下，界面布局是不一样的，我们先来处理logo：

小屏幕下，这个图片是居中显示的：

![](images\ax02.jpg)

超小屏幕下：图片没了，换成了文字：阿里百秀。

![](images\ax01.jpg)

结构：

```html
<div class="logo">
     <a href="#">
         <!--超小屏幕不显示-->
         <img src="images/logo.png" alt="" class="hidden-xs">
         <!--超小屏幕显示-->
         <span class="visible-xs">阿里百秀</span>
     </a>
 </div>
```

样式：

```css
/* 将logo显示风格改变，图片不再百分百显示，而是居中显示  */
.logo img {
    display: block;
    /* width: 100%; */   /*注意：这个百分百是与父亲一般宽，父亲宽度变化，与其一起变化*/
    /* logo图片不需要放大，缩小还是需要的 */
    max-width: 100%; /*注意：这个max-width:100%，指的是最大的宽度是有限制的，限制为自身宽度，意思就是不会放大但是还可以缩小  */
    margin: 0 auto;
}


/* 1.我们如果进入了超小屏幕下  logo里面的图片就隐藏起来 在结构中添加了hidden-xs*/


/* 2. 我们事先准备好一个盒子 在logo里面，它平时是隐藏起来的，只有在超小屏幕下显示 */

.logo span {
    display: block;
    height: 50px;
    line-height: 50px;
    color: #fff;
    font-size: 18px;
    text-align: center;
}
```

##### 问题：

width:100%;与max-width:100%的区别：

- width:100%，这个参照父级，父级变大变小，都跟着一起变化。
- max-width:100%，这个依然是参照父级变化，但是有个最大值的现在，最大为自身宽度，但是可以变小



#### 3.12 26-阿里百秀nav响应式制作

发现在小屏幕和超小屏幕下，导航就一行显示了：

![](images\ax03.jpg)

样式：只需要修改样式即可

```css
/* 当我们进入 小屏幕 还有 超小屏幕的时候 我们 nav 里面的li 浮动起来 并且宽度为 20%  */

@media screen and (max-width: 991px) {
    .nav li {
        float: left;
        width: 20%;
    }
}
/* 当我们进入 超小屏幕的时候 我们 nav 文字会变成14px  */

@media screen and (max-width: 767px) {
    .nav li a {
        font-size: 14px;
    }
}

```



#### 3.13 27-阿里百秀news响应式制作

小屏幕下，article要添加间距：

![](images\ax04.jpg)

代码：

```css

@media screen and (max-width: 991px) { /*增加如下*/
    article {
        margin-top: 10px;
    }
}
```

背景颜色： body是灰色的，容器是白色的：

![](images\ax05.jpg)

代码：

```css
body {
    background-color: #f5f5f5;
}

.container {
    background-color: #fff;
}
```

新闻在超小屏幕下： 第一个盒子百分百，后边都是百分之50

![](images\ax06.jpg)

代码：

```css
@media screen and (max-width: 767px) { /*增加如下*/
    /* 当我们处于超小屏幕 news 第一个li 宽度为 100%  剩下的小li  各 50% */
    .news li:nth-child(1) {
        width: 100%!important;
    }
    .news li {
        width: 50%!important;
    }
}
```



#### 3.14 28-阿里百秀publish响应式制作

**导航文字**：

![](images\ax07.jpg)

**代码**：

```css
@media screen and (max-width: 767px) {
    .nav li a {
        font-size: 14px;
        padding-left: 3px; /*增加*/
    }
}
```

**效果**：

![](images\ax072.jpg)



**发布模块**，在超小屏幕下，很多东西是不显示的：

![](images\ax08.jpg)

**结构**：

```html
<div class="row"> <!-- 这里增加了很多hidden-xs样式 -->
    <div class="col-sm-9">
        <h3>生活馆 关于指甲的10个健康知识 你知道几个？</h3>
        <p class="text-muted hidden-xs">alibaixiu 发布于 2015-11-23</p>
        <p class="hidden-xs">指甲是经常容易被人们忽略的身体部位， 事实上从指甲的健康状况可以看出一个人的身体健康状况， 快来看看10个暗藏在指甲里知识吧！</p>
        <p class="text-muted">阅读(2417)评论(1)赞 (18) <span class="hidden-xs">标签：健康 / 感染 / 指甲 / 疾病 / 皮肤 / 营养 / 趣味生活</span>

        </p>
    </div>
    <div class="col-sm-3 pic hidden-xs">
        <img src="upload/3.jpg" alt="">
    </div>
</div>
```

**样式**：

```css

@media screen and (max-width: 767px) { /*增加*/
    .publish h3 {
        font-size: 14px;
    }
}
```



#### 3.15 29-移动端开发总结

- 流式布局（百分比布局）
- **flex 弹性布局（推荐）**
- **rem适配布局（推荐）**
- 响应式布局

建议：  我们选取一种主要技术选型， 其他技术做为辅助，这种混合技术开发

##### 阿里百秀项目总结：

以上的案例，我们利用bootstrap做响应式开发（界面布局变化），只用到了两点：

1. hidden+visible  （某些屏幕下，某些元素显示或者隐藏）

   ```html
   <div class="logo">
        <a href="#">
            <!--超小屏幕不显示-->
            <img src="images/logo.png" alt="" class="hidden-xs">
            <!--超小屏幕显示-->
            <span class="visible-xs">阿里百秀</span>
        </a>
    </div>
   ```

2. 媒体查询，设置元素不同占比

   ```css
   @media screen and (max-width: 991px) {
       .nav li {
           float: left;
           width: 20%;
       }
   }
   ```

3. 指定多个不同屏幕的col类（这一点在项目中没有用到）

   ```html
   <body>
       <div class="container">
           <div class="row">
               <div class="col-lg-3 col-md-4 col-sm-6 col-xs-12">1</div>
               <div class="col-lg-3 col-md-4 col-sm-6 col-xs-12">2</div>
               <div class="col-lg-3 col-md-4 col-sm-6 col-xs-12">3</div>
               <div class="col-lg-3 col-md-4 col-sm-6 col-xs-12">4</div>
           </div>
       </div>
   </body>
   ```

   


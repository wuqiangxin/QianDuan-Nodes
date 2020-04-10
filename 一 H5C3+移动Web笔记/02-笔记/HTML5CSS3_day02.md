# day02 - 移动web开发_H5C3

## 1. 2D转换（变换）transform

转换（transform）是CSS3中具有颠覆性的特征之一，可以实现元素的位移、旋转、变形、缩放。

- 缩放：scale
- 移动：translate
- 旋转：rotate
- 倾斜：skew （不介绍，感兴趣自己看：<https://blog.csdn.net/alwayssmlilewpc/article/details/79890004>）

2d转换是改变标签在**2维平面**上的**位置和形状**的一种技术，我们先来学习2维坐标系。

### 1.1. 2维坐标系

**2维坐标系**其实就是指布局的时候的坐标系 如图

![1524965494414](medias/1524965494414.png)

### 1.2. 2d移动 translate

2d移动是2d转换里面的一种功能，可以改变元素在页面中的位置，类似 **定位**

使用2d移动的步骤：

1. 给元素添加 **转换属性**  `transform`
2. 属性值为 `translate(x,y)`  如  `transform:translate(50px,50px)`;

```css
  div{
    transform: translate(50px,50px);
    /*transform：改变；translate：有移动的意思
    理解，我要改变这个div，怎么改变呢？通过移动来改变div的位置。
    注意：这个操作没有动画过程，是直接瞬间向下向右移动了50px
    还可以分开写：
      transform:translateX(50px);
      transform:translateY(50px);
      */
  }
```

![1524965782388](media/1524965782388.png)

**小结**:

1. **translate**中的百分比单位是相对于自身元素的  `translate:(50%,50%);`
2. **translate**类似定位，不会影响到其他元素的位置
3. 对行内标签没有效果

### 1.3. 2d旋转 rotate

#### 1.3.1 rotate介绍

2d旋转指的是让元素在2维平面内顺时针旋转或者逆时针旋转

使用步骤：

1. 给元素添加转换属性 `transform`
2. 属性值为 `rotate(角度)`  
3. 如 `transform:rotate(30deg)`  顺时针方向旋转**30度**
4. 代码：

```css
div{
      transform: rotate(0deg);
      // rotate：旋转
      // deg：degree：度
}
```

在浏览器中手动修改 **rotate** 的效果：

![4](media/4.gif)

观察过后，2d旋转有以下特点

1. 角度为正时 顺时针 负时 为逆时针
2. 默认旋转的中心点是元素的中心点
3. **注意**：这个其实也没有动画过程，我们在演示的时候，是在浏览器中手动修改了rotate这个值，角度一直改变，才出现上图旋转效果

#### 1.3.2 案例：三角箭头旋转

效果：

默认效果：

![](medias\arrow1.jpg)

鼠标悬浮效果：做动画向上转动

![](medias\arrow2.jpg)

代码：

```html
 <head>
	<style>
        div {
            position: relative;
            width: 249px;
            height: 35px;
            border: 1px solid #000;
        }
        
        div::after { /*小三角通过微元素来处理 ： 通过只显示两个方向的边框来控制显示三角*/
            content: "";
            position: absolute;
            top: 8px;
            right: 15px;
            width: 10px;
            height: 10px;
            border-right: 1px solid #000;
            border-bottom: 1px solid #000;
            transform: rotate(45deg);
            transition: all 0.2s; /* transition：过渡，有动画过程 ；all代表所有变化属性都做动画*/
        }
        /* 鼠标经过div  里面的三角旋转 */
        
        div:hover::after {
            transform: rotate(225deg);
        }
    </style>
</head>

<body>
    <div></div>
</body>
```

#### 1.3.3 转换中心 transform-origin 了解

该属性可以修改元素旋转的时候的中心点。

origin：原点，如果与rotate旋转配合使用，就是旋转的中心点。如果与scale配合使用，就是缩放的基准点。

**语法**： `transform-origin: x y;`

**注意**：

- 注意后面的参数 x 和 y 用空格隔开
- x y **默认转换的中心点是元素的中心点** (50%  50%)
- 还可以给x y 设置 像素 或者  方位名词  （top  bottom  left  right  center）

**常见写法**：

1. transform-origin:**50% 50%;**  默认值  元素的中心位置 百分比是相对于自身的宽度和高度
2. transform-origin:**top left;**  左上角   和 transform-origin：0 0;相同
3. transform-origin:**50px 50px;**  距离左上角 50px 50px 的位置
4. transform-origin：**0**;  只写一个值的时候  第二个值默认为 50%;

案例：

效果：

![](medias\rotate.gif)

代码：

```html
   <style>
        div {
            overflow: hidden;
            width: 200px;
            height: 200px;
            border: 1px solid pink;
            margin: 10px;
            float: left;
        }
        
        div::before { /* 通过伪元素来处理旋转的红色内容 */
            content: "黑马";
            display: block;
            width: 100%;
            height: 100%;
            background-color: hotpink;
            transform: rotate(180deg);
            transform-origin: left bottom;
            transition: all 0.4s;
        }
        /* 鼠标经过div 里面的before 复原 */
        div:hover::before {
            transform: rotate(0deg);
        }
    </style>
</head>

<body>
    <div></div>
</body>
```



### 1.4. 2d缩放 scale

#### 1.4.1 scale介绍

缩放，顾名思义，可以放大和缩小。 只要给元素添加上了这个属性就能控制它放大还是缩小 

**语法**： `transform:scale(x,y);`

**步骤**：

1. 给元素添加转换属性 `transform`
2. 转换的属性值为 `scale(宽的倍数,高的倍数)`    
3. 如 宽变为两倍，高变为3倍 `transform:scale(2,3)`
4. 代码：

```css
div{
    transform:scale(2,3);
    //scale：比例的意思，理解为按照比例缩放。
}
```

**分析图**：

![1524966701225](media/1524966701225.png)

**注意**：

- 注意其中的x和y用逗号分隔
- transform:scale(1,1) ：宽和高都放大一倍，相对于没有放大
- transform:scale(2,2) ：宽和高都放大了2倍
- transform:scale(2) ：只写一个参数，第二个参数则和第一个参数一样，相当于 scale(2,2)
- transform:scale(0.5,0.5)：缩小
- sacle缩放最大的优势：可以设置转换中心点缩放，默认以中心点缩放的，而且不影响其他盒子（**相对于修改宽高而言：宽高修改之后会影响其他盒子**）



#### 1.4.2. 案例

##### 案例1：图片放大案例

**效果**：

![](medias\scale01.gif)

**代码**：

```html
    <style>
        div {
            overflow: hidden;
            float: left;
            margin: 10px;
        }
        
        div img {
            transition: all .4s;
        }
        
        div img:hover { /*鼠标悬浮之后，将img变大1.1倍*/
            transform: scale(1.1);
        }
    </style>
</head>

<body>
    <div>
        <a href="#"><img src="media/scale.jpg" alt=""></a>
    </div>
    <div>
        <a href="#"><img src="media/scale.jpg" alt=""></a>
    </div>
    <div>
        <a href="#"><img src="media/scale.jpg" alt=""></a>
    </div>
</body>
```

##### 案例2：分页按钮案例：

**效果**：

![](medias\scale02.gif)



**代码**：

```html
 <style>
        li {
            float: left;
            width: 30px;
            height: 30px;
            border: 1px solid pink;
            margin: 10px;
            text-align: center;
            line-height: 30px;
            list-style: none;
            border-radius: 50%;
            cursor: pointer;
            transition: all .4s;
        }
        
        li:hover {/*鼠标悬浮之后，将li变大1.2倍*/
            transform: scale(1.2);
        }
    </style>
</head>

<body>
    <ul>
        <li>1</li>
        <li>2</li>
        <li>3</li>
        <li>4</li>
        <li>5</li>
        <li>6</li>
        <li>7</li>
    </ul>
</body>
```

### 1.5. 综合写法&总结

综合写法注意：

1. 同时使用多个转换，其格式为：transform: translate() rotate() scale() ...等（**空格隔开多个转换**）
2. 其顺序会影转换的效果。（先旋转会改变坐标轴方向）
   1. transform:  translate(150px, 50px) rotate(180deg); 这个会在向右向下位移过程中进行旋转。
   2. transform: rotate(180deg) translate(150px, 50px);  这个会先旋转，旋转之后坐标轴方向颠倒了，然后他就会向左向上位移了。
3. 所以 当我们同时有位移和其他属性的时候，记得要将**位移**放到最前。

总结：

1. 转换transform 我们简单理解就是变形 有2D 和 3D 之分
2. 我们暂且学了三个 分别是 位移 旋转 和 缩放
3. 2D 移动 translate(x, y)   最大的优势是不影响其他盒子， 里面参数用%，是相对于自身宽度和高度来计算的
4. 可以分开写比如 translateX(x)  和 translateY(y)
5. 2D 旋转 rotate(度数)    可以实现旋转元素   度数的单位是deg
6. 2D 缩放 sacle(x,y)   里面参数是数字 不跟单位 可以是小数   最大的优势 不影响其他盒子
7. 设置转换中心点 transform-origin : x y;    参数可以百分比、像素或者是方位名词
8. 当我们进行综合写法，同时有位移和其他属性的时候，记得要将位移放到最前

## 2. 动画 animation

- 动画（animation）是CSS3中具有颠覆性的特征之一，
- 可通过设置多个节点来精确控制一个或一组动画，常用来实现复杂的动画效果。
- 相比较过渡，动画可以实现更多变化，更多控制，连续自动播放等效果。
- 初学者容易对 **动画** 和 **过渡** 傻傻分不清楚
- 过渡 只能看到一次变化过程 如 **宽度  1000px  变化到  100px** 

- **动画 可以设置变化的次数 甚至是无数次**   


![](media\animate.gif)

### 2.1. 步骤

制作动画分为两步：

1. 在css中定义动画函数     
2. 给目标元素调用动画函数

![1524985595597](media/1524985595597.png)

代码如下：

```css
    /* 1 声明动画函数  */
    @keyframes ani_div {
      0%{
        width: 100px;
        background-color: red;
      }
      50%{
        width: 150px;
        background-color: green;
      }
      100%{
        width: 300px;
        height: 300px;
        background-color: yellow;
      }
    }
/*keyframes关键帧，理解，定义动画就是定义动画过程中的几个关键帧，然后根据关键帧依次变化*/

    div {
      width: 200px;
      height: 200px;
      background-color: aqua;
      margin: 100px auto;
      /* 2 调用动画 */
      animation-name: ani_div;
      /* 持续时间 */
      animation-duration: 2s;
    }
```

动画序列：

- 0% 是动画的开始，100% 是动画的完成。这样的规则就是动画序列。
- 在 @keyframes 中规定某项 CSS 样式，就能创建由当前样式逐渐改为新样式的动画效果。
- 动画是使元素从一种样式逐渐变化为另一种样式的效果。您可以改变任意多的样式任意多的次数。
- 请用百分比来规定变化发生的时间，或用关键词 "from" 和 "to"，等同于 0% 和 100%。

**总结**：

keyframes：关键帧，理解，定义动画就是定义动画过程中的几个关键帧，然后根据关键帧依次变化。

### 2.2. 语法

**动画常用属性**：

![](medias\animate-prop.jpg)

1. 动画名

   设置要使用的动画名 `animation-name:xxx;`

2. 持续时间

   设置动画播放的持续时间  `animation-duration:3s`

3. 速度曲线

   和设置过渡的速度曲线一样 `animation-timing-function:linear;`

   timing：定时。function：功能，作用

   - linear： 匀速  （linear：线性的）

     - 线性理解图：

     ![](media\linear-线性.png)

     **线性理解为匀速，如何理解**？ y=kx，比如k是速度，这个速度是固定的（匀速），那么x是时间，y就是距离。

   - ease： 慢-快-慢  默认值  （ease：减缓，这里理解为变化，速度是变化的）

   - ease-in： 慢-快。  （ease-in：in，在..里面，进入）

   - ease-out： 快-慢。（ease-out：out，在..外边，外部，离去）

   - ease-in-out： 慢-快-慢。

   **理解**：ease-in和ease-out的理解，这里我们把in和out理解为进入和离去。

   ​	    一个车进入你的视线，感觉上肯定是由慢到快  （ease-in）

   ​	    一个车离开你的视线，感觉上肯定是由快到慢（ease-out）

4. 延迟时间

   `animation-delay: 0s;`

5. 循环次数

   设置动画播放的循环次数  `animation-iteration-count: 2;` 

   可以指定数字，也可以指定 **infinite** ，infinite为无限循环

   interation：反复，循环

6. 循环方向

   `animation-direction`：direction：方向

   如在动画中定义了  **0%：红色**  **100%：黑色** 那么 当属性值为 

   1. **normal**  默认值  **红 -> 黑**
   2. **reverse** 反向运行    **黑 -> 红**  （reverse：反向，逆向播放）
   3. **alternate**  正-反-正...  **红 -> 黑 -> 红...**   （alternate：交替，轮流）
   4. **alternate-reverse**  反-正-反..   **黑 -> 红 -> 黑 ...** 
   5. 以上与循环次数有关 （如果是交替，那么循环次数最少为2，才能来回交替一次）

7. 动画等待或者结束的状态

   `animation-fill-mode` 设置动画在等待或者结束的时候的状态 。

   动画结束之后默认是回到初始状态：backwards。

   - **forwards**：动画结束后，元素样式停留在 100% 的样式  （forwards：向前）
   - **backwards**： 在延迟等待的时间内，元素样式停留在 0% 的样式 （backwards：向后）
   - **both**： 同时设置了 forwards和backwards两个属性值

   **理解**：fill：装满，理解为填充。动画结束之后填充为什么状态，以什么状态停留

   ​	    forwards，停留在100%，那就是向前不回头

   ​	    backwards，停留在0%，动画执行完成是在100%，又回到0%初始位置，那就是向后回头了。

8. 暂停和播放

   `animation-play-state`  控制 **播放** 还是 **暂停**   （animation-play-state：动画播放状态）

   `running` 播放   `paused` 暂停



### 2.3. 复合写法（简写）

动画简写语法：

```css
animation：动画名称 持续时间 运动曲线  何时开始  播放次数  是否反方向  动画起始或者结束的状态;
animation: name duration timing-function delay iteration-count direction fill-mode;
```

- 前边两个属性必须要写，后边的可以省略
- 简写属性里面不包含 animation-play-state 
- 暂停动画：animation-play-state:   puased;   经常和鼠标经过等其他配合使用
- 想要动画走回来 ，而不是直接跳回来：animation-direction   ：  alternate
- 盒子动画结束后，停在结束位置：  animation-fill-mode  ：   forwards 

### 2.4. 多个动画写法

用逗号分隔

```css
animation: name duration timing-function delay iteration-count direction fill-mode，
animation: name duration timing-function delay iteration-count direction fill-mode;
```

### 2.5. 动画结束事件animationend

元素在动画结束之后，会自动触发的事件 **animationend**   

```javascript
    var div = document.querySelector("div");
    div.addEventListener("animationend", function () {
      console.log("div的动画结束之后，触发");
    })
```

### 2.6 案例

#### 案例1：大数据热点图：

效果：

![](medias\hotpoints.gif)

代码：

```html
   <style>
        body {
            background-color: #333;
        }
        
        .map { /* 地图，水平居中，热点效果需要定位，所以子绝父相 */
            position: relative;
            width: 747px;
            height: 616px;
            background: url(media/map.png) no-repeat;
            margin: 0 auto;
        }
        
        .city { /* 北京 处理位置 */
            position: absolute;
            top: 227px;
            right: 193px;
            color: #fff;
        }
        
        .tb {/* 台北  */
            top: 500px;
            right: 80px;
        }
        
        .dotted { /* 小圆点 */
            width: 8px;
            height: 8px;
            background-color: #09f;
            border-radius: 50%;
        }
        
        .city div[class^="pulse"] {
            /* 保证我们小波纹在父盒子里面水平垂直居中 放大之后就会中心向四周发散 */
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            width: 8px;
            height: 8px;
            box-shadow: 0 0 12px #009dfd; /*阴影效果*/
            border-radius: 50%;
            animation: pulse 1.2s linear infinite;   /* 动画，匀速，无线循环  */
        }
        
        .city div.pulse2 {  /* 第二层波纹延迟0.4s */
            animation-delay: 0.4s;
        }
        
        .city div.pulse3 { /* 第三层波纹延迟0.8s */
            animation-delay: 0.8s;
        }
        /* 定义动画，0%默认,70%大小变大，透明度不变。100%继续变大，透明度变为0。
       	效果就是，波纹从小到70%越来越大，让再大的话就开始变虚。
       */
        @keyframes pulse {
            0% {}
            70% {
                /* transform: scale(5);  我们不要用scale 因为他会让 阴影变大*/
                width: 40px;
                height: 40px;
                opacity: 1;
            }
            100% {
                width: 70px;
                height: 70px;
                opacity: 0;
            }
        }
    </style>
</head>

<body>
    <div class="map">
        <div class="city"> <!-- 北京 -->
            <div class="dotted"></div> <!-- 小圆点 -->
            <div class="pulse1"></div> <!-- 波纹1 -->
            <div class="pulse2"></div> <!-- 波纹2 -->
            <div class="pulse3"></div> <!-- 波纹3 -->
        </div>
        <div class="city tb">
            <div class="dotted"></div>
            <div class="pulse1"></div>
            <div class="pulse2"></div>
            <div class="pulse3"></div>
        </div>
    </div>
</body>
```

#### 案例2：奔跑的熊大案例

在看案例2之前，我们需要来普及一个知识点：

##### 1. 速度曲线细节

animation-timing-function：规定动画的速度曲线，默认是“ease”

| 值          | 描述                                           |
| ----------- | ---------------------------------------------- |
| linear      | 动画从头到尾的速度是相同的。匀速               |
| ease        | 默认。动画以低速开始，然后加快，在结束前变慢。 |
| ease-in     | 动画以低速开始。                               |
| ease-out    | 动画以低速结束。                               |
| ease-in-out | 动画以低速开始和结束。                         |
| steps()     | 指定了时间函数中的间隔数量（步长）             |

之前已经介绍过除了steps之外的速度曲线了。我们来看一下steps()

代码：

```html
    <style>
        div {
            overflow: hidden;
            font-size: 20px;
            width: 0;
            height: 30px;
            background-color: pink;
            /* 让我们的文字强制一行内显示 */  //注意：这个强制换行可以不写
            /* white-space: nowrap; */
            /* steps 就是分几步来完成我们的动画 有了steps 就不要在写 ease 或者linear 了 */
            animation: w 4s steps(10) forwards;
        }
        
        @keyframes w {
            0% {
                width: 0;
            }
            100% {
                width: 200px;
            }
        }
    </style>
</head>

<body>
    <div>世纪佳缘我在这里等你</div>
</body>

```

理解： steps(n) : step意为**步长**，与linear和ease都属于属于速度曲线的一种，效果为 **分n步完成动画**。



##### 2. 案例开始：

效果：

![](medias\beer-run.gif)

代码：

```html
   <style>
        body {
            background-color: #ccc;
        }
        
        div {
            position: absolute;
            width: 200px;
            height: 100px;
            background: url(media/bear.png) no-repeat;
            /* 我们元素可以添加多个动画， 用逗号分隔 */
            animation: bear .4s steps(8) infinite, move 3s forwards;
        }
        
        @keyframes bear {
            0% {
                background-position: 0 0;
            }
            100% {
                background-position: -1600px 0;
            }
        }
        
        @keyframes move {
            0% {
                left: 0;
            }
            100% {
                left: 50%;
                /* margin-left: -100px; */
                transform: translateX(-50%);
            }
        }
    </style>
</head>

<body>
    <div></div>
</body>
```




## 3. 动画库animate.css  （暂不介绍）

封装了常见的有意思的小动画  **发疯似的建议看官网来学习使用**

[官网](https://daneden.github.io/animate.css/)

[中文](https://www.awesomes.cn/repo/daneden/animate-css)

### 3.1. 使用步骤

1. 引入css文件

   ```html
   <head>
     <link rel="stylesheet" href="animate.min.css">
   </head>
   ```

2. 给元素添加对应的class

   ```html
   <h1 class="animated infinite bounce">快来看看我</h1>
   ```

   简单解读：

   `animated`  必须添加的class 

   `infinite` 无限播放 

   `bounce` 弹跳动画的效果，可以查官网自己选择喜欢的

### 3.2. css3兼容处理

css3涉及到较多的新属性，某些低版本（如ie8以及以下）的浏览器对css3的支持程度不够，因此需要做以下处理

添加对应的浏览器的前缀 常见前缀如下

- 谷歌 -webkit
- 火狐 -moz
- IE -ms

如对 `border-radius` 进行兼容性处理   

```css
      -webkit-border-radius: 30px 10px;
      -moz-border-radius: 30px 10px;
      -ms-border-radius: 30px 10px;
	  // border-radius 一定要放在最后
      border-radius: 30px 10px;
```

如果发现添加前缀也解决不了兼容性问题，那么就不要使用该css3属性
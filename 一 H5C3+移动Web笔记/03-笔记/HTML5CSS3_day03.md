# day02 - 移动web开发_H5C3

## 1. 学习目标

- 理解
  - 3d转换的中的3d移动，3d旋转
  - 动画属性的设置和使用
  - animate.css动画库的使用
- 应用
  - 实现3d立方体
  - 实现3d轮播图
  - 无缝滚动
  - 正在等待图标的制作
  - 自己实现animate.css



## 2. 3D转换（变换）

3d转换是改变标签在3**坐标系**上的**位置和形状**的一种技术 

我们生活的环境是3D的，照片就是3D物体在2D平面呈现的例子。

3D特点：

- 近大远小。
- 物体后面遮挡不可见

![1563676213939](media\1563676213939.png)

### 2.1 3维坐标系

3维坐标系其实就是指立体空间，立体空间是由3个轴共同组成的  

- x轴 水平向右   注意： x 右边是正值，左边是负值 
- y轴 垂直向下   注意： y 下面是正值，上面是负值
- z轴 垂直屏幕 由屏幕里面指向屏幕的外面   注意： 往外面是正值，往里面是负值 

![img](medias/1943303239310571602.png)



**z轴理解**：

- 上图中的网格面板，即可理解为电脑屏幕。
- 眼睛到屏幕的线，就是z轴。 
- 眼睛离屏幕越近，z轴越小。进入屏幕是负值。

### 2.2 3d移动 translate3d

3d移动在2d移动的基础上多加了一个可以移动的方向，就是z轴方向

**语法：**

1. transform:**translate3d**(x,y,z)  其中 **x y z** 分别指要移动的轴的方向的距离
2. translform:**translateX**(100px)  仅仅是移动在x轴上移动
3. translform:**translateY**(100px)  仅仅是移动在Y轴上移动
4. translform:**translateZ**(100px)  仅仅是移动在Z轴上移动  

**代码**：

```html
    <style>
        
        div {
            width: 200px;
            height: 200px;
            background-color: pink;
            /* transform: translateX(100px);
            transform: translateY(100px); */
            /* transform: translateX(100px) translateY(100px) translateZ(100px); */
            /* 1. translateZ 沿着Z轴移动 */
            /* 2. translateZ 后面的单位我们一般跟px */
            /* 3. translateZ(100px) 向外移动100px （向我们的眼睛来移动的） */
            /* 4. 3D移动有简写的方法 */
            /* transform: translate3d(x,y,z); */
            /* transform: translate3d(100px, 100px, 100px); */
            /* 5. xyz是不能省略的，如果没有就写0 */
            transform: translate3d(400px, 100px, 100px);
        }
    </style>
</head>

<body>
    <div></div>
</body>
```

**注意**:

因为z轴是垂直屏幕，由里指向外面，所以 默认是看不到元素在z轴的方向上移动，想要看到，可以使用下面的 **视距** 属性设置



### 2.3. 视距 perspertive 了解

#### 2.3.1 介绍

- 人在看物体时，有个规律，如 **远的物体看起来小** **近的物体看起来大**   
- **perspertive** 视距：就是用来设置  **人** 和 **物体** 的距离      

![](media\toushi.jpg)

**上图总结**：

d：视距，眼睛到屏幕的距离，视距与物体大小的关系成反比。   (**近大远小  ： 视距变小，眼睛离屏幕越来越近，物体离眼睛越来越近，物体变大----近大** )

z：translateZ，物体距离屏幕的距离，z轴距离与物体大小的关系成正比。  (**近大远小：translateZ变大，物体离眼睛越近，物体变大 ----- 近大**)

z，并不是z轴，其实是translateZ。视距和translateZ其实都是在Z轴上的距离。  

perspective ，透视，理解为视距。 （也可以理解为3D眼睛，给元素添加3D效果，并且想看到，必须带上3D眼睛，给父亲添加perspective ）

**问题**：

z轴，是物体距离屏幕的距离，难道物体还能脱离屏幕跑出来么？如上图图1。

物体并不会脱离屏幕，上图中的物体其实是 虚线圆圈，我们真是看到的其实是屏幕上的实线圆圈。

真实情况就是物体与屏幕是没有距离的，但是你要把屏幕里的世界理解为3D世界，那么物体与屏幕就有距离了。那么CSS3就是利用了translateZ来表示物体与屏幕的距离，通过translateZ这个属性让物体变大变小。

**网络理解**：

- perspective字面意思是：透视。
- 在w3school中它的解释为：设置元素被查看位置的视图。
- 通俗讲，就是我们看看一个物体的所处的视角，近大远小。
- 就比如我们正对着电脑：当我无限贴近电脑屏幕的时候，电脑的屏幕就无限大；
- 当我们站起来远离电脑的时候，电脑的屏幕就无限变小。

**例子**：

如 我们想要看到 物体 在z轴上的移动  的 **远大近小** 效果时  

1. 设置物体的 `translateZ` 一般大于 0  如  `transform:translateZ(100px)`
2. 设置 人和物体的距离 （ 视距）    这个值规定要设置给**物体的父元素**   `perspertive:1000px`
3. 动态改变物体的 `translateZ` 即可观察效果

```css
    /* 父元素 */
    body {
      /* 视距 */
      perspective: 1000px;
    }

    /* 目标 */
    div {
      width: 200px;
      height: 200px;
      background-color: aqua;
      margin: 100px auto;
      /* z轴的移动 */
      transform: translateZ(0px);
    }
```

![5](media/5.gif)

**注意**： 这个效果很像放大效果，但其实是不一样的。

#### 2.3.2. perspertive与translateZ

d：视距，眼睛到屏幕的距离，视距与物体大小的关系成反比。

z：translateZ，物体距离屏幕的距离，轴距离与物体大小的关系成正比。

从上述结果中发现，perspective与translateZ都可以调整物体的大小。那么我们要使用哪个呢？

perspective是给父元素添加的，而translateZ是给自己添加的。

我们可能会碰到这样的情况，一个父盒子中有多个子盒子。我们给父盒子设置一个固定的视距perspective，然后子盒子设置不同的translateZ，这样子盒子就会有一个相同视距下的不同的大小。

而且，物体想实现3D效果，必须添加透视perspective。

**如何使用**：

父元素添加一个固定的perspective，子元素再添加translateZ，才会有3D效果。

必须配合使用。

虽然两个都可以让盒子大小改变，但是必须配合使用才行。

让盒子变大变小，一般不会改变perspective，而是是调整translateZ来改变。



#### 2.3.2. 小结

1. translateZ的值和perspertive都要大于0 否则容易出现兼容性问题

2. translateZ：近大远小（translateZ距离近（值越大）物体越大，近大）

3. translateZ：往外是正值

4. translateZ：往里是负值




### 2.4. 3d旋转 rotate3d

#### 2.4.1 介绍

3d旋转指可以让元素在3维平面内沿着 **x轴，y轴，z轴或者自定义轴**进行旋转  

语法：

```html
transform:rotateX(45deg)：沿着x轴正方向旋转 45度
transform:rotateY(45deg) ：沿着y轴正方向旋转 45deg
transform:rotateZ(45deg) ：沿着Z轴正方向旋转 45deg
transform:rotate3d(x,y,z,deg)： 沿着自定义轴旋转 deg为角度（了解即可）
```

效果如图：

![](media\rotate3D.gif)

#### 2.4.2 rotateX

效果图：

![](media\rotateX.gif)

##### 1. **X旋转示例**：

```html
   <style>
        body {
            perspective: 300px;
        }
        
        img {
            display: block;
            margin: 100px auto;
            transition: all 1s;
        }
        
        img:hover {
            transform: rotateX(45deg); /* 图片向后倒，向屏幕内部倒 */
            transform: rotateX(-45deg); /* 图片向前倾，向屏幕外部倒  */
        }
    </style>
</head>

<body>
    <img src="media/pig.jpg" alt="">
</body>
```

发现旋转的度数有正负，正负值往哪边旋转，这个是有规律的。我们看左手准则：

##### 2. **左手准则：**

对于元素旋转的方向的判断 我们需要先学习一个**左手准则**

比如要判断某元素沿着x轴是怎么旋转的

1. 左手的手拇指指向 x轴的正方向
2. 其余手指的弯曲方向就是该元素沿着x轴旋转的方向了

![1523585209390](medias/1523585209390.png)

**总结**：rotateX( 正值 )，旋转方向是向后倒，向屏幕里旋转。

#### 2.4.3 rotateY

效果图：

![](media\rotateY.gif)

##### 1. Y旋转示例：

```html
    <style>
        body {
            perspective: 500px;
        }
        
        img {
            display: block;
            margin: 100px auto;
            transition: all 1s;
        }
        
        img:hover {
            transform: rotateY(45deg); /* 右边向里旋转*/
            transform: rotateY(-45deg); /* 左边向里旋转*/
        }
    </style>
</head>

<body>
    <img src="media/pig.jpg" alt="">
</body>
```

Y轴方向旋转的正负值，也是影响了旋转的方向，方向如何区分？依然看左手准则：

##### 2. 左手准则：

- 左手的手拇指指向 y轴的正方向
- 其余手指的弯曲方向就是该元素沿着y轴旋转的方向（正值）
- 如图：

![](media\rotateY-zhunze.jpg)

#### 2.4.4 rotateZ

效果图：

![](media\rotateZ.gif)

##### 1. Z旋转示例：

```html
    <style>
        body {
            perspective: 500px;
        }
        
        img {
            display: block;
            margin: 100px auto;
            transition: all 1s;
        }
        
        img:hover {
            transform: rotateZ(180deg); /* 顺时针旋转*/
            transform: rotateZ(-180deg); /* 逆时针旋转*/
        }
    </style>
</head>

<body>
    <img src="media/pig.jpg" alt="">
</body>
```

##### 2. 左手准则

z轴正方向是屏幕到眼睛的方向，四指的方向是顺时针方向（反之逆时针）

![](media\rotate-z-zhunze.jpg)

#### 2.4.5 rotate3d-自定义轴 （了解）

**语法**：

```
transform:rotate3d(x,y,z,deg)： 沿着自定义轴旋转 deg为角度（了解即可）
```

- xyz是表示旋转轴的矢量，是标示你是否希望沿着该轴旋转，最后一个标示旋转的角度。
- transform:rotate3d(1,0,0,45deg) 就是沿着x轴旋转 45deg
- transform:rotate3d(1,1,0,45deg) 就是沿着对角线旋转 45deg

**理解**：

矢量（vector）是一种既有大小又有方向的量，又称为向量。

xyz是矢量，x指定1说明沿着x轴旋转。0说明不沿着x轴旋转。（0，1有大小，又代表x或y或z，也有方向）

**代码分析图**：

![](media\rotate3d.jpg)

### 2.5 3D呈现 transform-style 

#### 2.5.1 介绍

- 控制子元素是否开启三维立体环境。
- transform-style: flat 子元素不开启3d立体空间  默认的   （flat：平的，平面）
- transform-style: preserve-3d; 子元素开启立体空间  （preserve：[prɪˈzɜ:v] 保持）
- 代码写给父级，但是影响的是子盒子
- **perspective是开启3D效果，transform-style: preserve-3d是保持3D效果**  ***
- 这个属性很重要，后面必用

![](medias\transform-style.jpg)



上图效果不佳，看下图：

![](media\pingmian.jpg)



**完整代码**：

```html
    <style>
        body { 
            perspective: 500px; /* 让子盒子有3D效果，其实也可以添加给.box */
        }
        
        .box {
            position: relative;
            width: 200px;
            height: 200px;
            margin: 100px auto;
            transition: all 2s;  /* 悬浮旋转添加过渡效果 */
            /* 让子元素保持3d立体空间环境 */
            transform-style: preserve-3d;
        }
        
        .box:hover { /* 悬浮在外层盒子上，进行y轴旋转 */
            transform: rotateY(60deg);
        }
        
        .box div {  /* 子绝父相，通过定位让俩div与box位置重叠  */
            position: absolute; 
            top: 0;
            left: 0; 
            width: 100%;
            height: 100%;
            background-color: pink;
        }
        
        .box div:last-child {/* 第二个div，x轴旋转，向后倒 */
            background-color: purple;
            transform: rotateX(60deg);
        }
    </style>
</head>

<body>
    <div class="box">
        <div></div>
        <div></div>
    </div>
</body>
```

#### 2.5.2 区别

```css
  body {
            /*perspective 有继承性 ，可以给父元素，爷爷辈的添加.... */
            /* 这个案例，只能给body添加此属性，section和div都需要有近大远小的效果 */
            /* 近大远小 */
            perspective: 1000px;
            /* transform-style 没有继承性，只能给要保持3D效果的元素的直接父元素添加 */
            /* 我们现在希望每个div保持3D效果，只能给section添加此属性 */
            /* 让子元素保持3D效果 */
            /* transform-style: preserve-3d; */
        }
```



### 2.6 案例

#### 案例1：两面翻转的盒子

**效果**：

![](medias\rotate-box.gif)

**html结构**：

```html
<div class="box">
    <div class="front">黑马程序员</div>
    <div class=“back">pink老师等你</div>
</div>
// box父盒子里面包含前后两个子盒子
// box 是翻转的盒子  front是前面盒子 back是后面盒子

```

**css样式**：

- box指定大小，切记要添加3d呈现
- back盒子要沿着Y轴翻转180度
- 最后鼠标经过box 沿着Y旋转180deg
- 代码：

```html
 <style>
        body {
            perspective: 400px;
        }
        
        .box {
            position: relative;
            width: 300px;
            height: 300px;
            margin: 100px auto;
            transition: all .4s;
            /* 让背面的紫色盒子保留立体空间 给父级添加的 */
            transform-style: preserve-3d;
        }
        
        .box:hover {/* 鼠标悬浮，让box沿着Y轴翻转*/
            transform: rotateY(180deg);
        }
        
        .front,
        .back { /* 正反面需要通过定位与父亲box重叠 */
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            border-radius: 50%;
            font-size: 30px;
            color: #fff;
            text-align: center;
            line-height: 300px;
        }
        
        .front {
            background-color: pink;
            z-index: 1; /* 正面需要显示在顶部 */
        }
        
        .back {
            background-color: purple;
            /* 默认back需要是背面显示，因为我们要鼠标悬浮让back翻转过来看到正面，
            但是如果不让back默认就是背面显示，那么翻转过来看到的就是back的背面 */
            transform: rotateY(180deg);
        }
    </style>
```



#### 案例2：3D导航栏

**效果**：

![](medias\3d-daohanglan.gif)

**html结构**：

```html
<ul>
    <li>
            <div class="box">
                <div class="front">黑马程序员</div>
                <div class="bottom">pink老师等你</div>
            </div>
    </li>
    <li>
            <div class="box">
                <div class="front">黑马程序员</div>
                <div class="bottom">pink老师等你</div>
            </div>
    </li>
    .......剩下的省略
</ul>
// li  做导航栏
//.box 是翻转的盒子  front是前面盒子 bottom是底下盒子


```

**css样式**：

- li设置大小，加透视和 3d呈现
- front 需要前移 17.5像素 
- bottom 需要下移 17.5像素 并且要沿着x轴翻转  负90度 
- 鼠标放到box 让盒子旋转90度
- 代码：

```html
   <style>
        * {
            margin: 0;
            padding: 0;
        }
        
        ul {
            margin: 100px;
        }
        
        ul li {
            float: left;
            margin: 0 5px;
            width: 120px;
            height: 35px;
            list-style: none;
            /* 一会我们需要给box 旋转 也需要透视 干脆给li加 里面的子盒子都有透视效果 */
            perspective: 500px;
        }
        
        .box { /*  让儿子开启3D空间，并且添加悬浮后沿着X旋转和过渡效果  */
            position: relative;
            width: 100%;
            height: 100%;
            transform-style: preserve-3d;
            transition: all .4s;
        }
        /* 第三步： */
       /* 鼠标悬浮，让盒子开始旋转 */
        .box:hover {
            transform: rotateX(90deg);
        }
        
        .front,
        .bottom { /* 前边的盒子和下边的盒子 需要与  父亲box 重叠在一起（我们发现要想做3D效果，都需要有一个父亲，因为 transform-style: preserve-3d 需要给父亲添加，父亲让儿子开启3D空间）  */
            position: absolute;
            left: 0;
            top: 0;
            width: 100%;
            height: 100%;
        }
        
        .front {
            background-color: pink;
            z-index: 1; /* 默认显示  */
            /* 第二步： */
            /* 前边的盒子向眼睛的方向走自身高度一半 */
            transform: translateZ(17.5px);
        }
        
        .bottom {
            background-color: purple;
            /* 第一步： */
            /* 需要让下边的盒子向屏幕外扑倒，所以x轴为负值*/
            /* 并且向下走自身高度的一半35/2，y轴向下是正的，所以向下走是正值*/
            /* 我们如果有移动 或者其他样式，必须先写我们的移动 */
            transform: translateY(17.5px) rotateX(-90deg);
        }
    </style>
```



#### 案例3：旋转木马

**效果**：

![](medias\rotate-dog.gif)

**html结构**：

```html
<section>
    <div></div>
    <div></div>
    <div></div>
    <div></div>
    <div></div>
    <div></div>
</section>
//里面的6个div 分别是 6个狗狗图片
//注意最终旋转是section标签 ，section也有图片，就是那个猪


```

**css样式**：

- 给body添加 透视效果 perspective: 1000px;
- 给section 添加 大小，一定不要忘记添加  3d呈现效果控制里面的6个div 
- 别忘记子绝父相，section要加相对定位
- 里面6个div 全部绝对定位叠到一起，然后移动不同角度旋转和距离
- 注意：旋转角度用rotateY   距离 肯定用 translateZ来控制
- 给section  添加动画animation ，让它可以自动旋转即可
- 代码

```html
  <style>
        body {
            perspective: 1000px;
        }
        
        section { /*让section 旋转360度，一直旋转*/
            position: relative;
            width: 300px;
            height: 200px;
            margin: 150px auto;
            /*2.2 所有图片都到自己位置之后，保留3D效果*/
            transform-style: preserve-3d;
            /* 3.2 section添加动画 */
            animation: rotate 10s linear infinite;
            background: url(media/pig.jpg) no-repeat;
        }
        section:hover {
            /*3.3  鼠标放入section 停止动画 */
            animation-play-state: paused;
        }
        /*第三步，开始处理动画
      	  3.1 先定义动画，沿着Y轴旋转360度
      	*/
        @keyframes rotate {
            0% {
                transform: rotateY(0);
            }
            100% {
                transform: rotateY(360deg);
            }
        }
        
        section div {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: url(media/dog.jpg) no-repeat;
        }
        /* 第一步：让第一个盒子到自己的位置
      		往眼睛方向走300px，不需要旋转
      	*/
        section div:nth-child(1) {
            transform: rotateY(0) translateZ(300px);
        }
         /* 第二步：2.1 让第后边的五个盒子到自己的位置
      		绕着Y旋转60度，朝着眼睛位移的距离一样，都是300px
      	     为啥是60度？因为有6张图片，需要形成一圈图片，所以每张图片绕着Y轴依次递增旋转60度
      	*/
        section div:nth-child(2) {
            /* 先旋转好了再 移动距离  */
            transform: rotateY(60deg) translateZ(300px);
        }
        
        section div:nth-child(3) {
            /* 先旋转好了再 移动距离 */
            transform: rotateY(120deg) translateZ(300px);
        }
        
        section div:nth-child(4) {
            /* 先旋转好了再 移动距离 */
            transform: rotateY(180deg) translateZ(300px);
        }
        
        section div:nth-child(5) {
            /* 先旋转好了再 移动距离 */
            transform: rotateY(240deg) translateZ(300px);
        }
        
        section div:nth-child(6) {
            /* 先旋转好了再 移动距离 */
            transform: rotateY(300deg) translateZ(300px);
        }
    </style>
```

问题：

为啥这里就需要先旋转再移动了呢？

因为我们需要他们先通过旋转改变了坐标轴的方向，然后再移动，这样才能形成四周散开的效果。

其实可以看一下，如果是先移动，在旋转是啥效果：

![](medias\muma_error.jpg)

## 3. 浏览器私有前缀

浏览器私有前缀是为了兼容老版本的写法，比较新版本的浏览器无须添加。

1. 私有前缀

   - -moz-：代表 firefox 浏览器私有属性  （moz：Mozilla，firefox由Mozilla打造）
   - -ms-：代表 ie 浏览器私有属性 （ms：Microsoft）
   - -webkit-：代表 safari、chrome 私有属性 （这俩浏览器的内核为webkit）
   - -o-：代表 Opera 私有属性 （o：opear缩写）

2. 提倡的写法

   ```html
   -moz-border-radius: 10px; 
   -webkit-border-radius: 10px; 
   -o-border-radius: 10px; 
   border-radius: 10px;
   ```


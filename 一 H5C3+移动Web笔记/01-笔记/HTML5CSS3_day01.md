# day01 - 移动web开发_H5C3

## 1.0. HTML5

> 学习目标：
>
> ​	了解 H5 新变化
>
> ​	掌握 H5 新增语义化标签
>
> ​	掌握 H5 新增多媒体标签
>
> ​	掌握 H5 新增 input 表单、表单属性

HTML5介绍：

- HTML5 就是HTML 版本的第五次重大修改，目的为了适用移动端的发展
- 版本： HTML4 --  XHTML – HTML5
- HTML5 前景移动端优先 
- 广义的HTML5 是 HTML5本身 + CSS3 + JavaScript

## 1.1. 语义化标签 了解

使用语义化标签的好处是增强了代码的可阅读性，也方便了网站的seo（Search Engine Optimization，搜索引擎优化）。

- header  头部标签
- nav 导航标签
- article 内容标签
- section 块级标签  （块级标签 啥意思？ ）
- aside 侧边栏标签
- footer 尾部标签

![1523421588540](medias/1523421588540.png)



**注意**：

- 这种语义化标准主要针对搜索引擎的
- 这些新标签页面中可以使用多次的 
- 在IE9中，需要把这些元素转换为块级元素（在IE9中这些标签被当做行内标签，设置大小不生效）
- 其实，我们移动端更喜欢使用这些标签
- HTML5 还增加了很多其他标签，我们后面再慢慢学

## 1.2. 多媒体标签

多媒体标签分为 音频 **audio** 和视频 **video** 两个标签 使用它们，我们可以很方便的在页面中嵌入音频和视频，而不再去使用落后的flash和其他浏览器插件了。

因为多媒体标签的 属性、方法、事件比较多，因此我们需要什么功能的时候，就需要去查找相关的文档进行学习使用。

![1525055132280](medias/1525055132280.png)

### 1.2.1. audio 音频标签

**使用**

```html
<audio src="小猪佩奇.mp3" autoplay> </audio>
source : 源，文件路径
```

**支持的格式**

| 格式 | MIME-type  |
| ---- | ---------- |
| MP3  | audio/mpeg |
| Ogg  | audio/ogg  |
| Wav  | audio/wav  |

**浏览器对音频格式支持情况**

![](medias/audio_allow.jpg)

**source标签**

可以通过在多媒体标签内加入**source**标签，用来指定多个播放路径，当第一个**source**标签的路径出错时，自动会切换到第二个**source**标签

```html
<audio controls="controls">
    <source src="media/snow.mp3" type="audio/mpeg" />
    <source src="media/snow.ogg" type="audio/ogg" />
    您的浏览器不支持播放声音
</audio>
audio指定单一音频源：audio中添加src属性
audio指定多个音频源：source标签替代audio的src属性
type：类型， 当前音频文件的具体类型  ， audio/mpeg  : audio是大类型/具体类型   （MIMEtype）
图片类型： jpg , jpeg  ----- image/jpeg
```

**audio常用属性**

| 属性     | 值       | 描述                                                         |
| -------- | -------- | ------------------------------------------------------------ |
| autoplay | autoplay | 如果出现该属性，则音频在就绪后马上播放。                     |
| controls | controls | 如果出现该属性，则向用户显示控件，比如播放按钮。             |
| loop     | loop     | 如果出现该属性，则每当音频结束时重新开始播放。               |
| preload  | preload  | 如果出现该属性，则音频在页面加载时进行加载，并预备播放。如果使用 "autoplay"，则忽略该属性。 |
| src      | url      | 要播放的音频的 URL。                                         |

**注意**：谷歌浏览器禁用了autoplay属性，因为它认为界面一打开就播放音频，如果音频声音比较大，体验不太好。

**补充：单一源与多个源对比**：

```html
<audio src="小猪佩奇.mp3"  controls="controls" autoplay> </audio>
<audio controls="controls" autoplay>
    <source src="media/snow.mp3" type="audio/mpeg" />
    <source src="media/snow.ogg" type="audio/ogg" />
    您的浏览器不支持播放声音
</audio>
问题1：指定多个源的时候，为啥还要给audio指定controls属性？
答：多个源，只是将audio的src属性替换为了source标签而已，其他属性（controls，autoplay...）还是需要给audio添加
问题2：为啥单一源时，不需要type，而多个源需要type？
答：其实都需要指定，规范写法就是需要添加type。
```



### 1.2.2. video 视频标签

**使用**

```html
  <video src="小猪佩奇.mp4" autoplay controls ></video>
```

**支持的格式**

| 格式 | MIME-type  |
| ---- | ---------- |
| MP4  | video/mp4  |
| WebM | video/webm |
| Ogg  | video/ogg  |

**浏览器对视频格式支持情况**

![](medias/video_allow.jpg)

**video常用属性、方法、事件**

| 属性                     | 方法       | 事件                          |
| ------------------------ | ---------- | ----------------------------- |
| duration  视频播放时长   | play 播放  | canplay 视频加载完毕 准备播放 |
| currentTime 当前播放进度 | pause 暂停 | timeupdate 播放时-持续触发    |
| volume 音量大小          |            |                               |

**source标签**

不仅audio可以使用source来指定多个文件源，video也可以：

```html
    <!-- 当1.mp4出错时，自动切换到2.mp4 ... -->
    <video >
      <source src="1.mp4">
      <source src="2.mp4">
      <source src="3.mp4">
    </video>
```

**video常见属性**

| 属性     | 值                                       | 描述                                                         |
| -------- | ---------------------------------------- | ------------------------------------------------------------ |
| autoplay | autoplay                                 | 视频就绪自动播放（谷歌浏览器需要添加muted来解决自动播放问题） |
| controls | controls                                 | 向用户显示播放控件                                           |
| width    | pixels(像素)                             | 设置播放器宽度                                               |
| height   | pixels(像素)                             | 设置播放器高度                                               |
| loop     | loop                                     | 播放完是否继续播放该视频，循环播放                           |
| preload  | auto（预先加载视频）none（不应加载视频） | 规定是否预加载视频(如果有了autoplay 就忽略该属性）           |
| src      | url                                      | 视频url地址                                                  |
| poster   | Imgurl                                   | 加载等待的画面图片  （视频首帧：首画面。海报）               |
| muted    | muted                                    | 静音播放                                                     |

**谷歌浏览器自动播放视频代码：**

```html
   <!-- 谷歌浏览器把自动播放功能给禁用了 有解决方案： 给视频添加静音属性 -->
    <video autoplay="autoplay" muted="muted">
        <source src="media/video.mp4" type="video/mp4" />
        <source src="media/video.ogg" type="video/ogg" />
        您的浏览器太low了，不支持播放此视频
    </video>
```

**总结**：

- 音频标签和视频标签使用基本一致
- 浏览器支持情况不同
- 谷歌浏览器把音频和视频自动播放禁止了
- 我们可以给视频标签添加 muted 属性可以自定播放视频，音频不可以
- 视频标签是重点，我们经常设置自动播放，不使用controls控件，循环和设置大小属性





**object-fit属性**

当**video**标签视频内容宽度没有铺满video标签时，可以在css写上 该属性即可

```css
    video {
      /* 让视频内容铺满整个video标签  fit意为：合适 */
      object-fit: fill; /* fit意为：合适 */
    }
```

**注意**：此属性用的比较少，视频一般都是铺满video标签的

### 1.2.3. 兼容性

因为多媒体标签在不同的浏览器下是不一样的外观，我们有时候需要统一所有的样式，所以就需要我们自己使用**div + 多媒体 **的一些api实现 控制条工具 。

![1525056633662](medias/1525056633662.png)

感兴趣的读一读：<https://blog.csdn.net/qq_22557797/article/details/72866358> 

![](medias/video_control.jpg)



## 1.3. h5表单

### 1.3.1 H5新增表单

**新增表单类型如下**：

| 属性值        | 说明                                                     |
| ------------- | -------------------------------------------------------- |
| type="email"  | 限制用户输入必须为Email类型                              |
| type="url"    | 限制用户输入必须为URL类型                                |
| type="date"   | 限制用户输入必须为日期类型                               |
| type="time"   | 限制用户输入必须为时间类型                               |
| type="month"  | 限制用户输入必须为月类型                                 |
| type="week"   | 限制用户输入必须为周类型                                 |
| type="number" | 限制用户输入必须为数字类型                               |
| type="tel"    | 手机号码（不限制只能输入数字，因为有些特殊电话会有符号） |
| type="search" | 搜索框                                                   |
| type="color"  | 生成一个颜色选择表单                                     |

**代码**：

```html
<form action="">
    <ul>
        <li>邮箱: <input type="email" /></li>
        <li>网址: <input type="url" /></li>
        <li>日期: <input type="date" /></li>
        <li>日期: <input type="time" /></li>
        <li>数量: <input type="number" /></li>
        <li>手机号码: <input type="tel" /></li>
        <li>搜索: <input type="search" /></li>
        <li>颜色: <input type="color" /></li>
        <li> <input type="submit" value="提交"></li>
    </ul>
</form>
```

**效果**：

![](medias\input-02.jpg)



**手机端效果**：

![](medias\input-01.jpg)



手机端效果中，如果是手机号码，那么会显示数字键盘。

### 1.3.2 新增表单属性

**属性如下**：

| 属性         | 值        | 说明                                                         |
| ------------ | --------- | ------------------------------------------------------------ |
| required     | required  | 表单拥有该属性表示其内容不能为空，必填                       |
| placeholder  | 提示文本  | 表单的提示信息，存在默认值将不显示                           |
| autofocus    | autofocus | 自动聚焦属性，页面加载完成自动聚焦到指定表单                 |
| autocomplete | off / on  | 当用户在字段开始键入时，浏览器基于之前键入过的值，应该显示出在字段中填写的选项。默认已经打开，如 autocomplete=”on “ 关闭 autocomplete =”off”-需要放在表单内同时加上name属性-同时成功提交 |
| multiple     | multiple  | 可以多选文件提交                                             |

#### 1. required:必填验证

```html
<form action="">
     用户名: <input type="text" required="required" > <input type="submit" value="提交"> 
</form>
```

效果如下图：

![](medias/required.jpg)

- novalidate:关闭验证
  - 在表单上添加该属性，那么在提交的时候就不会再执行 required验证
- pattern：自定义验证-通过编写正则表达式自定义验证规则 一般和required同时使用
  - 表单事件

#### 2. placeholder:占位符-提示信息

```html
<form action="">
     用户名: <input type="text" placeholder="请输入用户名">
     <input type="submit" value="提交">
</form>
```

效果如下图：

![](medias/placeholder.jpg)

#### 3. autofocus 自动获取焦点

autofocus：自动获得焦点-一般页面中放1个

代码：

```html
<form action="">
    用户名: <input type="text" required="required" placeholder="请输入用户名" autofocus="autofocus">
</form>
```

效果：

![](medias\input-autofocus.jpg)

#### 4. autocomplete 自动完成

autocomplete 自动完成：自动补全，类似百度搜索框一样，会以下拉菜单形式提示以往输入过的内容

- 当用户在字段开始键入时，浏览器基于之前输入过的值，开始提示
- 默认已经打开 如 `autocomplete=on`  关闭 `autocomplete =off`
- 需要放在表单内同时加上name属性

代码：

```html
 <form action="">
     用户名: <input type="text" name="username" autocomplete="off"> 
     <input type="submit" value="提交"> 
</form>
//注意：代码中需要带上name属性，提交的时候才会将input的内容提交过去
```

效果如下：

![](medias/autocomplate.jpg)



#### 5. multiple:可以多选文件提交

- 结合文件上传标签   `<input type="file" >`   一起使用
- 以前的input:file只能上传一个文件，现在增加multiple属性即可

代码：

```html
<form action="">
    用户名: <input type="text" name="username" > 
    <input type="submit" value="提交"> 
    上传头像: <input type="file" name="" id="" multiple="multiple">
</form>
```

效果：

![](medias/multiple.jpg)



#### 6. form属性

form属性：可以将输入标签放在表单的外面，还受到表单的管理 

```html
<!-- 指定了id为ff -->
<form action="" id="ff" >
  <input type="submit" value="提交">
</form>
<!-- 指定了属性form，值为表单的id=ff -->
<input type="text" required form="ff"  >
```

## 1.4. 属性选择器 

属性选择器如下：

| 选择符        | 简介                                  |
| ------------- | ------------------------------------- |
| E[att]        | 选择具有att属性的E元素                |
| E[att="val"]  | 选择具有att属性且属性值等于val的E元素 |
| E[att^="val"] | 匹配具有att属性、且值以val开头的E元素 |
| E[att$="val"] | 匹配具有att属性、且值以val结尾的E元素 |
| E[att*="val"] | 匹配具有att属性、且值中含有val的E元素 |

**注意**：类选择器、属性选择器、伪类选择器，权重为 10

**特殊符号**：

^ : 匹配开头

$：匹配结尾

\* : 匹配任意位置  

代码：

```html
<style>
        /* 属性选择器使用方法 */
        /* 属性选择器的权重是 10 */
        /* 1.直接写属性 */
     
        button[disabled] {   /* 选择的是：  既是button 又有 disabled 这个属性的元素 */
            cursor: default;
        }
        
        button {
            cursor: pointer;
        }
        /* 2. 属性等于值 */
        
        input[type="search"] {
            color: pink;
        }
        /* 3. 以某个值开头的 属性值 */
        
        div[class^="icon"] {
            color: red;
        }
        /* 4. 以某个值结尾的 */
        
        div[class$="icon"] {
            color: green;
        }
        /* 5. 可以在任意位置的 */
        
        div[class*="icon"] {
            color: blue;
        }
    </style>
</head>

<body>
    <!-- disabled 是禁用我们的按钮 -->
    <button>按钮</button>
    <button>按钮</button>
    <button disabled="disabled">按钮</button>
    <button disabled="disabled">按钮</button>

    <input type="text" name="" id="" value="文本框">
    <input type="text" name="" id="" value="文本框">
    <input type="text" name="" id="" value="文本框">
    <input type="search" name="" id="" value="搜索框">
    <input type="search" name="" id="" value="搜索框">
    <input type="search" name="" id="" value="搜索框">
    <div class="icon1">图标1</div>
    <div class="icon2">图标2</div>
    <div class="icon3">图标3</div>
    <div class="iicon3">图标4</div>
    <div class="absicon">图标5</div>
</body>
```



## 1.5. 伪类选择器

结构伪类选择器如下：

| 选择符           | 简介                        |
| ---------------- | --------------------------- |
| E:first-child    | 匹配父元素中的第一个子元素E |
| E:last-child     | 匹配父元素中最后一个E元素   |
| E:nth-child(n)   | 匹配父元素中的第n个子元素E  |
| E:first-of-type  | 指定类型E的第一个           |
| E:last-of-type   | 指定类型E的最后一个         |
| E:nth-of-type(n) | 指定类型E的第n个            |

### 1.5.1. E:first-child

E:first-child ：匹配父元素的第一个子元素E

**代码**：

```html
  <style>
    ul li:first-child{
      background-color: red;
    }
    /*  ul li:first-child ------ 在ul li的选择器选中的结果中进行过滤，过滤出第一个儿子  */
  </style>

  <ul>
    <li>列表项一</li>
    <li>列表项二</li>
    <li>列表项三</li>
    <li>列表项四</li>
  </ul>
```

**效果-分析图**：

![1525000310879](medias/1525000310879.png)

**注意**： 

- 匹配到的是ul的第一个li子元素
- **这里比较容易混淆的是**：E:first-child，找E的第一个儿子。**其实应该是找E父亲中第一个儿子E**。
- **E:last-child** ：匹配父元素的最后一个子元素E ，如上案例中使用ul li:last-child，则是选择到了最后一个li标签 




### 1.5.2. E:nth-child(n)    E:nth-last-child(n)

匹配到父元素的第n个子元素E 或者 是倒数第n个子元素E

nth：第n个的意思（**注意**：nth是一个单词，单词意思就是第n个）

相比 `E:first-child`   则要强大了不少，功能如下

- 匹配到父元素的第2个子元素  （**这里不能直接写0，写0会被忽略，想选择第一个就写1**）

  `ul li:nth-child(2){}`

- 匹配到父元素的倒数第2个子元素

  `ul li:nth-last-child(2){}`

- 匹配到父元素的序号为奇数的子元素

  `ul li:nth-child(odd){}`    **odd** 是关键字  奇数的意思

- 匹配到父元素的序号为偶数的子元素 

  `ul li:nth-child(even){}`   **even**偶数的意思

代码：

```html
<style>
    ul li:first-child {
        background-color: pink;
    }

    ul li:last-child {
        background-color: deeppink;
    }
    /* nth-child(n)  我们要第几个，n就是几  比如我们选第8个， 我们直接写 8就可以了 */

    ul li:nth-child(8) {
        background-color: lightpink;
    }
</style>
```

#### nth-child（n）- n详细介绍：

- n可以是数字，关键字和公式
- n如果是数字，就是选择第n个，（**从1开始**，也可以认为从0开始，但是会被忽略）
- 常见的关键词  even 偶数 odd 奇数
- 常见的公式如下 ( 如果n是公式，则从0开始计算，但是 **第0个元素或者超出了元素的个数会被忽略** ）

![](medias\nth-n.jpg)

n+5，从5开始往后选择

-n+5，从5开始往前选择

**这里的-，负号，可以理解为代表方向。正号往后，负号往前**

**注意**：不能写成5-n，这里的-就是减号了，而不是负号。

- **匹配到父元素的前3个子元素**

  `ul li:nth-child(-n+3){}`    

  选择器中的  **n** 是怎么变化的呢？

  因为 n是从 0 ，1，2，3.. 一直递增

  所以 -n+3 就变成了   

  - n=0 时   -0+3=3
  - n=1时    -1+3=2
  - n=2时    -2+3=1
  - n=3时    -3+3=0 
  - ...

  

### 1.5.3. E:nth-of-type(n)

这里只讲明  **E:nth-child(n)**  和 **E:nth-of-type(n)**  的区别  

剩下的 **E:first-of-type**     **E:last-of-type**  **E:nth-last-of-type(n)**   同理做推导即可

```html
  <style>
    ul li:nth-child(2){
      /* 字体变成红色 */
        color: red;
    }

    ul li:nth-of-type(2){
      /* 背景变成绿色 */
      background-color: green;
    }
  </style>


  <ul>
    <li>列表项一</li>
    <p>乱来的p标签</p>
    <li>列表项二</li>
    <li>列表项三</li>
    <li>列表项四</li>
  </ul>
```

![1525002608570](medias/1525002608570.png)

也就是说

- `E:nth-child(n)`     匹配父元素的第n个子元素E。（**找第n个儿子E**）
- `E:nth-of-type(n)  `  匹配父元素中第n个同类型中的第n个元素E。 （**找第n个E类型的儿子**）
- 区别：
- nth-child(n)  选择 父元素里面的 第 n个孩子， 它不管里面的孩子是否同一种类型 
- nth-of-type(n) 选择 父元素里边的 第n个同类型的孩子，孩子必须是同类型

最终记住，理解如下内容即可：

> ​        E:nth-child(n)  n: E父元素中所有儿子进行排序
>
> ​        E:nth-of-type(n)  n: E父元素中E儿子进行排序   



## 1.6. 伪元素选择器 

### 1.6.1. 伪元素种类

1. E::before： 在E元素前插入一个元素
2. E::after：  在E元素后插入一个元素

代码：

```html
<style>
    div {
        width: 300px;
        height: 300px;
        border: 1px solid #000;
    }

    div::before {
        content: "我";
        display: inline-block;
        width: 100px;
        height: 100px;
        background-color: pink;
    }

    div::after {
        content: "小猪佩奇";
        display: inline-block;
        width: 100px;
        height: 100px;
        background-color: pink;
    }
</style>
</head>

<body>
    <div>是</div>
</body>
```

效果：

![](medias\伪元素插入元素.jpg)

### 1.6.2. h5写法和传统写法区别 

1. 单冒号 `E:before`
2. 双冒号 `E::before`
3. 浏览器对以上写法都能识别 **双冒号** 是h5上语法的规范

### 1.6.3. 伪元素的注意事项 

- before 和 after 必须有 content 属性 
- before 在内容的前面，after 在内容的后面
- before 和 after 创建一个元素，但是属于行内元素。
- 因为在 dom 里面看不见刚才创建的元素，所以我们称为伪元素
- 伪元素和标签选择器一样，权重为 1

想要让伪元素有效，必须遵循以下注意事项

1. 伪元素只能给双标签加 不能给单标签加
2. 伪元素的冒号前不能有空格 如 `E    ::before`  这个写法是错误的
3. 伪元素里面必须写上属性 `content:""`;

### 1.6.4 \ 转义符

​        md文档：  *  ----  无序符号 （小圆点）

​                  将特殊含义的*  转义为普通字符*  ----- \*    

​                  

​                  \：将特殊字符转换为普通字符使用

 

​        css中：   ea50  ----  ico字体中是一个向下的三角箭头

 

​                  将普通字符串ea50  转义为特殊的icon字体  ---- \ea50

 

​                  \ : 可以将普通字符与特殊字符进行转换

​                  \ 是一个转义字符

## 1.7. 2D转换（变换）transform

转换（transform）是CSS3中具有颠覆性的特征之一，可以实现元素的位移、旋转、变形、缩放。

- 缩放：scale
- 移动：translate
- 旋转：rotate
- 倾斜：skew

2d转换是改变标签在**2维平面**上的**位置和形状**的一种技术，我们先来学习2维坐标系。

### 1.7.1. 2维坐标系

**2维坐标系**其实就是指布局的时候的坐标系 如图

![1524965494414](medias/1524965494414.png)

### 1.7.2. 2d移动 translate

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

![1524965782388](medias/1524965782388.png)

**小结**:

1. **translate**中的百分比单位是相对于自身元素的  `translate:(50%,50%);`
2. **translate**类似定位，不会影响到其他元素的位置
3. 对行内标签没有效果


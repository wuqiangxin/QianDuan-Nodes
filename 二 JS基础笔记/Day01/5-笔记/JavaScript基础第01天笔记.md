# JavaScript基础第01天

## 1. 编程语言

### 1.1 编程

- 编程：就是让计算机为解决某个问题而使用某种程序设计语言编写程序代码，并最终得到结果的过程。
  - **编程：编写程序，程序就是软件，网站等等（写代码）**
- 计算机程序：就是计算机所执行的一系列的指令集合，而程序全部都是用我们所掌握的语言来编写的，所以人们要控制计算机一定要通过计算机语言向计算机发出命令。
- 从事编程的人员，就是程序员。  但是一般程序员都比较幽默，为了形容自己的辛苦工作，也成为“码农”， 或者  “程序猿”/ “程序媛”
- 注意：上面所定义的计算机指的是任何能够执行代码的设备，可能是智能手机、ATM机、黑莓PI、服务器等等。

### 1.2 计算机语言

- 计算机语言指用于人与计算机之间通讯的语言，它是人与计算机之间传递信息的媒介。

  - **语言：人与人沟通的工具  （英文：语法，词汇）**
  - **计算机语言：人与计算机沟通的工具  （高级语言：语法，词汇）**

- 计算机语言的种类非常的多，总的来说可以分成机器语言，汇编语言和高级语言三大类。

- 实际上计算机最终所执行的都是 机器语言，它是由“0”和“1”组成的二进制数，二进制是计算机语言的基础。

  ![](images\图片1.png)

### 1.3 编程语言

- 编程语言：可以通过类似于人类语言的 ”语言”来控制计算机，让计算机为我们做事情，这样的语言就叫做编程语言（Programming Language）。
- **编程语言是用来控制计算机的一系列指令，它有固定的格式和词汇**（不同编程语言的格式和词汇不一样），必须遵守。

- 如今通用的编程语言有两种形式：**汇编语言和高级语言**。

| 语言类型     | 说明                                                         |
| ------------ | :----------------------------------------------------------- |
| **汇编语言** | 汇编语言和机器语言实质是相同的，都是直接对硬件操作，<br>只不过指令采用了英文缩写的标识符，容易识别和记忆。 |
| **高级语言** | 高级语言主要是相对于低级语言而言，它并不是特指某一种具体的语言，<br/>而是包括了很多编程语言，常用的有C语言、C++、Java、C#、Python、PHP、<br/>JavaScript、Go语言、Objective-C、Swift等。 |

![](images\图片2.png)

### 1.4 翻译器

- 高级语言所编制的程序不能直接被计算机识别，必须经过转换才能被执行，为此，我们需要一个翻译器。
- 翻译器可以将我们所编写的源代码转换为机器语言，这也被称为二进制化。 记住1和 0。


 ![](images\图片3.png)

### 1.5 编程语言和标记语言区别

| 语言     | 说明                                                         |
| -------- | ------------------------------------------------------------ |
| 编程语言 | **编程语言有很强的逻辑和行为能力**。在编程语言里, 你会看到很多<br> if else 、for 、while等具有逻辑性和行为能力的指令，这是主动的。 |
| 标记语言 | 标记语言（html）不用于向计算机发出指令，常用于格式化和链接。<br/>标记语言的存在是用来被读取的, 他是被动的。 |

**理解**：逻辑：  先做什么，后做什么，编程思路。	

### 1.6 总结

1. 计算机可以帮助人类解决某些问题

2. 程序员利用编程语言编写程序发出指令控制计算机来实现这些任务

3. 编程语言有机器语言、汇编语言、高级语言

4. **高级语言需要一个翻译器转换为计算机识别的机器语言**

5. 编程语言是主动的有很强的**逻辑性**

6. **概念理解**：

   1. 语言： 人与人沟通的工具
   2. 计算机语言： 人与计算机沟通
   3. 编程： 编写程序（软件，网站，app），写代码
   4. 编程语言： 写程序的工具，通过编程语言，来写代码，来编程

   

## 2.  计算机基础

### 2.1 计算机组成

![](images\图片4.png)

![](images\图片5.png)



### 2.2 数据存储

1. **计算机内部使用二进制 0 和 1来表示数据**。
2. 所有数据，包括文件、图片等最终都是以二进制数据（0 和 1）的形式存放在硬盘中的。
3. 所有程序，包括操作系统，本质都是各种数据，也以二进制数据的形式存放在硬盘中。平时我们所说的安装软件，其实就是把程序文件复制到硬盘中。
4. 硬盘、内存都是保存的二进制数据。

### 2.3 数据存储单位***

数据存储单位的大小关系：bit < byte < kb < GB < TB<.....

- 位(bit)：   1bit 可以保存一个 0 或者 1 （最小的存储单位）
  - 位：理解为：位置
- 字节(Byte)：1B = 8b
- 千字节(KB)：1KB = 1024B
- 兆字节(MB)：1MB = 1024KB
- 吉字节(GB):  1GB = 1024MB
- 太字节(TB):  1TB = 1024GB

### 2.4 程序运行

计算机运行软件的过程：

1. 打开某个程序时，先从硬盘中把程序的代码加载到内存中

2. CPU执行内存中的代码

    ![](images\图片6.png)

**注意**：之所以要内存的一个重要原因，是因为 cpu运行太快了，如果只从硬盘中读数据，会浪费cpu性能，所以，才使用存取速度更快的内存来保存运行时的数据。（内存是电，硬盘是机械）

### 2.5 内存的主要作用以及特点 ***

- 内存作用：**存储运行中的程序的数据**
- 内存特点：运行速度极快，断电数据丢失
- 硬盘： 1-2T  （存储数据）
- 内存： 8-16G   （存储程序运行中的数据）
- 例如：vlc播放视频 ： 将硬盘中的数据，读取到内存中
- 程序运行过程中存储什么数据呢？vlc播放视频的当前时间，总时长等。

## 3.  初识JavaScript

### 3.1 JavaScript 是什么 ***



![](.\images\图片7.png)

- 布兰登·艾奇（Brendan Eich，1961年～）。神奇的大哥用10天完成 JavaScript 设计。最初命名为 LiveScript，后来在与 Sun 合作之后将其改名为 JavaScript。


- JavaScript 是世界上最流行的语言之一，是**一种运行在客户端的脚本语言** （Script 是脚本的意思）


  - 客户端：客户：用户，用户的计算机，计算机中的浏览器

- 脚本语言：**不需要编译**，运行过程中由 js 解释器( js 引擎，**js翻译器**）**逐行来进行解释并执行**

- 现在也可以基于 Node.js 技术进行服务器端编程

  ![](images\图片8.png)

### 3.2 JavaScript的作用 

-  表单动态校验（密码强度检测）  （ JS 产生最初的目的 ）
-  网页特效
-  服务端开发(Node.js)
-  桌面程序(Electron)  
-  App(Cordova) 
-  控制硬件-物联网(Ruff)
-  游戏开发(cocos2d-js)

### 3.3 HTML/CSS/JS 的关系

![](images\图片9.png)

### 3.4 浏览器执行 JS 简介 ***

**浏览器分成两部分：渲染引擎和 JS 引擎**

| 引擎     | 说明                                                         |
| -------- | ------------------------------------------------------------ |
| JS 引擎  | 也称为 JS 解释器。 用来读取网页中的JavaScript代码，对其处理后运行，比如 chrome  <br />浏览器的 V8 |
| 渲染引擎 | 用来解析HTML与CSS，俗称内核，比如 chrome 浏览器的 blink ，老版本的 webkit |

- 浏览器本身并不会执行JS代码，而是通过内置 **JavaScript 引擎(解释器) 来执行 JS 代码** 。
- JS 引擎执行代码时逐行解释每一句源码（转换为机器语言），然后由计算机去执行，
- 所以 JavaScript 语言归为脚本语言，会逐行解释执行。

![](images\图片10.png)

- **总结**：js是脚本语言，特点：**逐行解释执行**  ***
- **补充，**不同语言运行过程对比：
  - 编译型语言：java ： 1. 编译：翻译   2. 运行       （java ---- 翻译（编译） --- 0101）
  - 解释型语言(脚本语言)：JavaScript   1.运行过程中解释（翻译） （JavaScript  ---- 翻译（解释）  ---- 0101）

### 3.5 JS 的组成

![](images\图片11.png)

- ECMAScript：Js语法
- DOM：文档对象模型  ， 文档：html文档  ，操作html文档  （操作html文档的工具）
	 BOM：浏览器对象模型 ， 操作浏览器的工具			

#### 3.5.1 ECMAScript

- ECMAScript 是由ECMA 国际（ 原欧洲计算机制造商协会）进行标准化的一门编程语言，
- 这种语言在万维网上应用广泛，它往往被称为 JavaScript或 JScript，
- 但实际上后两者是 ECMAScript 语言的实现和扩展。

   ![](images\图片12.png)

-    ECMAScript：规定了JS的编程语法和基础核心知识，是所有浏览器厂商共同遵守的一套JS语法工业标准。

-    更多参看MDN: [MDN手册](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/JavaScript_technologies_overview)


#### 3.5.2 DOM——文档对象模型

- **文档对象模型**（DocumentObject Model，简称DOM）
- 是W3C组织推荐的处理可扩展标记语言的标准编程接口
- 通过 DOM 提供的接口可以对页面上的各种元素进行操作（大小、位置、颜色等）
- **接口理解**：**工具**

#### 3.5.3  BOM——浏览器对象模型

- **浏览器对象模型**(Browser Object Model，简称BOM) 
- 它提供了独立于内容的、可以与浏览器窗口进行互动的对象结构
- 通过BOM可以操作浏览器窗口，比如弹出框、控制浏览器跳转、获取分辨率等

### 3.6 JS 初体验

JS 有3种书写位置，分别为行内、内嵌和外部。

#### 3.6.1 行内式

- 直接写到元素的内部 ，用的比较少
- 写法如下：

```html
<input type="button" value="点我试试" onclick="alert('Hello World')" />
<!-- onclick : on当，click点击。当点击发生时，执行什么代码 -->
```

- 可以将单行或少量 JS 代码写在HTML标签的事件属性中（以 on 开头的属性），如：onclick
- 注意单双引号的使用：在HTML中我们推荐使用双引号, JS 中我们推荐使用单引号
- 可读性差， 在html中编写JS大量代码时，不方便阅读；
- 引号易错，引号多层嵌套匹配时，非常容易弄混；
- 特殊情况下使用

#### 3.6.2 内嵌式***

- 学习时常用的方式
- 语法如下：

```html
<script>
    alert('Hello  World~!');
</script>
```

- 可以将多行JS代码写到 <script> 标签中
- 内嵌 JS 是学习时常用的方式

#### 3.6.3 外部JS文件***

- 工作中常用
- 语法如下：

```html
<script src="my.js"></script>
```

- src：源：source
- 利于HTML页面代码结构化，把大段 JS代码独立到 HTML 页面之外，既美观，也方便文件级别的复用
- 引用外部 JS文件的 script 标签中间不可以写代码
- 适合于JS 代码量比较大的情况
- **注意**：  外链式不要与内嵌式混用，外部式会将内嵌式的代码覆盖

## 4.  JavaScript注释

+ 为了提高代码的可读性，JS与CSS一样，也提供了注释功能。
+ JS中的注释主要有两种，分别是**单行注释**和**多行注释**。

### 4.1  单行注释

- 单行注释的注释方式如下：


```js
// 我是一行文字，不想被 JS引擎 执行，所以 注释起来	
```

-   快捷键   ctrl  +  /   

### 4.2 多行注释

- 多行注释的注释方式如下：


```js
/*
  获取用户年龄和姓名
  并通过提示框显示出来
*/
```

- 默认快捷键  alt +  shift  + a  
- 快捷键修改为：   ctrl + shift  +  /

- vscode → 首选项按钮 → 键盘快捷方式 → 查找 原来的快捷键 → 修改为新的快捷键 → 回车确认
- **注意**：  多行注释，无法嵌套

## 5.  JavaScript输入·输出语句***

为了方便信息的输入输出，JS中提供了一些输入输出语句，其常用的语句如下：

| 方法             | 说明                           | 归属   |
| ---------------- | ------------------------------ | ------ |
| alert(msg)       | 浏览器弹出警示框               | 浏览器 |
| console.log(msg) | 浏览器控制台打印输出信息       | 浏览器 |
| prompt(info)     | 浏览器弹出输入框，用户可以输入 | 浏览器 |

- 注意：alert() 主要用来显示消息给用户，console.log() 用来给程序员自己看运行时的消息。
- **理解**：
  - alert：警告，弹出警告框
  - console.log()：控制台 的 日志（点理解为的）
  - prompt：提示，弹出输入提示框
  - **以上三个都是方法，方法就是一个工具，可以实现某个功能（加括号使用的都叫做方法）**
  - 有的方法直接写，有的方法需要通过其他人**加点**进行调用（使用）

## 6.  变量的概念***

### 6.1 什么是变量

- 白话：变量就是一个装东西的盒子。

- 通俗：变量是用于存放数据的容器。 我们通过 变量名 获取数据，甚至数据可以修改。
  ![](images\图片13.png)


- **变量理解**：变化的量，变化的内容，变化的数据
- **变量存储数据理解**：程序运行过程中的数据存储在内存中，但是内存比较大，为了方便管理，所以将内存分成一个一个的盒子（变量）来存储

### 6.2 变量在内存中的存储

- 本质：变量是程序在内存中申请的一块用来存放数据的空间。
- 例子：类似我们酒店的房间，一个房间就可以看做是一个变量。  

![](images\图片14.png)

- **例子再理解**：js声明变量-----旅客去酒店开房。

  - 1.酒店开房（在内存条开辟空间，开辟的空间类似于一个盒子，就是变量）  

    ​    酒店：内存条
        房间：变量 

     2.旅客入住房间（数据放入变量中存储）			

       旅客：数据				

  - 补充：房间号：变量名 （通过变量来找到内存条中存储的数据）


## 7.  变量的使用***

变量的使用分为两步：

1. 变量的声明   
2. 变量的赋值 

### 7.1 声明变量

- 变量声明语法如下：

```javascript
var 变量名;
var age; //  声明一个 名称为age 的变量     
```

- **var** 是一个 JS**关键字**，用来声明变量( **variable** 变量的意思 )。
- 使用该关键字声明变量后，计算机会自动为变量分配内存空间，不需要程序员管
- age 是程序员定义的变量名，我们要通过变量名来访问内存中分配的空间
- **关键字**：js中有特殊作用的词。

### 7.2 赋值

- 变量赋值的语法如下：

```javascript
变量名 = 值;
age = 10; // 给 age  这个变量赋值为 10    
```

- = 用来把右边的值赋给左边的变量空间中  ，**等号此处代表赋值的意思**
- 变量值是程序员保存到变量空间里的值
- **注意**：这里的等号，**不是相等**，1+1=2. 

### 7.3 变量的初始化

- 声明一个变量并赋值， 我们称之为变量的初始化
- 变量的初始化 ：变量声明+变量赋值
- 语法如下：

```js
var 变量名 = 值;
var age  = 18;  // 声明变量age同时赋值为 18          
```

### 7.4 变量案例

1. 案例1：

```js
var myname = '旗木卡卡西';  // 字符串
var address = '火影村';
var age = 30;  // 数字
var email = 'kakaxi@itcast.cn';
var gz = 2000;
console.log(myname);
console.log(address);
console.log(age);
console.log(email);
console.log(‘gz’); // gz
console.log(gz); // 2000
```

**注意**：

- 变量赋值时，值如果是字符串需要添加'',“”
- 每行代码结束，都需要添加;
- 变量在使用时，不能添加引号 （定义，声明变量的时候，没有引号，使用的时候自然也不能添加引号）

2. 案例2：

```js
// 1. 用户输入姓名  存储到一个 myname的变量里面
var myname = prompt('请输入您的名字');
// prompt 做的事情：
// (1). 弹出输入框 , 用户输入内容:zs
// (2). 将用户输入内容返回 ，相当于 ：var myname = 'zs';
// 2. 输出这个用户名
alert(myname); // zs
```

### 7.5 变量语法扩展

- 更新变量 ***

  一个变量被重新复赋值后，它原有的值就会被覆盖，变量值将以最后一次赋的值为准。

  ```js
  var age = 18;
  
  age = 81;   // 最后的结果就是81因为18 被覆盖掉了          
  ```

- 同时声明多个变量

  同时声明多个变量时，只需要写一个 var， 多个变量名之间使用英文逗号隔开。

  ```js
  var age = 10,  name = 'zs', sex = 2;   //同时初始化多个变量
  var age,name,sex;//这个才是同时声明多个变量
  ```

- 声明变量特殊情况

  | 情况                              | 说明                    | 结果                    |
  | --------------------------------- | ----------------------- | ----------------------- |
  | var  age ; console.log (age); *** | 只声明 不赋值           | undefined               |
  | console.log(age)                  | 不声明 不赋值  直接使用 | 报错:age is not defined |
  | age   = 10; console.log (age);    | 不声明   只赋值         | 10                      |

  **总结**：

  ​	undefined：未定义 ： 只声明未赋值，**值未定义**

  ​	not defined ： 没有定义，**变量没有定义**

### 7.6 变量命名规范

| 规则                                                         |
| ------------------------------------------------------------ |
| 由字母(A-Za-z)、数字(0-9)、下划线(_)、美元符号( $ )组成，如：usrAge, num01, _name *** |
| 严格区分大小写。var app; 和 var App; 是两个变量              |
| 不能 以数字开头。  18age   是错误的                          |
| 不能 是关键字、保留字。例如：var、for、while                 |
| 变量名必须有意义。 MMD   BBD        nl   →     age           |
| 遵守驼峰命名法。首字母小写，后面单词的首字母需要大写。 myFirstName![](images\图片15.png) |
| 推荐翻译网站： 有道    爱词霸                                |

### 7.7 变量案例-交换两个变量 ***

```js
// js 是编程语言有很强的逻辑性在里面： 实现这个要求的思路 先怎么做后怎么做 
// 1. 我们需要一个临时变量帮我们
// 2. 把apple1 给我们的临时变量 temp 
// 3. 把apple2 里面的苹果给 apple1 
// 4. 把临时变量里面的值 给 apple2 
var temp; // 声明了一个临时变量为空
var apple1 = '青苹果';
var apple2 = '红苹果';
temp = apple1; // 把右边给左边
apple1 = apple2;
apple2 = temp;
console.log(apple1);
console.log(apple2);
```

交换两个变量可以不使用第三方变量，详情参照：files目录下的：JavaScript两个变量交换值（不使用临时变量） - 我是leon - 博客园.html

## 8.  数据类型

### 8.1 数据类型简介

- 为什么需要数据类型
  - 在计算机中，**不同的数据所需占用的存储空间是不同的**，
  - 为了**便于把数据分成所需内存大小不同的数据，充分利用存储空间，于是定义了不同的数据类型**。
  -  简单来说，**数据类型就是数据的类别型号**。
  - 比如姓名“张三”，年龄18，这些数据的类型是不一样的。

- 变量的数据类型
  - 变量是用来存储值的所在处，它们有名字和数据类型。

  - 变量的数据类型决定了如何将代表这些值的位存储到计算机的内存中。

  - **JavaScript 是一种弱类型或者说动态语言**。

  - 这意味着不用提前声明变量的类型，在程序运行过程中，类型会被自动确定。

  - 如下例子：

    ```js
     var age = 10;        // 这是一个数字型
     var areYouOk = '是的';   // 这是一个字符串    
    ```

    	在代码运行时，变量的数据类型是由 JS引擎 根据 = 右边变量值的数据类型来判断 的，运行完毕之后， 变量就确定了数据类型。

  - **弱类型语言理解**：

    ```js
    1.语法不规范。
    2.在声明变量时，没有强制规定变量类型。
        js:统一使用var。
            var num = 10;
            var str = 'zs';
        java: 强类型
            int num;
            string str;
    ```

-  JavaScript 拥有动态类型，同时也意味着相同的变量可用作不同的类型：


  ```js
  var x = 6;           // x 为数字
  var x = "Bill";      // x 为字符串   
  //在其他语言中是不允许的，一个变量的类型是固定的
  //但是js是动态类型，可以这么做
  ```

- 数据类型的分类，JS 把数据类型分为两类：

     - 简单数据类型 （Number,String,Boolean,Undefined,Null）
     	 复杂数据类型 （object)	

### 8.2 简单数据类型

#### 8.2.1 简单数据类型（基本数据类型）

JavaScript 中的简单数据类型及其说明如下：

![](images\图片16.png)

#### 8.2.2 数字型 Number

- JavaScript 数字类型既可以用来保存整数值，也可以保存小数(浮点数）。  

  ```js
  var age = 21;       // 整数
  var Age = 213.747;  // 小数  
  ```

- 数字型进制

  最常见的进制有二进制、八进制、十进制、十六进制。

  ```js
   // 1.八进制数字序列范围：0~7
   var num1 = 07;   // 对应十进制的7
   var num2 = 023;  // 对应十进制的19 (PPT中写的是019是错误的)
   var num3 = 010;   // 对应十进制的8
    // 2.十六进制数字序列范围：0~9以及A~F
   var num = 0xA;   
  ```

  现阶段我们只需要记住，在JS中八进制前面加0，十六进制前面加 0x  

  **进制补充**：

  ```js
  十进制：0-9，逢10进1
  	12: 2*10的0次方+1*10的1次方 = 12
  
  十六进制：0-9，a-f ， 逢16进1
  	0x29 : 9*16的0次方+2*16的1次方 = 41
  
  八进制： 0-7  逢8进1
  	023 ： 3* 8的0次方 + 2* 8的1次方  = 19
  ```

- 数字型范围：JavaScript中数值的最大和最小值

  ```js
  alert(Number.MAX_VALUE); // 1.7976931348623157e+308  （10的正308次方）
  alert(Number.MIN_VALUE); // 5e-324   5e-324 （10的负324次方）
  ```

  - 最大值：Number.MAX_VALUE，这个值为： 1.7976931348623157e+308
  - 最小值：Number.MIN_VALUE，这个值为：5e-32
  - 点：理解为的。Number数字的最大值/最小值

- 数字型三个特殊值

  ```js
  alert(Infinity);  // Infinity
  alert(-Infinity); // -Infinity
  alert(NaN);       // NaN  ***
  //课堂代码：
  // 5. 无穷大
  console.log(Number.MAX_VALUE * 2); // Infinity 无穷大  
  // 6. 无穷小
  console.log(-Number.MAX_VALUE * 2); // -Infinity 无穷大
  // 7. 非数字
  console.log('pink老师' - 100); // NaN：字符串是无法与数字进行运算的，所以结果是一个非数字
  ```

  - Infinity ，代表无穷大，大于任何数值
  - -Infinity ，代表无穷小，小于任何数值
  - NaN ，Not a number，代表一个非数值

- isNaN

  用来判断一个变量/值是否为非数字的类型，返回 true 或者 false

![](images\图片17.png)



代码：

```js
var usrAge = 21;
var isOk = isNaN(userAge);
console.log(isNum);            // false ，21 不是一个非数字
var usrName = "andy";
console.log(isNaN(userName));  // true ，"andy"是一个非数字
console.log(isNaN('jack'))
console.log('jack');
console.log('jack'+'red');
```

**补充**：isNaN()是一个方法，方法： 实现了某个功能的一段代码

**补充理解**： 

- isNaN : is：是否，是不是，NaN：非数字 
- isNaN：是否是非数字，如果是非数字返回真true，如果不是非数字返回假false 

#### 8.2.3 字符串型 String

字符串型可以是引号中的任意文本，其语法为 双引号 "" 和 单引号''

```js
var strMsg = "我爱北京天安门~";  // 使用双引号表示字符串
var strMsg2 = '我爱吃猪蹄~';    // 使用单引号表示字符串
// 常见错误
var strMsg3 = 我爱大肘子;       // 报错，没使用引号，会被认为是js代码，但js没有这些语法
```

因为 HTML 标签里面的属性使用的是双引号，JS 这里我们更推荐使用单引号。

##### 8.2.3.1 字符串引号嵌套

JS 可以用单引号嵌套双引号 ，或者用双引号嵌套单引号 (**外双内单，外单内双**)

```js
var strMsg = '我是"高帅富"程序猿';   // 可以用''包含""
var strMsg2 = "我是'高帅富'程序猿";  // 也可以用"" 包含''
//  常见错误
var badQuotes = 'What on earth?"; // 报错，不能 单双引号搭配
```
##### 8.2.3.2 字符串转义符

类似HTML里面的特殊字符，字符串中也有特殊字符，我们称之为转义符。

**转义符都是 \ 开头的**，常用的转义符及其说明如下：

| 转义符 | 解释说明                                                     |
| ------ | ------------------------------------------------------------ |
| \n     | 换行符，n   是   newline   的意思                            |
| \ \    | 斜杠   \                                                     |
| \\'    | '   单引号                                                   |
| \\"    | ”双引号                                                      |
| \t     | tab  缩进                                                    |
| \b     | 空格 ，b   是   blank  的意思<br />视频中有**问题**<br />\b 是退格backspace，不是空格 |

**总结**：

- 转义符：\ ,  将特殊字符转义为非特殊字符，非特殊字符转义为特殊字符  ***
  - 特殊字符转换为非特殊字符：‘ ---- \\'
  - 非特殊字符转换为特殊字符：n ---- \n

案例-弹出网页警示框：

```js
<script>
        alert('酷热难耐，火辣的太阳底下，我挺拔的身姿，成为了最为独特的风景。\n我审视四周，这里，是我的舞台，我就是天地间的王者。\n这一刻，我豪气冲天，终于大喊一声："收破烂啦～"');
    </script>
```

##### 8.2.3.3 字符串长度  ***

- 字符串是由若干字符组成的，这些字符的数量就是字符串的长度
- 通过字符串的 length 属性可以获取整个字符串的长度

```js
   var strMsg = "我是帅气多金的程序猿！";
   alert(strMsg.length); // 显示 11
```

- **补充**：属性：跟方法一样，也是实现了某个功能的代码，但是不添加小括号

##### 8.2.3.4 字符串拼接 ***

- 多个字符串之间可以使用 + 进行拼接，其拼接方式为 字符串 + 任何类型 = 拼接之后的新字符串

- 拼接前会把与字符串相加的任何类型转成字符串，再拼接成一个新的字符串

  ```js
  //1.1 字符串 "相加"
  alert('hello' + ' ' + 'world'); // hello world
  //1.2 数值字符串 "相加"
  alert('100' + '100'); // 100100
  //1.3 数值字符串 + 数值
  alert('11' + 12);     // 1112 
  //以上的字符串拼接都没有意义，一般我们字符串会与变量进行拼接，这个下边加强会讲
  ```

- **总结**：***+ 号总结口诀：数值相加 ，字符相连***

- 补充：代码执行理解： ***

  ```js
  //console.log(isNaN(12))   
  // （）里边是一个方法，先执行方法，然后再去处理方法的结果
  // console.log(12 + 12); 
  // () 里边是一个表达式，先计算表达式的结果，然后再去处理这个结果
  // 因为是log的(): console.log() ，所以是将结果打印出来
  
  var result = isNaN(12) ;//false
  console.log(result);//false
  
  var myname = 'egg';
  // 如果小括号中是一个变量，先根据变量的名字，找到变量的值，然后再打印
  console.log(myname);
  console.log('twoEgg');
  ```

##### 8.2.3.5 字符串拼接加强 ***

```js
console.log('pink老师' + 18);           // 只要有字符就会相连 
var age = 18;
// console.log('pink老师age岁啦');       // 这样不行哦
console.log('pink老师' + age);          // pink老师18
console.log('pink老师' + age + '岁啦');  // pink老师18岁啦
```

- 经常会将**字符串和变量来拼接**，**变量可以很方便地修改里面的值**
- 变量是不能添加引号的，因为加引号的变量会变成字符串
- 如果变量两侧都有字符串拼接，口诀“引引加加 ”，删掉数字，变量写加中间
- **应用场景**：如果要将写死的字符串通过变量写活，可以使用“引引加加”
	 **补充**：js引擎执行代码的规律：	1. 由上至下	2. 由左至右

#### 8.2.4 布尔型Boolean

- 布尔类型有两个值：true 和 false ，其中 true 表示真（对，有，1），而 false 表示假（错，无，0）

- **布尔型和数字型相加的时候， true 的值为 1 ，false 的值为 0**

  ```js
  console.log(true + 1);  // 2 ，这里其实js引擎对true做了一个隐式转换
  console.log(false + 1); // 1
  ```

- **补充**：

  ```js
  //在定义一个boolean类型的变量时，经常使用的一个变量名
  var flag = false;//true; 
  
  flag: 标记
  ```

#### 8.2.5 Undefined和 Null

- 一个声明后没有被赋值的变量会有一个默认值undefined

- ( 如果进行相连或者相加时，注意结果）

  ```js
  var variable;
  console.log(variable);           // undefined
  console.log('你好' + variable);  // 你好undefined
  console.log(11 + variable);     // NaN
  console.log(true + variable);   //  NaN
  ```

- 一个声明变量给 null 值，里面存的值为空（学习对象时，我们继续研究null)

  ```js
  var vari = null;
  console.log('你好' + vari);  // 你好null
  console.log(11 + vari);     // 11
  console.log(true + vari);   //  1
  ```

- **补充**：只有字符串需要添加引号，其他的都不需要添加：  数字，true，false，undefined，null，变量名

- **总结**：任何数据类型与字符串相加，意味字符串拼接

### 8.3 获取变量数据类型

#### 8.3.1 typeof  ***

- 获取变量的数据类型：typeof 

- 语法如下：

  ```js
  typeof 变量/值   
  ```

- 例子：

  ```js
  var num = 18;
  console.log(typeof num) // 结果 number   
  console.log(typeof 18) // 也可以直接获取值的数据类型   
  ```

- 不同类型的返回值

  ![](images\图片18.png)

  **注意**： 以上结果都是字符串。

  **问题**： typeof null ---- object   检测null的类型竟然是复杂数据类型的对象类型，这其实是一个历史遗留问题

  ​	    按照数据类型分类，null就是null类型，但是小猪佩奇搞错了

  ​	    按理说null应该就是属于对象这种数据类型的，因为很多语言都称null为空对象

  **补充**： typeof 的另一种语法

  ```js
  语法：
  typeof(变量/值) 
  例子：
  var num = 18;
  console.log(typeof(num)) // 结果 number   
  console.log(typeof(18)) // 也可以直接获取值的数据类型 
  console.log( typeof( typeof(18) ) )
  ```

#### 8.3.2 字面量

字面量是在源代码中一个固定值的表示法，通俗来说，就是字面量表示如何表达这个值。

- 数字字面量：0-9组成的数字
- 字符串字面量：‘’或 “”
- 布尔字面量：true，false

字面量**理解**：从字面意思就可以知道是什么数据类型

### 8.4 数据类型转换

- 什么是数据类型转换	
   - 使用表单、prompt 获取过来的数据默认是字符串类型的，
   - 此时就不能直接简单的进行加法运算，而需要转换变量的数据类型。
   - 通俗来说，就是把一种数据类型的变量转换成另外一种数据类型。

- 通常会实现3种方式的转换：
    - 转换为字符串类型
    - 转换为数字型
    - 转换为布尔型

- 转换为字符串

  ![](images\图片19.png)

  - toString() 和 String()  使用方式不一样。
  - 三种转换方式，更多第三种加号拼接字符串转换方式， 这一种方式也称之为隐式转换。
  - **重点掌握**：toString()和+

- 转换为数字型（重点）

  ![](images\图片20.png)

  - 注意 parseInt 和 parseFloat 单词的大小写，这2个是重点

  - 隐式转换是我们在进行算数运算的时候，JS 自动转换了数据类型

  - **重点掌握**：parseInt()和parseFloat()

  - parse，解析；int，integer，整数；

  - float：小数，浮点数。浮点数理解：小数点可以左右浮动（其实只需要看到浮点数这个词中有个点）

  - 代码：

    ```js
    var num1 = parseInt("12.3abc");  //12，如果第一个字符是数字会解析直到遇到非数字结束
    var num2 = parseInt("abc123");   //NaN，如果第一个字符不是数字或者符号就返回NaN
    
    parseFloat('12.34'); //12.34
    parseFloat('12.34.56');//12.34 //parseFloat会解析第一个. 遇到第二个.或者非数字结束
    parseFloat('12.34a'); //12.34
    ```

- 转换为布尔型

  ![](images\图片21.png)

  - **代表空、否定的值会被转换为 false  ，如 ''、0、NaN、null、undefined*****  

  - 其余值都会被转换为 true

    ```js
    console.log(Boolean('')); // false·
    console.log(Boolean(0)); // false
    console.log(Boolean(NaN)); // false
    console.log(Boolean(null)); // false
    console.log(Boolean(undefined)); // false
    console.log(Boolean('小白')); // true
    console.log(Boolean(12)); // true
    ```


## 9.  解释型语言和编译型语言

### 9.1 概述

- 计算机不能直接理解任何除机器语言以外的语言，所以必须要把程序员所写的程序语言翻译成机器语言才能执行程序。程序语言翻译成机器语言的工具，被称为翻译器。

![](images\图片22.png)

-  翻译器翻译的方式有两种：一个是编译，另外一个是解释。两种方式之间的区别在于翻译的时间点不同
-  编译器是在代码执行之前进行编译，生成中间代码文件
-  解释器是在运行时进行及时解释，并立即执行(当编译器以解释方式运行的时候，也称之为解释器)

### 9.2 执行过程

![](images\图片23.png)

- 类似于请客吃饭：


​	编译语言：首先把所有菜做好，才能上桌吃饭

​	解释语言：好比吃火锅，边吃边涮，同时进行

## 10.  关键字和保留字

### 10.1 标识符

- 标识(zhi)符：就是指开发人员为变量、属性、函数、参数取的名字。
- 标识符不能是关键字或保留字。

### 10.2 关键字

- 关键字：是指 JS本身已经使用了的字，不能再用它们充当变量名、方法名。
- 包括：break、case、catch、continue、default、delete、do、else、finally、for、function、if、in、instanceof、new、return、switch、this、throw、try、typeof、var、void、while、with 等。

### 10.3 保留字

- 保留字：实际上就是预留的“关键字”，意思是现在虽然还不是关键字，但是未来可能会成为关键字，同样不能使用它们当变量名或方法名。

- 包括：boolean、byte、char、class、const、debugger、double、enum、export、extends、fimal、float、goto、implements、import、int、interface、long、mative、package、private、protected、public、short、static、super、synchronized、throws、transient、volatile 等。

- 注意：如果将保留字用作变量名或函数名，那么除非将来的浏览器实现了该保留字，否则很可能收不到任何错误消息。当浏览器将其实现后，该单词将被看做关键字，如此将出现关键字错误。


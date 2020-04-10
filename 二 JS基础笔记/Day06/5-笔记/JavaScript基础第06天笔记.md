# JavaScript基础第06天笔记

## 1.  内置对象

### 1.1 内置对象

-  JavaScript 中的对象分为3种：**自定义对象 、内置对象、 浏览器对象**
-  前面两种对象是JS 基础 内容，属于 ECMAScript；  
-  第三个浏览器对象属于 JS 独有的， JS API 讲解内置对象就是指 JS 语言自带的一些对象，这些对象供开发者使用，并提供了一些常用的或是**最基本而必要的功能**（属性和方法），内置对象最大的优点就是帮助我们快速开发
	  JavaScript 提供了多个内置对象：Math、 Date 、Array、String等	


### 1.2 查文档

- 查找文档：学习一个内置对象的使用，只要学会其常用成员的使用即可，我们可以通过查文档学习，可以通过MDN/W3C来查询。
- Mozilla 开发者网络（MDN）提供了有关开放网络技术（Open Web）的信息，包括 HTML、CSS 和万维网及 HTML5 应用的 API。
- MDN:   https://developer.mozilla.org/zh-CN/

### 1.3 Math对象

#### 1.3.1 介绍

​	Math 对象**不是构造函数**，它**具有数学常数和函数的属性和方法**。跟数学相关的运算（求绝对值，取整、最大值等）可以使用 Math 中的成员。

| 属性、方法名          | 功能                                         |
| --------------------- | -------------------------------------------- |
| Math.PI               | 圆周率                                       |
| Math.floor()          | 向下取整 （parseInt()）                      |
| Math.ceil()           | 向上取整                                     |
| Math.round()          | 四舍五入版 就近取整   注意 -3.5   结果是  -3 |
| Math.abs()            | 绝对值                                       |
| Math.max()/Math.min() | 求最大和最小值                               |
| Math.random()         | 获取范围在[0,1)内的随机值                    |

注意：上面的方法使用时必须带括号

#### 1.3.2 例子

例子：最大值

```js
console.log(Math.PI); // 一个属性 圆周率
console.log(Math.max(1, 99, 3)); // 99
console.log(Math.max(-1, -10)); // -1
console.log(Math.max(1, 99, 'pink老师')); // NaN
console.log(Math.max()); // -Infinity
```

例子：封装自己的数学对象

```js
// 利用对象封装自己的数学对象  里面有 PI 最大值和最小值
var myMath = {
    PI: 3.141592653,
    max: function() {
        var max = arguments[0];
        for (var i = 1; i < arguments.length; i++) {
            if (arguments[i] > max) {
                max = arguments[i];
            }
        }
        return max;
    },
    min: function() {
        var min = arguments[0];
        for (var i = 1; i < arguments.length; i++) {
            if (arguments[i] < min) {
                min = arguments[i];
            }
        }
        return min;
    }
}
console.log(myMath.PI);
console.log(myMath.max(1, 5, 9));
console.log(myMath.min(1, 5, 9));
```

例子：其他方法

```js
// 1.绝对值方法
console.log(Math.abs(1)); // 1
console.log(Math.abs(-1)); // 1
console.log(Math.abs('-1')); // 隐式转换 会把字符串型 -1 转换为数字型
console.log(Math.abs('pink')); // NaN 

// 2.三个取整方法
// (1) Math.floor()   地板 向下取整  往最小了取值
console.log(Math.floor(1.1)); // 1
console.log(Math.floor(1.9)); // 1
// (2) Math.ceil()   ceil 天花板 向上取整  往最大了取值
console.log(Math.ceil(1.1)); // 2
console.log(Math.ceil(1.9)); // 2
// (3) Math.round()   四舍五入  其他数字都是四舍五入，但是 .5 特殊 它往大了取  
console.log(Math.round(1.1)); // 1
console.log(Math.round(1.5)); // 2
console.log(Math.round(1.9)); // 2
console.log(Math.round(-1.1)); // -1
console.log(Math.round(-1.5)); // 这个结果是 -1
```

#### 1.3.2 随机数 ***

Math对象随机数方法   random() 返回一个随机的小数  0 =< x < 1    [0,1)

例子：

```js
console.log(Math.random());//这个方法里面不跟参数
```

**获取指定范围内的随机整数**：这是个固定写法，大家不需要记忆，知道怎么用即可。

```js
function getRandom(min, max) {
  return Math.floor(Math.random() * (max - min + 1)) + min; 
  //传入1,10，过程如下：
  //Math.floor( 0 =< x < 1 * (max - min + 1) ) + min;
  //Math.floor( 0 =< x < 1 * 10 ) + min;
  //Math.floor( 0 =< x < 10  ) + min; // 这个是带小数的范围
  // 0 =< x < 10  + 1; // 取过floor之后就是整数
  // 1 =< x < 11  // [1,10]
}
```

案例-随即点名：

```js
var arr = ['张三', '张三丰', '张三疯子', '李四', '李思思', 'pink老师'];
// console.log(arr[0]);
console.log(arr[getRandom(0, arr.length - 1)]);
```

案例-猜数字游戏：

```js
// 猜数字游戏
// 1.随机生成一个1~10 的整数  我们需要用到 Math.random() 方法。
// 2.需要一直猜到正确为止，所以需要一直循环。
// 3.while 循环更简单
// 4.核心算法：使用 if  else if 多分支语句来判断大于、小于、等于。
function getRandom(min, max) {
    return Math.floor(Math.random() * (max - min + 1)) + min;
}
var random = getRandom(1, 10);
while (true) { // 死循环
    var num = prompt('你来猜？ 输入1~10之间的一个数字');
    if (num > random) {
        alert('你猜大了');
    } else if (num < random) {
        alert('你猜小了');
    } else {
        alert('你好帅哦，猜对了');
        break; // 退出整个循环结束程序
    }

}
// 要求用户猜 1~50之间的一个数字 但是只有 10次猜的机会（课后作业）
```

### 1.4 日期对象

#### 1.4.1 日期对象介绍

- 介绍
  - Date 对象和 Math 对象不一样，**Date是一个构造函数**
  - 所以使用时需要实例化后才能使用其中具体方法和属性
  - Date 实例用来处理日期和时间

- 使用Date实例化日期对象

  - 获取当前时间必须实例化：

  ```js
  var now = new Date();//当前时间对应的日期对象
  ```

  - 获取指定时间的日期对象

  ```js
  var time = new Date('2019/5/1');//指定时间对应的日期对象
  ```

  **注意**：如果创建实例时并未传入参数，则得到的日期对象是当前时间对应的日期对象

- 例子：

  ```js
  // Date() 日期对象  是一个构造函数 必须使用new 来调用创建我们的日期对象
  var arr = new Array(); // 创建一个数组对象
  var obj = new Object(); // 创建了一个对象实例
  // 1. 使用Date  如果没有参数 返回当前系统的当前时间
  var date = new Date();
  console.log(date);
  // 2. 参数常用的写法  数字型  2019, 10, 01  或者是 字符串型 '2019-10-1 8:8:8'
  var date1 = new Date(2019, 10, 1);
  console.log(date1); // 返回的是 11月 不是 10月 
  var date2 = new Date('2019-10-1 8:8:8');
  console.log(date2);
  ```

####  1.4.2  日期对象的方法和属性

Date实例的方法和属性	，如下图：

![](images\图片1.png)

**注意**：这里有几个特殊的方法

- getFullYear，为啥不是getYear，因为getYear获取的是两位年份比如2019年获取的是19，或者是距离1970的年份差。getFullYear获取的是四位年份，比较常用
- getDay，获取的是周几，有同学想为啥不是getWeek。估计小猪佩奇在制定这个方法名的时候脑袋被驴踢了，起的不太好

#### 1.4.3 格式化日期

- 日期默认格式是外国人习惯的格式，我们需要给他格式化为中国特有的格式

- 获取日期指定部分，然后按照要求格式，进行拼接即可

- 代码--格式年月日：

  ```js
  // 格式化日期 年月日 
  var date = new Date();
  console.log(date.getFullYear()); // 返回当前日期的年  2019
  console.log(date.getMonth() + 1); // 月份 返回的月份小1个月   记得月份+1 呦
  console.log(date.getDate()); // 返回的是 几号
  console.log(date.getDay()); // 3  周一返回的是 1 周六返回的是 6 但是 周日返回的是 0
  // 我们写一个 2019年 5月 1日 星期三
  var year = date.getFullYear();
  var month = date.getMonth() + 1;
  var dates = date.getDate();
  var arr = ['星期日', '星期一', '星期二', '星期三', '星期四', '星期五', '星期六'];
  var day = date.getDay();
  console.log('今天是：' + year + '年' + month + '月' + dates + '日 ' + arr[day]);
  ```

  - 注意：0-6转换为星期日-星期六，这个做法大家肯定一开始是想不到的。这里只需要理解即可。
  - 以后碰到将一组数字转换为一组对应的文字这种情况时，能够相关用数组即可。

- 代码--格式化时分秒

  ```js
  // 格式化日期 时分秒
  var date = new Date();
  console.log(date.getHours()); // 时
  console.log(date.getMinutes()); // 分
  console.log(date.getSeconds()); // 秒
  // 要求封装一个函数返回当前的时分秒 格式 08:08:08
  function getTimer() {
      var time = new Date();
      var h = time.getHours();
      h = h < 10 ? '0' + h : h;
      var m = time.getMinutes();
      m = m < 10 ? '0' + m : m;
      var s = time.getSeconds();
      s = s < 10 ? '0' + s : s;
      return h + ':' + m + ':' + s;
  }
  console.log(getTimer());
  ```

#### 1.4.4 通过Date实例获取总毫秒数

- 总毫秒数的含义

  - 基于1970年1月1日（世界标准时间）起的毫秒数（不是从公元0年开始数的毫秒数）

  - 总的毫秒数，又叫做时间戳， 不是当前时间的毫秒数 而是距离1970年1月1号过了多少毫秒数 
  - 时间戳，戳代表唯一，因为这个总的毫秒数是唯一的
  - 戳就可以理解为公章，一个公司的公章只会有一个，是唯一的。

- 获取总毫秒数

  ```js
  // 实例化Date对象
  var now = new Date();
  // 1. 用于获取对象的原始值
  console.log(date.valueOf())	
  console.log(date.getTime())	
  // 2. 简单写可以这么做
  var now = + new Date();			
  // 3. HTML5中提供的方法，有兼容性问题
  var now = Date.now();
  ```

#### 1.4.5 案例--倒计时

```js
// 倒计时效果
// 1.核心算法：输入的时间减去现在的时间就是剩余的时间，即倒计时 ，但是不能拿着时分秒相减，比如 05 分减去25分，结果会是负数的。
// 2.用时间戳来做。用户输入时间总的毫秒数减去现在时间的总的毫秒数，得到的就是剩余时间的毫秒数。
// 3.把剩余时间总的毫秒数转换为天、时、分、秒 （时间戳转换为时分秒）
// 转换公式如下： 
//  d = parseInt(总秒数/ 60/60 /24);    //  计算天数
//  h = parseInt(总秒数/ 60/60 %24)   //   计算小时
//  m = parseInt(总秒数 /60 %60 );     //   计算分数
//  s = parseInt(总秒数%60);            //   计算当前秒数
function countDown(time) {
    var nowTime = +new Date(); // 返回的是当前时间总的毫秒数
    var inputTime = +new Date(time); // 返回的是用户输入时间总的毫秒数
    var times = (inputTime - nowTime) / 1000; // times是剩余时间总的秒数 
    var d = parseInt(times / 60 / 60 / 24); // 天
    d = d < 10 ? '0' + d : d;
    var h = parseInt(times / 60 / 60 % 24); //时
    h = h < 10 ? '0' + h : h;
    var m = parseInt(times / 60 % 60); // 分
    m = m < 10 ? '0' + m : m;
    var s = parseInt(times % 60); // 当前的秒
    s = s < 10 ? '0' + s : s;
    return d + '天' + h + '时' + m + '分' + s + '秒';
}
console.log(countDown('2019-5-1 18:00:00'));
var date = new Date();
console.log(date);
```

**注意**：秒数转换为天，时分秒的公示不需要记忆。

 	    小任务：将97201 s转换为天时分秒（进而理解上述公式）

### 1.5 数组对象

#### 1.5.1 创建数组的两种方式

- 字面量方式 ：

  - 示例代码如下

    ```js
    var arr = [1,"test",true];
    ```

- new Array() 方式 ：

  - 示例代码如下

    ```
    var arr = new Array();
    ```

  		注意：上面代码中arr创建出的是一个空数组，如果需要使用构造函数Array创建非空数组，可以在创建数组时传入参数

  参数传递规则如下：

  - 如果只传入一个参数，则参数规定了数组的长度
  - 如果传入了多个参数，则参数称为数组的元素

- 例子：

  ```js
  // 创建数组的两种方式
  // 1. 利用数组字面量
  var arr = [1, 2, 3];
  console.log(arr[0]);
  
  // 2. 利用new Array()
  // var arr1 = new Array();  // 创建了一个空的数组
  // var arr1 = new Array(2);  // 这个2 表示 数组的长度为 2  里面有2个空的数组元素 
  var arr1 = new Array(2, 3); // 等价于 [2,3]  这样写表示 里面有2个数组元素 是 2和3
  console.log(arr1);
  ```

#### 1.5.2 检测是否为数组

- instanceof 运算符

  - instanceof 可以判断一个对象是否是某个构造函数的实例

  - 语法：

    ```js
    A instanceof B : 判断A是否是B的一个实例（对象）
    ```

  - 例子：

    ```js
    var arr = [1, 23];
    var obj = {};
    console.log(arr instanceof Array); // true，arr是不是Array的实例？是的
    console.log(obj instanceof Array); // false，obj是不是Array的实例？不是
    ```

  - instance：实例，of：谁的

  - instanceof：谁的实例，谁的对象

- Array.isArray()

  - Array.isArray()用于判断一个对象是否为数组，isArray() 是 HTML5 中提供的方法

    ```js
    var arr = [1, 23];
    var obj = {};
    console.log(Array.isArray(arr));   // true
    console.log(Array.isArray(obj));   // false
    ```

  - **注意**：Array是一个构造函数，但是isArray()方法比较特殊，是属于Array的方法，不需要实例化就可以调用

- instanceof 与 typeof区别

  - typeof用于检查数据是否为简单数据类型和object (**没有办法检测object的具体分类)**

  - instanceof用于某个对象是否为某个类的实例（某个构造函数创建出来的）  ， **用于检测具体是哪一类对象 ： Person，Star，Array**

  - 例子：

    ```js
    //比如现在有如下构造函数，如下对应的对象：
    Person，Star，Array
    zs      ldh    arr
    //判断如下：
    zs instanceof Person    true
    ldh instanceof Star     true
    
    typeof zs  ---- object //只能知道zs是对象，但是不知道是Person类对象
    typeof ldh ---- object
    typeof arr ---- object
    
    //但是：要与Object进行对比，都为true，万物即为对象
    console.log(arr instanceof Object);  // true :  Array也是Object，是其中的一种分类，Array属于Object
    console.log(obj instanceof Object);// true 
    console.log(zs instanceof Object);// true 
    
    ```

  - 总结：

    - typeof  用来检测数据是哪种数据类型：简单：number ， string ， boolean ， undefined ， null  复杂：object		
    - 比如：typeof  zs ---- object , typeof只能检测出来zs是一个对象object，但是不能检测他的具体类型
    - instanceof 用来检测复杂数据object的具体类型(具体分类下的对象)：  
    -  比如： zs是否为Person的一个实例 ： zs instanceof Person ---- true

#### 1.5.3 添加删除数组元素的方法

- 数组中有进行增加、删除元素的方法，部分方法如下表

  ![](images\图片2.png)

  注意：push、unshift为增加元素方法；pop、shift为删除元素的方法

- **理解**：

  - push：推，推进去。往后边添加
  - pop：崩，崩掉。删掉最后一个
  - unshift：shift：去掉，un: 取反义词，去掉反义词就是添加。开头添加
  - shift：开头删除一个

- 代码：

  ```js
  // 添加删除数组元素方法
  // 1. push() 在我们数组的末尾 添加一个或者多个数组元素   push  推
  var arr = [1, 2, 3];
  // arr.push(4, 'pink');
  console.log(arr.push(4, 'pink'));
  
  console.log(arr);
  // (1) push 是可以给数组追加新的元素
  // (2) push() 参数直接写 数组元素就可以了
  // (3) push完毕之后，返回的结果是 新数组的长度 
  // (4) 原数组也会发生变化
  // 2. unshift 在我们数组的开头 添加一个或者多个数组元素
  console.log(arr.unshift('red', 'purple'));
  
  console.log(arr);
  // (1) unshift是可以给数组前面追加新的元素
  // (2) unshift() 参数直接写 数组元素就可以了
  // (3) unshift完毕之后，返回的结果是 新数组的长度 
  // (4) 原数组也会发生变化
  
  // 3. pop() 它可以删除数组的最后一个元素  
  console.log(arr.pop());
  console.log(arr);
  // (1) pop是可以删除数组的最后一个元素 记住一次只能删除一个元素
  // (2) pop() 没有参数
  // (3) pop完毕之后，返回的结果是 删除的那个元素 
  // (4) 原数组也会发生变化
  // 4. shift() 它可以删除数组的第一个元素  
  console.log(arr.shift());
  console.log(arr);
  // (1) shift是可以删除数组的第一个元素 记住一次只能删除一个元素
  // (2) shift() 没有参数
  // (3) shift完毕之后，返回的结果是 删除的那个元素 
  // (4) 原数组也会发生变化
  ```

- 案例-筛选数组：

  ```js
  // 有一个包含工资的数组[1500, 1200, 2000, 2100, 1800]，要求把数组中工资超过2000的删除，剩余的放到新数组里面
  var arr = [1500, 1200, 2000, 2100, 1800];
  var newArr = [];
  for (var i = 0; i < arr.length; i++) {
      if (arr[i] < 2000) {
          // newArr[newArr.length] = arr[i];
          newArr.push(arr[i]);
      }
  }
  console.log(newArr);
  ```

#### 1.5.4 数组排序（不讲）

- 数组中有对数组本身排序的方法，部分方法如下表

  ![](images\图片3.png)

  注意：sort方法需要传入参数来设置升序、降序排序

  - 如果传入“function(a,b){ return a-b;}”，则为升序
  - 如果传入“function(a,b){ return b-a;}”，则为降序

- 代码：

  ```js
  // 数组排序
  // 1. 翻转数组
  var arr = ['pink', 'red', 'blue'];
  arr.reverse();
  console.log(arr);
  
  // 2. 数组排序（冒泡排序）
  var arr1 = [13, 4, 77, 1, 7];
  arr1.sort(function(a, b) {
      //  return a - b; 升序的顺序排列
      return b - a; // 降序的顺序排列
  });
  console.log(arr1);
  ```

#### 1.5.5 数组索引方法 （不讲）

- 数组中有获取数组指定元素索引值的方法，部分方法如下表

  ![](images\图片4.jpg)

- 代码：

  ```js
  // 返回数组元素索引号方法  indexOf(数组元素)  作用就是返回该数组元素的索引号 从前面开始查找
  // 它只返回第一个满足条件的索引号 
  // 它如果在该数组里面找不到元素，则返回的是 -1  
  // var arr = ['red', 'green', 'blue', 'pink', 'blue'];
  var arr = ['red', 'green', 'pink'];
  console.log(arr.indexOf('green'));
  // 返回数组元素索引号方法  lastIndexOf(数组元素)  作用就是返回该数组元素的索引号 从后面开始查找
  var arr = ['red', 'green', 'blue', 'pink', 'blue'];
  console.log(arr.lastIndexOf('blue')); // 4
  ```

#### 1.5.6 数组转换为字符串

- 数组中有把数组转化为字符串的方法，部分方法如下表

  ![](images\图片5.png)

  注意：join方法如果不传入参数，则按照 “ , ”拼接元素

- 代码：

  ```js
  // 数组转换为字符串 
  // 1. toString() 将我们的数组转换为字符串
  var arr = [1, 2, 3];
  console.log(arr.toString()); // 1,2,3
  // 2. join(分隔符) 
  var arr1 = ['green', 'blue', 'pink'];
  console.log(arr1.join()); // green,blue,pink （如果不指定分隔符，那么与toString一致，以逗号分隔）
  console.log(arr1.join('-')); // green-blue-pink
  console.log(arr1.join('&')); // green&blue&pink
  ```

#### 1.5.7 其他方法 （自己查询用法）

- 数组中还有其他操作方法，同学们可以在课下自行查阅学习

	![](images\图片6.png)

### 1.6 字符串对象

#### 1.6.1 基本包装类型

- 为了方便操作基本数据类型，JavaScript 还提供了三个特殊的引用类型：String、Number和 Boolean。

- **基本包装类型就是把简单数据类型包装成为复杂数据类型**，这样**基本数据类型就有了属性和方法**。

- 我们来看一个问题：

  ```js
  // 下面代码有什么问题？
  var str = 'andy';
  console.log(str.length);
  ```

- 按道理基本数据类型是没有属性和方法的，而对象才有属性和方法，但上面代码却可以执行，这是因为js 会把基本数据类型包装为复杂数据类型，其执行过程如下 ：

  ```js
  // 1. 生成临时变量，把简单类型包装为复杂数据类型
  var temp = new String('andy');
  // 2. 赋值给我们声明的字符变量
  str = temp;
  // 3. 销毁临时变量
  temp = null;
  ```

#### 1.6.2 字符串的不可变

- 指的是里面的值不可变，虽然看上去可以改变内容，但其实是地址变了，内存中新开辟了一个内存空间。

- **当重新给字符串变量赋值的时候，变量之前保存的字符串不会被修改，依然在内存中重新给字符串赋值，会重新在内存中开辟空间，这个特点就是字符串的不可变**。

- 由于字符串的不可变，在**大量拼接字符串**的时候会有效率问题

- 例子：

  ```js
  var str = 'abc';
  str = 'hello';
  // 当重新给 str 赋值的时候，常量'abc'不会被修改，依然在内存中
  // 重新给字符串赋值，会重新在内存中开辟空间，这个特点就是字符串的不可变
  // 由于字符串的不可变，在大量拼接字符串的时候会有效率问题
  var str = '';
  for (var i = 0; i < 100000; i++) {
      str += i;
  }
  console.log(str); // 这个结果需要花费大量时间来显示，因为需要不断的开辟新的空间
  ```

- 总结：

  - **由于字符串的不可变，导致字符串所有的方法，都不会修改字符串本身，操作完成会返回一个新的字符串**
  - 字符串不可变，指的是字符串本身在内存中不会改变
  - 字符串变量存储的值可以改变

#### 1.6.3 根据字符返回位置

- 字符串通过基本包装类型可以调用部分方法来操作字符串，以下是返回指定字符的位置的方法：


![](images\图片7.png)

- 代码：

  ```js
  // 字符串对象  根据字符返回位置  str.indexOf('要查找的字符', [起始的位置])
  var str = '改革春风吹满地，春天来了';
  console.log(str.indexOf('春'));
  console.log(str.indexOf('春', 3)); // 从索引号是 3的位置开始往后查找
  ```

- 案例：查找字符串"abcoefoxyozzopp"中所有o出现的位置以及次数 （不讲）

1. 先查找第一个o出现的位置

2. 然后 只要indexOf 返回的结果不是 -1 就继续往后查找

3. 因为indexOf 只能查找到第一个，所以后面的查找，利用第二个参数，当前索引加1，从而继续查找 

  ```js
  // 查找字符串"abcoefoxyozzopp"中所有o出现的位置以及次数
  // 核心算法：先查找第一个o出现的位置
  // 然后 只要indexOf 返回的结果不是 -1 就继续往后查找
  // 因为indexOf 只能查找到第一个，所以后面的查找，一定是当前索引加1，从而继续查找
  var str = "oabcoefoxyozzopp";
  var index = str.indexOf('o');
  var num = 0;
  // console.log(index);
  while (index !== -1) {
      console.log(index);
      num++;
      index = str.indexOf('o', index + 1);
  }
  console.log('o出现的次数是: ' + num);
  // 课后作业 ['red', 'blue', 'red', 'green', 'pink','red'], 求 red 出现的位置和次数
  ```

#### 1.6.4 根据位置返回字符

- 字符串通过基本包装类型可以调用部分方法来操作字符串，以下是根据位置返回指定位置上的字符：


![](images\图片8.png)

​	  **注意**：为啥字符串可以通过str[index]方式获取指定位置字符，因为字符串是字符数组。

- 在上述方法中，charCodeAt方法返回的是指定位置上字符对应的ASCII码，ASCII码对照表如下：

![](images\图片9.png)

- 代码：

  ```js
  // 根据位置返回字符
  // 1. charAt(index) 根据位置返回字符
  var str = 'andy';
  console.log(str.charAt(3));
  // 遍历所有的字符
  for (var i = 0; i < str.length; i++) {
      console.log(str.charAt(i));
  }
  // 2. charCodeAt(index)  返回相应索引号的字符ASCII值 目的： 判断用户按下了那个键 
  console.log(str.charCodeAt(0)); // 97
  // 3. str[index] H5 新增的
  console.log(str[0]); // a
  ```

	 案例：判断一个字符串 'abcoefoxyozzopp' 中出现次数最多的字符，并统计其次数	

  ```js
  //  判断一个字符串 'abcoefoxyozzopp' 中出现次数最多的字符，并统计其次数。
  // o.a = 1
  // o.b = 1
  // o.c = 1
  // o.o = 4
  // 核心算法：利用 charAt(） 遍历这个字符串
  // 把每个字符都存储给对象， 如果对象没有该属性，就为1，如果存在了就 +1
  // 遍历对象，得到最大值和该字符
  var str = 'abcoefoxyozzopp';
  var o = {}; // {'a':1,'b':1,'c':1,'o':4,'e:'1,'f':1}
  for (var i = 0; i < str.length; i++) {
      var chars = str.charAt(i); // chars 是 字符串的每一个字符 : a,b,c,o.....o
      // 判断chars中的字符，是否在o对象中
      // o[chars] 得到的是属性值 ： 
      // 循环第一次：if(o['a']) --- 取出o对象中属性名叫做a的属性值 ， 没有默认值为undefined
      //      if(undefined) : if小括号内有隐式转换---- false
      // 如果循环到第二个o，o['o'] --- 1  --- true ，o中有o属性，有的话值就++
      if (o[chars]) {
          o[chars]++; // o['o']=o['o']+1
      } else { // 代表当前o对象中没有chars存储的字符的属性  ， o没有a属性
          o[chars] = 1; // 没有就添加一个a属性，并且给a添加值为1.----- o['a'] = 1
      }
  }
  console.log(o);
  // 2. 遍历对象
  var max = 0;
  var ch = '';
  for (var k in o) { //k='a' , k='o'
      // k 得到是 属性名
      // o[k] 得到的是属性值
      if (o[k] > max) { //  o['a'] > max  -- 1 > 0   ,  o['o']  > max  , 4 > 1
          max = o[k]; // max = 1  , max = 4
          ch = k; //     ch = 'a' , ch = 'o'
      }
  }
  console.log(max);
  console.log('最多的字符是' + ch);
  ```

#### 1.6.5 字符串操作方法

- 字符串通过基本包装类型可以调用部分方法来操作字符串，以下是部分操作方法：


![](images\图片10.png)

- 重点掌握substr即可

- 代码：

  ```js
  // 字符串操作方法
  // 1. concat('字符串1','字符串2'....)
  var str = 'andy';
  console.log(str.concat('red'));
  
  // 2. substr('截取的起始位置', '截取几个字符');
  var str1 = '改革春风吹满地';
  console.log(str1.substr(2, 2)); // 第一个2 是索引号的2 从第几个开始  第二个2 是取几个字符
  ```

- 注意：

  ```js
  // 字符串操作方法，都是操作完之后返回新字符串
  // 比如 concat('字符串1','字符串2'....)
  var str = 'andy';
  console.log(str.concat('red'));// 由于字符串不可变性，所以是在新字符串长进行操作，并返回，不操作原字符串：andyred
  console.log(str);//原字符串的内容没有改变：red
  ```

#### 1.6.7 replace()方法

replace() 方法用于在字符串中用一些字符替换另一些字符，其使用格式如下：  

```js
replace(oldStr,newStr)；//将oldStr替换为newStr
```

#### 1.6.8 split()方法

- split()方法用于切分字符串，它可以将字符串切分为数组。在切分完毕之后，返回的是一个新数组。

- 其使用格式如下：


```js
字符串.split("分割字符")
```

- 代码：

```js
// 1. 替换字符 replace('被替换的字符', '替换为的字符')  它只会替换第一个字符
var str = 'andyandy';
console.log(str.replace('a', 'b'));
// 有一个字符串 'abcoefoxyozzopp'  要求把里面所有的 o 替换为 *
var str1 = 'abcoefoxyozzopp';
while (str1.indexOf('o') !== -1) {
    str1 = str1.replace('o', '*');
}
console.log(str1);

// 2. 字符转换为数组 split('分隔符')    前面我们学过 join 把数组转换为字符串
var str2 = 'red, pink, blue';
console.log(str2.split(','));
var str3 = 'red&pink&blue';
console.log(str3.split('&'));
```

#### 1.6.9 字符串与数组

- 字符串与数组的很多地方都类似
- 因为字符串，又成字符数组 ：var str = ’abc‘；  // str_arr = ['a','b','c']
- 数组的方法： 根据元素返回位置
   1.indexOf(xxx) 
   	查找xxx在数组中第一次出现的索引，如果不存在返回-1
   	arr.indexOf('pink')
   2.lastIndexOf(xxx)
   	查找xxx在数组中最后一次出现的索引，如果不存在返回-1
     字符串的方法	： 根据某个/某些字符返回位置
   1.indexOf(xxx) 
   	查找xxx在字符串中第一次出现的索引，如果不存在返回-1
   	str.indexOf('abc')
   2.lastIndexOf(xxx)
   	查找xxx在字符串中最后一次出现的索引，如果不存在返回-1
	 length属性	

```js
str.length   //字符串的长度
arr.length   //数组的长度
```

## 2.  简单数据类型和复杂数据类型

### 2.1 简单数据类型

**简单类型**（**基本数据类型**、**值类型**）：在存储时变量中存储的是值本身，包括string ，number，boolean，undefined，null

### 2.2 复杂数据类型

复杂数据类型（引用类型）：在存储时变量中存储的仅仅是地址（引用），通过 new 关键字创建的对象（系统对象、自定义对象），如 Object、Array、Date等；

### 2.3 堆栈

- 堆栈空间分配区别：

　　1、栈（操作系统）：由操作系统自动分配释放存放函数的参数值、局部变量的值等。其操作方式类似于数据结构中的栈；

简单数据类型存放到栈里面

　　2、堆（操作系统）：存储复杂类型(对象)，一般由程序员分配释放，若程序员不释放，由垃圾回收机制回收。

![](images\图片11.png)

- 简单数据类型的存储方式

  值类型变量的数据直接存放在变量（栈空间）中

![](images\图片12.png)

- 复杂数据类型的存储方式

  引用类型变量（栈空间）里存放的是地址，真正的对象实例存放在堆空间中

  ![](images\图片13.png)

### 2.4 简单类型传参

​	函数的形参也可以看做是一个变量，当我们把一个值类型变量作为参数传给函数的形参时，其实是把变量在栈空间里的值复制了一份给形参，那么在方法内部对形参做任何修改，都不会影响到的外部变量。

```js
function fn(a) {
    a++;
    console.log(a); 
}
var x = 10;
fn(x);
console.log(x)；
```

运行结果如下：

![](images\图片14.png)

### 2.5 复杂数据类型传参

​	函数的形参也可以看做是一个变量，当我们把引用类型变量传给形参时，其实是把变量在栈空间里保存的堆地址复制给了形参，形参和实参其实保存的是同一个堆地址，所以操作的是同一个对象。

```JavaScript
function Person(name) {
    this.name = name;
}
function f1(x) { // x = p
    console.log(x.name); // 2. 这个输出什么 ?    
    x.name = "张学友";
    console.log(x.name); // 3. 这个输出什么 ?    
}
var p = new Person("刘德华");
console.log(p.name);    // 1. 这个输出什么 ?   
f1(p);
console.log(p.name);    // 4. 这个输出什么 ?  
```

运行结果如下：

![](images\图片15.png)

**总结**：

- 简单数据类型传参和复杂数据类型传参都遵循一个规则。

- **将实参在栈中存储的内容，复制一份，赋值给形参**。
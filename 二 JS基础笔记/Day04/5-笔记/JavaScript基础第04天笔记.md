# JavaScript基础第04天笔记

## 1 数组 ***

### 1.1 数组的概念

- 数组可以把**一组相关的数据一起存放**，并提供方便的访问(获取）方式
- 数组是指**一组数据的集合**，其中的每个数据被称作**元素**（项）
- 在数组中可以**存放任意类型的元素**
  - 在数组中可以存放任意类型的元素，但是我们一般会把**一组相关的，并且数据类型相同的数据一起存放**
- 数组是一种将一组数据存储在单个变量名下的优雅方式
- **数组的理解**：数据组合，数据集合

### 1.2 创建数组

- JS 中创建数组有两种方式：
  1. 利用  new 创建数组  

  ```js
  var 数组名 = new Array() ；
  var arr = new Array();   // 创建一个新的空数组
  ```

     **注意:** Array () ，A 要大写    

  2. 利用数组字面量创建数组 ***

  ```js
  //1. 使用数组字面量方式创建空的数组
  var  数组名 = []；
  //2. 使用数组字面量方式创建带初始值的数组
  var  数组名 = ['小白','小黑','大黄','瑞奇'];
  ```

  - 数组的字面量是方括号 [ ] 
  - 声明数组并赋值称为数组的初始化
  - 这种字面量方式也是我们以后最多使用的方式

- 数组元素的类型

  数组中可以存放任意类型的数据，例如字符串，数字，布尔值等。

  ```js
  var arrStus = ['小白',12,true,28.9];
  
  var week = ["星期一","星期二",3];  //允许，但是一般不这么做
  var week = ["星期一","星期二","星期三"]; //我一般这么做***
  ```

- **总结**：

  - 普通变量： 1:1   (一个变量名对应一个数据)
  - 数组变量： 1:n   (一个数组对应多个数据)


### 1.3 获取数组中的元素

- **索引** (下标) ：**用来访问数组元素的序号**（数组下标从 0 开始）
- 如下图：

![](images\图片1.png)

- 数组可以通过索引来访问、设置、修改对应的数组元素
- 可以通过“**数组名[索引]**”的形式来获取数组中的元素
- 获取元素如下：

```js
// 定义数组
var arrStus = [1,2,3];
// 获取数组中的第2个元素
alert(arrStus[1]);    
```

**注意**：如果访问时数组没有和索引值对应的元素，则得到的值是undefined

- 课堂练习：

```js
var week = ["星期一","星期二","星期三","星期四","星期五","星期六","星期日"];
console.log(week[6])
console.log(week[0])
console.log(week[1])
```

**补充**： 数组内部存储数据的形式：

```js
var  dogs = ['小白','小黑','大黄','rui奇'];
var  dogs = [0:'小白',1:'小黑',2:'大黄',3:'rui奇'];   //（key:value ，键值对，索引键，数据值）
凡是，存储的数据结构为键值对，都是通过键操作值。 ***
通过索引来操作数组的元素。  ***
操作:
1. 获取：var dog0 = dogs[0]; 
2. 新增/修改： dogs[索引] = 值
```

### 1.4 遍历数组

#### 1.4.1 遍历

- 数组遍历：把数组中的每个元素从头到尾都访问一次（类似学生的点名）

- 可以通过 for 循环索引遍历数组中的每一项

- 代码如下：

  ```js
  var arr = ['red','green', 'blue'];
  for(var i = 0; i < arr.length; i++){//注意：i从0开始(只要是遍历数组，一般都是从0开始)
      console.log(arrStus[i]);
  }
  ```

- 课堂练习：

  ```js
  var heros = ["关羽","张飞","马超","赵云","黄忠","刘备","姜维"];
  for(var i = 0 ; i < 7 ; i++){
      console.log(heros[i]);
  }
  ```

#### 1.4.2 数组的长度

- 数组的长度：默认情况下表示数组中元素的个数

- 使用“**数组名.length**”可以访问数组元素的数量（数组长度）

  ```js
  var arrStus = [1,2,3];
  alert(arrStus.length);  // 3
  ```

-   **注意**：
  - **此处数组的长度是数组元素的个数 ，不要和数组的索引号混淆**
  - 当我们数组里面的元素个数发生了变化，这个 length 属性跟着一起变化
  - 数组的length属性可以被修改： （这个不需要记忆，一般不会修改length属性，只用于获取）
    - 如果设置的length属性值大于数组的元素个数，则会在数组末尾出现空白元素；
    - 如果设置的length属性值小于数组的元素个数，则会把超过该值的数组元素删除

- 遍历数组的固定写法 ***

  ```js
  for (var i = 0; i < arr.length; i++) {
  	console.log(arr[i]);
  }
  
  for (var i = 0; i <= arr.length - 1; i++) {
  	console.log(arr[i]);
  }
  ```

- 与字符串的length对比

  ```js
  //字符串其实也是一个数组
  var str = 'abc';  //字符串，字符集合，字符数组。 var str_array = ['a','b','c'] ; //str_array.length
  //str.length
  
  var arrStus = [1,2,3];
  alert(arrStus.length);  
  
  //数组的长度： 元素的个数
  //字符串的长度：字符的个数
  ```

### 1.5 数组案例

#### 1.5.1 06-计算数组的和以及平均值

```js
// 1. 求数组 [2,6,1,7, 4] 里面所有元素的和以及平均值。
// (1)声明一个求和变量 sum。
// (2)遍历这个数组，把里面每个数组元素加到 sum 里面。
// (3)用求和变量 sum 除以数组的长度就可以得到数组的平均值。
var arr = [2, 6, 1, 7, 4];
var sum = 0;
var average = 0;
for (var i = 0; i < arr.length; i++) {
    sum += arr[i]; // 我们加的是数组元素 arr[i] 不是计数器 i
}
average = sum / arr.length;
console.log(sum, average); // 想要输出多个变量，用逗号分隔即可
```

#### 1.5.2 07-求数组中的最大值

```js
// 求数组[2,6,1,77,52,25,7]中的最大值
// 声明一个保存最大元素的变量 max。
// 默认最大值可以取数组中的第一个元素。
// 遍历这个数组，把里面每个数组元素和 max 相比较。
// 如果这个数组元素大于max 就把这个数组元素存到 max 里面，否则继续下一轮比较。
// 最后输出这个 max
var arr = [2, 6, 1, 77, 52, 25, 7, 99];
var max = arr[0];
for (var i = 1; i < arr.length; i++) {
    if (arr[i] > max) {
        max = arr[i];
    }
}
console.log('该数组里面的最大值是：' + max);
```

**注意**：一般如果是number变量那么初始值为0，1。

​            如果是string变量那么初始值为""，空字符串。

​	    但是这个题目比较特殊，将第一个元素作为初始值。

#### 1.5.3 08-数组转换为字符串

```js
// 将数组 ['red', 'green', 'blue', 'pink'] 转换为字符串，并且用 | 或其他符号分割
// 1.需要一个新变量用于存放转换完的字符串 str。
// 2.遍历原来的数组，分别把里面数据取出来，加到字符串里面。
// 3.同时在后面多加一个分隔符
var arr = ['red', 'green', 'blue', 'pink'];
var str = '';
var sep = '*';//可以不用提取这个变量，但是分隔符可能会变化，那么我们习惯用变量来表示经常变化的内容。
for (var i = 0; i < arr.length; i++) {
    str += arr[i] + sep;
}
console.log(str);
```

### 1.5 数组中新增元素

- 数组中可以通过以下方式在数组的末尾插入新元素：

- 语法：

  ```
    数组[ 数组.length ] = 新数据;
  ```

- 例子：

  ```js
  var arr = ['red', 'green', 'blue', 'pink'];
  arr[4] = 'hotpink';//新索引，就是新增元素
  arr[0] = 'yellow';//老索引，就是修改元素
  console.log(arr);
  ```

### 1.7数组案例

#### 1.7.1 10-数组存放1~10个值

```js
// 新建一个数组，里面存放10个整数（ 1~10）
// 核心原理：使用循环来追加数组。
// 1、声明一个空数组 arr。
// 2、循环中的计数器 i  可以作为数组元素存入。
// 3、由于数组的索引号是从0开始的， 因此计数器从 0 开始更合适，存入的数组元素要+1。
var arr = [];
for (var i = 0; i < 100; i++) {
    // arr = i; 不要直接给数组名赋值 否则以前的元素都没了
    arr[i] = i + 1;
}
console.log(arr);
```

#### 1.7.2 11-筛选数组方法1

```js
// 将数组 [2, 0, 6, 1, 77, 0, 52, 0, 25, 7] 中大于等于 10 的元素选出来，放入新数组。
// 1、声明一个新的数组用于存放新数据newArr。
// 2、遍历原来的旧数组， 找出大于等于 10 的元素。
// 3、依次追加给新数组 newArr。
// 方法1
var arr = [2, 0, 6, 1, 77, 0, 52, 0, 25, 7];
var newArr = [];
var j = 0;
for (var i = 0; i < arr.length; i++) {
    if (arr[i] >= 10) {
        // 新数组索引号应该从0开始 依次递增
        newArr[j] = arr[i];
        j++;
    }
}
console.log(newArr);
```

#### 1.7.3 12-筛选数组方法2

```js
// 方法2 
var arr = [2, 0, 6, 1, 77, 0, 52, 0, 25, 7];
var newArr = [];
// 刚开始 newArr.length 就是 0
for (var i = 0; i < arr.length; i++) {
    if (arr[i] >= 10) {
        // 新数组索引号应该从0开始 依次递增
        newArr[newArr.length] = arr[i];// 给数组连续追加元素的固定写法 ***
    }
}
console.log(newArr);
```

**总结**：

```js
此题重点，大家需要会通过arr[arr.length]=新元素，来动态给数组添加元素。***  （连续追加元素）
	
    length总比数组中最大索引大1  ，那么arr.length就可以当做这个数组的新索引 ***


var arr = ['red', 'green', 'blue', 'pink'];
//不使用length
arr[4] = 'hotpink';//['red', 'green', 'blue', 'pink','hotpink'];
arr[5] = 'hotpink2';//['red', 'green', 'blue', 'pink','hotpink','hotpink2'];
arr[数组的最新索引] = 新元素;// 给数组连续追加元素的语法
//使用length
arr[arr.length] = 'hotpink'; // arr[4] = 'hotpink';  // ['red', 'green', 'blue', 'pink' ,'hotpink'];`
arr[arr.length] = 'hotpink2'; //arr[5] = 'hotpink2'; // ['red', 'green', 'blue', 'pink' ,'hotpink','hotpink2'];
```

#### 1.7.4 13-删除数组指定元素(数组去重）

```js
// 将数组[2, 0, 6, 1, 77, 0, 52, 0, 25, 7]中的 0 去掉后，形成一个不包含 0 的新数组。
// 1、需要一个新数组用于存放筛选之后的数据。
// 2、遍历原来的数组， 把不是 0 的数据添加到新数组里面(此时要注意采用数组名 + 索引的格式接收数据)。
// 3、新数组里面的个数， 用 length 不断累加。
var arr = [2, 0, 6, 1, 77, 0, 52, 0, 25, 7];
var newArr = [];
for (var i = 0; i < arr.length; i++) {
    if (arr[i] != 0) {
        newArr[newArr.length] = arr[i];
    }
}
console.log(newArr);
```

#### 1.7.5 14-翻转数组

```js
// 将数组 ['red', 'green', 'blue', 'pink', 'purple'] 的内容反过来存放
// 1、声明一个新数组 newArr
// 2、把旧数组索引号第4个取过来（arr.length - 1)，给新数组索引号第0个元素 (newArr.length)
// 3、我们采取 递减的方式  i--
var arr = ['red', 'green', 'blue', 'pink', 'purple', 'hotpink'];
var newArr = [];
for (var i = arr.length - 1; i >= 0; i--) {
    newArr[newArr.length] = arr[i]
}
console.log(newArr);
//其实老师的思路稍微有点饶了，代码没问题，就是思路饶了，以下是新思路
//1.倒序输出数组
//2.倒序输出的元素，连续追加到新数组中
var arr = ['red', 'green', 'blue', 'pink', 'purple', 'hotpink'];
var newArr = [];
for (var i = arr.length - 1; i >= 0; i--) {
    //1.倒序输出数组
    //console.log(arr[i]);
    //2.倒序输出的元素，连续追加到新数组中
    newArr[newArr.length] = arr[i]
}
console.log(newArr);
```

#### 1.7.6 15-复习交换两个变量值

```js
// 交换两个变量
var num1 = 'pink';
var num2 = 'yellow';
var temp;
temp = num1;
num1 = num2;
num2 = temp;
console.log(num1, num2);
```

#### 1.7.7 16-冒泡排序原理

1.冒泡排序：是一种算法，把一系列的数据按照一定的顺序进行排列显示(从小到大或从大到小）。

#### 1.7.8 17-冒泡排序

```js
// 冒泡排序 --- 视频代码内外循环条件不应该带等号
// var arr = [5, 4, 3, 2, 1];
var arr = [4, 1, 2, 3, 5];
for (var i = 0; i < arr.length - 1; i++) { // 外层循环管趟数 
    for (var j = 0; j < arr.length - i - 1; j++) { // 里面的循环管 每一趟的交换次数
        // 内部交换2个变量的值 前一个和后面一个数组元素相比较
        if (arr[j] < arr[j + 1]) {
            var temp = arr[j];
            arr[j] = arr[j + 1];
            arr[j + 1] = temp;
        }

    }
}
console.log(arr);
```

分析图：

![](images\冒泡排序分析.png)

## 2 函数 ***

### 2.1 函数的概念

- 在 JS 里面，可能会定义非常多的相同代码或者功能相似的代码，这些代码可能需要大量重复使用
- 虽然 for循环语句也能实现一些简单的重复操作，但是比较具有局限性，此时我们就可以使用 JS 中的函数
  - 后边我们会对比for循环和函数的相同与不同
- 函数：就是**封装了一段可被重复调用执行的代码块**。通过此代码块可以**实现大量代码的重复使用** 
- 方法：实现了某个功能的一段代码
  - alert()：将内容以对话框的形式弹出到界面上
  - 函数就是方法，都可以理解为一个工具


### 2.2 函数的使用

使用步骤：声明函数和调用函数

#### 2.2.1 声明函数

- 语法如下：

```js
// 声明函数
function 函数名() {
    //函数体代码
}
```

- function 是声明函数的关键字,必须小写
- function：功能，方法，函数
- **注意**：由于函数一般是为了实现某个功能才定义的， 所以通常我们将函数名命名为**动词**，比如 getSum
- 例子：

```js
function sayHi() {
    console.log('hi~~');
}
```

#### 2.2.2 调用函数

- 语法如下：

```js
// 调用函数
函数名(); 
```

- 调用的时候千万不要忘记添加小括号

- **注意**：声明函数本身并不会执行代码，只有调用函数时才会执行函数体代码。

- **口诀**：**函数不调用，自己不执行**

- 例子：

  ```js
  function sayHi() {
      console.log('hi~~');
  }
  sayHi();
  ```

### 2.3 函数的封装

- 函数的封装是**把一个或者多个功能通过函数的方式封装起来**，**对外只提供一个简单的函数接口**

- 简单理解：封装类似于将电脑配件整合组装到机箱中 ( **类似快递打包**）  

  ![](images\图片2.png)

- **再理解**：函数将功能封装好，调用者不用关心里边是如何实现的，只管使用。比如alert()。

- 例子：封装计算1-100累加和

  ```js
  /* 
     计算1-100之间值的函数
  */
  // 声明函数
  function getSum(){
    var sumNum = 0;// 准备一个变量，保存数字和
    for (var i = 1; i <= 100; i++) {
      sumNum += i;// 把每个数值 都累加 到变量中
    }
    alert(sumNum);
  }
  // 调用函数
  getSum();
  ```

### 2.4 函数的参数

#### 2.4.1 函数参数语法

- 在声明函数时，可以在函数名称后面的小括号中添加一些参数，这些参数被称为形参
- 而在调用该函数时，同样也需要传递相应的参数，这些参数被称为实参

- 形参：函数定义时设置的未知参数

- 实参：函数调用时传入的真实数据

  ![](images\图片3.png)

- 参数的作用 : 在函数内部某些值不能固定，我们可以通过参数在调用函数时传递不同的值进去

  - **参数作用理解**：将函数写死内容写活，让函数功能更加强大，更加灵活 ***

- 函数参数的语法：

  ```js
  // 带参数的函数声明
  function 函数名(形参1, 形参2 , 形参3...) { // 可以定义任意多的参数，用逗号分隔
    // 函数体
  }
  // 带参数的函数调用
  函数名(实参1, 实参2, 实参3...); 
  ```

  1. 函数调用的时候实参值会传递给形参
  2. 形参简单理解为：不用声明的变量

- 例子：

  ```js
  // 字符串与变量拼接
  var str = '今年我18岁了';
  var age = 18;
  var str = '今年我'+age+'岁了';
  
  //写死的函数
  function cook() {
      console.log('酸辣土豆丝');
  }	
  //通过参数写活的函数
  function cook(aru) { //形参：相当于声明了一个变量：var aru;   ***
      console.log(aru);
  }
  cook('酸辣土豆丝');//实参，相当于给变量赋值：aru='酸辣土豆丝' ***
  cook('大肘子');
  var aru = '烩面'
  cook(aru);
  ```

  aru/arg：argument，参数

#### 2.4.2 案例-利用函数求任意两个数的和以及累加和

```js
// 1. 利用函数求任意两个数的和
function getSum(num1, num2) {
    console.log(num1 + num2);
}
getSum(1, 3);
getSum(3, 8);
// 2. 利用函数求任意两个数之间的和
function getSums(start, end) {
    var sum = 0;
    for (var i = start; i <= end; i++) {
        sum += i;
    }
    console.log(sum);
}
getSums(1, 100);
getSums(1, 10);
// 3. 注意点
// (1) 多个参数之间用逗号隔开
// (2) 形参可以看做是不用声明的变量
```

**补充**：

如何根据题目需求，确定参数？  ***

​	分析题目中的不确定因素，**一个不确定因素就是一个参数**

#### 2.4.3 函数形参和实参数量不匹配时 （不用记）

![](images\图片4.png)

小结：

-  注意：在JavaScript中，形参的默认值是undefined（形参其实就是变量，所以跟变量默认值一样）
-  函数可以带参数也可以不带参数
-  声明函数的时候，函数名括号里面的是形参，形参的默认值为 undefined
-  调用函数的时候，函数名括号里面的是实参
-  多个参数中间用逗号分隔
-  形参的个数可以和实参个数不匹配，但是结果不可预计，我们尽量要匹配
-  **注意：这个不用记，因为一般函数定义几个形参，调用就会传到几个实参**

### 2.5 函数与for循环对比

函数与for循环：

- for循环： **避免重复代码的书写**，将重复代码（循环体）**连续不间断**的执行  （for循环执行重复代码，是一瞬间立马执行完）
- 函数：**避免重复代码的书写**，将重复代码（函数体），**可以间断调用**（放到一个公用的js文件中，很多html都可以使用）  （**只有调用才会执行**） 

### 2.6 函数的返回值

#### 2.6.1 return 语句

- 有的时候，我们会希望函数将值返回给调用者，此时通过使用 return 语句就可以实现

- 语法：

  ```js
  // 声明函数
  function 函数名（）{
      ...
      return  需要返回的值；
  }
  // 调用函数
  函数名();    // 此时调用函数就可以得到函数体内return 后面的值
  ```

- 在使用 return 语句时，函数会停止执行，并返回指定的值

- 如果函数没有 return ，默认返回的值是 undefined

- **return的作用**：将函数写死内容写活，让函数功能更加强大，更加灵活 ***

- 例子

  ```js
  function getResult() {
      return 666;
  }
  getResult(); // getResult()   = 666
  console.log(getResult());
  
  function cook(aru) {
      // 买肘子
      // 准备
      return aru;
  }
  // 传递一个菜名，cook方法执行完了之后，返回的是一盘做好的大肘子
  console.log(cook('大肘子'));
  // console.log('大肘子');
  // 4. 求任意两个数的和
  function getSum(num1, num2) {
      return num1 + num2;
  }
  //函数调用分为两步执行  ***
  // (1) 函数体代码执行
  // (2) 函数的返回值放到调用的位置
  console.log(getSum(1, 2)); // 调用函数相当于调用了函数的返回值
  //最后相当于以下代码：
  console.log(3);
  ```

- return特性：（这个视频在后边：28-return终止函数并且只能返回一个值-----29-函数返回值2个注意事项）

  ```js
  1.return 语句之后的代码不被执行。
  
  function add(num1，num2){
      //函数体
      return num1 + num2; // 注意：return 后的代码不执行
      alert('我不会被执行，因为前面有 return');
  }
  var resNum = add(21,6); // 调用函数，传入两个实参，并通过 resNum 接收函数返回值
  alert(resNum);          // 27
  
  2. return 只能返回一个值。如果用逗号隔开多个值，以最后一个为准。
  
  function add(num1，num2){
      //函数体
      return num1，num2;
  
  }
  var resNum = add(21,6); // 调用函数，传入两个实参，并通过 resNum 接收函数返回值
  alert(resNum);          // 6
  
  // 3.  我们求任意两个数的 加减乘数结果
  function getResult(num1, num2) {
      return [num1 + num2, num1 - num2, num1 * num2, num1 / num2];
  }
  var re = getResult(1, 2); // 返回的是一个数组
  console.log(re);
  // 4. 我们的函数如果有return 则返回的是 return 后面的值，如果函数么有 return 则返回undefined
  function fun1() {
      return 666;
  }
  console.log(fun1()); // 返回 666
  function fun2() {
  
  }
  console.log(fun2()); // 函数返回的结果是 undefined
  
  ```

#### 2.6.2 break ,continue ,return 的区别

- break ：结束当前的循环体（如 for、while）
- continue ：跳出本次循环，继续执行下次循环（如 for、while）
- return ：不仅可以退出循环，还能够返回 return 语句中的值，同时还可以结束当前的函数体内的代码

### 2.7 函数总结***

我们现在再从头给案例过一遍，进而理解一下函数的参数和返回值

#### 2.7.1 没有参数，没有返回值

```js
function getSums() {
    var sum = 0;
    for (var i = 1; i <= 100; i++) {
        sum += i;
    }
    console.log(sum);

}
getSums();
function getSums2() {
    var sum = 0;
    for (var i = 1; i <= 1000; i++) {
        sum += i;
    }
    console.log(sum);

}
function getSums3() {
    var sum = 0;
    for (var i = 5; i <= 50; i++) {
        sum += i;
    }
    console.log(sum);

}
```

#### 2.7.2 有参数 

```js
function getSums(start, end) {
    // 我们自己判断谁大谁小
    var sum = 0;
    for (var i = start; i <= end; i++) {
        sum += i;
    }
    console.log(sum);
    // return undefined;
}
getSums(1,100); // 输出5050  ,返回undefined
//但是如果需求要将结果弹出，怎么办？
function getSums(start, end) {
    var sum = 0;
    for (var i = start; i <= end; i++) {
        sum += i;
    }
    alert(sum);
    // return undefined;
}
getSums(1,100);// 弹出5050,返回undefined
//那如果需求要将结果参与后续运算，怎么办？再定义方法？显而有点不现实。
//结论：参数让当前函数更加灵活，更加强大，但是没有返回值，发现函数还是功能单一
```

#### 2.7.3 有参数，有返回值

```js
function getSums(start, end) {
    var sum = 0;
    for (var i = start; i <= end; i++) {
        sum += i;
    }
    return sum;
}
var result = geSums(1,100);//5050
console.log(result);//可以打印
alert(result);//可以弹出
result + 10 //可以参与后续运算
//返回值的作用与参数作用类似，让当前函数更加灵活，更加强大
```

#### 2.7.4 返回值的理解 ***

```js
function getSums(start, end) {
    var sum = 0;
    for (var i = start; i <= end; i++) {
        sum += i;
    }
    return sum;
} 
var result = geSums(1,100); // 调用函数，相当于直接调用返回值  
//(函数调用时，会做两件事情：1.执行函数的代码 2.会将返回值返回 （返回值替换到原来调用位置）) 
//所以上述代码相当于 var result = sum;
console.log(result);
```
#### 2.7.5 函数理解与使用步骤

- 函数： 封装了一个带有功能性的代码，并将结果返回。
- 如何根据一个需求，编写函数

```js
	需求： 计算n-m之间的和。
		  如何编写一个函数：  ********
            1. 确定函数名   : getSum 
            2. 确定参数 ： 只要有一个不确定的因素，都可以变成一个参数  : n , m
            3. 确定返回值  ： 运算结果(根据需求判断是否需要返回结果)
```

#### 2.7.6 什么情况下要添加返回值？

```js
//什么情况下要添加返回值？
//没有明确说明要把返回值如何处理，那就都需要添加返回值。  （大部分情况都是有返回值的）
//如果，明确说明，将结果弹出，这时候就不需要添加返回值。

// 就是弹出对话框，不需要返回
alert('今年5岁了');  //没有返回值，默认返回 undefined
//接收用户的输入，返回用户输入的内容
prompt('请输入内容')  //输入5 ， 返回输入内容5
```

### 2.8 函数案例

#### 2.8.1 26-利用函数求两个数的最大值

```js
// 利用函数 求两个数的最大值
function getMax(num1, num2) {
    // if (num1 > num2) {
    //     return num1;
    // } else {
    //     return num2;
    // }
    return num1 > num2 ? num1 : num2;
}
console.log(getMax(1, 3));
console.log(getMax(11, 3));
```

#### 2.8.2 27-利用函数求数组中的最大值

```js
 // 利用函数求数组 [5,2,99,101,67,77] 中的最大数值。
function getArrMax(arr) { // arr 接受一个数组  arr =  [5,2,99,101,67,77]
    var max = arr[0];
    for (var i = 1; i <= arr.length; i++) {
        if (arr[i] > max) {
            max = arr[i];
        }
    }
    return max;
}
// getArrMax([5, 2, 99, 101, 67, 77]); // 实参是一个数组送过去
// 在我们实际开发里面，我们经常用一个变量来接受 函数的返回结果 使用更简单
// var re = getArrMax([5, 2, 99, 101, 67, 77]);
var re = getArrMax([3, 77, 44, 99, 143]);
console.log(re);
```

### 2.9 arguments的使用

#### 2.9.1 介绍

1. 在 JavaScript 中，arguments 实际上它是当前函数的一个内置对象。

2. 当我们不确定有多少个参数传递的时候，可以用 arguments 来获取。所有函数都内置了一个 arguments 对象，arguments 对象中存储了传递的所有实参。

3. arguments展示形式是一个伪数组，因此可以进行遍历。

4. 伪数组具有以下特点：

   - 具有 length 属性
   - 按索引方式储存数据
   	 不具有数组的 push , pop 等方法	

5. **总结**：

   	伪数组，数组都是有序集合 （集合：存储多个数据）
   	对象是无序集合

6. **arguments的应用场景**：我们的函数允许用户调用时，传递不定长（不确定个数）的参数，函数声明时，不会使用形参，而是使用arguments  ***

7. aruguments与形参

   参数个数固定时，依然使用形参，因为方便

   参数个数不固定时，可以使用arguments

#### 2.9.2 案例

```js
function getSums() {
    var sum = 0;
    var start = arguments[0];
    var end = arguments[1];
    //for (var i = arguments[0]; i <= arguments[1]; i++) {
    for (var i = start; i <= end; i++) {
        sum += i;
    }
    return sum;
}
getSums(1,100);

function fn() {
    // console.log(arguments); // 里面存储了所有传递过来的实参  arguments = [1,2,3]
    // console.log(arguments.length);
    // console.log(arguments[2]);
    // 我们可以按照数组的方式遍历arguments
    for (var i = 0; i < arguments.length; i++) {
        console.log(arguments[i]);

    }
}
fn(1, 2, 3);
fn(1, 2, 3, 4, 5);
```

#### 2.9.3 问题

```js
//1.console.log()内部是如何获取参数的？
console.log(1)
console.log(1,2)
function log(a,b,c,....){   // xxx

}
function log(){
    arguments[0] ---- 1
    arguments[1] ---- 2
}

//2. arguments能替代形参么？
//如果现在确定函数的参数有两个，你觉得使用哪种形式处理简单？arguments?还是形参？
function getSum(a,b){
    a
    b
}
function getSum(){
    arguments[0]
    arguments[1]
}
```

### 2.10 函数案例

#### 2.10.1 02-利用函数求任意个数的数的最大值

```js
// 利用函数求任意个数的最大值
function getMax() { // arguments = [1,2,3]
    var max = arguments[0];
    for (var i = 1; i < arguments.length; i++) {
        if (arguments[i] > max) {
            max = arguments[i];
        }
    }
    return max;
}
console.log(getMax(1, 2, 3));
console.log(getMax(1, 2, 3, 4, 5));
console.log(getMax(11, 2, 34, 444, 5, 100));
```

#### 2.10.2 03-利用函数翻转数组

```js
 // 利用函数翻转任意数组 reverse 翻转
function reverse(arr) {
    var newArr = [];
    for (var i = arr.length - 1; i >= 0; i--) {
        newArr[newArr.length] = arr[i];
    }
    return newArr;
}
var arr1 = reverse([1, 3, 4, 6, 9]);
console.log(arr1);
var arr2 = reverse(['red', 'pink', 'blue']);
console.log(arr2);
```

#### 2.10.3 04-函数封装冒泡排序

```js
// 利用函数冒泡排序 sort 排序
function sort(arr) {
    for (var i = 0; i < arr.length - 1; i++) {
        for (var j = 0; j < arr.length - i - 1; j++) {
            if (arr[j] > arr[j + 1]) {
                var temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
            }
        }
    }
    return arr;
}
var arr1 = sort([1, 4, 2, 9]);
console.log(arr1);
var arr2 = sort([11, 7, 22, 999]);
console.log(arr2);
```

#### 2.10.4 05-利用函数判断闰年

```js
// 利用函数判断闰年
function isRunYear(year) {
    // 如果是闰年我们返回 true  否则 返回 false 
    var flag = false;
    if (year % 4 == 0 && year % 100 != 0 || year % 400 == 0) {
        flag = true;
    }
    return flag;
}
console.log(isRunYear(2000));
console.log(isRunYear(1999));
```

#### 2.10.5 函数调用函数

- 函数可以相互调用

- 因为每个函数都是独立的代码块，用于完成特殊任务，因此经常会用到函数相互调用的情况

- 例子：

  ```js
  function fn1(param1,param2,arg1,arg2) {
      console.log(111);
      fn2();
      console.log('fn1');
  }
  function fn2() {
      console.log(222);
      console.log('fn2');
      //fn1();
  }
  fn1();
  		
  ```

- **注意点**：可以相互调用，但是不能 同时 相互调用，会形成死循环。 ***

- 案例：07-输出年份的2月份天数

  ```js
  // 用户输入年份，输出当前年份2月份的天数
  function backDay() {
      var year = prompt('请您输入年份:');
      // 调用函数需要加小括号
      if (isRunYear(year)) {//注意的写法相当于if(isRunYear(year) == true) 
          alert('当前年份是闰年2月份有29天');
      } else {
          alert('当前年份是平年2月份有28天');
      }
  }
  backDay();
  
  
  // 判断是否为闰年的函数
  function isRunYear(year) {
      // 如果是闰年我们返回 true  否则 返回 false 
      var flag = false;
      if (year % 4 == 0 && year % 100 != 0 || year % 400 == 0) {
          flag = true;
      }
      return flag;
  }
  ```


### 2.11 函数的两种声明方式

#### 2.11.1 自定义函数方式(命名函数)

- 利用函数关键字 function 自定义函数方式

  ```js
  // 声明定义方式
  function fn() {...}
  // 调用  
  fn(); 
  ```

- 因为有名字，所以也被称为命名函数

- 调用函数的代码既可以放到声明函数的前面，也可以放在声明函数的后面

  - 一般放到后边，先有了函数，再去使用函数，这才正常
  - 为啥可以在函数声明前调用，后边预解析解释

#### 2.11.2 函数表达式方式(匿名函数）

- 利用函数表达式方式的写法如下： 

  ```js
  // 这是函数表达式写法，匿名函数后面跟分号结束
  var fn = function(){...}；
  // 调用的方式，函数调用必须写到函数体下面
  fn();
  ```

- 因为函数没有名字，所以也被称为匿名函数

- 这个fn 里面存储的是一个函数  

- 函数表达式方式原理跟声明变量方式是一致的

- 函数调用的代码必须写到函数体后面

- 补充：
  - **应用场景**：在对象中声明函数时，使用函数表达式方式 ***
  - 命名函数： 有名字：fn
  - 匿名函数： 没有名字，有变量名fn


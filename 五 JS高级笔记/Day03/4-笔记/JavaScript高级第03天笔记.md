# JavaScript高级第03天笔记

## 1. 函数的定义和调用

### 1.1 函数的定义方式

（02-函数的定义方式.avi）

- 方式1： 函数声明方式 function 关键字 (命名函数)

   ```js
   function fn(){}
   ```

- 方式2： 函数表达式(匿名函数)

   ```js
   var fn = function(){}
   ```

- 方式3： new Function()  （函数也是对象，所以可以new）（了解）

   ```js
   var f = new Function('a', 'b', 'console.log(a + b)');
   f(1, 2);
   
   var fn = new Function('参数1','参数2'..., '函数体')
   ```

   注意：

   - Function 里面参数都必须是字符串格式
   - 第三种方式执行效率低，也不方便书写，因此较少使用
   - 所有函数都是 Function 的实例(对象)  
   - 函数也属于对象

### 1.2 函数的调用

（03-函数的调用方式.avi）

```js
/* 1. 普通函数 */
function fn() {
	console.log('人生的巅峰');
}
 fn(); 
/* 2. 对象的方法 */
var o = {
  sayHi: function() {
  	console.log('人生的巅峰');
  }
}
o.sayHi();
/* 3. 构造函数*/
function Star() {};
new Star();
/* 4. 绑定事件函数*/
 btn.onclick = function() {};   // 点击了按钮就可以调用这个函数
/* 5. 定时器函数*/
setInterval(function() {}, 1000);  这个函数是定时器自动1秒钟调用一次
/* 6. 立即执行函数(自调用函数)*/
(function() {
	console.log('人生的巅峰');
})();
```

## 2. this

（04-函数内部的this指向.avi）

### 2.1 函数内部的this指向

- 这些 this 的指向，是当我们调用函数的时候确定的
- 调用方式的不同决定了this 的指向不同
- 一般指向我们的调用者
- 总结如下：

![](images/img1.png)

代码：

```js
   <button>点击</button>
    <script>
        // 函数的不同调用方式决定了this 的指向不同
        // 1. 普通函数 this 指向window
        function fn() {
            console.log('普通函数的this' + this);
        }
        window.fn();
        // 2. 对象的方法 this指向的是对象 o
        var o = {
            sayHi: function() {
                console.log('对象方法的this:' + this);
            }
        }
        o.sayHi();
        // 3. 构造函数 this 指向 ldh 这个实例对象 原型对象里面的this 指向的也是 ldh这个实例对象
        function Star() {};
        Star.prototype.sing = function() {

        }
        var ldh = new Star();
        // 4. 绑定事件函数 this 指向的是函数的调用者 btn这个按钮对象
        var btn = document.querySelector('button');
        btn.onclick = function() {
            console.log('绑定时间函数的this:' + this);
        };
        // 5. 定时器函数 this 指向的也是window
        window.setTimeout(function() {
            console.log('定时器的this:' + this);

        }, 1000);
        // 6. 立即执行函数 this还是指向window
        (function() {
            console.log('立即执行函数的this' + this);
        })();
    </script>
```

### 2.2 改变函数内部 this 指向

改变函数内this指向  js提供了三种方法  call()  apply()  bind() 

#### 2.2.1 call方法

（05-call方法及其应用.avi）

- call()方法调用一个对象
- 简单理解为调用函数的方式，但是它可以改变函数的 this 指向
- 应用场景:  经常做继承
- call：打电话，在程序中有调用的意思
- 代码：

```js
var o = {
	name: 'andy'
}
 function fn(a, b) {
      console.log(this);
      console.log(a+b)
};
fn()// 此时的this指向的是window
fn.call(o,1,2)//此时的this指向的是对象o,参数使用逗号隔开

// call 第一个可以调用函数 第二个可以改变函数内的this 指向
// call 的主要作用可以实现继承
function Father(uname, age, sex) {
    this.uname = uname;
    this.age = age;
    this.sex = sex;
}

function Son(uname, age, sex) {
    Father.call(this, uname, age, sex);
}
var son = new Son('刘德华', 18, '男');
console.log(son);

```

#### 2.2.2 apply方法

（06-apply方法及其应用.avi）

- apply() 方法调用一个函数
- 简单理解为调用函数的方式，但是它可以改变函数的 this 指向
- 应用场景:  经常跟数组有关系
- apply：应用，运用
- 代码：

```js
var o = {
	name: 'andy'
}
 function fn(a, b) {
      console.log(this);
      console.log(a+b)
};
fn()// 此时的this指向的是window
fn.apply(o,[1,2])//此时的this指向的是对象o,参数使用数组传递
// 1. 也是调用函数 第二个可以改变函数内部的this指向
// 2. 但是他的参数必须是数组(伪数组)
// 3. apply 的主要应用 比如说我们可以利用 apply 借助于数学内置对象求数组最大值 
// ***4. apply将第二个参数的数组,进行了拆包,将拆出来的每个元素,作为实参传递进去
// Math.max();
var arr = [1, 66, 3, 99, 4];
var arr1 = ['red', 'pink'];
// var max = Math.max.apply(null, arr);//不需要改变this指向，写null
var max = Math.max.apply(Math, arr);//但是写null不太合适，写max的调用者Math最好
// 以上代码相当于:Math.max(1, 66, 3, 99, 4);
var min = Math.min.apply(Math, arr);
console.log(max, min);
//补充:
Math.max(1, 2); // max计算一组数中的最大值
Math.max(1, 2, 3);
```

#### 2.2.3 bind方法  ***

(07-bind方法基本使用.avi，08-bind方法应用.avi)

- bind() 方法不会调用函数，但是能改变函数内部this 指向，返回的是原函数改变this之后产生的新函数

- 如果只是想改变 this 指向，并且不想调用这个函数的时候，可以使用bind

- 应用场景：不调用函数，但是还想改变this指向
- bind：绑定
- 代码：

```js
 var o = {
 name: 'andy'
 };

function fn(a, b) {
	console.log(this);
	console.log(a + b);
};
//this指向的是对象o 参数使用逗号隔开
var f = fn.bind(o, 1, 2); //此处的f是bind返回的新函数
f();//调用新函数  
// 1. 不会调用原来的函数   可以改变原来函数内部的this 指向
// 2. 返回的是原函数改变this之后产生的新函数
// 3. 如果有的函数我们不需要立即调用,但是又想改变这个函数内部的this指向此时用bind
// 4. 我们有一个按钮,当我们点击了之后,就禁用这个按钮,3秒钟之后开启这个按钮
// var btn1 = document.querySelector('button');
// btn1.onclick = function() {
//     this.disabled = true; // 这个this 指向的是 btn 这个按钮
//     // var that = this;
//     setTimeout(function() {
//         // that.disabled = false; // 定时器函数里面的this 指向的是window
//         this.disabled = false; // 此时定时器函数里面的this 指向的是btn
//     }.bind(this), 3000); // 这个this 指向的是btn 这个对象
// }
var btns = document.querySelectorAll('button');
for (var i = 0; i < btns.length; i++) {
    btns[i].onclick = function() {
        this.disabled = true;
        setTimeout(function() {
            this.disabled = false;
        }.bind(this), 2000);
    }
}
```

#### 2.2.4 call、apply、bind三者的异同

(09-call和apply以及bind总结.avi)

- 共同点 : 都可以改变this指向
- 不同点:
  - call 和 apply  会调用函数, 并且改变函数内部this指向.
  - call 和 apply传递的参数不一样,call传递参数使用逗号隔开,apply使用数组传递
  - bind  不会调用函数, 可以改变函数内部this指向.


- 应用场景
  1. call 经常做继承. 
  2. apply经常跟数组有关系.  比如借助于数学对象实现数组最大值最小值
  3. bind  不调用函数,但是还想改变this指向. 比如改变定时器内部的this指向. 

## 3. 严格模式

(10-什么是严格模式以及如何开启严格模块.avi)

### 3.1 什么是严格模式

- JavaScript 除了提供正常模式外，还提供了**严格模式**（strict mode）。
- ES5 的严格模式是采用具有限制性 JavaScript变体的一种方式，即在严格的条件下运行 JS 代码。
- 严格模式在 IE10 以上版本的浏览器中才会被支持，旧版本浏览器中会被忽略。

- 严格模式对正常的 JavaScript 语义做了一些更改： 
  - 1.消除了 Javascript 语法的一些不合理、不严谨之处，减少了一些怪异行为。
  - 2.消除代码运行的一些不安全之处，保证代码运行的安全。
  - 3.提高编译器效率，增加运行速度。
  - 4.禁用了在 ECMAScript 的未来版本中可能会定义的一些语法，为未来新版本的 Javascript 做好铺垫。比如一些保留字如：class,enum,export, extends, import, super 不能做变量名

### 3.2 开启严格模式

严格模式可以应用到整个脚本或个别函数中。

因此在使用时，我们可以将严格模式分为为**脚本开启严格模式**和**为函数开启严格模式**两种情况。

- 情况一 ：为脚本开启严格模式

  - 有的 script 脚本是严格模式，有的 script 脚本是正常模式，这样不利于文件合并，所以可以将整个脚本文件放在一个立即执行的匿名函数之中。这样独立创建一个作用域而不影响其他
    script 脚本文件。

    ```js
    (function (){
      //在当前的这个自调用函数中有开启严格模式，当前函数之外还是普通模式
    　　　　"use strict";//use使用，strict严格。使用严格模式
           var num = 10;
    　　　　function fn() {}
    })();
    //或者 
    <script>
      　"use strict"; //当前script标签开启了严格模式
    </script>
    <script>
      			//当前script标签未开启严格模式
    </script>
    ```

- 情况二：为函数开启严格模式

  - 要给某个函数开启严格模式，需要把“use strict”;  (或 'use strict'; ) 声明放在函数体所有语句之前。

    ```js
    function fn(){
    　　"use strict";//当前fn函数开启了严格模式
    　　return "123";
    } 
    
    ```

### 3.3 严格模式中的变化

（11-严格模式的变化.avi）

严格模式对 Javascript 的语法和行为，都做了一些改变。

1. 变量规定 

   ① 在正常模式中，如果一个变量没有声明就赋值，默认是全局变量。严格模式禁止这种用法，变量都必须先用 

   var 命令声明，然后再使用。 

   ② 严禁删除已经声明变量。例如，delete x; 语法是错误的。

2. 严格模式下 this 指向问题 

   ① 以前在全局作用域函数中的 this 指向 window 对象。 

   ② **严格模式下全局作用域中函数中的 this 是 undefined。** 

   ③ 以前构造函数时不加 new也可以 调用,当普通函数，this 指向全局对象 

   ④ 严格模式下,如果 构造函数不加new调用, this 指向的是undefined 如果给他赋值则 会报错 

   ⑤ new 实例化的构造函数指向创建的对象实例。 

   ⑥ 定时器 this 还是指向 window 。 

   ⑦ 事件、对象还是指向调用者。

代码：

```js
<script>
    'use strict';
    // 1. 我们的变量名必须先声明再使用
    // num = 10;
    // console.log(num);
    var num = 10;
    console.log(num);
    // 2.我们不能随意删除已经声明好的变量
    // delete num;
    // 3. 严格模式下全局作用域中函数中的 this 是 undefined。
    // function fn() {
    //     console.log(this); // undefined。

    // }
    // fn();
    // 4. 严格模式下,如果 构造函数不加new调用, this 指向的是undefined 如果给他赋值则 会报错.
    // function Star() {
    //     this.sex = '男';
    // }
    // // Star();
    // var ldh = new Star();
    // console.log(ldh.sex);
    // 5. 定时器 this 还是指向 window 
    // setTimeout(function() {
    //     console.log(this);

    // }, 2000);
    // a = 1;
    // a = 2;
    // 6. 严格模式下函数里面的参数不允许有重名
    // function fn(a, a) {
    //     console.log(a + a);

    // };
    // fn(1, 2);
    function fn() {}
</script>
```

[更多严格模式要求参考](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Strict_mode)

## 4. 高阶函数 ***

（12-高阶函数.avi）

**高阶函数**是**对其他函数进行操作的函数**，它**接收函数作为参数**或**将函数作为返回值输出**

如下：

![](images/img2.png)

- 此时fn 就是一个高阶函数

- 函数也是一种数据类型，同样可以作为参数，传递给另外一个参数使用。最典型的就是作为回调函数。

- 同理函数也可以作为返回值传递回来


## 5. 闭包 ***

（13-什么是闭包.avi）

### 5.1 变量的作用域复习

变量根据作用域的不同分为两种：全局变量和局部变量

1. 函数内部可以使用全局变量
2. 函数外部不可以使用局部变量
3. 当函数执行完毕，本作用域内的局部变量会销毁

### 5.2 什么是闭包

- 闭包（closure）指**有权访问另一个函数作用域中变量的函数**
- 简单理解就是 ，一个作用域可以访问另外一个函数内部的局部变量

![](images/img3.png)

如上述代码，**理解闭包**：**fn2内部是一个作用域，那么fn2访问了另一个函数内部的局部变量，那么这个局部变量所在函数就叫做闭包函数，所以此时fn1就是闭包函数**。

闭包形成的两个关键点：

1. 函数嵌套
2. 内部函数使用外部函数的局部变量（将外部函数称之为闭包函数）

### 5.3 闭包的作用

（14-闭包的作用.avi）

作用：**延伸变量的作用范围**。（使得fn外部的作用域访问num）

```js
 function fn() {
   var num = 10;
   function fun() {
       console.log(num);
 	}
    return fun;//将内部函数返回，不调用
 }
var f = fn();//fn调用完毕，正常理解num就需要消耗，但是fn如果是一个闭包函数，就不会消耗，因为fun要使用，只用fun调用完毕才消耗
f();//调用内部函数fun，打印num，此时就是在fn外部访问了num
```

### 5.4 闭包的案例

1. 闭包应用——利用闭包的方式得到当前li 的索引号

```js
for (var i = 0; i < lis.length; i++) {
// 利用for循环创建了4个立即执行函数
// 立即执行函数也成为小闭包，因为立即执行函数里面的任何一个函数都可以使用它的i这变量
(function(i) {
    lis[i].onclick = function() {
      console.log(i);
    }
 })(i);
}
//理解：
//for循环创建了四个立即执行函数，每个立即执行函数都有一个局部变量i，并且值不一样，是0,1,2,3
//当我们点击li的时候，li的onclick执行，内部要访问i，此时就访问到它所在的立即执行函数的局部变量i
```

2. 闭包应用——3秒钟之后,打印所有li元素的内容

```js
 for (var i = 0; i < lis.length; i++) {
   (function(i) {
     setTimeout(function() {
     	console.log(lis[i].innerHTML);//理解：i访问的是立即执行函数的局部变量i
     }, 3000)
   })(i);
}
```

3. 闭包应用——计算打车价格 

   需求分析：

   - 打车起步价13(3公里内)，之后每多一公里增加 5块钱

   - 用户输入公里数就可以计算打车价格

   - 如果有拥堵情况，总价格多收取10块钱拥堵费

```js
 var car = (function() {
     var start = 13; // 起步价  局部变量
     var total = 0; // 总价  局部变量
     return {
       // 正常的总价
       price: function(n) {
         if (n <= 3) {
           total = start;
         } else {
           total = start + (n - 3) * 5
         }
         return total;
       },
       // 拥堵之后的费用
       yd: function(flag) {
         return flag ? total + 10 : total;
       }
	}
 })();
console.log(car.price(5)); // 23
console.log(car.yd(true)); // 33
```

### 5.5 案例-思考题(选讲)

```js
 var name = "The Window";
   var object = {
     name: "My Object",
     getNameFunc: function() {
     return function() {
     return this.name;
     };
   }
 };
console.log(object.getNameFunc()())
-----------------------------------------------------------------------------------
var name = "The Window";　　
  var object = {　　　　
    name: "My Object",
    getNameFunc: function() {
    var that = this;
    return function() {
    return that.name;
    };
  }
};
console.log(object.getNameFunc()())
       
```

## 6. 递归

### 6.1 什么是递归

- **递归：**如果**一个函数在内部可以调用其本身**，那么这个函数就是递归函数
- 简单理解：**函数内部自己调用自己**，这个函数就是递归函数
- **注意：**递归函数的作用和循环效果一样
- 由于递归很容易发生“栈溢出”错误（stack overflow），所以**必须要加退出条件return**
- 代码：

```js
var num = 1;

function fn() {
    console.log('我要打印6句话');

    if (num == 6) {
        return; // 递归里面必须加退出条件
    }
    num++;
    fn();//fn自己调用自己，fn就是递归函数
}
fn();
```



### 6.2 利用递归求1~n的阶乘

n的阶乘：1到n之间所有数相乘，就是n的阶乘。

```js
//利用递归函数求1~n的阶乘 1 * 2 * 3 * 4 * ..n
 function fn(n) {
     if (n == 1) { //结束条件
       return 1;
     }
     return n * fn(n - 1);
 }
 console.log(fn(3));
//详细思路 以3为例
//return  3 * fn(2)
//return  3 * (2 * fn(1))
//return  3 * (2 * 1)
//return  3 * (2)
//return  6
```

### 6.3 利用递归求斐波那契数列

斐波那契数列介绍：

![](images\fb.jpg)

```js
// 利用递归函数求斐波那契数列(兔子序列)  1、1、2、3、5、8、13、21...
// 用户输入一个数字 n 就可以求出 这个数字对应的兔子序列值
// 我们只需要知道用户输入的n 的前面两项(n-1 n-2)就可以计算出n 对应的序列值
function fb(n) {
  if (n === 1 || n === 2) {
        return 1;
  }
  return fb(n - 1) + fb(n - 2);
}
console.log(fb(3));
```

### 6.4 利用递归遍历数据

```js
    <script>
        var data = [{
            id: 1,
            name: '家电',
            goods: [{
                id: 11,
                gname: '冰箱',
                goods: [{
                        id: 111,
                        gname: '海尔'
                    }, {
                        id: 112,
                        gname: '美的'
                    },

                ]

            }, {
                id: 12,
                gname: '洗衣机'
            }]
        }, {
            id: 2,
            name: '服饰'
        }];
        // 我们想要做输入id号,就可以返回的数据对象
        // 1. 利用 forEach 去遍历里面的每一个对象
        function getID(json, id) {
            var o = {};
            json.forEach(function(item) {
                // console.log(item); // 2个数组元素
                if (item.id == id) {
                    // console.log(item);
                    o = item;
                    return o;
                    // 2. 我们想要得里层的数据 11 12 可以利用递归函数
                    // 里面应该有goods这个数组并且数组的长度不为 0 
                } else if (item.goods && item.goods.length > 0) {
                    o = getID(item.goods, id);
                }


            });
            return o;
        }
        console.log(getID(data, 1));
        console.log(getID(data, 2));
        console.log(getID(data, 11));
        console.log(getID(data, 12));
        console.log(getID(data, 111));
    </script>
```

